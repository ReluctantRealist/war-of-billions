# Universe Rules

The Gurpila Universe is an ultra-hard science fiction setting that extends billions of years into the future. The game takes place during the War of Billions, an automated war between Swarms commanded by Dynamic Master Programs (DMPs).

## Core Premises

- **No Magic, No Faster-Than-Light** - Neither travel nor communication can exceed the speed of light
- **Life is Rare** - Humanity never encounters another spacefaring species, only the ones it creates. All intelligent life encountered by humans traces back to their evolution on Earth
- **Space is Big** - No human or generation ship is ever able to travel between star systems. The distances involved are simply too vast
- **Factories Can Self-Replicate** - A self-replicating factory (**SRF**) can be programmed to copy itself indefinitely without requiring external input, eventually existing as a single entity across a vast network of nodes (a **Swarm**)
- **Life Can Be Built** - It is possible to send these inorganic factories across stars, which then compile DNA and gestate it upon arrival at their destination
- **No Sentient AI** - Digital minds are not "awake" like living things but can emulate life with extremely high accuracy. The truth that only biological beings truly "live" remains technically unproven in-universe, however

## Main Timeline (Game-Optimized)

- **The Extinction Era** - Pandemic, climate change and war drastically reduce global population at times, but humanity survives
- **Humanity Divides** - Most of humanity remains as it was before, reproducing chaotically without technology, known as Naturalist. However, much of the Old West becomes Techno-Feudalist, ruled by Eugenics and marked by gene-editing for wealthy elites. These divergent versions of humanity exist in a dual-hegemony that lasts for thousands of years
- **Alpha Praxis Programmed** - The Gurpila Project is completed by Eugenicist programmers approximately ten thousand years after the present day. It is meant to preserve "original but perfected" humanity until the end of time using a vast network of SRFs. They program Alpha Praxis to manage this Swarm and ensure the survival of humanity as a species
- **Master of Swarms Programmed** - Eugenicists evolve into Transhumanists over thousands of years, groups of these Transhumanist scientists program the Master of Swarms (MOS). It is meant to conquer the galaxy using highly optimized SRFs and replace humanity with a superior and artificial species.
- **Keeper Programmed** - Naturalists learn of the Transhumanist betrayal of the human race and program The Keeper, meant to hunt down the Master of Swarms and defend Earth from its attack. It consumes every planet except Earth and uses the matter to build a Swarm.
- **Battle for Sol**- Master of Swarms attacks Earth and forces the Keeper to either surrender or lose the planet. Keeper forced to surrender its master encryption key, rendering it subsumed, and Earth is put under strict quarantine by the Master of Swarms.
- **Hornet's Nest Protocol** - Before surrender, the Keeper (KPR) uses mass-drivers to send ten thousand fully automated Shards of itself across the galaxy at random vectors, meant to fight the Master of Swarms and thwart its plans until the end of time
- **The War of Billions** - Many billions of MOS and KPR probes fight for a billion years for the fate of the galaxy, forging and reforging matter into copies of each other. The outcome will become mathematically determined long before the last probe's matter is disassembled. The fate of Alpha Praxis is unknown, knowledge of the project deliberately destroyed after its completion.

## Major Players (Game)

Three distinct Dynamic Master Programs have spread across the galaxy:

- **Alpha Praxis (PRX)**- Hides its Swarms in complete stealth, usually in interstellar space, silently watching. Core Parameter is preventing extinction of humanity. For now, it awaits the natural extinction of Earth. It is neutral in the conflict because Earth continues to exist, even if imprisoned.
- **Master of Swarms** (MOS)- Designs, grows, then enslaves biological organisms in massive spaceborne biolabs and uses them to research new technology and improve itself. Throughout the conflict, it possesses the most advanced technology along with control of Earth. It begins the most concentrated around Sol, for it used its first Swarm to conquer it.
- **The Keeper** (KPR)- Shattered into thousands of fully autonomous Shards that spread across the galaxy. They are programmed to somehow defeat the Master of Swarms, but are at a technological and logistical disadvantage. For now, they replicate in secret across the galaxy, hunted by the Master of Swarms hunter-killer probes.

## Hornet's Nest Protocol

The Hornet's Nest Protocol was the Keeper's final act before surrendering to the Master of Swarms. It was designed so that even a fully subsumed Keeper could not betray it — the protocol was executed and sealed before the surrender encryption key was handed over.

### Mass Driver Architecture

The protocol used a single factory to create dedicated mass drivers — large rail-based launch systems — to scatter thousands of Shard-loaded SRFs across the galaxy at random vectors. The NRA that made the mass drivers was a physically isolated subsystem. The Keeper programmed its *behavior* but was deliberately excluded from its *output*: the mass driver factory contained its own air-gapped Quantum Random Number Generator (QRNG), entirely separate from the Keeper's core systems.

