# Trapstar Module Contract Standard

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Standard structure and behavioral contract for modular design and implementation references  
**Architecture role:** Core architecture document  
**Design maturity:** Design Accepted  
**Last updated:** 2026-07-13

---

## 1. Purpose

This standard defines how modular parts of *Trapstar the Demo* should be documented and implemented.

A useful contract makes clear:

1. what the module owns;
2. what it does not own;
3. its one Primary Kind;
4. its Architecture Role;
5. its Design Maturity;
6. its Demo Default Activation;
7. its Activation Role for the named contract or slice;
8. what it receives and returns;
9. what happens when it or an integration is unavailable.

Not every module needs the same amount of documentation. This standard defines Lightweight, Standard, and Resolver profiles.

---

## 2. Governing Rules

```text
Commands change the world.
Events report what changed.
```

```text
ActionRequest
-> specialized Resolver
-> bounded Rule Modules
-> ordered State Transition
-> ResolvedOutcome
-> Presentation / Notifications
```

Required principles:

- each module has one Primary Kind;
- each module owns one bounded responsibility;
- data ownership and behavior ownership remain distinct;
- shared structures have one recorded owner;
- modules propose changes only within their authority;
- modules do not directly mutate unrelated state;
- resolvers coordinate cross-module actions without absorbing every internal rule;
- one authoritative transition applies accepted changes;
- presentation does not create gameplay truth;
- Phaser objects never become portable state or stable identity;
- gameplay randomness is controlled and reproducible;
- optional integrations have explicit absence behavior;
- missing required modules fail visibly and safely.

---

## 3. Governance-Document Exemption

The System Registry, this Contract Standard, and other architecture-governance documents are not gameplay modules.

They are exempt from gameplay-module requirements such as Module ID, Demo Default Activation, runtime interfaces, resolver participation, and semantic outcome signals. They should still record their document role, Architecture Role, Design Maturity, and authority relationship.

---

## 4. Domain-Based Authority

| Document or artifact | Authority domain |
|---|---|
| `README.md` | Introduction and navigation. |
| `PROJECT_STATE.md` | Current phase, blockers, priorities, and approved next work. |
| Master System Architecture | Universal design and technical boundaries. |
| System Registry | Module identity, kind, role, maturity, Demo Default Activation, ownership, and authority location. |
| Focused module reference | Detailed authority for the named module. |
| Resolver Contract | Action-specific participation, validation, coordination, and consequence order. |
| Codex task | One bounded implementation order. |
| Implementation and tests | Evidence that approved behavior works. |

A focused contract may refine its own module, but it must not silently override universal architecture or redefine unrelated modules.

---

## 5. Classification Fields

### 5.1 Primary Kind

Every module has exactly one:

```text
Design Philosophy
Choice Frame
Action Language
Data Model
Rule Module
Resolver
Scenario Module
Presentation Module
Infrastructure Module
```

A Data Model owns a portable shape or authoritative state model. It does not calculate how that state changes.

A Rule Module owns one bounded category of gameplay calculation. It may propose changes but does not silently redefine the data structures it reads or writes.

A Resolver coordinates accepted actions and participating modules. It does not own the generic request envelope unless the request is explicitly resolver-specific.

### 5.2 Architecture Role

```text
Core
Supporting
```

### 5.3 Design Maturity

```text
Design Draft
Design Accepted
Implementation Ready
Prototype Active
Experimental
Superseded
Removed
```

`Design Accepted` is safe for planning, naming, and compatibility. It is not sufficient by itself for implementation.

### 5.4 Activation Scope

Three related concepts must not be combined.

#### Demo Default Activation

Stored in the System Registry:

```text
Required
Optional Integration
Deferred Integration
```

#### Current production status

Stored in `PROJECT_STATE.md`:

```text
Active
Paused
Blocked
Not yet scheduled
```

#### Action-specific participation

Stored in Resolver Contracts:

```text
Required
Optional Integration
Not Consulted
```

---

## 6. Required Contract Header

Every focused module reference should begin with:

```markdown
# Module Name

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `category.module_name`  
**Primary Kind:** `[one kind]`  
**Architecture Role:** `Core / Supporting`  
**Design Maturity:** `Design Draft / Design Accepted / Implementation Ready / Prototype Active / Experimental / Superseded / Removed`  
**Demo Default Activation:** `Required / Optional Integration / Deferred Integration`  
**Activation Role for this contract or slice:** `Required / Optional Integration / Deferred Integration`  
**Contract Profile:** `Lightweight / Standard / Resolver`  
**Detailed Authority:** `This file controls ...`  
**Last updated:** `YYYY-MM-DD`
```

