# Usage — Blender

## Interface orientation

Blender's window is divided into **areas**. Each area can show any editor type (3D Viewport, Outliner, Properties, Shader Editor, etc.). You can:

- **Split** an area: right-click on the border of an area → *Vertical Split* / *Horizontal Split*, then click where to split.
- **Join** two areas: right-click on the shared border → *Join Areas*, click the area to consume.
- **Change editor type**: click the icon at the top-left of any area's header.
- **Maximize** an area: hover, `Ctrl+Space`.
- **Full-screen an area + hide UI**: hover, `Ctrl+Alt+Space`.

**Workspaces** are tab-based layout presets at the top of the window: *Layout, Modeling, Sculpting, UV Editing, Texture Paint, Shading, Animation, Rendering, Compositing, Geometry Nodes, Scripting*. They are saved layouts — switch workspaces, don't rearrange areas manually every time.

## The default scene data model

Open Blender. The `Cube`, `Light`, and `Camera` are **objects** in the current **scene**. The Outliner (top-right) shows this hierarchy.

Each object has:
- A **transform** (location/rotation/scale).
- **Object data** — for a mesh object, that's the vertex/edge/face data. Multiple objects can share the same object data (linked duplicates).
- **Modifiers** — a stack of non-destructive transformations applied to object data at render/display time.
- **Materials** — assigned per-object or per-mesh; each material is a node tree.
- **Constraints** — runtime transform modifiers (follow, track-to, limit, etc.).

**Object ↔ Mesh distinction matters.** "Rename Cube.001 to Head" — which are you renaming, the object or the mesh? The Outliner shows both; the active mode changes which is edited.

## Modes

Tab (or the mode dropdown in the viewport header) switches mode. Each mode reshapes the toolbar and available operations on the selected object.

| Mode              | What you edit                              | Typical use                              |
|-------------------|--------------------------------------------|------------------------------------------|
| Object Mode       | Transforms and object-level settings       | Placing, duplicating, modifying stack    |
| Edit Mode         | Vertices / edges / faces of the active mesh| Modeling                                 |
| Sculpt Mode       | Mesh via brushes                           | Sculpting, dyntopo, multires            |
| Vertex Paint      | Color attributes on vertices               | Baking AO, masking shader inputs         |
| Weight Paint      | Vertex group weights                       | Rigging                                  |
| Texture Paint     | Image textures                             | Hand-painted texturing                   |
| Pose Mode         | Armature bone transforms                   | Posing a rigged character                |

## Essential keyboard shortcuts

These are the non-negotiable shortcuts. Memorize them before doing anything else.

