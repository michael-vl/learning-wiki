# Godot — Beginner to Advanced

!!! tip "If you only do one thing"
    Run scenes in isolation with **F6** instead of always launching the whole project with F5. Catches a class of bugs immediately and tightens the iteration loop. Each scene should work standalone — that's the discipline that makes Godot projects scale.

!!! note "GDScript by default; C# only with reason"
    GDScript has tighter editor integration and faster iteration. Pick C# only if you're coming from Unity, need .NET libraries, or have a specific perf concern.

A guide to **Godot 4.3+**: an open-source, MIT-licensed game engine with a clean node/scene model, a first-class scripting language (GDScript), and full C# support via .NET.

## Scope

- The Godot editor and node/scene system.
- GDScript 2.0 — Godot's primary scripting language.
- C# scripting via .NET 8/9.
- 2D and 3D workflows.
- Physics, animation, audio, particles.
- The Forward+ renderer (Vulkan), Mobile renderer, and Compatibility (GLES3) renderer.
- Shaders in Godot's shader language (GLSL-ish).
- Exports and shipping.

## Sections

1. [Usage](./usage.md) — editor, scenes, nodes, signals
2. [Tutorial](./tutorial.md) — Level 1 → Level 5
3. [Examples](./examples.md) — concrete scripts and scenes
4. [Best Practices](./best-practices.md) — conventions and pitfalls
5. [Learning](./learning.md) — resources

## Prerequisites

- General programming literacy. **GDScript is intentionally easy** — Python-like, dynamically typed (with optional static types). If you've written Python, you'll write GDScript on day one.
- **C# Godot** is fully supported but lags GDScript on cutting-edge features by a release. Pick C# if you're coming from Unity or you need .NET libraries; otherwise GDScript is the smoother default.

## Versioning

- **Godot 4.x** (current as of writing). 4.3, 4.4, 4.5 are the recent stable lines.
- **Godot 3.x** is a separate codebase, still maintained for legacy. Don't start a new project there.
- Engine binary is ~100 MB; portable, no installer required.

## The mental model

Godot is a **scene-of-nodes engine**:

- Everything in the world is a **Node**. There are dozens of node types: `Sprite2D`, `RigidBody3D`, `Camera3D`, `Label`, `Timer`, `AnimationPlayer`, etc.
- A **Scene** is a tree of nodes saved as a `.tscn` file. The root is one node; children are its descendants.
- A scene can **instance** another scene as a child — that's how you compose. A `Player.tscn` can be instanced inside a `Level.tscn`.
- Nodes communicate via **signals** (Godot's built-in event system) and via direct method calls along the scene tree.
- Each node's behavior is defined by its **script**, attached to that node.

Compared to Unity: Godot's "node *is* the component" — there's no GameObject + Components distinction. A `RigidBody3D` *is* a node; it has built-in physics behavior. You add capability by adding child nodes (`CollisionShape3D` as a child of the body) or attaching a script to extend behavior.

This makes Godot scenes more *tree-shaped* than Unity scenes, but less component-flexible. Both work; pick based on which mental model fits how you decompose problems.
