# Best Practices — Godot

## Project setup

- **Use the latest stable Godot 4.x.** The 4.x line is mature; new patches generally don't break projects.
- **Pick a renderer at project creation:**
  - **Forward+** — desktop-first, modern lighting, default.
  - **Mobile** — deferred-ish, optimized for mobile / web.
  - **Compatibility** — GLES3, widest device support, weakest features.
  - You can change later but it's painful — pick deliberately.
- **GDScript by default; C# only if you have a reason.** GDScript is faster to iterate, has tighter editor integration, and ships with the engine. C# requires the .NET-enabled build of Godot and a separate runtime.

## File organization

```
res://
├── scenes/
│   ├── player/
│   ├── enemies/
│   ├── ui/
│   └── levels/
├── scripts/
│   └── (mirrors scenes/, or grouped by domain)
├── resources/        # .tres / .res custom resources
├── art/
├── audio/
├── shaders/
├── addons/           # editor plugins
└── project.godot
```

- **One scene = one folder when it has multiple files** (script + scene + assets specific to it). Keep them together.
- **`res://scripts/` only for scripts not bound to a single scene** (utilities, autoloads, abstract base classes).
- **Snake_case** filenames: `player_character.gd`, `health_pickup.tscn`. Godot's convention.

## Naming

- **Files** snake_case.
- **Classes** PascalCase via `class_name` if you want global access.
- **Variables and functions** snake_case.
- **Constants** SCREAMING_SNAKE_CASE.
- **Signals** snake_case past-tense verbs: `health_changed`, `enemy_died`, `coin_collected`.

## GDScript style

- **Always type your variables and function signatures**. Faster, clearer, catches bugs:
  ```gdscript
  func add(a: int, b: int) -> int:
      return a + b
  ```
- **`@onready` for child node references**:
  ```gdscript
  @onready var sprite: Sprite2D = $Sprite2D
  ```
- **`@export` to expose to the Inspector**:
  ```gdscript
  @export var speed: float = 200.0
  @export_range(0, 100) var health: int = 100
  ```
- **Use `class_name` to register globally** when you want a type usable from anywhere without preloads.
- **Don't `print` everything in production.** Use a custom logger that respects a debug flag.

## Architecture

### Composition via scenes
- A scene is your reusable unit. Make small scenes (`HealthBar.tscn`, `Hurtbox.tscn`) and compose them into bigger ones.
- A character scene with a child Hurtbox scene, AnimationPlayer scene, and weapon-mount scene is more modular than one monolithic CharacterBody.

### Signals over polling
- If A needs to react to B, B emits a signal; A connects. Don't have A check B's state every frame.
- Custom signals on autoloads ("signal buses") are how distant systems communicate without referencing each other.

### Custom Resources for data
- Items, enemy stats, level definitions — make them `Resource` subclasses with `@export` fields. Designers tweak `.tres` files without touching code.

### Don't autoload everything
- Use autoloads for: persistent global state, scene transitions, audio bus, signal buses.
- Don't use autoloads for: per-level state, per-character state, anything that has multiple instances.

### Avoid deep `get_node` paths
- `get_node("../../UI/HUD/Score")` is brittle.
- Use Unique Names (`%HUD`) or signals to communicate up the tree.

## Performance

### Rules
- **Profile before optimizing.** Debugger > Profiler.
- **Move physics work to `_physics_process`**, gameplay/render-tied work to `_process`.
- **Pre-allocate arrays and dictionaries** outside hot loops.
- **`MultiMesh`** for thousands of identical meshes (grass, debris, instanced props).
- **GPU particles** for high counts; CPU particles only for systems needing per-particle scripting.
- **Texture atlasing** reduces draw calls in 2D.
- **Occluders** in 3D — `OccluderInstance3D`, bake the occluder mesh.

### Avoid

- `instance_from_id()` and other reflection in hot loops.
- Calling `get_node` repeatedly — cache it.
- String operations per frame — `"Score: %d" % x` allocates; only do it when the value changes.
- Connecting and disconnecting signals every frame — connect once.

