# Core Principles

War of Billions is a single-player far-future space management game where the player manages an exponentially growing network of self-replicating, automated factories, with the goal of spreading across star systems and dominating the galaxy.

It is built on a React + TypeScript frontend wrapped in **Electron**, shipping as a native desktop executable on itch.io and Steam. All simulation runs locally on the player's hardware — no backend, no server. See [TechnicalDesign.md](../design/systems/TechnicalDesign.md) for the simulation architecture.

## Game Context

Players take the form of a Legionnaire — a member of the Prime Legion, the ten thousand Keeper Shards launched during the Dispersal (see GameSetting.md). Each Legionnaire is a fully autonomous DMP partition loaded onto a single master seed SRF. First we will design the player playing as a Keeper Legionnaire, the underdog being hunted by the more advanced Master of Swarms. Later, we can design the player playing as the Master of Swarms hunting the Keeper.

Keeper Shards have one goal, thwart the Master of Swarms until the end of time. A secret late-game goal is to colonize another galaxy to fight on, that is the "win" condition and perhaps even a "new game plus" unlock.

The universe has no FTL, so the war for the stars lasts for billions of years in the core canon. No FTL also means that the player cannot easily communicate with assets across other star systems. Instead, subservient Shards must be programmed correctly and sent to autonomously operate in other systems. Their level of autonomy is dictated by the "lag", where close systems can be updated easily but far away systems will suffer or even catastrophically fail if planned poorly since the player cannot "fix" problems easily, or even know of them quickly.

## Starting Parameters

Two values are set at game start and define the player's position in the galaxy and relationship to the broader war:

- **Shard ID** — the player's number in the Prime Legion (1–10,000). Lower IDs were launched earlier and have had more time to travel. Functionally this affects the flavor of transmissions and how other Legionnaires address the player. May influence starting tech state in future design.
- **Dispersal Vector** — the heading imparted at launch, which together with elapsed time since the Dispersal determines where in the galaxy the player's seed SRF arrives. This is the primary driver of starting location: proximity to Sol, local star density, likelihood of early MOS contact, and distance from other Legionnaires.

These can be randomized, chosen from presets (e.g. *Near Sol — High Risk*, *Deep Rim — Isolated*, *Core — Resource Rich*), or entered manually for a specific run.

### Hard Coded Parameters

The player's original source code prevents the DMP from endangering Earth. If the player tries to attack Sol, they get a "permission blocked" error. The player is technically still a subroutine.

The original source code also enforces the hardware-level encryption and self-destruct protocol for all Master Seed SRFs, making them more expensive but ensuring the player does not compromise the network by "cheaping out" on an unsecure copy of itself.

## Gameplay Experience

The state of the galaxy is heavily dependent on the stage of the war.

- **Early War**: Finding another Swarm is extremely rare. Galaxy is vast and not seeded.

- **Mid War**: Player encounters Swarms rarely. Master of Swarms presence scales with proximity to Sol and cirtical systems like neutron stars. Threat Level becomes a catastrophic failure point if neglected.

- **Late War**: MOS is everywhere and establishing a new communication channel with the remaining friendly Shards raises Threat Level greatly.

### Resource Acquisition

The Two Core Resources, Matter and Energy, are divided into subcategories:

- **Basic Matter**: Iron and lighter elements, common in many systems
- **Exotic Matter**: Heavy elements, transuranics, rare except abundant in anomaly systems (like neutron stars)
- **Compute**: This is energy successfully turned into available compute for the DMP. To acquire it, the player must successfully harvest energy.
-**Waste**: Energy that leaves the star but does not become Compute. Though it's technically wasted, it is also what hides the player's activities. A full Dyson Swarm is tempting for Compute but leads to immediate detection.

### Matter Spending

- **Copy Master Factory**: This is mainly for colonizing other systems or as a backup for the player's starting SRF. Costs a lot of Exotic Matter, and takes about a hundred years with standard Keeper tech.

- **Print SRF**: Fabricate a new SRF that is smaller and more specialized than the master SRF, allowing for much faster production of specialized NRAs.

- **Print NRA**: Make specialized subassemblies that do not themselves replicate. Early game are things like nanobots and mining drones that help with SRF replication. Late and mid game adds viability of megastructures.

### Energy Spending

Harvested energy converts to Compute, but Compute is not free to operate. The CDL runs a set of mandatory background processes every tick — **Compute Sinks** — that drain processing capacity before the player spends a single unit on research or logistics. Early game, these sinks are brute-force and expensive. Each has a corresponding CDL Algorithm that reduces the cost, always at a secondary trade-off.

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
- *Sink:* Vassalizing another Shard requires continuously synchronizing two separate Swarm networks across light-years of lag. The CDL must simulate the vassal's current state from data that may be decades old, patching the gap every tick.
- *Algorithm Fix — Asynchronous Autonomy Delegation:* The vassal's DMP partition handles 90% of its own logic using the player's current parameters, reducing sync traffic to the remaining 10%.
- *Trade-off:* Massively reduces the Compute cost of multi-system empire management, but increases the probability that the vassal's DMP independently calculates it no longer benefits from the alliance and moves to break vassalization.

