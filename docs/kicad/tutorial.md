# KiCad — Tutorial

Five levels, each one a complete project. Don't skip levels; each introduces a constraint the next assumes you've internalized. The point is **finished boards**, not pristine ones — every level ends with Gerbers you could send to a fab.

!!! tip "Working rule"
    A board you finished and ordered teaches more than three boards you started and abandoned. If a level feels stuck, route ugly tracks, run DRC, export Gerbers, and *then* iterate.

---

## Level 1 — Blinking LED

**Goal:** end-to-end pipeline on the smallest possible circuit.

**Circuit:** Coin cell → slide switch → resistor → LED → back to coin cell.

**What you'll learn:** the four operations from [Quickstart](./quickstart.md), but for real — with through-hole footprints sized for an actual battery holder you can buy, traces wide enough to be hand-solderable, and a board outline.

**Steps:**

1. Schematic: `BAT_HLD_CR2032`, `SW_SPDT`, `R 470Ω`, `LED`. Wire them. ERC clean.
2. Footprint assignments: real parts you can find on Digi-Key or LCSC. `BatteryHolder_Keystone:BatteryHolder_Keystone_3000_1x12mm` is a real battery holder.
3. PCB: drop a 50 × 25 mm rectangle on the **Edge.Cuts** layer. Place the parts inside.
4. Route 0.4 mm tracks on F.Cu. Two layers is overkill for this — leave B.Cu empty or fill it with a GND zone.
5. DRC clean. Export Gerbers + drill files: `File → Plot`. Send the zip to JLCPCB or PCBWay if you want; their cheap option is ~$5 for 5 boards.

**Stop conditions:** ERC clean, DRC clean, Gerbers exported, 3D viewer looks like a circuit.

---

## Level 2 — Microcontroller dev board

**Goal:** a real digital board with a regulator and a chip.

**Circuit:** USB-C connector → 5V → AMS1117-3.3V LDO regulator → ATtiny85 / ATmega328 / RP2040 (pick one) → status LED + reset button + ICSP/SWD header.

**What you'll learn:**

- **Decoupling caps** — every IC needs 100 nF as close to its power pins as physically possible. This is non-negotiable.
- **Net classes** — make a `Power` class with wider tracks (0.6 mm) and stricter clearance.
- **2-layer routing with a ground pour** — F.Cu for signals, B.Cu as a solid GND plane filled with `Add Filled Zone`.
- **SMD pads** — most modern parts are 0805 or smaller. You'll need to learn to place them by typing exact coordinates.
- **Hierarchical labels** — when the schematic gets > ~30 components, split it into sheets.

**Steps:**

1. Draft the power section first. ERC the partial schematic.
2. Add the MCU. Decoupling caps within 5 mm of every power pin.
3. Programming header on the edge of the board for cable clearance.
4. PCB: place the MCU first (it's the busiest), then everything radiates outward. USB-C goes on a board edge.
5. Route signals on F.Cu, leave B.Cu as a continuous GND pour. Use vias to stitch GND.
6. DRC. Order the board.

**Stop conditions:** the board powers up without smoke when you plug in USB.

---

## Level 3 — Mixed-signal board

**Goal:** stop pretending PCBs are 2D.

**Circuit:** MCU + microphone preamp (op-amp + filter) + audio output (PWM through low-pass) — or any analog block of your choosing. The point is *one analog domain, one digital domain, on the same board*.

**What you'll learn:**

- **Star grounding / split planes / single-point connection** — analog GND and digital GND are the *same net* in KiCad, but you control where they meet on the board. Get this wrong and your audio path picks up MCU clock harmonics.
- **Differential pairs** (skim) — KiCad's tuned routing for things like USB D+/D−, even at low speeds it doesn't hurt to learn.
- **Component placement strategy** — analog parts on one side of the board, digital on the other, single bridge between the GND pours.
- **Net classes for analog vs digital** — different track widths, different clearances.

This is also the level to start using the **Schematic hierarchy**. Make the analog block its own sheet so it's reusable.

**Stop conditions:** the analog signal is recognizable on a scope without obvious 1 MHz hash riding on it.

---

## Level 4 — Multi-layer board (4 layers)

**Goal:** stackup awareness. Most "professional" boards are 4-layer; the cost premium is small (~2× of 2-layer at JLCPCB) and it eliminates an entire class of routing problems.

**Project ideas:** a USB-PD trigger board, a bigger MCU board with an external crystal and a few ICs, an LED matrix driver.

**What you'll learn:**

- **Stackup design** — `Board Setup → Board Stackup → Physical Stackup`. Set the manufacturer's stackup (JLCPCB has fixed 4-layer stackups; you don't pick layer thicknesses, you pick from their menu).
- **Power and GND planes as their own layers** — F.Cu (signals), GND (plane), Power (plane), B.Cu (signals). This is the standard 4-layer recipe and it solves a huge amount of EMI and decoupling weirdness.
- **Vias as a first-class layout tool** — once you have a GND plane, every component drops a via to GND right at its pad. No more "running a GND track halfway across the board."
- **Impedance** — for any high-speed line (USB, HDMI, DDR), trace width is determined by stackup, not by intuition. Use the [Saturn PCB Toolkit](http://saturnpcb.com) or your fab's impedance calculator.

**Stop conditions:** the board works the first time. (At Level 4 it usually does, because power integrity is no longer fighting you.)

---

## Level 5 — Custom symbols, footprints, and a board you'd put in a product

**Goal:** the part you need isn't in the standard library. Make it yourself, correctly.

**What you'll learn:**

- **Symbol Editor**: draw a new schematic symbol from a part datasheet. Pin numbers MUST match the manufacturer's package. Add a description, datasheet URL, and at least one MPN to the symbol fields.
- **Footprint Editor**: lay out pads from the datasheet's "Recommended Land Pattern." This is the most error-prone step in PCB design — get it wrong and the part doesn't fit. Use [IPC-7351](https://en.wikipedia.org/wiki/IPC-7351) recommended land patterns when the datasheet doesn't specify one.
- **3D model linking**: download a STEP file from the manufacturer (or [GrabCAD](https://grabcad.com)) and link it to the footprint so the 3D viewer is accurate.
- **Design for manufacturing (DFM)**: silkscreen polarity marks, designators readable on the assembled board, fiducials if you're going to PCBA, panelization if you're ordering quantity.
- **BOM and pick-and-place files** for assembly: `Tools → Generate Bill of Materials` and `File → Fabrication Outputs → Component Placement`.

**Project idea:** a small product. A dev tool, a USB gadget, a custom keyboard PCB, a sensor board. Something you'd be willing to put in a case and use for a year.

**Stop conditions:** you assemble the board (or pay JLCPCBA to assemble it), it works, and you'd be willing to send the design files to another person without embarrassment.

---

## After Level 5

You're not "done" — but the marginal value of more tutorials is low. Pick a real problem and design a board for it. Topics to dig into when relevant:

- **High-speed routing**: length matching, controlled impedance, return paths.
- **RF**: antenna keep-outs, ground stitching, microstrip vs. CPW.
- **Power supplies**: switcher layout (current loops!), thermal vias, copper area for heat dissipation.
- **Flex / rigid-flex**: when your product needs to bend.
- **Scripting KiCad**: the Python API for batch operations and custom DRC checks.

The [Learning](./learning.md) page has resources for each.
