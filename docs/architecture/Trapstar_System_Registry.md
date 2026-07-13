# Trapstar System Registry

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Contract standard:** `docs/architecture/Trapstar_Module_Contract_Standard.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Canonical registry of module identity, classification, maturity, Demo Default Activation, ownership, and detailed authority  
**Architecture role:** Core architecture document  
**Design maturity:** Design Accepted  
**Last updated:** 2026-07-13

---

## 1. Purpose

This registry identifies the modular parts of *Trapstar the Demo* without treating philosophies, data models, rule modules, resolvers, presentation, and infrastructure as the same kind of thing.

It controls:

- stable Module IDs;
- exactly one Primary Kind per module;
- Architecture Role;
- Design Maturity;
- Demo Default Activation;
- high-level ownership boundaries;
- detailed-authority locations.

The master architecture controls universal boundaries. Focused references control module-specific detail. Resolver Contracts control action-specific participation and order.

---

## 2. Domain-Based Authority

| Document or artifact | Authority domain |
|---|---|
| `README.md` | Introduction and navigation. |
| `PROJECT_STATE.md` | Current phase, blockers, priorities, and approved next work. |
| Master System Architecture | Universal design relationships, prohibitions, and technical boundaries. |
| This registry | Module identity, kind, role, maturity, Demo Default Activation, ownership, and authority location. |
| Focused module reference | Detailed rules, structures, values, limits, and open questions for one module. |
| Resolver Contract | Action-specific participation, validation, coordination, and consequence order. |
| Codex task | One bounded approved implementation order. |
| Implementation and tests | Evidence that approved behavior works. |

Conflict routing:

```text
Current phase or next work
-> PROJECT_STATE.md

Universal architecture
-> Master System Architecture

Module identity, classification, maturity, ownership, or demo default
-> System Registry

Module-specific rules
-> focused module reference

Action-specific participation or order
-> approved Resolver Contract

Bounded implementation scope
-> approved Codex task, within higher authority
```

---

## 3. Classification Fields

### 3.1 Primary Kind

Every module has exactly one Primary Kind.

| Primary Kind | Meaning |
|---|---|
| Design Philosophy | Project-wide design lens without runtime rule ownership. |
| Choice Frame | Broad player strategic intent. |
| Action Language | Manner, tone, modifiers, permissions, or ability expression. |
| Data Model | Portable structure or authoritative data shape. |
| Rule Module | One bounded category of gameplay calculation. |
| Resolver | Explicit coordinator for a class of action. |
| Scenario Module | Mission-specific or run-specific truth. |
| Presentation Module | Input and display behavior without simulation authority. |
| Infrastructure Module | Identity, transition, save, test, asset-standard, portability, or reproducibility support. |

A Data Model may describe state but does not calculate how that state changes. A Rule Module may calculate or propose changes but does not own unrelated data shapes.

### 3.2 Architecture Role

- **Core** — foundational to project identity or minimum architecture.
- **Supporting** — additive, specialized, or phase-dependent.

### 3.3 Design Maturity

| Maturity | Meaning | Implementation use |
|---|---|---|
| Design Draft | Important details remain unresolved. | Do not implement unless a task defines a bounded temporary behavior. |
| Design Accepted | Concept and architecture relationship are accepted; implementation contract is incomplete. | Safe for planning and naming, not code-ready by itself. |
| Implementation Ready | Selected slice has explicit ownership, interfaces, dependencies, failure behavior, determinism, order, and tests. | May be named by a bounded Codex task. |
| Prototype Active | Implemented, tested, verified, and accurately documented. | Safe within recorded limitations. |
| Experimental | Isolated trial, not canonical. | Keep behind a boundary. |
| Superseded | Replaced but retained for history. | Do not use as current guidance. |
| Removed | No longer accepted. | Do not reference in new work. |

### 3.4 Demo Default Activation

This field describes expected participation in the intended course demo, independent of whether work is active now.

- **Required** — expected to be necessary for the intended demo architecture.
- **Optional Integration** — may contribute when enabled; absence must be explicit.
- **Deferred Integration** — intentionally absent from the current demo target.

Separate concepts:

```text
System Registry
-> Demo Default Activation

PROJECT_STATE.md
-> current production status: Active / Paused / Blocked / Not yet scheduled

