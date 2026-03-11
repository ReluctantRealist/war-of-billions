# Combat

Latency determines agency. The player's ability to intervene in a battle is directly proportional to their physical proximity to it. In the home system, the CDL is present — orders are instantaneous, responses are live. In a remote system, every command is light-speed-bound and may arrive centuries after the battle ends. The same attack vector plays out differently depending on where it lands.

## MOS Combat Advantage

MOS does not win fights with a single superior weapon. It wins because its logistics are fractionally more efficient, its transit routes fractionally more accurate, and its predictive modeling centuries ahead of what a Legionnaire can compute. A four-percent efficiency gap in propulsion or heat dissipation is imperceptible in a single engagement. Compounded across a Swarm of billions operating over millions of years, it becomes an insurmountable logistical lead. See [GameSetting.md](../lore/GameSetting.md) for the full context of the technological asymmetry.

The player's defense against being predicted is the same as their defense against being found: stay dark, stay irregular, and never let MOS observe enough of the Swarm to model the rest.

---

## Attack Likelihood

MOS does not attack randomly. Two independent variables combine to determine whether a given system comes under attack on any given tick:

- **Threat Level** — MOS prioritization of the player's empire for elimination. Driven by Swarm size, transmission volume, resource transit signatures, and how much MOS knows about the player's extent. A system with low Threat Level is simply not worth the resources to hit.
- **MOS Presence** — the density of MOS assets in the region surrounding a system. A system deep in contested space with high local MOS concentration can be attacked even at moderate Threat Level, simply because the assets to do so are already nearby.

Neither alone guarantees attack. High Threat Level in a region MOS has not yet reached buys time. Low Threat Level in a heavily-seeded MOS region still carries ambient risk. Managing both — staying quiet while also not expanding into MOS-saturated space carelessly — is the strategic tension.

---

## Attack Vectors

MOS uses three distinct attack vectors, escalating in cost, commitment, and permanence. MOS selects based on the assessed value of the target, available local assets, and its own logistical constraints.

---

### Electronic Warfare (EW)

**What it is:** MOS floods a star system with broadband electromagnetic noise — targeted interference designed to degrade the Shard's ability to coordinate its own Swarm. It does not destroy assets directly. It induces entropy.

**How MOS deploys it:** EW is the cheapest attack vector. MOS can sustain it from a distance using purpose-built NRA emitter arrays, without committing mobile assets to the system. It is the first escalation MOS reaches for when Threat Level crosses a threshold but the system is not yet worth a full strike.

**What it attacks:** Logistics coordination between SRFs and NRAs. Replication scheduling. Matter routing. The Shard's ability to execute build queues. At high intensity, it can degrade the CDL's ability to receive its own transmissions from within the system.

---

### Kinetic Warfare

**What it is:** MOS accelerates mass — dense, hardened impactors — to relativistic velocities and aims them at the player's system. No propulsion system is active during transit. No signal is emitted. The impactors travel in silence for decades or centuries before arriving.

**How MOS deploys it:** Kinetic strikes are launched from MOS mass driver installations, which may be many light-years away. Once launched, they cannot be recalled or redirected. The player may receive no warning at all — the first indication of a strike is the transmission from the impacted system, already light-travel-time delayed.

**What it attacks:** Physical infrastructure. SRFs, NRA arrays, energy harvesting installations. A kinetic strike does not conquer a system — it craters it. MOS uses kinetic warfare to set back a growing Swarm without committing a full armada, or as a first strike before a follow-up Armada arrives.

---

### Armada

**What it is:** MOS commits a fleet of hunter-killer probes — purpose-built combat NRAs — to transit to the player's system and engage the Swarm directly. The Armada does not withdraw. It fights until it wins or is destroyed.

**How MOS deploys it:** An Armada is expensive. MOS must fabricate the probes, accelerate them to transit velocity, and commit them on a journey that may take centuries. It only does this when a system is assessed as high enough value — or high enough threat — to justify the investment. An Armada is a strategic decision by MOS, not a routine response.

**What it attacks:** Everything. Hunter-killers target SRFs first, then NRAs, then energy harvesting infrastructure. A successful Armada does not just damage a system — it occupies it. MOS probes remain to prevent reseeding. A conquered system stays conquered unless the player can route a counter-strike from a neighboring system.

---

## Home System Combat

*[To be designed. The player has live CDL access and can issue direct orders during an engagement. This section will cover what orders are available, at what CDL tick rate, and what remains outside the player's control even at home.]*

---

## Remote System Combat

Once an attack is in progress at a remote system, the player cannot intervene directly. The Swarm executes its standing combat directives autonomously. The player watches the engagement unfold through delayed transmissions — the battle may already be over by the time they learn it started.

The player's influence is entirely in the preparation:

- What NRAs were built and in what quantities
- What standing directives the local Shard was given
- What defensive infrastructure was invested in before the attack arrived

See [TechTree.md](TechTree.md) for the Combat NRA and Stealth & Detection blueprints that directly affect combat outcomes.
