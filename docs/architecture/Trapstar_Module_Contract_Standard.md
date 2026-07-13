# Trapstar Module Contract Standard

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Standard structure and behavioral contract for modular design and implementation references  
**Architecture role:** Core architecture document  
**Design maturity:** Design Draft  
**Last updated:** 2026-07-13

---

## 1. Purpose

This standard defines how modular parts of *Trapstar the Demo* should be documented and implemented.

Its purpose is to let modules be added, refined, enabled, disabled, deferred, replaced, or removed without turning the project into one tightly coupled block.

A useful contract makes these things obvious:

1. what the module owns;
2. what it does not own;
3. what kind of module it is;
4. how important it is to the architecture;
5. how mature its design is;
6. whether it is required, optional, or deferred for the current scope;
7. what it receives and returns;
8. what happens when it is unavailable.

Not every module requires the same amount of documentation. This standard therefore defines three contract profiles:

- Lightweight Contract;
- Standard Module Contract;
- Resolver Contract.

---

## 2. Governing Architecture Rules

Every contract must preserve these project rules:

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

- Each module has one primary kind.
- Each module owns one bounded category of responsibility.
- Architecture role, design maturity, and activation role are independent fields.
- A module may calculate or propose changes within its responsibility.
- A module does not directly mutate unrelated state.
- A resolver coordinates cross-module actions.
- A resolver does not absorb every module's internal rules.
- One authoritative transition applies accepted state changes.
- Presentation does not create gameplay truth.
- Phaser objects never become portable state or stable identity.
- Gameplay randomness is controlled and reproducible.
- Optional integrations have explicit absence behavior.
- Missing required modules fail visibly and safely.

---

## 3. Domain-Based Authority

A module contract must respect the authority domain of each repository document.

| Document or artifact | Authority domain |
|---|---|
| `README.md` | Introduction and navigation. |
| `PROJECT_STATE.md` | Current phase, blockers, active priorities, and approved next work. |
| Master System Architecture | Universal cross-project design and technical boundaries. |
| System Registry | Module identity, primary kind, architecture role, design maturity, activation role, and detailed-authority location. |
| Focused module reference | Detailed authority for the named module. |
| Design packet | Implementation-ready feature or content specification. |
| Codex task | One bounded implementation order. |
| Implementation and tests | Evidence that approved behavior works. |

A focused contract may refine its module's details, but it must not silently override universal architecture boundaries or redefine unrelated modules.

---

## 4. Required Contract Header

Every focused module reference should begin with:

