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

See [TechTree.md](TechTree.md) for the full list of Compute Sinks and their Algorithm fixes.

### Blueprints and Technology

Technology is divided into Matter and Compute (see TechTree.md).

### Swarm Infrastructure

The player's CDL must be physically housed somewhere. As the Swarm grows, the choice between a fortified central core and a fully distributed mesh becomes the defining mid-game architectural decision — with direct consequences for Threat Level, survivability, build cost, and expansion speed. The late-game endpoint is the Matrioshka Brain: the star fully encased in layered distributed compute.

See [Infrastructure.md](Infrastructure.md) for full stages and strategy trade-offs.

### Stealth Management

**Threat Level** is MOS's prioritization of the player for elimination. See [Combat.md](Combat.md) for the mechanical definition and how Threat Level combines with MOS Presence to determine attack likelihood.

**Delayed Punishment**: Threat Level can be high for a long time before MOS can mobilize assets to hit the player. If it sees rapid early growth, the player can feel "safe" — but the strike will come later, and harder, because MOS knows.

**Distance from Sol**: Sol is MOS's home system. Starting farther away means a later start and more isolation from friendly Shards, but also distance from MOS. The galactic center has the best star systems but is hotly contested in mid game. Near Sol gives the quickest start but the hardest opening.

**Secret Colonies**: MOS cannot automatically know that Swarms in neighboring systems are aligned to the player — only that they are hostile. It must observe signals or resource transfers. MOS constantly maps which assets belong to which Legionnaire. The player should appear small and manage colonies quietly. A mistake can spike Threat Level massively as MOS discovers the true extent of the empire. However, MOS will still attack large colonies that independently meet Threat Level thresholds — it just won't link them to the player's home system.

**Flagging Friendly**: The player wants to signal allied status to other Keeper Shards while remaining hidden from MOS.

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

MOS is better than the player at almost everything — by design. Its biolab-driven research, purpose-built CDL architecture, and predictive modeling create a permanent, compounding advantage. The player cannot win through raw efficiency. Victory requires deception, unpredictability, and exploiting the speed of light as a shield.

See [GameSetting.md](../lore/GameSetting.md) for the full context of the technological gap, and [Combat.md](Combat.md) for how the asymmetry plays out in engagements.

---

## Emergent Gameplay

The following is a target example of intended systems-based emergent play — showing how the game's mechanics should combine without scripting.

### The Smash and Grab

**Setup:** Use a Cold-burn Mass Driver to silently transit a Seed SRF into a resource-rich Dormant system. No detectable exhaust signature. MOS does not observe the launch.

**Strip mine:** On Wake Event, the CDL queues Disposable Flux Harvesters and mining NRAs — Blueprints with high `Reclaim_Yield` and 1-tick `Disassembly_Time`. The system runs hot and loud. Threat Level climbs. This is intentional: the player is ringing the dinner bell.

**The trap:** Decades before MOS Hunter-Killers arrive, the CDL triggers the Plasma Arc Crucible. All mining infrastructure melts in one tick. The recovered Basic Matter is immediately converted into Combat NRAs — Area-Denial Mine Fields and Point Defense Arrays seeded throughout the system.

**The payoff:** MOS arrives expecting a vulnerable mining colony and flies into a prepared kill zone. Because no physical Key Courier or resource convoy was ever sent back to the home system, MOS has no signal chain to follow. It cannot link this system to the player's home Shard.

**MOS counter-play:** If MOS detects the trap pattern before the Armada arrives, it deploys an Electromagnetic Suppression Array — see [Combat.md](Combat.md). The system goes dark. The local Shard fights on autonomous programming alone, and the player learns the outcome only when the jamming ends.
