# Trapstar the Demo — Project State

Last updated: 2026-07-13  
Current phase: Phaser transition / course prototype planning  
Primary build target: Phaser 3.90 browser-playable course capstone  
Repo role: Source of truth for design, bounded implementation tasks, and pipeline documentation

---

## 0. Usage Note

This file is the current command brief for *Trapstar the Demo*.

Codex should use it for project context, then implement only from a specific approved task in `codex_tasks/`. The master architecture reference is:

```text
docs/Trapstar_Master_System_Architecture.md
```

Phaser implementation work should remain small, testable, and directly tied to the seven-week playable target.

---

## 1. Current Project Identity

*Trapstar the Demo* is a bounded, replayable city-block mystery implemented in **Phaser 3.90 with TypeScript** for the course prototype.

The player investigates the **Stolen Package** case over three in-game days while navigating:

- hard-tracked resources and time
- NPC motives, truths, lies, and information
- two factions
- police HEAT
- reputation and access pressure
- Deal / Pressure / Ask choices colored by BASED traits and Vibes

The game should prove that a small environment can feel socially alive when clear rules, changing pressure, negotiation, and consequences continuously affect one another.

Phaser 3.90 is the committed demo engine. It is not automatically the engine for the later full production project.

---

## 2. Core Pitch

A small block.  
Three days.  
Two factions.  
One stolen package.  
Several suspects.  
A police-monitored environment.  
A player trying to resolve the case before time, pressure, reputation, or resources collapse.

The game is not an open-city simulator. It is a tightly bounded social investigation with controlled replay variation.

---

## 3. Locked Course-Demo Direction

The following decisions are currently locked:

- The project is called **Trapstar the Demo**.
- The demo engine is **Phaser 3.90**.
- The implementation language is **TypeScript**.
- The playable deliverable is a **browser build**.
- Phaser is the demo engine, not a guaranteed full-project engine.
- GitHub is the canonical source of truth.
- The production spine is **ChatGPT/Nova → GitHub → Codex → Phaser → browser playtest → ChatGPT/Nova review**.
- The main scenario is **Stolen Package**.
- The player has **three in-game days**.
- The environment is one small city block / looping room-style map with connected streets, interiors, and alley exits.
- Two major factions and police pressure support the mystery.
- The central design philosophy is **Structured / Emergent / Negotiated**.
- **Deal / Pressure / Ask** is the player-facing strategic choice frame, not an ordered loop.
- **BASED** traits and Vibes color the selected approach.
- Mystery variation must remain bounded, solvable, testable, and finishable for the course.

---

## 4. Production Pipeline

The active workflow is:

1. Develop and refine ideas in ChatGPT/Nova.
2. Record accepted design truth in GitHub.
3. Convert one bounded outcome into a Codex task.
4. Use Codex to plan and implement TypeScript, tests, content data, and Phaser presentation.
5. Run the browser build.
6. Return screenshots, logs, bugs, and playtest notes for review.
7. Update the repo source of truth.

Codex must not treat this file as a direct request to implement everything it describes.

---

## 5. Simulation / Presentation Boundary

The demo must separate portable game truth from Phaser-specific presentation.

### Portable simulation responsibilities

- run seed and Run-Card generation
- player, NPC, faction, location, inventory, and world state
- truth, lie, guilt, belief, and knowledge state
- SEN, DPA, and BASED action resolution
- Info Cards, Social Assets, and Hard Assets
- TIME COST, Energy, HEAT, REP, and consequence rules
- win, loss, run-end, and save-state logic

Portable simulation code must not depend on Phaser scenes, sprites, cameras, animation objects, or physics bodies.

### Phaser presentation responsibilities

- scenes and scene transitions
- browser input
- sprites and layered character animation playback
- movement, collision, cameras, and Y-depth sorting
- dialogue panels, menus, HUD, and Info Card display
- audio, asset loading, and browser deployment

Governing rule:

```text
Phaser sends player intentions to the simulation and displays the result.
The simulation owns what the action means and how game state changes.
```

---

## 6. Portability Rules

- Use stable string IDs for NPCs, factions, locations, items, information, and actions.
- Store content in portable data where practical.
- Keep save state plain and versioned; never serialize Phaser objects as game truth.
- Use controlled seeded randomness for gameplay-affecting variation.
- Keep core action resolution testable without loading a Phaser scene.
- Standardize sprite frames, origins, ground anchors, layer alignment, tiles, panels, file names, and transparency outside the engine.
- Do not build a multi-engine abstraction layer during the course.
- Reuse design, data, rules, tests, and assets; allow presentation code to be replaced later.

Expected conceptual project split:

```text
PhaserProject/
  src/
    simulation/
    presentation/
    content/
  tests/
  public/
    assets/
```

This is a boundary guide, not permission to invent a large framework before a bounded task requires it.

---

## 7. SEN, DPA, and BASED

### SEN

- **Structured:** hard-tracked state and constraints
- **Emergent:** pressure and reactions produced by the current state
- **Negotiated:** the player chooses how to act inside that situation

