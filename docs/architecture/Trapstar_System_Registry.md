# Trapstar System Registry

**Parent architecture:** `docs/Trapstar_Master_System_Architecture.md`  
**Contract standard:** `docs/architecture/Trapstar_Module_Contract_Standard.md`  
**Project:** *Trapstar the Demo*  
**Document role:** Canonical registry of module identity, classification, readiness, activation, and detailed authority  
**Architecture role:** Core architecture document  
**Design maturity:** Design Draft  
**Last updated:** 2026-07-13

---

## 1. Purpose

This registry records the modular parts of *Trapstar the Demo* without treating every concept as the same kind of system.

It exists so modules can be refined, enabled, disabled, deferred, replaced, or removed without forcing the entire project to change at once.

The registry answers:

- What modules exist?
- What is each module's one primary kind?
- Is the module architecturally core or supporting?
- How mature is its design?
- Is it required, optional, or deferred for the current scope?
- What does it own?
- What does it explicitly not own?
- Which focused document controls its detailed rules?

This registry does not replace the master architecture. The master architecture controls universal cross-project boundaries. Focused references control module-specific details.

---

## 2. Domain-Based Document Authority

The repository does not use one linear override chain. Each document controls a different domain of truth.

| Document or artifact | Authority domain |
|---|---|
| `README.md` | Project introduction, navigation, and reading entry point. |
| `PROJECT_STATE.md` | Current phase, current blockers, active priorities, and approved next work. |
| `docs/Trapstar_Master_System_Architecture.md` | Universal design relationships, technical boundaries, and cross-module architecture rules. |
| `docs/architecture/Trapstar_System_Registry.md` | Module identity, primary kind, architecture role, design maturity, activation role, and detailed-authority location. |
| Focused module reference | Detailed rules, data, formulas, limits, and open questions for one module. |
| Design packet | Implementation-ready feature or content specification assembled from accepted references. |
| Codex task | One bounded, approved work order. A task does not silently redefine architecture or module rules. |
| Implementation and tests | Evidence that approved behavior works. Code does not silently overrule accepted documentation. |

### 2.1 Conflict routing

When documents disagree, route the conflict by subject:

```text
Current phase, blocker, or next-task conflict
-> PROJECT_STATE.md

Universal design or cross-module boundary conflict
-> Master System Architecture

Module identity, classification, readiness, or activation conflict
-> System Registry

Module-specific rule or value conflict
-> Focused module reference

Bounded implementation-scope conflict
-> Approved Codex task, within the limits of higher-level authority

Observed behavior conflict
-> Implementation evidence triggers documentation review; it does not silently become design truth
```

### 2.2 Authority rules

1. The README helps readers find authority; it is not the highest design authority.
2. `PROJECT_STATE.md` controls what the project is doing now, not the permanent internal rules of every module.
3. The master architecture controls universal relationships and prohibitions.
4. This registry controls module classification and readiness.
5. A focused reference controls the detailed design of its named module.
6. A Codex task may implement only approved, named contracts.
7. Tests demonstrate behavior and expose mismatches; they do not silently redefine accepted rules.

---

## 3. Module Classification Axes

Every registry entry uses four separate fields.

### 3.1 Primary kind

Each module has exactly one primary kind.

| Primary kind | Meaning | Examples |
|---|---|---|
| **Design Philosophy** | A lens used to judge the whole game; not a runtime rule owner. | SEN |
| **Choice Frame** | Defines the player's broad strategic intent. | Deal / Pressure / Ask |
| **Action Language** | Defines how an action is expressed, modified, or permitted. | BASED traits and Vibes |
| **Data Model** | Defines portable structures and authoritative data shapes. | Info Cards, Runtime State |
| **Rule Module** | Owns one bounded category of gameplay calculation. | HEAT, REP, TIME |
| **Resolver** | Coordinates the modules needed for one class of action. | InteractionResolver |
| **Scenario Module** | Owns bounded mission or run-specific truth. | Stolen Package, Run Card |
| **Presentation Module** | Collects input or displays outcomes without owning simulation truth. | Phaser runtime, blackboard |
| **Infrastructure Module** | Supports identity, transitions, saving, testing, portability, or reproducibility. | Stable IDs, seeded randomness |

