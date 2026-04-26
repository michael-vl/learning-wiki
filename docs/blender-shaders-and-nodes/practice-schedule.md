# Blender Shaders & Nodes — 12-Week Practice Schedule

20 minutes daily, 5 days a week. Builds on the Blender 12-week schedule; do that first if you're new to Blender.

## Week 1 — Shader Editor basics

- [ ] Day 1: [Quickstart](./quickstart.md)
- [ ] Day 2: Build a 3-color material (base, mid via ColorRamp, accent via Mix)
- [ ] Day 3: Add Image Texture; route via Texture Coordinate (UV vs Generated vs Object)
- [ ] Day 4: Roughness map (Non-Color!) controlling roughness
- [ ] Day 5: Normal map via Normal Map node; verify orientation

## Week 2 — Procedural textures

- [ ] Day 1: Noise Texture deep-dive; Detail and Distortion params
- [ ] Day 2: Voronoi Texture: F1, F2, Distance to Edge — what each does
- [ ] Day 3: Wave Texture; combine with noise via Mix
- [ ] Day 4: Musgrave / FBM-style — stack with Math nodes for warping
- [ ] Day 5: Build a procedural marble or wood; **save as node group**

## Week 3 — Math and masks

- [ ] Day 1: Math node tour: Multiply, Add, Power, Greater Than, Clamp
- [ ] Day 2: ColorRamp as remapper (constant interpolation = threshold)
- [ ] Day 3: Geometry > Pointiness (Cycles only) → ColorRamp → Mix as edge wear mask
- [ ] Day 4: Object Info > Random for per-object color variation
- [ ] Day 5: Vertex paint / Color Attribute → custom mask read in shader

## Week 4 — Project: weathered metal

- [ ] Build the [weathered painted metal](./examples.md#1-weathered-painted-metal) example end-to-end. Don't read; rebuild from memory after first study.

## Week 5 — Geometry Nodes intro

- [ ] Day 1: Read [Tutorial Level 4](./tutorial.md#level-4--geometry-nodes-for-procedural-assets)
- [ ] Day 2: Distribute Points on Faces → Instance on Points
- [ ] Day 3: Random Value → rotation/scale randomization
- [ ] Day 4: Capture Attribute on Point domain
- [ ] Day 5: Named Attribute pass-through to shader

## Week 6 — Geometry Nodes: a small system

- [ ] Build the [scatter rocks system](./tutorial.md#a-minimal-procedural-system-scatter-rocks-on-a-surface). Expose density, seed, scale range as group inputs.

## Week 7 — Fields and domains

- [ ] Day 1: Position field; Set Position with noise displacement
- [ ] Day 2: Domain conversions (Capture, Evaluate on Domain, Interpolate Domain)
- [ ] Day 3: Boolean masking (Capture + Less Than threshold)
- [ ] Day 4: Spline-based scattering — Curve to Points, Curve to Mesh
- [ ] Day 5: Read Spreadsheet editor; debug a field that's wrong

## Week 8 — Project: ivy or vine system

- [ ] Build a parametric ivy system on any mesh, controlled by vertex paint mask. Ship it as a node group.

## Week 9 — Compositor intro

- [ ] Day 1: Render Layers; route into Composite/Viewer
- [ ] Day 2: Color balance (lift/gamma/gain), curves
- [ ] Day 3: Vignette via Mask + multiply
- [ ] Day 4: Glare; bloom on emissive elements
- [ ] Day 5: Cryptomatte for object isolation

## Week 10 — Performance and baking

- [ ] Day 1: Bake material to image (Cycles, Bake type: Combined or Diffuse+Roughness+Normal separately)
- [ ] Day 2: Identify expensive nodes; replace with baked equivalents in EEVEE
- [ ] Day 3: Texture resolution choices; mipmaps
- [ ] Day 4: Light Linking (4.x+) on a complex scene
- [ ] Day 5: Profile a scene; reduce render time by 30% or more

## Week 11 — OSL (optional, Cycles)

- [ ] Day 1: Enable OSL; build the [stripes](./tutorial.md#osl-open-shading-language--cycles-only) shader
- [ ] Day 2: Add a custom uniform input
- [ ] Day 3: Implement a simple distance field (sphere, box) in OSL
- [ ] Day 4: Animate via TIME or input
- [ ] Day 5: Decide: do you need OSL for your work, or is the node language enough?

## Week 12 — Ship a procedural asset

- [ ] Pick: a procedural environment, a tileable material library, or a procedural prop generator (e.g. Geometry-Nodes building generator). Ship + thumbnail + parameter doc. Mark as Asset in Blender's Asset Browser.

---

## After Week 12

- Asset Library expansion — keep adding well-documented node groups.
- Pick a real shading challenge (NPR / cel shading; iridescence; SSS skin; volumetrics) and dedicate 4 weeks.
- Cross-reference [Mental Models](../mental-models.md) #2 (DAGs) — same skills transfer to Unity Shader Graph and Godot VisualShader.
