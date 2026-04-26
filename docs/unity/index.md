# Unity — Beginner to Advanced

!!! tip "If you only do one thing"
    **Finish small games.** Five small finished games > one ambitious unfinished game. Pong, Breakout, a 2D platformer with one level, a small puzzle game — each forces a complete loop (design → code → polish → build → ship). The shipping habit is the curriculum.

!!! warning "Don't start with DOTS or multiplayer"
    Both are advanced topics that will confuse before they help. Ship classic-MonoBehaviour single-player games first.

A guide to **Unity 6 LTS** and current Unity workflows. Unity is a general-purpose game engine and realtime app platform with broad platform reach, a C# scripting model, and a deep but evolving ecosystem.

## Scope

- The Unity Editor (Hierarchy, Scene, Game, Inspector, Project, Console, etc.).
- Scripting in C# with MonoBehaviour, ScriptableObject, and the new Input System.
- The Universal Render Pipeline (URP) and a brief on HDRP.
- 2D and 3D game project structures.
- UI Toolkit (the modern UI), and where uGUI still applies.
- Asset pipeline, Prefabs, Variants, Addressables, and Scene management.
- Physics, animation (Animator + Animation), audio, particles (VFX Graph + Shuriken).
- Building, profiling, and shipping.

## Sections

1. [Usage](./usage.md) — editor anatomy, project structure, MonoBehaviour lifecycle
2. [Tutorial](./tutorial.md) — Level 1 (first scene) → Level 5 (architecture, performance, multiplayer)
3. [Examples](./examples.md) — concrete mini-projects
4. [Best Practices](./best-practices.md) — code, architecture, project organization
5. [Learning](./learning.md) — resources

## Prerequisites

- Comfort with **C#** at the level of: classes, properties, generics, events, LINQ basics, async/await. If you don't have this, run through Microsoft's free C# Learn track first; otherwise Unity-isms get conflated with C#-isms in your mental model.
- A reasonable computer. Unity 6 in URP runs fine on a 5-year-old laptop; HDRP wants a real GPU.

## Versioning sanity

Unity uses LTS (Long Term Support) releases. **As of the current period, target Unity 6 LTS** (released late 2024, with 6.1 / 6.2 patches following) unless you have a specific reason to use 2022 LTS (a legacy project, a frozen plugin). Unity 6 dropped the year-based naming used 2017–2023.

Use **Unity Hub** to install, manage, and switch versions per project. Never edit a project in a version newer than the one created it without backing up first; downgrades are not supported.

## The mental model

Unity is a **component-based scene graph** driven by a **per-frame update loop**:

- A **Scene** contains **GameObjects** in a hierarchy.
- Each GameObject is an empty container with a Transform plus a list of **Components**.
- **Components** are pieces of behavior or data: a MeshRenderer, a Collider, a Rigidbody, a Light, or a custom script (a class that derives from `MonoBehaviour`).
- The engine ticks each MonoBehaviour every frame (`Update()`) and at fixed physics intervals (`FixedUpdate()`).
- **Prefabs** are reusable, instanceable templates — turn a configured GameObject into a Prefab and you can spawn many copies, edit the source to update all instances.
- **ScriptableObjects** are data assets, not GameObjects — for shared config, settings, items, etc.

Once you internalize *"a GameObject is just a list of components, and behavior is the sum of its components,"* most Unity confusion dissolves.
