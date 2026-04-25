# Tutorial — Blender Beginner to Advanced

Five levels. Each is a week-to-a-month of deliberate practice for most people. Don't race.

---

## Level 1 — Navigation, selection, and the default cube

**Goal:** transform, duplicate, and do not panic when you click somewhere weird.

### Do
1. Open Blender. You see the default cube, camera, light.
2. **Orbit** (middle-mouse drag), **pan** (Shift+MMB), **zoom** (scroll).
3. Press `Numpad 1`, `3`, `7` — front, side, top.
4. Select the cube (click). Press `G`, move, click to confirm. `G` then `X`, `15`, Enter — move 15 units on X.
5. `R`, `Z`, `45`, Enter — rotate 45° around Z.
6. `Shift+D` — duplicate. Esc places the copy at original location; left-click to place elsewhere.
7. `Shift+A` — add menu. Add a UV sphere, a cylinder. Move them around.
8. Try `Tab` (Edit Mode). Notice the cube's vertices. `Tab` back. Your first fork in the road.

### Understand
- Blender's pivot for rotate/scale is set by the **Transform Pivot Point** in the header (default: Median Point). Change it when you need to rotate around a cursor or individual origins.
- The **3D cursor** (crosshair with red/white circle) is where new objects appear. Shift+right-click to move it. `Shift+S` menu snaps selection/cursor.

### Don't
- Don't model yet. Level 1 is purely about not being lost in the viewport.

---

## Level 2 — Modeling fundamentals: box modeling a simple prop

**Goal:** build a low-poly sword or chair from a cube.

### Box modeling flow
1. Start with a cube. Tab into Edit Mode.
2. **Loop cut** (`Ctrl+R`, scroll to add multiple cuts) to add topology.
3. **Extrude** (`E`) faces to build form.
4. **Inset** (`I`) to create a sub-face, then extrude it inward/outward.
5. **Bevel** (`Ctrl+B`, scroll for segments) edges for chamfers.
6. Use a **Mirror** modifier for symmetric objects — model one side, mirror the other.

### The chair exercise
1. Start with a cube. Scale to chair proportions.
2. Loop-cut a horizontal and vertical line to split into the seat and back regions.
3. Extrude the back region up.
4. Inset and extrude four legs from the bottom.
5. Bevel all sharp edges 2mm for realism.
6. Add a Subdivision Surface modifier; see how it smooths (probably too much) — you'll learn to control this with topology in Level 3.

### Key idea
Modeling is **adding detail where you want form**. Flat areas don't need topology. Curves and transitions do. This is the seed of topology thinking — see [topology.md](./topology.md).

---

## Level 3 — Topology, subdivision, and clean geometry

**Goal:** build meshes that subdivide cleanly and deform well.

Read [topology.md](./topology.md) in full before doing Level 3 exercises. It's not optional.

### Exercise: the "hard surface vs organic" split

1. Hard surface: model a Sci-Fi crate. All quads, clean 90° corners, bevels for Subsurf control.
2. Organic: block out a humanoid torso in box-modeling. Edge flow along muscle direction (pectoral loop, deltoid loop, rib cage horizontal band).

### Subdivision surface mastery
- Subdivision Surface is Catmull-Clark by default. It smooths aggressively.
- **Creasing** (`Shift+E` on an edge) locally prevents smoothing — but use *weighted edge creases* sparingly. They're a crutch.
- The real answer: **control loops** (edge loops close to the edge you want to stay sharp). Two close loops = sharp; one loop = soft. Plan topology so you add loops where you need sharpness.
- Quad dominant (>98% quads) is the rule. Tris are OK on flat surfaces and game assets. N-gons are OK on flat surfaces *if they're temporary* before final cleanup.

### Retopology intro
Start in Sculpt mode to get form, then retopologize (create new clean geometry on top). Blender's *Poly Build* tool (T panel in Edit Mode) + Shrinkwrap modifier is a workable manual retopo workflow. Add-ons like *RetopoFlow* (paid) speed this up dramatically.

---

## Level 4 — Sculpting, UV, texturing, rigging, animation

This is a big level — you're learning to complete an asset, not just model one.

### Sculpting
1. Enter Sculpt Mode. Brushes are in the left toolbar.
2. Core brushes: **Draw** (add/subtract mass), **Grab** (move), **Smooth** (shift), **Crease** (hard edge), **Inflate**, **Flatten**, **Pinch**.
3. Use **Dyntopo** (top header) for rapid exploration — it adds/removes topology dynamically. Turn it off before doing anything requiring stable topology.
4. Use **Multires modifier** for stable base topology with progressively higher detail levels. This is the production-safe workflow.
5. **Masking** (`M` with a brush) lets you sculpt only where the mask isn't.

### UV unwrapping
1. In Edit Mode, select edges along natural seams (where a texture can visibly split), mark as seam (`Ctrl+E > Mark Seam`).
2. Select all (`A`), unwrap (`U > Unwrap`).
3. Open the UV Editor workspace. See the flattened layout.
4. **Check stretch** (UV editor overlay → Stretch). Red = bad.
5. For hard-surface, unwrap + *Pack Islands* (UV menu) is enough. For organic, seams go in hidden areas (inside the mouth, under arms, scalp part line).

**Shortcut:** *Smart UV Project* is acceptable for non-hero props. It's automatic; quality is decent; don't use it on heroes.

