# Godot — Quickstart (30 minutes)

If you have 30 minutes, do exactly these three things.

!!! tip "Why Godot?"
    Free, open-source, ~100MB binary, instant launch, no account required. Lower friction than Unity for prototyping.

---

## 1. Install + new project (5 min)

- Download Godot 4.x from [godotengine.org/download](https://godotengine.org/download). Pick the **Standard** build (GDScript only) unless you specifically want C#.
- Unzip, run the binary. No installer.
- Click *New Project*. Renderer: **Forward+**. Pick a folder. Create.

---

## 2. The scene-of-nodes mental model (15 min)

Everything is a Node. A Scene is a tree of Nodes saved as a `.tscn` file.

- Click *Add Node* (the + at the top of the Scene dock).
- Search "Node2D"; add it as the root. Save scene as `main.tscn`.
- Right-click the Node2D → *Add Child Node* → `Sprite2D`.
- In the Inspector, drag the included `icon.svg` (in FileSystem) onto the *Texture* property.
- You see the Godot icon in the viewport.

Now attach a script:
- Right-click `Sprite2D` → *Attach Script*. Save as `mover.gd`. Replace contents:

```gdscript
extends Sprite2D

@export var speed: float = 200.0

func _process(delta: float) -> void:
    var input := Vector2(
        Input.get_axis("ui_left", "ui_right"),
        Input.get_axis("ui_up", "ui_down"))
    position += input * speed * delta
```

- Press `F5` to run. Pick `main.tscn` as the main scene. Arrow keys move the sprite.

What you used: a Node (`Sprite2D`), a script extending it, `@export` (Inspector), `_process(delta)` (per-frame), `Input` (built-in singleton). These five concepts cover most of GDScript.

---

## 3. Signals — the event system (10 min)

- Add another node: `Timer` as a child of the Node2D root.
- In the Inspector: Wait Time = 1.0, Autostart = on.
- Click the **Node** dock (right side, second tab) — list of signals.
- Double-click `timeout`. In the dialog, pick the script holding node, method `_on_timer_timeout`. Connect.
- A new function appears in `mover.gd`:

```gdscript
func _on_timer_timeout() -> void:
    rotation_degrees += 90
```

- Run again. The sprite rotates every second.

You just used Godot's signal system — the way nodes talk to each other without tight coupling.

---

## What's next

- **Tomorrow:** read [Usage](./usage.md), focusing on "Common nodes you'll use constantly" and "Signals."
- **This week:** start [Tutorial Level 1](./tutorial.md#level-1--move-a-sprite) and follow the [12-week schedule](./practice-schedule.md).
- **Anki users:** import [godot.csv](../../anki/godot.csv) — node types, GDScript syntax, signal API.
- **F6 over F5.** Run the *current* scene (F6) instead of the whole game (F5) while iterating.
