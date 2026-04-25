# Examples — Blender Shaders & Nodes

Worked node recipes. Each is small enough to rebuild in under 10 minutes. Rebuild, don't copy — the repetition is the point.

---

## 1. Weathered painted metal

**Goal:** paint chipped off around edges, showing metal underneath.

```
Geometry > Pointiness ──┐
                        ColorRamp (crush to sharp mask)
                                     │
                                     │
Paint Color ──┐                      │
              Mix Color ─ Fac ───────┘
Metal Color ──┘             │
                            └── Principled Base Color

Metal Roughness (0.35) ──┐
                         Mix Float ─ Fac ── same ColorRamp output
Paint Roughness (0.6) ───┘             │
                                       └── Principled Roughness

Same Fac ── Principled Metallic (0 = paint, 1 = metal)
```

**Notes:**
- `Geometry > Pointiness` only works in Cycles (EEVEE gets 0). For EEVEE, bake pointiness to vertex color once, then read via *Color Attribute*.
- Crank the ColorRamp into near-constant interpolation for sharp chips, or use *Constant* interpolation with one color stop at 0.7.

---

## 2. Organic cell walls (Voronoi → veins)

**Goal:** biological-looking surface with veins along Voronoi cell borders.

```
Texture Coordinate > Object ── Voronoi Texture (Distance to Edge)
                                         │
                                         ColorRamp (invert, sharpen)
                                         │
                                         Principled Base Color (vein color)
                                 ─ same ── Principled Roughness (0.2 for wet)
                                 ─ same ── Bump (Strength 0.1) ── Principled Normal
```

**Notes:**
- *Distance to Edge* is the mode that gives you the skeleton. Everything else is remapping.
- Route into a Bump node for free geometric detail; don't plug the grayscale directly into Normal.

---

## 3. Magic shield (EEVEE-friendly)

**Goal:** translucent energy shield with fresnel falloff and animated noise.

```
Noise Texture (Scale 5, Detail 4) ──── Mapping (location Z driven by frame)
                                          │
                                          ColorRamp (contrast ramp)
                                          │
                                          Emission (color * strength 5)
                                                    │
Layer Weight > Facing (Blend 0.3) ── Mix Shader ────┤
Transparent BSDF ─────────────────────── Shader A ──┘
                                          │
                                          Material Output

Material settings: Blend Mode = Alpha Blend, Backface Culling off
```

**Notes:**
- Use *Mix Shader* with Facing as factor — at grazing angles you see emission, straight-on you see through.
- `Mapping > Location > Z` with a driver (`frame * 0.01`) scrolls the noise.
- In EEVEE Next: enable *Raytracing* for proper shield-behind-shield blending.

---

## 4. Procedural wood (with grain direction and knots)

```
Texture Coordinate > Object ── Mapping (scale Y huge to stretch noise) ── Noise Texture (3D, Scale 1)
                                                                                   │
                                                                        ColorRamp (3 stops: dark wood, ring, light wood)
                                                                                   │
                                                                        Mix with knot mask (Voronoi Distance to Edge, sparse)
                                                                                   │
                                                                        Principled Base Color
```

**Notes:**
- Stretching noise along one axis gives you rings. Stretching it along two gives grain.
- Knots = Voronoi with very low cell density and a heavy threshold.
- For realism, route a slightly different noise into roughness — wood's roughness varies with grain.

---

## 5. Geometry Nodes: ivy growth on a mesh

**Minimal system** (not full simulation — just a distribution that hugs geometry):

```
Group Input (Geometry)
        │
Distribute Points on Faces (density from a vertex-paint attribute "ivy_mask")
        │
Capture Attribute (Normal, domain: Point)
        │
Points to Curves (sort by XYZ or a noise field → curves)   # optional: skip for just leaves
        │
Instance on Points (leaf mesh from Collection Info)
        │
Align Euler to Vector (captured Normal → Z axis)
        │
Rotate Euler (random twist around Z)
        │
Realize Instances (for export) or keep instanced (for performance)
        │
Group Output
```

**Notes:**
- Vertex-paint a density mask, read it via *Named Attribute > ivy_mask*, feed into Distribute Points density.
- *Align Euler to Vector* with the captured normal makes leaves sit flat against the surface.

---

## 6. Compositor: film grain and vignette

```
Render Layers > Image
        │
Color Balance (lift/gamma/gain) ──┐
                                  Add (Fac 0.05) ──── Noise (Filter node with grain preset, or Texture > Noise Texture via a generated UV)
        │
        Mix (multiply) ──┐
Ellipse Mask (inverted, feathered) ┘
        │
Composite
```

**Notes:**
- Grain: a small-scale grayscale noise added with low factor. If you want *proper* grain, use a premade noise image — procedural looks too clean.
- Vignette: Mask node → feather heavily → multiply with the image. Tune mask position and size.

---

## 7. OSL: Mandelbulb distance-field surface

(Cycles CPU only.)

```osl
shader mandelbulb(
    point P = P,
    int Iterations = 8,
    float Power = 8.0,
    float Bailout = 2.0,
    output float Inside = 0.0,
    output color Col = 0)
{
    point z = P;
    float dr = 1.0;
    float r = 0.0;
    int i;
    for (i = 0; i < Iterations; ++i) {
        r = length(z);
        if (r > Bailout) break;
        float theta = acos(z[2] / r);
        float phi = atan2(z[1], z[0]);
        dr = pow(r, Power - 1) * Power * dr + 1;
        float zr = pow(r, Power);
        theta *= Power;
        phi *= Power;
        z = zr * point(sin(theta) * cos(phi), sin(theta) * sin(phi), cos(theta)) + P;
    }
    Inside = (i == Iterations) ? 1.0 : 0.0;
    Col = color(i / (float)Iterations);
}
```

Drive an emission shader with `Col` and `Inside` to visualize — feed into a Volume Emission with a small density. Works beautifully on a simple cube Volume.

---

## 8. Procedural city block (Geometry Nodes skeleton)

```
Grid (X=10, Y=10, resolution 10x10) → Mesh Island (per face)
                                          │
Scale Elements (random per island 0.5–1.0) → Extrude Mesh (random height per island)
                                          │
Store Named Attribute "building_id" (Random Value per island)
                                          │
Group Output → pass into shader which reads "building_id" for per-building color
```

**Notes:**
- `Mesh Island` is only valid for disconnected islands. Instead, use `Index` per face + careful capture.
- Real approach for a city: scatter points on streets (splines) with *Curve to Points*, then *Instance on Points* with building meshes from a collection, filtered by zone.
