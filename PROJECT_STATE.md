# Trapstar the Demo — Project State

Last updated: 2026-07-13  
Current phase: Modular architecture and focused-system definition  
Primary build target: Phaser 3.90 browser-based course demo  
Repo role: Canonical source of truth for design, implementation tasks, and pipeline documentation

---

## 0. Current Command Brief

The project is not yet in gameplay implementation.

The immediate goal is to finish the modular architecture, then define only the focused contracts needed for the first Phaser interaction slice.

```text
Active implementation task: None

Paused future implementation task:
codex_tasks/TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD.md
```

Task 002 must not be handed to Codex until its complete implementation gate is satisfied and Teddy explicitly reactivates it.

---

## 1. Current Project Identity

*Trapstar the Demo* is a bounded, replayable city-block mystery and socioeconomic negotiation game presented through a 2D belt-scroller-style street environment.

The player investigates the **Stolen Package** case over three in-game days while navigating limited time, information, social pressure, factions, police attention, and resource risk.

The course-facing technical showcase is a legible runtime simulation whose state, choices, resolver logic, and consequences can be explained and tested.

---

## 2. Locked Core Direction

The following remain accepted high-level design truth:

- Phaser 3.90 + TypeScript is the committed seven-week demo target.
- Phaser is not guaranteed to be the full production engine.
- GitHub is the canonical source of truth.
- The main scenario is **Stolen Package**.
- The player has three in-game days.
- The demo uses one compact city block, two primary factions, and police-monitored pressure.
- Run variation is bounded and reproducible where gameplay truth is randomized.
- SEN is the Structured / Emergent / Negotiated design philosophy.
- Deal / Pressure / Ask is the player-facing strategic frame and is not an ordered loop.
- BASED defines the manner, tone, or Vibe of action.
- Portable simulation owns gameplay truth.
- Small modules own bounded responsibilities.
- Specialized resolvers coordinate module intersections.
- Consequence order must be visible and testable.
- Commands change the world; events report completed changes.

---

## 3. Document Authority

Read by authority domain:

```text
README.md
= introduction and navigation

PROJECT_STATE.md
= current phase, priorities, blockers, and approved next work

docs/Trapstar_Master_System_Architecture.md
= universal design and technical boundaries

docs/architecture/Trapstar_System_Registry.md
= module identity, Primary Kind, Architecture Role,
  Design Maturity, Demo Default Activation, and authority

docs/architecture/Trapstar_Module_Contract_Standard.md
= focused contract profiles, ownership, and boundary requirements

Focused module references
= detailed rules for named modules

Resolver Contracts
= action-specific participation and consequence order

Codex tasks
= bounded approved implementation work
```

---

## 4. Three Separate Status Questions

These concepts must not be combined:

### Demo Default Activation

Stored in the System Registry:

```text
Required
Optional Integration
Deferred Integration
```

This describes expected participation in the intended course demo.

### Current production status

Stored in this file:

```text
Active
Paused
Blocked
Not yet scheduled
```

This describes what work is happening now.

### Action-specific participation

Stored in Resolver Contracts:

```text
Required
Optional Integration
Not Consulted
```

This describes which modules participate in one action type.

---

## 5. Current Documentation Priorities

Complete these before implementation resumes:

1. Finalize the System Registry and Module Contract Standard.
2. Extract and refine the BASED focused reference.
3. Extract the DPA focused reference.
4. Define the Information state model and Info Card schema.
5. Define the `information.rules` contract for disclosure, withholding, hardening, and reveal eligibility.
6. Define the minimum TIME contract.
7. Define the routing-neutral `runtime.action_request` contract.
8. Decide whether REP and HEAT participate in the first thin slice or are explicitly excluded.
9. Define the InteractionResolver contract.
10. Define the thin-slice ContentDefinitions, RuntimeState, StateChange, StateTransition, and ResolvedOutcome contracts.
11. Define the minimum presentation contracts for Phaser, the Presentation Adapter, and the Runtime Blackboard.
12. Revise Task 002 against the accepted focused contracts.

---

## 6. Complete Task 002 Implementation Gate

Every required contract below must be **Implementation Ready for the selected thin slice** before Task 002 can return to `Ready for Codex`.

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

`infra.random` must be Implementation Ready and included when the selected slice uses randomized gameplay truth. Otherwise, the revised task must explicitly declare a deterministic non-random path.

`social.rep` and `social.heat` must each be either:

```text
Implementation Ready and included
```

or:

```text
explicitly excluded from the revised slice
```

A contract is a design prerequisite. Its implementation may still be produced by Task 002 after that contract is ready.

No implementation task may silently invent mechanics from a Design Draft or treat Design Accepted as Implementation Ready.

---

## 7. Shared Ownership Required by the First Slice

The first slice must preserve these ownership boundaries:

| Shared structure or responsibility | Owning module |
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

A shared interface does not need to become its own module, but it must have one recorded owner.

---

## 8. Active Technical Architecture

```text
Content Definitions
-> Authoritative Runtime State
-> routing-neutral ActionRequest
-> specialized Resolver selection
-> bounded Rule Modules
-> ordered State Transition
-> secondary consequence checks
-> ResolvedOutcome
-> Phaser Presentation
```

Governing rules:

```text
Commands change the world.
Events report what changed.
```

```text
Phaser gathers intent and displays resolved outcomes.
It does not own the rules that determine those outcomes.
```

The Presentation Adapter may translate player intent into an `ActionRequest`, but `runtime.action_request` owns the generic request structure. Specialized resolvers own validation and coordination for the action types they accept.

---

## 9. Paused Phaser Foundation Target

The future first implementation slice is still intended to prove:

1. one player, one NPC, and one location;
2. one approved DPA selection;
3. one approved BASED Vibe selection;
4. one routing-neutral `ActionRequest`;
5. one InteractionResolver;
6. only approved participating modules;
7. one authoritative state transition;
8. one explicit ResolvedOutcome;
9. deterministic replay under the same state and seed when randomness participates;
10. a simple Phaser blackboard showing cause and effect.

This remains a preserved target, not active work.

---

## 10. Current Risks

High risks:

- implementing BASED before its mechanics are specific;
- allowing tasks to invent missing system rules;
- mixing information state ownership with information-behavior ownership;
- letting a specialized resolver own the generic request envelope;
- creating duplicate shared-interface ownership;
- creating a universal manager;
- letting resolvers become god objects;
- leaking simulation truth into Phaser scenes;
- using hidden event chains for critical consequences;
- allowing animation timing to control in-world TIME;
- expanding the number of modules before one complete interaction works.

---

## 11. Definition of Done for the Current Phase

The modular-definition phase is complete when:

- the registry and contract standard are accepted;
- `PROJECT_STATE.md` remains a complete current command brief;
- BASED, DPA, Information, Info Cards, `information.rules`, and minimum TIME references exist;
- `runtime.action_request` has an approved routing-neutral contract;
- the first resolver, runtime, infrastructure, and presentation contracts are Implementation Ready;
- shared structures have one recorded owner;
- REP, HEAT, and randomness participation are explicitly decided;
- Task 002 lists only the required focused references;
- Task 002 acceptance criteria match the approved module set;
- Task 002 can be marked Ready for Codex without contradiction or invention;
- Teddy explicitly authorizes reactivation.
