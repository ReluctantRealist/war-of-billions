# Save File Schema

This document defines the exact JSON structure of save files. It is the single source of truth for what gets serialized to disk. When writing save/load code, implement this schema directly.

**How to use this doc:** Define every field before writing serialization code. If a new mechanic adds persistent state, add its fields here first, then implement. See [TechnicalDesign.md](TechnicalDesign.md) for the save architecture (compression, versioning, migration strategy).

**Format:** Compressed JSON via pako. Written to disk via Electron file system API.

---

## Top-Level Structure

```jsonc
{
  "save_version": 1,
  "saved_at": "",          // ISO 8601 timestamp (real-world save time)
  "current_tick": 0,       // Current in-game year

  "galaxy": { },           // Galaxy seed and generation parameters
  "player": { },           // Player identity and starting parameters
  "home_system": { },      // Full-fidelity home system state
  "active_systems": { },   // All remote active systems (aggregate parameters)
  "transmissions": [ ],    // In-flight signals not yet arrived
  "diplomacy": { },        // Known Legionnaires, OTP budgets, vassal states
  "research": { },         // Quantum Compute allocation and progress
  "cdl": { },              // CDL algorithm states and Compute accounting
  "threat": { }            // Global Threat Level and MOS attention state
}
```

---

## Section Definitions

Define every field in each section. For each field include: name, type, description, and default value.

### galaxy

```jsonc
{
  "seed": "",              // string — master seed for deterministic galaxy generation
  "star_count": 0          // number — total stars (derived from seed, stored for validation)
}
```

### player

```jsonc
{
  "shard_id": 0,           // number (1-10000) — player's Prime Legion ID
  "dispersal_vector": "",  // string — galactic coordinate bearing at launch
  "start_tick": 0          // number — in-game year when the player's SRF arrived
}
```

### home_system

*Full-fidelity state — individual asset tracking, not aggregate parameters.*

```jsonc
{
  "system_id": "",         // string — deterministic ID from galaxy seed
  "star_type": "",         // string — spectral class
  "resources": {
    "basic_matter": 0,     // number — current stockpile
    "exotic_matter": 0,    // number — current stockpile
    "compute": 0,          // number — current available compute this tick
    "waste": 0             // number — waste energy this tick
  },
  "assets": [ ],           // array — individual SRFs and NRAs (home system only)
  "build_queue": [ ],      // array — fabrication jobs in progress
  "infrastructure": "",    // string — current housing stage ("seed", "monolithic", "mesh", "matrioshka")
  "threat_level": 0,       // number — local Threat Level
  "event_queue": [ ]       // array — pending local events
}
```

### active_systems

*Keyed by system_id. Each entry uses aggregate parameters, not individual assets.*

```jsonc
{
  "[system_id]": {
    "star_type": "",
    "wake_tick": 0,                  // number — in-game year the system was activated
    "shard_autonomy_level": "",      // string — autonomy configuration
    "standing_directives": { },      // object — current directive set
    "aggregate": {
      "compute_generation": 0,       // number — total compute output per tick
      "defensive_strength": 0,       // number — combined combat rating
      "srf_replication_rate": 0,     // number — SRFs produced per tick
      "basic_matter_stockpile": 0,
      "exotic_matter_stockpile": 0,
      "threat_level": 0
    },
    "event_queue": [ ],              // array — scheduled future events
    "last_transmission_tick": 0      // number — tick of most recent EVT_ sent
  }
}
```

### transmissions

*All in-flight signals. Sorted by arrival_tick.*

```jsonc
[
  {
    "type": "",            // string — "EVT_WAKE", "MSG_TECH_SHARE", etc.
    "source_system": "",   // string — system_id of sender
    "target_system": "",   // string — system_id of receiver (usually home)
    "sent_tick": 0,        // number — in-game year transmitted
    "arrival_tick": 0,     // number — in-game year it arrives
    "payload": { }         // object — content (defined per type in Events.md)
  }
]
```

### diplomacy

```jsonc
{
  "known_legionnaires": {
    "[shard_id]": {
      "verified": false,         // boolean — handshake completed?
      "otp_budget_remaining": 0, // number — bytes of OTP data left
      "relationship": "",        // string — "independent", "vassal", "allied", "hostile"
      "last_contact_tick": 0,    // number — tick of last MSG_ received
      "location_known": false,   // boolean — do we know their system?
      "location_system_id": ""   // string — system_id if known
    }
  },
  "key_couriers_in_transit": [ ] // array — fabricated couriers with destination and arrival_tick
}
```

### research

```jsonc
{
  "quantum_compute_pool": 0,     // number — total QC available this tick
  "allocations": {
    "metallurgy": 0,             // number — QC allocated this tick
    "propulsion": 0,
    "combat_nra": 0,
    "galaxy_simulation": 0,
    "stealth_detection": 0,
    "cdl_algorithms": 0
  },
  "progress": {
    "metallurgy": { "depth": 0, "likelihood": 0 },
    "propulsion": { "depth": 0, "likelihood": 0 },
    "combat_nra": { "depth": 0, "likelihood": 0 },
    "galaxy_simulation": { "depth": 0, "likelihood": 0 },
    "stealth_detection": { "depth": 0, "likelihood": 0 },
    "cdl_algorithms": { "depth": 0, "likelihood": 0 }
  },
  "unlocked_blueprints": [ ],   // array — Blueprint IDs earned
  "unlocked_algorithms": [ ]    // array — Algorithm IDs earned
}
```

### cdl

```jsonc
{
  "active_algorithms": [ ],      // array — Algorithm IDs currently running
  "total_compute_upkeep": 0,     // number — sum of all Algorithm upkeep costs
  "compute_sinks": {
    "n_body_orbital": 0,         // number — current cost per tick
    "relativistic_trajectory": 0,
    "ledger_verification": 0,
    "thermodynamic_balancing": 0,
    "desync_bridging": 0
  },
  "suspension": {
    "is_suspended": false,
    "wake_on": {
      "hostile_contact": true,
      "incoming_message": false,
      "resource_threshold": null,  // number or null
      "probe_arrival": false,
      "build_complete": false,
      "timer_ticks": null          // number or null
    }
  }
}
```

### threat

```jsonc
{
  "global_threat_level": 0,      // number — MOS's overall assessment of the player
  "mos_attention_budget": 0,     // number — MOS resources currently allocated against the player
  "last_spike_tick": 0,          // number — tick of most recent major Threat Level increase
  "decay_rate": 0                // number — per-tick reduction when player is inactive
}
```

---

## Versioning & Migration

- `save_version` increments on every breaking schema change
- On load: check version, run sequential migrations (`v1 -> v2 -> v3`, etc.)
- During early development: wipe saves on breaking changes instead of migrating
- Migration functions become mandatory approaching public playable builds

See [TechnicalDesign.md](TechnicalDesign.md) for implementation details.
