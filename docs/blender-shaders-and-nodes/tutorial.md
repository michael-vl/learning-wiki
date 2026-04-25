# Tutorial — Blender Shaders & Nodes

A five-level path from "my first material" to writing custom OSL and building procedural asset systems. Work sequentially — each level assumes the previous.

---

## Level 1 — Your first PBR material

**Goal:** understand Principled BSDF, texture sampling, and UVs.

1. Add a default cube → open the *Shading* workspace.
2. `New` a material. You should see `Principled BSDF` → `Material Output`.
3. Change **Base Color** to red. Switch viewport shading to *Rendered* (top-right of viewport, or `Z` → Rendered).
4. Now plug a texture. `Shift+A` → *Texture* → *Image Texture*. Open any PNG.
5. Connect `Image Texture` **Color** → Principled **Base Color**. You see the texture, but probably stretched.
6. `Shift+A` → *Input* → *Texture Coordinate*. Connect **UV** → `Image Texture` **Vector**. Now it uses the object's UV map.

**Key takeaway:** a texture doesn't know *where* on the mesh it is. The coordinate chain (Texture Coordinate → Image Texture) is how that information is injected.

## Level 1 — Principled BSDF inputs to understand

| Input          | What it means                                               | Typical value                    |
|----------------|-------------------------------------------------------------|----------------------------------|
| Base Color     | Diffuse albedo                                              | from texture                     |
| Metallic       | 0 = dielectric (wood, plastic, skin), 1 = metal              | 0 or 1, no middle                |
| Roughness      | Microsurface roughness; 0 = mirror, 1 = matte               | from roughness map or 0.3–0.7    |
| IOR            | Index of refraction for dielectrics                         | ~1.45 for most (default is fine) |
| Normal         | Surface normal perturbation                                 | Normal Map node output           |
| Transmission   | Glass/translucent fraction                                  | 0 or 1, no middle                |

> **Why "no middle" for metallic/transmission?** Because in reality a surface is either metal or dielectric (and either opaque or transparent). Values in between exist only as a blend of two distinct materials — which is exactly what a mask/mixed material represents.

---

## Level 2 — Procedural textures and math

**Goal:** stop relying on image textures; build patterns from math.

1. New material. Add *Noise Texture* → `Fac` into Base Color. The output is grayscale (auto-converted from float).
2. Add *ColorRamp* between them: `Shift+A` → *Converter* → *Color Ramp*. Noise `Fac` → ColorRamp `Fac` → Base Color. Now you can remap noise values to a custom gradient — the workhorse of procedural shading.
3. Replace Noise with *Voronoi Texture*, set *Feature* to *Smooth F1*. You get organic cell patterns.
4. Combine two textures: *MixRGB* (or *Mix > Color* in 4.x). One texture is the base, another (run through a ColorRamp → high contrast) is the mask controlling the mix factor.

**Pattern to memorize:** `Procedural Source → Remap (ColorRamp or Math) → Mask/Mix → Shader Input`. Nearly every procedural material follows this.

### Math nodes you'll use constantly
- *Multiply* — scale a value (e.g. scale noise coordinates by 3 for tighter noise).
- *Add* — shift a value.
- *Power* — harden a mask (`^4` or `^8` turns a soft gradient into a sharp edge).
- *Greater Than* — threshold (if you want hard cut-off, though ColorRamp with *Constant* interpolation is often better).
- *Clamp* — force 0–1 range.

---

## Level 3 — Node groups, drivers, and reusable materials

**Goal:** build materials you can reuse and control from a small parameter surface.

1. Take any working material tree. Select the internal nodes (everything except the Principled BSDF or parts you want "outside"). `Ctrl+G` to group.
2. Inside the group, use the **Group Input** node to expose parameters. Drag from an input socket to the Group Input's empty socket to add a new input.
3. Rename group sockets: in the group's N-panel, set names, default values, min/max. The outside node now looks like a function call with named parameters.
4. Nest groups. A material is cleaner when it's `DetailNoise` → `SurfaceWear` → `ColorPalette` → Principled, where each is a group.

### Drivers
- Right-click any socket default value → *Add Driver*. Expression: a Python snippet referencing another property.
- Example: drive roughness by the frame number: `frame / 200`.
- Drivers turn a static node into an animated or cross-object-linked value.

### Asset library
- In 4.x, mark a material as an **asset** via Outliner or the Asset Browser: right-click → *Mark as Asset*. Set a catalog, add a thumbnail, save.
- Assets drop into any future file by drag-and-drop. This is how you build a personal material library.

---

## Level 4 — Geometry Nodes for procedural assets

**Goal:** generate geometry procedurally with parameters, not by sculpting.

