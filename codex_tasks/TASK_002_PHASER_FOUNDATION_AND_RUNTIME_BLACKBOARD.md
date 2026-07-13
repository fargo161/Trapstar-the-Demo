# TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD

## Task Status

Status: **Paused — Blocked by Module Definition**

Do not hand this task to Codex and do not begin implementation until the complete reactivation gate below is satisfied and Teddy explicitly reactivates the task.

---

## Why This Task Is Paused

The intended Phaser interaction slice remains valid, but several required contracts are still Design Draft or Design Accepted.

Implementing now would force Codex to invent BASED, DPA, information behavior, TIME, resolver, runtime, infrastructure, presentation, or optional social mechanics.

This task is preserved as a future foundation target. Its implementation details must be revised against accepted focused contracts before its status returns to `Ready for Codex`.

---

## Reactivation Gate

Every required contract below must be **Implementation Ready for the selected thin slice** before coding begins.

### Required interaction contracts

```text
interaction.dpa
interaction.based
data.information
data.info_cards
information.rules
resource.time
resolver.interaction
```

### Required runtime contracts

```text
runtime.content_definitions
runtime.action_request
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

```text
presentation.blackboard contract
-> Implementation Ready before reactivation

presentation.blackboard implementation
-> produced by Task 002
```

### Conditional contracts

`infra.random` is required only when the approved slice uses randomized gameplay truth. Otherwise, the revised task must explicitly declare a deterministic non-random path.

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

## Shared Structure and Behavior Ownership

The reactivated task must preserve these owners:

| Structure or responsibility | Owning module |
|---|---|
| `InfoCard` schema | `data.info_cards` |
| Soft / Hard information state and classification | `data.information` |
| disclosure, withholding, hardening, and reveal eligibility | `information.rules` |
| `ContentDefinitions` | `runtime.content_definitions` |
| generic routing-neutral `ActionRequest` | `runtime.action_request` |
| `RuntimeState` | `runtime.state` |
| interaction validation policy | `resolver.interaction` |
| `InteractionValidationResult` | `resolver.interaction` |
| `StateChange` | `runtime.state_transition` |
| authoritative transition application | `runtime.state_transition` |
| `ResolvedOutcome` | `runtime.outcome` |
| stable identity rules | `infra.ids` |
| controlled random source | `infra.random` |
| test harness and deterministic acceptance rules | `infra.tests` |
| presentation instructions | `presentation.adapter` |
| blackboard display model and controls | `presentation.blackboard` |

A shared interface does not need to become its own module, but Codex may not silently redefine a structure owned by another contract.

### Information boundary

```text
data.info_cards
-> owns the InfoCard schema

data.information
-> owns Soft / Hard classification and information state

information.rules
-> owns disclosure, withholding, hardening,
   reveal eligibility, proposed information changes,
   and information semantic signals
```

### ActionRequest boundary

```text
presentation.adapter
-> translates player intent into a request

runtime.action_request
-> owns the generic routing-neutral ActionRequest structure

resolver.interaction
-> accepts supported interaction requests,
   owns interaction validation policy,
   and coordinates approved modules
```

`resolver.interaction` owns `InteractionValidationResult`, not a universal `ValidationResult` shared by all future resolvers.

---

## Preserved Goal

Create the smallest Phaser 3.90 + TypeScript browser foundation that proves Trapstar's contained-complexity architecture through one complete interaction:

```text
DPA + BASED player intent
-> generic ActionRequest
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
| `information.rules` | Required | The interaction must disclose, withhold, or harden information through approved rules. |
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
5. the generic ActionRequest versus resolver-specific validation boundary;
6. the information-state versus information-rules boundary;
7. selected modules and action-specific participation;
8. the included/excluded module declaration;
9. the shared ownership map;
10. proposed portable TypeScript types;
11. the responsibility of `InteractionResolver`;
12. the exact consequence order;
13. tests it will create;
14. risks, conflicts, or missing information;
15. the smallest safe implementation plan.

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
      actionRequest.ts
      runtimeState.ts
      stateTransition.ts
      seededRandom.ts          # only when infra.random is included
      systems/
        informationRules.ts
        timeSystem.ts
        [only other approved modules]
    resolution/
      interactionValidation.ts
      interactionResolver.ts
      resolvedOutcome.ts
    presentation/
      presentationAdapter.ts
    scenes/
      RuntimeBlackboardScene.ts
  test/
    interactionResolver.test.ts
