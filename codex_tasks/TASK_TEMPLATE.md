# Codex Task Template

Use this template for every Codex implementation task in *Trapstar the Demo*.

Each task is a bounded work order. Codex must not expand scope beyond the accepted task and must not implement directly from `PROJECT_STATE.md` or the master architecture alone.

---

## Task Name

```text
TASK_###_SHORT_NAME
```

Example:

```text
TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD
```

---

## Task Status

Status: Draft / Ready for Codex / In Progress / Complete / Blocked

---

## Goal

Describe one concrete, testable outcome.

Example:

> Create a minimal Phaser 3.90 + TypeScript foundation that submits one DPA + BASED action request through an `InteractionResolver`, applies an ordered state transition, returns a `ResolvedOutcome`, and displays the result in a runtime blackboard.

---

## Project Context

Before starting, read:

- `PROJECT_STATE.md`
- `docs/Trapstar_Master_System_Architecture.md`
- this task file
- only the focused subsystem references named by this task

Core relationships:

```text
SEN = world-state philosophy
DPA = strategic frame
BASED = manner of action
Resolver = cross-system coordinator
Bounded systems = focused rule owners
Runtime state = authoritative mutable truth
Resolved outcome = explicit result record
Phaser = input and presentation runtime
```

DPA is not an ordered loop.

```text
Deal     = Logos / Structured / hard reality
Pressure = Pathos / Emergent / dynamic force
Ask      = Ethos / Negotiated / social opening
```

Governing rules:

```text
Commands change the world.
Events report what changed.
```

```text
Action Request
-> Resolver
-> Bounded Systems
-> Ordered State Transition
-> Resolved Outcome
-> Phaser Presentation / Notifications
```

---

## Files to Read First

List exact paths only.

Required:

```text
PROJECT_STATE.md
docs/Trapstar_Master_System_Architecture.md
codex_tasks/TASK_###_SHORT_NAME.md
```

Optional task-specific references:

```text
docs/...
agent_specs/...
design_packets/...
previous codex_tasks/...
```

Do not scan or rewrite unrelated files without a stated reason.

---

## Files to Create or Modify

Use exact paths when possible.

Example:

```text
PhaserProject/src/data/contentDefinitions.ts
PhaserProject/src/simulation/runtimeState.ts
PhaserProject/src/resolution/actionRequest.ts
PhaserProject/src/resolution/resolvedOutcome.ts
PhaserProject/src/resolution/interactionResolver.ts
PhaserProject/src/presentation/presentationAdapter.ts
PhaserProject/src/scenes/RuntimeBlackboardScene.ts
PhaserProject/test/interactionResolver.test.ts
```

Identify which files are:

- portable simulation;
- content data;
- Phaser presentation;
- tests;
- configuration.

---

## Architecture Ownership Check

Complete this section before coding.

### Content Definitions

Which files describe relatively stable game content?

### Runtime State

Which files own mutable authoritative truth?

### Action Request

What structured player or system intent enters resolution?

### Resolver

Which specialized resolver coordinates the action?

### Independent Systems

Which focused rule systems participate, and what does each own?

### State Transition

What changes become authoritatively true, and in what order?

### Resolved Outcome

What explicit record is returned for tests, logs, and presentation?

### Phaser Presentation

Which Phaser objects gather input or display results without owning core rules?

### Events

Which events report completed changes after resolution?

---

## Non-Goals

List explicit exclusions.

Common non-goals:

- Do not build the full dialogue system.
- Do not build the full mystery generator.
- Do not add live LLM or external API calls.
- Do not implement final art or final UI.
- Do not add unrelated Social Assets or BASED abilities.
- Do not redesign the accepted architecture.
- Do not add third-party packages unless explicitly approved.
- Do not create a universal `TrapstarManager` or `GameStateManager` that owns unrelated systems.
- Do not store Phaser scenes, sprites, cameras, containers, animation objects, or physics bodies in portable runtime state or save data.
- Do not let independent systems directly command unrelated systems.
- Do not implement authoritative consequences through uncontrolled event-listener chains.
- Do not let animation duration determine in-world TIME cost.
- Do not let a resolver absorb the internal rules of every participating system.

---

## Required Behavior

Describe concrete, testable behavior.

For each meaningful action specify:

