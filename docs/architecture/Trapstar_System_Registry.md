# Trapstar System Registry

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Contract standard:** `docs/architecture/Trapstar_Module_Contract_Standard.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Canonical registry of module identity, classification, maturity, Demo Default Activation, and detailed authority  
**Architecture role:** Core architecture document  
**Design maturity:** Design Accepted  
**Last updated:** 2026-07-13

---

## 1. Purpose

This registry records the modular parts of *Trapstar the Demo* without treating philosophies, data, rule modules, resolvers, presentation, and infrastructure as the same kind of thing.

It exists so modules can be refined, enabled, disabled, deferred, replaced, or removed without forcing the entire project to change at once.

This registry controls:

- stable Module IDs;
- one Primary Kind per module;
- Architecture Role;
- Design Maturity;
- Demo Default Activation;
- detailed-authority location;
- high-level ownership boundaries.

The master architecture controls universal cross-project boundaries. Focused references control module-specific detail.

---

## 2. Domain-Based Document Authority

| Document or artifact | Authority domain |
|---|---|
| `README.md` | Introduction and navigation. |
| `PROJECT_STATE.md` | Current phase, blockers, priorities, and approved next work. |
| `docs/Trapstar_Master_System_Architecture.md` | Universal design relationships, prohibitions, and technical boundaries. |
| This registry | Module identity, Primary Kind, Architecture Role, Design Maturity, Demo Default Activation, and detailed-authority location. |
| Focused module reference | Detailed rules, structures, values, limits, and open questions for one module. |
| Design packet | Implementation-ready feature or content specification. |
| Resolver Contract | Action-specific module participation and consequence order. |
| Codex task | One bounded approved work order. |
| Implementation and tests | Evidence that approved behavior works. |

Conflict routing:

```text
Current phase or next-work conflict
-> PROJECT_STATE.md

Universal architecture conflict
-> Master System Architecture

Module identity, classification, maturity, or demo-default activation conflict
-> System Registry

Module-specific rule conflict
-> Focused module reference

Action-specific participation conflict
-> Approved Resolver Contract

Bounded implementation-scope conflict
-> Approved Codex task, within higher authority
```

---

## 3. Classification Fields

### 3.1 Primary Kind

Every module has exactly one Primary Kind.

| Primary Kind | Meaning |
|---|---|
| **Design Philosophy** | Project-wide design lens without runtime rule ownership. |
| **Choice Frame** | Broad player strategic intent. |
| **Action Language** | Manner, tone, modifiers, permissions, or ability expression. |
| **Data Model** | Portable structure or authoritative data shape. |
| **Rule Module** | One bounded category of gameplay calculation. |
| **Resolver** | Explicit coordinator for a class of action. |
| **Scenario Module** | Mission-specific or run-specific truth. |
| **Presentation Module** | Input and display behavior without simulation authority. |
| **Infrastructure Module** | Identity, transition, save, test, asset-standard, portability, or reproducibility support. |

A module may own data or use infrastructure without receiving a second Primary Kind.

### 3.2 Architecture Role

| Architecture Role | Meaning |
|---|---|
| **Core** | Foundational to project identity or minimum architecture. |
| **Supporting** | Additive, specialized, or phase-dependent. |

### 3.3 Design Maturity

| Design Maturity | Meaning | Implementation use |
|---|---|---|
| **Design Draft** | Important design details remain unresolved. | Do not implement detailed behavior unless a task explicitly defines a bounded temporary behavior. |
| **Design Accepted** | Concept and architectural relationship are accepted, but the implementation-facing contract is incomplete. | Safe for naming, planning, compatibility, and high-level design; not sufficient by itself for implementation. |
| **Implementation Ready** | The selected slice has complete ownership, interfaces, dependencies, failure behavior, determinism, order, and tests. | May be named by a bounded Codex task. |
| **Prototype Active** | Implemented, tested, verified, and accurately documented. | Safe to rely on within recorded limitations. |
| **Experimental** | Isolated test not yet canonical. | Keep behind a clear boundary. |
| **Superseded** | Replaced but retained for history. | Do not use as current guidance. |
| **Removed** | No longer accepted. | Do not reference in new work. |

### 3.4 Demo Default Activation

This field records the module's expected default participation in the intended course demo. It is independent of whether implementation work is active today.

| Demo Default Activation | Meaning |
|---|---|
| **Required** | Expected to be necessary for the intended demo architecture or target slice. |
| **Optional Integration** | May contribute when enabled; absence must be explicit. |
| **Deferred Integration** | Intentionally absent from the current demo target. |

Three different questions are controlled in three places:

```text
System Registry
-> Demo Default Activation

