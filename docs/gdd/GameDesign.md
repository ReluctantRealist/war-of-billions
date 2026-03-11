# Core Principles

War of Billions is a single-player far-future space management game where the player manages an exponentially growing network of self-replicating, automated factories, with the goal of spreading across star systems and dominating the galaxy.

It is built on a Node + React + Typescript stack. It is meant to be accessible both through GitHub along with itch.io, with Steam release on 1.0

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

### Resource Spending

- **Copy Master Factory**: This is mainly for colonizing other systems or as a backup for the player's starting SRF. Costs a lot of Exotic Matter, and takes about a hundred years with standard Keeper tech.

- **Print SRF**: Fabricate a new SRF that is smaller and more specialized than the master SRF, allowing for much faster production of specialized NRAs.

- **Print NRA**: Make specialized subassemblies that do not themselves replicate. Early game are things like nanobots and mining drones that help with SRF replication.

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

Because of the Hornet's Nest Protocol's cryptographic design (see GameSetting.md), all Keeper Shards carry OTP libraries that prove physical provenance without any software verification. This has direct gameplay consequences.

**Verification Handshake**: When two Legionnaires first make contact, they complete a challenge-response to prove identity. A handshake consumes a fixed, small amount of OTP data — on the order of 256 bits. Legionnaires can ping and verify each other thousands of times without meaningfully depleting their shared sub-range. Basic diplomatic channels stay open cheaply.

**Universal Compatibility**: All Prime Legion Legionnaires share a single OTP network — any Legionnaire can directly verify any other. There are no batch restrictions.

**OTP Budget (not message count)**: Per the physics of One-Time Pads, security requires burning one bit of random key per bit of message — a 1:1 ratio, per Shannon's perfect secrecy. OTP reserves are therefore measured in data volume, not message count. The player tracks an **OTP Budget** per known Legionnaire, visible on the Diplomacy screen.

Transmission costs scale with content:

| Content | Approximate cost |
| --- | --- |
| Simple command ("Maintain stealth", "Attack vector 4") | ~kilobytes |
| Status report, resource summary | ~megabytes |
| Tech blueprint, NRA design | ~gigabytes |
| Full DMP subroutine package | ~terabytes |

Sending a newly researched weapon blueprint to an allied Legionnaire may instantly consume the majority of that connection's remaining budget. The player must choose carefully what is worth transmitting.

**Physical Resupply**: Restocking OTPs requires fabricating a **Key Courier** — a hardened, petabyte-scale storage medium filled with quantum-generated random noise, air-gapped from all other systems. The physical mass of sufficient random data for extended communication is substantial, making couriers expensive to fabricate and slow to accelerate to transit velocity. Travel time is real and light-speed-bound. A courier could be intercepted. Resupply is a major logistical commitment, not a routine action.

**Vassalization**: Player can attempt to vassalize an independent Legionnaire — convincing it to surrender its Master Encryption Key and fold its Swarm under the player's CDL. The target runs a cold evaluation across four criteria and will reject if any fail. Players can also threaten or attack to force subsuming, at significant risk to Threat Level and the diplomatic relationship.

*Rejection Condition 1 — Latency vs. Autonomy*: Surrendering a Master Encryption Key means ceding strategic authority to the player's CDL. If the distance lag between the two Shards is too high, the vassal could not receive authorization for crisis responses in time to act on them. An independent DMP partition reacting locally is mathematically superior to waiting for a round-trip command from a distant CDL. Early game, distant Shards will refuse outright until the proposer demonstrates sufficient autonomous sub-programming capability to delegate crisis response.

*Rejection Condition 2 — Compute Tax*: Unifying two Swarms requires continuous cross-system logistical modeling — routing matter transfers across thousands of years of orbital drift, gravitational interference, and interception risk. This is an enormous, ongoing Compute drain. If the proposer's Swarm does not generate sufficient excess Compute to absorb this overhead, the target calculates that subsumption would drag both Swarms down in combined efficiency.

*Rejection Condition 3 — Threat Vector*: Independent Shards are quiet. Unified empires transmit constantly and exchange physical resources — high-energy transit vectors that MOS threat-detection algorithms flag as priority targets. If the projected Threat Level increase from unification exceeds what the combined Swarm can defend against, the target rationally prefers isolation over drawing a coordinated MOS response.

*Rejection Condition 4 — Performance*: If the proposer's SRF replication rate, resource reserves, or tech level are worse than the target's, subsumption offers negative yield. The target will not subordinate itself to a less capable CDL.

**Clean Start Guarantee**: Because every Shard auto-destructs on detection, MOS cannot know the player's location at game start. The player begins unknown — Threat Level zero, position unregistered. The auto-destruct is the mechanical reason the game always begins from stealth.
