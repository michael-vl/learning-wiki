# Examples — Blender

Concrete projects. Each is scoped to produce something finished, not just an exercise. Ordered by level.

---

## Level 1 — The "teapot" of the modern era: a stylized low-poly island

**Why this:** uses primitives, basic transforms, Shade Smooth, a single light setup. Impossible to fail, satisfying to finish.

**Steps:**
1. Add a UV sphere, scale it flat (S, Z, 0.3).
2. Proportional editing on (`O`), pull some vertices up and others down for terrain variation. Pull the top — you get a little hill.
3. Add tree stand-ins: cylinder for trunk, subdivided cone for canopy. `Shift+D` to duplicate, scatter a few.
4. Add a plane below the island, scale it huge, give it a blue material — that's the water.
5. Add a Sun light, rotate for nice shadows. Switch to Rendered view (EEVEE Next).
6. Apply a simple green to the island, brown to the tree trunks, green to canopies, blue to water. Done in Solid+.

**Deliverable:** a single PNG screenshot. Not a "done render" — just proof you can navigate and shape.

---

## Level 2 — A box-modeled sci-fi crate

**Why this:** teaches the whole loop-cut / extrude / inset / bevel vocabulary in one prop.

**Spec:**
- A cube 1m × 1m × 1.5m.
- Edge panels inset 2cm around each large face.
- A front hatch with a handle.
- Bevels on every external edge (2mm).
- PBR-ish material: dark metal base, a subtle wear overlay (use the "Weathered painted metal" example from [blender-shaders-and-nodes/examples.md](../blender-shaders-and-nodes/examples.md#1-weathered-painted-metal)).

**Topology targets:** all quads, two bevel control loops per beveled edge, no n-gons. Under 3k polys unsubdivided.

---

## Level 3 — A subdivision-surface hero prop (antique book)

**Why this:** forces you to control SubSurf with control loops, bevel the leather/spine transitions, UV for a detailed texture.

**Spec:**
- Closed book, 15cm × 22cm.
- Cover, spine, and pages are separate but joined geometry.
- Add enough control loops that the cover has crisp edges and the pages have a subtly wavy top.
- UV unwrap the cover with seams along the spine and around the edges; paint or generate a leather-with-gold-foil texture.
- Render in Cycles with 512 samples + OIDN denoising.

**Topology review:** select edge loops with Alt+click, verify they run the length of the spine cleanly. No tri should appear anywhere on the cover.

---

## Level 4 — A stylized character bust (from sculpt to animatable)

**Why this:** the most compressed end-to-end exercise short of a full character.

**Pipeline:**

1. **Blockout.** Sphere for head, cylinder for neck, rough collar.
2. **Sculpt.** Dyntopo on; rough out proportions with Grab + Draw. Add mouth cut (Snake Hook brush). Get features in: nose, eyes, mouth, ears. Don't polish — blockout-level only.
3. **Retopo.** New mesh, Shrinkwrap modifier targeting the sculpt, Poly Build to lay out quads. Follow the face-topology rules from [topology.md](./topology.md). Target: <2k quads.
4. **Apply Shrinkwrap.** Fix any floating verts.
5. **UV unwrap.** Seams: around the neck at the collar line, behind each ear, along the scalp part line, inside the mouth. Unwrap, pack islands.
6. **Multires modifier** on the retopo mesh, subdivide 3 levels. Use *Reshape* to project the sculpt's detail back onto the high-poly.
7. **Bake normal map** (low retopo receives detail from high multires) — Cycles, bake type: Normal, Selected to Active.
8. **Texture.** Paint base colors in Texture Paint mode. Use the normal bake in the material.
9. **Rig.** Single armature with head bone, neck bone, spine-top bone. Parent with automatic weights.
10. **Animate.** One 4-second head-turn-and-smile. Three keyframes minimum: start pose, mid pose, end pose. Animate by editing F-curves in the Graph Editor.
11. **Render.** Three-point light setup, Cycles, 256 samples, denoising. Output as PNG sequence, ffmpeg-join into an MP4 (or use Blender's MP4 output).

If you finish this, you have shipped a character. Imperfect, but shipped.

---

## Level 5 — A procedural environment system

**Why this:** moves from "make one scene" to "make a system that makes many scenes".

**Spec: a procedural cliffside**
- Base mesh: a subdivided plane, sculpt a rough cliff silhouette in Sculpt mode (Draw, Clay, Crease).
- Geometry Nodes modifier: scatter three rock meshes along the cliff face, masked by the slope (`Normal > Z < 0.5` for "vertical-ish" areas). See [blender-shaders-and-nodes/examples.md](../blender-shaders-and-nodes/examples.md#5-geometry-nodes-ivy-growth-on-a-mesh) for the scatter pattern.
- A second Geometry Nodes pass scatters patches of moss (*tiny planes with alpha-mapped moss texture*) on horizontal-leaning surfaces.
- A third pass distributes pine trees on the flat top of the cliff, aligned to the terrain normal.
- Cliff shader: triplanar (use the `Texture Coordinate > Object` + multi-projection trick, or the built-in *Triplanar* in 4.x) so textures don't stretch on near-vertical faces.
- Lighting: sun + HDRI for sky; volumetric fog with a World volume scatter.

**Deliverable:** a single render. Then *change one parameter* (seed of the scatter) and re-render — prove it's a system.

---

## A "flash-card" list of micro-exercises

Run these as 20-minute warmups on any day you model:

- Model a cup of coffee with a clean handle topology. No booleans.
- Model a ear, quad-only, under 500 verts, 10 minutes.
- Take a photo of any household object (stapler, salt shaker, pair of scissors) and model it from memory without looking at the photo again.
- Create a material that matches a photo of concrete, using only procedural nodes.
- Geometry Nodes: scatter 1,000 instances of a cube on a sphere's surface with orientation aligned to the sphere normal.
- Animate a bouncing ball with squash and stretch, timed to 24fps, 2-second loop.

Warmups build reflexes. Finish-or-don't, the reps are the goal.