Module IDs should be stable, lowercase, and namespaced.

---

## 7. Contract Profiles

### 7.1 Lightweight Contract

Use for Design Philosophies, Choice Frames, conceptual Action Language references, simple Data Models, and small presentation or infrastructure standards that do not calculate gameplay outcomes.

Required sections:

1. Purpose
2. Architecture Relationship
3. Owns
4. Does Not Own
5. Key Concepts or Data
6. Relationships
7. Design Maturity and Activation Scope
8. Open Questions
9. Change Impact

### 7.2 Standard Module Contract

Use for Rule Modules, substantial Data Models, Scenario Modules, implementation-facing Presentation Modules, and authoritative Infrastructure Modules.

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

### 7.3 Resolver Contract

Use only for Resolver modules. It includes the relevant Standard sections plus:

1. Accepted Action Types
2. Request types accepted
3. Required Modules by Action Type
4. Optional Modules by Action Type
5. Modules Not Consulted by Action Type
6. Validation Stages
7. Exact Consequence Phases
8. Conflict-Resolution Policy
9. State-Transition Policy
10. Secondary-Check Order
11. ResolvedOutcome Responsibility
12. Presentation Handoff
13. Input Locking and Restoration Boundary
14. Resolver-Specific Tests

A Resolver Contract must state whether it accepts the generic `ActionRequest` directly or a resolver-specific narrowed request derived from it.

---

## 8. Shared Structure and Behavior Ownership

A shared interface, data shape, or behavioral category is not automatically a separate module, but it must have one owner.

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

Ownership means the named contract controls the shape, validation rules, compatibility expectations, or behavioral rules named in the table. Other modules may consume the result but may not silently redefine it.

### 8.1 Information boundary

```text
data.info_cards
-> InfoCard schema

data.information
-> Soft / Hard classification and information state

information.rules
-> disclosure, withholding, hardening, reveal eligibility,
   proposed information-state changes, and semantic signals
```

A Data Model must not be assigned behavior merely because the behavior concerns that data.

### 8.2 ActionRequest boundary

```text
presentation.adapter
-> translates player intent into a request

runtime.action_request
-> owns the generic routing-neutral ActionRequest structure

specialized resolver
-> accepts supported requests, validates its action class,
   chooses participating modules, and coordinates consequence order
```

`resolver.interaction` may own `InteractionValidationResult`, but it does not own a universal `ValidationResult` unless a later shared contract explicitly establishes one.

---

## 9. Contract Prerequisites Versus Implementation Deliverables

A contract being required before a task begins does not mean its implementation must already exist.

```text
presentation.blackboard contract
-> Implementation Ready before Task 002 is reactivated

presentation.blackboard implementation
-> may be produced by Task 002
```

Design must be ready before coding begins; implementation may then be created by the approved task.

---

## 10. Lightweight Template

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Primary Kind:** `[kind]`  
**Architecture Role:** `[Core / Supporting]`  
**Design Maturity:** `[maturity]`  
**Demo Default Activation:** `[role]`  
**Activation Role for this contract or slice:** `[role]`  
**Contract Profile:** `Lightweight`

## 1. Purpose
## 2. Architecture Relationship
## 3. Owns
## 4. Does Not Own
## 5. Key Concepts or Data
## 6. Relationships
## 7. Design Maturity and Activation Scope
## 8. Open Questions
## 9. Change Impact
```

---

## 11. Standard Template

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Primary Kind:** `[kind]`  
**Architecture Role:** `[Core / Supporting]`  
**Design Maturity:** `[maturity]`  
**Demo Default Activation:** `[role]`  
**Activation Role for this contract or slice:** `[role]`  
**Contract Profile:** `Standard`

## 1. Purpose
## 2. Owns
## 3. Does Not Own
## 4. Inputs
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

## 12. Resolver Template

```markdown
# [Resolver Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `resolver.[name]`  
**Primary Kind:** `Resolver`  
**Architecture Role:** `[Core / Supporting]`  
**Design Maturity:** `[maturity]`  
**Demo Default Activation:** `[role]`  
**Activation Role for this contract or slice:** `[role]`  
**Contract Profile:** `Resolver`

