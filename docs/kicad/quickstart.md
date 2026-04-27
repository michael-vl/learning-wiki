# KiCad — Quickstart (30 minutes)

If you have 30 minutes today, do exactly these three things. Don't read the rest of the wiki yet.

!!! tip "If you only do one thing"
    Do step 2. Drawing a schematic and assigning footprints — even on a trivial circuit — is the gate every other KiCad skill is built on.

---

## 1. Install + project + tour (5 min)

- Download KiCad 9.x from [kicad.org/download](https://www.kicad.org/download/).
- Open KiCad. The window you see is the **Project Manager**, not an editor.
- `File → New Project`, name it `blink`, save it somewhere you'll find again.
- Notice the four icons: **Schematic Editor**, **Symbol Editor**, **PCB Editor**, **Footprint Editor**. KiCad is four programs sharing one project.

---

## 2. A schematic with one resistor and one LED (15 min)

This is the smallest complete circuit that exercises the whole pipeline.

- Double-click the schematic file (`blink.kicad_sch`). The Schematic Editor opens.
- Press `A` (Add Symbol). Search `LED`, pick `Device:LED`, click to place it on the sheet.
- Press `A` again. Search `R_Small`, pick `Device:R_Small`, place it next to the LED.
- Press `A` again. Search `Battery`, pick `Device:Battery_Cell`, place it.
- Press `W` (Wire) and connect: battery `+` → resistor → LED anode → LED cathode → battery `-`.
- Press `P` to add power flags if needed (KiCad will warn during ERC otherwise).
- Annotate: `Tools → Annotate Schematic → Annotate`. References go from `R?` to `R1`, etc.
- Footprints: `Tools → Assign Footprints`. Pick something for each symbol — for the LED, `LED_THT:LED_D5.0mm`; for the resistor, `Resistor_THT:R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal`. Don't agonize; you can change them.
- Run ERC: `Inspect → Electrical Rules Checker → Run ERC`. Fix any errors. Most common: missing power flag — add `PWR_FLAG` symbols to your `+` and `-` nets.

You just used the four most important operations: **Add symbol, Wire, Annotate, Assign footprints**. Every schematic extends from these.

---

## 3. Open the PCB editor (10 min)

- Back in the Project Manager, open the PCB Editor.
- `Tools → Update PCB from Schematic` (or press `F8`). Click *Update PCB*. Three footprints fall onto the board.
- Move them around with `M`. Notice the thin white lines — these are the **ratsnest**, showing connections you still need to route.
- Press `X` (Route Track) and click pad-to-pad to draw a copper trace following each ratsnest line. Three traces, you're done.
- `File → Board Setup → Board Stackup` — see the layers. Default is 2-layer (F.Cu and B.Cu). Don't change anything yet.
- Run DRC: `Inspect → Design Rules Checker`. Fix any unrouted nets or clearance violations.
- `View → 3D Viewer` (or `Alt+3`) — admire your two-resistor circuit in 3D. This is the moment KiCad clicks for most people.

---

## What's next

- **Tomorrow (20 min):** read [Usage](./usage.md) — the four editors and how they share data.
- **This week:** [Tutorial Level 1](./tutorial.md#level-1--blinking-led) — the same circuit but with a real switch and a real battery holder, exporting Gerbers at the end.
- **Big picture:** [Best Practices](./best-practices.md) "First-board sanity checks" — ten things to verify before you send anything to a manufacturer.

Set a calendar reminder. PCB design rewards reps over marathons; one finished board teaches more than ten half-finished ones.
