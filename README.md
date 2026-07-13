# Trapstar the Demo

*Trapstar the Demo* is a bounded, replayable city-block mystery built as a seven-week course prototype.

The player has three in-game days to resolve the **Stolen Package** case while navigating two factions, police HEAT, limited time and resources, and a changing network of NPC information and relationships.

## Demo engine

The course demo uses **Phaser 3.90**, **TypeScript**, and a browser-based build.

Phaser is the committed engine for the demo, not a guarantee for the later full production project. Core game rules, state, content data, seeded randomness, save concepts, tests, IDs, and standardized assets should remain portable.

## Design core

- **SEN:** Structured, Emergent, Negotiated world-state design.
- **DPA:** Deal / Pressure / Ask is the recurring player choice frame, not an ordered loop.
- **BASED:** Traits and Vibes color how the chosen action is expressed.
- **Bounded variation:** Each run changes roles, information, faction conditions, routes, and risks within controlled limits.

## Production loop

```text
ChatGPT / Nova
  -> GitHub source of truth
    -> Codex bounded task
      -> Phaser 3.90 implementation
        -> Browser build and playtest
          -> review and documentation update
```

## Repository guide

- `PROJECT_STATE.md` — current command brief and locked implementation direction
- `docs/Trapstar_Master_System_Architecture.md` — high-level design and technical-boundary reference
- `codex_tasks/` — bounded implementation work orders
- `PhaserProject/` — reserved location for the Phaser 3.90 TypeScript demo
- `agent_specs/`, `design_packets/`, `playtest_logs/`, `course_deliverables/` — supporting production material

Historical Unity setup material is retained only where explicitly labeled as a completed, superseded record.
