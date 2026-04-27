# KiCad — Usage

The orientation guide. Read this *before* the Tutorial. KiCad is four editors stitched together by a project file; once you internalize the data flow, everything else is mechanical.

## The four editors

| Editor | What it edits | File extension |
|---|---|---|
| **Project Manager** | The project (the launcher) | `.kicad_pro` |
| **Schematic Editor** (Eeschema) | Schematics — symbols, wires, nets | `.kicad_sch` |
| **Symbol Editor** | Schematic symbols (libraries) | `.kicad_sym` |
| **PCB Editor** (Pcbnew) | Boards — footprints, tracks, zones | `.kicad_pcb` |
| **Footprint Editor** | PCB footprints (libraries) | `.kicad_mod` (in `.pretty` libs) |

The Project Manager is just a launcher. You'll spend ~40% of your time in the Schematic Editor and ~50% in the PCB Editor; the other two are for making custom parts.

## The pipeline

```
Schematic Editor          PCB Editor
   │                         │
   │   ── Update PCB ───────►│
   │      (forward annot.)   │
   │                         │
   │◄── Update Schematic ────│
   │      (back annot.)      │
   ▼                         ▼
.kicad_sch                .kicad_pcb
```

- *Forward annotation* (`F8` in the PCB editor): "I changed the schematic, push changes to the board."
- *Back annotation*: "I swapped pin numbers on the board (e.g., to make routing cleaner), push that change back to the schematic." Used much more rarely.

## Project anatomy

A KiCad project is a folder. Don't move files individually — move the folder.

```
blink/
├── blink.kicad_pro      # project file (settings, net classes)
├── blink.kicad_sch      # schematic
├── blink.kicad_pcb      # board
├── blink.kicad_prl      # local preferences (gitignore this)
├── sym-lib-table        # project-local symbol libs
├── fp-lib-table         # project-local footprint libs
└── fp-info-cache        # caches (gitignore)
```

For version control, commit `.kicad_pro`, `.kicad_sch`, `.kicad_pcb`, the lib tables, and any `.kicad_sym` / `.pretty/` directories you've added. Ignore `.kicad_prl` and `fp-info-cache`.

## Libraries — the most-confusing concept

There are two libraries: **symbol libs** (for the schematic) and **footprint libs** (for the PCB). Each can be:

- **Global** — installed with KiCad, available in every project. Configured in `Preferences → Manage Symbol/Footprint Libraries → Global`.
- **Project** — only this project. Configured in the same dialog, *Project* tab.

Custom symbols you draw yourself usually go in a **project library** until you decide they're worth promoting to global. Don't pollute your global libs with one-off parts.

A schematic symbol references a footprint by **`Library:Name`** (e.g. `Resistor_THT:R_Axial_DIN0207_L6.3mm_D2.5mm_P10.16mm_Horizontal`). If KiCad can't find that library at the time you open the project, the link breaks. This is the source of 90% of "missing footprint" errors.

## Modes / tools

Both editors are **mode-based** like Blender, but lighter. You're either in *select* mode (default) or you've activated a tool (Wire, Add Symbol, Route Track). `Esc` always returns to select.

## Essential shortcuts

### Schematic Editor

| Key | Action |
|---|---|
| `A` | Add symbol |
| `P` | Add power port |
| `W` | Add wire |
| `K` | End wire |
| `L` | Add label (local net name) |
| `H` | Add global label (cross-sheet net) |
| `M` | Move (no re-route) |
| `G` | Drag (rubber-band wires) |
| `R` | Rotate |
| `F` | Flip |
| `E` | Edit properties |
| `Del` | Delete |
| `Y` | Mirror Y |
| `Ctrl+S` | Save |

### PCB Editor

| Key | Action |
|---|---|
| `X` | Route track |
| `V` | Add via (mid-route) |
| `D` | Drag track (preserves connections) |
| `M` | Move (breaks connections) |
| `B` | Refill all zones |
| `R` | Rotate |
| `F` | Flip to opposite side |
| `T` | Track width / layer popup (mid-route) |
| `+` / `-` | Cycle layers |
| `Alt+3` | 3D Viewer |
| `F8` | Update PCB from Schematic |

The shortcut you'll use most often is **`X` then click**, repeating for every connection. The second is **`B`** to refresh ground/power pours after you move things.

## The Appearance panel (right side, PCB editor)

The right panel controls layer visibility and net highlighting. Things to know:

- The **active layer** is the one you draw on. Click the layer name to make it active.
- Toggle layer visibility with the eye icon. Routing on F.Cu while looking at B.Cu is a common confusion.
- Use **net highlighting** (click on a track or pad with `~` activated, or use the Net inspector) to verify a net goes where you expect.

## ERC and DRC

- **ERC** (Electrical Rules Check) — schematic side. Catches dangling wires, unconnected pins, conflicting drivers (two outputs on one net).
- **DRC** (Design Rules Check) — PCB side. Catches clearance violations, unrouted nets, holes too close to edges.

You should run ERC after every meaningful schematic change and DRC before every fabrication output. There's no "save = check"; you have to run them yourself.

## Where to go next

- [Tutorial](./tutorial.md) — work through Levels 1 → 5.
- [Best Practices](./best-practices.md) — once you've finished Level 1, skim this to internalize the conventions.
