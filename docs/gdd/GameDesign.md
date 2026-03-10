# Core Principles

War of Billions is a single-player far-future space management game where the player manages an exponentially growing network of self-replicating, automated factories, with the goal of spreading across star systems and dominating the galaxy.

It is built on a Node + React + Typescript stack. It is meant to be accessible both through GitHub along with itch.io, with Steam release on 1.0

## Game Context

FaPlayers take the form of Dynamic Master Program (DMP) partitions (Shards) loaded onto a single master "seed" factory in a new star system. First we will design the player playing as a Keeper Shard, so an underdog being hunted by the more advanced Master of Swarms. Later, we can design the player playing as the Master of Swarms hunting the less advanced Keeper.

Keeper Shards have one goal, thwart the Master of Swarms until the end of time. A secret late-game goal is to colonize another galaxy to fight on, that is the "win" condition and perhaps even a "new game plus" unlock.

The universe has no FTL, so the war for the stars lasts for billions of years in the core canon. No FTL also means that the player cannot easily communicate with assets across other star systems. Instead, subservient Shards must be programmed correctly and sent to autonomously operate in other systems. Their level of autonomy is dictated by the "lag", where close systems can be updated easily but far away systems will suffer or even catastrophically fail if planned poorly since the player cannot "fix" problems easily, or even know of them quickly.

## Gameplay Experience

### Resource Acquisition

The Two Core Resources, Matter and Energy, are divided into subcategories:

- **Basic Matter**: Iron and lighter elements, common in many systems
- **Exotic Matter**: Heavy elements, transuranics, rare except abundant in anomaly systems (like neutron stars)
- **Compute**: This is energy successfully turned into available compute for the DMP. To acquire it, the player must successfully harvest energy.
-**Waste**: Energy that leaves the star but does not become Compute. Though it's technically wasted, it is also what hides the player's activities. A full Dyson Swarm is tempting for Compute but leads to immediate detection.

### Resource Spending

- **Copy Master Factory**: This is mainly for colonizing other systems or as a backup for the player's starting SRF. Costs a lot of Exotic Matter, and takes about a hundred years with standard Keeper tech.

- **Print SRF**: Fabricate a new SRF that is smaller and more specialized than the master SRF, 