A module may own data, use infrastructure, or sit on a boundary without receiving a second primary kind. Those relationships belong in its contract.

### 3.2 Architecture role

Architecture role describes importance to the overall design.

| Architecture role | Meaning |
|---|---|
| **Core** | Foundational to the project's identity or minimum architecture. |
| **Supporting** | Expands, strengthens, or specializes the game without defining the entire architecture. |

### 3.3 Design maturity

Design maturity describes readiness, not importance or activation.

| Design maturity | Meaning | Implementation use |
|---|---|---|
| **Design Draft** | Important details remain unresolved. | Do not implement detailed behavior unless a task explicitly defines a bounded temporary behavior. |
| **Implementation Ready** | The intended slice has explicit ownership, inputs, outputs, dependencies, failure behavior, determinism, order, and tests. | May be named by a bounded Codex task. |
| **Prototype Active** | Implemented, tested, verified, and accurately documented in the current build. | Safe to rely on within recorded limitations. |
| **Experimental** | Isolated trial that is not yet canonical. | Keep behind a clear boundary. |
| **Superseded** | Replaced but retained for project history. | Do not use as current guidance. |
| **Removed** | No longer part of the accepted design. | Do not reference in new work. |

### 3.4 Activation role

Activation role describes whether the current build, action, or phase uses the module.

| Activation role | Meaning |
|---|---|
| **Required** | The relevant feature cannot function correctly without the module. |
| **Optional Integration** | The module adds context or consequences when enabled, but its absence must be handled explicitly. |
| **Deferred Integration** | The module is recognized by the architecture but intentionally absent from the current phase. |

A module can therefore be:

```text
Core + Design Draft + Required
Supporting + Implementation Ready + Optional Integration
Supporting + Design Draft + Deferred Integration
```

These combinations are not contradictory because they answer different questions.

---

## 4. Universal Module Rules

Every module must preserve these project-wide rules:

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

- Each module has one primary kind and one bounded responsibility.
- Modules do not directly command unrelated modules.
- Resolvers coordinate intersections but do not absorb every internal rule.
- Authoritative gameplay state remains portable and contains no Phaser objects.
- Gameplay identity uses stable IDs rather than scene, sprite, or physics-object identity.
- Randomness affecting gameplay truth is controlled and reproducible.
- Presentation may request actions and display outcomes; it does not invent consequences.
- Optional modules have explicit absence behavior.
- Missing required modules fail clearly rather than producing partial hidden behavior.
- Numeric rules belong in focused references, not in this registry.

---

## 5. Current Registry

### 5.1 Design and interaction

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `design.sen` | SEN | Design Philosophy | Core | Design Draft | Required | Current master architecture; focused SEN reference planned |
| `interaction.dpa` | Deal / Pressure / Ask | Choice Frame | Core | Design Draft | Required | Current master architecture; focused DPA reference planned |
| `interaction.based` | BASED Traits and Vibes | Action Language | Core | Design Draft | Required | Focused BASED reference planned |

#### `design.sen`

**Owns:** The Structured / Emergent / Negotiated philosophy used to judge situations, pressure, and consequences.  
**Does not own:** Runtime mutation, action validation, HEAT, REP, TIME, Info, or presentation behavior.

#### `interaction.dpa`

**Owns:** The selected strategic frame: Deal, Pressure, or Ask.  
**Does not own:** The consequence calculations attached to the selected frame.

#### `interaction.based`

**Owns:** The manner, tone, Vibe, modifiers, permissions, and future abilities used to express an action.  
**Does not own:** Direct REP, HEAT, TIME, Info, inventory, mission, or Phaser mutations.

---

### 5.2 Information and social modules

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `data.information` | Soft / Hard Information Model | Data Model | Core | Design Draft | Required | Focused information model planned |
| `data.info_cards` | Info Cards | Data Model | Core | Design Draft | Required | Focused Info Card reference planned |
| `social.heat` | HEAT | Rule Module | Supporting | Design Draft | Optional Integration | Focused HEAT reference planned |
| `social.rep` | REP / Relationship | Rule Module | Supporting | Design Draft | Optional Integration | Focused REP reference planned |
| `social.fac` | FAC | Rule Module | Supporting | Design Draft | Deferred Integration | Focused FAC reference planned |
| `social.favor` | FAVOR | Rule Module | Supporting | Design Draft | Deferred Integration | Focused FAVOR reference planned |
| `social.access` | ACCESS | Rule Module | Supporting | Design Draft | Deferred Integration | Focused ACCESS reference planned |
| `social.lore` | LORE | Rule Module | Supporting | Design Draft | Deferred Integration | Focused LORE reference planned |

