# Blender — Beginner to Advanced

A full-stack guide to Blender as a 3D DCC (digital content creation) application. Covers modeling, sculpting, UV, texturing, rigging, animation, rendering, and — because it's the single most important skill most people skip — **topology**.

## Scope

- Modeling: box modeling, poly modeling, hard-surface, subdiv.
- Sculpting: dynamic topology, multires, brushes, retopology.
- Topology: what it is, why it matters, how to build good topology, how to fix bad topology.
- UV unwrapping and texturing.
- Rigging and weight painting.
- Animation principles and the Graph / Dope Sheet editors.
- Lighting and rendering (EEVEE Next, Cycles).
- Scene organization and pipeline.

Shaders, Geometry Nodes, and the Compositor have their own topic in [Blender — Shaders & Node Programming](../blender-shaders-and-nodes/). This guide links to that where relevant but does not duplicate it.

## Sections

1. [Usage](./usage.md) — interface, data model, workspaces, essential shortcuts
2. [Tutorial](./tutorial.md) — Level 1 (the default cube) → Level 5 (full character pipeline)
3. [Topology](./topology.md) — its own section because it deserves one
4. [Examples](./examples.md) — concrete projects at each level
5. [Best Practices](./best-practices.md) — conventions, pitfalls, production habits
6. [Learning](./learning.md) — curated resources

## The single most important mental model

Blender is **modal** and **data-driven**.

- *Modal* — your tools depend on what mode you're in (Object, Edit, Sculpt, Weight Paint, etc.). Selecting the wrong mode is 80% of beginner confusion.
- *Data-driven* — everything is data: meshes are vertex/edge/face arrays with attributes; materials are node trees; actions are F-Curve collections; modifiers are non-destructive stacks. Once you see this, tools become less magical and more *functions on data*.

The Blender interface is not a canvas; it's a **debugger for a 3D data model**. Treat it that way.
