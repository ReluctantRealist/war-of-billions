# Tech Tree

Research in War of Billions is divided into two branches mirroring the game's core resources: **Matter** and **Compute**. All research is conducted by Quantum Supercomputer NRAs — specialized, non-replicating assemblies that consume Compute and Exotic Matter to generate blueprints.

## Research Mechanics

### Blueprints, Not Tiers

There are no linear upgrade tiers within a subcategory. Instead, each subcategory has a pool of blueprints. Assigning Quantum Lab capacity to a subcategory generates a probability roll each tick. Blueprints are discovered at random from the pool — sustained effort guarantees eventual discovery, but an early lucky roll can yield a game-changing blueprint before MOS expects it.

This models real research: you cannot know in advance which experiment will succeed. A player who invests heavily in Metallurgy early might stumble onto an exotic alloy that outperforms MOS-equivalent tech for decades.

### Quantum Compute

Most novel research requires **Quantum Compute** — a scarce resource generated exclusively by Quantum Lab NRAs. Standard Compute keeps the CDL and logistics running; Quantum Compute is the bottleneck for research throughput. Building better Quantum Labs requires advanced Metallurgy, creating a dependency loop between the two branches.

Quantum Compute is consumed per research tick. The player allocates it across active subcategories. Spreading thin slows everything; focusing accelerates one area at the cost of others.

### Tech Diplomacy

A player can request a blueprint from another Legionnaire via OTP-encrypted transmission. The target evaluates the request and usually demands a blueprint in return. The exchange raises both parties' Threat Level — two Swarms transmitting complex data packages is detectable. Tech sharing is powerful but never free.

---

## MATTER Branch

Research into physical materials, propulsion systems, and combat hardware. All hardware-based blueprints live here.

### Metallurgy

Quantum molecular modeling applied to alloy design and material science.

**Blueprint pool includes:**

- **High-density alloy composites** — reduces heat generated during SRF replication, enabling faster copy cycles
- **Quantum-modeled crystal lattices** — improves energy storage density; more Compute per unit of harvested energy
- **Refractory metamaterials** — heat dissipation for high-output propulsion; prerequisite for antimatter drives
- **Exotic matter containment vessels** — increases exotic matter storage capacity and reduces transit loss
- **Nano-scale self-repair matrices** — SRFs and NRAs slowly repair damage without consuming build queue capacity
- **Dense radiation shielding** — reduces detection signature of active reactors; minor stealth benefit

*Metallurgy is a prerequisite for advanced Quantum Lab NRAs. Without it, Quantum Compute output is capped at the base tier.*

---

### Propulsion

Transit speed, fuel efficiency, and detection tradeoffs for all mobile assets. Every propulsion type has a distinct stealth/speed tradeoff.

**Blueprint pool includes:**

- **Ion Drive Mk.II** — moderate speed improvement, low cost, produces detectable ion exhaust plume at range
- **Ion Drive Mk.III** — further improvement; exhaust signature reduced but not eliminated
- **Antimatter Drive** — very high speed; extreme detection risk during burn; unsuitable for covert operations
- **Cold-burn Mass Driver** — slow but near-silent bulk transit; best for Key Couriers and Matter convoys
- **Stealth Thruster Array** — slow; emission profile near-undetectable; preferred for scout probes
- **Relativistic Probe Core** — extreme speed; one-way only (no deceleration package); used for kamikaze scouts or long-range seeding at high Threat Level
- **Inertial dampening frame** — reduces launch signature from mass drivers; harder for MOS to detect Shard dispersal events

---

### Combat NRAs

Hunter-killer and defensive assemblies. These do not replicate. They are fabricated, deployed, and expended.

**Blueprint pool includes:**

- **Standard Hunter-Killer** — baseline intercept unit; effective against unshielded probes
- **Swarm Disruptor** — targets SRF replication protocols; slows enemy Swarm growth rather than destroying units
- **Kinetic Impactor** — high-mass, low-signature impact weapon; slow but undetectable in transit
- **Area-Denial Mine Field** — stationary; detonates on proximity; useful for system defense
- **Point Defense Array** — intercepts incoming kinetic or energy weapons; defensive installation
- **Hardened Hull Package** — passive armor for SRFs and key NRAs; requires advanced Metallurgy alloys
- **EMP Burst NRA** — disables enemy electronics temporarily; does not destroy; creates intercept window