Required separation:

- Information truth is not the same as HEAT, REP, or faction strength.
- Social Asset values are runtime data; the named rule modules determine how those values may change.
- Information disclosure is owned by the Information design and rules, even when social modules influence eligibility, risk, or cost.

---

### 5.3 Resource and survival modules

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `resource.inventory` | Inventory and Item Transfer | Rule Module | Supporting | Design Draft | Deferred Integration | Hard Assets / inventory reference planned |
| `resource.money_contra` | Money and Contra Economy | Rule Module | Supporting | Design Draft | Deferred Integration | Economy reference planned |
| `resource.weapons` | Weapons and Legality | Rule Module | Supporting | Design Draft | Deferred Integration | Weapons reference planned |
| `resource.sustenance` | Sustenance | Rule Module | Supporting | Design Draft | Deferred Integration | Survival reference planned |
| `resource.time` | TIME Cost and Advancement | Rule Module | Core | Design Draft | Required | TIME reference planned |
| `resource.energy` | Energy and Survival Pressure | Rule Module | Supporting | Design Draft | Deferred Integration | Energy / survival reference planned |

Required separation:

- Time as a stored value belongs to runtime state.
- `resource.time` owns minute-cost and time-advancement calculations.
- Animation duration never determines in-world TIME cost.
- Inventory owns material-transfer rules; social modules may influence eligibility or consequence but do not perform hidden transfers.

---

### 5.4 World, scenario, and conflict modules

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `world.map` | Map and Traversal | Rule Module | Supporting | Design Draft | Deferred Integration | Map and traversal reference planned |
| `world.schedule` | NPC Schedules | Rule Module | Supporting | Design Draft | Deferred Integration | Schedule reference planned |
| `scenario.stolen_package` | Stolen Package Mission | Scenario Module | Core | Design Draft | Required | Focused demo-scope reference planned |
| `scenario.run_card` | Run-Card Generator | Scenario Module | Supporting | Design Draft | Deferred Integration | Run-card reference planned |
| `conflict.combat` | Combat Alert State | Rule Module | Supporting | Design Draft | Deferred Integration | Combat reference planned |

Required separation:

- The mission owns objective truth, role assignments, and win/failure conditions.
- The run-card scenario module establishes starting truth while using infrastructure such as stable IDs and seeded randomness.
- The world module owns traversal rules and route legality; ACCESS may modify permission but does not own map geometry.
- Combat is a crisis-state module, not the universal resolution path.

---

### 5.5 Resolver modules

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `resolver.interaction` | InteractionResolver | Resolver | Core | Design Draft | Required | Action-resolution reference planned |
| `resolver.street_action` | StreetActionResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future action-resolution reference |
| `resolver.travel` | TravelResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future traversal reference |
| `resolver.combat` | CombatResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future combat reference |
| `resolver.end_of_day` | EndOfDayResolver | Resolver | Supporting | Design Draft | Deferred Integration | Future run-structure reference |
| `resolver.run_setup` | RunSetupResolver | Resolver | Supporting | Design Draft | Deferred Integration | Run-card reference planned |

Resolvers may know which modules participate and in what order. They must not recreate the internal rules of participating modules.

---

### 5.6 Runtime data and infrastructure

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `runtime.content_definitions` | Content Definitions | Data Model | Core | Design Draft | Required | Technical architecture reference planned |
| `runtime.state` | Authoritative Runtime State | Data Model | Core | Design Draft | Required | Technical architecture reference planned |
| `runtime.outcome` | ResolvedOutcome | Data Model | Core | Design Draft | Required | Action-resolution reference planned |
| `runtime.state_transition` | Ordered State Transition | Infrastructure Module | Core | Design Draft | Required | Consequence-order reference planned |
| `infra.ids` | Stable IDs | Infrastructure Module | Core | Implementation Ready | Required | Portability reference planned |
| `infra.random` | Seeded Randomness | Infrastructure Module | Core | Design Draft | Deferred Integration | Portability reference planned |
| `infra.save` | Save-State Schema | Infrastructure Module | Supporting | Design Draft | Deferred Integration | Save-data reference planned |
| `infra.tests` | Engine-Light Simulation Tests | Infrastructure Module | Core | Design Draft | Required | Task-specific tests plus technical standards |

