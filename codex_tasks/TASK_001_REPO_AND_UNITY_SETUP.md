# TASK_001_REPO_AND_UNITY_SETUP

## Task Status

Status: Complete

Completed: 2026-07-11

---

## Completion Note

This task has been completed. The repository has been prepared to support Trapstar the Demo documentation, Codex task files, and a nested Unity project location.

This file is now a completed task record. Future implementation work should not continue from this setup task. The next active implementation task should be created as a new bounded task file in `codex_tasks/`.

Recommended next task:

```text
TASK_002_RUNTIME_BLACKBOARD
```

---

## Goal

Prepare the GitHub repository so Trapstar the Demo can safely support both project documentation and a nested Unity project.

This task established the repo folder structure, made sure Unity-generated files will not pollute GitHub, and prepared the project for future Codex and Unity implementation tasks.

This task did **not** create gameplay systems.

This task did **not** create a Unity project from scratch.

---

## Project Context

Trapstar the Demo uses the Structured / Emergent / Negotiated loop:

- **Structured** = hard-tracked state such as time, money, items, BASED stats, player energy/health, clues, and concrete game values.
- **Emergent** = pressure such as rumors, reputation, faction goals, personal NPC goals, police heat, scarcity, and social consequences.
- **Negotiated** = player choice through the Deal / Pressure / Ask frame, colored by BASED traits and Vibes.

DPA is not an ordered loop. The player does not cycle through Deal, then Pressure, then Ask. DPA is the recurring strategic choice frame at meaningful decision points.

The active production spine is:

```text
ChatGPT/Nova → GitHub → Codex → Unity → ChatGPT/Nova review
```

GitHub is the source of truth. Codex should work from bounded task files. Unity should live in a clean, safe project structure.

---

## Files Read During Setup

Required context files:

```text
PROJECT_STATE.md
codex_tasks/TASK_TEMPLATE.md
.gitignore
README.md
```

---

## Files Created or Modified

This task prepared the following structure:

```text
.gitignore
docs/.gitkeep
agent_specs/.gitkeep
design_packets/.gitkeep
playtest_logs/.gitkeep
course_deliverables/.gitkeep
UnityProject/.gitkeep
```

The `.gitkeep` files allow GitHub to track empty project organization folders.

---

## Completed Repo Setup

The repo now supports the following organization:

```text
docs/
agent_specs/
codex_tasks/
design_packets/
playtest_logs/
course_deliverables/
UnityProject/
```

Unity is expected to live inside:

```text
UnityProject/
```

Unity-generated folders should not be committed.

---

## `.gitignore` Protection

The repo `.gitignore` protects both root-level Unity generated folders and nested `UnityProject/` generated folders.

Nested Unity generated folders ignored by this setup include:

```text
UnityProject/Library/
UnityProject/Temp/
UnityProject/Obj/
UnityProject/Build/
UnityProject/Builds/
UnityProject/Logs/
UnityProject/UserSettings/
UnityProject/MemoryCaptures/
UnityProject/Recordings/
```

---

## Non-Goals Confirmed

This task did **not**:

- build gameplay
- create the runtime blackboard
- create a Unity project from scratch
- manually create Unity `Assets/`, `Packages/`, or `ProjectSettings/`
- implement NPCs, factions, police heat, mystery logic, dialogue, map traversal, economy, or BASED/DPA choice systems
- add live LLM/API calls
- install Unity packages
- add third-party dependencies
- add large binary assets
- commit Unity-generated folders

---

## Structured / Emergent / Negotiated Check

### Structured

This task created the hard project structure that future work depends on:

- repo folders
- Unity project location
- ignored file rules
- Codex task organization
- documentation locations

### Emergent

This task reduces future production pressure by preventing:

- Unity-generated junk from entering GitHub
- unclear file locations
- Codex editing the wrong files
- confusion between design docs, task files, and Unity implementation
- repo sprawl

### Negotiated

This task does not create player-facing DPA or BASED choices.

Its Negotiated value is production-facing: it preserves the agreed workflow where ChatGPT/Nova, GitHub, Codex, and Unity each have a clear role.

---

## Acceptance Criteria Status

Complete:

- The repo contains the planned organizational folders.
- Empty folders are tracked using `.gitkeep` files.
- `.gitignore` protects both root-level Unity folders and nested `UnityProject/` folders.
- No Unity-generated folders are committed.
- No Unity project was manually created by this task.
- No gameplay systems were added.
- The repo is ready for a future Unity project to live inside `UnityProject/`.
- The next task can safely focus on the runtime blackboard prototype.

---

## Verification Steps

To verify this setup:

1. Open the GitHub repo.
2. Confirm the project folders exist.
3. Confirm `.gitignore` includes nested `UnityProject/` generated-folder rules.
4. Later, create or move the Unity project into `UnityProject/`.
5. After Unity creates local folders such as `UnityProject/Library/` and `UnityProject/Temp/`, confirm GitHub does not show those folders as files to commit.

---

## Next Recommended Task

```text
TASK_002_RUNTIME_BLACKBOARD
```

The next task should create a small visible runtime blackboard/debug layer that proves the core loop:

```text
Structured state changes → Emergent pressure updates → player chooses DPA frame + BASED approach → consequence updates state again.
```
