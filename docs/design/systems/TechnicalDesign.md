# Technical Design

The galaxy is simulated to a realistic scale, so many billions of systems. 

It is generated in a way similar to No Man's Sky, with a mathematical seed creating a static coordinate system for stars and anomalies.

The player will be "blind" until they spend Compute on Intel, so the "billions of systems" exist as empty placeholders until the player experience requires data.

Stars do not move in the first version of the game.

## System Lifecycle

Every star system exists in one of three states:

- **Dormant** — seed-only. No save data. All properties (star type, resource distribution, anomalies, MOS presence probability) are derived deterministically from the galaxy seed and the system's coordinates. Costs nothing to store.
- **Waking** — a probe is in transit. The system does not yet exist in the save file. Its seed-derived properties are pre-calculated client-side when the player views the probe's trajectory.
- **Active** — a probe has arrived and transmitted. The system is instantiated from its seed, timestamped with the in-game year of wake, and written to the save file. From this point it is simulated forward.

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

Only Active systems are written to the save file. Dormant systems are pure seed — they cost nothing. This means save file size scales with player activity, not galaxy size, and remains manageable even in late game.

## Tick System

The simulation advances in discrete ticks. One tick equals one in-game year.

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

## Vassalization Evaluation

When a player proposes vassalization, the target Legionnaire runs a deterministic evaluation across four independent criteria. All four must pass for the proposal to be accepted. Each is calculated from live simulation state at the moment of the proposal transmission's arrival (accounting for signal travel time).

### 1. Latency Threshold

```text
round_trip_latency = distance_in_light_years × 2
```

The target compares `round_trip_latency` against its current `threat_response_window` — the maximum tolerable delay before a local crisis becomes unrecoverable. If latency exceeds the window, vassalization is rejected regardless of other factors.

The player can improve this outcome by pre-deploying autonomous sub-Shards with delegated crisis authority closer to the target, reducing effective response lag.

### 2. Compute Overhead

The simulation calculates a `logistics_compute_cost` for the proposed unified Swarm based on:

- Number of active systems under combined control
- Inter-system distance (longer routes = more predictive modeling)
- Current matter transfer volume

If `proposer_excess_compute < logistics_compute_cost`, rejection. The player must grow Compute generation or reduce existing overhead before re-proposing.

### 3. Threat Vector Projection

The simulation projects combined Threat Level after unification, factoring in:

- Increased transmission volume between systems
- Physical resource transit routes (visible to MOS detection)
- Combined Swarm size relative to MOS asset concentration in the region

If `projected_threat_level > combined_defensive_capacity`, rejection.

### 4. Performance Comparison

The target scores the proposer on:

- SRF replication rate (per tick)
- Exotic Matter reserves (normalized to Swarm size)
- Tech level (blueprint generation rating)

If the proposer scores below the target on the weighted composite, rejection. The target will not subordinate to a less capable CDL.