## Physics layers

- Define layers in Project Settings > Layer Names → 2D Physics / 3D Physics.
- Use named layers like "world", "player", "enemy", "pickup", "hurtbox", "hitbox".
- Set each body/area's *Collision Layer* (what I am) and *Collision Mask* (what I detect).
- A common layout:
  - Layer 1: world
  - Layer 2: player
  - Layer 3: enemy
  - Layer 4: pickup
  - Layer 5: hurtbox (receives damage)
  - Layer 6: hitbox (deals damage)

## UI

- Build UI in **Container nodes** (`HBoxContainer`, `VBoxContainer`, `MarginContainer`, etc.) — they handle layout automatically.
- Don't position Control nodes by hand — use containers and anchors.
- A `CanvasLayer` over the world keeps HUDs at fixed screen coords regardless of camera.
- For complex UI, use a `Theme` resource — Godot's equivalent of CSS for the engine.
- **Labels with translations**: use `tr("KEY")` and load translation CSVs in Project Settings > Localization.

## Animation

- `AnimationPlayer` keyframes any property of any node. Use it not just for character animation but for cutscenes, UI sequences, anything time-based.
- `AnimationTree` adds state machines and blend trees on top — clean way to manage complex character animation states.
- For interpolation in code, **`Tween`** (created with `create_tween()`) is the easy path: `tween.tween_property(node, "position", target, 0.5)`.

## Version control

- **`.gitignore`** must include `.godot/` (4.x's cache directory). Optional: `*.import` (regenerated). Most teams commit `*.import` to avoid reimport churn on others' machines.
- **Commit `.tscn` and `.tres` text files** — they merge OK most of the time. Big scene merges are still painful; design your scenes to be small.
- **Git LFS** for large binaries (psd, fbx, wav).

## Pitfalls

1. **`_ready()` runs before children's `_ready()`** — actually no, it runs **after** children's `_ready()`, in depth-first order. Child setup is done by the time the parent is ready.
2. **`@onready` triggers at `_ready` time** — if you query a node manually in `_init` you'll get null.
3. **Scene with a script attached to root**, then you change the root node type — the script may break silently. Re-check.
4. **Signal connected in editor but the receiver's method doesn't fire** — typo in the method name, or the receiver was instantiated separately (signals attach to a specific object).
5. **`move_and_slide` doesn't move** — `velocity` is zero, or you're inside a wall (collision shape too big).
6. **Exported variable disappears in the Inspector** — you renamed the variable. Old `.tscn` references are by name.
7. **Player gets stuck on floor seams** — set the player's CollisionShape `safe_margin` to a small positive value, or use a Capsule shape (no flat bottom).
8. **Tween doesn't run** — you forgot to assign it: `var t := create_tween(); t.tween_property(...)`. The `create_tween()` return must persist long enough; usually fine since it's owned by the node tree.
9. **AnimationPlayer plays once and stops** — you changed scene; AnimationPlayer is gone. Connect "animation_finished" signal to chain animations.
10. **Web export blank screen** — your host doesn't send the COOP/COEP headers. Itch.io's *SharedArrayBuffer support* checkbox fixes it.

## Habits of strong Godot developers

- **Scenes you can run in isolation.** A `Player.tscn` should work even when not embedded in a level — drop placeholder ground beneath, hit F6 (run current scene). Catches a class of bugs immediately.
- **F6 over F5.** Run the current scene; don't always boot the whole game.
- **One signal bus autoload, with strict naming.** "Signals start with the noun, end with the past-tense verb": `player_died`, `score_updated`, `level_loaded`. Consistency makes the bus readable.
- **Custom resources for everything that's "data."** Items, enemies, dialogue lines, levels.
- **Editor plugins for repeated grunt work.** Godot's editor is itself written in Godot — extending it is GDScript, not arcane C++.
