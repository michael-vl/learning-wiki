# KiCad — Best Practices

Conventions, manufacturing pitfalls, and habits that pay off across every board you design. Roughly ordered from "applies to Level 1" to "applies once you're doing real products."

## Schematic hygiene

- **One signal name per net.** If you see `LED_DRV` on one wire and `D1_A` on another but they're connected, the schematic lies. Rename until they match.
- **Use power symbols (`PWR_FLAG`, `+3V3`, `GND`) instead of long wires across the sheet.** Wires are for *signals* and short power links. For nets that touch many places, named labels are clearer.
- **Hierarchical sheets** for any block over ~20 components. Power supply, USB, MCU, sensors — each its own sheet.
- **Designators in reading order, top-left to bottom-right.** KiCad's auto-annotate has a setting for this; use it.
- **Add manufacturer part numbers (MPN) and datasheet URLs to symbol fields.** Future-you will thank present-you when generating the BOM.
- **Always run ERC before saving.** A clean ERC is the contract that says "the schematic is sane."

## PCB layout

- **Place before you route.** Spend 60–80% of layout time on placement. Good placement makes routing trivial; bad placement makes routing impossible.
- **Power-flow direction is a real thing.** Connector → fuse/protection → regulator → loads. Lay them out in that order on the board.
- **Decoupling caps within 5 mm of every IC's power pin.** Closer is better. Use the GND plane via right at the cap's pad.
- **Keep analog and digital domains physically apart.** If they share a ground, decide *where* they share it (typically directly under the ADC or DAC).
- **Track widths** — don't use the default for everything. Power: 0.4–1.0 mm depending on current. Signals: 0.15–0.25 mm. Use net classes to encode this.
- **Vias are cheap.** Stitch GND planes liberally.
- **Don't route under crystals.** Keep the area below an oscillator or crystal as solid GND, no signals.
- **45° tracks, not arbitrary angles.** Easier to read, less prone to acid traps in older fab processes.

## Manufacturing — DFM checklist

Before clicking "Plot":

- [ ] Board outline closed and on `Edge.Cuts` only (no other layers, no doubled lines).
- [ ] All silkscreen text ≥ 1.0 mm tall, ≥ 0.15 mm stroke. Smaller is unreadable on most fab processes.
- [ ] No silkscreen *on* pads (move designators if they overlap).
- [ ] All footprints have a clear polarity / pin-1 indicator on silkscreen for assembly.
- [ ] Drill holes ≥ 0.3 mm (most cheap fabs); 0.2 mm costs extra.
- [ ] Annular ring ≥ 0.15 mm. KiCad's default is fine; just confirm.
- [ ] Track-to-edge clearance ≥ 0.3 mm.
- [ ] Mounting holes added, plated or unplated as appropriate.
- [ ] At least one fiducial if you're going to PCBA assembly (three for SMT).
- [ ] Check the **3D viewer** — do connectors clear the board edge? Do tall components clash with each other?
- [ ] Check **DRC with "Test for parity between PCB and schematic" enabled**. This catches the "I changed the schematic but forgot to update the PCB" class of bugs.

## File output conventions

- **Gerbers + drill** — use `Plot` → `Generate Gerbers`, then `Generate Drill Files`. Default settings work for JLCPCB, PCBWay, OSHPark.
- **Filename includes the project version** — `blink-rev2-gerbers.zip`, not `gerbers.zip`. After your fifth board you'll have many `gerbers.zip` files and no idea which is which.
- **Keep a `manufacturing/` folder** in the project with one zip per revision sent. Never overwrite.
- **For assembly (PCBA)** — also export the BOM CSV and the position file (`Component Placement`). JLCPCB has specific format requirements; their docs are good.

## Version control

- **Git, not Dropbox.** KiCad files are text-ish, diffs work surprisingly well for the schematic.
- **Commit before every layout session, even if "nothing changed."** Layout changes are heavy and frequent — diffs of `.kicad_pcb` are noisy but invaluable for "what did I just break?"
- **Tag releases that you ordered.** `git tag rev1-ordered-2026-04-01`. Future you, holding rev3 in your hands, will want to diff against rev1.
- **Do NOT commit `*.kicad_prl`, `fp-info-cache`, `*-backups/`.** Add to `.gitignore`.

## First-board sanity checks

The ten things to verify before you click "Submit Order":

1. **Schematic ERC clean.**
2. **PCB DRC clean** (and check "parity between PCB and schematic").
3. **Power and ground are obviously correct in the 3D viewer** — no battery polarity reversed, no `VCC` accidentally tied to `GND`.
4. **All connectors face outward** so cables can plug in without hitting a tall component.
5. **Polarized parts have polarity marks on silk** (electrolytics, diodes, ICs, LEDs).
6. **Designators readable on the assembled board** — none hidden under a part or off the board edge.
7. **Mounting holes** present and the right size for your enclosure (M2.5 or M3 are common).
8. **Pin 1 of every IC** is unambiguous from the silkscreen.
9. **You spot-checked at least three nets** by clicking pads in the PCB editor and confirming the net name matches the schematic.
10. **A friend looked at it.** Even ten seconds of fresh eyes catches things you've gone blind to.

## Common beginner mistakes

- Forgetting to run *Update PCB from Schematic* after changing the schematic. The board still has the old netlist; DRC won't always catch this.
- Routing on the wrong layer. Look at the active-layer indicator before you press `X`.
- Putting decoupling caps on the *opposite* side of the board from the IC, with vias in between. Defeats the point — keep them on the same side, close to the pin.
- Not realizing the schematic is two pages. Split sheets are great, but check both before declaring ERC clean.
- Ordering the wrong board. *Triple-check the project name in the Plot dialog.*

## Habits worth forming

- **3D viewer pass** before every order. Just rotate the board for 30 seconds.
- **Read one datasheet a week.** Especially the "Recommended PCB Layout" section, which is gold.
- **Open one of your old projects every month.** Half of all design wisdom is "the thing past me did wrong."
- **Annotate the schematic with comments** (text labels) explaining *why* a particular value or topology was chosen. Future you will not remember.
