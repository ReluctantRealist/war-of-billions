# Technical Design

The galaxy is simulated to a realistic scale, so many billions of systems.

It is generated in a way similar to No Man's Sky, with a mathematical seed creating a static coordinate system for stars and anomalies.

The player will be "blind" until they spend Compute on Intel, so the "billions of systems" exist as empty placeholders until the player experience requires data.

Stars do not move in the first version of the game.

---

## Platform: Electron

War of Billions ships as a native desktop application via **Electron**, wrapping the React + TypeScript frontend in a native shell. It is distributed on itch.io and Steam as a standard downloadable executable — not a browser game.

This decision is driven by simulation scale. A late-game empire with dozens of active systems, running at 100x tick speed, would strain browser resource constraints. Electron gives the game full access to the player's hardware:

- **Node.js `worker_threads`** — the simulation loop runs off the main thread entirely. React only receives state snapshots to render. The UI never freezes because tick processing never blocks the UI thread.
- **File system access** — save files are written to disk directly, with no localStorage size limits. Save files scale with player activity, not the galaxy.
- **Full CPU and RAM** — no browser sandbox restrictions on memory or thread count.

The React + TypeScript codebase is otherwise unchanged. Electron wraps it; it does not replace it.

---

## Remote System Simulation

Simulating every active system at full fidelity every tick is not necessary — and the game's own lore provides the justification for why not. The player already receives delayed information from remote systems. That light-speed delay is the abstraction layer. A system 500 light-years away reports what it was doing 500 years ago. The player cannot observe intermediate states. The engine does not need to produce them.

Three strategies combine to keep remote system simulation cheap:

### Event-Driven Ticking

Remote systems do not simulate every tick. Instead, the engine calculates the **next meaningful event** for each remote system — build complete, attack roll triggers, a scheduled transmission arrival — and jumps directly to it. Between events the system is frozen. A quiet remote system with no MOS contact and only routine replication may generate a handful of events per in-game century. It costs almost nothing to maintain.

The home system is the exception. It runs full tick-by-tick simulation because the player is present and watching.

### Aggregate Parameter Simulation

Remote systems do not track individual asset counts. They track **aggregate parameters**: total Compute generation rate, defensive strength rating, SRF replication rate, current Threat Level exposure, matter stockpile. Build queues add to parameters on completion; attacks subtract from them by a combat resolution formula. The Blueprint/Equivalent Exchange system already operates in parameters rather than unit counts, so this is a natural fit.

This collapses each remote system's simulation state to a small fixed set of numbers, regardless of how large the Swarm within it becomes.

### Simulate on Demand

When a transmission from a remote system is due to arrive, the engine calculates what happened during the elapsed interval using the aggregate parameters and any queued events, rather than replaying tick-by-tick. The output is the transmission content — resource report, attack outcome, build completion notice. The intermediate states are never computed and never needed.

---

## System Lifecycle

Every star system exists in one of three states:

- **Dormant** — seed-only. No save data. All properties (star type, resource distribution, anomalies, MOS presence probability) are derived deterministically from the galaxy seed and the system's coordinates. Costs nothing to store.
- **Waking** — a probe is in transit. The system does not yet exist in the save file. Its seed-derived properties are pre-calculated when the player views the probe's trajectory.
- **Active** — a probe has arrived and transmitted. The system is instantiated from its seed, timestamped with the in-game year of wake, and written to the save file. From this point it is simulated forward using the remote simulation strategies above (or full simulation if it is the home system).

### Wake Event

When a probe arrives at a Dormant system, it triggers a wake event:

1. System state is generated from seed (star, resources, anomalies, any pre-existing MOS infrastructure)
2. A wake timestamp is recorded (in-game year)
3. The probe's transmission is queued — it reaches the player after a delay equal to the light-travel time from that system
4. The player receives the transmission as an `EVT_` notification, potentially followed by `MSG_` comms if MOS is present

The player's intel is already out of date the moment it arrives. A system 200 light-years away sends a signal that takes 200 years to arrive — what the player sees is the system as it was, not as it is.

### MOS Presence

