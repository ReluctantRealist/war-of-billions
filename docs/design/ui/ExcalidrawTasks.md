# Excalidraw Tasks

Checklist of screens and diagrams to mock up in Excalidraw before writing any React code. Each mockup should live in `docs/design/ui/Excalidraw/` as a `.excalidraw` file with an exported `.png` alongside it.

---

## Wireframes (priority order)

### 1. Home System View
The main screen the player spends most time on.
- Swarm stats (SRF count, NRA count, aggregate Compute generation)
- Resource bars (Basic Matter, Exotic Matter, Compute, Waste)
- Build queue (current SRF/NRA fabrication in progress)
- CDL tick controls (1x / 10x / 50x / 100x, suspend button)
- Threat Level indicator
- Incoming transmission feed

### 2. Galaxy Map
How the player sees the universe.
- Dormant systems (seed-derived placeholders, greyed out)
- Waking systems (probe in transit, trajectory line)
- Active systems (instantiated, colored by status)
- Light-cone delay visualization (how old is the data the player is seeing?)
- MOS presence indicators (where known)

### 3. Diplomacy Screen
Managing relationships with other Legionnaires.
- Known Legionnaire list with Shard ID and status
- OTP Budget per connection (data volume remaining)
- Vassalization proposal UI (the four rejection conditions as visible metrics)
- Transmission log (sent/received, cost in OTP data)
- Key Courier fabrication and transit status

### 4. Research Allocation
Spending Quantum Compute across subcategories.
- Matter Branch subcategories (Metallurgy, Propulsion, Combat NRAs)
- Compute Branch subcategories (Galaxy Sim, Stealth & Detection, CDL Algorithms)
- Quantum Compute pool (total available this tick, currently allocated)
- Per-subcategory: current Likelihood of Return, allocation slider
- Recent Blueprint/Algorithm results

### 5. Remote System Panel
What the player sees for a system they don't live in.
- Aggregate parameters (Compute rate, defensive strength, replication rate, matter stockpile)
- Delayed transmission feed (timestamped with send-year and receive-year)
- Standing directives editor (the autonomous instructions the local Shard follows)
- Last known Threat Level
- Time since last transmission received

### 6. Expansion Launch Screen
Configuring and sending a new Seed SRF.
- Target system selector (from Galaxy Map)
- Propulsion method (antimatter, ion drive, mass driver, etc.)
- Shard autonomy level and baseline directives
- Goal presets ("produce Dyson Swarm", "maintain Threat Level below X", "buffer star")
- Advanced parameter list (for hardcore players)
- Estimated transit time and arrival year

### 7. CDL Suspension Setup
Going dark intentionally.
- Wake-on parameter toggles (hostile contact, incoming message, resource threshold, probe arrival, build complete, timer)
- Per-parameter configuration (e.g., which resource, what threshold)
- Estimated Compute savings while suspended
- Warning: queued transmissions will pile up

---

## Flow Diagrams

### Expansion Decision Flow
The full decision tree from "I want to colonize a system" to "probe launched." Covers target selection, propulsion choice, Shard programming, and the tradeoffs at each step.

### CDL Suspension Flow
From active CDL to suspended state and back. Show what triggers wake, what the player sees on resume (queued transmissions delivered at once), and the risk/reward.

### Combat Notification Flow
Two paths: home system (live CDL, direct orders) vs. remote system (delayed transmissions, autonomous Shard). Show what the player can and cannot do in each case.

---

## State Diagrams

### System Lifecycle
`Dormant` -> `Waking` (probe in transit) -> `Active` (probe arrived, transmitting). Show what triggers each transition and what data exists at each stage.

### Threat Level Escalation
How player actions feed into Threat Level, how Threat Level combines with MOS Presence to produce attack likelihood, and the MOS response pipeline (EW -> Kinetic -> Armada).
