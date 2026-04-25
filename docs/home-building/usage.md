# Usage — Software, Tools, and File Formats

## Design and CAD/BIM software

| Tool                        | Best for                                | License             | Notes                                                       |
|-----------------------------|------------------------------------------|---------------------|-------------------------------------------------------------|
| **Revit** (Autodesk)        | Full BIM, professional residential/commercial | Subscription, expensive | Industry standard for architects/MEP. Steep learning curve. |
| **AutoCAD**                 | 2D drafting                              | Subscription        | Aging but widely accepted; everyone reads `.dwg`            |
| **Chief Architect**         | Residential design (purpose-built)       | One-time + upgrades | Best balance of capability and learnability for homes       |
| **SketchUp Pro**            | Massing, schematic, conceptual           | Subscription        | Easy to start; weak for documentation                        |
| **SketchUp Free** (web)     | Quick concepts                            | Free                | Good for first studies                                       |
| **Sweet Home 3D**           | Floor plans + room layout                | Free, open source   | Limited but instant; good for kitchen/furniture studies     |
| **Home Designer (Suite/Pro)** | Consumer Chief Architect              | One-time            | Same engine, fewer pro features                             |
| **Blender**                 | Visualization, photoreal renders         | Free, open source   | See the Blender topic in this wiki. Not a documentation tool|
| **FreeCAD**                 | Parametric 3D                            | Free, open source   | Mechanical-engineer friendly; not a typical building tool   |
| **QCAD / LibreCAD**         | 2D drafting                              | Free                | Reads/writes `.dxf`/`.dwg`                                   |

**For an owner-builder pursuing this seriously**: Chief Architect (or Home Designer Pro) hits the sweet spot — purpose-built for houses, generates code-checkable drawings, manages a 3D model and 2D documents from one source. If you have engineering background and want full BIM, Revit + Revit MEP is the professional path.

## Structural and engineering tools

- **Forte WEB** (Weyerhaeuser) — free, fast member sizing for joists/beams using engineered wood products. Industry-trusted.
- **WoodWorks Sizer / Shearwalls / Connections** — paid; comprehensive for wood-framed structures.
- **RISA-3D** — general structural; used in residential for unusual conditions.
- **Hilti PROFIS** — anchor design; free.
- **Simpson Strong-Tie SDPWS / SDC** tools — connector and shearwall sizing; free.
- **Manual J / S / D / T** — ACCA load-calculation methodology for HVAC. Tools: WrightSoft (industry standard), CoolCalc (free residential calculator). Required for permit in many jurisdictions.

## Specifications and documentation

- **MasterFormat / UniFormat** (CSI) — standardized specification structure. Even residential benefits from organized specs ("here's the schedule of windows; here's the schedule of doors").
- **Bluebeam Revu** — PDF markup, takeoffs, plan review. Industry standard for the field.
- **PlanGrid / Procore** — construction management; overkill for one house but used widely.

## Cost estimating

- **RSMeans Online** — building cost data by region. The professional reference.
- **Buildertrend / CoConstruct (now CoBuildr)** — owner-builder/GC management software with cost tracking.
- **Excel** — perfectly fine for one project. A good spreadsheet beats poor software every time.

## Local government tools

- **Online permit portals** — your AHJ (Authority Having Jurisdiction) likely has one. Find your jurisdiction's "building department" or "development services."
- **Property record / GIS** — public site for parcel info, zoning, utilities, easements.
- **Code search** — UpCodes (free tier + paid) for state-amended IRC/IBC online.

## File formats you'll touch

| Format    | What it is                       | Tools that read/write                                         |
|-----------|----------------------------------|---------------------------------------------------------------|
| `.dwg`    | Native AutoCAD, the lingua franca | AutoCAD, BricsCAD, DraftSight, QCAD                            |
| `.dxf`    | Open AutoCAD interchange         | Almost all CAD tools                                          |
| `.rvt`    | Native Revit                     | Revit only (others import via IFC)                            |
| `.ifc`    | Open BIM exchange                | Revit, ArchiCAD, FreeCAD, BIMcollab                           |
| `.skp`    | SketchUp                         | SketchUp; Revit imports limited                               |
| `.pdf`    | Final published drawings         | Everything                                                    |
| `.glb`/`.fbx` | 3D model exchange            | Blender, SketchUp, Unity, Unreal                              |

**Always deliver final drawings as PDF.** Working files (`.dwg`, `.rvt`) are versioned, but contractors price from PDFs.

## Drawing types you'll produce or commission

For a building permit set:

1. **Cover sheet** — project info, sheet index, code summary, applicable codes, climate data, design loads.
2. **Site plan** — parcel, building footprint, setbacks, drives, utilities, drainage, grading.
3. **Foundation plan** — footings, stem walls, slab, anchors.
4. **Floor plans** — by level, with dimensions, room labels, door/window tags.
5. **Roof plan** — pitches, framing direction, drains/scuppers/gutters.
6. **Elevations** — N, S, E, W exterior views.
7. **Building sections** — vertical cuts showing floor-to-floor, ceiling, roof assembly.
8. **Wall sections / details** — typical exterior wall, foundation/wall transition, roof eave/rake, parapets.
9. **Schedules** — windows, doors, finishes, fixtures.
10. **Structural plans** — separate set; floor framing, roof framing, shearwall layouts, beam schedule, post schedule, hold-down schedule.
11. **MEP plans** — electrical (load calc, panel schedule, layout), plumbing (DWV, supply, riser), HVAC (Manual J/S/D output, ductwork).
12. **Energy compliance** — REScheck or RES (state energy code) compliance certificate.

For a small home, this is 30–60 sheets. A custom home: 80–150+.

## Site evaluation tools you'll use

- **Survey** by a licensed surveyor — boundary, topography, easements, encroachments. ~$1,500–$5,000.
- **Geotech / soils report** if required — borings, soil bearing, drainage. ~$2,000–$10,000.
- **Tree survey** if treed lot.
- **Title search** — your real estate attorney; identifies recorded easements, restrictions.
- **Zoning verification letter** from the AHJ — what the lot allows.
- **Utilities** — verify availability/cost of water, sewer, gas, electric, internet at the property line.

## Common gotchas (software/process)

- **CAD/BIM file compatibility** — Revit files don't open in older versions; SketchUp updates break old plugins; always archive a PDF and a current native file at each milestone.
- **Drawing scale** — printed at the wrong scale, dimensions don't match. Always title-block scale and graphic scale on every sheet.
- **Round-tripping plans through email** loses metadata, occasionally line weights. Use a transfer service (WeTransfer, Dropbox links) for working files.
- **Survey datum mismatches** — your surveyor's datum may differ from your engineer's; always coordinate elevations early.
- **Energy code compliance** done at the end — you discover you needed thicker walls or better windows after you've designed the envelope. Run REScheck during schematic design.