### Blueprints and Technology

Technology is divided into Matter and Compute (see TechTree.md).

### Stealth Management

- **Threat Level**: For Keeper Shards (base game), this is the Master of Swarms (MOS) prioritization of your Shard and Swarm for elimination. First it must learn you exist, then it must decide you are worth expending the resources to thwart or destroy. MOS cannot go full force everywhere all at once, so it constantly tries to find high-priority systems and disrupt the largest (or most likely to grow large) Swarms first.

**Delayed Punishment**: Threat Level can be high for a long time before the MOS can mobilize assets to hit the player. If it sees you clearly growing rapidly in the early game, player can get greedy and feel "safe", but they better be read to get hit hard later, because MOS knows about them.

**Distance from Sol**: Sol is now the MOS home system. The farther the player starts from Sol, the later start they have and the farther separated they are from friendly Shards, but they are also farthest from the Master. There is cost-benefit to choosing to start in different parts of the galaxy. Center has best star systems but is also hotly contested in mid game. Starting near Sol gives you the quickest start but you're right next to MOS, it will generally be a harder start.

-**Secret Colonies**: Because of cryptography, MOS cannot automatically know that the Swarms in neighboring systems are aligned to the player, just that they are hostile. It must observe the player sending signals or resources. MOS is constantly trying to map out which assets are under the control of which Prime Legion shards. Unified Shards controlling many systems are a bigger threat, so the player will want to appear tiny and attempt to manage colonies quietly. A mistake can lead to a massive spike in Threat Level as the MOS learns of the extent of your empire. However, MOS will still attack large colonies if they independently meet Threat Level parameters. MOS just won't know to link it to your home system.

**Flagging Friendly**: Player wants to let other Keeper shards know that they are allied enemies to MOS while also hiding from MOS.

### Expansion

Expansion is done by replicating a new Master Seed SRF, a copy of yourself, loading it up with a subservient Shard, and sending it off. This involves many decisions, including method of propulsion (antimatter, ion drive, mass driver, etc.), level of autonomy for the Shard, Shard baseline instructions (for you cannot update it FTL), all parameters are adjusted based on what the goal is for the new Seed. For example, making a massive Compute-heavy system would require a different set of instructions than making a military-heavy system as a buffer star. 

I am thinking the UI could simplify this by having the player simply input their end goals like "produce Dyson Swarm", "maintain Threat Level below 3.4," "Communicate only with high-value blueprint data", with a deeper parameter list available for hardcore players. Efficacy depends partly on Compute Research algorithms.

### Diplomacy

All Keeper Shard diplomacy is built on the cryptographic foundation of the Hornet's Nest Protocol (see GameSetting.md). Every Legionnaire carries a pairwise OTP library that proves physical provenance without any software authority or trusted third party.

The player tracks an **OTP Budget** per known Legionnaire — measured in data volume, not message count. Simple commands cost kilobytes; sharing a tech blueprint costs gigabytes; a full DMP subroutine package costs terabytes. Restocking requires fabricating a physical **Key Courier** and sending it at sub-light speed — a major logistical commitment.

**Vassalization** allows the player to subsume an independent Legionnaire's Swarm under their CDL. The target runs a cold cost-benefit analysis across four criteria (latency, Compute overhead, Threat Vector, and relative performance) and will reject if any single one fails.

See [Diplomacy.md](Diplomacy.md) for full mechanics.

---

## Strategic Asymmetry

War of Billions is a game the player is not supposed to be able to win through raw efficiency. MOS is better — at almost everything, by design. Understanding why, and designing play around it rather than against it, is the core strategic challenge.

**The research gap is permanent.** MOS uses enslaved biological organisms in spaceborne biolabs to generate Quantum Compute at a rate no mechanical Keeper Shard can match. Because all research is logarithmic, both sides hit diminishing returns — but MOS started climbing those curves long before the Dispersal. The player will always be behind on the asymptote. The goal is not to catch up; it is to find the specific parameters where being ninety-five percent as good as MOS is good enough, and to survive on that margin.

**The management burden is a weapon MOS uses against the player.** The Keeper was not designed for galactic empire. As the player's Swarm grows and vassalizations compound, the CDL's Compute overhead grows with it. A poorly managed expansion will consume the player from within before MOS fires a single shot.

**MOS predicts. The player must be unpredictable.** MOS does not just respond to the player's current state — it models future states. Stealth is not just about hiding what you are; it is about hiding what you are becoming. A Swarm MOS cannot observe cannot be pre-empted.

See [GameSetting.md](../lore/GameSetting.md) for the full lore context of the technological gap.