### Texturing
Two main paths:
- **Texture Paint** in Blender directly. Pick a brush, paint on the 3D view or UV layout. Fast, fine for stylized.
- **External:** export the model (FBX/OBJ), texture in Substance Painter or Quixel Mixer, import the resulting PBR set. Production standard.

For a first pass without external tools:
1. Add a new texture image to the material's *Image Texture* node.
2. Texture Paint Mode → start painting. Color, alpha, layers via *Image > New* repeatedly.

### Rigging and weight painting
1. Add an Armature (`Shift+A > Armature`). Extrude bones (`E`) from its root to match your model's skeleton.
2. Name bones with `.L` / `.R` suffixes for symmetry (e.g., `shoulder.L`). Enable *X-Axis Mirror* in pose/edit tools.
3. Parent the mesh to the armature with *Automatic Weights* (`Ctrl+P > Armature Deform > With Automatic Weights`).
4. Enter Weight Paint Mode on the mesh. Fix weights where auto failed (wrist, shoulder, hip — always problems).
5. Pose Mode on the armature lets you test. Add constraints for IK (Inverse Kinematics) on limbs.

### Animation
1. Select an object. Press `I` with the pointer in the viewport — insert keyframe menu. Pick *Location*.
2. Move the timeline forward (bottom). Move the object. `I` again.
3. Scrub the timeline — it interpolates.
4. **Graph Editor** shows F-curves — the animation curves. Learn to edit handles: pull a keyframe's handles to adjust ease-in/ease-out.
5. **Dope Sheet** shows keyframes in time — use to retime, copy/paste, reverse.

**The 12 principles of animation** (Disney, 1981) apply to 3D. Squash/stretch, anticipation, follow-through, overlapping action, arcs, etc. These are not optional; they're what separates "thing moves" from "thing feels alive".

### Putting it together (Level 4 deliverable)
Model → sculpt details → retopo → UV → texture → rig → animate a 4-second idle loop. If you finish this, you are a working 3D generalist at a junior level.

---

## Level 5 — Pipelines, automation, production habits

**Goal:** move from "can make one asset" to "can ship many assets consistently."

### Asset pipelines
- Establish a **file structure** per project: `/textures`, `/models`, `/renders`, `/refs`, master `.blend` and working `.blend` files.
- Use **Collections** religiously. Every object lives in a named collection. Collections can be linked across files.
- **Asset Browser**: mark finalized models, materials, node groups as assets. Build a studio library.
- **Library Override**: link a character rig from its source file, then locally override its pose. This is how studios animate without touching the rig source.

### Automation with Python
- Use `bpy` to batch-rename, batch-export, batch-render.
- Common tasks: export every collection as a separate FBX; apply modifiers on all selected; bake AO/normal for every mesh with an exposed setting.
- The `Text Editor` runs scripts; the `Scripting` workspace has it alongside the console.

### Hard-surface mastery
- Boolean-and-bevel workflow: use booleans (with Exact solver) for complex cuts, bevel + weighted normals for edges. Add-ons: *Hard Ops / Box Cutter*, *Machin3tools*.
- Alternative: Sub-D only, every detail done with control loops. Slower, more controlled.

### Organic character mastery
- Anatomical reference is not optional. Anatomy for Sculptors, Loomis's figure-drawing books, actual écorché models.
- Retopo: manual with Poly Build, or auto with *QuadriFlow* (inside Blender, *Object > Quad Remesher*) for drafts. Auto-retopo is never final for animated characters.
- Shape keys for facial expressions; FACS (Facial Action Coding System) as a driver for realistic face rigs.
- Use a control rig (Rigify add-on, built-in) as a shortcut, or build a custom rig with constraints and drivers.

### Rendering and lookdev

- Set up a neutral lookdev scene: HDRI, gray sphere, chrome sphere, material study sphere. Judge materials here, not in your final scene.
- Cycles denoising: enable *OpenImageDenoise* or *OptiX* (if NVIDIA). Combine with lower sample counts for interactive-speed renders.
- Use **Light Linking** and **Shadow Linking** (4.x+) for art-directed lighting.
- Render passes: output diffuse, glossy, normal, depth as separate passes so you can finesse in the compositor or externally in Nuke/After Effects/Davinci Resolve Fusion.

### Color management

- Scene-referred workflow. View Transform: **AgX** (default in 4.x) or ACES. Never Standard for final renders — you'll crush highlights.
- Save as **OpenEXR (32-bit float)** for later grading. PNG/JPG only for finals.
- When matching a photograph, import the photo as a camera background; color-pick with the eyedropper in a **rendered** viewport (not solid).

### What separates "Level 5" from "Level 4"
You can hand a finished `.blend` to another artist and they can open, find, understand, and modify it. Your file is readable, your names are meaningful, your references are packed, your rigs have user-facing controls, and your render settings are documented. A hero file should read like a well-commented program.

---

## Where to focus if you have limited time

| You care about...          | Focus on                                  |
|----------------------------|-------------------------------------------|
| Environments / archviz     | Modeling, hard-surface, Geometry Nodes, lighting, Cycles |
| Characters                 | Sculpting, topology, UV, rigging, shape keys |
| Motion graphics            | Geometry Nodes, shaders, compositing      |
| Game assets                | Low-poly modeling, UV, baking high→low, texturing in Substance |
| VFX / simulation           | Rigid body / fluid / smoke / Mantaflow simulations, compositing |

Each column is a specialization. Don't try to do all five at once.
