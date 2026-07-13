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

Task 002 must not be handed to Codex until its required module contracts satisfy the implementation gate in:

```text
docs/architecture/Trapstar_System_Registry.md
```

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

## 3. Current Architecture Documents

Read by authority domain:

```text
README.md
= introduction and navigation

PROJECT_STATE.md
= current phase, priorities, blockers, and approved next work

docs/Trapstar_Master_System_Architecture.md
= universal design and technical boundaries

docs/architecture/Trapstar_System_Registry.md
= module identity, primary kind, role, maturity, activation, and authority

docs/architecture/Trapstar_Module_Contract_Standard.md
= focused contract profiles and boundary requirements
```

---

## 4. Current Documentation Priorities

Complete these before implementation resumes:

1. Finalize the System Registry and Module Contract Standard.
2. Extract and refine the BASED focused reference.
3. Extract the DPA focused reference.
4. Define the Information model and Info Card authority.
5. Define the minimum TIME contract.
6. Decide whether REP and HEAT participate in the first thin slice or are explicitly excluded.
7. Define the InteractionResolver contract.
8. Define the thin-slice RuntimeState, StateChange, StateTransition, and ResolvedOutcome contracts.
9. Revise Task 002 against the accepted focused contracts.

---

## 5. Current Implementation Gate

Task 002 remains blocked until the selected slice has sufficient contracts for:

```text
interaction.dpa
interaction.based
data.information
resource.time
resolver.interaction
runtime.state
runtime.outcome
runtime.state_transition
```

For the first slice, `social.rep` and `social.heat` must each be either:

```text
Implementation Ready and included
```

or:

```text
explicitly excluded from the revised task
```

No implementation task may silently invent missing mechanics from a Design Draft.

---

## 6. Active Technical Architecture

```text
Content Definitions
-> Authoritative Runtime State
-> Action Request
-> Specialized Resolver
-> Bounded Rule Modules
-> Ordered State Transition
-> Secondary Consequence Checks
-> Resolved Outcome
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

---

## 7. Paused Phaser Foundation Target

The future first implementation slice is still intended to prove:

1. one player, one NPC, and one location;
2. one DPA selection;
3. one BASED Vibe selection;
4. one structured ActionRequest;
5. one InteractionResolver;
6. only the approved participating modules;
7. one authoritative state transition;
8. one explicit ResolvedOutcome;
9. deterministic replay under the same state and seed;
10. a simple Phaser blackboard showing cause and effect.

This remains a preserved target, not active work.

---

## 8. Current Risks

High risks:

- implementing BASED before its mechanics are specific;
- allowing tasks to invent missing system rules;
- creating a universal manager;
- letting resolvers become god objects;
- leaking simulation truth into Phaser scenes;
- using hidden event chains for critical consequences;
- allowing animation timing to control in-world TIME;
- expanding the number of modules before one complete interaction works.

---

## 9. Definition of Done for Current Phase

The modular-definition phase is complete when:

- the registry and contract standard are accepted;
- BASED, DPA, Information, and minimum TIME references exist;
- the first resolver and runtime contracts are Implementation Ready;
- REP and HEAT participation is explicitly decided;
- Task 002 is revised to read only the required focused references;
- Task 002 can be marked Ready for Codex without contradiction or invention.