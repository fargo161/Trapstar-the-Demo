# TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD

## Task Status

Status: **Paused — Blocked by Module Definition**

Do not hand this task to Codex and do not begin implementation until the prerequisites below are satisfied and Teddy explicitly reactivates the task.

---

## Why This Task Is Paused

The original task correctly identified the intended first Phaser interaction slice, but it was written before the module registry and contract standard existed.

Several participating modules are still Design Drafts. Implementing now would require Codex to invent BASED, DPA, Information, TIME, REP, HEAT, resolver, state-transition, or outcome behavior.

This task is preserved as the future Phaser foundation target. Its implementation details must be revised against accepted focused contracts before its status can return to `Ready for Codex`.

---

## Reactivation Prerequisites

The selected thin slice requires sufficient contracts for:

```text
interaction.dpa
interaction.based
data.information
resource.time
resolver.interaction
runtime.state
runtime.outcome
runtime.state_transition
```

Before reactivation:

- `interaction.dpa` must be Implementation Ready for the selected frame behavior.
- `interaction.based` must be Implementation Ready for the selected test Vibes.
- `data.information` must be Implementation Ready for the selected Soft / Hard Info behavior.
- `resource.time` must be Implementation Ready for the selected action costs.
- `resolver.interaction` must define accepted actions, participating modules, validation, consequence phases, transition policy, and outcome responsibility.
- `runtime.state`, `runtime.outcome`, and `runtime.state_transition` must be Implementation Ready for the thin slice.
- `social.rep` and `social.heat` must each be either Implementation Ready and included or explicitly excluded from the revised task.

No Design Draft module may be implemented through invented behavior.

---

## Preserved Goal

Create the smallest Phaser 3.90 + TypeScript browser foundation that proves Trapstar's contained-complexity architecture through one complete interaction:

```text
DPA + BASED Action Request
-> InteractionResolver
-> approved bounded modules
-> ordered authoritative state transition
-> explicit ResolvedOutcome
-> Phaser runtime-blackboard presentation
```

The future task is complete when a tester can choose an approved DPA frame, select an approved BASED Vibe, submit an action, and see an explicit deterministic resolution trace and updated state in the browser.

---

## Required Reading After Reactivation

```text
PROJECT_STATE.md
docs/Trapstar_Master_System_Architecture.md
docs/architecture/Trapstar_System_Registry.md
docs/architecture/Trapstar_Module_Contract_Standard.md
codex_tasks/TASK_TEMPLATE.md
codex_tasks/TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD.md
```

The reactivated task must also list only the focused module references required by the approved thin slice.

---

## Report Before Coding

After reactivation and before implementation, Codex must report:

1. Its understanding of the approved task.
2. Exact files it will read.
3. Exact files it plans to create or modify.
4. The portable simulation versus Phaser presentation boundary.
5. The selected modules and their activation roles for each test action.
6. The proposed portable TypeScript types.
7. The responsibility of `InteractionResolver`.
8. The responsibility of each participating module.
9. The exact consequence order.
10. The tests it will create.
11. Risks, unresolved conflicts, or missing information.
12. The smallest safe implementation plan.

Codex must wait for Teddy's approval after this report.

---

## Expected Project Root

```text
PhaserProject/
```

Preferred high-level structure after reactivation:

```text
PhaserProject/
  package.json
  tsconfig.json
  vite.config.ts
  index.html
  src/
    main.ts
    data/
      demoContent.ts
    simulation/
      runtimeState.ts
      stateTransition.ts
      seededRandom.ts
      systems/
        [only approved modules]
    resolution/
      actionRequest.ts
      resolvedOutcome.ts
      interactionResolver.ts
    presentation/
      presentationAdapter.ts
    scenes/
      RuntimeBlackboardScene.ts
  test/
    interactionResolver.test.ts
```

The exact filenames may change in the approved Codex report, but the responsibility boundaries may not.

---

## Minimum Preserved Demo Content

The future slice should remain small:

- one player ID;
- one NPC ID;
- one location ID;
- one approved Soft Info example;
- one approved Hard Info example or hardening path;
- one run seed when controlled randomness is used;
- one simple requested result;
- only the state values required by approved participating modules.

Use stable string IDs. Do not use Phaser objects as identity.

