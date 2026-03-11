# Swarm Infrastructure

The player's DMP partition needs somewhere to live. As the Swarm grows, where and how the CDL is physically housed becomes one of the most consequential strategic decisions in the game — affecting heat signature, Threat Level, survivability, build cost, and expansion speed.

## Stages of Housing

**Stage 1 — The Seed SRF**
The player starts as a single condensed SRF. The DMP partition, factories, and logic boards share one hull. No architectural choices yet — just survive and replicate.

**Stage 2 — The Mid-Game Split**
As NRA printing begins in earnest, the player must decide where the CDL lives. This is the core infrastructure decision: centralize into a fortified core, or distribute across the Swarm itself. See strategies below.

**Stage 3 — The Matrioshka Brain**
The physics-perfected late-game endpoint. The entire star is encased in layered distributed compute architecture. Practically unreachable in the early or mid game, and conspicuous enough to require serious stealth investment to maintain.

---

## Stage 2 Strategies

### Strategy A: Monolithic Core (Dumb Swarm)

One massive armored supercomputer in deep orbit. Surrounding NRAs are cheap "dumb" mirror probes — no onboard logic, they just beam harvested energy back to the core for processing.

| Factor | Effect |
|---|---|
| **Cheap expansion** | Dumb probes cost almost exclusively Basic Matter. Mass-producible early. |
| **Exotic Matter efficiency** | Exotic Matter investment concentrated in one structure. |
| **Heat beacon** | Concentrated computation generates a localized thermal bloom — an unnatural signature that spikes Threat Level. Waste normally hides the Swarm; a single hot point does the opposite. |
| **Latency vulnerability** | Light-speed lag within the system means dumb probes must wait for the core to process threats and return evasion vectors. Fringe attacks are slow to respond to. |

---

### Strategy B: Distributed Mesh (Smart Swarm)

The CDL is spread across millions of independent probes. There is no center — the Swarm is the brain.

| Factor | Effect |
|---|---|
| **Thermal camouflage** | Heat is spread across millions of kilometers. To MOS passive scans, it reads as a marginally warmer star — not a Swarm. Significant Threat Level reduction. |
| **No critical weak point** | A kinetic strike destroys thousands of nodes; the CDL reroutes instantly through survivors. No single target can decapitate the Swarm. |
| **Crushing upfront cost** | Every probe requires onboard logic boards — heavy Exotic Matter investment per unit. Early expansion is slow and expensive. |
| **Research dependency** | Full efficiency requires CDL Algorithm advances to manage the coordination overhead of millions of semi-autonomous nodes. |

---

## Asset Recycling

Every NRA has two disassembly parameters that determine how much of its material can be recovered and how long it takes:

- **Reclaim Yield** — the fraction of original Basic Matter and Exotic Matter returned when the asset is torn down. Dense, exotic-matter-heavy structures like Quantum Matrices have low yields; simple iron mirrors have high ones. Atomic bonds in complex quantum logic boards must be carefully unsolved; a solar reflector can simply be snapped apart.
- **Disassembly Time** — ticks required for safe breakdown. Rushing below this threshold destroys the materials.

### Disposable Blueprints

The Research Optimizer can be targeted at `Reclaim_Yield` and `Disassembly_Time` as primary parameters. Blueprints that roll high on these stats produce **Disposable NRAs** — assets with degraded energy output and high mass, but near-total material recovery in one tick. They are designed to fall apart on signal. The trade-off (Equivalent Exchange) is always worse operational performance; a Disposable Flux Harvester produces less energy per unit than a standard one.

### Plasma Arc Crucible

For assets with long disassembly times — Quantum Matrices, Nodal Nexuses, Circumstellar Colliders — the player can bypass `Disassembly_Time` entirely using the **Plasma Arc Crucible** megastructure. It melts billions of probes into raw slag in a single tick.

The trade-off is severe: the thermodynamic violence of instantly converting that much mass generates an extreme localized heat spike. `Heat_Generation` is flagged at maximum in the CSV (`9999`). While Waste energy normally masks Swarm activity, a full-system melt in one tick produces an unmistakable signature. Threat Level spikes immediately. The Plasma Arc Crucible is a deliberate trade: lose stealth, recover matter fast.
