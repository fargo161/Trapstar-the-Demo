# TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD

## Task Status

Status: Ready for Codex

---

## Goal

Create the smallest Phaser 3.90 + TypeScript browser foundation that proves Trapstar's contained-complexity architecture through one complete interaction:

```text
DPA + BASED Action Request
-> InteractionResolver
-> small independent TIME / HEAT / REP / Info rules
-> ordered authoritative state transition
-> explicit ResolvedOutcome
-> Phaser runtime-blackboard presentation
```

The task is complete when a player can choose Deal, Pressure, or Ask, select one BASED Vibe, submit the action, and see an explicit, deterministic resolution trace and updated state in the browser.

---

## Project Context

Read first:

```text
PROJECT_STATE.md
docs/Trapstar_Master_System_Architecture.md
codex_tasks/TASK_TEMPLATE.md
codex_tasks/TASK_002_PHASER_FOUNDATION_AND_RUNTIME_BLACKBOARD.md
```

Core rules:

```text
DPA chooses the strategic frame.
BASED defines the manner of action.
A specialized resolver coordinates the relevant systems.
Each system owns one bounded category of rule.
One ordered state transition applies the result.
A ResolvedOutcome reports what happened.
Phaser presents the result.
```

```text
Commands change the world.
Events report what changed.
```

---

## Report Before Coding

Before implementation, Codex must report:

1. Its understanding of the task.
2. Exact files it will read.
3. Exact files it plans to create or modify.
4. The portable simulation versus Phaser presentation boundary.
5. The proposed TypeScript types for content definitions, runtime state, action requests, state changes, and resolved outcomes.
6. The responsibility of `InteractionResolver`.
7. The responsibility of each small participating system.
8. The exact consequence order.
9. The tests it will create.
10. Risks or missing information.
11. The smallest safe implementation plan.

Do not begin implementation until Teddy approves the report.

---

## Expected Project Root

```text
PhaserProject/
```

Codex may initialize the minimum files required for a Phaser 3.90 + TypeScript browser project after approval.

Preferred high-level structure:

```text
PhaserProject/
  package.json
  tsconfig.json
  vite.config.ts
  index.html
  src/
    main.ts
    data/
      demoContent.ts
    simulation/
      runtimeState.ts
      stateTransition.ts
      seededRandom.ts
      systems/
        timeSystem.ts
        heatSystem.ts
        relationshipSystem.ts
        infoSystem.ts
    resolution/
      actionRequest.ts
      resolvedOutcome.ts
      interactionResolver.ts
    presentation/
      presentationAdapter.ts
    scenes/
      RuntimeBlackboardScene.ts
  test/
    interactionResolver.test.ts
```

The exact filenames may be adjusted in the report if Codex gives a clear reason, but the responsibility boundaries must remain intact.

---

## Required Demo Content

Use a minimal fixed content set:

- one player ID;
- one NPC ID;
- one location ID;
- one Soft Info card;
- one Hard Info card or hardening path;
- one personal REP value;
- one player HEAT value;
- one run seed;
- one simple target request, such as asking the NPC to disclose information.

Use stable string IDs. Do not use Phaser objects as identity.

---

## Required DPA and BASED Input

The browser scene must allow the tester to choose:

```text
Deal
Pressure
Ask
```

and at least three test Vibes, including:

```text
AB_Menacing
SA_Charismatic
SE_Compassionate
```

The submitted `ActionRequest` should contain, where relevant:

```text
actorId
targetId
actionType
frame
vibe
requestedResult
offerOrDemand
leverage
locationId
witnessIds
```

No UI choice should directly mutate HEAT, REP, TIME, or Info state.

---

## Required Portable Types

Codex should define small explicit types or interfaces for:

- `ContentDefinitions`
- `RuntimeState`
- `ActionRequest`
- `ValidationResult`
- `StateChange`
- `ResolvedOutcome`
- `PresentationCue`

`RuntimeState` and `ResolvedOutcome` must contain plain data only.

---

## Required Independent Systems

Implement only the smallest useful versions of:

### TIME System

Owns the selected action's minute cost and time advancement contribution.

### HEAT System

Owns legal/public-attention contribution based on frame, location, leverage, and witnesses.

### Relationship System

Owns the personal REP contribution between the NPC and player.

### Info System

Owns whether the NPC discloses, withholds, or hardens information.

Each system should return a calculation or proposed state change. It should not directly command another system or Phaser object.

---

## InteractionResolver Responsibility

`InteractionResolver` should:

1. receive the current state, content, action request, and controlled random source;
2. validate the action;
3. gather the required context;
4. call the small participating systems in a visible order;
5. combine their proposed changes;
6. apply one authoritative state transition;
7. process ordered secondary checks required by this task;
8. return the updated state and one explicit `ResolvedOutcome`.

It should not contain every internal HEAT, REP, TIME, or Info rule itself.

---

## Required Consequence Order

For this task use:

```text
1. Validate action.
2. Resolve primary social / information result.
3. Calculate REP contribution.
4. Calculate HEAT contribution.
5. Calculate TIME cost.
6. Apply one state transition.
7. Check simple threshold or mission/debug consequences.
8. Build ResolvedOutcome.
9. Send presentation cues to Phaser.
10. Restore input.
```

Animation timing must not determine in-world TIME cost.

---

## Required ResolvedOutcome Fields

Include at least:

```text
actionId
resolver
valid
result
primaryReason
frame
vibe
stateChanges
timeSpent
infoChanges
repChanges
heatChanges
secondaryConsequences
presentationCues
debugTrace
```

The exact shape may be refined in the report, but the outcome must make cause and effect explicit.

---

## Runtime Blackboard Requirements

Display:

### Current state

- run seed;
- current day and minute;
- player HEAT;
- personal REP;
- known Soft and Hard Info;
- player and NPC IDs;
- current location.

### Selected request

- DPA frame;
- BASED Vibe;
- request target;
- leverage or offer.

### Last resolution

- resolver;
- validation;
- primary result;
- old and new values;
- ordered state changes;
- TIME spent;
- secondary consequences;
- presentation events.

### Controls

- frame selection;
- Vibe selection;
- submit action;
- reset fixed state;
- replay with same seed.

---

## Events and Presentation

After an authoritative outcome exists, the presentation adapter may emit or invoke cues such as:

```text
hud_time_changed
hud_heat_changed
hud_rep_changed
info_disclosed
npc_recoils
npc_opens_up
dialogue_result
```

These cues may update UI, text, animation placeholders, or logs. They must not become the hidden owner of critical state changes.

---

## Automated Test Requirements

At minimum test:

1. The same state, request, and seed produce the same outcome.
2. A valid action returns the expected resolver name.
3. DPA and BASED remain separate fields.
4. Systems return bounded contributions.
5. State changes occur in the documented order.
6. TIME advances by the rule result, not animation duration.
7. Phaser objects are absent from runtime state and resolved outcomes.
8. Presentation cues appear only after resolution.
9. Reset restores the original test state.

Use the lightest testing setup compatible with the chosen project foundation.

---

## Browser Test Steps

After implementation:

1. Install dependencies.
2. Start the development server.
3. Open the local browser build.
4. Confirm the runtime blackboard loads.
5. Select `Pressure` and `AB_Menacing`.
6. Submit the action.
7. Confirm Info, REP, HEAT, and TIME changes match the visible outcome trace.
8. Reset.
9. Repeat with the same seed and confirm the same result.
10. Test `Ask` with `SE_Compassionate` and confirm a different bounded result.
11. Confirm the browser console has no errors.

---

## Non-Goals

Do not:

- build final movement or map traversal;
- build the full Stolen Package generator;
- create full NPC AI;
- create the full dialogue system;
- implement all 20 Vibes;
- implement full FAC, FAVOR, ACCESS, or LORE rules;
- implement combat;
- implement final save/load;
- add production art or final animation;
- add live LLM/API calls;
- create a universal manager;
- hide simulation logic in Phaser scenes or event listeners;
- add unrelated dependencies or systems.

---

## Acceptance Criteria

This task is complete when:

- the Phaser 3.90 + TypeScript project runs in a browser;
- the runtime blackboard is visible;
- one complete DPA + BASED action resolves through `InteractionResolver`;
- TIME, HEAT, REP, and Info rules are separate and bounded;
- one ordered state transition updates authoritative state;
- one explicit `ResolvedOutcome` explains the result;
- presentation cues occur after resolution;
- deterministic tests pass;
- no Phaser objects exist in portable runtime state;
- no universal manager owns the full game;
- Codex supplies exact browser test instructions and a completion report.

---

## Completion Report

Codex must report:

1. Files created or modified.
2. Dependencies added and why.
3. Portable simulation structure.
4. Phaser presentation structure.
5. Resolver and system responsibilities.
6. Consequence order.
7. Automated test results.
8. Browser test steps.
9. Screens or controls implemented.
10. Known limitations.
11. Recommended next bounded task.