### DPA

DPA is not an ordered loop.

```text
Deal     = Logos / Structured / hard reality
Pressure = Pathos / Emergent / dynamic force
Ask      = Ethos / Negotiated / social opening
```

At a meaningful situation, the player chooses one frame.

### BASED

BASED stands for Belligerence, Aggression, Sociability, Empathy, and Deception.

A BASED trait or two-trait Vibe colors how the chosen Deal, Pressure, or Ask action is expressed. DPA selects the strategic frame; BASED shapes the approach.

---

## 8. Minimum Playable Loop

1. Generate a bounded run from a reproducible seed.
2. Enter the block.
3. Assign hidden mystery, NPC, faction, information, and pressure states.
4. Move, talk, observe, trade, investigate, or wait.
5. Spend minutes and update hard state.
6. Let NPC, faction, rumor, REP, and police pressure react.
7. Choose Deal, Pressure, or Ask.
8. Apply a BASED trait or Vibe.
9. Resolve the action in the portable simulation.
10. Present the result through Phaser.
11. Update clues, assets, relationships, HEAT, time, and world state.
12. Resolve or fail the Stolen Package case within three in-game days.

The first playable build must prove this loop, not the full dream game.

---

## 9. Runtime Blackboard Target

The first technical proof should make the simulation legible.

The blackboard/debug view should expose:

### Structured state

- current day and minute
- current location
- player Money, Contra, inventory, Energy, and known information
- active mystery state
- relevant NPC and faction values

### Emergent pressure

- police HEAT
- faction pressure
- REP or relationship state
- rumor and information state
- NPC goal, suspicion, mood, or stance
- recent consequences

### Negotiated action state

- last DPA frame
- last BASED trait or Vibe
- action target
- information and assets used
- action cost
- outcome and reason
- resulting state changes

Debug-only information may expose hidden roles and truth state for development and course evaluation.

---

## 10. Map, Time, Economy, and Combat Direction

- The map is one compact city block with connected street space, interiors, passages, and alley exits.
- Traversal supports repeated investigation and interaction rather than large-scale exploration.
- Meaningful actions consume minutes.
- Time, Money, Contra, Sustenance, Energy, and inventory create tradeoffs.
- Police HEAT and faction pressure constrain where and how the player acts.
- Combat is an alert/crisis state, not the primary grind loop.
- Economy, survival, faction, and police systems must stay narrow until the mystery loop works.

---

## 11. Next Recommended Build Task

```text
TASK_002_RUNTIME_BLACKBOARD
```

The task should create the smallest visible proof of:

```text
Structured state
-> Emergent pressure
-> player selects DPA + BASED approach
-> portable resolution
-> changed state
-> Phaser/browser feedback
```

Suggested implementation targets must be scoped by the actual task file, but may include:

- portable simulation state types
- deterministic test state
- a minimal action resolver
- a Phaser debug scene or HTML debug panel
- test controls for state changes and DPA/BASED actions
- readable browser-console and on-screen reason logging

---

## 12. Current Risks

High risk:

- scope creep from open-world ambitions
- building too many systems before the mystery loop works
- allowing Phaser presentation objects to become game-state truth
- runtime behavior becoming invisible or hard to evaluate
- DPA becoming an ordered loop
- BASED becoming cosmetic
- uncontrolled procedural mystery generation

Medium risk:

- premature architecture
- unclear data contracts
- Phaser implementation complexity
- Codex producing code before design contracts are stable
- art polish distracting from playable logic
- faction or police systems becoming larger than the mystery

---

## 13. Current Design Principle

The demo should be:

- bounded, not sprawling
- replayable, not infinite
- readable, not opaque
- systemic, not overcomplicated
- agentic, not random
- portable beneath the presentation layer
- playable before polished
- course-ready before dream-complete

Every feature should answer:

1. What state is tracked?
2. What pressure does it create?
3. What Deal / Pressure / Ask choice does it support?
4. How does BASED color the action?
5. What changes afterward?
6. Does the rule live in portable simulation or Phaser presentation?

---

## 14. Recent Decisions

- Phaser 3.90 replaces Unity as the seven-week demo engine.
- TypeScript and a browser build are the current implementation target.
- Core simulation and content data must remain separate from Phaser presentation.
- Stable IDs, versioned state, seeded randomness, testable action resolution, and standardized assets protect future portability.
- The repo remains the source of truth.
- The first technical target remains a visible runtime blackboard/debug proof.
- Historical Unity setup material is not current implementation guidance.

---

## 15. Definition of Done for the Current Phase

This transition/planning phase is complete when:

- the repo identifies Phaser 3.90 as the demo engine
- the README and command brief no longer direct active work toward Unity
- the Codex task template uses TypeScript, browser, and Phaser examples
- the repo has a clear Phaser project location
- the `.gitignore` protects Node/Phaser generated output
- historical Unity material is explicitly marked as superseded
- future tasks preserve the simulation/presentation boundary
- the first bounded Phaser implementation task can be handed to Codex
