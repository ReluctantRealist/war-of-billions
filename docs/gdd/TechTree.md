# Tech Tree

Research in War of Billions is divided into two branches mirroring the game's core resources: **Matter** and **Compute**. There are no fixed upgrade tiers. Progress is procedural, infinite in scope, and bound by hard physics — meaning returns diminish forever but never reach zero, and no parameter can exceed what the laws of the universe permit.

---

## MOS Research Advantage

The player is not competing on equal footing. MOS generates Quantum Compute through spaceborne biolab research programs that have been running since before the Dispersal. Its asymptotic curves are further along than any Legionnaire can reach through purely mechanical research. The player's research ceiling is lower. This is not a temporary disadvantage — it is the permanent condition of the war. See [GameSetting.md](../lore/GameSetting.md) for the lore context.

The player's viable strategy is not to match MOS research-for-research, but to identify which specific parameters matter most for their current situation and invest there — accepting inferiority everywhere else.

---

## Core Philosophy: Asymptotic Progression

Every researchable parameter has a physical ceiling. Heat dissipation cannot exceed what thermodynamics allows. Propulsion cannot exceed the speed of light. Transit stealth cannot reach zero emissions while an engine is burning.

Because of this, all research returns are logarithmic. Early investment in a subcategory produces large, dramatic improvements. Continued investment produces smaller and smaller gains — each breakthrough costs more Quantum Compute than the last for a proportionally smaller effect. There is no endgame where the player has "finished" a branch. There is only the question of whether further investment in a given parameter is worth the Compute.

This is not a limitation — it is the intended pressure. MOS operates under the same physics. The player who finds the right asymptote to exploit early wins strategically, not the player who grinds longest.

---

## Research Mechanics

### Probability Per Tick, Not a Progress Bar

Research does not fill a bar. The player allocates **Quantum Compute** to a subcategory, and each tick that subcategory rolls a chance to generate a result. The UI displays the current **Likelihood of Return** — the per-tick probability given current Quantum Compute allocation.

A small allocation produces a low probability per tick. A massive allocation produces a high probability but still never guarantees an immediate result. The player can drip-feed Compute over centuries for a slow but cheap chance, or burn large reserves to brute-force a result during a crisis. Neither approach is always correct.

Early in a subcategory, probabilities are higher — the low-hanging fruit of any field is easier to find. As the player advances deeper into a subcategory, the per-tick probability for the next result decreases for the same allocation. More Compute is required to maintain the same research tempo. This is asymptotic progression made mechanical.

### Quantum Compute

All research consumes **Quantum Compute** — a scarce resource generated exclusively by Quantum Lab NRAs. Standard Compute runs the CDL and logistics. Quantum Compute is the research bottleneck.

The player allocates Quantum Compute across active subcategories each tick. Spreading allocation thin slows all fronts. Focusing on one subcategory accelerates it at the cost of everything else. There is no free allocation — unspent Quantum Compute does not carry over; it represents research capacity that went unused that tick.

Building higher-tier Quantum Labs requires Matter Branch advances, creating a dependency loop: better materials science unlocks better research infrastructure, which accelerates all further research.

### Tech Diplomacy

Blueprints and Algorithms can be transmitted to allied Legionnaires via OTP-encrypted signal. See [Diplomacy.md](Diplomacy.md) for full mechanics. Sharing a tech result raises both parties' Threat Level — large data transmissions are detectable. It is powerful but never free.

---

## MATTER Branch: Blueprints

Matter research yields **Blueprints**. A Blueprint is not an unlock of a new structure — it is a set of parameter modifiers applied to an existing Asset (SRF or NRA). The base Asset exists regardless; the Blueprint makes it better in specific, targeted ways.

### The Rule of Equivalent Exchange

Because matter obeys physics, every Blueprint must balance. Every parameter it improves must be offset by a proportional penalty to one or more other parameters. There are no free improvements.

Each parameter has a **physics weight** — a measure of how costly that property is to change in the real universe. Heat dissipation, for example, is heavily weighted: it is physically expensive to move heat efficiently. Basic Matter cost is lightly weighted: there is a lot of iron in the universe.