PROJECT_STATE.md
-> current production status: Active / Paused / Blocked / Not yet scheduled

Resolver Contract
-> action-specific participation: Required / Optional Integration / Not Consulted
```

Example:

```text
social.heat
Demo Default Activation: Optional Integration
Current production status: Not yet Implementation Ready

Public Pressure action: Required
Private Ask action: Optional Integration
Inventory-only action: Not Consulted
```

A resolver may differ from the demo default only within its approved action scope and must document the difference.

---

## 4. Universal Module Rules

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

- Each module has one Primary Kind and one bounded responsibility.
- Modules do not directly command unrelated modules.
- Resolvers coordinate intersections without absorbing every rule.
- Portable gameplay state contains no Phaser objects.
- Stable IDs, not engine objects, establish identity.
- Gameplay randomness is controlled and reproducible.
- Presentation displays outcomes; it does not invent them.
- Missing required modules fail clearly.
- Missing optional integrations follow explicit reduced behavior.
- Deferred integrations create no hidden placeholder behavior.

---

## 5. Current Registry

### 5.1 Design and interaction

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `design.sen` | SEN | Design Philosophy | Core | Design Accepted | Required | Current master architecture; focused SEN reference planned |
| `interaction.dpa` | Deal / Pressure / Ask | Choice Frame | Core | Design Accepted | Required | Current master architecture; focused DPA reference planned |
| `interaction.based` | BASED Traits and Vibes | Action Language | Core | Design Draft | Required | Focused BASED reference planned |

### 5.2 Information and social

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `data.information` | Soft / Hard Information Model | Data Model | Core | Design Draft | Required | Focused information model planned |
| `data.info_cards` | Info Cards | Data Model | Core | Design Draft | Required | Focused Info Card reference planned |
| `social.heat` | HEAT | Rule Module | Supporting | Design Draft | Optional Integration | Focused HEAT reference planned |
| `social.rep` | REP / Relationship | Rule Module | Supporting | Design Draft | Optional Integration | Focused REP reference planned |
| `social.fac` | FAC | Rule Module | Supporting | Design Draft | Deferred Integration | Focused FAC reference planned |
| `social.favor` | FAVOR | Rule Module | Supporting | Design Draft | Deferred Integration | Focused FAVOR reference planned |
| `social.access` | ACCESS | Rule Module | Supporting | Design Draft | Deferred Integration | Focused ACCESS reference planned |
| `social.lore` | LORE | Rule Module | Supporting | Design Draft | Deferred Integration | Focused LORE reference planned |

### 5.3 Resources and survival

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `resource.inventory` | Inventory and Item Transfer | Rule Module | Supporting | Design Draft | Deferred Integration | Inventory reference planned |
| `resource.money_contra` | Money and Contra Economy | Rule Module | Supporting | Design Draft | Deferred Integration | Economy reference planned |
| `resource.weapons` | Weapons and Legality | Rule Module | Supporting | Design Draft | Deferred Integration | Weapons reference planned |
| `resource.sustenance` | Sustenance | Rule Module | Supporting | Design Draft | Deferred Integration | Survival reference planned |
| `resource.time` | TIME Cost and Advancement | Rule Module | Core | Design Draft | Required | TIME reference planned |
| `resource.energy` | Energy and Survival Pressure | Rule Module | Supporting | Design Draft | Deferred Integration | Energy / survival reference planned |

### 5.4 World, scenario, and conflict

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `world.map` | Map and Traversal | Rule Module | Supporting | Design Draft | Deferred Integration | Map and traversal reference planned |
| `world.schedule` | NPC Schedules | Rule Module | Supporting | Design Draft | Deferred Integration | Schedule reference planned |
| `scenario.stolen_package` | Stolen Package Mission | Scenario Module | Core | Design Draft | Required | Focused demo-scope reference planned |
| `scenario.run_card` | Run-Card Generator | Scenario Module | Supporting | Design Draft | Deferred Integration | Run-card reference planned |
| `conflict.combat` | Combat Alert State | Rule Module | Supporting | Design Draft | Deferred Integration | Combat reference planned |

The Stolen Package premise is accepted high-level design, but the module remains Design Draft because its detailed scenario contract is not complete.

### 5.5 Resolvers

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `resolver.interaction` | InteractionResolver | Resolver | Core | Design Draft | Required | Action-resolution reference planned |
| `resolver.street_action` | StreetActionResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future action-resolution reference |
| `resolver.travel` | TravelResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future traversal reference |
| `resolver.combat` | CombatResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future combat reference |
| `resolver.end_of_day` | EndOfDayResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future run-structure reference |
| `resolver.run_setup` | RunSetupResolver | Resolver | Supporting | Design Draft | Deferred Integration | Run-card reference planned |

### 5.6 Runtime and infrastructure

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `runtime.content_definitions` | Content Definitions | Data Model | Core | Design Draft | Required | Technical architecture reference planned |
| `runtime.state` | Authoritative Runtime State | Data Model | Core | Design Draft | Required | Technical architecture reference planned |
| `runtime.outcome` | ResolvedOutcome | Data Model | Core | Design Draft | Required | Action-resolution reference planned |
| `runtime.state_transition` | Ordered State Transition | Infrastructure Module | Core | Design Draft | Required | Consequence-order reference planned |
| `infra.ids` | Stable IDs | Infrastructure Module | Core | Design Accepted | Required | Current master portability rules; focused reference planned |
| `infra.random` | Seeded Randomness | Infrastructure Module | Core | Design Accepted | Optional Integration | Current master portability rules; focused reference planned |
| `infra.save` | Save-State Schema | Infrastructure Module | Supporting | Design Draft | Deferred Integration | Save-data reference planned |
| `infra.tests` | Engine-Light Simulation Tests | Infrastructure Module | Core | Design Draft | Required | Technical standards planned |
| `infra.asset_standards` | Asset and Animation Standards | Infrastructure Module | Supporting | Design Accepted | Deferred Integration | Current master asset-portability rules; focused reference planned |

`infra.asset_standards` owns engine-independent naming, frame dimensions, origins, anchors, layer alignment, animation metadata, export requirements, and portable asset compatibility. Phaser loading and playback remain presentation responsibilities.

### 5.7 Presentation

| Module ID | Name | Primary Kind | Architecture Role | Design Maturity | Demo Default Activation | Detailed Authority |
|---|---|---|---|---|---|---|
| `presentation.phaser` | Phaser 3.90 Runtime | Presentation Module | Core | Design Accepted | Required | Current master engine boundary; focused reference planned |
| `presentation.adapter` | Presentation Adapter | Presentation Module | Core | Design Draft | Required | Action-resolution reference planned |
| `presentation.blackboard` | Runtime Blackboard | Presentation Module | Supporting | Design Draft | Required | Paused Task 002; focused contract required before reactivation |

---

## 6. Complete Task 002 Implementation Gate

Task 002 remains paused until every required contract below is Implementation Ready for the selected thin slice.

### 6.1 Required interaction contracts

```text
interaction.dpa
interaction.based
data.information
data.info_cards
resource.time
resolver.interaction
```

### 6.2 Required runtime contracts

```text
runtime.content_definitions
runtime.state
runtime.state_transition
runtime.outcome
```

### 6.3 Required infrastructure contracts

```text
infra.ids
infra.tests
```

### 6.4 Required presentation contracts

```text
presentation.phaser
presentation.adapter
presentation.blackboard
```

A contract is a prerequisite. The implementation of `presentation.blackboard`, and any other approved implementation deliverable, may be produced by Task 002 only after its contract is Implementation Ready.

### 6.5 Conditional contracts

`infra.random` is required only if the approved slice uses randomized gameplay truth. Otherwise, the revised task must explicitly declare a fully deterministic non-random path.

`social.rep` and `social.heat` must each be either:

- Implementation Ready and included; or
- explicitly excluded from the revised slice.

### 6.6 Shared structure ownership

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

No task may silently use a Design Draft or Design Accepted module as if it were Implementation Ready, and no shared structure may be introduced without one recorded owner.

---

## 7. Change Control

When a module changes Primary Kind, Architecture Role, Design Maturity, Demo Default Activation, ownership, or authority:

1. update this registry;
2. update its focused reference when one exists;
3. review affected resolver contracts;
4. review active and paused tasks;
5. review state, save, test, and semantic-signal impact;
6. avoid rewriting unrelated modules without a real contract change.

---

## 8. Registry Principle

```text
The master explains how the whole project fits together.
The registry identifies each module, its one kind, its role, its maturity, and its Demo Default Activation.
PROJECT_STATE records what work is active, paused, blocked, or unscheduled.
Focused references define module detail.
Resolver Contracts define action-specific participation.
Codex tasks implement only approved named contracts.
```