# TASK_001_REPO_AND_UNITY_SETUP

## Task Status

Status: Draft

---

## Goal

Prepare the GitHub repository so Trapstar the Demo can safely support both project documentation and a nested Unity project.

This task should establish the repo folder structure, make sure Unity-generated files will not pollute GitHub, and prepare the project for future Codex and Unity implementation tasks.

This task does **not** create gameplay systems.

This task does **not** create a Unity project from scratch unless Teddy explicitly approves that in a later instruction.

---

## Project Context

Before starting, read:

- `PROJECT_STATE.md`
- `codex_tasks/TASK_TEMPLATE.md`

Trapstar the Demo uses the Structured / Emergent / Negotiated loop:

- **Structured** = hard-tracked state such as time, money, items, BASED stats, player energy/health, clues, and concrete game values.
- **Emergent** = pressure such as rumors, reputation, faction goals, personal NPC goals, police heat, scarcity, and social consequences.
- **Negotiated** = player choice through the BASED system: Belligerence, Aggression, Sociability, Empathy, and Deception.

This setup task supports the production pipeline, not gameplay directly.

The active production spine is:

```text
ChatGPT/Nova → GitHub → Codex → Unity → ChatGPT/Nova review
```

GitHub is the source of truth. Codex should work from bounded task files. Unity should live in a clean, safe project structure.

---

## Files to Read First

Required:

- `PROJECT_STATE.md`
- `codex_tasks/TASK_TEMPLATE.md`
- `.gitignore`
- `README.md`

---

## Files to Create or Modify

Expected files or folders:

```text
.gitignore
docs/.gitkeep
agent_specs/.gitkeep
design_packets/.gitkeep
playtest_logs/.gitkeep
course_deliverables/.gitkeep
UnityProject/.gitkeep
```

Use `.gitkeep` files for this setup task.

Do **not** create folder README files in this task unless Teddy specifically requests them later.

Do **not** create actual Unity project folders manually yet, including:

```text
UnityProject/Assets/
UnityProject/Packages/
UnityProject/ProjectSettings/
```

Those folders should be created by Unity itself when Teddy creates or moves the Unity project.

Do **not** create or commit Unity-generated folders such as:

```text
UnityProject/Library/
UnityProject/Temp/
UnityProject/Obj/
UnityProject/Logs/
UnityProject/UserSettings/
```

Those folders should be ignored, not committed.

Allowed file modification:

```text
.gitignore
```

Avoid modifying these files unless absolutely necessary:

```text
PROJECT_STATE.md
README.md
codex_tasks/TASK_TEMPLATE.md
```

---

## Non-Goals

Do **not** build gameplay.

Do **not** create the runtime blackboard yet.

Do **not** create a Unity project from scratch.

Do **not** create Unity `Assets/`, `Packages/`, or `ProjectSettings/` folders manually.

Do **not** implement NPCs, factions, police heat, mystery logic, dialogue, map traversal, economy, or BASED choice systems.

Do **not** add live LLM/API calls.

Do **not** install Unity packages.

Do **not** add third-party dependencies.

Do **not** add large binary assets.

Do **not** create Unity-generated folders manually.

Do **not** redesign the project architecture beyond the setup described here.

Do **not** change unrelated documentation.

---

## Required Behavior

This task should make the repo safe and ready for Unity work.

Required setup:

1. Confirm the repo is using `main` as the default branch.

2. Confirm these files already exist:

```text
README.md
.gitignore
PROJECT_STATE.md
codex_tasks/TASK_TEMPLATE.md
```

3. Confirm the project recommendation that Unity should live inside:

```text
UnityProject/
```

4. Update `.gitignore` so it safely ignores Unity-generated folders both at the repo root and inside `UnityProject/`.

The `.gitignore` should ignore nested Unity-generated folders such as:

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

5. Create placeholder folders for project organization:

```text
docs/
agent_specs/
design_packets/
playtest_logs/
course_deliverables/
UnityProject/
```

6. Use `.gitkeep` files so GitHub tracks the empty folders.

7. Do not create or commit heavy Unity-generated content.

8. Do not create gameplay scripts or Unity scenes.

---

## Structured / Emergent / Negotiated Check

### Structured

This task creates the hard project structure that future work depends on:

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

This task does not create player-facing BASED choices.