When a Blueprint improves a heavily-weighted parameter, the offset penalty is large. When it improves a lightly-weighted parameter, the penalty is small. The total improvement value, measured in physics-weighted units, must equal the total penalty value. The generator cannot create something for nothing.

This means every Blueprint is a trade. The player cannot find a Blueprint that is strictly better across all parameters. They must decide which trade is worth making for their current strategic situation.

### Target Weighting

Before rolling for a Blueprint result, the player instructs the Quantum Lab which parameter to **prioritize**. This biases the generator toward improvements in that parameter, at the cost of larger or more numerous penalties elsewhere. Targeting a heavily-weighted parameter like heat dissipation will produce a Blueprint with a meaningful improvement — and a correspondingly steep trade-off. Targeting a lightly-weighted parameter produces a modest improvement with a smaller penalty.

The player cannot dictate the exact Blueprint — only the direction of the search.

### Disposable Blueprint Type

`Reclaim_Yield` and `Disassembly_Time` are valid target parameters for the Research Optimizer. Blueprints that prioritize these stats produce **Disposable NRAs** — assets optimized to be rapidly recovered rather than operated indefinitely. They trade operational performance (lower energy output, higher mass) for near-total material recovery in minimal ticks. Useful for strip-mine-and-retreat operations where the infrastructure will be deliberately demolished before MOS arrives. See [Infrastructure.md](Infrastructure.md) for full recycling mechanics.

---

### Metallurgy

**What it modifies:** The material properties of SRFs and NRAs — heat generation during operation, heat generated during replication, structural integrity, exotic matter storage efficiency, self-repair rate, and reactor emission signature.

**Research direction:** Metallurgy Blueprints trade between these parameters according to the Equivalent Exchange rule. A Blueprint that reduces replication heat might increase the exotic matter cost of the alloy. One that improves structural integrity might increase the basic matter cost per unit. One that reduces reactor emission signature might reduce output energy slightly.

**Strategic role:** Metallurgy is the foundation of the Matter Branch. Higher-tier Quantum Labs require Metallurgy advances to construct. Without investment here, research throughput is capped and many other Blueprint categories are inaccessible.

---

### Propulsion

**What it modifies:** Transit speed, fuel consumption per light-year, engine emission signature (the electromagnetic and particle exhaust detectable by MOS), deceleration capability, and launch signature from mass drivers.

**Research direction:** The core trade in Propulsion is always speed versus signature. A Blueprint that improves transit speed will worsen emission signature, increase fuel consumption, or both. A Blueprint that reduces emission signature will reduce speed or increase the exotic matter cost of the drive. Near-silent propulsion and high-speed propulsion are physically incompatible — both can be improved asymptotically, but the gap between them cannot be closed.

**Strategic role:** Propulsion choices determine how long expansion takes and how detectable movement is. Faster colonization increases Threat Level exposure. Silent transit takes longer but leaves the player harder to map.

---

### Combat NRAs

**What it modifies:** Intercept effectiveness against different MOS asset types, area denial coverage radius, point defense intercept rate, kinetic impact yield versus transit detectability, EMP disable duration, hull integrity of SRFs and key NRAs, and the Swarm disruption rate against enemy replication.

**Research direction:** Offensive Combat Blueprints trade between lethality, signature, and cost. A Blueprint that improves kinetic yield will increase transit mass and therefore detectability. A Blueprint that improves EMP duration will increase the exotic matter cost of the NRA. Defensive Blueprints trade between coverage, upkeep Compute, and build cost. A Point Defense Array that intercepts more incoming projectiles per tick requires more Compute to run.

**Strategic role:** Combat NRAs do not replicate. They are fabricated, deployed, and expended or destroyed. Investment here only pays off if the player expects to be attacked — or intends to attack. Over-investing produces Compute-draining defensive infrastructure that slows economic growth. Under-investing leaves the Swarm naked against MOS strikes.

---

## COMPUTE Branch: Algorithms

Compute research yields **Algorithms**. An Algorithm is a software modification to the CDL or to a class of NRA's operating logic. Algorithms do not cost Matter to apply — they are code, not hardware. But they carry a different cost.

### The Upkeep Tax

