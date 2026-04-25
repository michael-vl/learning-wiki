# Topology — The Discipline Most People Skip

**Topology** is the *structure* of a mesh: how vertices, edges, and faces are arranged, regardless of sculpted shape. Two meshes can look identical and have completely different topologies — and one will animate, subdivide, and texture beautifully while the other will be a nightmare.

This guide is engine-agnostic in principle. The screenshots and shortcuts are Blender, but everything said here applies to Maya, Max, Modo, ZBrush retopo, Houdini, etc.

---

## Why topology matters

1. **Deformation.** Bad topology bunches, pinches, and collapses when bent. Good topology deforms smoothly because its edge loops follow the *direction of deformation*.
2. **Subdivision.** Catmull-Clark subdivision (the thing SubSurf does) assumes quad faces. Tris and n-gons produce artifacts — pinching, wavy silhouettes.
3. **UV and texturing.** Clean topology makes UVs regular, which makes textures painterly and seamless. Chaotic topology makes UVs a jigsaw.
4. **Readability.** A mesh is a document. Someone else (or future you) reads it to understand, modify, rig, or repair. Bad topology is obfuscated code.
5. **Performance.** Overly dense or uneven topology wastes memory and subdivision passes.

---

## The three goals of good topology

### 1. Quads, mostly
- Aim for **>98% quads** in any mesh going to subdivision, rigging, or deformation.
- Tris are acceptable on:
  - Flat surfaces that won't deform (ground, static props).
  - Final game-engine meshes (engines triangulate anyway; control the triangulation explicitly).
- **N-gons** (faces with 5+ sides) are acceptable on large flat surfaces during blockout. They must be removed before subdivision, sculpting, or export to most pipelines.

**Why quads?** Subdivision algorithms are defined on quad grids. Edge loops are only meaningful on quad-dominant meshes. Deformation math (skinning) is smoother across quads.

### 2. Edge flow follows form
- Edge loops should follow the *natural lines of the form*:
  - On a face: around the eyes, around the mouth, along the jawline, along the brow ridge.
  - On a body: around the shoulder (deltoid loop), around the elbow (bend axis), around the hip.
  - On a hard-surface object: along the silhouette, along the bevel lines.
- This isn't arbitrary. Edge loops define **where the mesh can bend** and **where the texture can wrap cleanly**. Put loops where the form bends; put them where the mask needs to follow a seam.

### 3. Poles are placed with intent
A **pole** is a vertex where ≠4 edges meet. Poles are *necessary* — you can't have all-quad topology on a non-flat surface without them (Euler characteristic forbids it). But each pole is a small cost in the subdivision surface — a subtle pinch.

- **5-pole** (E-pole): 5 edges meet. Most common, usually harmless, used to redirect edge flow.
- **3-pole** (N-pole): 3 edges meet. Also common. Creates a "star" that deflects loops.
- **6+ poles**: avoid. These create visible artifacts under subdivision.

**Rules for poles:**
- Hide poles in flat or low-curvature areas.
- Never put a pole on a deformation line (like the eyelid edge or the knee bend).
- Two poles together (3-pole adjacent to 5-pole) is a classic redirect pattern — used to reduce density while staying quad.

---

## The core patterns

### The "redirect" (3-5 pole pair)

To **reduce** edge density (fewer edge loops in a region without killing the flow):

```
Before (4 loops):          After (2 loops):
│ │ │ │                    │       │
│ │ │ │                    │       │
│ │ │ │        →           │──\ /──│
│ │ │ │                     \ X /     ← 5-pole and 3-pole
│ │ │ │                      Y        ← where loops merge
```

This pattern appears in every professional mesh. Learn it, build it from memory.

### The "loop terminator"

To end a loop (without it cutting through the entire mesh):

- Inset the face around the feature, make the inset an edge ring, then pinch the ring to a pole or redirect. Common in bolt details, vents, eyes.

### The "three-to-one"

Three quads meeting at one quad's edge. Clean way to introduce density.

```
┌──┬──┬──┐
│  │  │  │
├──┴──┴──┤
│        │
└────────┘
```

The top edge has three edge segments meeting the one below via a 3-pole and a 5-pole on the next row down.

### The "corner" (L-shape)

Turning 90° in edge flow: a 3-pole on the inside, a 5-pole on the outside, or vice versa. Common at the corner of a square inset.

---

## Topology patterns for the face

The face is the proving ground for topology because *everyone* sees faces and your brain knows when one is wrong.

### Non-negotiable loops
- **Eye loop** (concentric rings around each eye, following the orbital bone).
- **Mouth loop** (concentric rings around the mouth, following the orbicularis oris).
- **Nose loop** (follows the alar crease and the nasolabial fold).
- **Brow / forehead flow** connecting eye loops upward.
- **Jaw / chin flow** connecting mouth loops downward.
- **Ear loop** (insertion ring, so the ear can be welded/detached).

### How the loops meet
- The eye loop meets the brow flow at poles above/below the eye.
- The mouth loop meets the nose loop at poles above the mouth corners.
- The nasolabial fold is a *diagonal edge* from the wing of the nose to the mouth corner — this edge is what lets the cheek crease realistically on smile.