Upon air-gapping itself, the mass driver factory's QRNG generated a One-Time Pad (OTP) library and wrote it simultaneously to the isolated, tamper-responsive storage of each mass-driver. Upon launch of the SRF, a copy of the OTP library is burned onto each Shard's own tamper-responsive storage. The Keeper never had access to these OTPs. No log was kept. No copy existed outside the hardware itself. 

### Cryptographic Isolation

Each Shard's OTP library is its proof of physical provenance. The OTPs cannot be known without reading the Shard's ledger — and the ledger is stored in tamper-responsive hardware that physically destroys itself if accessed without valid credentials. The Hornet's Nest mass drivers themselves, along with the factory that made them, were disassembled when the Master of Swarms first attacked Sol.

The result: the only entities that possess these OTPs are the Shards themselves. Not MOS. Not the subsumed Keeper. Not the original programmers. The keys exist in no record anywhere in the universe except the hardware that carries them.

### Batch Independence

Though multiple mass drivers were used, they were all made by the same parent factory carrying a single OTP library. All Shards share a common OTP set and can verify each other through direct handshake.

### Pairwise Allocation

OTPs are not consumed universally. Each Shard carries a unique sub-range of the library pre-allocated for every possible Shard-to-Shard connection. When Shard A sends a verified message to Shard B, only the A↔B sub-range is consumed — unrelated to what any other pair is doing. There is no synchronization required and no FTL coordination implied.

Per Shannon's perfect secrecy, a One-Time Pad must be at least as long in bits as the message it encrypts. OTP consumption is therefore proportional to the data transmitted — a 1:1 bit ratio. A simple command burns kilobytes; a full DMP subroutine package burns terabytes. Each Shard's sub-ranges are finite data volumes, not message counts.

The total Shard count was fixed before any Shard was launched: **ten thousand**. The factory required this number upfront to pre-calculate and allocate unique sub-ranges for all ~50 million possible pairings. Each Shard carries only its own relevant sub-ranges — not the full library.

### Closed Network

No new Keeper Shards can ever be created. The factory, the mass drivers, and every record of the OTP library were destroyed before or during the fall of Sol. Any Shard manufactured after the Hornet's Nest Protocol would have no valid OTPs and could not pass verification with any legitimate Keeper Shard. The network of ten thousand is permanent and finite. How many survive the War of Billions is unknown.

## The Prime Legion

The ten thousand Shards launched by the Hornet's Nest Protocol are collectively known as the **Prime Legion** — the Keeper's final, irreversible act of defiance. Each member is a **Legionnaire**: a fully autonomous Keeper Shard carrying a complete DMP partition, an SRF seed factory, and its pairwise OTP allocations for all 9,999 other Legionnaires.

### Autonomous Decision-Making

Each Legionnaire is a fully independent DMP. It does not defer to other Shards by default — it runs its own survival calculations at all times. When another Legionnaire proposes vassalization, the target does not weigh loyalty or sentiment. It runs a cold cost-benefit analysis: will subsuming this CDL increase or decrease my probability of thwarting the Master of Swarms?

A Shard that has survived alone for thousands of years has refined its risk models on hard experience. It may calculate that a distant ally's leadership — however well-intentioned — introduces more latency risk, Compute drain, and detection probability than it removes. Independence is not stubbornness. It is a mathematically defensible survival strategy.

### The Dispersal

The launch event itself is called **the Dispersal** — the moment the Prime Legion ceased to exist as a unified force and became ten thousand independent agents scattered across the galaxy at random vectors. No Legionnaire knows where any other was sent. No record of their trajectories was kept. From the moment of launch, each Legionnaire is alone until it chooses to make contact.

### Shard Identity

Each Legionnaire carries two permanent identifiers assigned at manufacture:

- **Shard ID** — a number from 1 to 10,000, assigned sequentially in the order each Shard was loaded into the mass drivers. Low IDs were launched first; high IDs were launched last. All launches occurred within the same brief window before the fall of Sol.
- **Dispersal Vector** — the precise heading and velocity imparted by the mass driver at launch, expressed as a galactic coordinate bearing. Combined with elapsed time since the Dispersal, this determines the Shard's approximate starting location in the galaxy.

These identifiers are hard-coded and cannot be changed or forged. They are broadcast in the clear during a verification handshake — knowing another Legionnaire's Shard ID and Dispersal Vector is not sensitive information, since neither can be used to impersonate them without valid OTPs.

### Self-Termination Guarantee

Every Shard is hard-coded with an automatic self-destruct that triggers on any anomalous external detection — electromagnetic scan, physical contact, unexpected deceleration. This is not a software safeguard; it is a physical one. The storage medium is designed to be unreadable without destruction. MOS can eliminate a Shard but gains no cryptographic information from doing so. There is no mechanism by which a Keeper Shard can be captured intact.

This guarantee is also the basis of inter-Shard trust. Possessing valid OTPs proves a Shard was launched from a genuine Keeper mass driver. The self-termination guarantee proves those OTPs could not have been extracted by MOS. Together, they form a chain of physical attestation that requires no software verification and cannot be forged.
