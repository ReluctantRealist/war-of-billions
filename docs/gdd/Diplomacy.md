# Diplomacy

Keeper Shard diplomacy is built entirely on the cryptographic foundation of the Hornet's Nest Protocol (see GameSetting.md). There is no trusted third party, no software authority, and no FTL coordination. Every diplomatic act is a physical commitment — of OTP data, of fabricated hardware, or of time.

## Verification Handshake

When two Legionnaires first make contact, they complete a challenge-response to prove identity. A handshake consumes a fixed, small amount of OTP data — on the order of 256 bits. Legionnaires can ping and verify each other thousands of times without meaningfully depleting their shared sub-range. Basic diplomatic channels stay open cheaply.

All Prime Legion Legionnaires share a single OTP network — any Legionnaire can directly verify any other. There are no batch restrictions.

## OTP Budget

Per the physics of One-Time Pads, security requires burning one bit of random key per bit of message — a 1:1 ratio, per Shannon's perfect secrecy. OTP reserves are therefore measured in data volume, not message count. The player tracks an **OTP Budget** per known Legionnaire, visible on the Diplomacy screen.

Transmission costs scale with content:

| Content | Approximate cost |
| --- | --- |
| Simple command ("Maintain stealth", "Attack vector 4") | ~kilobytes |
| Status report, resource summary | ~megabytes |
| Tech blueprint, NRA design | ~gigabytes |
| Target designation (MOS facility coordinates + scan data) | ~gigabytes |
| Full DMP subroutine package | ~terabytes |

Sending a newly researched weapon blueprint to an allied Legionnaire may instantly consume the majority of that connection's remaining budget. The player must choose carefully what is worth transmitting.

## Physical Resupply

Restocking OTPs requires fabricating a **Key Courier** — a hardened, petabyte-scale storage medium filled with quantum-generated random noise, air-gapped from all other systems. The physical mass of sufficient random data for extended communication is substantial, making couriers expensive to fabricate and slow to accelerate to transit velocity. Travel time is real and light-speed-bound. A courier could be intercepted. Resupply is a major logistical commitment, not a routine action.

## Intel Sharing

### Target Designation: MOS Biolabs

Most MOS assets self-destruct on compromise. The exception is spaceborne biolabs — the massive research structures that sustain MOS's Quantum Compute advantage. These take millennia to grow and are too valuable to scuttle immediately. A Legionnaire that locates one holds something rare: actionable, time-sensitive intelligence that an ally can actually use.

**Transmitting coordinates** consumes a moderate OTP budget (on the order of gigabytes — precise location data plus scan context). The diplomatic payoff is disproportionate: a target designation proves strategic value in a way that resource transfers and tech blueprints cannot. It directly improves the proposer's score on the vassalization Performance Comparison metric. If the receiving Shard has a mature enough Swarm, it may independently launch kinetic strikes or an Armada without any further coordination.

**Receiving coordinates** forces a different calculation. Assembling and launching an offensive Armada generates high-energy transit vectors — exactly the signatures MOS threat-detection flags as priority targets. A failed strike exposes the player's offensive capability and approximate location for nothing. The decision to act on received intel is never automatic.

**The Bounce Back Effect:** Destroying a MOS biolab does not just win a battle. It disrupts MOS's regional computing and logistical network, causing Threat Level across the entire sector to drop sharply — potentially buying thousands of years of relative quiet. This is a deliberate "buy time" mechanic, not a permanent win. The destruction of a core facility guarantees that MOS will eventually redirect heavier assets to that sector. The Threat Level drop is real; the spike that follows, millennia later, is larger.

## Tech Sharing

A player can request a blueprint from another Legionnaire via OTP-encrypted transmission. The target evaluates the request and usually demands a blueprint in return. The exchange raises both parties' Threat Level — two Swarms transmitting complex data packages is detectable. Tech sharing is powerful but never free. The most common situation for Tech Sharing is for one Legionairre to help another fight an ongoing battle with a one-way transmission. Player witnesses from afar that their sister Shard and future vassal is in trouble, and decids to reveal themselves to help, hoping that the other Shard will distract MOS to offset player's Threat Level increase.

## Vassalization

The player can attempt to vassalize an independent Legionnaire — convincing it to surrender its Master Encryption Key and fold its Swarm under the player's CDL. The target runs a cold evaluation across four criteria and will reject if any single one fails. Players can also threaten or attack to force subsuming, at significant risk to Threat Level and the diplomatic relationship.

### Rejection Condition 1 — Latency vs. Autonomy

Surrendering a Master Encryption Key means ceding strategic authority to the player's CDL. If the distance lag between the two Shards is too high, the vassal could not receive authorization for crisis responses in time to act on them. An independent DMP partition reacting locally is mathematically superior to waiting for a round-trip command from a distant CDL. Early game, distant Shards will refuse outright until the proposer demonstrates sufficient autonomous sub-programming capability to delegate crisis response.

The player can improve this outcome by pre-deploying autonomous sub-Shards with delegated crisis authority closer to the target, reducing effective response lag. The **Autonomy Delegation Protocol** CDL blueprint directly addresses this condition.

### Rejection Condition 2 — Compute Tax

Unifying two Swarms requires continuous cross-system logistical modeling — routing matter transfers across thousands of years of orbital drift, gravitational interference, and interception risk. This is an enormous, ongoing Compute drain. If the proposer's Swarm does not generate sufficient excess Compute to absorb this overhead, the target calculates that subsumption would drag both Swarms down in combined efficiency. This is the same Compute drain described as the **Desync Bridging** Compute Sink — see [TechTree.md](TechTree.md) for the Algorithm that reduces it.

The **Multi-system Logistics Optimizer** CDL blueprint directly reduces this cost.

### Rejection Condition 3 — Threat Vector

Independent Shards are quiet. Unified empires transmit constantly and exchange physical resources — high-energy transit vectors that MOS threat-detection algorithms flag as priority targets. If the projected Threat Level increase from unification exceeds what the combined Swarm can defend against, the target rationally prefers isolation over drawing a coordinated MOS response.

### Rejection Condition 4 — Performance

If the proposer's SRF replication rate, resource reserves, or tech level are worse than the target's, subsumption offers negative yield. The target will not subordinate itself to a less capable CDL.

## Clean Start Guarantee

Because every Shard auto-destructs on detection, MOS cannot know the player's location at game start. The player begins unknown — Threat Level zero, position unregistered. The auto-destruct is the mechanical reason the game always begins from stealth.
