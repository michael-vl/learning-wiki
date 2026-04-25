# Tutorial — Godot Beginner to Advanced

Five levels.

---

## Level 1 — Move a sprite

**Goal:** sprite moves with arrow keys; you understand scene/node basics.

1. New project. Pick *Forward+* renderer.
2. Add a `Node2D` as the root. Save the scene as `main.tscn`.
3. Right-click root → Add Child Node → `Sprite2D`. Drag any image (the Godot icon at `res://icon.svg` works) onto its *Texture* property.
4. Project Settings → Input Map → add actions: `move_left` (A and Left), `move_right` (D and Right), `move_up` (W and Up), `move_down` (S and Down).
5. Right-click the Sprite2D → Attach Script. Save as `mover.gd`.

```gdscript
extends Sprite2D

@export var speed: float = 200.0

func _process(delta: float) -> void:
    var input := Vector2(
        Input.get_axis("move_left", "move_right"),
        Input.get_axis("move_up", "move_down"))
    position += input * speed * delta
```

6. Project > Run Project (`F5`). It asks for a main scene; pick `main.tscn`. WASD/Arrows move the sprite.

**Concepts:** scene tree, node attachment, `_process(delta)`, `Input.get_axis`, `position`.

---

## Level 2 — A real movement scene

**Goal:** a `CharacterBody2D` with gravity, jump, and proper collisions on a tile-based level.

1. New scene → root: `CharacterBody2D` → save as `player.tscn`.
2. Add child: `CollisionShape2D`. Inspector → Shape → New RectangleShape2D, size to fit.
3. Add child: `Sprite2D` with a placeholder texture.
4. Attach script:

```gdscript
extends CharacterBody2D

@export var speed: float = 200.0
@export var jump_velocity: float = -380.0
const GRAVITY := 980.0

func _physics_process(delta: float) -> void:
    if not is_on_floor():
        velocity.y += GRAVITY * delta

    if Input.is_action_just_pressed("jump") and is_on_floor():
        velocity.y = jump_velocity

    velocity.x = Input.get_axis("move_left", "move_right") * speed
    move_and_slide()
```

5. New scene → root: `Node2D` → save as `level.tscn`.
6. Add child: `TileMapLayer`. Create a TileSet resource: drag a tile sheet image, define cells, set physics layer 0 with collision polygons on solid tiles.
7. Paint a floor and a couple of platforms.
8. Instance `player.tscn` in the level (chain-link icon → select). Place above the floor.
9. Make `level.tscn` the main scene, run.

**Concepts:** physics bodies, `move_and_slide`, `TileMapLayer`, scene instancing.

> Note: Godot 4.3 deprecated the older `TileMap` node in favor of one or more `TileMapLayer` nodes — easier to layer foreground/background.

---

## Level 3 — Signals, scenes, and game state

**Goal:** a coin pickup, a score, a HUD, and a game-over flow.

### Coin

1. New scene: `Area2D` root → `coin.tscn`. Add `Sprite2D` and `CollisionShape2D` children.
2. Script on the coin:

```gdscript
extends Area2D

signal collected

func _ready() -> void:
    body_entered.connect(_on_body_entered)

func _on_body_entered(body: Node2D) -> void:
    if body.is_in_group("player"):
        collected.emit()
        queue_free()
```

3. In the player script, add the player to the "player" group: in editor → Node dock → Groups tab → add "player".

### HUD and score

1. Create `hud.tscn`: `CanvasLayer` root → `Label` child. Mark the Label as a **Unique Name** in the scene (right-click → Access as Unique Name) and rename to "ScoreLabel".
2. Script on the HUD:

```gdscript
extends CanvasLayer

@onready var score_label: Label = %ScoreLabel
var score: int = 0

func add_score(n: int) -> void:
    score += n
    score_label.text = "Score: %d" % score
```

3. In the level, instance the HUD. When you instance a coin (or for each existing coin in the level), connect its `collected` signal to a level method that calls `hud.add_score(1)`.

### Game over

A hazard is another `Area2D` that, on `body_entered`, calls `get_tree().reload_current_scene()` or loads a `game_over.tscn`.

```gdscript
get_tree().change_scene_to_file("res://scenes/game_over.tscn")
```

---

## Level 4 — Architecture: autoloads, custom resources, state machines

### Autoloads (singletons done right)

Project Settings → Autoload. Add a script (e.g. `globals.gd`) with a name (e.g. "G"). Now `G.score`, `G.player_died.emit()` are accessible from any script.

```gdscript
# globals.gd
extends Node

signal player_died
var score: int = 0

func add_score(n: int) -> void:
    score += n
```

Use autoloads for: scene transitions, persistent settings, one-instance services (audio bus, save system). Don't shove everything in autoloads — they're powerful but a god-object is a god-object.