A "good" face mesh is a ballet of these flows. Look at character topology reference (Hippydrome / polygoogle, or the freely available MetaHuman topology) and **trace it with a pen** on a printout. You learn more from tracing than from reading.

---

## Topology for the body

- **Shoulder loop** — one continuous ring around the deltoid. Where shirt sleeves cut.
- **Armpit junction** — handled with a 3-pole under the arm, letting torso and arm loops diverge.
- **Elbow / knee** — at least 3 edge loops across the bend, to allow smooth deformation. More if you want extreme poses.
- **Wrist / ankle** — loop where gloves/shoes separate.
- **Hip / crotch** — classic topology pain point. Standard solution: a single "waist" loop that splits into two "leg" loops at the crotch via a pair of poles (think of the letter Y).

---

## Hard-surface topology

Hard-surface topology is less about loops and more about **control loops for subdivision**.

### The control loop principle
- Subdivision softens edges.
- An edge loop *very close* to an edge makes that edge *stay sharp* after subdivision.
- Two control loops flanking an edge hold it even sharper.
- Distance between control loop and target edge controls the sharpness: closer = sharper.

### The "grease pencil" rule
Before modeling a hard-surface panel, draw it (literally, with a pencil) as a flat layout:
- Where are the panel lines?
- Where are the bevels?
- Where are cutouts?

Each of those features will need a loop or loops. If the layout has ten panels, your mesh needs ten sets of control loops.

### Booleans + weighted normals
- Boolean subtractions leave messy topology (tris, n-gons). Two approaches:
  - **Fix up**: retopologize the boolean region after the fact (slow, precise).
  - **Don't care**: keep the messy topology but add a **Weighted Normal** modifier so the shading reads correctly. Works because hard-surface usually doesn't deform.
- Weighted normals (+ auto smooth / sharpen angle) shade the mesh as if its normals were authored, even when the topology is irregular. This is the secret sauce behind a lot of modern hard-surface work.

---

## Reading a mesh

When you open someone else's model, read topology like you'd read code:

1. **Zoom out, turn on wireframe** (`Z > Wireframe`, or overlays). Look at the overall flow.
2. **Find the poles.** They're where loops originate and die. Do they sit in smart places?
3. **Find the loops.** Alt-click to select an edge loop. Trace where it goes. Does it close on itself or terminate at a pole?
4. **Subdivide in viewport** (Subsurf modifier, set level 1–2). See where the mesh pinches or waves. Those are the topology bugs.
5. **Pose-test or deform-test.** Apply a twist/bend modifier, or rig-test. Bad topology shows as collapsing geometry.

---

## Common topology failures

| Symptom                         | Cause                                          | Fix                                  |
|---------------------------------|------------------------------------------------|--------------------------------------|
| Pinched highlight on flat area  | Pole in wrong place                            | Redirect pole off the highlight      |
| Wavy silhouette on subdiv       | Irregular quads (varying sizes suddenly)       | Even out spacing; add control loops  |
| Elbow collapses on bend         | Not enough cross-loops at the joint            | Add 1–2 more loops across the bend   |
| Face smile pinches              | No cheek loop, or loop doesn't follow muscle   | Add cheek loop following zygomatic   |
| UVs stretch ugly in one spot    | Dense topology area but no seam to relieve     | Add a seam along a natural panel line|
| Shading artifacts on hard edges | Bevel too small / missing weighted normals     | Add WN modifier, or widen bevel      |
| "Zippered" quads                | Alternating flip of quad diagonals visible     | Use *Mesh > Clean Up > Fix Shading*  |

---

## Retopology workflow

When you've sculpted a high-poly model and need clean topology for animation/UV/export:

1. **Decimate** the sculpt (Decimate modifier, ratio 0.1–0.3) as a proxy for snapping — or keep the multires base.
2. Create a new mesh object at origin.
3. Add a **Shrinkwrap** modifier targeting the sculpt. Set to "Target Normal Project" for smooth adherence.
4. Model the retopo mesh vertex by vertex using *Poly Build* (in Edit Mode toolbar) or manual extrusion, with snap to face enabled.
5. Follow all topology rules above. This is not a speed exercise — it's where topology is actually *built*.
6. When done, apply the Shrinkwrap and check deformation / UV / subdivision.

Automatic retopo (QuadriFlow, QuadRemesher, ZRemesher) is fast and produces "OK" results. They're:
- **Great** for: static props, backgrounds, drafts.
- **Never** for: hero character faces, animated characters, hero deforming props.

Auto-retopo doesn't know where you *need* loops. Only you do.

---

## Practice

- **Daily reps:** model an ear from reference, quad-only, under 500 verts. Three a week for a month.
- **A face a week:** five minutes, no polish, just the flows. By month three you'll know by feel.
- **Critique your own:** every Friday, open last week's mesh, subdivide, bend, look for artifacts. Name the mistake out loud. Fix it.
- **Study reference:** download the [Hippydrome.com](https://hippydrome.com) face and body topology references. Trace on paper. Feel where the loops go.

**Topology is muscle memory for a 3D artist, the way scales are for a musician.** You don't need to think about it in production if you've drilled it in practice.
