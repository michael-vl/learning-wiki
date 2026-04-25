# Learning — Blender Shaders & Nodes

A short list. Not "everything that exists" — just what's worth your time.

## Official

- **Blender Manual — Shading** section (docs.blender.org). Dry but authoritative. Especially the *Nodes* and *Fields* articles.
- **Blender Manual — Geometry Nodes**. Read *Fields*, *Domains*, and *Simulation Zones* before watching any tutorial. The tutorials assume these concepts.

## Courses and videos

- **Blender Guru — "The Nodevember" series / Procedural material videos.** Andrew Price's earlier material-focused videos (donut aside) are still the best intro for *why* you combine noise + ColorRamp + math.
- **Default Cube (CGMatter)** — weird, fast, deep. Especially good for odd procedural tricks and math-heavy solutions. Expect to pause a lot.
- **Erindale** — *the* Geometry Nodes channel. Long-form, explains fields properly. His *Procedural Worlds* and *Scatter System* series are templates for building real production systems.
- **Bad Normals** — stylized shading and NPR (non-photorealistic rendering) with Blender nodes. Exceptional for cel-shading and toon edge logic.
- **Johnny Matthews / Higgsas** — Geometry Nodes add-ons with open source code; reading them teaches node-graph architecture.

## Books / long reads

- **"The PBR Guide"** by Allegorithmic (free PDF). Not Blender-specific; it explains the *why* of Principled BSDF inputs. Read before you do any PBR material work anywhere.
- **"Physically Based Rendering: From Theory to Implementation"** (Pharr, Jakob, Humphreys) — free online at pbrt.org. Overkill if you just want to make pretty pictures; required reading if you want to *understand* why BSDFs are structured the way they are.

## OSL

- **Open Shading Language — Language Specification** (github.com/AcademySoftwareFoundation/OpenShadingLanguage). The spec is short. Skim it; it's less than a textbook.
- **Larry Gritz's OSL introductory slides** (various SIGGRAPH years) — the origin story and design principles from OSL's creator.

## Procedural content generation

- **"The Book of Shaders"** (thebookofshaders.com) — browser-based shader lessons by Patricio Gonzalez Vivo and Jen Lowe. Teaches GLSL, but everything transfers 1:1 to Blender nodes (noise, SDFs, domain warping, cellular patterns).
- **Inigo Quilez's articles** (iquilezles.org). SDFs, noise functions, domain warping, raymarching. Foundational. Much of it implemented as nodes in *examples.md* of this wiki.

## Asset sources (for reference, not for "done for you")

- **Poly Haven** — CC0 HDRIs, textures, and models. Study their PBR texture sets: open the roughness/normal/displacement maps in an image editor to see what "real" PBR maps look like before assuming your procedural ones are right.
- **ambientCG** — another CC0 PBR source. Same use: study and compare.

## Communities

- **Blender Artists forum** (blenderartists.org). Old-school forum, but "Technical Support" and "Support" sections are where experts actually answer hard questions.
- **r/blender** — help threads are fine for beginner questions; the Friday "weekend challenge" is a great forcing function for practice.
- **Blender Stack Exchange** (blender.stackexchange.com). The top-rated answers are usually high quality. Search before asking.
- **Right-Click Select** (blender.community/c/rightclickselect) — feature request + community-built nodes/scripts.

## Practice structure

If you only have 30 minutes a day:
1. **Week 1–2:** rebuild every material from *examples.md* of this wiki. By hand. No copy-paste.
2. **Week 3–4:** one material a day from a photo reference (Google "old leather", "weathered concrete", "iridescent insect wing"). Constraint: only procedural, no image textures.
3. **Week 5+:** a Geometry Nodes project with a user-facing parameter surface — something *someone else could use.* Ship it to the asset library.

This is an apprenticeship, not a library.
