# Trapstar the Demo — Project State

Last updated: 2026-07-13  
Current phase: Phaser architecture alignment / pre-implementation foundation  
Primary build target: Phaser 3.90 browser-based course demo  
Repo role: Canonical source of truth for design, implementation tasks, and pipeline documentation  

---

## 0. Usage Note

This file is the current command brief for *Trapstar the Demo*.

Codex should use it for orientation, then work from a specific bounded task file in `codex_tasks/`. Codex should not implement the whole project directly from this file or from the master architecture alone.

Required high-level reference:

```text
docs/Trapstar_Master_System_Architecture.md
```

Active implementation task:

```text
codex_tasks/TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD.md
```

Phaser work should remain small, testable, browser-playable, and directly tied to the current vertical-slice target.

---

## 1. Current Project Identity

*Trapstar the Demo* is a bounded, replayable city-block mystery and socioeconomic negotiation game presented through a 2D belt-scroller-style street environment.

The player investigates the **Stolen Package** case over three in-game days while navigating:

- hard-tracked resources and facts;
- changing NPC, faction, and police pressure;
- Deal / Pressure / Ask strategic choices;
- BASED traits and Vibes;
- Soft and Hard information;
- Social Assets and Hard Assets;
- TIME and Energy pressure;
- bounded randomized roles and starting conditions.

The course-facing technical showcase is a legible runtime simulation: state, motives, choices, resolver logic, and consequences should be visible enough to debug and explain.

---

## 2. Core Pitch

```text
One block.
Three days.
Two factions.
One stolen Contra shipment.
Several suspects.
A police-monitored environment.
A player trying to solve the case before time, pressure,
reputation, resources, or survival state collapses.
```

The game is not an open-city simulator. It is a tightly bounded social investigation in which a small number of systems recombine to create replayable pressure.

---

## 3. Locked Core Direction

The following decisions are current architecture truth for the course prototype:

- The project is called **Trapstar the Demo**.
- **Phaser 3.90** is the committed engine for the seven-week demo.
- Phaser is not guaranteed to be the full production engine.
- The demo uses **TypeScript** and targets a browser build.
- GitHub is the canonical source of truth.
- The active production spine is **ChatGPT/Nova → GitHub → Codex → Phaser → browser playtest → ChatGPT/Nova review**.
- The main mission is **Stolen Package**; the in-world object is a missing Contra shipment/package.
- The player has **three in-game days**.
- The playable environment is one compact city block with three node-connected streets, interiors, passages, and hidden routes.
- The demo contains two primary factions and police-monitored pressure.
- Run variation is bounded and seedable.
- SEN means **Structured / Emergent / Negotiated**.
- Deal / Pressure / Ask is the player-facing strategic choice frame and is **not** an ordered loop.
- BASED defines the manner, tone, or Vibe of action.
- Core gameplay truth belongs to portable simulation data and rules rather than Phaser scenes or sprites.
- Small systems own bounded rules.
- Specialized resolvers coordinate cross-system actions.
- Critical consequences follow a documented order.
- Commands apply authoritative changes; events report completed outcomes.
- The project must remain bounded, testable, and finishable for the course.

---

## 4. Current Production Pipeline

```text
Chat / Nova
  -> Accepted GitHub Markdown
    -> Bounded Codex Task
      -> Phaser 3.90 + TypeScript Implementation
        -> Browser Build / Playtest
          -> Bugs, Logs, Screenshots, and Design Feedback
            -> Chat / Nova Review
              -> Updated GitHub Truth
```

Workflow rules:

1. Refine design before implementation.
2. Commit accepted design to GitHub.
3. Translate accepted design into one bounded Codex task.
4. Require Codex to report its plan before coding.
5. Keep simulation logic testable without loading a Phaser scene where practical.
6. Use Phaser for input, movement, rendering, scenes, animation, UI, audio, cameras, and browser delivery.
7. Bring implementation evidence back for review.
8. Record accepted changes in markdown so repo truth stays current.

---

## 5. Core Design Stack

### SEN

SEN is the world-state philosophy:

```text
Structured situation
-> Emergent pressure
-> Negotiated consequence
-> Updated situation
```

### DPA

Deal / Pressure / Ask is the strategic frame chosen at a meaningful decision point:

```text
Deal     = Logos / Structured / hard reality
Pressure = Pathos / Emergent / dynamic force
Ask      = Ethos / Negotiated / social opening
```

