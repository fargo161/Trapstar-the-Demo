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

Its purpose is to let modules be added, refined, enabled, disabled, deferred, replaced, or removed without turning the project into one tightly coupled block.

A useful contract makes clear:

1. what the module owns;
2. what it does not own;
3. its one Primary Kind;
4. its Architecture Role;
5. its Design Maturity;
6. its Activation Role for the named contract or slice;
7. what it receives and returns;
8. what happens when it or an integration is unavailable.

Not every module needs the same amount of documentation. This standard therefore defines Lightweight, Standard, and Resolver contract profiles.

---

## 2. Governing Rules

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

- each module has one Primary Kind;
- each module owns one bounded responsibility;
- Architecture Role, Design Maturity, and Activation Role are separate;
- modules propose changes only within their authority;
- modules do not directly mutate unrelated state;
- resolvers coordinate cross-module actions without absorbing every internal rule;
- one authoritative transition applies accepted state changes;
- presentation does not create gameplay truth;
- Phaser objects never become portable state or stable identity;
- gameplay randomness is controlled and reproducible;
- optional integrations have explicit absence behavior;
- missing required modules fail visibly and safely.

---

## 3. Governance-Document Exemption

The System Registry, this Contract Standard, and other architecture-governance documents are not gameplay modules.

They are exempt from gameplay-module requirements such as:

- Module ID;
- Current-Phase Default Activation;
- action-specific Activation Role;
- runtime inputs and outputs;
- resolver participation;
- semantic outcome signals.

They should still record their document role, Architecture Role, Design Maturity, and authority relationship.

---

## 4. Domain-Based Authority

| Document or artifact | Authority domain |
|---|---|
| `README.md` | Introduction and navigation. |
| `PROJECT_STATE.md` | Current phase, blockers, priorities, and approved next work. |
| Master System Architecture | Universal cross-project design and technical boundaries. |
| System Registry | Module identity, Primary Kind, Architecture Role, Design Maturity, Current-Phase Default Activation, and authority location. |
| Focused module reference | Detailed authority for the named module. |
| Design packet | Implementation-ready feature or content specification. |
| Resolver Contract | Action-specific module participation and consequence order. |
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

A module may own data, use infrastructure, or sit on a boundary without receiving a second Primary Kind.

### 5.2 Architecture Role

```text
Core
Supporting
```

- **Core** — foundational to project identity or minimum architecture.
- **Supporting** — additive, specialized, or phase-dependent.

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

- **Design Draft** — important details remain unresolved.
- **Design Accepted** — concept and architectural relationship are approved, but the implementation-facing contract is incomplete.
- **Implementation Ready** — the selected slice has complete ownership, interfaces, dependencies, failure behavior, determinism, order, and tests.
- **Prototype Active** — implemented, tested, verified, and accurately documented.
- **Experimental** — isolated trial, not canonical.
- **Superseded** — replaced but retained for history.
- **Removed** — no longer accepted.

`Design Accepted` is safe for naming, planning, compatibility, and high-level design. It is not sufficient by itself for implementation.

### 5.4 Activation Scope

The System Registry records **Current-Phase Default Activation**.

Focused contracts record:

```text
Activation role for this contract or slice:
Required
Optional Integration
Deferred Integration
```

Resolver Contracts are the final authority for action-specific participation.

Example:

```text
social.heat
Registry default: Optional Integration

Public Pressure: Required
Private Ask: Optional Integration
Inventory-only action: Not consulted
```

A resolver may differ from the registry default only within its approved scope and must state the difference explicitly.

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
**Activation Role for this contract or slice:** `Required / Optional Integration / Deferred Integration`  
**Contract Profile:** `Lightweight / Standard / Resolver`  
**Detailed Authority:** `This file controls ...`  
**Last updated:** `YYYY-MM-DD`
```

Module IDs should be stable, lowercase, and namespaced. File names may change; Module IDs should change only when conceptual identity changes.

---

## 7. Contract Profiles

### 7.1 Lightweight Contract

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
7. Design Maturity and Activation Scope
8. Open Questions
9. Change Impact

### 7.2 Standard Module Contract

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

### 7.3 Resolver Contract

Use only for Resolver modules.

It includes the relevant Standard sections plus:

1. Accepted Action Types
2. Required Modules by Action Type
3. Optional Modules by Action Type
4. Modules Not Consulted by Action Type
5. Validation Stages
6. Exact Consequence Phases
7. Conflict-Resolution Policy
8. State-Transition Policy
9. Secondary-Check Order
10. ResolvedOutcome Responsibility
11. Presentation Handoff
12. Input Locking and Restoration Boundary
13. Resolver-Specific Tests

### 7.4 Default Profile by Primary Kind

| Primary Kind | Default Profile |
|---|---|
| Design Philosophy | Lightweight |
| Choice Frame | Lightweight |
| Action Language | Lightweight until implementation-facing; Standard when calculating or proposing effects |
| Data Model | Lightweight for simple schemas; Standard for substantial authoritative models |
| Rule Module | Standard |
| Resolver | Resolver |
| Scenario Module | Standard |
| Presentation Module | Lightweight or Standard according to responsibility |
| Infrastructure Module | Lightweight or Standard according to responsibility |

A module may use a stricter profile than its default. It may not omit sections required by its real responsibility.

---

## 8. Lightweight Template

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Primary Kind:** `[kind]`  
**Architecture Role:** `[Core / Supporting]`  
**Design Maturity:** `[maturity]`  
**Activation Role for this contract or slice:** `[role]`  
**Contract Profile:** `Lightweight`  
**Detailed Authority:** `This file controls ...`  
**Last updated:** `[date]`

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

## 9. Standard Template

```markdown
# [Module Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `[category.module]`  
**Primary Kind:** `[kind]`  
**Architecture Role:** `[Core / Supporting]`  
**Design Maturity:** `[maturity]`  
**Activation Role for this contract or slice:** `[role]`  
**Contract Profile:** `Standard`  
**Detailed Authority:** `This file controls ...`  
**Last updated:** `[date]`

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