```

The exact filenames may change in the approved Codex report, but ownership boundaries may not.

---

## Minimum Preserved Demo Content

The future slice should remain small:

- one player ID;
- one NPC ID;
- one location ID;
- one approved Soft Info example;
- one approved Hard Info example or hardening path;
- one simple requested result;
- one run seed only when controlled randomness is included;
- only the state values required by approved participating modules.

Use stable string IDs. Do not use Phaser objects as identity.

---

## DPA, BASED, and ActionRequest Input

The browser scene should allow only the frames and Vibes approved by focused contracts.

The Presentation Adapter may translate player input into the generic `ActionRequest` owned by `runtime.action_request`.

The generic envelope may contain approved fields such as:

```text
actionId
actionType
actorId
targetId
locationId
payload
context
```

For the interaction slice, the approved payload or context may include:

```text
frame
vibe
requestedResult
offerOrDemand
leverage
witnessIds
```

The generic request structure does not determine action validity or consequence order. No UI choice may directly mutate simulation state.

---

## Information Boundary

`data.information` and `data.info_cards` provide approved structures and state.

`information.rules` calculates or proposes only approved information consequences, such as:

```text
disclosed
withheld
hardened
reveal_ineligible
```

It must return bounded proposals, reasons, semantic signals, and debug trace. It must not directly mutate global state, calculate REP or HEAT, or issue Phaser instructions.

---

## InteractionResolver Boundary

`InteractionResolver` may:

1. receive current state, content, a generic `ActionRequest`, and controlled randomness when included;
2. verify that it accepts the request's action type;
3. produce an `InteractionValidationResult`;
4. identify Required, Optional Integration, and Not Consulted modules;
5. call approved modules in documented order;
6. combine proposed changes;
7. resolve conflicts according to its contract;
8. apply one authoritative state transition;
9. process approved secondary checks;
10. return updated state and one explicit `ResolvedOutcome`;
11. hand semantic signals to presentation after truth is established.

It must not own the generic ActionRequest schema or contain every internal BASED, Information, TIME, REP, HEAT, mission, or presentation rule.

---

## Consequence Order

The exact sequence must come from the approved Resolver Contract.

The future task must preserve:

```text
translate intent before resolution
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
- REP or HEAT only when included.

### Selected request

- generic action type;
- DPA frame;
- BASED Vibe;
- target;
- approved offer, demand, leverage, or requested-result fields.

### Last resolution

- resolver;
- `InteractionValidationResult`;
- modules Required, Optional, Not Consulted, or Excluded;
- primary result;
- information-rules result;
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
4. the generic `ActionRequest` is routing-neutral and contains no Phaser objects;
5. `InteractionValidationResult` remains interaction-specific;
6. information state and information behavior have separate owners;
7. required-module absence fails without a state transition;
8. optional-module absence follows the documented reduced path;
9. excluded and Not Consulted modules are not invoked;
10. modules return bounded calculations or proposals;
11. shared structures match their owning contracts;
12. state changes occur through one documented transition;
13. TIME uses rule data rather than animation duration;
14. semantic signals occur only after authoritative resolution;
15. reset restores the original test state.

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
- assign information behavior to a Data Model;
- make `resolver.interaction` own the generic request envelope;
- create duplicate ownership for shared structures.

---

## Reactivation Checklist

Task 002 may return to `Ready for Codex` only when:

- [ ] every required interaction contract is Implementation Ready;
- [ ] every required runtime contract, including `runtime.action_request`, is Implementation Ready;
- [ ] every required infrastructure contract is Implementation Ready;
- [ ] every required presentation contract is Implementation Ready;
- [ ] `information.rules` is separate from information data models;
- [ ] REP and HEAT are each included or explicitly excluded;
- [ ] randomness is included with an Implementation Ready contract or explicitly excluded;
- [ ] every shared structure has one recorded owner;
- [ ] the Resolver Contract defines action-specific participation and order;
- [ ] the task lists exact focused references;
- [ ] acceptance criteria match the final approved module set;
- [ ] Teddy explicitly authorizes reactivation.

---

## Preserved Architecture Principle

```text
DPA chooses the strategic frame.
BASED defines the manner of action.
ActionRequest carries routing-neutral intent.
Specialized resolvers validate and coordinate approved modules.
Rule Modules own bounded consequences.
One transition establishes authoritative truth.
ResolvedOutcome explains what happened.
Phaser presents the result.
```

```text
Commands change the world.
Events report what changed.
```