### Custom resources

Godot's equivalent to Unity's ScriptableObject. Create a `Resource` subclass:

```gdscript
# enemy_data.gd
extends Resource
class_name EnemyData

@export var display_name: String
@export var max_health: int = 100
@export var move_speed: float = 80.0
@export var sprite: Texture2D
```

Right-click in FileSystem → New Resource → `EnemyData`. Fill in the Inspector. Save as `goblin.tres`. Now an enemy scene can take an `@export var data: EnemyData` and you have data-driven enemies.

### State machine pattern

For an enemy with idle/patrol/chase/attack:

```gdscript
# state.gd
extends Node
class_name State

func enter() -> void: pass
func exit() -> void: pass
func process(delta: float) -> void: pass
```

Each state is a child node extending `State`. A `StateMachine` node holds a reference to the current state, handles transitions, and ticks `process()` from `_physics_process()`.

Or use Godot's built-in `AnimationTree` with state machine mode for animation states; combine with code-driven gameplay states for behavior.

### Signal-driven decoupling

Your HUD shouldn't know about your player; both should know about a global signal channel. Use the `G` autoload (above), or create dedicated signal-bus autoloads (`SignalBus.player_health_changed.emit(value)`).

---

## Level 5 — Performance, shaders, exports, multiplayer

### Profiling

- Debugger panel → Profiler tab. Start, play, stop, inspect.
- Monitor frametime, idle vs. physics, function-level samples.
- Visual profiler (graphics) shows GPU breakdown by pass.

### Common perf wins (Godot-specific)

- **Use `_physics_process` for physics, `_process` for everything else.** Don't double-do work.
- **`MultiMeshInstance3D` / `MultiMesh`** for thousands of identical instances.
- **Occlusion culling** — bake an occlusion mesh from `OccluderInstance3D`. Cuts draw calls dramatically in dense scenes.
- **GPU particles** (`GPUParticles2D` / `3D`) over CPU particles when the count is large.
- **Texture compression** — for desktop ETC2/BPTC; for mobile target ASTC. Project Settings → Rendering → Textures.
- **Don't allocate in hot paths.** Pre-allocate Vector2/3 arrays, reuse.
- **Avoid `instantiate()` per frame.** Pool instances.

### Custom shaders

Godot has its own shader language (GLSL with conveniences). Create a `ShaderMaterial` on a sprite/mesh, add a `Shader` resource:

```glsl
// dissolve.gdshader
shader_type canvas_item;

uniform sampler2D noise_tex;
uniform float threshold : hint_range(0.0, 1.0) = 0.5;
uniform vec4 edge_color : source_color = vec4(1.0, 0.5, 0.0, 1.0);

void fragment() {
    vec4 base = texture(TEXTURE, UV);
    float n = texture(noise_tex, UV).r;
    float diff = n - threshold;
    if (diff < 0.0) discard;
    if (diff < 0.05) COLOR = edge_color;
    else COLOR = base;
}
```

Drive `threshold` from script:

```gdscript
material.set_shader_parameter("threshold", t)
```

### Exports

- Project > Export. Add a preset (Windows Desktop, macOS, Linux/X11, Android, iOS, Web).
- First-time exports require **export templates**: Editor > Manage Export Templates > Download. Match the template version to your editor.
- For mobile: install platform SDKs (Android Studio for Android; Xcode for iOS) and configure paths.
- For Web: Godot 4 web exports require SharedArrayBuffer headers (COEP/COOP) on your host. Itch.io supports this with a checkbox.

### Multiplayer

- Built-in **High-level Multiplayer API** with `MultiplayerPeer` (ENet, WebSocket, WebRTC, custom transports).
- Mark methods with `@rpc("any_peer", "call_local")` for replication.
- For larger games: Godot's networking is solid for small-scale (4–8 players). For larger or competitive, integrate dedicated servers and consider rollback netcode (community libraries available).

```gdscript
@rpc("any_peer", "call_local")
func say_hello(text: String) -> void:
    print("Player %d says: %s" % [multiplayer.get_remote_sender_id(), text])
```

### Shipping checklist

- Settings menu (audio, key rebinds — Input Map can be modified at runtime via `InputMap.action_*`).
- Save / load via `FileAccess` to `user://saves/`.
- Localization with the `tr("KEY")` system and CSV translation files.
- Crash reporting via Sentry SDK or in-engine `OS.alert` for fatal handlers.
- Test on the lowest-spec target you commit to. Frame budget early.

### What "advanced" means in Godot

You can ship a game with a custom editor plugin (yes, Godot's editor is itself a Godot scene — extensible from inside), a clear node/scene architecture that another developer can navigate, and exports running smoothly on at least three platforms. That's the bar.