DPA is not a required sequence.

### BASED

BASED defines how the player expresses the selected frame:

```text
B = Belligerence
A = Aggression
S = Sociability
E = Empathy
D = Deception
```

Vibes are ordered two-trait pairings. DPA chooses the frame; BASED colors the approach.

---

## 6. Active Technical Architecture

The portable resolution path is:

```text
Content Definitions
-> Authoritative Runtime State
-> Player Action Request
-> Specialized Resolver
-> Independent Rule Systems
-> Ordered State Transition
-> Secondary Consequence Processing
-> Resolved Outcome
-> Phaser Presentation
```

### Content Definitions

Relatively stable data describing NPCs, factions, items, locations, Info Cards, actions, Vibes, dialogue, animation metadata, run-generation pools, and balancing values.

### Runtime State

Mutable truth for the current run: day, minute, player state, inventory, locations, NPC states, relationships, HEAT, known information, mission roles, and world flags.

### Specialized Resolvers

Small coordinators such as:

```text
InteractionResolver
StreetActionResolver
CombatResolver
TravelResolver
EndOfDayResolver
RunSetupResolver
```

A resolver selects the relevant systems and controls resolution order. It does not absorb every system's rules.

### Independent Rule Systems

Likely bounded owners include:

- Info System
- Relationship / REP System
- HEAT System
- TIME System
- Inventory System
- Mission System
- Schedule System
- Combat System

Systems should not directly command unrelated systems.

### Resolved Outcome

An explicit record of what happened, why, what changed, what TIME was spent, what secondary consequences occurred, and what presentation cues should be shown.

### Phaser Presentation

Phaser collects intent and presents outcomes. It does not independently invent authoritative consequences.

---

## 7. Governing Architecture Rules

```text
Trapstar should not eliminate complexity.
It should contain complexity inside small systems, explicit coordinators,
portable state transitions, and a controlled order of consequence.
```

```text
Commands change the world.
Events report what changed.
```

Required dependency direction:

```text
Action Request
-> Resolver
-> Bounded Systems
-> State Transition
-> Outcome
-> Presentation / Notifications
```

Prohibited direction:

```text
Phaser button event
-> unknown listener mutates REP
-> another listener reveals Info
-> another listener spends TIME
-> another listener raises HEAT
```

Events may update HUD, dialogue, audio, camera, animation, analytics, or logs after the authoritative result is known.

---

## 8. Current Playable Prototype Target

The first playable/debuggable version should prove one thin interaction slice:

1. Load a small set of content definitions.
2. Create one authoritative runtime state.
3. Present one player and one NPC in a minimal Phaser scene.
4. Let the player choose Deal, Pressure, or Ask.
5. Let the player select a BASED Vibe.
6. Submit one structured action request.
7. Route it through `InteractionResolver`.
8. Let small TIME, HEAT, REP, and Info rules calculate bounded contributions.
9. Apply one ordered state transition.
10. Produce one explicit resolved outcome.
11. Display dialogue/debug text, state changes, and presentation events.
12. Repeat the action and verify deterministic behavior under a fixed seed.

This slice should prove the architecture, not the full mystery.

---

## 9. Runtime Blackboard Target

The first visible debug layer should show:

### Authoritative state

- Current day and minute
- Player location
- Player Money / Contra / inventory
- Player Energy and condition
- Player HEAT
- Relevant personal REP
- Known Soft and Hard Info
- Active mission state

### Last action request

- Actor
- Target
- DPA frame
- BASED Vibe
- Offer, demand, or requested result
- Leverage
- Location
- Witnesses

### Resolution trace

- Resolver used
- Validation result
- Primary outcome
- Systems consulted
- Controlled random value or seed position when relevant
- Ordered state changes
- TIME spent
- Secondary consequences
- Win/loss or mission checks

### Presentation reports

- Dialogue cue
- HUD cue
- Animation cue
- Audio cue
- Camera cue
- Log events emitted after resolution

This debug layer should make cause and effect legible to Teddy, Codex, instructors, collaborators, and playtesters.

---

## 10. Stolen Package Scenario Direction

The mission must remain solvable and bounded.

Current run variables may include:

- guilty NPC;
- lying NPC;
- truth-telling NPC;
- NPC goals;
- NPC monitoring state;
- faction strength and pressure;
- Soft Info placement;
- Hard receipt placement;
- ACCESS routes;
- FAVOR debts;
- faction relationship state;
- police pressure conditions;
- missing shipment location or holder.

