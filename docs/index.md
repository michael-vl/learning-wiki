# Learning Wiki

A personal wiki covering creative and game-dev software. Each topic is organized into five sections:

- **usage** — interface, core concepts, how to actually drive the software day-to-day
- **tutorial** — a beginner → advanced path with concrete steps
- **examples** — worked examples and recipes
- **best-practices** — conventions, pitfalls, what professionals do differently
- **learning** — curated resources (books, channels, courses, communities)

## Topics

### 3D / Technical Art
- [Blender — Shaders & Node Programming](./blender-shaders-and-nodes/)
- [Blender — Beginner to Advanced (with Topology)](./blender/)

### Game Engines
- [Unity — Beginner to Advanced](./unity/)
- [Godot — Beginner to Advanced](./godot/)

## How to use this wiki

- Read top-to-bottom per topic, or jump to the section you need.
- Every tutorial section is structured in **Levels** (1 = beginner, 5 = advanced). Don't skip ahead unless you already have the prerequisite reps.
- Examples are intentionally small and self-contained — rebuild them yourself rather than copying.
- The *learning* page of each topic is a shortlist, not a dump. Resources are chosen because they teach *thinking*, not just buttons.

## Format

Plain Markdown. Works in any editor, on any OS, forever. If you later want a rendered site, this structure drops straight into [VitePress](https://vitepress.dev), [Starlight](https://starlight.astro.build), or [Quartz](https://quartz.jzhao.xyz) with no restructuring.

## Conventions used in this wiki

- `Ctrl` on Windows/Linux = `Cmd` on macOS unless otherwise noted.
- Blender conventions assume **4.x** (EEVEE Next, modern Geometry Nodes).
- Unity conventions assume **Unity 6 LTS** (URP default, new Input System, UI Toolkit).
- Godot conventions assume **Godot 4.3+** (Forward+ renderer, GDScript 2.0).
- Code blocks use the target language tag (`gdscript`, `csharp`, `glsl`, `python`).
