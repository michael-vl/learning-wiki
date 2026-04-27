# KiCad — Learning

Curated. Not exhaustive — just the resources that are actually worth your time, organized by where you are in the learning curve.

## Official documentation

- **[KiCad Getting Started](https://docs.kicad.org/9.0/en/getting_started_in_kicad/getting_started_in_kicad.html)** — official walk-through. The single most underused resource by beginners.
- **[Schematic Editor manual](https://docs.kicad.org/9.0/en/eeschema/eeschema.html)** — reference, not a tutorial. Use as a lookup.
- **[PCB Editor manual](https://docs.kicad.org/9.0/en/pcbnew/pcbnew.html)** — same. The chapter on Board Setup and Stackup is essential before designing 4-layer.
- **[KiCad Forum](https://forum.kicad.info)** — high signal-to-noise. Search before posting; the answer usually exists.

## Video — beginner

- **[Phil's Lab](https://www.youtube.com/@PhilsLab)** — the most coherent KiCad-on-YouTube curriculum. Start with his STM32 board series; it's a masterclass in layout reasoning, not button-pushing.
- **[Robert Feranec](https://www.youtube.com/@RobertFeranec)** — long-form courses, often free. Especially strong on signal integrity and 4-layer.
- **[Digi-Key's KiCad series](https://www.youtube.com/playlist?list=PLEBQazB0HUyR24ckSZ5u05TZHV9khgA1O)** — 9 episodes, official-ish, covers the full pipeline cleanly.

## Video — intermediate / advanced

- **[Shawn Hymel @ Digi-Key](https://www.youtube.com/@ShawnHymel)** — introductions to specific topics (USB, ESP32, debouncing, etc.) with KiCad layouts.
- **[The Signal Path](https://www.youtube.com/@TheSignalPathBlog)** — bench-style RF and high-speed work. Not a KiCad channel, but watching how an EE thinks rewires your design intuition.
- **[Eric Bogatin (lectures, papers)](https://www.beTheSignal.com)** — *the* signal-integrity teacher. Look up his "Rule of Thumb" series.

## Books

- **Phil's Lab — *Hardware Design with KiCad* (2024)** — the only KiCad-specific book worth buying. Tracks his YouTube series.
- **Henry W. Ott — *Electromagnetic Compatibility Engineering*** — the textbook on EMI / grounding. Long, dense, worth it. Read after Tutorial Level 3.
- **Howard Johnson, Martin Graham — *High-Speed Digital Design: A Handbook of Black Magic*** — the classic on signal integrity. Older but the physics doesn't change.
- **Robert Pease — *Troubleshooting Analog Circuits*** — old, charming, and full of the war stories that turn into intuition.
- **Hank Zumbahlen — *Linear Circuit Design Handbook*** — Analog Devices' reference. Free PDF online.

## Datasheets that double as tutorials

When the part you're using has a *Recommended Layout* section, that section IS the tutorial. Especially read:

- **Texas Instruments TPS / LM series regulators** — every datasheet has an exemplary layout figure.
- **Analog Devices op-amp datasheets** — gold for analog board layout.
- **Microchip / STM32 reference manuals** — the "minimum design" sections show the ground truth for MCU support circuitry.
- **JLCPCB Capabilities & Stackups** — [jlcpcb.com/capabilities](https://jlcpcb.com/capabilities) — read this before designing for them.

## Tools and references

- **[Saturn PCB Toolkit](http://saturnpcb.com/saturn_pcb_toolkit/)** — free Windows app for impedance, current capacity, via thermal calculations. Old UI, accurate math.
- **[KiCad-StepUp](https://github.com/easyw/kicadStepUpMod)** — FreeCAD workbench for round-tripping mechanical designs.
- **[InteractiveHtmlBom](https://github.com/openscopeproject/InteractiveHtmlBom)** — generates a clickable BOM/board view for assembly. Install as a KiCad plugin.
- **[OctoPart](https://octopart.com)** — multi-distributor part search. Use it for sourcing checks before you commit to a footprint.
- **[GrabCAD](https://grabcad.com)** — free 3D STEP files for nearly every common part.
- **[Component Search Engine (Samacsys / Ultra Librarian)](https://componentsearchengine.com)** — symbols + footprints + 3D models for tens of thousands of parts. Worth signing up.

## Open-source hardware to read

- **[Adafruit on GitHub](https://github.com/adafruit)** — see [Examples](./examples.md).
- **[Sparkfun on GitHub](https://github.com/sparkfun)** — same.
- **[Olimex](https://github.com/OLIMEX)** — industrial-style designs.
- **[Awesome KiCad](https://github.com/mikolajczyk/awesome-kicad)** — curated list of plugins, libraries, and example projects.

## Communities

- **[KiCad Forum](https://forum.kicad.info)** — official, well-moderated.
- **[r/PrintedCircuitBoard](https://www.reddit.com/r/PrintedCircuitBoard/)** — submit your layout for free critique. Frighteningly good feedback.
- **[r/AskElectronics](https://www.reddit.com/r/AskElectronics/)** — for the electrical, not the layout side.
- **EEVblog forum** — older crowd, deep expertise on analog and RF.

## What to skip

- *Eagle-to-KiCad migration tutorials* unless you're literally migrating. They date fast and bias toward Eagle's mental model.
- *AI-generated PCB tutorial sites.* Many exist; nearly all are wrong about subtle things (clearances, stackups, layer-stackup terminology).
- *Random "10 KiCad tips" articles.* Read the official manual sections instead — same content, no ad-tech.

## Where to put your hours

A rough weighting that worked for me:

- 50% — *finishing boards.* Nothing else moves the needle as much.
- 20% — reading datasheets of parts you're using.
- 15% — watching one focused video tutorial per week.
- 10% — reading other people's open-source schematics.
- 5% — fiddling with KiCad settings and plugins.

If your weights look like the inverse of this (i.e., 50% on tools and tweaks), step away from the screen and go solder something.