Its Negotiated value is production-facing: it preserves the agreed workflow where ChatGPT/Nova, GitHub, Codex, and Unity each have a clear role.

---

## Debug / Logging Requirements

No Unity runtime logging is required for this setup task.

However, Codex should clearly report:

- which files were created
- which files were modified
- whether `.gitignore` was updated
- whether the Unity project is expected to live inside `UnityProject/`
- any remaining setup risks

---

## Unity Test Steps

This task may be completed before an actual Unity project exists.

Teddy should test the result as follows:

1. Open the GitHub repo.
2. Confirm the following paths exist:

```text
PROJECT_STATE.md
codex_tasks/TASK_TEMPLATE.md
docs/.gitkeep
agent_specs/.gitkeep
design_packets/.gitkeep
playtest_logs/.gitkeep
course_deliverables/.gitkeep
UnityProject/.gitkeep
```

3. Open `.gitignore`.

4. Confirm it ignores both root-level Unity-generated folders and nested `UnityProject/` generated folders.

5. Later, create or move the Unity project into:

```text
UnityProject/
```

6. After Unity creates local folders such as `UnityProject/Library/` and `UnityProject/Temp/`, confirm GitHub does not show those folders as files to commit.

7. Confirm this task did not create gameplay scripts, Unity scenes, Unity packages, or Unity-generated folders.

---

## Acceptance Criteria

This task is complete only when:

- The repo contains the planned organizational folders.
- Empty folders are tracked using `.gitkeep` files.
- `.gitignore` protects both root-level Unity folders and nested `UnityProject/` folders.
- No Unity-generated folders are committed.
- No Unity project is manually created by this task.
- No gameplay systems are added.
- `PROJECT_STATE.md`, `README.md`, and `codex_tasks/TASK_TEMPLATE.md` are not changed unless absolutely necessary.
- The repo is ready for a future Unity project to live inside `UnityProject/`.
- The next task can safely focus on the runtime blackboard prototype.

---

## Report Before Coding

Before making changes, Codex must report:

1. What it understands this setup task to be.
2. Which files it plans to read.
3. Which files it plans to create or modify.
4. Confirmation that it will use `.gitkeep` files, not folder README files.
5. Confirmation that it will not create a Unity project from scratch.
6. Confirmation that it will not create Unity `Assets/`, `Packages/`, or `ProjectSettings/` manually.
7. Any risks or ambiguities.
8. The smallest safe implementation plan.

Codex should not begin implementation until this plan is reviewed and approved.

---

## Implementation Notes

After approval, Codex should:

- Make the smallest useful setup change.
- Keep the folder structure simple.
- Use `.gitkeep` for empty folder tracking.
- Preserve the current project direction from `PROJECT_STATE.md`.
- Avoid changing design language unless necessary.
- Avoid adding any external dependencies.
- Avoid touching files unrelated to repo setup.
- Prefer clear, boring setup over clever architecture.

Required folder placeholder approach:

```text
docs/.gitkeep
agent_specs/.gitkeep
design_packets/.gitkeep
playtest_logs/.gitkeep
course_deliverables/.gitkeep
UnityProject/.gitkeep
```

Recommended `.gitignore` addition:

```text
# Nested Unity project generated folders
/[Uu]nity[Pp]roject/[Ll]ibrary/
/[Uu]nity[Pp]roject/[Tt]emp/
/[Uu]nity[Pp]roject/[Oo]bj/
/[Uu]nity[Pp]roject/[Bb]uild/
/[Uu]nity[Pp]roject/[Bb]uilds/
/[Uu]nity[Pp]roject/[Ll]ogs/
/[Uu]nity[Pp]roject/[Uu]ser[Ss]ettings/
/[Uu]nity[Pp]roject/[Mm]emory[Cc]aptures/
/[Uu]nity[Pp]roject/[Rr]ecordings/
```

---

## Completion Report

After implementation, Codex should report:

1. Files created or modified.
2. What changed in `.gitignore`.
3. Which folders now exist.
4. Confirmation that no Unity-generated folders were committed.
5. Confirmation that no gameplay systems were created.
6. Confirmation that no Unity project was manually created.
7. How Teddy should verify the setup in GitHub and Unity.
8. Any recommended next task.

Recommended next task after this setup is complete:

```text
TASK_002_RUNTIME_BLACKBOARD
```

---