1. Input action request.
2. Validation conditions.
3. Resolver used.
4. Systems consulted.
5. Controlled randomness, if any.
6. Primary outcome.
7. Ordered state changes.
8. TIME cost.
9. Secondary consequences.
10. Resolved-outcome fields.
11. Presentation cues.

---

## Data and Portability Requirements

When relevant, require:

- stable string IDs;
- plain TypeScript data structures;
- JSON-compatible content definitions;
- versionable save-compatible state;
- controlled seeded randomness;
- no direct Phaser references in portable state;
- explicit action-request and outcome types;
- simulation tests that run without a Phaser scene.

---

## Structured / Emergent / Negotiated Check

### Structured

What hard-tracked truth does this task create, expose, or change?

### Emergent

What pressure, reaction, instability, or opportunity does it create or expose?

### Negotiated

What DPA frame and BASED manner can the player choose?

### Consequence

What state changes, TIME costs, secondary checks, and future situations result?

---

## Debug and Logging Requirements

Every runtime feature should make cause and effect legible.

Include, when relevant:

- action-request summary;
- resolver name;
- validation result;
- systems consulted;
- old and new values;
- reason strings;
- run seed or deterministic random trace;
- ordered state-transition entries;
- secondary consequences;
- last DPA frame;
- last BASED Vibe;
- emitted presentation events;
- debug-only hidden mission truth.

Example:

```text
InteractionResolver accepted Pressure + AB_Menacing.
REP: 1 -> 0. Reason: public intimidation.
HEAT: 2 -> 3. Reason: two witnesses in monitored location.
TIME: +12 minutes.
Outcome event emitted: npc_recoils, hud_heat_changed, dialogue_disclosure.
```

---

## Automated / Simulation Test Steps

Describe tests that do not require a Phaser scene where practical.

Example:

1. Create a fixed `RuntimeState` and run seed.
2. Submit a known `ActionRequest`.
3. Resolve through the named resolver.
4. Assert validation.
5. Assert the exact ordered state changes.
6. Assert TIME and secondary consequences.
7. Assert the `ResolvedOutcome` fields.
8. Run the same seed again and confirm the same result.

---

## Browser / Phaser Test Steps

Describe exactly how Teddy should test the browser build.

Example:

1. Install dependencies.
2. Run the development server.
3. Open the runtime-blackboard scene.
4. Select a DPA frame and BASED Vibe.
5. Submit the action.
6. Confirm the visible state matches the resolved outcome.
7. Confirm dialogue, HUD, audio, camera, or animation cues occur only after resolution.
8. Confirm no browser-console errors.

---

## Acceptance Criteria

A task is complete only when:

- requested files exist;
- TypeScript compiles;
- relevant automated tests pass;
- the browser build runs without errors;
- the required behavior is reproducible;
- portable simulation logic does not depend on a Phaser scene;
- authoritative state changes are traceable through the resolver and outcome;
- consequence order is visible and testable;
- events report completed changes rather than secretly owning critical rules;
- DPA and BASED remain distinct;
- no unrelated systems were expanded;
- known limitations are documented.

---

## Report Before Coding

Before making changes, Codex must report:

1. What it understands the task to be.
2. Which files it will read.
3. Which files it plans to create or modify.
4. The simulation-versus-presentation boundary.
5. The resolver and bounded systems involved.
6. The expected consequence order.
7. Risks, ambiguities, or missing information.
8. The smallest safe implementation plan.

Codex must wait for approval before implementation when Teddy's task instructions require a report-and-confirm step.

---

## Implementation Notes

After approval, Codex should:

- make the smallest useful change;
- prefer plain TypeScript and readable data structures;
- keep systems focused;
- keep resolvers explicit and small;
- avoid premature abstraction and optimization;
- avoid external dependencies unless necessary;
- add comments only where they clarify ownership or ordering;
- preserve stable IDs and portable state;
- preserve the distinction between SEN, DPA, and BASED;
- update tests and documentation when behavior changes.

---

## Completion Report

After implementation, Codex must report:

1. Files created or modified.
2. Behavior implemented.
3. Resolver used.
4. Independent systems touched.
5. Authoritative state changes and consequence order.
6. Resolved-outcome fields and events emitted.
7. Automated tests run and results.
8. Browser test steps.
9. Known limitations.
10. Recommended next task.
11. Whether the simulation/presentation boundary changed.
12. Whether any Phaser-specific dependency entered portable state.
13. Whether any DPA frame or BASED behavior changed.