```markdown
# Module Name

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `category.module_name`  
**Primary kind:** Design Philosophy / Choice Frame / Action Language / Data Model / Rule Module / Resolver / Scenario Module / Presentation Module / Infrastructure Module  
**Architecture role:** Core / Supporting  
**Design maturity:** Design Draft / Implementation Ready / Prototype Active / Experimental / Superseded / Removed  
**Activation role:** Required / Optional Integration / Deferred Integration  
**Contract profile:** Lightweight / Standard / Resolver  
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

## 5. Independent Classification Fields

### 5.1 Primary kind

Every module has exactly one primary kind.

| Primary kind | Use |
|---|---|
| **Design Philosophy** | Project-wide design lens without runtime rule ownership. |
| **Choice Frame** | Broad player intent or strategic framing. |
| **Action Language** | Manner, tone, modifiers, permissions, or ability expression. |
| **Data Model** | Portable structure or authoritative data shape. |
| **Rule Module** | Bounded gameplay calculation. |
| **Resolver** | Explicit coordinator for a class of action. |
| **Scenario Module** | Mission-specific or run-specific truth. |
| **Presentation Module** | Input and display behavior without simulation authority. |
| **Infrastructure Module** | Identity, transition, save, test, portability, or reproducibility support. |

A module may own data or use infrastructure without receiving a second primary kind.

### 5.2 Architecture role

```text
Core
Supporting
```

- **Core** means foundational to the project's identity or minimum architecture.
- **Supporting** means additive, specialized, or phase-dependent.

### 5.3 Design maturity

```text
Design Draft
Implementation Ready
Prototype Active
Experimental
Superseded
Removed
```

Design maturity answers whether the contract is ready to be implemented, not whether the module is important or currently enabled.

### 5.4 Activation role

```text
Required
Optional Integration
Deferred Integration
```

Activation role may vary by feature or phase. A module that is optional in one resolver may be required in another; resolver contracts must state the action-specific truth.

---

## 6. Contract Profiles

### 6.1 Lightweight Contract

Use for:

- Design Philosophies;
- Choice Frames;
- conceptual Action Language references;
- simple Data Models;
- small presentation or infrastructure standards that do not calculate gameplay outcomes.

Required sections:

1. Purpose
2. Architecture Relationship
3. Owns
4. Does Not Own
5. Key Concepts or Data
6. Relationships
7. Design Maturity and Activation
8. Open Questions
9. Change Impact

A lightweight contract must still define clear boundaries. It is shorter because it does not pretend that every conceptual document is an implementation-ready rule engine.

### 6.2 Standard Module Contract

Use for:

- Rule Modules;
- substantial Data Models;
- Scenario Modules;
- implementation-facing Presentation Modules;
- Infrastructure Modules that participate directly in authoritative behavior.

Required sections:

1. Purpose
2. Owns
3. Does Not Own
4. Inputs
5. Outputs
6. State Read
7. State Changes Proposed
8. Required Dependencies
9. Optional Integrations
10. Called By
11. May Call
12. Validation and Failure Behavior
13. Determinism
14. Consequence Participation
15. Semantic Outcome Signals
16. Events
17. Tests
18. Open Questions
19. Change Impact
20. Definition of Ready
21. Definition of Done

### 6.3 Resolver Contract

Use only for Resolver modules.

A Resolver Contract includes the relevant Standard sections plus:

1. Accepted Action Types
2. Required Modules by Action Type
3. Optional Modules by Action Type
4. Validation Stages
5. Exact Consequence Phases
6. Conflict-Resolution Policy
7. State-Transition Policy
8. Secondary-Check Order
9. ResolvedOutcome Responsibility
10. Presentation Handoff
11. Input Locking and Restoration Boundary
12. Resolver-Specific Tests

### 6.4 Default profile by primary kind

| Primary kind | Default contract profile |
|---|---|
| Design Philosophy | Lightweight |
| Choice Frame | Lightweight |
| Action Language | Lightweight until implementation-facing; Standard when it calculates or proposes gameplay effects |
| Data Model | Lightweight for simple schemas; Standard for substantial authoritative models |
| Rule Module | Standard |
| Resolver | Resolver |
| Scenario Module | Standard |
| Presentation Module | Lightweight or Standard according to responsibility |
| Infrastructure Module | Lightweight or Standard according to responsibility |

A module may use a stricter profile than its default. It may not omit sections required by its actual responsibility.

---

## 7. Lightweight Contract Template

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Primary kind:** `[kind]`  
**Architecture role:** `[Core / Supporting]`  
**Design maturity:** `[maturity]`  
**Activation role:** `[role]`  
**Contract profile:** Lightweight  
**Detailed authority:** This file controls [specific authority].  
**Last updated:** `[date]`

---

## 1. Purpose

## 2. Architecture Relationship

## 3. Owns

## 4. Does Not Own

## 5. Key Concepts or Data

## 6. Relationships

## 7. Design Maturity and Activation

## 8. Open Questions

## 9. Change Impact
```

---

## 8. Standard Module Contract Template

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Primary kind:** `[kind]`  
**Architecture role:** `[Core / Supporting]`  
**Design maturity:** `[maturity]`  
**Activation role:** `[role]`  
**Contract profile:** Standard  
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

## 14. Consequence Participation

## 15. Semantic Outcome Signals

## 16. Events

## 17. Tests

## 18. Open Questions

## 19. Change Impact

## 20. Definition of Ready