Every Algorithm permanently increases the CDL's minimum **Compute Upkeep** — the ongoing cost of running its own software. More sophisticated code is more expensive to execute each tick. A small algorithm adds a small upkeep. A powerful algorithm that dramatically reduces transit lag or masks Threat Level adds substantial upkeep.

If the Swarm's Compute generation falls below the total upkeep of all active Algorithms, the empire stalls. Algorithms do not deactivate cleanly when underpowered — they degrade. A CDL running under its own upkeep threshold produces cascading inefficiencies: logistics slow, Threat Level accuracy drops, vassal Shards receive delayed commands. Recovery requires either building more Compute generation or accepting the performance penalty.

This means the player's algorithmic sophistication is bounded by their Compute economy. A player with a small Swarm cannot run the same algorithms as a player with a mature Dyson infrastructure. Algorithms scale the ceiling; Compute generation determines whether you can reach it.

---

### Galaxy Simulation & Prediction

**What it modifies:** Long-range matter routing accuracy, convoy interception rate, Intel extracted per unit of passive scan data, Threat Level projection accuracy, the player's ability to identify low-detection transit corridors, and the cost in probes to map a region.

**Upkeep cost:** Simulation algorithms are among the most Compute-intensive. More accurate modeling of orbital drift and gravitational interference across thousands of systems requires continuous background processing. Each advance in this subcategory adds to the baseline simulation load the CDL must sustain every tick.

**Strategic role:** Simulation algorithms do not help in a firefight. They reduce the invisible tax that distance and physics impose on logistics — fewer convoys intercepted, better routing, earlier warning. Their value is proportional to the size and spread of the Swarm. A player with two systems gains little. A player managing dozens of systems across hundreds of light-years gains enormously.

---

### Stealth & Detection

**What it modifies:** The player's infrared and electromagnetic emission profile, the detectability of resource transit routes, the player's ability to identify MOS assets without active emissions, false signature generation, and the Compute-to-Waste conversion ratio of energy harvesting.

**Upkeep cost:** Stealth algorithms have moderate upkeep. Passive scanning is cheap. Active deception — maintaining false signatures, scrambling transit route data — is expensive. The player must weigh the Compute cost of staying hidden against the Threat Level cost of being seen.

**Strategic role:** Detection and stealth are the information layer of combat. A player who invests here learns MOS is coming before the strike arrives, and presents a harder target to map. Combined with Simulation algorithms, it creates a significant intelligence advantage. But the upkeep compounds — a fully stealthy, fully surveilled empire runs a heavy Compute overhead that constrains economic growth.

---

### CDL Algorithms

**What it modifies:** The CDL's effective command range, tick processing capacity at large Swarm sizes, the ability to pre-authorize vassal crisis responses (reducing effective latency for vassalization), the Compute overhead of unified multi-system management, the OTP cost of standard transmissions, and the accuracy of Threat Level assessment.

**Upkeep cost:** CDL Algorithms are directly tied to empire scale. An algorithm that enables managing fifty systems simultaneously costs far more Compute upkeep than one designed for five. The player must grow their Compute generation ahead of their CDL algorithmic ambitions, or the expansion will outpace their ability to manage it.

**Strategic role:** CDL Algorithms directly unlock diplomatic options. The Autonomy Delegation Protocol addresses vassalization's latency rejection condition (see [Diplomacy.md](Diplomacy.md)). The Multi-system Logistics Optimizer addresses its Compute overhead condition. A player who neglects this subcategory will find that even willing allies cannot be vassalized, and that their own empire becomes harder to manage as it grows.

#### Compute Sinks

The CDL runs mandatory background processes every tick — **Compute Sinks** — that drain processing capacity before the player spends a single unit on research or logistics. Early game, these sinks are brute-force and expensive. Each has a corresponding CDL Algorithm that reduces the cost, always at a secondary trade-off.

**N-Body Orbital Correction**
- *Sink:* With millions of NRAs orbiting a star, the CDL must continuously calculate gravitational forces from the star, planets, and neighboring assets and fire micro-thrusters to prevent collisions.
- *Algorithm Fix — Harmonic Resonance Pathfinding:* Groups NRAs into mathematically self-correcting orbital schools, eliminating per-unit calculations.
- *Trade-off:* Reduces Compute cost per orbital NRA by ~40%, but the algorithm itself adds a permanent base Upkeep of 500 Compute per tick.

