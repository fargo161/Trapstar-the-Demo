# Trapstar System Registry

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Contract standard:** `docs/architecture/Trapstar_Module_Contract_Standard.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Canonical registry of design modules, rule modules, coordinators, scenario modules, presentation layers, and infrastructure boundaries  
**Status:** Architecture Draft  
**Last updated:** 2026-07-13

---

## 1. Purpose

This registry records the major modular parts of *Trapstar the Demo* and their current status.

It exists so the project can add, defer, replace, or remove modules without forcing every other document or system to change at the same time.

The registry answers:

- What modules exist?
- What kind of module is each one?
- Is it required for the current demo?
- Is its design ready for implementation?
- What does it own?
- What does it explicitly not own?
- Which document controls its detailed rules?
- Which resolvers or other modules may depend on it?

This registry does not replace the master architecture. The master architecture controls universal project boundaries. Focused reference files control module-specific details.

---

## 2. Source-of-Truth Order

Use this order when documents overlap:

```text
README.md
-> PROJECT_STATE.md
-> docs/Trapstar_Master_System_Architecture.md
-> docs/architecture/Trapstar_System_Registry.md
-> focused module reference
-> design packet
-> Codex task
-> implementation and tests
```

Rules:

1. The master architecture controls cross-project boundaries.
2. This registry controls module identity, status, classification, and document ownership.
3. A focused module reference controls that module's detailed design.
4. A Codex task may implement only modules and details explicitly marked ready.
5. Implementation evidence may reveal a needed design change, but code does not silently override accepted documentation.

---

## 3. Module Kinds

| Kind | Meaning | Examples |
|---|---|---|
| **Design Philosophy** | A lens used to judge the whole game. It is not a runtime rule owner. | SEN |
| **Choice Frame** | Defines the player's broad strategic intent. | Deal / Pressure / Ask |
| **Action Language** | Defines how an action is expressed or modified. | BASED traits and Vibes |
| **Data Model** | Defines information or state structures. | Info Cards, Runtime State |
| **Rule Module** | Owns one bounded category of gameplay calculation. | HEAT, REP, TIME |
| **Resolver** | Coordinates the modules needed for one class of action. | InteractionResolver |
| **Scenario Module** | Owns bounded mission or run-specific truth. | Stolen Package, Run Card |
| **Presentation Module** | Collects input and displays outcomes without owning core rules. | Phaser scenes, HUD |
| **Infrastructure Module** | Supports portability, identity, saving, testing, or reproducibility. | stable IDs, seeded randomness |

These categories are intentionally different. A value, philosophy, resolver, and presentation layer should not be treated as interchangeable systems.

---

## 4. Status Vocabulary

| Status | Meaning | Implementation Use |
|---|---|---|
| **Core** | Required architectural truth. | Safe to rely on at a high level. |
| **Design Draft** | Still being defined. | Do not implement detailed behavior without an approved task. |
| **Implementation Ready** | Specific enough for bounded implementation. | May be named by a Codex task. |
| **Prototype Active** | Present in the current playable build. | Must have tests and current documentation. |
| **Optional** | May be omitted without breaking the minimum core loop. | Resolver must handle absence explicitly. |
| **Deferred** | Intentionally excluded from the current phase. | Do not implement. |
| **Experimental** | Being tested but not canonical. | Isolate behind a clear boundary. |
| **Superseded** | Replaced but retained for project history. | Do not use as current guidance. |
| **Removed** | No longer part of the accepted design. | Do not reference in new work. |

A module may also have an **activation role**:

- **Required** — the action or build cannot function correctly without it.
- **Optional Integration** — contributes extra consequences when enabled.
- **Deferred Integration** — recognized by architecture but intentionally absent.

---

## 5. Universal Module Rules

Every module must follow these project-wide rules:

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

Required boundaries:

- Modules own one clear category of responsibility.
- Modules do not directly command unrelated modules.
- Resolvers coordinate intersections but do not absorb every internal rule.
- Authoritative gameplay state remains portable and contains no Phaser objects.
- Gameplay truth uses stable IDs rather than scene, sprite, or physics-object identity.
- Randomness affecting gameplay truth must be controlled and reproducible.
- Presentation may request actions and display outcomes; it does not invent consequences.
- Optional modules must have explicit absence behavior.
- Missing required modules must fail clearly rather than producing partial hidden behavior.
- Detailed numeric rules belong in focused references, not in this registry.

---

## 6. Current Registry

### 6.1 Design and Interaction Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `design.sen` | SEN | Design Philosophy | Core | Required | Current master architecture; focused SEN file planned |
| `interaction.dpa` | Deal / Pressure / Ask | Choice Frame | Core / Design Draft | Required | Current master architecture; focused DPA file planned |
| `interaction.based` | BASED Traits and Vibes | Action Language | Design Draft | Required before social-action implementation | Focused BASED reference planned |

#### `design.sen`

**Owns:** The Structured / Emergent / Negotiated philosophy used to judge situations, pressure, and consequences.  
**Does not own:** Runtime state mutation, action validation, HEAT, REP, TIME, Info, or presentation behavior.

#### `interaction.dpa`

**Owns:** The selected strategic frame: Deal, Pressure, or Ask.  
**Does not own:** The consequence calculations attached to the selected frame.

#### `interaction.based`

**Owns:** The manner, tone, Vibe, modifiers, permissions, and future abilities used to express an action.  
**Does not own:** Direct REP, HEAT, TIME, Info, inventory, mission, or Phaser mutations.

---

### 6.2 Information and Social Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `data.information` | Soft / Hard Information Model | Data Model | Design Draft | Required | Focused information model planned |
| `data.info_cards` | Info Cards | Data Model | Design Draft | Required | Existing Info Card reference should become authority |
| `social.heat` | HEAT | Rule Module | Design Draft | Optional for earliest foundation; required for intended demo | Existing HEAT scope reference should become authority |
| `social.rep` | REP / Relationship | Rule Module | Design Draft | Optional for earliest foundation; required for intended demo | Existing REP scope reference should become authority |
| `social.fac` | FAC | Rule Module / Data Model | Deferred | Deferred | Focused FAC reference planned |
| `social.favor` | FAVOR | Rule Module / Data Model | Deferred | Deferred | Focused FAVOR reference planned |
| `social.access` | ACCESS | Rule Module / Data Model | Design Draft | Likely required for traversal and social gating | Focused ACCESS reference planned |
| `social.lore` | LORE | Data Model / Rule Module | Deferred | Deferred | Focused LORE reference planned |

#### Required separation

- Information truth is not the same as HEAT, REP, or faction strength.
- Social Asset values are data; their corresponding rule modules determine how those values change.
- Info disclosure is owned by the Information module, even when another module influences the likelihood or cost.

---

### 6.3 Resource and Survival Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `resource.inventory` | Inventory and Item Transfer | Rule Module | Design Draft | Required later | Hard Assets reference planned |
| `resource.money_contra` | Money and Contra Economy | Rule Module | Design Draft | Required later | Economy reference planned |
| `resource.weapons` | Weapons and Legality State | Rule Module / Data Model | Deferred | Deferred until conflict scope is ready | Weapons reference planned |
| `resource.sustenance` | Sustenance | Data Model / Rule Module | Deferred | Deferred | Survival reference planned |
| `resource.time` | TIME Cost and Advancement | Rule Module | Design Draft | Required for intended demo | TIME reference planned |
| `resource.energy` | Energy and Survival Pressure | Rule Module | Deferred | Deferred until core interaction works | Energy / survival reference planned |

#### Required separation

- Time as a stored value is part of runtime state.
- The TIME module owns minute costs, advancement, and time-triggered proposals.
- Animation duration never determines in-world TIME cost.
- Inventory owns material transfers; social modules may influence eligibility or consequence but do not perform hidden inventory changes.

---

### 6.4 World, Scenario, and Conflict Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `world.map` | Map and Traversal | Rule Module / Data Model | Design Draft | Required later | Map and traversal reference planned |
| `world.schedule` | NPC Schedules | Rule Module | Deferred | Deferred | Schedule reference planned |
| `scenario.stolen_package` | Stolen Package Mission | Scenario Module | Design Draft | Required | Focused demo-scope reference planned |
| `scenario.run_card` | Run-Card Generator | Scenario / Infrastructure Module | Design Draft | Required later | Run-card reference planned |
| `conflict.combat` | Combat Alert State | Rule Module | Deferred | Deferred | Combat reference planned |

#### Required separation

- The mission owns objective truth, guilt, lying, truth-telling roles, and win/failure conditions.
- The run-card generator establishes starting truth; it does not create Phaser objects.
- The world module owns locations, routes, and traversal legality; ACCESS may modify permissions but does not own map geometry.
- Combat is a crisis-state module, not the universal resolution path.

---

### 6.5 Resolver Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `resolver.interaction` | InteractionResolver | Resolver | Design Draft | Required for first social prototype | Action-resolution reference planned |
| `resolver.street_action` | StreetActionResolver | Resolver | Deferred | Deferred | Future action-resolution reference |
| `resolver.travel` | TravelResolver | Resolver | Deferred | Deferred | Future traversal reference |
| `resolver.combat` | CombatResolver | Resolver | Deferred | Deferred | Future combat reference |
| `resolver.end_of_day` | EndOfDayResolver | Resolver | Deferred | Deferred | Future run-structure reference |
| `resolver.run_setup` | RunSetupResolver | Resolver | Design Draft | Required when seeded runs begin | Run-card reference planned |

Resolvers may know which modules participate and in what order. They must not recreate the internal rules of those modules.

---

### 6.6 Runtime and Infrastructure Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `runtime.content_definitions` | Content Definitions | Data Model | Core / Design Draft | Required | Technical architecture reference planned |
| `runtime.state` | Authoritative Runtime State | Data Model | Core / Design Draft | Required | Technical architecture reference planned |
| `runtime.state_transition` | Ordered State Transition | Infrastructure Module | Core / Design Draft | Required | Consequence-order reference planned |
| `runtime.outcome` | ResolvedOutcome | Data Model | Core / Design Draft | Required | Action-resolution reference planned |
| `infra.ids` | Stable IDs | Infrastructure Module | Core | Required | Portability reference planned |
| `infra.random` | Seeded Randomness | Infrastructure Module | Core / Design Draft | Required when randomness affects truth | Portability reference planned |
| `infra.save` | Save-State Schema | Infrastructure Module | Deferred | Deferred | Save-data reference planned |
| `infra.tests` | Engine-Light Simulation Tests | Infrastructure Module | Core | Required for implemented rules | Task-specific tests plus technical standards |

---

### 6.7 Presentation Layer

| Module ID | Name | Kind | Status | Demo Role | Detailed Authority |
|---|---|---|---|---|---|
| `presentation.phaser` | Phaser 3.90 Runtime | Presentation Module | Core technical direction | Required for browser demo | Phaser portability boundary planned |
| `presentation.adapter` | Presentation Adapter | Presentation / Boundary Module | Design Draft | Required when implementation begins | Action-resolution reference planned |
| `presentation.blackboard` | Runtime Blackboard | Presentation Module | Draft / Paused | Useful first debug presentation | Current Phaser task, presently paused pending system detail |
| `presentation.assets` | Asset and Animation Standards | Infrastructure / Presentation Standard | Design Draft | Required before production assets | Asset standards reference planned |

Presentation modules may display state, gather input, play animation, move cameras, update UI, and emit non-authoritative notifications after resolution. They do not own gameplay truth.

---

## 7. Provisional Implementation Gate

The current Phaser runtime-blackboard task should not begin until the modules it depends on are sufficiently defined.

Recommended prerequisites:

| Dependency | Minimum status before implementation |
|---|---|
| `interaction.dpa` | Implementation Ready |
| `interaction.based` | Implementation Ready for the selected test Vibes |
| `data.information` | Implementation Ready for the selected Soft/Hard Info behavior |
| `resource.time` | Implementation Ready for the selected action costs |
| `social.rep` | Either Implementation Ready or explicitly excluded |
| `social.heat` | Either Implementation Ready or explicitly excluded |
| `resolver.interaction` | Implementation Ready |
| `runtime.state` | Implementation Ready for the thin slice |
| `runtime.outcome` | Implementation Ready for the thin slice |

No task should silently use draft modules by inventing missing mechanics.

---

## 8. Optional-Module Behavior

A resolver must classify each participating module as required or optional.

### Missing required module

```text
Missing required module
-> validation fails
-> no authoritative transition occurs
-> ResolvedOutcome records the reason
```

### Missing optional module

```text
Optional module disabled
-> resolver skips that contribution
-> outcome records that the module was not consulted
-> remaining required modules continue normally
```

Example:

```text
Ask action
- Information: required
- TIME: required
- BASED: required if a Vibe was selected
- REP: optional integration
- HEAT: optional integration
- Faction: deferred integration
```

The exact required/optional list belongs in the relevant resolver or task reference.

---

## 9. Change-Control Rules

When a module changes status:

1. Update this registry.
2. Update the focused reference if one exists.
3. Review any active tasks that depend on it.
4. Review resolver contracts that require it.
5. Do not rewrite unrelated modules unless the contract actually changed.
6. Record whether the change affects save data, deterministic tests, or presentation cues.

When a module is removed:

- replace hard dependencies with explicit validation failures or alternate modules;
- remove it from resolver participation lists;
- preserve historical references only when useful;
- do not leave hidden state fields or listeners that still assume it exists.

---

## 10. Next Documentation Priorities

Recommended order:

1. Finalize `Trapstar_Module_Contract_Standard.md`.
2. Extract and refine the BASED focused reference.
3. Extract the DPA focused reference.
4. Define the Information model and Info Card authority.
5. Define the minimum TIME contract.
6. Decide whether REP and HEAT participate in the first prototype or remain excluded.
7. Define `InteractionResolver`, `ActionRequest`, `StateChange`, and `ResolvedOutcome` contracts.
8. Rewrite or renumber the paused Phaser runtime-blackboard task after its dependencies are ready.

---

## 11. Registry Principle

```text
The master architecture explains how the whole project fits together.
The registry identifies what modules exist and whether they are ready.
Focused references define how each module works.
Resolvers combine only the modules needed for a specific action.
Codex tasks implement only approved, named contracts.
```