## 10. Resolver Template

```markdown
# [Resolver Name]

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Registry:** `docs/architecture/Trapstar_System_Registry.md`  
**Module ID:** `resolver.[name]`  
**Primary Kind:** `Resolver`  
**Architecture Role:** `[Core / Supporting]`  
**Design Maturity:** `[maturity]`  
**Activation Role for this contract or slice:** `[role]`  
**Contract Profile:** `Resolver`  
**Detailed Authority:** `This file controls ...`  
**Last updated:** `[date]`

## 1. Purpose
## 2. Owns
## 3. Does Not Own
## 4. Accepted Action Types
## 5. Action Request Inputs
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

## 11. Standard Section Guidance

### Owns and Does Not Own

State the exact category of rules or data the module controls and explicitly name nearby responsibilities it does not control.

### Inputs and Outputs

Use the smallest useful plain-data context. Rule Modules should return calculations or proposals rather than directly mutate global state.

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

### State Boundaries

List state fields the module may read and state paths it may propose changing. A proposal is not permission to mutate immediately.

### Dependencies and Integrations

Required dependencies must be few and explicit. Optional integrations must define absence behavior. Rule Modules should normally call no unrelated Rule Modules; cross-module coordination belongs in a Resolver.

### Validation and Failure

Define behavior for missing inputs, invalid IDs, forbidden actions, unavailable required modules, absent optional context, out-of-range values, and content/runtime disagreement.

Failures return explicit data. They do not silently do nothing.

### Determinism

State whether the module is fully deterministic, may use controlled randomness, records random draws or seed position, and returns the same result for identical input and seed.

Uncontrolled randomness is prohibited for gameplay truth.

### Semantic Outcome Signals

Simulation modules may report semantic facts:

```text
heat_changed
heat_threshold_crossed
relationship_shifted
information_disclosed
time_advanced
```

They must not prescribe camera shake, HUD flashing, animation names, or audio clips. The Presentation Adapter translates semantic signals into Phaser-facing cues.

### Events

Events report completed results. They do not become hidden owners of critical state changes.

---

## 12. Data Ownership Rules

```text
Content Definitions = what something is
Runtime State = what is currently true
Rule Module = how truth may change
Resolver = which modules participate and in what order
Presentation = how the result is shown
```

A value is not automatically a module:

- `heat: 3` is state;
- HEAT calculation belongs to `social.heat`;
- `currentMinute: 480` is state;
- TIME rules belong to `resource.time`.

Portable state must not contain Phaser scenes, sprites, cameras, containers, animation objects, physics bodies, DOM nodes, or event emitters.

---

## 13. Required, Optional, and Deferred Behavior

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

## 14. Design-Maturity Gates

### Design Draft

May contain unresolved mechanics. Do not implement unless an approved task defines a bounded temporary behavior.

### Design Accepted

The concept and architecture relationship are approved. It may guide naming and planning but is not code-ready by itself.

### Implementation Ready

The selected slice has:

- clear purpose and ownership;
- one Primary Kind;
- explicit inputs and outputs;
- state-read and proposed-change boundaries;
- required dependencies and optional integrations;
- failure behavior;
- determinism requirements;
- consequence participation;
- tests;
- no blocking open questions.

### Prototype Active

Implementation exists, tests pass, relevant browser behavior is verified, documentation matches behavior, and limitations are recorded.

---

## 15. Definition of Ready Checklist

Before a module is named in an implementation task:

- [ ] stable Module ID;
- [ ] one Primary Kind;
- [ ] Architecture Role recorded;
- [ ] Design Maturity permits implementation;
- [ ] Activation Role explicit for the intended slice;
- [ ] registry entry exists;
- [ ] ownership is bounded;
- [ ] profile is appropriate;
- [ ] interfaces are explicit where relevant;
- [ ] state boundaries are explicit where relevant;
- [ ] required dependencies and optional integrations are explicit;
- [ ] missing-module behavior is explicit;
- [ ] determinism is explicit;
- [ ] resolver participation is explicit where relevant;
- [ ] tests are specified;
- [ ] blocking questions are resolved.

---

## 16. Definition of Done Checklist

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

## 17. Contract Principle

```text
A module should be understandable without reading the whole game.
A module has one Primary Kind.
Architecture Role, Design Maturity, and Activation Role answer different questions.
Design Accepted does not mean Implementation Ready.
The registry sets a current-phase default; Resolver Contracts set action-specific participation.
A Resolver combines modules without becoming all of them.
A missing optional integration reduces behavior.
A missing required module fails clearly.
```