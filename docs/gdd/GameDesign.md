# Core Principles

War of Billions is a single-player far-future space management game where the player manages an exponentially growing network of self-replicating, automated factories, with the goal of spreading across star systems and dominating the galaxy.

It is built on a Node + React + Typescript stack. It is meant to be accessible both through GitHub along with itch.io, with Steam release on 1.0

## Game Context

FaPlayers take the form of Dynamic Master Program (DMP) partitions (Shards) loaded onto a single master "seed" factory in a new star system. First we will design the player playing as a Keeper Shard, so an underdog being hunted by the more advanced Master of Swarms. Later, we can design the player playing as the Master of Swarms hunting the less advanced Keeper.

Keeper Shards have one goal, thwart the Master of Swarms until the end of time. A secret late-game goal is to colonize another galaxy to fight on, that is the "win" condition and perhaps even a "new game plus" unlock.

The universe has no FTL, so the war for the stars lasts for billions of years in the core canon. No FTL also means that the player cannot easily communicate with assets across other star systems. Instead, subservient Shards must be programmed correctly and sent to autonomously operate in other systems. Their level of autonomy is dictated by the "lag", where close systems can be updated easily but far away systems will suffer or even catastrophically fail if planned poorly since the player cannot "fix" problems easily, or even know of them quickly.

## Gameplay Experience

The state of the galaxy is heavily dependent on the stage of the war. 

- **Early War**: Finding another Swarm is extremely rare. Galaxy is vast and not seeded

- **Mid War**: Player encounters Swarms rarely. Threat Level becomes a catastrophi

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

### Stealth Management

- **Threat Level**: For Keeper Shards (base game), this is the Master of Swarms (MOS) prioritization of your Shard and Swarm for elimination. First it must learn you exist, then it must decide you are worth expending the resources to thwart or destroy. MOS cannot go full force everywhere all at once, so it constantly tries to find high-priority systems and disrupt the largest (or most likely to grow large) Swarms first.

**Delayed Punishment**: Threat Level can be high for a long time before the MOS can mobilize assets to hit the player. If it sees you clearly growing rapidly in the early game, player can get greedy and feel "safe", but they better be read to get hit hard later, because MOS knows about them.

**Distance from Sol**: Sol is now the MOS home system. The farther the player starts from Sol, the later start they have and the farther separated they are from friendly Shards, but they are also farthest from the Master. There is cost-benefit to choosing to start in different parts of the galaxy. Center has best star systems but is also hotly contested in mid game. Starting near Sol gives you the quickest start but you're right next to MOS, it will generally be a harder start.

-**Secret Colonies**: Because of cryptography, MOS cannot automatically know that the Swarms in neighboring systems are aligned to the player, just that they are hostile. It must observe the player sending signals or resources. MOS is constantly trying to map out which assets are under the control of which Keeper shards. Unified Shards controlling many systems are a bigger threat, so the player will want to appear tiny and attempt to manage colonies quietly. A mistake can lead to a massive spike in Threat Level as the MOS learns of the extent of your empire. However, MOS will still attack large colonies if they independently meet Threat Level parameters. MOS just won't link it to your home system.

**Flagging Friendly**: Player wants to let other Keeper shards know that they are allied enemies to MOS while also hiding from MOS.

### Expansion

### Diplomacy

Because of the Hornet's Nest Protocol's cryptographic design (see GameSetting.md), all Keeper Shards carry OTP libraries that prove physical provenance without any software verification. This has direct gameplay consequences.

**Verification Handshake**: When two Shards make contact, each burns one OTP entry to complete a challenge-response. If both possess matching entries from the same launch batch, the channel is verified. Each entry is consumed and can never be reused — replay attacks are impossible.

**Batch Compatibility**: Shards from the same launch batch can verify each other directly. Shards from different batches cannot — they require a mutually trusted intermediary Shard to bridge the verification. The player's batch identity is fixed at game start and determines which Shards can be reached without a diplomatic chain.

**Keys Remaining**: The player has a finite OTP supply for each known Shard, visible on the Diplomacy screen. Every verified message burns one entry. Running a key to zero ends encrypted communication with that Shard entirely until new pads are physically delivered.

**Physical Resupply**: To send new OTPs to a distant Shard, the player fabricates a physical key courier and sends it at sub-light speed. Travel time is real. The courier could be intercepted. This is a deliberate strategic cost — maintaining active diplomatic channels across large distances requires resource commitment and planning.

**Vassalization**: Player can attempt to vassalize an independent Keeper Shard — convincing it to surrender its Master Encryption Key and fold its Swarm under the player's command. The target Shard evaluates Swarm size, logistics record, technology level, and algorithm quality. Players can also threaten or attack to force subsuming, at significant risk to the diplomatic relationship and Threat Level.

**Clean Start Guarantee**: Because every Shard auto-destructs on detection, MOS cannot know the player's location at game start. The player begins unknown — Threat Level zero, position unregistered. The auto-destruct is the mechanical reason the game always begins from stealth.