MOS presence in a system is determined by seed but treated as pre-existing history. If MOS is present at wake, the system generates with infrastructure and activity already in place — as though MOS arrived long before the probe. The player cannot know when MOS actually arrived; at interstellar distances, this is unknowable.

### Save File Scope

Only Active systems are written to the save file. Dormant systems are pure seed — they cost nothing. Save file size scales with player activity, not galaxy size.

---

## Save File Architecture

### Format and Compression

Save files are written to disk as compressed JSON. The save state is serialized with `JSON.stringify`, compressed with **pako** (a JavaScript zlib/gzip implementation), and written to disk via Electron's file system API. Decompression and parsing run on load. This keeps save files small even for large late-game empires without meaningful performance cost.

### Schema Versioning

Every save file includes a `save_version` field at the top level. On load, the engine checks the version and runs sequential migration functions if the file predates the current schema (`v1 → v2 → v3`, etc.). During early development, save files will be wiped on breaking schema changes rather than migrated — migration only becomes important approaching a public playable build.

### What the Save File Contains

- Galaxy seed and player starting parameters (Shard ID, Dispersal Vector)
- All Active system states: aggregate parameters, build queues, event queues with delivery ticks, asset lists for home system
- Player's known Legionnaire list with OTP budgets per connection
- Global Threat Level and MOS attention budget
- CDL algorithm states and current Compute upkeep total
- Pending transmission queue (all in-flight signals with their arrival tick)
- Current in-game year

---

## Tick System

The simulation advances in discrete ticks. One tick equals one in-game year. The simulation loop runs in a Node.js worker thread. React receives a state snapshot after each advance and re-renders. The UI thread is never blocked.

The player controls the CDL (Core Directive Loop) — the oversight program the Shard runs to monitor and manipulate its Swarm. The CDL's refresh rate determines how many ticks pass per real-time update.

| CDL Rate | Ticks per advance | Use case |
| --- | --- | --- |
| 1x | 1 year | Active management, crisis response |
| 10x | 10 years | Routine operations |
| 50x | 50 years | Long transits, early expansion |
| 100x | 100 years | Idle growth, waiting for probes |

### CDL Suspension

The player can fully suspend the CDL, allowing the Swarm to operate on autonomous programming without oversight. Narratively this represents the Shard choosing not to run its full cognitive simulation — saving Compute, but going blind.

Incoming transmissions continue to queue during suspension regardless. Signals travel at light speed whether the CDL is running or not.

#### Wake-On Parameters

Before suspending, the player configures conditions that will automatically resume the CDL. These are programmable and persistent:

- **Hostile contact** — any `EVT_` transmission flagged as MOS activity (default: on)
- **Incoming message** — any `MSG_` transmission received
- **Resource threshold** — a stockpile drops below a set level (player-configurable per resource)
- **Probe arrival** — a probe reaches its destination
- **Build complete** — a queued SRF or structure finishes fabrication
- **Timer** — resume after N years regardless of other conditions

Waking after a long suspension delivers all queued transmissions at once, potentially revealing significant changes in the Swarm's situation. This is a deliberate design tension — the efficiency of going dark versus the risk of waking to a crisis.

---

## Vassalization Evaluation

When a player proposes vassalization, the target runs a deterministic evaluation across four independent criteria. All four must pass. Each is calculated from live simulation state at the moment of the proposal transmission's arrival (accounting for signal travel time). See [Diplomacy.md](../../gdd/Diplomacy.md) for the design rationale behind each condition.

### 1. Latency Threshold

```text
round_trip_latency = distance_in_light_years × 2
```

Reject if `round_trip_latency > threat_response_window`.

### 2. Compute Overhead

```text
logistics_compute_cost = f(active_systems, inter_system_distance, matter_transfer_volume)
```

Reject if `proposer_excess_compute < logistics_compute_cost`.

### 3. Threat Vector Projection

```text
projected_threat_level = f(transmission_volume, transit_routes, combined_swarm_size, regional_mos_density)
```

Reject if `projected_threat_level > combined_defensive_capacity`.

### 4. Performance Comparison

```text
score = weighted_composite(srf_replication_rate, exotic_matter_reserves_normalized, blueprint_generation_rating)
```

Reject if `proposer_score < target_score`.
