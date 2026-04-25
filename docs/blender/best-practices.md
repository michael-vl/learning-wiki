# Best Practices — Blender

## File hygiene

- **Name everything.** `Cube.001` is a bug. Rename in the Outliner immediately (double-click or F2).
- **One project, one master file.** Reference other files via `File > Link`; never copy-paste objects between files at production scale.
- **Save incrementally.** `Ctrl+Alt+S` in File menu → *Save As Incremental*. Scripts can break; undo doesn't persist across sessions.
- **Pack external data** before sending a file (`File > External Data > Pack Resources`), unless you're sharing a folder with textures alongside.

## Units and scale

- Set scene units in Scene Properties before starting. Default is meters — fine for most work. Change it if you're doing archviz (cm), miniatures (mm), or astronomy (km).
- **Always apply scale** (Ctrl+A > Scale) before rigging, exporting, or applying modifiers that depend on world-space size (bevel width, solidify thickness, physics).
- A chair should be a chair-height tall in the viewport. Resist the urge to model at "some size" and scale later — many modifiers misbehave at non-unit scale.

## Organization

- **Collections** are your folders. Use nested collections: `Scene / Characters / Hero / Mesh`, `Scene / Characters / Hero / Rig`, etc.
- **One collection per asset category.** Lights in their own collection; cameras in theirs; props grouped thematically.
- Toggle collection visibility (eye icon) to isolate while working. Toggle render visibility (camera icon) to exclude from renders.
- Use **Viewport Display > Color** to color-code collections. Visual at a glance.

## Modeling habits

- **Model symmetric things symmetrically.** Mirror modifier on during modeling; apply only when you need to break symmetry.
- **Turn on the statistics overlay** (Viewport Overlays > Statistics) so you see vertex/face counts. "How heavy is this?" is a question you should answer without guessing.
- **Quad-check often.** `Select > All by Trait > Faces by Sides > 3` then `4` then `5+` — pass through your mesh to spot non-quads.
- **Recalculate normals** (Shift+N) before exporting. Inverted normals cause shading bugs that you won't see in Blender but will in every engine.
- **Merge by distance** (`M > By Distance`) before finalizing. Duplicate vertices cause seams, weight painting bugs, export issues.

## Modifier stack conventions

A typical modifier stack order, top to bottom:
1. **Generate** (Mirror, Array, Screw, Solidify) — creates geometry.
2. **Deform** (Bend, Lattice, Shrinkwrap) — moves existing geometry.
3. **Subdivision Surface** — smooths.
4. **Bevel** — rounds edges.
5. **Armature** — for deforming rigs; always last or near-last.

Subsurf before Bevel gives softer bevels; Bevel before Subsurf gives sharper control. Both are valid — pick consciously.

**Apply modifiers** only when:
- Exporting to a format that doesn't support them.
- You need to bake a specific state for further modeling.
- You're certain you won't need to undo.

## Sculpting habits

- **Work on a symmetrized mesh** (X-axis mirror on) until you need asymmetry.
- Start with **Dyntopo** for blockouts, switch to **Multires** for stable detail passes.
- **Often use Smooth** (Shift while any brush is active). Good sculpture is a rhythm of adding and smoothing.
- **Mask areas you're not working on** (M with a brush, Ctrl+I to invert). Prevents drift on finished zones.
- Sculpt at a **light** viewport color with **neutral matcap**; harsh matcaps lie.

## UV habits

