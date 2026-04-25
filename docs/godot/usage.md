# Usage — Godot

## Editor anatomy

Default layout, top to bottom and left to right:

- **FileSystem dock** (bottom-left) — your project's files.
- **Scene dock** (top-left) — the active scene's node tree.
- **Inspector** (right) — properties of the selected node.
- **Node dock** (right, second tab) — signals and groups for the selected node.
- **2D / 3D / Script / AssetLib** workspace switcher (top-center).
- **Output / Debugger / Audio / Animation** panels (bottom).

Switch between **2D** and **3D** workspaces from the top center. The **Script editor** is built-in and full-featured (no external editor required, though you can use VS Code with the godot-tools extension).

## Scenes and nodes

- **Right-click in the Scene dock → Add Child Node** to add a node.
- Save with `Ctrl+S` — a scene becomes a `.tscn` file in your project.
- **Instance a scene** as a child of another with the chain-link icon (or `Ctrl+Shift+A`). This is composition.
- A scene's root node defines what the scene *is*: a `CharacterBody2D` root means the scene is a character; a `Node2D` root means it's a generic 2D scene.

## Common nodes you'll use constantly

### 2D
- `Node2D` — generic 2D node with transform.
- `Sprite2D` — displays a texture.
- `AnimatedSprite2D` — sprite with frame-based animation.
- `CharacterBody2D` — kinematic character.
- `RigidBody2D` — physics body.
- `Area2D` — overlap detection (triggers).
- `CollisionShape2D` — child of bodies/areas to define collision.
- `Camera2D` — viewport camera.

### 3D
- `Node3D` — generic 3D node.
- `MeshInstance3D` — displays a mesh.
- `CharacterBody3D` — kinematic character.
- `RigidBody3D` — physics body.
- `Area3D` — overlap detection.
- `CollisionShape3D` — child of body/area.
- `Camera3D` — viewport camera.
- `DirectionalLight3D` / `OmniLight3D` / `SpotLight3D` — lights.
- `WorldEnvironment` — sky, fog, post-processing.

### UI (Control nodes)
- `Control` — base of all UI.
- `Label` — text.
- `Button`, `LineEdit`, `TextEdit`, `OptionButton`, etc.
- `Container`, `HBoxContainer`, `VBoxContainer`, `GridContainer` — layout.
- `MarginContainer`, `PanelContainer` — wrappers.
- `CanvasLayer` — pin UI to the screen, not the world.

### Utility
- `Timer` — fires a signal after duration; great for one-shot delays.
- `AnimationPlayer` — keyframes properties of any node, including signals as method tracks.
- `AnimationTree` — state machines and blend trees over animations.
- `AudioStreamPlayer` (and `2D`/`3D` variants) — audio playback.
- `Tween` (created in code, not a node anymore in Godot 4) — interpolate properties without keyframes.

## GDScript essentials

```gdscript
extends CharacterBody2D

@export var speed: float = 200.0
@export var jump_velocity: float = -400.0

const GRAVITY := 980.0

func _physics_process(delta: float) -> void:
    if not is_on_floor():
        velocity.y += GRAVITY * delta

    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_velocity

    var direction := Input.get_axis("move_left", "move_right")
    velocity.x = direction * speed

    move_and_slide()
```

### Key syntax notes
- `extends X` — class inherits from node type X.
- `@export var foo` — exposes the variable in the Inspector.
- `func _ready() -> void` — called when the node and its children enter the scene tree.
- `func _process(delta)` — every frame.
- `func _physics_process(delta)` — at the physics tick rate.
- `:=` is type-inferred declaration; `: int =` is explicit.
- Signals with `signal my_signal(arg1, arg2)`; emit with `my_signal.emit(a, b)`.

### Type hints (recommended)
GDScript is dynamically typed but supports static hints. **Use them.** Better autocomplete, faster runtime, errors caught at parse time.

```gdscript
var health: int = 100
func take_damage(amount: int) -> void:
    health -= amount
```

## Signals

Signals are Godot's event system. Built into nearly every node.

### Connecting in the editor
Select a node → Node dock → list of signals. Double-click a signal → choose the receiver and method. Generates a `func _on_signal_name(args)` stub on the receiver.

### Connecting in code

```gdscript
func _ready() -> void:
    $Button.pressed.connect(_on_button_pressed)

func _on_button_pressed() -> void:
    print("Clicked!")
```

### Custom signals

```gdscript
signal health_changed(new_value: int)

func take_damage(amount: int) -> void:
    health -= amount
    health_changed.emit(health)
```

Signals are how you decouple. The HUD listens for `health_changed`; the player doesn't know about the HUD.

## Node access

```gdscript
@onready var sprite: Sprite2D = $Sprite2D    # child by name
@onready var hud: HUD = %HUD                  # by unique name (set in editor)
@onready var bullet: Bullet = preload("res://scenes/bullet.tscn").instantiate()
```

- `$Path/To/Node` is shorthand for `get_node("Path/To/Node")`.
- `%Name` accesses a node marked as a *Unique Name* in the scene (% icon in Scene dock).
- `preload` loads at parse time (resource path is constant); `load` is dynamic at runtime.

## Lifecycle

- `_init()` — when the object is created (rare to override).
- `_enter_tree()` — when the node enters the scene tree.
- `_ready()` — when the node *and all descendants* are ready. Use for setup.
- `_process(delta)` — per frame.
- `_physics_process(delta)` — per physics tick.
- `_input(event)` / `_unhandled_input(event)` — input events.
- `_exit_tree()` — when leaving the scene tree.

## File layout

A typical project:

```
res://
├── scenes/
│   ├── player.tscn
│   ├── enemy.tscn
│   ├── ui/
│   └── levels/
├── scripts/
│   ├── player.gd
│   ├── enemy.gd
│   └── globals/
├── art/
├── audio/
├── shaders/
└── project.godot          # project settings file
```

`res://` refers to the project root. `user://` is the writable per-user directory (saves, settings) — Godot resolves the OS-specific path for you.

## Project settings

`Project > Project Settings`. Highlights:

- **Application > Run > Main Scene** — the scene loaded on startup.
- **Application > Config > Name / Icon** — your game's identity.
- **Display > Window** — resolution, stretch mode (`canvas_items` for crisp 2D scaling, `viewport` for pixel art).
- **Input Map** — name actions ("jump", "move_left") and bind keys/buttons. Read with `Input.is_action_pressed("jump")`.
- **Rendering > Renderer** — Forward+ (default desktop), Mobile (deferred, mobile/web), or Compatibility (GLES3).
- **Autoload** — singleton scripts/scenes loaded once at startup, accessible globally by name.

## Common gotchas

- **`$Node` returns null** — wrong path, or you're calling it before `_ready()` (use `@onready`).
- **Physics jitter** — moving in `_process` instead of `_physics_process`. Move bodies in physics_process.
- **Signal connected twice** — an `_on_X` callback fires twice when you both connect in editor *and* in code. Pick one.
- **CharacterBody movement does nothing** — forgot `move_and_slide()` after setting `velocity`.
- **Collision layers don't match** — set both layer and mask correctly. Layer is "what I am"; mask is "what I check against."
- **UI nodes don't show up** — UI lives under a `CanvasLayer` *or* directly under a `Control` root; it doesn't inherit world transforms.
- **Exported variable doesn't persist** — you renamed the variable; old `.tscn` references are by name. Re-set it in the Inspector.