---

## COMPUTE Branch

Research into software, simulation, detection, and CDL capability. All intelligence and algorithmic improvements live here.

### Galaxy Simulation & Prediction

Better modeling of the physical universe means better logistics, better Intel from the same scan data, and more accurate threat projection.

**Blueprint pool includes:**

- **Orbital drift compensation v2** — more accurate long-range matter routing; reduces convoy interception rate
- **Stellar cartography algorithm** — extracts more Intel from passive scan data; fewer probes needed to map a region
- **MOS behavior prediction model** — identifies patterns in MOS asset movement; improves Threat Level accuracy
- **Gravitational lens array** — passive deep-space observation using stellar mass; no emissions, long range
- **Transit window calculator** — identifies low-detection routing corridors between systems

---

### Stealth & Detection

Blueprints for staying hidden and finding what is hidden. Most Intel work is about using existing data carefully; this subcategory provides the tools to do so.

**Blueprint pool includes:**

- **Laser verification ping array** — identifies Swarm nodes as hostile or friendly without radio emissions; short range, near-undetectable
- **Waste ratio optimizer** — improves the Compute-to-Waste conversion ratio; same Compute output, lower detection signature
- **Passive scan NRA** — long-range listening post; generates Intel with zero active emissions
- **Signal scrambler package** — masks resource transit route signatures; reduces MOS ability to map your empire
- **Thermal sink array** — absorbs and disperses reactor heat over time; reduces infrared detection signature
- **Decoy beacon** — emits a false Swarm signature at a chosen location; diverts MOS attention

---

### CDL Algorithms

Improvements to the Core Directive Loop itself — how efficiently it processes, how far its authority can reach, and what new capabilities it gains.

**Blueprint pool includes:**

- **Autonomy delegation protocol** — allows the CDL to pre-authorize crisis responses for vassal Shards; reduces effective latency for vassalization; directly improves vassalization rejection odds
- **Multi-system logistics optimizer** — reduces Compute overhead for unified Swarm management; directly improves vassalization rejection odds
- **Threat assessment v2** — more accurate Threat Level projection; earlier warning of MOS mobilization
- **Predictive build scheduling** — CDL plans build queues further ahead; reduces idle time in resource processing
- **Compressed transmission protocol** — reduces OTP cost of standard command messages by up to 40%
- **Parallel CDL threading** — CDL processes multiple systems simultaneously; reduces tick processing time at high Swarm sizes

---

### Quantum Compute (Special Subcategory)

Quantum Compute is not researched — it is generated by Quantum Lab NRAs and consumed by all other research. This subcategory contains blueprints for the labs themselves.

**Blueprint pool includes:**

- **Quantum Lab NRA Mk.I** — base quantum research assembly; requires standard Metallurgy alloys
- **Quantum Lab NRA Mk.II** — higher throughput; requires high-density alloy composites (Metallurgy)
- **Quantum Lab NRA Mk.III** — highest throughput; requires quantum-modeled crystal lattices and refractory metamaterials (Metallurgy)
- **Distributed Quantum Mesh** — links multiple Quantum Labs into a single research network; probability rolls across linked labs are pooled

---

## Dependency Map

| Blueprint / Capability | Requires |
| --- | --- |
| Quantum Lab Mk.II | High-density alloy composites (Metallurgy) |
| Quantum Lab Mk.III | Quantum-modeled crystal lattices + Refractory metamaterials (Metallurgy) |
| Antimatter Drive | Refractory metamaterials (Metallurgy) |
| Hardened Hull Package | High-density alloy composites (Metallurgy) |
| Autonomy Delegation Protocol | CDL Algorithms Mk.I (any CDL blueprint unlocked) |
| Multi-system Logistics Optimizer | Orbital drift compensation v2 (Galaxy Simulation) |
| Any advanced blueprint | Quantum Compute above base threshold |