Gameplay truth that affects the run should be generated from a controlled seed rather than scattered uncontrolled randomness.

---

## 11. Map, Movement, and Presentation Direction

Current presentation target:

```text
Phaser 3.90
TypeScript
Browser build
2D beat-em-up-style X/Y street movement
Three standardized movement lanes where applicable
Node exits and interiors
Pointer and keyboard interaction
Menu-readable DPA / BASED actions
Layered character sprites
Y-depth sorting
```

Phaser may own collision, input, cameras, animation playback, audio, UI, and scene transitions. Portable runtime state must not serialize Phaser objects.

---

## 12. Time, Economy, and Survival Direction

- The player has three in-game days.
- Meaningful actions cost minutes.
- Real-time animation duration does not determine in-world TIME cost.
- Money, Contra, Weapons, Sustenance, Time, and Energy are Hard Assets.
- HEAT, REP, FAC, FAVOR, ACCESS, and LORE are Social Assets carried through information state.
- Hunger and tiredness pressure should remain light until the main interaction loop works.
- Combat remains an alert/crisis state rather than the primary reward loop.

---

## 13. Next Active Build Task

```text
TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD
```

Expected foundation concepts:

```text
GameSession
ContentDefinitions
RuntimeState
ActionRequest
ResolvedOutcome
InteractionResolver
small TIME / HEAT / REP / Info rules
PresentationAdapter
RuntimeBlackboardScene
```

The task must not create a universal `GameStateManager` or `TrapstarManager`.

---

## 14. Current Risk List

### High risk

- Scope creep from open-world ambitions.
- Too many systems before one complete interaction works.
- Simulation rules leaking into Phaser scenes or sprites.
- A universal manager absorbing unrelated rules.
- Resolvers becoming second god objects.
- Systems directly commanding one another.
- Critical consequences being hidden in listener chains.
- Animation timing controlling in-world TIME.
- Runtime state storing direct Phaser references.
- Inconsistent consequence order.
- DPA being implemented as an ordered loop.
- BASED becoming cosmetic rather than mechanically meaningful.
- Runtime AI becoming invisible or impossible to explain.

### Medium risk

- Dialogue content expanding before action resolution stabilizes.
- Faction and police systems becoming larger than the mystery.
- Visual polish delaying playable logic.
- Too many NPC goals or unclear goal definitions.
- Portable architecture becoming overengineered for the demo.

---

## 15. Current Design Principle

Trapstar the Demo should be:

- bounded, not sprawling;
- replayable, not infinite;
- readable, not opaque;
- systemic, not entangled;
- agentic, not random;
- portable beneath the engine;
- playable before polished;
- course-ready before dream-complete.

Every meaningful action should answer:

1. What is the player's intent?
2. Which DPA frame is chosen?
3. Which BASED Vibe colors it?
4. Which resolver coordinates the action?
5. Which bounded systems calculate consequences?
6. What becomes authoritatively true?
7. In what order are secondary consequences processed?
8. What does Phaser display afterward?

---

## 16. Recent Decisions

- Phaser 3.90 replaces Unity as the active seven-week demo engine.
- Phaser is the demo runtime, not the guaranteed full production engine.
- The canonical master architecture is `docs/Trapstar_Master_System_Architecture.md`.
- Simulation truth is separated from Phaser presentation.
- Content definitions and mutable runtime state are separate.
- Stable string IDs should replace direct engine-object identity.
- Run randomness should be reproducible.
- Small systems own bounded rules.
- Specialized resolvers coordinate system intersections.
- Consequence order must be visible and testable.
- Commands apply authoritative state changes.
- Events report completed outcomes.
- The next implementation target is the Phaser foundation and runtime blackboard task.

---

## 17. Definition of Done for Current Phase

This architecture-alignment phase is complete when:

- the master architecture is canonical and current;
- the README and project brief identify Phaser 3.90 as the demo engine;
- the Codex template enforces the simulation/presentation boundary;
- the repository contains a Phaser project root placeholder;
- the historical Unity setup task is marked as superseded guidance;
- a bounded Phaser foundation task is ready for Codex;
- no active document recommends a universal game manager;
- Codex can identify the action-request, resolver, bounded-system, state-transition, outcome, and presentation boundaries without guessing.