Resolver Contract
-> action-specific participation: Required / Optional Integration / Not Consulted
```

---

## 4. Universal Module Rules

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

- Each module has one Primary Kind and one bounded responsibility.
- Modules do not directly command unrelated modules.
- Resolvers coordinate intersections without absorbing every internal rule.
- Portable gameplay state contains no Phaser objects.
- Stable IDs, not engine objects, establish identity.
- Gameplay randomness is controlled and reproducible.
- Presentation displays outcomes; it does not invent them.
- Missing required modules fail clearly.
- Missing optional integrations follow explicit reduced behavior.
- Deferred integrations create no hidden placeholder behavior.
- Every shared structure has one recorded owner.

---

## 5. Current Registry

### 5.1 Design and interaction

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `design.sen` | SEN | Design Philosophy | Core | Design Accepted | Required | Master architecture; focused SEN reference planned |
| `interaction.dpa` | Deal / Pressure / Ask | Choice Frame | Core | Design Accepted | Required | Master architecture; focused DPA reference planned |
| `interaction.based` | BASED Traits and Vibes | Action Language | Core | Design Draft | Required | Focused BASED reference planned |

### 5.2 Information and social

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `data.information` | Soft / Hard Information State | Data Model | Core | Design Draft | Required | Focused information-state model planned |
| `data.info_cards` | Info Cards | Data Model | Core | Design Draft | Required | Focused Info Card reference planned |
| `information.rules` | Information Disclosure and Hardening | Rule Module | Core | Design Draft | Required | Focused information-rules reference planned |
| `social.heat` | HEAT | Rule Module | Supporting | Design Draft | Optional Integration | Focused HEAT reference planned |
| `social.rep` | REP / Relationship | Rule Module | Supporting | Design Draft | Optional Integration | Focused REP reference planned |
| `social.fac` | FAC | Rule Module | Supporting | Design Draft | Deferred Integration | Focused FAC reference planned |
| `social.favor` | FAVOR | Rule Module | Supporting | Design Draft | Deferred Integration | Focused FAVOR reference planned |
| `social.access` | ACCESS | Rule Module | Supporting | Design Draft | Deferred Integration | Focused ACCESS reference planned |
| `social.lore` | LORE | Rule Module | Supporting | Design Draft | Deferred Integration | Focused LORE reference planned |

Ownership separation:

```text
data.info_cards
-> InfoCard schema

data.information
-> Soft / Hard classification, truth state, knowledge state,
   verification state, and proof relationships

information.rules
-> disclosure, withholding, hardening, reveal eligibility,
   proposed information-state changes, and semantic signals
