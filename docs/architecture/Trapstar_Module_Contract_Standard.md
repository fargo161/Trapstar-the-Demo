# Trapstar Module Contract Standard

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Standard structure and behavioral contract for modular design and implementation references  
**Status:** Architecture Draft  
**Last updated:** 2026-07-13

---

## 1. Purpose

This standard defines how every modular part of *Trapstar the Demo* should be documented and implemented.

The goal is to let systems be added, refined, disabled, deferred, replaced, or removed without turning the project into one tightly coupled block.

A module contract should make four things obvious:

1. what the module owns;
2. what it does not own;
3. what it receives and returns;
4. what should happen when it is unavailable.

This standard applies to rule modules, data models, resolvers, scenario modules, presentation boundaries, and infrastructure modules. Design philosophies such as SEN may use a lighter version because they do not own runtime rules.

---

## 2. Governing Architecture Rules

Every module contract must preserve these project rules:

```text
Commands change the world.
Events report what changed.
```

```text
Action Request
-> Resolver
-> Bounded Modules
-> Ordered State Transition
-> Resolved Outcome
-> Presentation / Notifications
```

Required principles:

- One module owns one bounded category of responsibility.
- A module may calculate or propose changes within its responsibility.
- A module does not directly mutate unrelated module state.
- A resolver coordinates cross-module actions.
- A resolver does not absorb every module's internal rules.
- One authoritative transition applies accepted state changes.
- Presentation does not create gameplay truth.
- Phaser objects never become portable state or stable identity.
- Gameplay randomness is controlled and reproducible.
- Optional modules have explicit absence behavior.
- Missing required modules fail visibly and safely.

---

## 3. Required Contract Header

Every focused module reference should begin with:

```markdown
# Module Name

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `category.module_name`  
**Module kind:** Rule Module / Data Model / Resolver / Scenario Module / Presentation Module / Infrastructure Module  
**Status:** Core / Design Draft / Implementation Ready / Prototype Active / Optional / Deferred / Experimental / Superseded / Removed  
**Activation role:** Required / Optional Integration / Deferred Integration  
**Detailed authority:** This file controls the module-specific rules described below.  
**Last updated:** YYYY-MM-DD
```

A module ID should be stable, lowercase, and namespaced.

Examples:

```text
interaction.based
social.heat
resource.time
resolver.interaction
runtime.outcome
presentation.blackboard
```

File names may change later. Module IDs should change only when the conceptual identity changes.

---

## 4. Required Contract Sections

Every implementation-facing module reference should contain the following sections.

### 4.1 Purpose

Explain the one problem the module exists to solve.

Good:

> The HEAT module calculates police-attention changes and threshold consequences.

Too broad:

> The HEAT module manages police, crime, factions, NPC fear, missions, movement, and combat.

### 4.2 Owns

List the rules or data for which this module is the authority.

Example:

```text
Owns:
- action-minute cost calculation
- current-time advancement proposals
- time-threshold checks owned by TIME
- reason strings for TIME changes
```

### 4.3 Does Not Own

State boundaries explicitly.

Example:

```text
Does not own:
- animation duration
- NPC schedule relocation
- mission failure
- HEAT changes
- Phaser clocks
```

Another module or resolver may use TIME output to process those effects, but TIME should not perform them secretly.

### 4.4 Inputs

List the plain-data inputs the module may read.

Include:

- required fields;
- optional fields;
- stable IDs;
- relevant current-state slices;
- relevant content definitions;
- controlled random input, if permitted.

A module should receive the smallest useful context rather than unrestricted access to the whole game whenever practical.

### 4.5 Outputs

List the plain-data output shape.

A rule module should generally return a calculation or proposal, not directly alter global state.

Example:

```text
{
  moduleId,
  accepted,
  proposedChanges,
  reasons,
  secondaryChecks,
  presentationCues,
  debugTrace
}
```

The exact TypeScript shape belongs in an implementation-ready contract or task.

### 4.6 State Read

List which authoritative state fields the module is allowed to inspect.

### 4.7 State Changes Proposed

List which state paths the module may propose changing.

This is an ownership boundary, not permission to mutate immediately.

### 4.8 Required Dependencies

List modules without which this module cannot function.

Required dependencies should be few and explicit.

### 4.9 Optional Integrations

List modules that may add context or consequences but are not necessary for the module's minimum function.

### 4.10 Called By

List the resolvers or lifecycle processes allowed to invoke the module.

### 4.11 May Call

Rule modules should normally call no unrelated rule modules.

If a call is necessary, document why it is not better handled by a resolver.

### 4.12 Validation and Failure Behavior

Specify what happens when:

- required input is missing;
- an ID is invalid;
- the action is not permitted;
- a required module is unavailable;
- optional context is absent;
- numeric data is outside the valid range;
- content and runtime state disagree.

Failures should return explicit data rather than silently doing nothing.

### 4.13 Determinism

State whether the module:

- is fully deterministic;
- may use a controlled random source;
- must record random draws or seed position;
- must produce the same result for the same inputs and seed.

