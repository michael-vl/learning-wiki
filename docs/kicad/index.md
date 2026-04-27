# KiCad — Beginner to Advanced

!!! tip "If you only do one thing"
    Treat the schematic as the source of truth. Every PCB problem traces back to either a wrong schematic or a missed step in the *schematic → footprint → board* handoff. Don't edit the PCB to "fix" something that should be fixed in the schematic.

!!! warning "Read [Usage](./usage.md) before starting the Tutorial"
    KiCad has its own mental model — projects, libraries, and the schematic-to-PCB pipeline. Skip Usage and you'll get lost in the Footprint Assignment dialog wondering why nothing connects.

A full guide to KiCad as a free, GPL-licensed EDA (Electronic Design Automation) suite. Covers the complete pipeline from schematic capture to fabrication outputs, plus the conceptual side of PCB design — stackups, impedance, manufacturing constraints, and the tradeoffs that don't show up until your first board comes back wrong.

## Scope

- **Schematic capture** — symbols, nets, hierarchical sheets, ERC.
- **Footprint assignment** — symbol/footprint relationships, library tables.
- **PCB layout** — placement, routing, copper zones, design rules.
- **Board setup** — layer stackups, net classes, manufacturer constraints.
- **Custom libraries** — drawing your own symbols, footprints, and 3D models.
- **Fabrication outputs** — Gerbers, drill files, BOM, pick-and-place.
- **PCB design fundamentals** — what a PCB *is* before what KiCad does with one.

## Sections

1. [Quickstart](./quickstart.md) — install, open, blink an LED schematic in 30 minutes
2. [Usage](./usage.md) — the four editors, libraries, projects, essential shortcuts
3. [Tutorial](./tutorial.md) — Level 1 (LED + resistor) → Level 5 (multi-layer mixed-signal board)
4. [Practice Schedule](./practice-schedule.md) — daily / weekly cadence to actually finish a board
5. [Examples](./examples.md) — concrete projects at each level
6. [Best Practices](./best-practices.md) — conventions, manufacturing pitfalls, DFM habits
7. [Learning](./learning.md) — curated resources

## The single most important mental model

KiCad is a **pipeline**, not an editor.

The pipeline is: **Schematic → Footprint Assignment → PCB Layout → Fabrication Outputs.** Each stage takes the previous stage as input. Forward annotation pushes schematic changes into the PCB; back annotation pushes PCB-side cleanups (like swapped pin numbers) back to the schematic.

- *Symbols* live in the schematic and represent electrical behavior.
- *Footprints* live on the PCB and represent the physical pad geometry.
- A *symbol → footprint* link is what turns a wire into a copper trace.

Most beginner confusion ("I drew a connection but DRC says nothing's connected") is a broken link in this pipeline — usually an unannotated symbol, a missing footprint assignment, or a forgotten *Update PCB from Schematic*.

The PCB editor is not a drawing program. It's a **physical realization of the schematic netlist**. Treat it that way.
