# Trapstar the Demo

*Trapstar the Demo* is a bounded, replayable 2D social-crime investigation being developed as a seven-week browser prototype in **Phaser 3.90 + TypeScript**.

The player has three in-game days to resolve the **Stolen Package** case inside one police-monitored city block involving two factions, a limited NPC cast, shifting information, resource pressure, and bounded randomized roles.

## Core design language

- **SEN** — Structured, Emergent, Negotiated world-state philosophy.
- **Deal / Pressure / Ask** — the recurring strategic choice frame. DPA is not an ordered loop.
- **BASED** — the trait and Vibe language that defines how an action is expressed.
- **Contained complexity** — bounded modules own focused rules; specialized resolvers coordinate their intersections.

```text
DPA chooses the strategic frame.
BASED defines the manner of action.
Resolvers coordinate the required modules.
Rule modules calculate bounded consequences.
Runtime state records authoritative truth.
Phaser presents the resolved result.
```

## Current phase

The project is currently defining its modular architecture and focused system contracts before gameplay implementation begins.

There is no active implementation task. The preserved Phaser foundation task is paused until its required DPA, BASED, Information, TIME, resolver, runtime-state, state-transition, and outcome contracts are ready.

## Current technical direction

Phaser 3.90 is the committed demo engine, not the guaranteed full-project engine.

The simulation beneath Phaser is designed around portable content definitions, stable IDs, authoritative runtime state, seeded randomness, bounded rule modules, explicit action resolvers, ordered state transitions, resolved outcomes, and engine-light tests.

```text
Commands change the world.
Events report what changed.
```

## Read first

1. [`PROJECT_STATE.md`](PROJECT_STATE.md) — current phase, blockers, and documentation priorities.
2. [`docs/Trapstar_Master_System_Architecture.md`](docs/Trapstar_Master_System_Architecture.md) — canonical high-level architecture truth.
3. [`docs/architecture/Trapstar_System_Registry.md`](docs/architecture/Trapstar_System_Registry.md) — module identity, classification, maturity, activation, and authority.
4. [`docs/architecture/Trapstar_Module_Contract_Standard.md`](docs/architecture/Trapstar_Module_Contract_Standard.md) — required contract profiles and module-boundary rules.
5. [`codex_tasks/TASK_TEMPLATE.md`](codex_tasks/TASK_TEMPLATE.md) — required structure for bounded Codex work orders.
6. [`codex_tasks/TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD.md`](codex_tasks/TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD.md) — preserved future Phaser task, currently paused.

## Repository layout

```text
docs/                 Accepted design and architecture references
codex_tasks/          Bounded implementation work orders
agent_specs/          Focused runtime or agent contracts
design_packets/       Implementation-ready design packets
playtest_logs/        Test observations and iteration records
course_deliverables/  Course-facing artifacts
art/                   Source and reference art
PhaserProject/         Browser-demo implementation root
```

The repository is the canonical source of truth. Gameplay code should be produced from accepted focused contracts through bounded Codex tasks rather than improvised directly from the master architecture.