# Blender — 12-Week Practice Schedule

Designed for **20 minutes daily, 5 days a week**. Skip weekends without guilt — the spacing helps consolidation. Mark off each day; honest tracking is the point.

!!! tip "How to use this page"
    Don't try to do every checkbox. The schedule is a *floor*, not a ceiling. If you only get 3 of 5 days in a week, log it in the journal and move on.

---

## Week 1 — Modal navigation and selection

- [ ] Day 1: [Quickstart](./quickstart.md) (30 min one-time investment)
- [ ] Day 2: Practice `G/R/S` + axis lock (`X/Y/Z`) on 3 different primitives
- [ ] Day 3: Selection drills — `A` / `Alt+A` / `B` (box) / `C` (circle) / `Alt+click` (loop)
- [ ] Day 4: Add 5 different primitives via `Shift+A`; rename each in the Outliner
- [ ] Day 5: Save/load drill — save 3 different `.blend` files in 3 folders; reopen each

## Week 2 — Edit Mode fundamentals

- [ ] Day 1: Loop cuts (`Ctrl+R`), inset (`I`), extrude (`E`) on a cube
- [ ] Day 2: Bevel (`Ctrl+B`) — try with 1, 3, 6 segments
- [ ] Day 3: Knife (`K`), merge by distance, fill (`F`)
- [ ] Day 4: Recalculate normals (`Shift+N`); spot-check with backface culling on
- [ ] Day 5: Shade Smooth vs Flat; auto-smooth angle setting

## Week 3 — Modifiers (non-destructive)

- [ ] Day 1: Subdivision Surface — viewport vs. render levels
- [ ] Day 2: Mirror — symmetric primitive modeling
- [ ] Day 3: Array — duplicate along an axis or curve
- [ ] Day 4: Solidify — give a flat plane thickness
- [ ] Day 5: Boolean (Exact mode) — union and difference

## Week 4 — Project: low-poly stylized prop

- [ ] Day 1: Pick reference (one object: chair, mug, lamp); collect 3 photos
- [ ] Day 2: Blockout with primitives + transforms (no Edit Mode yet)
- [ ] Day 3: Convert blockout to Edit Mode; add loop cuts where form turns
- [ ] Day 4: Bevel sharp edges; apply Subsurf
- [ ] Day 5: Render in EEVEE Next; save preview PNG; **journal the result**

## Week 5 — Materials and the Shader Editor (intro)

- [ ] Day 1: Read [Shader Usage](../blender-shaders-and-nodes/usage.md)
- [ ] Day 2: Build a Principled BSDF with base color, roughness, metallic
- [ ] Day 3: Add an Image Texture; connect via Texture Coordinate + UV
- [ ] Day 4: Add a Noise Texture → ColorRamp → Base Color
- [ ] Day 5: Make a node group from your noise + ramp; expose Scale and Color inputs

## Week 6 — UV unwrapping

- [ ] Day 1: Mark seams on a cube; unwrap (`U`); inspect in UV Editor
- [ ] Day 2: Unwrap a UV sphere — try Smart UV Project as comparison
- [ ] Day 3: Unwrap your Week-4 prop; check stretch overlay
- [ ] Day 4: Pack islands; export UV layout PNG
- [ ] Day 5: Apply image texture using your unwrap (PNG with checker pattern from texturecan.com or similar)

## Week 7 — Topology focus

- [ ] Day 1: Read [Topology](./topology.md) end-to-end; print or PDF for reference
- [ ] Day 2: Model an ear from photo reference, all quads, < 500 verts
- [ ] Day 3: Model a hand blockout, focusing on knuckle/wrist edge loops
- [ ] Day 4: Model a face blockout, eye + mouth loops only (very rough)
- [ ] Day 5: Apply Subsurf to each above; spot pinches; identify each pole; **journal the lessons**

## Week 8 — Sculpting (intro)

- [ ] Day 1: Sphere → Sculpt Mode; brush tour (Draw, Grab, Smooth, Crease, Pinch)
- [ ] Day 2: Dyntopo on; rough out a creature head in 20 min
- [ ] Day 3: Multires modifier on a low-poly base; subdivide 2 levels; add details
- [ ] Day 4: Mask painting; symmetry; alphas (skin pore, scratch)
- [ ] Day 5: Decimate output to manageable poly count; export OBJ

## Week 9 — Lighting and rendering

- [ ] Day 1: 3-point lighting setup (key, fill, rim) in Cycles
- [ ] Day 2: HDRI lighting via World Environment Texture
- [ ] Day 3: EEVEE Next vs Cycles A/B comparison on the same scene
- [ ] Day 4: Render passes (diffuse, glossy, normal, depth); export multilayer EXR
- [ ] Day 5: Compositing — color balance, vignette, grain on a render

## Week 10 — Geometry Nodes (first system)

- [ ] Day 1: Read [Tutorial Level 4 Geometry Nodes](../blender-shaders-and-nodes/tutorial.md#level-4--geometry-nodes-for-procedural-assets)
- [ ] Day 2: Distribute Points on Faces → Instance on Points (cube on a plane)
- [ ] Day 3: Random rotation + scale per instance via Random Value
- [ ] Day 4: Replace cube with collection of 3 rock meshes; Pick Instance on
- [ ] Day 5: Expose density, scale range, seed as group inputs; **make it a reusable group**

## Week 11 — Rigging and animation (intro)

- [ ] Day 1: Add Armature; extrude bones to match a simple character; name with `.L`/`.R`
- [ ] Day 2: Parent mesh with automatic weights; check in Pose Mode
- [ ] Day 3: Weight paint fixes — wrist, shoulder, hip
- [ ] Day 4: Keyframe a 2-second animation; review F-curves in Graph Editor
- [ ] Day 5: Render preview animation as MP4

## Week 12 — Project: ship something

- [ ] Day 1: Decide what to ship — a prop set, a procedural environment, a character bust
- [ ] Day 2–4: Build it. End-to-end. No new tutorials this week
- [ ] Day 5: Publish — render, upload to ArtStation/sketchfab/personal site, or just save to a portfolio folder; **journal what you'd do differently**

---

## After Week 12 — what to do next

- Decide your next quarter focus (refer to [now.md](../now.md)). Possible directions:
  - **Hard surface specialization** — Hard Ops, weighted normals, baking workflows.
  - **Character pipeline** — sculpt → retopo → rig → animate → game export.
  - **Procedural environments** — deeper Geometry Nodes + World Building.
  - **Technical art** — shaders + node programming (see [Blender Shaders & Nodes](../blender-shaders-and-nodes/practice-schedule.md)).
- Update `now.md` with your Q3 deliverable.
- Spend 30 min reviewing your journal for patterns. Improvements are usually visible at this scale.