Direct uncontrolled randomness is prohibited for gameplay truth.

### 4.14 Consequence Order

Explain where the module participates in the relevant resolver sequence.

The module should not determine the full global order unless consequence ordering is its specific responsibility.

### 4.15 Presentation Cues

List non-authoritative cues the module may propose after resolution.

Examples:

```text
hud_heat_changed
npc_recoils
info_disclosed
time_advanced
```

Presentation cues do not mutate authoritative state.

### 4.16 Events

List events that may report completed results.

Events must not become the hidden owner of critical state changes.

### 4.17 Tests

List the minimum tests needed before implementation can be considered complete.

### 4.18 Open Questions

Record unresolved design details. Codex must not invent answers to open questions unless a task explicitly authorizes a bounded placeholder.

### 4.19 Change Impact

Identify which other module contracts, tasks, save fields, tests, or presentation cues may need review if this module changes.

---

## 5. Standard Contract Template

Use this template for a focused module reference:

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Module kind:** `[kind]`  
**Status:** `[status]`  
**Activation role:** `[role]`  
**Detailed authority:** This file controls [specific authority].  
**Last updated:** `[date]`

---

## 1. Purpose

## 2. Owns

## 3. Does Not Own

## 4. Inputs

### Required

### Optional

## 5. Outputs

## 6. State Read

## 7. State Changes Proposed

## 8. Required Dependencies

## 9. Optional Integrations

## 10. Called By

## 11. May Call

## 12. Validation and Failure Behavior

## 13. Determinism

## 14. Consequence Order

## 15. Presentation Cues

## 16. Events

## 17. Tests

## 18. Open Questions

## 19. Change Impact

## 20. Definition of Ready

