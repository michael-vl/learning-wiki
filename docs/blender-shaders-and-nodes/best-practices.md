# Best Practices — Blender Shaders & Nodes

## Architecture

### Favor node groups, even for one-shot materials
Even if you never reuse a group, wrapping a logical chunk (*detail noise*, *edge wear*, *color variation*) into a named group:
- turns your graph into a readable block diagram;
- exposes exactly the parameters you want to tweak, hiding the rest;
- lets future-you (or a teammate) edit without being afraid of breaking something internal.

### Don't mix "generator" and "composition" in the same tree
A generator (the math that makes a pattern) and compositor (the thing that decides *where* that pattern applies on the object) have different scales. Group them separately. A generator group outputs a value or color; a compositor group uses masks and mixes. This separation makes both layers reusable.

### Expose the right parameters
Not all inputs are equal. A material has 2–5 parameters an artist cares about — color, roughness, wear amount, scale, maybe an intensity. Everything else should be hidden inside groups with reasonable defaults. If the parameter surface of your top-level material is larger than that, rethink.

## Naming

- Use **kebab or Title Case group names** that describe the output, not the implementation: "Edge Wear" not "Pointiness + Ramp + Multiply".
- Name sockets like function parameters: `color: Base`, `float: Wear Amount (0–1)`, not `Color1`, `Fac`.
- Put the units in the name when ambiguous: `Scale (world units)`, `Rotation (deg)`.
- Use frame labels (`N` panel > Item > Label) on logical subsections of a non-grouped tree. Colored frames = visual sectioning.

## Colors and gamma

- **Always** set `Image Texture > Color Space` correctly:
  - Color/albedo textures → **sRGB**
  - Roughness, metallic, normal, displacement, masks → **Non-Color** (linear)
- Forgetting this is the #1 cause of "my PBR looks wrong." Roughness in sRGB washes out; normal in sRGB produces subtly wrong lighting.
- Use **ACES** or **AgX** as the view transform (Render Properties > Color Management). AgX is default in 4.x and strongly recommended — it preserves highlights and skin tones where the old Filmic clipped.

## Performance

### Cycles
- Noise and Voronoi at high detail are expensive. *Detail > 8* is usually invisible but doubles cost.
- Heavy displacement: use *Adaptive Subdivision* (Experimental feature set) or bake to a displacement map and use a *Subdivision Surface* modifier with a displacement map instead.
- *Subsurface Scattering* is expensive; use *Random Walk* only where it matters (skin, wax), and keep SSS radius realistic — large radii blow up sample counts.

### EEVEE Next
- Use **baked** textures for anything static. A baked 4K diffuse + roughness + normal will outperform any procedural graph.
- Limit *raytracing options* to what you need. Raytraced reflections/refractions are nice but costly.
- Avoid large transparent stacks (multiple alpha-blended layers) — they serialize and break early-z.

### Geometry Nodes
- Keep geometry **instanced** as long as possible. *Realize Instances* should be near the output, not in the middle.
- When debugging: temporarily insert a *Viewer* node with geometry input, switch the viewport overlay to show the viewer, and inspect the Spreadsheet. Never debug Geometry Nodes blind.
- Use *Merge by Distance* cautiously — it's O(n log n) but on millions of points it's still expensive.
- Simulations are slow; avoid for anything that could be a static bake.

## Debugging

- **Viewer node** (Ctrl+Shift+click) is the print statement of Blender. Learn to use it.
- **Isolate**: mute (`M`) or disconnect downstream nodes. Watch one input at a time.
- **Spreadsheet** (for Geometry Nodes): shows every attribute per element. If a field is `NaN` or `inf`, you'll see it here.
- **Compare Cycles vs EEVEE** outputs early. If they diverge, you're using a Cycles-only feature (pointiness, light paths, OSL, true displacement) without a fallback.
- **Watch for infinite loops in Simulation Zones.** Simulation state accumulates — if you see exponential growth in point count, the zone is spawning without bound.

## Assets and libraries

- Organize a personal **Asset Library**: a single folder with `.blend` files you've marked assets inside. Set it in Preferences > File Paths > Asset Libraries.
- Tag materials consistently: `pbr`, `stylized`, `sci-fi`, `nature`, etc.
- Render thumbnails at a consistent angle and lighting. The asset browser's `Render Preview` button is fine, but a bespoke `_preview.blend` with your reference scene is more professional.
- Mark node groups as assets too — not just materials. A *FBM Noise with Warping* group is infinitely reusable.

## Versioning and sharing

- Save incrementally (`Ctrl+Alt+S` in File menu saves `file_001.blend`, `file_002.blend`, ...). Blender doesn't undo across sessions.
- When sharing a `.blend`, use *File > External Data > Pack All Into .blend*. Otherwise, textures break on other machines.
- For team workflows, use **linked libraries**: *File > Link* pulls a material/object from another file by reference; update the source and all linked files see the change.

## Pitfalls that bite everyone

1. **Black shader** → missing connection to `Material Output > Surface`, or the material isn't assigned to any face (check Material Properties > Slot).
2. **Wrong color space** → see above; it's always this.
3. **Displacement invisible** → Cycles *Experimental* feature set + material's *Settings > Surface > Displacement and Bump* + a subdivision modifier (or Adaptive Subdivision). All three.
4. **Geometry Nodes doing nothing** → you added the modifier but didn't plug Group Input into Group Output with a chain. A blank tree outputs empty geometry.
5. **"Instances don't render in Cycles"** → they do, but *Object Properties > Visibility > Camera* is off, or *Viewport Display > Instancing* is off.
6. **Normal map looks wrong** → always route through a *Normal Map* node (not plugged raw into `Normal`), set color space to Non-Color, and match the tangent space (DirectX vs OpenGL) — Blender expects OpenGL; Substance exports default to DirectX, which flips green.
7. **Procedural texture flickers in animation** → you're using screen-space coords (`Window` or `Camera`) instead of object/generated. Use *Texture Coordinate > Object* for stable procedural textures.

## Habits of strong technical artists

- Think in **masks first**. Most materials are: a base, some variations, and masks that control where variations appear. Design the masks before you design the shaders.
- Every material should answer: *what is the storytelling level?* Hero asset → hand-tuned. Midground → PBR recipe. Background → flat color with vertex AO. Spending equal time on all three is waste.
- Reference real materials. Photograph or find reference for the actual material you're shading. "Wood" is not a material; "old barn oak, east face, 40 years weathered" is.
- Bake when done iterating. Procedural is for iteration; baked is for production.
