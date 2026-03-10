# Technical Design

The galaxy is simulated to a realistic scale, so many billions of systems. 

It is generated in a way similar to No Man's Sky, with a mathematical seed creating a static coordinate system for stars and anomalies.

The player will be "blind" until they spend Compute on Intel, so the "billions of systems" exist as empty placeholders until the player experience requires data.

Stars do not move in the first version of the game.

## System Lifecycle

Every star system exists in one of three states:

- **Dormant** — seed-only. No save data. All properties (star type, resource distribution, anomalies, MOS presence probability) are derived deterministically from the galaxy seed and the system's coordinates. Costs nothing to store.
- **Waking** — a probe is in transit. The system does not yet exist in the save file. Its seed-derived properties are pre-calculated client-side when the player views the probe's trajectory.
- **Active** — a probe has arrived and transmitted. The system is instantiated from its seed, timestamped with the in-game year of wake, and written to the save file. From this point it is simulated forward.

### Wake Event

When a probe arrives at a Dormant system, it triggers a wake event:

1. System state is generated from seed (star, resources, anomalies, any pre-existing MOS infrastructure)
2. A wake timestamp is recorded (in-game year)
3. The probe's transmission is queued — it reaches the player after a delay equal to the light-travel time from that system
4. The player receives the transmission as an `EVT_` notification, potentially followed by `MSG_` comms if MOS is present

The player's intel is already out of date the moment it arrives. A system 200 light-years away sends a signal that takes 200 years to arrive — what the player sees is the system as it was, not as it is.

### MOS Presence

MOS presence in a system is determined by seed but treated as pre-existing history. If MOS is present at wake, the system generates with infrastructure and activity already in place — as though MOS arrived long before the probe. The player cannot know when MOS actually arrived; at interstellar distances, this is unknowable.

### Save File Scope

Only Active systems are written to the save file. Dormant systems are pure seed — they cost nothing. This means save file size scales with player activity, not galaxy size, and remains manageable even in late game.
