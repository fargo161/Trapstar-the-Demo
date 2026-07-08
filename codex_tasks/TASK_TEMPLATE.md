# Codex Task Template

Use this template for every Codex implementation task in Trapstar the Demo.

Codex should treat each task file as a bounded work order. Do not expand scope beyond the task. Do not implement directly from `PROJECT_STATE.md` alone.

---

## Task Name

`TASK_###_SHORT_NAME`

Example:

`TASK_002_RUNTIME_BLACKBOARD`

---

## Task Status

Status: Draft / Ready for Codex / In Progress / Complete / Blocked

---

## Goal

Describe the single concrete outcome of this task.

The goal should be specific enough that Codex can complete it without guessing the larger game design.

Example:

Create a simple Unity runtime blackboard that displays current Structured state, Emergent pressure, and Negotiated BASED choice results.

---

## Project Context

Before starting, read:

- `PROJECT_STATE.md`

Relevant design principle:

Trapstar the Demo uses the Structured / Emergent / Negotiated loop.

- **Structured** = hard-tracked state such as time, money, items, BASED stats, player energy/health, clues, and concrete game values.
- **Emergent** = pressure such as rumors, reputation, faction goals, personal NPC goals, police heat, scarcity, and social consequences.
- **Negotiated** = player choice through the BASED system: Belligerence, Aggression, Sociability, Empathy, and Deception.

Every implementation should support this loop:

1. Structured state defines the situation.
2. Emergent pressure makes the situation unstable.
3. The player Negotiates through BASED choices.
4. The result changes Structured state.
5. New Emergent pressure appears.

---

## Files to Read First

List only the files Codex should read before working.

Required:

- `PROJECT_STATE.md`

Optional task-specific files:

- `docs/...`
- `agent_specs/...`
- `design_packets/...`
- previous `codex_tasks/...`

---

## Files to Create or Modify

List the expected files or folders.

Use exact paths when possible.

Example:

```text
UnityProject/Assets/Scripts/Core/GameStateManager.cs
UnityProject/Assets/Scripts/Debug/RuntimeBlackboard.cs
UnityProject/Assets/Scripts/Data/NPCState.cs
```

Do not modify unrelated files unless absolutely necessary.

---

## Non-Goals

List what Codex must not do in this task.

Example:

- Do not build the full dialogue system.
- Do not add live LLM/API calls.
- Do not implement final art.
- Do not create procedural mystery generation.
- Do not redesign the project architecture.
- Do not change unrelated documentation.
- Do not add third-party packages unless explicitly requested.

---

## Required Behavior

Describe what the task must actually do.

Use concrete, testable behavior.

Example:

- Display current day and time.
- Display police heat.
- Display faction pressure values.
- Display last BASED choice.
- Log state changes to the Unity console.
- Allow simple manual test buttons in the scene.

---

## Structured / Emergent / Negotiated Check

Explain how this task supports the core design loop.

### Structured

What hard-tracked state does this task create, expose, or modify?

### Emergent

What pressure, reaction, or changing situation does this task create, expose, or modify?

### Negotiated

What player choice, BASED interaction, or consequence does this task create, expose, or modify?

---

## Debug / Logging Requirements

Every runtime system should expose its behavior clearly.

Include relevant requirements such as:

- Console logs for state changes.
- On-screen debug values.
- Reason strings explaining why a value changed.
- Test buttons or inspector-accessible test values.
- Debug-only hidden information when useful.

Example:

```text
Police Heat changed from 20 to 35. Reason: Aggressive BASED choice in public location.
```

---

## Unity Test Steps

Describe exactly how Teddy should test the result in Unity.

Example:

1. Open Unity.
2. Open the test scene.
3. Press Play.
4. Confirm the debug panel appears.
5. Click the “Increase Police Heat” test button.
6. Confirm the value updates on screen.
7. Confirm a console log explains the change.

---

## Acceptance Criteria

This task is complete only when:

- The requested files exist.
- The project opens without compile errors.
- The required behavior works in Unity.
- Debug/logging requirements are visible.
- The feature can be tested using the Unity Test Steps.
- No unrelated systems were expanded.
- The Structured / Emergent / Negotiated purpose is clear.

---

## Report Before Coding

Before making changes, Codex must report:

1. What it understands the task to be.
2. Which files it plans to read.
3. Which files it plans to create or modify.
4. Any risks, ambiguities, or missing information.
5. The smallest safe implementation plan.

Codex should not begin implementation until this plan is reviewed and approved.

---

## Implementation Notes

After approval, Codex should:

- Make the smallest useful change.
- Prefer simple, readable code over clever architecture.
- Keep prototype systems modular.
- Avoid premature optimization.
- Avoid adding external dependencies.
- Include comments where they help future iteration.
- Preserve the project’s current direction from `PROJECT_STATE.md`.

---

## Completion Report

After implementation, Codex should report:

1. Files created or modified.
2. What behavior was implemented.
3. How to test it in Unity.
4. Any known limitations.
5. Any recommended next task.
6. Whether the task changed Structured, Emergent, or Negotiated systems.

---
