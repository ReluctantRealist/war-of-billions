# Balance Philosophy

This document defines the intended feel and pacing of the game before any CSV numbers are written. It answers: how fast should things happen, how scarce should resources feel, and what should the player be worried about at each stage?

**How to use this doc:** Fill in target values and ratios here first. Then use this as the reference when populating `data/balance/` CSVs. If a balance number in a CSV contradicts this doc, this doc wins — update the CSV, not the philosophy.

---

## Pacing Targets

Define the intended tempo for each game phase. One tick = one in-game year.

### Early Game (first system, pre-expansion)

**Duration target:** *How many ticks (years) should the early game last before the player is ready to expand?*

**Replication tempo:** *How many ticks to replicate the first SRF? How does this accelerate as more SRFs exist?*

**First NRA printing:** *When should the player first have enough SRFs to start printing NRAs?*

**First MOS contact likelihood:** *At what tick range should the player expect first signs of MOS, depending on start location?*

**Resource feel:** *Should Basic Matter feel abundant or scarce? Should Exotic Matter be a bottleneck from tick 1?*

---

### Mid Game (multi-system, pre-vassalization)

**Duration target:** *How many ticks should pass between first expansion and first viable vassalization?*

**Expansion tempo:** *How many ticks for a Seed SRF to reach a neighboring system? How many active systems should the player have before mid game "feels" right?*

**Threat Level pressure:** *At what Swarm size does Threat Level start becoming a real constraint? When should the player first feel the tension between growth and stealth?*

**Research tempo:** *How often should Blueprints/Algorithms drop at a reasonable Quantum Compute allocation?*

**Compute Sink pressure:** *When should Compute Sinks start meaningfully constraining the player's budget?*

---

### Late Game (empire management, MOS escalation)

**Duration target:** *How long should the late game sustain interesting decisions before the win condition becomes reachable?*

**MOS escalation curve:** *How does MOS attack frequency and severity scale with game progression?*

**Vassalization viability:** *What does a "ready to vassalize" empire look like in terms of Compute surplus, tech level, and system count?*

**Win condition proximity:** *When should the player first realize that intergalactic colonization is possible? How many more ticks to achieve it?*

---

## Resource Ratios

### Matter

| Parameter | Target value | Notes |
| --- | --- | --- |
| Basic Matter per asteroid belt | | *Common systems should provide X per tick* |
| Exotic Matter per anomaly system | | *Rare systems should provide X per tick* |
| SRF replication cost (Basic) | | |
| SRF replication cost (Exotic) | | |
| Master Seed SRF cost (Basic) | | *The expansion cost — should feel expensive* |
| Master Seed SRF cost (Exotic) | | |
| NRA cost range (Basic) | | *Min to max across all NRA types* |
| NRA cost range (Exotic) | | *Min to max across all NRA types* |

### Energy & Compute

| Parameter | Target value | Notes |
| --- | --- | --- |
| Base energy harvest per SRF | | |
| Energy-to-Compute conversion rate | | |
| Waste-to-Harvest ratio (stealth sweet spot) | | *What % Waste keeps Threat Level manageable?* |
| CDL base Compute cost per tick | | *The floor — just running the game* |
| Compute Sink costs (pre-Algorithm) | | *Reference TechTree.md for per-sink values* |
| Quantum Lab output per tick | | *The research bottleneck* |

---

## Threat Level Tuning

| Parameter | Target value | Notes |
| --- | --- | --- |
| Threat Level at game start | 0 | *Always — Clean Start Guarantee* |
| Threat Level threshold for EW response | | *When does MOS start jamming?* |
| Threat Level threshold for Kinetic strike | | *When does MOS launch impactors?* |
| Threat Level threshold for Armada | | *When does MOS commit a fleet?* |
| Threat Level decay rate (per tick, no activity) | | *How fast does going dark help?* |
| Threat Level spike from full Dyson Swarm | | *The "greedy trap" — should be dramatic* |
| Threat Level spike from Plasma Arc Crucible | | *Should be very high but temporary* |

---

## Equivalent Exchange Weights

Reference for Blueprint generation. These weights determine how "expensive" each parameter is to improve via research.

| Parameter | Physics Weight | Rationale |
| --- | --- | --- |
| Heat dissipation | | *Thermodynamics is hard — high weight* |
| Basic Matter cost | | *Iron is common — low weight* |
| Exotic Matter cost | | *Rare materials — medium-high weight* |
| Transit speed | | |
| Emission signature | | |
| Structural integrity | | |
| Reclaim Yield | | |
| Disassembly Time | | |

*Fill in weights before generating any Blueprint CSVs. These ratios define the entire research economy.*

---

## Design Constraints

Rules that balance numbers must never violate:

- **MOS is always ahead on the asymptote.** No combination of player research should close the gap to parity. 95% of MOS efficiency is the ceiling.
- **Stealth and growth are always in tension.** There must be no configuration where the player can grow at maximum rate with zero Threat Level increase.
- **Expansion has real cost.** A Master Seed SRF should represent a major investment — not something the player launches casually.
- **Compute is the true bottleneck.** Matter can be stockpiled. Energy can be harvested. Compute is consumed every tick and never banked.
- **Distance is safety, distance is isolation.** Far starts should feel safe but slow. Near starts should feel fast but dangerous. Neither should be strictly better.
