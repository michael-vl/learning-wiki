# Usage — Blender Shaders & Nodes

## Opening the right editor

Blender's top bar has workspace tabs. The relevant ones:

- **Shading** — 3D Viewport + Shader Editor. Use for materials.
- **Geometry Nodes** — 3D Viewport + Geometry Node Editor. Use for procedural modeling.
- **Compositing** — Compositor view. Use for post-render effects.

You can also split any area manually: right-click the area border → *Vertical Split* / *Horizontal Split*, then change the editor type from the dropdown in the area's header.

## Shader Editor anatomy

- **Header dropdowns** select the context: *Object* (materials on the active object), *World* (environment), *Line Style* (Freestyle).
- The **output node** (`Material Output`) is the root of evaluation. The `Surface` input is what you're building. `Volume` is for in-volume scattering (smoke, fog). `Displacement` is true displacement (Cycles only, with Experimental feature set).
- Nodes are added with `Shift+A`.
- `G` grabs, `X` deletes, `Ctrl+G` groups selected nodes into a reusable group, `Tab` enters/exits a group.
- `Ctrl+Shift+click` on any node routes its output to a temporary viewer via `Material Output` — incredibly useful for debugging graphs.

## Sockets and data types

Socket color = type:

- **Gray** — float (scalar)
- **Purple** — vector (3 floats; position, normal, UV, etc.)
- **Yellow** — color (RGBA; auto-converts to/from vector and float with implicit math)
- **Green** — shader (a BSDF or mix of BSDFs — not a color, *a function*)
- **Light blue** — string (Geometry Nodes)
- **Teal** — geometry (Geometry Nodes)
- **Red-orange** — object, collection, image, material (reference sockets)

Implicit conversions happen automatically when you connect mismatched types. A color → float conversion takes the luminance; a float → color broadcasts to grayscale.

## How a shader is evaluated

Cycles / EEVEE Next shade each visible point on a surface. For that point they:

1. Compute all input values (texture sampling, coordinates, math).
2. Plug into the BSDF mix you've built.
3. Ask the BSDF for a color given the incoming light direction and outgoing view direction.

**Practical consequence:** nodes are evaluated per shading point. Heavy procedural noise is run *every pixel, every frame* in EEVEE and *every sample* in Cycles. Optimize accordingly.

## Geometry Nodes anatomy

- Add a Geometry Nodes modifier to an object, then create/edit a node group inside the Geometry Node Editor.
- The group inputs/outputs appear on the modifier in the N-panel — this is how you expose parameters to the artist driving the object.
- Geometry flows through the **teal socket**. You modify it by chaining nodes like *Set Position*, *Instance on Points*, *Join Geometry*.
- **Fields** are a Geometry Nodes specialty: a socket can carry a *function that evaluates per element* rather than a single value. `Position` is a field — it's a different value per vertex. Fields let one node (e.g. *Set Position*) apply per-element logic without an explicit loop.
- The **Domain** of a field matters: point, edge, face, corner, spline, instance. Use *Capture Attribute* to lock a field's value in a specific domain, and *Evaluate on Domain* / *Interpolate Domain* to change it.

## Compositor anatomy

- Enable *Use Nodes* in the header if starting fresh.
- Input: *Render Layers* (your render) or *Image*. Output: *Composite* (final frame) and *Viewer* (preview).
- Operates on 2D image data — color, vector, and single-channel passes.
- Passes (depth, normal, mist, cryptomatte) are separate outputs of *Render Layers* that you route to fx nodes.

## Useful keyboard shortcuts

| Shortcut          | Action                                                   |
|-------------------|----------------------------------------------------------|
| `Shift+A`         | Add node                                                 |
| `Shift+D`         | Duplicate selected                                       |
| `M`               | Mute selected nodes (pass input through unchanged)       |
| `H`               | Hide/minimize node                                       |
| `F`               | Connect selected nodes by their matching sockets         |
| `Ctrl+G` / `Ctrl+Alt+G` | Make group / Ungroup                               |
| `Tab`             | Enter/exit group                                         |
| `Ctrl+Shift+click`| Attach a viewer (Shader: sets Material Output; Geo: viewer node; Compositor: viewer) |
| `N`               | Toggle sidebar (item properties, node properties)        |
| `Home`            | Frame all nodes                                          |

## Common gotchas

- **"My shader is black."** You probably forgot to plug into the `Surface` input of `Material Output`, or you're in Rendered view but no lights/HDRI exist.
- **"Noise pattern looks wrong in viewport but right in render."** EEVEE Next and Cycles differ for some nodes (especially ones involving raytracing, true displacement, or subsurface). Always spot-check in both.
- **"Geometry Nodes field is flat/wrong."** You're evaluating a field on the wrong domain. *Capture Attribute* on the correct domain (usually point) fixes this.
- **"UVs look stretched."** You're using generated coordinates instead of UVs, or the object hasn't been UV-unwrapped.
