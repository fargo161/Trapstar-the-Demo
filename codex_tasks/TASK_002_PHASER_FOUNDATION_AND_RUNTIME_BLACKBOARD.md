# TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD

## Task Status

Status: **Paused — Blocked by Module Definition**

Do not hand this task to Codex and do not begin implementation until the full reactivation gate below is satisfied and Teddy explicitly reactivates the task.

---

## Why This Task Is Paused

The original task correctly identified the intended first Phaser interaction slice, but it was written before the module registry and contract standard existed.

Several required contracts remain Design Draft or Design Accepted. Implementing now would force Codex to invent BASED, DPA, Information, TIME, resolver, runtime, infrastructure, presentation, or optional social behavior.

This task is preserved as the future Phaser foundation target. Its implementation details must be revised against accepted focused contracts before its status can return to `Ready for Codex`.

---

## Reactivation Gate

Every required contract below must be **Implementation Ready for the selected thin slice** before coding begins.

### Required interaction contracts

```text
interaction.dpa
interaction.based
data.information
data.info_cards
resource.time
resolver.interaction
```

### Required runtime contracts

```text
runtime.content_definitions
runtime.state
runtime.state_transition
runtime.outcome
```

### Required infrastructure contracts

```text
infra.ids
infra.tests
```

### Required presentation contracts

```text
presentation.phaser
presentation.adapter
presentation.blackboard
```

A required contract is a design prerequisite. Its implementation may still be produced by this task after the contract is ready.

Example:

```text
presentation.blackboard contract
-> Implementation Ready before reactivation

presentation.blackboard implementation
-> produced by Task 002
```

### Conditional contracts

`infra.random` is required only when the approved slice uses randomized gameplay truth. Otherwise, the revised task must explicitly declare a fully deterministic non-random path.

`social.rep` and `social.heat` must each be either:

```text
Implementation Ready and included
```

or:

```text
explicitly excluded from the revised slice
```

No Design Draft or Design Accepted module may be implemented through invented behavior.

---

## Shared Structure Ownership

The reactivated task must preserve these owners:

| Shared structure or responsibility | Owning module |
|---|---|
| `InfoCard` schema | `data.info_cards` |
| Soft / Hard information behavior | `data.information` |
| `ContentDefinitions` | `runtime.content_definitions` |
| `RuntimeState` | `runtime.state` |
| `ActionRequest` | `resolver.interaction` |
| `ValidationResult` | `resolver.interaction` |
| `StateChange` | `runtime.state_transition` |
| authoritative transition application | `runtime.state_transition` |
| `ResolvedOutcome` | `runtime.outcome` |
| stable identity rules | `infra.ids` |
| controlled random source | `infra.random` |
| test harness and deterministic acceptance rules | `infra.tests` |
| presentation instructions | `presentation.adapter` |
| blackboard display model and controls | `presentation.blackboard` |

A shared interface does not need to become its own module, but Codex may not silently redefine an interface owned by another contract.

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

## Included and Excluded Module Declaration

Before Codex receives the task, the revised task must include a table like:

| Module | Slice status | Reason |
|---|---|---|
| `resource.time` | Required | Every approved interaction spends minutes. |
| `social.rep` | Included or Excluded | Must be decided before reactivation. |
| `social.heat` | Included or Excluded | Must be decided before reactivation. |
| `infra.random` | Included or Excluded | Include only if gameplay truth is randomized. |

Every optional or conditional module must be explicitly included or excluded. Silence is not a valid activation decision.

---

## Report Before Coding

After reactivation and before implementation, Codex must report:

1. its understanding of the approved task;
2. exact files it will read;
3. exact files it plans to create or modify;
4. the portable simulation versus Phaser presentation boundary;
5. the selected modules and action-specific participation;
6. the included/excluded module declaration;
7. the shared structure ownership map;
8. the proposed portable TypeScript types;
9. the responsibility of `InteractionResolver`;
10. the responsibility of each participating module;
11. the exact consequence order;
12. the tests it will create;
13. risks, unresolved conflicts, or missing information;
14. the smallest safe implementation plan.

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
      seededRandom.ts          # only when infra.random is included
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

The exact filenames may change in the approved Codex report, but responsibility boundaries and shared owners may not.

---

## Minimum Preserved Demo Content

The future slice should remain small:

- one player ID;
- one NPC ID;
- one location ID;
- one approved Soft Info example;
- one approved Hard Info example or hardening path;
- one run seed only when controlled randomness is included;
- one simple requested result;
- only the state values required by approved participating modules.

Use stable string IDs. Do not use Phaser objects as identity.

---

## DPA and BASED Input

The browser scene should allow only the frames and Vibes approved by the focused contracts.

The future `ActionRequest`, owned by `resolver.interaction`, should contain only approved fields, potentially including:

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

The reactivated task should implement the approved shared structures according to their owning contracts. Portable types must contain no Phaser objects.

Expected structures include:

- `ContentDefinitions`;
- `RuntimeState`;
- `ActionRequest`;
- `ValidationResult`;
- `StateChange`;
- `ResolvedOutcome`;
- semantic outcome signals;
- presentation instructions produced by the Presentation Adapter.

---

## InteractionResolver Boundary

`InteractionResolver` may:

1. receive current state, content, an ActionRequest, and controlled randomness when included;
2. validate the request;
3. identify Required, Optional Integration, and Not Consulted modules by action type;
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

The future task must preserve:

```text
validate before calculation
calculate before transition
apply one authoritative transition
process secondary checks in documented order
build one explicit outcome
translate semantic signals after resolution
restore input last
```

Real-time animation duration must not determine in-world TIME cost.

---

## Runtime Blackboard

The future blackboard should display only approved thin-slice information.

### Current state

- current day and minute when TIME participates;
- player and NPC IDs;
- current location;
- approved information state;
- run seed when randomness participates;
- REP or HEAT only when those modules are included.

### Selected request

- DPA frame;
- BASED Vibe;
- target;
- approved offer, demand, leverage, or requested-result fields.

### Last resolution

- resolver;
- validation result;
- modules Required, Optional, Not Consulted, or Excluded;
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

1. identical state, request, and seed produce identical outcomes when randomness participates;
2. a non-random slice remains deterministic without `infra.random`;
3. DPA and BASED remain separate fields and responsibilities;
4. required-module absence fails clearly without a state transition;
5. optional-module absence follows the documented reduced path;
6. excluded and Not Consulted modules are not invoked;
7. modules return bounded calculations or proposals;
8. shared structures match their owning contracts;
9. state changes occur through one documented transition;
10. TIME uses rule data rather than animation duration;
11. portable state and outcomes contain no Phaser objects;
12. semantic signals occur only after authoritative resolution;
13. reset restores the original test state.

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
- invent rules from Design Draft or Design Accepted documents;
- create duplicate ownership for shared structures.

---

## Reactivation Checklist

Task 002 may return to `Ready for Codex` only when:

- [ ] every required interaction contract is Implementation Ready;
- [ ] every required runtime contract is Implementation Ready;
- [ ] every required infrastructure contract is Implementation Ready;
- [ ] every required presentation contract is Implementation Ready;
- [ ] REP and HEAT are each included or explicitly excluded;
- [ ] randomness is included with an Implementation Ready contract or explicitly excluded;
- [ ] every shared structure has one recorded owner;
- [ ] the Resolver Contract defines action-specific Required, Optional Integration, and Not Consulted participation;
- [ ] the task lists exact focused references;
- [ ] acceptance criteria match the final approved module set;
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