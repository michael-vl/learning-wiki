# Godot — 12-Week Practice Schedule

20 minutes daily, 5 days a week. Designed to ship a small game by quarter end.

## Week 1 — Editor and node basics

- [ ] Day 1: [Quickstart](./quickstart.md)
- [ ] Day 2: 5 different node types (Sprite2D, Label, Timer, Area2D, Button); add to a scene
- [ ] Day 3: Attach scripts; print "hello" in `_ready()` for each
- [ ] Day 4: Project Settings → Input Map; add `move_left/right/up/down` actions
- [ ] Day 5: Save a scene, close, reopen; verify nothing's lost

## Week 2 — Movement with CharacterBody2D

- [ ] Day 1: New scene rooted in `CharacterBody2D` + `CollisionShape2D` + `Sprite2D`
- [ ] Day 2: Velocity-based movement in `_physics_process`
- [ ] Day 3: Add gravity + jump + ground check (`is_on_floor()`)
- [ ] Day 4: Use `move_and_slide()`; tune friction and acceleration
- [ ] Day 5: Build a small platform level via TileMapLayer; place player; runs

## Week 3 — Signals and decoupled communication

- [ ] Day 1: Custom signal `signal health_changed(value: int)`; emit, connect
- [ ] Day 2: Connect via Editor (Node dock) and via code (`signal.connect(callable)`)
- [ ] Day 3: Disconnect signals on `_exit_tree`; avoid double-connections
- [ ] Day 4: Pickup as Area2D — `body_entered` triggers collected signal
- [ ] Day 5: HUD listens to a global signal bus (autoload); update score label

## Week 4 — Project: 2D collector

- [ ] Build a top-down 2D collector with player + 5 pickups + score HUD + game-over scene. Ship it.

## Week 5 — Autoloads and globals

- [ ] Day 1: Project Settings → Autoload; add `globals.gd` as `G`
- [ ] Day 2: Game state (score, lives, scene to load) on the autoload
- [ ] Day 3: Scene transitions via `get_tree().change_scene_to_file`
- [ ] Day 4: Save/load with `FileAccess` to `user://save.json`
- [ ] Day 5: Refactor week-4 game to use the autoload pattern

## Week 6 — Custom Resources

- [ ] Day 1: Read [Tutorial Level 4 Custom Resources](./tutorial.md#custom-resources)
- [ ] Day 2: `EnemyData` resource subclass with `@export` fields
- [ ] Day 3: Create 3 enemies (goblin, orc, troll) as `.tres` resources
- [ ] Day 4: An enemy scene that takes `@export var data: EnemyData`
- [ ] Day 5: Spawn enemies in your level using their resource data

## Week 7 — UI with Control nodes and Containers

- [ ] Day 1: Build a main menu — VBoxContainer with three Buttons
- [ ] Day 2: Wire Buttons to scene transitions
- [ ] Day 3: Settings menu — sliders bound to AudioServer bus volumes
- [ ] Day 4: Theme resource — apply a custom font, color
- [ ] Day 5: Pause menu (set `get_tree().paused = true`)

## Week 8 — State machines for AI

- [ ] Day 1: Implement the [State pattern](./tutorial.md#state-machine-pattern) for an enemy
- [ ] Day 2: Three states: Idle, Patrol, Chase
- [ ] Day 3: RayCast2D for line-of-sight; transition to Chase
- [ ] Day 4: Patrol path via Path2D + PathFollow2D
- [ ] Day 5: Tune transitions; **journal what feels right**

## Week 9 — Animation

- [ ] Day 1: AnimationPlayer with keyframes for sprite frames
- [ ] Day 2: Method tracks — call `take_damage` at a specific frame
- [ ] Day 3: AnimationTree with state machine; idle/walk/attack
- [ ] Day 4: AnimatedSprite2D for simple frame animation
- [ ] Day 5: Tween (`create_tween`) for property interpolation in code

## Week 10 — Shaders and 2D effects

- [ ] Day 1: Read [Shader: flag wave](./examples.md#10-shader-flag-wave-2d)
- [ ] Day 2: Apply ShaderMaterial to a Sprite2D; modify uniforms from script
- [ ] Day 3: Dissolve effect (discard based on noise threshold)
- [ ] Day 4: Outline shader for selected enemy
- [ ] Day 5: CanvasModulate for day/night cycle

## Week 11 — Audio and polish

- [ ] Day 1: AudioStreamPlayer for music; AudioStreamPlayer2D for positional SFX
- [ ] Day 2: Audio buses; volume control in settings
- [ ] Day 3: Camera shake on damage
- [ ] Day 4: Particle effects (GPUParticles2D) for hit feedback
- [ ] Day 5: Screen transitions (fade, wipe) on scene change

## Week 12 — Build and ship

- [ ] Day 1: Editor → Manage Export Templates → Download
- [ ] Day 2: Export → Add Preset → Windows/Mac/Linux Desktop
- [ ] Day 3: Web export with itch.io COOP/COEP setting
- [ ] Day 4: Test build on a friend's machine
- [ ] Day 5: Upload to itch.io; **post-mortem in journal**

---

## After Week 12

- 3D? Same engine, very similar workflow. Pick a 3D project for next quarter.
- Multiplayer? Godot's HighLevelMultiplayer API is very approachable.
- Editor plugin? Godot's editor is itself a Godot scene — extend in GDScript.
- Cross-reference [Mental Models](../mental-models.md) — Godot scenes ↔ Unity prefabs.
