# Event & Transmission Catalog

This document defines every event (`EVT_`) and message (`MSG_`) type in the game. Events and messages are the only way information travels between systems — they are light-speed-bound transmissions that arrive with real delay.

**How to use this doc:** Each entry defines what triggers the transmission, what data it carries, how it displays to the player, and its OTP cost (if encrypted). When designing a new game mechanic that generates information across systems, add its transmission type here first.

**Key distinction:**
- `EVT_` — system-generated notifications (automated reports from Shards, sensor alerts, build completions). No OTP cost — these travel on the Shard's own internal channel.
- `MSG_` — deliberate inter-Shard communications (diplomatic proposals, tech sharing, intel). These consume OTP budget because they must be encrypted against MOS interception.

---

## EVT_ Events (Automated)

For each event, copy this template:

### EVT_[NAME]

**Trigger:** *What causes this event to fire?*

**Source:** *Which system/Shard generates it?*

**Data payload:** *What information does the transmission carry? Be specific — these are the fields the UI will display.*

**Delay:** *Light-travel time from source to player's home system (variable by distance).*

**UI display:** *How does this appear to the player? Notification type, where on screen, priority level.*

**Notes:** *Edge cases, interactions with other systems.*

---

### EVT_WAKE

**Trigger:** A probe arrives at a Dormant system and begins instantiation.

**Source:** The newly activated system.

**Data payload:** System seed properties (star type, resource distribution, anomalies), MOS presence (if any), probe status.

**Delay:** Light-travel distance from new system to home system.

**UI display:** Galaxy Map notification — new system appears as Active. Transmission log entry with timestamp showing how old the data is.

**Notes:** The system may have changed significantly between wake and when the player receives this. First impressions are already outdated.

---

### EVT_BUILD_COMPLETE

**Trigger:** A queued SRF or NRA fabrication finishes.

**Source:** The system where the build occurred.

**Data payload:** Asset type, quantity, updated aggregate parameters.

**Delay:** Zero if home system. Light-travel distance if remote.

**UI display:** Build queue notification. Home system: immediate. Remote: delayed transmission log entry.

**Notes:** —

---

### EVT_HOSTILE_CONTACT

**Trigger:** MOS assets detected in or approaching a player-controlled system.

**Source:** The system under threat.

**Data payload:** Attack vector type (EW / Kinetic / Armada), estimated strength, estimated time to engagement.

**Delay:** Light-travel distance. The battle may already be over by the time the player reads this.

**UI display:** High-priority alert. CDL Suspension auto-wake trigger (if configured).

**Notes:** If MOS deploys Electromagnetic Suppression, this may be the last transmission received from that system for decades.

---

### EVT_COMBAT_RESOLVED

**Trigger:** A combat engagement in a remote system concludes.

**Source:** The surviving Shard (if any) in the affected system.

**Data payload:** Outcome (victory/defeat/partial), assets lost, assets destroyed, updated aggregate parameters, Threat Level change.

**Delay:** Light-travel distance. May arrive long after EVT_HOSTILE_CONTACT.

**UI display:** Transmission log entry with full combat summary. Galaxy Map system status update.

**Notes:** If the system was lost, no further EVT_ transmissions will arrive from it. Silence is also information.

---

### EVT_RESOURCE_THRESHOLD

**Trigger:** A resource stockpile drops below a player-configured threshold.

**Source:** The affected system.

**Data payload:** Resource type, current level, threshold value.

**Delay:** Zero if home system. Light-travel distance if remote.

**UI display:** Warning notification. CDL Suspension auto-wake trigger (if configured).

**Notes:** —

---

*Add new EVT_ types here as mechanics are designed.*

---

## MSG_ Messages (Deliberate, OTP-Encrypted)

For each message, copy this template:

### MSG_[NAME]

**Trigger:** *Player or allied Shard initiates transmission.*

**Sender/Receiver:** *Who sends, who receives.*

**Data payload:** *What information is transmitted.*

**OTP cost:** *Approximate data volume consumed from the pairwise OTP budget.*

**Delay:** *Light-travel distance between sender and receiver.*

**UI display:** *How this appears on the Diplomacy screen and/or transmission log.*

**Threat Level impact:** *Does this transmission increase detection risk?*

**Notes:** *Edge cases.*

---

### MSG_HANDSHAKE

**Trigger:** First contact between two Legionnaires, or periodic re-verification.

**Sender/Receiver:** Either Legionnaire can initiate.

**Data payload:** Shard ID, Dispersal Vector, challenge-response proof.

**OTP cost:** ~256 bits (negligible).

**Delay:** Light-travel distance between the two Shards.

**UI display:** New Legionnaire appears on Diplomacy screen with verified status.

**Threat Level impact:** Minimal — handshake is a tiny data burst.

**Notes:** Can be repeated thousands of times without meaningful OTP depletion.

---

### MSG_TECH_SHARE

**Trigger:** Player transmits a Blueprint or Algorithm to an allied Legionnaire.

**Sender/Receiver:** Player -> allied Legionnaire (or reverse).

**Data payload:** Full Blueprint or Algorithm specification.

**OTP cost:** ~gigabytes (Blueprints) to ~terabytes (full DMP subroutine packages).

**Delay:** Light-travel distance.

**UI display:** Diplomacy screen — OTP budget decreases. Transmission log entry.

**Threat Level impact:** Significant — large encrypted data transmission is detectable by MOS.

**Notes:** Receiving Shard may demand a Blueprint in return. See Diplomacy.md Tech Sharing section.

---

### MSG_TARGET_DESIGNATION

**Trigger:** Player transmits MOS Biolab coordinates to an allied Legionnaire.

**Sender/Receiver:** Player -> allied Legionnaire.

**Data payload:** Target coordinates, scan data, recommended approach vector.

**OTP cost:** ~gigabytes.

**Delay:** Light-travel distance.

**UI display:** Diplomacy screen — transmission log with target details.

**Threat Level impact:** Moderate — data volume is detectable.

**Notes:** See Diplomacy.md Intel Sharing section for the Bounce Back Effect.

---

### MSG_VASSALIZATION_PROPOSAL

**Trigger:** Player proposes vassalization to an independent Legionnaire.

**Sender/Receiver:** Player -> target Legionnaire.

**Data payload:** Proposal terms, player's current aggregate stats (for the target's evaluation).

**OTP cost:** ~megabytes.

**Delay:** Light-travel distance. The target evaluates on arrival, not on send.

**UI display:** Diplomacy screen — proposal pending, estimated arrival tick.

**Threat Level impact:** Low — small data volume.

**Notes:** Response arrives after another light-travel delay. See Diplomacy.md Vassalization section for the four rejection conditions.

---

### MSG_DIRECTIVE_UPDATE

**Trigger:** Player sends updated standing directives to a vassal or remote Shard.

**Sender/Receiver:** Player -> vassal/remote Shard.

**Data payload:** New directive set (goal parameters, priority weights, threat response rules).

**OTP cost:** ~kilobytes to ~megabytes depending on complexity.

**Delay:** Light-travel distance. The Shard operates on old directives until the update arrives.

**UI display:** Remote System Panel — directive update in transit, estimated arrival.

**Threat Level impact:** Low for simple commands. Higher for large directive packages.

**Notes:** If the update arrives during combat, the Shard may have already committed to actions based on old directives.

---

*Add new MSG_ types here as mechanics are designed.*