---

### 5.7 Presentation modules

| Module ID | Name | Primary kind | Architecture role | Design maturity | Activation role | Detailed authority |
|---|---|---|---|---|---|---|
| `presentation.phaser` | Phaser 3.90 Runtime | Presentation Module | Core | Design Draft | Required | Phaser portability boundary planned |
| `presentation.adapter` | Presentation Adapter | Presentation Module | Core | Design Draft | Required | Action-resolution reference planned |
| `presentation.blackboard` | Runtime Blackboard | Presentation Module | Supporting | Design Draft | Deferred Integration | Current Phaser task; implementation paused pending required contracts |
| `presentation.assets` | Asset and Animation Presentation Standards | Presentation Module | Supporting | Design Draft | Deferred Integration | Asset standards reference planned |

Presentation modules may display state, gather input, play animation, move cameras, update UI, and emit non-authoritative notifications after resolution. They do not own gameplay truth.

---

## 6. Provisional Implementation Gate

The Phaser runtime-blackboard implementation should not begin until every module required by its selected slice is sufficiently defined.

| Dependency | Minimum design maturity or decision before implementation |
|---|---|
| `interaction.dpa` | Implementation Ready |
| `interaction.based` | Implementation Ready for the selected test Vibes |
| `data.information` | Implementation Ready for the selected Soft / Hard behavior |
| `resource.time` | Implementation Ready for the selected action costs |
| `social.rep` | Implementation Ready or explicitly excluded from the slice |
| `social.heat` | Implementation Ready or explicitly excluded from the slice |
| `resolver.interaction` | Implementation Ready |
| `runtime.state` | Implementation Ready for the thin slice |
| `runtime.outcome` | Implementation Ready for the thin slice |
| `runtime.state_transition` | Implementation Ready for the thin slice |

No implementation task may silently use a Design Draft module by inventing missing mechanics.

---

## 7. Required and Optional Behavior

A resolver must classify participating modules for each accepted action type.

### 7.1 Missing required module

```text
Missing required module
-> validation fails
-> no authoritative transition occurs
-> ResolvedOutcome records the reason
```

### 7.2 Missing optional integration

```text
Optional integration disabled
-> resolver skips that contribution
-> outcome records that the module was not consulted
-> remaining required modules continue normally
```

### 7.3 Deferred integration

```text
Deferred integration
-> feature is unavailable or follows an explicitly documented reduced path
-> no hidden placeholder behavior is assumed
```

Example only:

```text
Ask action
- Information: required
- TIME: required
- BASED: required when a Vibe is selected
- REP: optional integration
- HEAT: optional integration
- Faction response: deferred integration
```

The exact participation list belongs in the relevant resolver contract or bounded task.

---

## 8. Change-Control Rules

When a module changes architecture role, design maturity, activation role, primary kind, ownership, or authority:

1. Update this registry.
2. Update the focused reference when one exists.
3. Review active tasks that depend on it.
4. Review resolver contracts that require or optionally integrate it.
5. Do not rewrite unrelated modules unless their contracts actually changed.
6. Record effects on runtime state, saves, deterministic tests, and outcome semantics.

When a module is removed or superseded:

- replace hard dependencies with explicit validation failures or approved alternatives;
- remove it from resolver participation lists;
- preserve historical references only when useful;
- do not leave hidden fields, listeners, or presentation assumptions that still require it.

---

## 9. Next Documentation Priorities

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

## 10. Registry Principle

```text
The master architecture explains how the whole project fits together.
The registry identifies each module, its one primary kind, its role, its maturity, and its activation.
Focused references define how individual modules work.
Resolvers combine only the modules needed for a specific action.
Codex tasks implement only approved, named contracts.
```