**Relativistic Trajectory Modeling**
- *Sink:* Launching matter to a system 40 light-years away means aiming at where that star will be in thousands of years. Every transfer requires high-precision trajectory math accounting for galactic drift, radiation pressure, and interception risk over millennia.
- *Algorithm Fix — Stellar Drift Heuristics:* A predictive model that achieves the same physical hit-rate with fewer decimal places of accuracy, dramatically cutting calculation cost per initiated transfer.
- *Trade-off:* Reduces deep-space transfer Compute cost significantly, but the improved sensor model requires more active pings — slightly increasing baseline Threat Level.

**Continuous Ledger Verification**
- *Sink:* Hard-coded paranoia from the Keeper's surrender. The CDL continuously verifies its local Swarm's integrity against tampering or MOS spoofing, checking every node's code against the internal ledger every tick.
- *Algorithm Fix — Asymmetric Hash Compression:* Makes ledger verification orders of magnitude faster without reducing coverage.
- *Trade-off:* Frees up large amounts of Compute, but the compressed verification layer is mathematically easier for a MOS cyber-warfare NRA to breach if one reaches the system.

**Thermodynamic Load Balancing**
- *Sink:* High-output NRA clusters generate heat faster than passive radiation can dissipate it. The CDL must constantly shift calculation loads between hot and cold nodes and align radiators to maximize heat loss, or risk thermal runaway.
- *Algorithm Fix — Predictive Heat-Sink Cycling:* The CDL anticipates which sectors will overheat before they do, pre-cooling them during low-load cycles rather than reacting after the fact.
- *Trade-off:* Reduces Compute overhead for running Quantum Labs, but requires more physical Basic Matter allocated to heat buffer infrastructure.

**Desync Bridging**
- *Sink:* Vassalizing another Shard requires continuously synchronizing two separate Swarm networks across light-years of lag. The CDL must simulate the vassal's current state from data that may be decades old, patching the gap every tick. This is the same Compute drain that drives Vassalization Rejection Condition 2 — see [Diplomacy.md](Diplomacy.md).
- *Algorithm Fix — Asynchronous Autonomy Delegation:* The vassal's DMP partition handles 90% of its own logic using the player's current parameters, reducing sync traffic to the remaining 10%.
- *Trade-off:* Massively reduces the Compute cost of multi-system empire management, but increases the probability that the vassal's DMP independently calculates it no longer benefits from the alliance and moves to break vassalization.

---

### Quantum Labs (Special Subcategory)

Quantum Labs are not researched through the standard probability system — they are hardware Assets built by Macro-Assembler Forges. However, their construction requires specific Metallurgy Blueprints, creating the dependency between the two branches.

**What it modifies:** The rate of Quantum Compute generation, the pool size available for allocation each tick, and whether multiple Labs can be networked into a single distributed research mesh (pooling their probability rolls).

Higher-tier Labs produce more Quantum Compute per tick, enabling faster research across all subcategories. Networking multiple Labs means a single roll covers the combined output of all linked Labs — a breakthrough from one propagates to the whole network.

**Strategic role:** Quantum Labs are the research economy's bottleneck. Every subcategory in both branches draws from the same Quantum Compute pool. A player with limited Lab capacity must choose which fronts to advance and which to leave dormant. Lab investment is not glamorous — it produces no weapons, no speed, no stealth — but it determines the tempo of everything else.

---

## Dependency Map

| Capability | Requires |
| --- | --- |
| Quantum Lab (tier 2) | Metallurgy advance in replication heat reduction |
| Quantum Lab (tier 3) | Metallurgy advances in energy storage density and high-output heat dissipation |
| High-output propulsion Blueprints | Metallurgy advance in heat dissipation |
| Hardened hull Blueprints | Metallurgy advance in structural integrity |
| Autonomy Delegation Protocol | Any CDL Algorithm previously unlocked |
| Multi-system Logistics Optimizer | Any Galaxy Simulation algorithm previously unlocked |
| Any advanced Blueprint or Algorithm | Quantum Compute above base Lab output |