```

`data.information` does not calculate disclosure or hardening. `information.rules` does not redefine the information-state schema.

### 5.3 Resources and survival

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `resource.inventory` | Inventory and Item Transfer | Rule Module | Supporting | Design Draft | Deferred Integration | Inventory reference planned |
| `resource.money_contra` | Money and Contra Economy | Rule Module | Supporting | Design Draft | Deferred Integration | Economy reference planned |
| `resource.weapons` | Weapons and Legality | Rule Module | Supporting | Design Draft | Deferred Integration | Weapons reference planned |
| `resource.sustenance` | Sustenance | Rule Module | Supporting | Design Draft | Deferred Integration | Survival reference planned |
| `resource.time` | TIME Cost and Advancement | Rule Module | Core | Design Draft | Required | TIME reference planned |
| `resource.energy` | Energy and Survival Pressure | Rule Module | Supporting | Design Draft | Deferred Integration | Energy reference planned |

### 5.4 World, scenario, and conflict

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `world.map` | Map and Traversal | Rule Module | Supporting | Design Draft | Deferred Integration | Map reference planned |
| `world.schedule` | NPC Schedules | Rule Module | Supporting | Design Draft | Deferred Integration | Schedule reference planned |
| `scenario.stolen_package` | Stolen Package Mission | Scenario Module | Core | Design Draft | Required | Demo-scope reference planned |
| `scenario.run_card` | Run-Card Generator | Scenario Module | Supporting | Design Draft | Deferred Integration | Run-card reference planned |
| `conflict.combat` | Combat Alert State | Rule Module | Supporting | Design Draft | Deferred Integration | Combat reference planned |

### 5.5 Resolvers

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `resolver.interaction` | InteractionResolver | Resolver | Core | Design Draft | Required | Action-resolution reference planned |
| `resolver.street_action` | StreetActionResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future reference |
| `resolver.travel` | TravelResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future reference |
| `resolver.combat` | CombatResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future reference |
| `resolver.end_of_day` | EndOfDayResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future reference |
| `resolver.run_setup` | RunSetupResolver | Resolver | Supporting | Design Draft | Deferred Integration | Run-card reference planned |

`resolver.interaction` accepts supported interaction requests and owns interaction-specific validation and coordination. It does not own the generic request envelope.

### 5.6 Runtime and infrastructure

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `runtime.content_definitions` | Content Definitions | Data Model | Core | Design Draft | Required | Technical reference planned |
| `runtime.action_request` | Generic ActionRequest | Data Model | Core | Design Draft | Required | Action-request reference planned |
| `runtime.state` | Authoritative Runtime State | Data Model | Core | Design Draft | Required | Technical reference planned |
| `runtime.outcome` | ResolvedOutcome | Data Model | Core | Design Draft | Required | Action-resolution reference planned |
| `runtime.state_transition` | Ordered State Transition | Infrastructure Module | Core | Design Draft | Required | Consequence-order reference planned |
| `infra.ids` | Stable IDs | Infrastructure Module | Core | Design Accepted | Required | Master portability rules; focused reference planned |
| `infra.random` | Seeded Randomness | Infrastructure Module | Core | Design Accepted | Optional Integration | Master portability rules; focused reference planned |
| `infra.save` | Save-State Schema | Infrastructure Module | Supporting | Design Draft | Deferred Integration | Save reference planned |
| `infra.tests` | Engine-Light Simulation Tests | Infrastructure Module | Core | Design Draft | Required | Technical standards planned |
| `infra.asset_standards` | Asset and Animation Standards | Infrastructure Module | Supporting | Design Accepted | Deferred Integration | Master asset rules; focused reference planned |

`runtime.action_request` owns the routing-neutral request envelope that exists before specialized resolver selection. It does not own resolver selection, action validity, DPA or BASED mechanics, consequence order, or state mutation.

### 5.7 Presentation

| Module ID | Name | Primary Kind | Role | Maturity | Demo Default | Detailed Authority |
|---|---|---|---|---|---|---|
| `presentation.phaser` | Phaser 3.90 Runtime | Presentation Module | Core | Design Accepted | Required | Master engine boundary; focused reference planned |
| `presentation.adapter` | Presentation Adapter | Presentation Module | Core | Design Draft | Required | Action-resolution reference planned |
| `presentation.blackboard` | Runtime Blackboard | Presentation Module | Supporting | Design Draft | Required | Paused Task 002; focused contract required |

The Presentation Adapter may construct or translate player intent into a generic `ActionRequest`, but it does not own that request schema.

---

## 6. Complete Task 002 Gate

Every required contract below must be Implementation Ready for the selected thin slice.

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

### Conditional contracts

- `infra.random` is required when gameplay truth uses randomness; otherwise the task declares a deterministic non-random path.
- `social.rep` and `social.heat` are each Implementation Ready and included, or explicitly excluded.

A contract is a prerequisite. Its implementation may still be produced by Task 002 after the contract is ready.

### Shared ownership for the slice

| Structure or responsibility | Owner |
|---|---|
| `InfoCard` schema | `data.info_cards` |
| Soft / Hard state and classification | `data.information` |
| disclosure, withholding, hardening, reveal eligibility | `information.rules` |
| `ContentDefinitions` | `runtime.content_definitions` |
| generic `ActionRequest` | `runtime.action_request` |
| `RuntimeState` | `runtime.state` |
| interaction validation policy | `resolver.interaction` |
| `InteractionValidationResult` | `resolver.interaction` |
| `StateChange` and transition application | `runtime.state_transition` |
| `ResolvedOutcome` | `runtime.outcome` |
| stable identity | `infra.ids` |
| controlled random source | `infra.random` |
| test harness and deterministic acceptance rules | `infra.tests` |
| presentation instructions | `presentation.adapter` |
| blackboard display model and controls | `presentation.blackboard` |

No task may use a Design Draft or Design Accepted module as if it were Implementation Ready, and no shared structure may have duplicate or implicit ownership.

---

## 7. Change Control

When a module changes kind, role, maturity, Demo Default Activation, ownership, or authority:

1. update this registry;
2. update its focused reference when one exists;
3. review affected Resolver Contracts;
4. review active and paused tasks;
5. review state, save, test, and semantic-signal impact;
6. avoid rewriting unrelated modules without real contract impact.

---

## 8. Registry Principle

```text
The master explains how the whole project fits together.
The registry identifies each module and its ownership.
PROJECT_STATE records current work.
Focused references define module detail.
Resolver Contracts define action-specific participation.
Codex tasks implement only approved named contracts.
```