## 21. Definition of Done
```

---

## 6. Data Ownership Rules

### 6.1 Definitions versus runtime state

```text
Content Definitions = what something is
Runtime State = what is currently true
Rule Module = how truth may change
Resolver = which modules participate and in what order
Presentation = how the result is shown
```

A content definition should not contain mutable run truth.

Runtime state should not contain Phaser scenes, sprites, cameras, animation objects, containers, physics bodies, DOM nodes, or event emitters.

### 6.2 Values versus systems

A value is not automatically a system.

Examples:

- `heat: 3` is state.
- HEAT calculation and threshold logic belong to `social.heat`.
- `currentMinute: 480` is state.
- action cost and time advancement belong to `resource.time`.

### 6.3 Stable identity

Modules should exchange stable IDs and plain data.

Good:

```text
actorId: "npc_marvin"
locationId: "location_center_store"
```

Avoid:

```text
actorSprite: Phaser.GameObjects.Sprite
locationScene: Phaser.Scene
```

---

## 7. Required and Optional Module Behavior

### 7.1 Required dependency unavailable

```text
required module missing
-> validation fails
-> no authoritative transition
-> explicit failure outcome
-> debug trace names missing module
```

### 7.2 Optional integration unavailable

```text
optional module missing or disabled
-> skip its calculation
-> do not fabricate a default consequence
-> record that it was not consulted
-> continue with required modules
```

### 7.3 Deferred module

A deferred module must not be represented by incomplete hidden behavior.

Either:

- the relevant feature is unavailable;
- the resolver follows an explicitly documented reduced path;
- or the task provides a bounded temporary placeholder.

---

## 8. Rule Module Standard

A rule module should normally behave like a focused calculation:

```text
current state slice
+ content definitions
+ action context
+ controlled random source if allowed
-> validation
-> proposed state changes
-> reasons
-> secondary-check requests
-> presentation cues
```

A rule module should not:

- apply changes to unrelated state;
- emit authoritative cross-system commands;
- locate dependencies through Phaser scenes or global listeners;
- mutate state while calculating;
- hide important consequences in callbacks;
- decide final presentation timing.

---

## 9. Resolver Standard

A resolver is explicit project-specific glue.

It may:

1. receive an action request;
2. validate basic structure;
3. gather relevant content and state;
4. identify required and optional modules;
5. call them in a documented order;
6. combine their proposed changes;
7. resolve conflicts;
8. apply one authoritative transition;
9. process ordered secondary checks;
10. build one ResolvedOutcome;
11. return presentation cues after truth is established.

A resolver must not:

- become a universal game manager;
- contain all internal HEAT, REP, TIME, Info, inventory, mission, or combat rules;
- depend on animation completion to decide truth;
- use uncontrolled event chains for critical consequences;
- directly manipulate Phaser sprites as part of simulation resolution.

### Resolver contract additions

Every resolver reference should also specify:

- accepted action types;
- required modules by action type;
- optional modules by action type;
- exact consequence phases;
- conflict-resolution policy;
- transition application policy;
- outcome schema;
- input locking and restoration responsibility at the presentation boundary.

---

## 10. Presentation Module Standard

Presentation modules may:

- collect keyboard, pointer, or menu input;
- display current state;
- animate resolved outcomes;
- play audio;
- update HUD and dialogue;
- move cameras;
- render characters and environments;
- emit non-authoritative notifications after resolution.

Presentation modules must not:

- directly change HEAT, REP, TIME, Info, inventory, mission truth, or win/loss state;
- use sprite identity as simulation identity;
- infer authoritative consequences from animation state;
- serialize Phaser objects into saves;
- hide gameplay logic inside scene update loops.

A presentation adapter should translate between player-facing inputs and plain simulation requests, then translate resolved outcomes into display instructions.

---

## 11. Scenario Module Standard

A scenario module may own:

- mission-specific roles;
- objective truth;
- bounded setup pools;
- win and failure conditions;
- scenario-specific validation;
- scenario-specific content definitions.

It must not silently redefine universal module rules.

For example, the Stolen Package scenario may assign guilt and evidence, but it should use the shared Information, TIME, REP, HEAT, and resolver contracts rather than creating private incompatible versions.

---

## 12. Infrastructure Module Standard

Infrastructure modules include:

- stable IDs;
- seeded randomness;
- save schemas;
- state transitions;
- test harnesses;
- content validation.

They should support gameplay modules without absorbing gameplay design.

For example:

- seeded randomness supplies reproducible draws;
- it does not decide whether Pressure should succeed;
- state transition applies accepted changes;
- it does not calculate the meaning of REP or HEAT.

---

## 13. Status Gates

### Design Draft

A module may still contain unresolved mechanics. It should not be implemented unless a task explicitly defines a temporary bounded behavior.

### Implementation Ready

A module is Implementation Ready only when:

- purpose and ownership are clear;
- inputs and outputs are defined;
- required and optional dependencies are identified;
- failure behavior is defined;
- determinism requirements are defined;
- relevant consequence order is known;
- tests are specified;
- open questions do not block the intended slice.

### Prototype Active

A module becomes Prototype Active only when:

- implementation exists;
- tests pass;
- browser behavior is verified where relevant;
- documentation matches behavior;
- known limitations are recorded.

---

## 14. Definition of Ready Checklist

Before a module is named in an implementation task, confirm:

- [ ] It has a stable module ID.
- [ ] It appears in the system registry.
- [ ] Its status permits implementation.
- [ ] Its ownership is bounded.
- [ ] Inputs and outputs are explicit.
- [ ] State read and proposed-change permissions are explicit.
- [ ] Required dependencies are explicit.
- [ ] Optional integrations are explicit.
- [ ] Missing-module behavior is explicit.
- [ ] Determinism requirements are explicit.
- [ ] Resolver participation is explicit.
- [ ] Minimum tests are explicit.
- [ ] Blocking open questions are resolved.

---

## 15. Definition of Done Checklist

An implemented module is complete only when:

- [ ] Code matches the approved contract.
- [ ] Portable state contains no Phaser objects.
- [ ] The module does not directly command unrelated modules.
- [ ] Required failure cases return explicit results.
- [ ] Optional absence behavior works.
- [ ] Deterministic tests pass where required.
- [ ] State changes are traceable.
- [ ] Events report completed changes rather than causing hidden truth.
- [ ] Presentation cues occur after authoritative resolution.
- [ ] The registry status is updated.
- [ ] Known limitations are documented.

---

## 16. Change-Control Procedure

When changing a module contract:

1. Identify the contract field being changed.
2. Identify affected resolvers.
3. Identify affected tasks and tests.
4. Identify affected runtime-state or save fields.
5. Identify affected presentation cues.
6. Update the focused reference.
7. Update the system registry if status, ownership, or dependencies changed.
8. Do not rewrite unrelated module references without a real contract impact.

A module may be replaced without rewriting the whole project when the replacement preserves the required interface or when dependent resolvers are deliberately updated.

---

## 17. Example Compact Contract — TIME

```text
Module ID: resource.time
Kind: Rule Module
Status: Design Draft
Activation role: Required for intended demo actions

Purpose:
Calculate in-world minute costs and propose time advancement.

Owns:
- action minute costs
- time advancement proposal
- TIME-owned threshold requests
- TIME reason strings

Does not own:
- animation duration
- hunger calculation
- schedule relocation
- mission failure
- HEAT

Inputs:
- action type
- action context
- current day/minute
- approved cost definitions

Outputs:
- proposed minute change
- resulting day/minute preview
- threshold checks requested
- reasons
- debug trace

Required dependencies:
- runtime state
- content definitions

Optional integrations:
- survival pressure
- schedules
- mission deadlines

Called by:
- InteractionResolver
- TravelResolver
- CombatResolver
- EndOfDayResolver

Failure behavior:
Missing cost definition fails validation unless the active task defines a safe explicit fallback.

Determinism:
Fully deterministic unless the approved cost rule explicitly uses controlled randomness.
```

---

## 18. Contract Principle

```text
A module should be understandable without reading the whole game.
A resolver should combine modules without becoming all of them.
A missing optional module should reduce behavior, not break hidden assumptions.
A missing required module should fail clearly.
The master architecture should remain stable while focused contracts evolve.
```
