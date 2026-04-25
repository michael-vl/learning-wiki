# Examples — Godot

Concrete recipes. Rebuild rather than copy-paste.

---

## 1. Smooth camera follow (2D)

```gdscript
extends Camera2D

@export var target_path: NodePath
@export var smoothness: float = 8.0
@onready var target: Node2D = get_node(target_path)

func _process(delta: float) -> void:
    if target == null: return
    global_position = global_position.lerp(target.global_position, smoothness * delta)
```

> `Camera2D` has built-in *Position Smoothing* in the Inspector — toggle it before writing custom code. The script above is for cases where you want the smoothing tied to game-time, or to combine with screen-shake.

---

## 2. Screen shake

```gdscript
extends Camera2D

var shake_amount: float = 0.0
var shake_decay: float = 5.0

func _process(delta: float) -> void:
    if shake_amount > 0.0:
        offset = Vector2(
            randf_range(-shake_amount, shake_amount),
            randf_range(-shake_amount, shake_amount))
        shake_amount = move_toward(shake_amount, 0.0, shake_decay * delta)
    else:
        offset = Vector2.ZERO

func shake(amount: float) -> void:
    shake_amount = max(shake_amount, amount)
```

Call `shake(8)` on damage, explosions, big landings.

---

## 3. Object pooling

```gdscript
extends Node
class_name Pool

@export var scene: PackedScene
@export var initial_size: int = 32
var available: Array[Node] = []

func _ready() -> void:
    for i in initial_size:
        var inst := scene.instantiate()
        inst.process_mode = Node.PROCESS_MODE_DISABLED
        add_child(inst)
        available.append(inst)

func acquire() -> Node:
    if available.is_empty():
        var inst := scene.instantiate()
        add_child(inst)
        return _wake(inst)
    return _wake(available.pop_back())

func release(node: Node) -> void:
    node.process_mode = Node.PROCESS_MODE_DISABLED
    available.append(node)

func _wake(node: Node) -> Node:
    node.process_mode = Node.PROCESS_MODE_INHERIT
    return node
```

The pooled scene's script should call `pool.release(self)` instead of `queue_free()` when "destroyed."

---

## 4. Custom resource for items

```gdscript
# item.gd
extends Resource
class_name Item

@export var display_name: String
@export var icon: Texture2D
@export var max_stack: int = 99
@export var description: String
```

Now any inventory slot has `@export var item: Item` and the editor lets the designer drop in a `.tres` resource file.

---

## 5. Inventory autoload

```gdscript
# globals.gd (autoload)
extends Node

signal inventory_changed

class Slot:
    var item: Item
    var count: int

var slots: Array[Slot] = []

func add(item: Item, n: int) -> void:
    for slot in slots:
        if slot.item == item and slot.count < item.max_stack:
            var add_n: int = mini(n, item.max_stack - slot.count)
            slot.count += add_n
            n -= add_n
            if n == 0: break
    while n > 0:
        var slot := Slot.new()
        slot.item = item
        slot.count = mini(n, item.max_stack)
        slots.append(slot)
        n -= slot.count
    inventory_changed.emit()
```

UI listens: `G.inventory_changed.connect(_refresh)`.

---

## 6. AnimationPlayer with method tracks

`AnimationPlayer` can keyframe properties *and* call methods:
- Add a Method Track in the animation editor.
- At a frame, call `do_attack_hit` on a script, passing args.

This lets a designer place hit-frames, sound-cue triggers, and screen-shake calls on the timeline without touching code.

---

## 7. Dialogue system (minimal)

```gdscript
extends CanvasLayer

@onready var label: RichTextLabel = %DialogueLabel
@onready var portrait: TextureRect = %Portrait

var lines: Array[Dictionary] = []
var index: int = -1

func play(new_lines: Array[Dictionary]) -> void:
    lines = new_lines
    index = -1
    advance()

func advance() -> void:
    index += 1
    if index >= lines.size():
        hide()
        return
    show()
    label.text = lines[index].get("text", "")
    portrait.texture = lines[index].get("portrait", null)

func _input(event: InputEvent) -> void:
    if event.is_action_pressed("ui_accept") and visible:
        advance()
        get_viewport().set_input_as_handled()
```

Trigger from a cutscene:

```gdscript
G.dialogue.play([
    {"text": "Hello, traveler.", "portrait": preload("res://art/old_man.png")},
    {"text": "Have you seen my chicken?", "portrait": preload("res://art/old_man.png")},
])
```

Real games will want a typewriter effect, branching, and localization keys — extend from this skeleton.

---

## 8. Top-down 2D enemy with line-of-sight chase

```gdscript
extends CharacterBody2D

@export var speed: float = 80.0
@export var sight_range: float = 200.0
@export var target_path: NodePath
@onready var target: Node2D = get_node(target_path)
@onready var ray: RayCast2D = $RayCast2D

enum State { IDLE, CHASE }
var state: State = State.IDLE

func _physics_process(delta: float) -> void:
    var to_target := target.global_position - global_position
    ray.target_position = to_target
    ray.force_raycast_update()

    var sees := not ray.is_colliding() and to_target.length() < sight_range

    match state:
        State.IDLE:
            velocity = Vector2.ZERO
            if sees: state = State.CHASE
        State.CHASE:
            velocity = to_target.normalized() * speed
            if not sees: state = State.IDLE

    move_and_slide()
```

`RayCast2D`'s collision mask must include the level walls but exclude the player and the enemy itself.

---

## 9. Save / load

```gdscript
func save_game(data: Dictionary) -> void:
    var f := FileAccess.open("user://save.json", FileAccess.WRITE)
    f.store_string(JSON.stringify(data, "  "))

func load_game() -> Dictionary:
    if not FileAccess.file_exists("user://save.json"): return {}
    var f := FileAccess.open("user://save.json", FileAccess.READ)
    var parsed = JSON.parse_string(f.get_as_text())
    return parsed if parsed is Dictionary else {}
```

`user://` resolves per-platform (`%APPDATA%\Godot\app_userdata\<game>` on Windows, `~/Library/Application Support/Godot/app_userdata/<game>` on macOS, etc.).

---

## 10. Shader: flag wave (2D)

`flag.gdshader`:

```glsl
shader_type canvas_item;

uniform float amplitude : hint_range(0.0, 0.2) = 0.04;
uniform float frequency : hint_range(0.0, 20.0) = 6.0;
uniform float speed : hint_range(0.0, 10.0) = 2.0;

void vertex() {
    VERTEX.x += sin(VERTEX.y * frequency + TIME * speed) * amplitude * VERTEX.y;
}
```

Apply to a `Sprite2D`'s ShaderMaterial. The wave amplitude scales with vertical position so the fixed end (top) doesn't move and the free end (bottom) waves more. Add subdivisions (a `MeshInstance2D` with a quad mesh has more vertices to animate than a `Sprite2D`'s 4-vert quad).
