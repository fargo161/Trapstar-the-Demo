# PhaserProject

This directory is reserved for the **Phaser 3.90 + TypeScript** implementation of *Trapstar the Demo*.

No framework files or dependencies are committed yet. Project creation should happen through an approved bounded Codex task rather than an unscoped setup pass.

Expected conceptual separation:

```text
src/
  simulation/   # portable state, rules, action resolution, seeded randomness
  presentation/ # Phaser scenes, sprites, input, movement, UI, audio
  content/      # portable definitions and balancing data
tests/          # simulation and integration tests
public/assets/  # standardized visual and audio assets
```

Portable simulation code must not import Phaser or store Phaser objects as game-state truth.
