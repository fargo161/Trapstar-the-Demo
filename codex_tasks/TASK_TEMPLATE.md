# Codex Task Template

Use this template for every Codex implementation task in *Trapstar the Demo*.

Codex should treat each task file as a bounded work order. Do not expand scope beyond the task, and do not implement directly from `PROJECT_STATE.md` alone.

---

## Task Name

`TASK_###_SHORT_NAME`

Example:

`TASK_002_RUNTIME_BLACKBOARD`

---

## Task Status

Status: Draft / Ready for Codex / In Progress / Complete / Blocked

---

## Goal

Describe one concrete, testable outcome.

Example:

> Create a minimal Phaser/browser runtime blackboard that displays portable Structured state, Emergent pressure, and the result of one DPA + BASED test action.

---

## Project Context

Before starting, read:

- `PROJECT_STATE.md`
- `docs/Trapstar_Master_System_Architecture.md` when the task touches core systems, SEN, DPA, BASED, assets, information, time, simulation, presentation, or portability

Current technical direction:

- Phaser 3.90
- TypeScript
- browser build
- portable simulation separated from Phaser presentation

DPA is not an ordered loop.

```text
Deal     = Logos / Structured / hard reality
Pressure = Pathos / Emergent / dynamic force
Ask      = Ethos / Negotiated / social opening
```

BASED colors the approach; it does not replace the DPA frame.

---

## Files to Read First

List only the files Codex must read.

Required:

- `PROJECT_STATE.md`

Optional task-specific context:

- `docs/Trapstar_Master_System_Architecture.md`
- `docs/...`
- `agent_specs/...`
- `design_packets/...`
- previous `codex_tasks/...`

---

## Files to Create or Modify

Use exact paths where possible.

Example:

```text
PhaserProject/src/simulation/state/GameState.ts
PhaserProject/src/simulation/actions/resolveAction.ts
PhaserProject/src/presentation/scenes/DebugScene.ts
PhaserProject/src/presentation/ui/RuntimeBlackboard.ts
PhaserProject/tests/resolveAction.test.ts
```

Do not modify unrelated files.

---

## Simulation / Presentation Ownership

State which side owns each change.

### Portable simulation

Use for:

- game state and rules
- action validation and resolution
- deterministic randomness
- world consequences
- save-ready plain data
- tests that should run without a Phaser scene

Portable simulation files must not import Phaser.

### Phaser presentation

Use for:

- scenes, sprites, input, collision, cameras, animation playback, UI, audio, and browser delivery
- converting player input into simulation requests
- displaying simulation results

Do not store direct Phaser objects as game-state truth.

---

## Non-Goals

List what Codex must not do.

Common examples:

- Do not build the full dialogue system.
- Do not add live LLM/API calls.
- Do not implement final art.
- Do not create unbounded procedural generation.
- Do not redesign unrelated architecture.
- Do not add packages unless explicitly required.
- Do not create a multi-engine abstraction framework.
- Do not move portable game rules into Phaser scenes.

---

## Required Behavior

Describe concrete, testable behavior.

Example:

- Display current day and minute.
- Display police HEAT and faction pressure.
- Display the last DPA frame and BASED Vibe.
- Trigger one deterministic test action.
- Show the action outcome and reason.
- Update portable state without mutating Phaser objects.
- Log the same state change in the browser console.
- Allow simple development-only test controls.

---

## Structured / Emergent / Negotiated Check

### Structured

What hard state does the task create, expose, or modify?

### Emergent

What pressure, reaction, or changed situation does the task create, expose, or modify?

### Negotiated

What Deal / Pressure / Ask choice and BASED approach does the task expose or resolve?

### Consequence

What state changes after resolution?

---

## Portability Check

Answer explicitly:

- Which files contain portable game truth?
- Which files are Phaser-specific?
- Are stable string IDs used instead of sprite or scene references?
- Is gameplay randomness controlled and reproducible where required?
- Can core resolution be tested without loading Phaser?
- Does saved or persistent state remain plain, versionable data?

---

## Debug / Logging Requirements

Every runtime system should make its behavior legible.

Possible requirements:

- browser-console logs
- on-screen debug values
- reason strings explaining state changes
- deterministic seed display
- development-only hidden state
- test buttons or keyboard controls
- last DPA frame and BASED approach
- before/after values

Example:

```text
HEAT changed 2 -> 3.
Reason: Pressure + Menacing used in a monitored public location.
Seed: demo-0007.
```

---

## Browser Test Steps

Describe exactly how Teddy should test the result.

Example:

1. Open a terminal in `PhaserProject/`.
2. Install dependencies only when the task introduces or requires them.
3. Run the task-defined development or test command.
4. Open the local browser build.
5. Confirm the debug view appears.
6. Trigger the test action.
7. Confirm the DPA frame and BASED approach update.
8. Confirm the portable state changes.
9. Confirm the browser console and on-screen reason agree.
10. Run the task-defined build, type-check, and test commands.

Do not invent commands that the repository does not yet define.

---

## Acceptance Criteria

This task is complete only when:

- requested files exist
- task-defined build/type-check/tests pass
- required browser behavior works
- debug output is visible and understandable
- portable simulation is separated from Phaser presentation
- no Phaser objects are stored as game-state truth
- DPA and BASED remain distinct
- no unrelated systems are expanded
- testing steps are reproducible

---

## Report Before Coding

Before making changes, Codex must report:

1. Its understanding of the task.
2. Files it plans to read.
3. Files it plans to create or modify.
4. Simulation-owned versus presentation-owned changes.
5. Risks, ambiguities, or missing contracts.
6. The smallest safe implementation plan.

Codex should not begin implementation until the plan is approved.

---

## Implementation Notes

After approval:

- Make the smallest useful change.
- Prefer simple TypeScript over clever architecture.
- Keep simulation functions deterministic and testable where practical.
- Keep Phaser-specific work close to presentation.
- Avoid premature optimization and dependencies.
- Use comments where they clarify boundaries.
- Preserve the current direction in `PROJECT_STATE.md`.

---

## Completion Report

After implementation, report:

1. Files created or modified.
2. Behavior implemented.
3. Portable simulation changes.
4. Phaser presentation changes.
5. Build/type-check/test results.
6. Browser test steps.
7. Known limitations.
8. Recommended next bounded task.
9. Any SEN, DPA, or BASED behavior introduced or changed.