### Viewport navigation
| Shortcut              | Action                                    |
|-----------------------|-------------------------------------------|
| Middle-mouse drag     | Orbit                                     |
| Shift+MMB drag        | Pan                                       |
| Scroll / Ctrl+MMB     | Zoom                                      |
| Numpad 1 / 3 / 7      | Front / Side / Top orthographic           |
| Numpad 5              | Toggle orthographic/perspective           |
| Numpad 0              | Camera view                               |
| Numpad . (period)     | Frame selected                            |
| Home                  | Frame all                                 |
| ` (backtick)          | Viewport navigation pie menu (no numpad)  |

### Selection
| Shortcut              | Action                                    |
|-----------------------|-------------------------------------------|
| LMB                   | Select                                    |
| Shift+LMB             | Add to selection                          |
| A                     | Select all                                |
| Alt+A                 | Deselect all                              |
| B                     | Box select                                |
| C                     | Circle select (paint select)              |
| Alt+LMB (edge/face)   | Loop select                               |
| Ctrl+LMB              | Shortest path select                      |
| L                     | Select linked under cursor                |
| Ctrl+L                | Select all linked                         |

### Transform
| Shortcut              | Action                                    |
|-----------------------|-------------------------------------------|
| G                     | Grab/move                                 |
| R                     | Rotate                                    |
| S                     | Scale                                     |
| G/R/S then X/Y/Z      | Constrain axis                            |
| G/R/S then Shift+X    | Exclude axis (free in Y/Z)                |
| G/R/S then X X        | Constrain to local X                      |
| G/R/S then numeric    | Type exact distance/angle                 |
| Ctrl (while moving)   | Snap increments                           |
| Shift                 | Fine/precise movement                     |

### Edit Mode essentials
| Shortcut              | Action                                    |
|-----------------------|-------------------------------------------|
| 1 / 2 / 3             | Vertex / Edge / Face select mode          |
| E                     | Extrude                                   |
| I                     | Inset                                     |
| F                     | Make face / fill                          |
| J                     | Connect vertex path (cut across face)     |
| K                     | Knife                                     |
| Ctrl+R                | Loop cut                                  |
| Ctrl+B                | Bevel                                     |
| Alt+M                 | Merge menu                                |
| M                     | Merge (also: Move to collection in Object mode) |
| P                     | Separate (to new object)                  |
| Ctrl+J                | Join (Object mode)                        |
| Shift+D               | Duplicate                                 |
| Alt+D                 | Duplicate linked (shared object data)     |

### General
| Shortcut              | Action                                    |
|-----------------------|-------------------------------------------|
| Z                     | Viewport shading pie (Wire/Solid/Material/Rendered) |
| N                     | Toggle sidebar                            |
| T                     | Toggle toolbar                            |
| F3                    | Search all operators (your safety net)    |
| Ctrl+Z / Ctrl+Shift+Z | Undo / Redo                               |
| F9                    | Adjust last operation (huge productivity win) |

## The Properties editor

Right side by default. Tabs from top to bottom:

1. **Render** — engine (Cycles/EEVEE Next/Workbench), samples, denoising.
2. **Output** — resolution, framerate, file paths.
3. **View Layer** — render passes, override groups.
4. **Scene** — units, gravity, keying sets.
5. **World** — environment shader and lighting.
6. **Collection** — selected collection's properties.
7. **Object** — transforms, visibility, display.
8. **Modifiers** (wrench icon) — the modifier stack.
9. **Particles** — old particle system (mostly superseded by Geometry Nodes).
10. **Physics** — cloth, fluid, rigid body, soft body.
11. **Object Constraints** — track-to, follow path, etc.
12. **Object Data** (green, varies by object type) — for mesh: vertex groups, shape keys, UVs, color attributes.
13. **Material** — material slots and shader editor proxy.
14. **Texture** — brushes and modifier textures; mostly a legacy tab now.

## Modifiers

Modifiers are a stack evaluated top → bottom. Common ones:

- **Subdivision Surface** — smooths geometry by Catmull-Clark subdivision. Toggle viewport/render levels separately.
- **Mirror** — mirrors across an axis. Pair with clipping to prevent vertices crossing the midline.
- **Array** — repeats the mesh along an offset or a curve.
- **Solidify** — adds thickness to a flat mesh.
- **Bevel** — runtime bevel, keyable by angle or weight.
- **Boolean** — union / difference / intersect with another mesh. Use *Exact* mode; *Fast* is unreliable.
- **Shrinkwrap** — projects one mesh onto another; essential for retopo.
- **Armature** — binds mesh deformation to a bone rig.
- **Geometry Nodes** — drops you into procedural modeling.

Apply a modifier (Ctrl+A over the modifier) only when you're sure. Applied = destructive.

## File and data management

- `.blend` files are self-contained but can **link** or **append** data from other `.blend` files (`File > Link`, `File > Append`).
- **Linked** data is a reference — changing the source updates here.
- **Appended** data is a copy — independent from the source.
- Use `File > External Data > Pack Resources` before sending a file to someone — otherwise textures won't come along.
- `.blend1`, `.blend2` are automatic backups. Keep them; they've saved countless projects.

## Rendering engines at a glance

| Engine        | Use case                                   | Strengths                       | Weaknesses                         |
|---------------|--------------------------------------------|---------------------------------|------------------------------------|
| EEVEE Next    | Realtime, stylized, viewport lookdev       | Fast; PBR-ish; raytracing opts  | Limited GI, shader parity w/ Cycles|
| Cycles        | Photoreal, production stills/animation     | Path-traced; unbiased           | Slower; needs denoising            |
| Workbench     | Modeling, matcap previews                  | Instant                         | Not a final renderer               |

## Common gotchas

- **"My mesh is inside out."** Enable *Backface Culling* (Viewport Overlays) to spot it; fix with *Mesh > Normals > Recalculate Outside* (`Shift+N`) in Edit Mode.
- **"Scale is 0.5, why?"** You scaled in Object Mode without applying. Apply with `Ctrl+A > Scale`. **Always apply scale** before rigging, physics, or modifier chains that depend on unit size (bevels, solidify thickness).
- **"My modifier isn't doing anything."** You're in Edit Mode and the modifier's *Edit Mode display* toggle is off, or you haven't set required inputs (a target object for Mirror/Shrinkwrap, etc.).
- **"Viewport is laggy."** Collapse heavy subdivision levels; disable modifiers in viewport while modeling; use *Simplify* (Render Properties) for big scenes.
- **"My object vanished."** You hid it (H) or moved it to another collection. Press `Alt+H` to unhide; check the Outliner filter.

## The scripting console

`Scripting` workspace → *Python Console*. Every operator you run shows up in the *Info* area log as Python. Copy it, tweak parameters, run in the console — that's how you automate.

```python
import bpy
for obj in bpy.context.selected_objects:
    obj.scale = (2, 2, 2)
```

This is also the gateway to writing add-ons, but scripting Blender is its own topic.