## 21. Definition of Done
```

---

## 9. Resolver Contract Template

```markdown
# [Resolver Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `resolver.[name]`  
**Primary kind:** Resolver  
**Architecture role:** `[Core / Supporting]`  
**Design maturity:** `[maturity]`  
**Activation role:** `[role]`  
**Contract profile:** Resolver  
**Detailed authority:** This file controls [resolver class] coordination.  
**Last updated:** `[date]`

---

## 1. Purpose

## 2. Owns

## 3. Does Not Own

## 4. Accepted Action Types

## 5. Action Request Inputs

## 6. Required Modules by Action Type

## 7. Optional Modules by Action Type

## 8. State and Content Read

## 9. Validation Stages

## 10. Exact Consequence Phases

## 11. Conflict-Resolution Policy

## 12. State-Transition Policy

## 13. Secondary-Check Order

## 14. ResolvedOutcome Responsibility

## 15. Semantic Outcome Signals

## 16. Presentation Handoff

## 17. Input Locking and Restoration Boundary

## 18. Failure Behavior

## 19. Determinism

## 20. Events

## 21. Tests

## 22. Open Questions

## 23. Change Impact

## 24. Definition of Ready

## 25. Definition of Done
```

---

## 10. Shared Standard Section Guidance

### 10.1 Purpose

Explain the one problem the module exists to solve.

Good:

> The HEAT module calculates police-attention changes and threshold consequences.

Too broad:

> The HEAT module manages police, crime, factions, NPC fear, missions, movement, and combat.

### 10.2 Owns

List the rules or data for which the module is the authority.

### 10.3 Does Not Own

State boundaries explicitly. Another module or resolver may use this module's output, but the module should not perform unrelated effects secretly.

### 10.4 Inputs

List the smallest useful plain-data context the module may read:

- required and optional fields;
- stable IDs;
- relevant current-state slices;
- relevant content definitions;
- controlled random input when permitted.

### 10.5 Outputs

A Rule Module should generally return a calculation or proposal, not directly mutate global state.

Example:

```text
{
  moduleId,
  accepted,
  proposedChanges,
  reasons,
  secondaryChecks,
  semanticSignals,
  debugTrace
}
```

### 10.6 State Read

List the authoritative state fields the module may inspect.

### 10.7 State Changes Proposed

List the state paths the module may propose changing. This is an ownership boundary, not permission to mutate immediately.

### 10.8 Required Dependencies

List modules without which the contract cannot perform its minimum responsibility.

### 10.9 Optional Integrations

List modules that may add context or consequences but are not required for minimum operation.

### 10.10 Called By

List resolvers or lifecycle processes allowed to invoke the module.

### 10.11 May Call

Rule Modules should normally call no unrelated Rule Modules. Cross-module coordination should usually remain in a Resolver.

### 10.12 Validation and Failure Behavior

Define behavior for:

- missing required input;
- invalid IDs;
- forbidden actions;
- unavailable required modules;
- absent optional context;
- out-of-range data;
- disagreement between content and runtime state.

Failures should return explicit data rather than silently doing nothing.

### 10.13 Determinism

State whether the module:

- is fully deterministic;
- may use a controlled random source;
- records random draws or seed position;
- returns the same result for identical input and seed.

Uncontrolled randomness is prohibited for gameplay truth.

### 10.14 Consequence Participation

State where the module participates in a Resolver's documented sequence. A Rule Module should not define the entire global order unless ordering is its specific responsibility.

### 10.15 Semantic Outcome Signals

Simulation modules may report semantic facts such as:

```text
heat_changed
heat_threshold_crossed
relationship_shifted
information_disclosed
time_advanced
```

They should not prescribe UI-specific actions such as camera shake, HUD flashing, animation names, or audio clips.

The Presentation Adapter translates semantic outcome signals into Phaser-facing cues.

### 10.16 Events

Events report completed results. They must not become the hidden owner of critical state changes.

### 10.17 Tests

List minimum contract, deterministic, failure, absence, and integration tests.

### 10.18 Open Questions

Codex must not invent answers to blocking questions unless a task explicitly authorizes a bounded temporary behavior.

### 10.19 Change Impact

Identify affected Resolver contracts, tasks, state fields, save schemas, tests, and semantic signals.

---

## 11. Data Ownership Rules

### 11.1 Definitions versus runtime state

```text
Content Definitions = what something is
Runtime State = what is currently true
Rule Module = how truth may change
Resolver = which modules participate and in what order
Presentation = how the result is shown
```

Content definitions should not contain mutable run truth.

Runtime state should not contain Phaser scenes, sprites, cameras, animation objects, containers, physics bodies, DOM nodes, or event emitters.

### 11.2 Values versus modules

A value is not automatically a module.

Examples:

- `heat: 3` is state;
- HEAT calculation and threshold logic belong to `social.heat`;
- `currentMinute: 480` is state;
- minute-cost and time-advancement rules belong to `resource.time`.

### 11.3 Stable identity

Modules exchange stable IDs and plain data.

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

## 12. Required, Optional, and Deferred Behavior

### 12.1 Required dependency unavailable

```text
required module missing
-> validation fails
-> no authoritative transition
-> explicit failure outcome
-> debug trace names the missing module
```

### 12.2 Optional integration unavailable

```text
optional integration missing or disabled
-> skip its calculation
-> do not fabricate a default consequence
-> record that it was not consulted
-> continue with required modules
```

### 12.3 Deferred integration

A deferred module must not be represented by incomplete hidden behavior.

Either:

- the relevant feature is unavailable;
- the Resolver follows an explicitly documented reduced path;
- or the task provides a bounded temporary placeholder.

---

## 13. Rule Module Standard

A Rule Module normally behaves like a focused calculation:

```text
current state slice
+ content definitions
+ action context
+ controlled random source if allowed
-> validation
-> proposed state changes
-> reasons
-> secondary-check requests
-> semantic outcome signals
```

A Rule Module must not:

- apply changes to unrelated state;
- emit authoritative cross-system commands;
- locate dependencies through Phaser scenes or global listeners;
- mutate state while calculating;
- hide important consequences in callbacks;
- decide final presentation timing.

---

## 14. Resolver Standard

A Resolver is explicit project-specific glue.

It may:

1. receive an Action Request;
2. validate basic structure;
3. gather relevant content and state;
4. identify required and optional modules;
5. call them in a documented order;
6. combine proposed changes;
7. resolve conflicts;
8. apply one authoritative transition;
9. process ordered secondary checks;
10. build one ResolvedOutcome;
11. hand semantic signals to presentation after truth is established.

A Resolver must not:

- become a universal game manager;
- contain all internal HEAT, REP, TIME, Info, inventory, mission, or combat rules;
- depend on animation completion to decide truth;
- use uncontrolled event chains for critical consequences;
- directly manipulate Phaser sprites as part of simulation resolution.

---

## 15. Presentation Module Standard

Presentation Modules may:

- collect keyboard, pointer, or menu input;
- display current state;
- animate resolved outcomes;
- play audio;
- update HUD and dialogue;
- move cameras;
- render characters and environments;
- emit non-authoritative notifications after resolution.

Presentation Modules must not:

- directly change HEAT, REP, TIME, Info, inventory, mission truth, or win/loss state;
- use sprite identity as simulation identity;
- infer authoritative consequences from animation state;
- serialize Phaser objects into saves;
- hide gameplay logic inside scene update loops.

A Presentation Adapter translates player-facing input into plain Action Requests and translates ResolvedOutcome semantic signals into display instructions.

---

## 16. Scenario Module Standard

A Scenario Module may own:

- mission-specific roles;
- objective truth;
- bounded setup pools;
- win and failure conditions;
- scenario-specific validation;
- scenario-specific content definitions.

It must not silently redefine universal module rules.

The Stolen Package scenario may assign guilt and evidence, but it should use shared Information, TIME, REP, HEAT, and Resolver contracts rather than creating private incompatible versions.

---

## 17. Infrastructure Module Standard

Infrastructure Modules include:

- stable IDs;
- seeded randomness;
- save schemas;
- state transitions;
- test harnesses;
- content validation.

They support gameplay modules without absorbing gameplay design.

For example:

- seeded randomness supplies reproducible draws; it does not decide whether Pressure succeeds;
- state transition applies accepted changes; it does not calculate the meaning of REP or HEAT.

---

## 18. Design-Maturity Gates

### 18.1 Design Draft

A Design Draft may contain unresolved mechanics. It should not be implemented unless a task explicitly defines a bounded temporary behavior.

### 18.2 Implementation Ready

A module is Implementation Ready only when the selected slice has:

- clear purpose and ownership;
- one primary kind;
- explicit inputs and outputs;
- explicit state-read and proposed-change boundaries;
- identified required and optional dependencies;
- defined failure behavior;
- defined determinism requirements;
- known consequence participation;
- specified tests;
- no blocking open questions.

### 18.3 Prototype Active

A module becomes Prototype Active only when:

- implementation exists;
- tests pass;
- browser behavior is verified where relevant;
- documentation matches behavior;
- known limitations are recorded.

---

## 19. Definition of Ready Checklist

Before a module is named in an implementation task, confirm:

- [ ] It has a stable Module ID.
- [ ] It has one Primary Kind.
- [ ] Its Architecture Role is recorded.
- [ ] Its Design Maturity permits implementation.
- [ ] Its Activation Role is explicit for the intended slice.
- [ ] It appears in the System Registry.
- [ ] Its ownership is bounded.
- [ ] Its contract profile is appropriate.
- [ ] Inputs and outputs are explicit where relevant.
- [ ] State-read and proposed-change permissions are explicit where relevant.
- [ ] Required dependencies are explicit.
- [ ] Optional integrations are explicit.
- [ ] Missing-module behavior is explicit.
- [ ] Determinism requirements are explicit.
- [ ] Resolver participation is explicit where relevant.
- [ ] Minimum tests are explicit.
- [ ] Blocking open questions are resolved.

---

## 20. Definition of Done Checklist

An implemented module is complete only when:

- [ ] Code matches the approved contract.
- [ ] Portable state contains no Phaser objects.
- [ ] The module does not directly command unrelated modules.
- [ ] Required failure cases return explicit results.
- [ ] Optional absence behavior works.
- [ ] Deterministic tests pass where required.
- [ ] State changes are traceable.
- [ ] Events report completed changes rather than causing hidden truth.
- [ ] Semantic signals are translated by presentation only after authoritative resolution.
- [ ] Registry maturity and activation are updated.
- [ ] Known limitations are documented.

---

## 21. Change-Control Procedure

When changing a module contract:

1. Identify the classification or contract field being changed.
2. Identify affected Resolvers.
3. Identify affected tasks and tests.
4. Identify affected runtime-state or save fields.
5. Identify affected semantic outcome signals and presentation mappings.
6. Update the focused reference.
7. Update the System Registry if kind, role, maturity, activation, ownership, or authority changed.
8. Do not rewrite unrelated references without a real contract impact.

A module may be replaced without rewriting the whole project when the replacement preserves the required interface or dependent Resolvers are deliberately updated.

---

## 22. Example Compact Standard Contract — TIME

```text
Module ID: resource.time
Primary kind: Rule Module
Architecture role: Core
Design maturity: Design Draft
Activation role: Required
Contract profile: Standard

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
- semantic signal: time_advanced
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

## 23. Contract Principle

```text
A module should be understandable without reading the whole game.
A module has one primary kind.
Architecture role, design maturity, and activation role answer different questions.
A Resolver combines modules without becoming all of them.
A missing optional integration should reduce behavior, not break hidden assumptions.
A missing required module should fail clearly.
The master architecture should remain stable while focused contracts evolve.
```