### A minimal procedural system: scatter rocks on a surface

1. Add a plane, subdivide it a few times, add a Geometry Nodes modifier, new node tree.
2. *Group Input* (geometry) → *Distribute Points on Faces* (Poisson disk, density 10) → *Instance on Points* → *Realize Instances* (optional) → *Group Output*.
3. Create a collection with 3 rock meshes. Add a *Collection Info* node → `Instances: true` → into *Instance on Points > Instance* with *Pick Instance* on. Each point gets a random rock.
4. Randomize rotation: *Random Value* (Vector, min `-1,-1,-1`, max `1,1,1` × π) → *Instance on Points > Rotation*.
5. Randomize scale: *Random Value* (Float, min 0.5, max 1.5) → *Instance on Points > Scale*.

**Seeds:** the *Random Value* node takes a seed. Expose it as a group input so the artist can reroll. Two random nodes with the same seed produce correlated results — add different constants or feed *Index* into the seed to decorrelate.

### Fields deep-dive

- A field is a **function** — it's not a value until you evaluate it.
- *Set Position* takes a vector field for `Position`. You can wire `Position + noise * Normal` — that's a field expression, evaluated per vertex at modifier time.
- *Capture Attribute* locks a field into geometry with a specific domain. Needed when a downstream node wants a plain value, not a function.
- The *Named Attribute* pair (`Store Named Attribute`, `Named Attribute`) lets you pass data between Geometry Nodes and shaders: store an attribute on the mesh, then read it in the Shader Editor via an *Attribute* node with the same name.

### Simulation zones

- In 4.x, *Simulation Input* / *Simulation Output* bracket a zone whose state carries between frames.
- Use for: growing vines, cloth, boid-like behavior.
- **Caveat:** not fast. Don't put heavy noise inside simulation zones — it re-evaluates per frame.

---

## Level 5 — Advanced: custom BSDFs, OSL, and performance

### OSL (Open Shading Language) — Cycles only

Enable *Open Shading Language* in Render Properties (CPU only). Then in the Shader Editor, add *Script* node → *Internal* → paste:

```osl
shader stripes(
    float Scale = 10.0,
    color A = color(0.1, 0.1, 0.1),
    color B = color(0.9, 0.2, 0.2),
    output color Col = 0)
{
    float u = mod(u * Scale, 1.0);
    Col = (u < 0.5) ? A : B;
}
```

Click the refresh icon. The node now has `Scale`, `A`, `B` inputs and `Col` output.

**When OSL is worth it:**
- A math expression would take 20 nodes and be unreadable.
- You need loops (e.g., raymarching a distance field).
- You want to read textures with custom filtering (OSL gives you `texture()` with derivative control).

**When OSL is *not* worth it:**
- EEVEE — not supported.
- GPU Cycles rendering on most backends — CPU-only restricts you.
- Any shader you want to ship as a node group for other artists.

### Custom BSDFs via mixing

Blender doesn't let you write your own BSDF directly in the Shader Editor, but you can build one by combining existing BSDFs with *Mix Shader* (weight by facing, angle, fresnel, masks):

```
Principled (rough metallic base) ──┐
                                   Mix Shader ── Material Output
Principled (clearcoat) ────────────┘    │
                                 Fresnel (IOR 1.5)
```

### Performance

- **Cycles** samples nodes per-sample — a heavy node tree multiplies cost by spp. Precompute what you can into baked textures.
- **EEVEE Next** runs per-fragment — even worse for heavy math. Move things to baked normal maps and lookup textures.
- **Bake** — in Cycles: Render Properties > Bake. Select a target image texture node in the material, pick a bake type (Combined, Diffuse, Normal, Ambient Occlusion, Emit for arbitrary passes), bake. Ship the texture, throw away the graph.
- **Viewport performance** in Geometry Nodes: *Realize Instances* breaks instancing and explodes memory — avoid unless necessary; prefer keeping instances until Group Output.
- Use the **Spreadsheet editor** to inspect attributes and point counts. If you see millions of points you didn't expect, you have a bug.

### Rendering-side optimizations

- Use **Light Linking** (4.x+) to restrict which lights affect which objects — massively reduces shading work for large scenes.
- Use **Shadow Linking** similarly for shadow casting.
- Use **denoising** (OIDN for Cycles; EEVEE Next has built-in temporal filtering) so you can render with lower sample counts.

---

## What "advanced" actually means

Shipping a node system someone else can drive. That means: readable groups, exposed parameters with sensible defaults and ranges, thumbnails, docs in the description fields, and pre-baked fallbacks for the expensive parts. A 200-node material no one else can modify is not a mastery signal — it's technical debt.