---

## DPA and BASED Input

The browser scene should allow only the frames and Vibes approved by the focused contracts.

The future `ActionRequest` should contain only approved fields, potentially including:

```text
actorId
targetId
actionType
frame
vibe
requestedResult
offerOrDemand
leverage
locationId
witnessIds
```

No UI choice may directly mutate simulation state.

---

## Portable Types

The reactivated task should define small plain-data types for the approved slice, expected to include:

- `ContentDefinitions`
- `RuntimeState`
- `ActionRequest`
- `ValidationResult`
- `StateChange`
- `ResolvedOutcome`
- semantic outcome signals
- presentation instructions produced by the Presentation Adapter

Portable types must contain no Phaser objects.

---

## InteractionResolver Boundary

`InteractionResolver` may:

1. receive current state, content, an ActionRequest, and controlled randomness when approved;
2. validate the request;
3. identify required and optional modules by action type;
4. call modules in the documented order;
5. combine proposed changes;
6. resolve conflicts according to its contract;
7. apply one authoritative state transition;
8. process approved secondary checks;
9. return updated state and one explicit `ResolvedOutcome`;
10. hand semantic signals to presentation after truth is established.

It must not contain every internal BASED, Info, TIME, REP, HEAT, inventory, mission, or presentation rule.

---

## Consequence Order

The exact sequence must come from the approved Resolver Contract.

The future task must still preserve these principles:

```text
validate before calculation
calculate before transition
apply one authoritative transition
process secondary checks in a documented order
build one explicit outcome
translate semantic signals after resolution
restore input last
```

Real-time animation duration must not determine in-world TIME cost.

---

## Runtime Blackboard

The future blackboard should display only the approved thin-slice information, including:

### Current state

- run seed when relevant;
- current day and minute when TIME participates;
- player and NPC IDs;
- current location;
- approved information state;
- REP or HEAT only when those modules are included.

### Selected request

- DPA frame;
- BASED Vibe;
- target;
- approved offer, demand, leverage, or requested-result fields.

### Last resolution

- resolver;
- validation result;
- modules consulted;
- modules skipped or excluded;
- primary result;
- proposed and applied changes;
- ordered secondary checks;
- semantic outcome signals;
- presentation instructions.

### Controls

- approved frame selection;
- approved Vibe selection;
- submit action;
- reset fixed state;
- replay with the same seed when applicable.

---

## Automated Test Requirements

After reactivation, test at minimum:

1. Identical state, request, and seed produce identical outcomes when randomness participates.
2. DPA and BASED remain separate fields and responsibilities.
3. Required-module absence fails clearly without a state transition.
4. Optional-module absence follows the documented reduced path.
5. Modules return bounded calculations or proposals.
6. State changes occur through one documented transition.
7. TIME uses rule data rather than animation duration.
8. Portable state and outcomes contain no Phaser objects.
9. Semantic signals occur only after authoritative resolution.
10. Reset restores the original test state.

---

## Non-Goals

Do not:

- build final movement or traversal;
- build the full Stolen Package generator;
- create full NPC AI;
- create a full dialogue engine;
- implement all 20 Vibes;
- implement modules not approved for the slice;
- implement combat;
- implement final save/load;
- add production art;
- add live LLM/API calls;
- create a universal manager;
- hide simulation logic in Phaser scenes or event listeners;
- invent rules from Design Draft documents.

---

## Reactivation Checklist

Task 002 may return to `Ready for Codex` only when:

- [ ] the System Registry identifies every participating module;
- [ ] each required module is Implementation Ready for the selected slice;
- [ ] REP and HEAT are each included or explicitly excluded;
- [ ] the Resolver Contract defines action-specific activation and order;
- [ ] the runtime and outcome contracts are explicit;
- [ ] the task lists exact focused references;
- [ ] acceptance criteria match the approved module set;
- [ ] Teddy explicitly authorizes reactivation.

---

## Preserved Architecture Principle

```text
DPA chooses the strategic frame.
BASED defines the manner of action.
Resolvers coordinate approved modules.
Modules own bounded consequences.
One transition establishes authoritative truth.
ResolvedOutcome explains what happened.
Phaser presents the result.
```

```text
Commands change the world.
Events report what changed.
```