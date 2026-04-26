# Blender — Shaders & Node Programming

!!! tip "If you only do one thing"
    Use the **viewer node** (`Ctrl+Shift+click` on any node) constantly. It's the print-statement of Blender's node editors and the single most useful debugging tool. The same shortcut works in Shader Editor, Geometry Nodes, and Compositor.

!!! warning "Color space"
    Albedo/color textures = **sRGB**; roughness, normal, displacement, masks = **Non-Color**. The single most common beginner bug in PBR shading. Set every texture's color space deliberately.

Node-based material authoring and procedural content in Blender. Covers the **Shader Editor**, **Geometry Nodes**, and **Compositor** — all three share the same node paradigm but operate on different data.

## Scope

- Shader Editor — materials for Cycles / EEVEE Next (PBR, procedural textures, custom BSDFs).
- Geometry Nodes — procedural modeling, scattering, instancing, simulation zones.
- Compositor — post-processing the rendered image.
- OSL (Open Shading Language) — writing custom Cycles shaders in code when nodes aren't enough.

## Sections

1. [Usage](./usage.md) — editors, data flow, node-tree anatomy, basic navigation
2. [Tutorial](./tutorial.md) — Level 1 (first material) → Level 5 (procedural asset systems, OSL)
3. [Examples](./examples.md) — worked node graphs you can rebuild
4. [Best Practices](./best-practices.md) — naming, performance, reusable node groups
5. [Learning](./learning.md) — channels, courses, reference material

## Prerequisites

- Know how to open Blender and select objects. If you don't, start with [Blender — Beginner](../blender/tutorial.md) first.
- A mental model of: **materials are programs that compute a surface's appearance per pixel**. Nodes are the programming language.

## The mental model

Every node tree in Blender is a **directed acyclic graph** evaluated per element:

| Editor          | Per-element means     | Output                        |
|-----------------|-----------------------|-------------------------------|
| Shader Editor   | per shaded point      | BSDF → pixel color            |
| Geometry Nodes  | per vertex/edge/face/point/instance | modified geometry |
| Compositor      | per pixel of final image | final image                |

If you internalize this — "what is 'one' for this editor, and what flows through the sockets" — the rest is learning the node zoo.