- **Seams go in hidden or natural boundaries.** Not on the surface of the hero silhouette.
- **Pack islands with 2–4px padding** (in UV editor's pack settings) to avoid texture bleeding on low-mip levels.
- **Check stretch** with the overlay. Fix stretched areas by adding seams to relieve.
- **Name UV maps** when you have more than one: `UVMap_main`, `UVMap_lightmap`, etc.

## Texturing and materials

- Follow [Best Practices — Shaders](../blender-shaders-and-nodes/best-practices.md).
- One rule worth repeating: **Non-Color data for non-color textures** (roughness, normal, displacement, masks). This is the single most common beginner bug.

## Rigging habits

- **Name bones with `.L` / `.R` suffixes.** Enables X-axis mirror in rigging tools and weight painting.
- **Use bone layers** to hide deform bones while posing.
- **Add a root bone at origin.** All other bones as children. You'll thank yourself when you need to move the whole rig.
- **Test weights in Pose Mode** *before* calling a rig done. Rotate each joint to its limits; look for pinches; fix with weight painting.
- **Use Rigify** (built-in add-on) for humanoid rigs unless you have a reason not to. Custom rigs eat weeks of time better spent elsewhere.

## Animation habits

- Set your **frame rate early** (24, 30, or 60). Changing mid-project resamples curves and usually ruins them.
- **Animate at the dope sheet first, the graph editor second.** Block poses (stepped interpolation) before splining.
- Use **Auto Keying** *only* when you know what you're doing. It will create keyframes you didn't want.
- **Organize the NLA** (Non-Linear Animation) editor for reusable actions. Walk cycles, idles, one-shots — each as a named strip.

## Rendering habits

- **Render regions** (`Ctrl+B` in viewport, then the Render Region checkbox) for fast iteration. Full-frame only for finals.
- Start with **low samples + denoising** to judge lighting. Crank samples only for final.
- **Save as EXR** for anything you might color-grade. PNG/JPG only for previews.
- **Use multi-layer EXR** if you want to do compositing later: includes all render passes in one file.

## Performance

- **Collapse Subsurf viewport levels** to 1 or 0 while modeling. Bump up for final renders.
- **Disable heavy modifiers in viewport** (camera icon vs. monitor icon on the modifier). Keep render-time computation, skip viewport-time.
- **Simplify settings** (Render Properties > Simplify) let you cap subdivision, particle counts, volume resolution — globally. Great for review renders and draft animations.
- **Instance, don't duplicate.** `Alt+D` gives you a linked duplicate (shared object data); `Shift+D` makes a copy. Use linked for repetitive assets.

## Add-ons worth enabling

Most shipped add-ons are useful. In Preferences > Add-ons:

- **LoopTools** — specialized loop operations (relax, flatten, circle, bridge).
- **Edit Mesh Tools** — face-info, edge-tools utilities.
- **Node Wrangler** — essential for shader/geometry node work. Memorize `Ctrl+T` (add texture chain), `Ctrl+Shift+click` (viewer), `Alt+S` (swap two connected nodes).
- **Copy Attributes Menu** — copy location/rotation/scale/modifiers from one object to another.
- **Rigify** — the default humanoid rig generator.
- **Import/Export format packs** — enable those relevant to your pipeline (FBX is on by default; glTF is bundled and reliable).

Third-party adds worth money (for pros):
- **Hard Ops + Box Cutter** — hard-surface superpowers.
- **RetopoFlow** — retopo productivity.
- **Auto-Rig Pro** — Rigify's more opinionated cousin, with better game-engine export.

## Pitfalls that bite everyone

1. **Unapplied scale** breaking physics, bevels, modifiers. Apply scale.
2. **Flipped normals** causing dark shading. Shift+N to recalculate.
3. **Double vertices** from careless extrusions. Merge by distance.
4. **Modifier stack order** backwards (Armature before Subsurf creates weird collapsing). Armature generally last.
5. **Render engine mismatch** between what you see in the viewport and what renders. Render in the same engine you preview in.
6. **Missing color space** on textures (sRGB for color, Non-Color for data). Check every texture.
7. **Editing linked data without noticing.** A linked material edit changes every object using it. Not always what you want.
8. **Forgetting to pack external data** before sharing. The other person sees pink "missing texture" planes.
9. **Doing everything in one collection** / everything parented to one empty. Pays down in organization forever.

## Production habits that separate hobby from work

- **Name every object the moment you create it.** `empty_cameraTarget`, not `Empty.017`.
- **Every asset has an origin at (0,0,0)** with the asset positioned above the ground plane. Makes linking and alignment sane.
- **Every asset ships with a preview render.** Asset Browser thumbnails set from a consistent lighting setup.
- **Every `.blend` has the render engine and output settings documented in a text data-block** (Scripting workspace → Text Editor). "Cycles 512 spp OIDN, 1920x1080, AgX View Transform."
- **Use version control for projects.** Git-LFS for textures, git for `.blend` if you can swing it. Alternatively, a disciplined folder-naming convention: `project_2026-04-24_v12.blend`.

The theme: you're not just making an image; you're making a thing another person — including future you — can work with.