## 1. Purpose
## 2. Owns
## 3. Does Not Own
## 4. Accepted Action Types
## 5. Accepted Request Types
## 6. Required Modules by Action Type
## 7. Optional Modules by Action Type
## 8. Modules Not Consulted by Action Type
## 9. State and Content Read
## 10. Validation Stages
## 11. Exact Consequence Phases
## 12. Conflict-Resolution Policy
## 13. State-Transition Policy
## 14. Secondary-Check Order
## 15. ResolvedOutcome Responsibility
## 16. Semantic Outcome Signals
## 17. Presentation Handoff
## 18. Input Locking and Restoration Boundary
## 19. Failure Behavior
## 20. Determinism
## 21. Events
## 22. Tests
## 23. Open Questions
## 24. Change Impact
## 25. Definition of Ready
## 26. Definition of Done
```

---

## 13. Standard Guidance

### Ownership and boundaries

State the exact category of rules or data the module controls and explicitly name nearby responsibilities it does not control.

### Inputs and outputs

Use the smallest useful plain-data context. Rule Modules should return calculations or proposals rather than directly mutate global state.

### State boundaries

List state fields the module may read and state paths it may propose changing. A proposal is not permission to mutate immediately.

### Dependencies and integrations

Required dependencies must be few and explicit. Optional integrations must define absence behavior. Rule Modules should normally call no unrelated Rule Modules; cross-module coordination belongs in a Resolver.

### Validation and failure

Define behavior for missing inputs, invalid IDs, forbidden actions, unavailable required modules, absent optional context, out-of-range values, and content/runtime disagreement. Failures return explicit data.

### Determinism

State whether the module is fully deterministic, may use controlled randomness, records random draws or seed position, and returns the same result for identical input and seed. Uncontrolled randomness is prohibited for gameplay truth.

### Semantic outcome signals

Simulation modules may report semantic facts such as `heat_changed`, `relationship_shifted`, `information_disclosed`, and `time_advanced`. They must not prescribe camera shake, HUD flashing, animation names, or audio clips.

### Events

Events report completed results. They do not become hidden owners of critical state changes.

---

## 14. Data Ownership Rules

```text
Content Definitions = what something is
Runtime State = what is currently true
Data Model = the portable shape of that truth
Rule Module = how truth may change
Resolver = which modules participate and in what order
Presentation = how the result is shown
```

Portable state must not contain Phaser scenes, sprites, cameras, containers, animation objects, physics bodies, DOM nodes, or event emitters.

---

## 15. Required, Optional, and Deferred Behavior

```text
required module unavailable
-> validation fails
-> no authoritative transition
-> explicit failure outcome
```

```text
optional integration unavailable
-> skip its contribution
-> fabricate no default consequence
-> record that it was not consulted
-> continue with required modules
```

```text
deferred integration
-> feature unavailable or explicit reduced path
-> no hidden placeholder behavior
```

---

## 16. Design-Maturity Gates

### Design Draft

May contain unresolved mechanics. Do not implement unless an approved task defines bounded temporary behavior.

### Design Accepted

The concept and architecture relationship are approved. It may guide naming and planning but is not code-ready by itself.

### Implementation Ready

The selected slice has clear ownership, one Primary Kind, explicit interfaces, state boundaries, dependencies, failure behavior, determinism, consequence participation, tests, and no blocking open questions.

### Prototype Active

Implementation exists, tests pass, relevant browser behavior is verified, documentation matches behavior, and limitations are recorded.

---

## 17. Definition of Ready Checklist

Before a module is named in an implementation task:

- [ ] stable Module ID;
- [ ] one Primary Kind;
- [ ] Architecture Role recorded;
- [ ] Design Maturity permits implementation;
- [ ] Demo Default Activation recorded;
- [ ] Activation Role explicit for the intended slice;
- [ ] registry entry exists;
- [ ] ownership is bounded;
- [ ] data ownership is separated from behavior ownership;
- [ ] shared structures have one owner;
- [ ] interfaces and state boundaries are explicit;
- [ ] required dependencies and optional integrations are explicit;
- [ ] missing-module behavior is explicit;
- [ ] determinism and tests are explicit;
- [ ] resolver participation is explicit where relevant;
- [ ] blocking questions are resolved.

---

## 18. Definition of Done Checklist

- [ ] code matches the approved contract;
- [ ] portable state contains no Phaser objects;
- [ ] the module does not command unrelated modules;
- [ ] failure cases return explicit results;
- [ ] optional absence behavior works;
- [ ] deterministic tests pass where required;
- [ ] state changes are traceable;
- [ ] events report completed changes;
- [ ] semantic signals are translated only after authoritative resolution;
- [ ] registry maturity and activation are updated;
- [ ] limitations are documented.

---

## 19. Contract Principle

```text
A module should be understandable without reading the whole game.
A module has one Primary Kind.
Data ownership and behavior ownership remain separate.
The generic ActionRequest exists before specialized resolver selection.
The registry sets Demo Default Activation.
PROJECT_STATE records current production status.
Resolver Contracts set action-specific participation.
Shared structures have one owner.
A missing optional integration reduces behavior.
A missing required module fails clearly.
```
