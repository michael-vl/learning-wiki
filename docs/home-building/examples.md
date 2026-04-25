# Examples — Plan & Detail Studies

Concrete exercises that mirror real design problems. None of these are full plans — they're the *kind* of thinking required at each step.

---

## 1. Programming a 1,800 sf single-family home

```
Occupants: couple + 2 kids + dog. WFH 1–2 days/week.
Climate zone: 4A (mixed, humid).
Lot: 0.25 acre, west-facing front, mature oaks east side.

Spaces (rough sf, with notes):
  Kitchen / dining / living open plan       450 sf  (cooking-heavy; 9' ceilings)
  Primary suite (bed, bath, closet)         350 sf  (king + reading chair; double vanity)
  2 secondary bedrooms                      250 sf  (jack-and-jill bath shared)
  Office / WFH                              120 sf  (door for calls; not a bedroom by code)
  Mudroom / laundry                         80 sf   (bench, hooks, side-by-side W/D)
  Powder bath                               25 sf
  Mechanical / closet                       35 sf   (heat pump indoor, water heater, ERV)
  Circulation, walls                        ~100 sf
                                            ─────
  Total conditioned                         ~1,410 sf
  Garage (unconditioned, attached, 2-car)   400 sf

Performance targets:
  HERS index ≤ 50 (state requires ≤ 60)
  ACH50 ≤ 1.5
  All-electric (no gas service)
  Solar-ready, EV-ready, battery-optional rough-in

Budget envelope:
  Hard costs: 1,410 sf × $300/sf = $423k + garage $50k = ~$475k
  Soft costs (15%): $71k
  Site, foundation premium, contingency: $90k
  TOTAL ENVELOPE: ~$636k
```

This is the document you sign yourself before you draw a thing. It defines success.

---

## 2. Code-summary cover sheet (fragment)

```
PROJECT INFORMATION
  Address:                  123 Example Ln
  APN:                      012-345-67-890
  Zoning:                   R-1 (Single Family Residential)
  Lot area:                 10,890 sf
  Floor area (proposed):    1,810 sf conditioned + 400 sf garage
  Lot coverage:             19% (max 35%)
  Setbacks:                 Front 25' / Sides 5' / Rear 20' (all met)
  Building height:          22'-6" to ridge (max 30')
  Construction type:        V-B (per IBC) — wood frame, unprotected

APPLICABLE CODES
  2021 IRC w/ State Amendments
  2021 IECC w/ State Amendments
  2020 NEC (NFPA 70)
  2021 IPC, IMC (per IRC adoption)
  2021 IFC

DESIGN LOADS (per IRC R301)
  Ground snow:              25 psf
  Wind:                     115 mph (Vult), Exp B
  Seismic:                  Ss = 0.50, S1 = 0.20  → SDC C
  Soil bearing (assumed):   1,500 psf (verify w/ geotech)

ENERGY COMPLIANCE
  REScheck attached. U-factor and SHGC per IECC Table R402.1.2.
  Climate zone 4A. Performance path used.
```

This sheet alone is ~30% of plan check. Get it right.

---

## 3. Wall section — typical 2x6 wall with continuous exterior insulation (CZ 4A)

```
EXTERIOR (outside to inside):
  - Fiber cement lap siding, 7" reveal
  - 1x4 vertical rain-screen battens (creates drainage gap)
  - Self-adhered WRB (water-resistive barrier) — critical air/water layer
  - 1.5" rigid mineral wool continuous insulation (R-6)
  - 1/2" exterior sheathing (OSB or plywood)
  - 2x6 stud wall @ 16" o.c., R-21 mineral wool batts
  - Smart vapor retarder (variable permeance, e.g., MemBrain)
  - 1/2" gypsum board, painted

CALCULATED PERFORMANCE:
  Whole-wall R-value (parallel paths):  ~R-26
  Vapor profile:                          dries to interior in winter; exterior CI keeps stud cavity warm above dew point
  Air barrier:                            primary at WRB; secondary at gypsum/Membrain
  ACH contribution:                       <0.5 ACH50 if detailed properly
```

Detail every penetration: windows, doors, hose bibs, electrical entries. Air leakage isn't fields; it's edges.

---

## 4. HVAC sizing — Manual J / S / D summary

```
House: 1,810 sf, climate zone 4A, oriented south-facing main glazing.
ENVELOPE: as wall section above; R-49 attic; U-0.25 windows; ACH50 = 1.5.

MANUAL J (block load):
  Heating design load:    18,200 BTU/hr  (10°F outdoor design)
  Cooling design load:    14,800 BTU/hr  (sensible) + 2,800 (latent) = 17,600 total
  Latent heat ratio:      ~0.16 (low; envelope is dry-leaning)

MANUAL S (equipment selection):
  Selected: 2-ton (24 kBTU/hr nominal) variable-speed heat pump (Mitsubishi MXZ inverter or equivalent).
    - Heating capacity at 10°F: 22,000 BTU/hr (sized to avoid resistance backup at design)
    - Cooling capacity at 95°F: 23,500 BTU/hr (target oversize ≤ 25% on cooling)
  Backup: 5-kW resistance strip (rare use; below 0°F only)

MANUAL D (duct design):
  Total external static pressure:   0.5 in.w.c.
  Friction rate:                    0.08 in.w.c per 100 ft
  Trunk: 14" round → 12" → 10" reductions
  Branch ducts: 6"-7" round to each register
  Velocity:                         < 700 fpm in trunks, < 600 fpm in branches (for low noise)
  Total estimated duct leakage:     < 4 cfm/100 sf @ 25 Pa (code threshold; aim better)
```

Compare to the contractor rule of thumb that would have you buying a 4-ton system. That oversized unit short-cycles, costs more, has worse humidity control, and uses more energy. The Manual J/S/D process exists to prevent that.

---

## 5. Electrical load calc (NEC Article 220)

For the sample home, all-electric, with EV:

```
Standard service-load calc (NEC 220.83 Method 1):

  Lighting / general (3 VA × sf):       1,810 × 3 =  5,430 VA
  Small appliance (2 × 1,500 VA):                    3,000 VA
  Laundry:                                           1,500 VA
  HVAC (heat pump 24 kBTU @ ~6 kW):                  6,000 VA
  Electric water heater (heat pump):                 1,500 VA
  Range (electric induction):                        8,000 VA
  Dishwasher / disposal:                             1,500 VA
  Dryer (heat pump):                                 1,200 VA
  EV charger (Level 2, 11.5 kW continuous):         11,500 VA × 1.0 (continuous) = 11,500 VA
                                                  ────────
  Subtotal:                                         39,630 VA

Apply demand factors (NEC 220.83):
  First 10 kVA at 100%, remainder at 40%:
    10,000 + (29,630 × 0.40) = 10,000 + 11,852 = 21,852 VA

  Service amps (240V):                21,852 / 240 = 91 A

Conclusion: 200A service is adequate; consider future-proofing to 200A panel with provisions for additional EV / battery.
```

The point is: do the math. "200A is standard, just put one in" works most of the time and bites you the day you add a heat pump pool heater.

---

## 6. Permit submittal sheet count (typical residential)

```
Cover sheet, code summary, sheet index             A0.0
Site plan                                          A1.0
Survey reference                                   A1.1
Foundation plan                                    A2.0
Floor plan(s)                                      A2.1, A2.2
Roof plan                                          A2.3
Reflected ceiling / lighting plan                  A2.4
Exterior elevations (4 views)                      A3.0
Building sections (2-3 cuts)                       A4.0, A4.1
Wall sections / details (typical, atypical)       A5.0, A5.1, A5.2
Window schedule / details                          A6.0
Door schedule / details                            A6.1
Finish schedule                                    A7.0
Specifications notes                               A8.0
Structural cover, gen notes, design criteria       S0.0
Foundation plan (structural)                       S1.0
Floor framing                                      S2.0, S2.1
Roof framing                                       S3.0
Shearwall / lateral plans                          S4.0
Beam / column / hardware schedules                 S5.0
Details                                            S6.x
Electrical: load calc, panel schedule, plan        E1.0–E2.0
Plumbing: DWV, supply, riser                       P1.0–P2.0
Mechanical: Manual J/S/D, plan                     M1.0–M2.0
Energy compliance (REScheck)                       T1.0
                                                  ─────
Approx. sheet count:                              30–45 sheets
```

Smaller jurisdictions accept simpler sets; bigger projects push toward 80+.

---

## 7. Owner-builder bid analysis spreadsheet (excerpt)

| Trade           | Bidder A         | Bidder B          | Bidder C         | Notes                                |
|-----------------|------------------|-------------------|------------------|--------------------------------------|
| Excavation      | $14,200          | $11,800           | $13,500          | B excludes rock removal; A includes  |
| Foundation      | $48,500          | $41,000           | $52,000          | C uses ICF; A/B are stem wall/slab   |
| Framing labor   | $62,000          | $55,000           | $58,000          | Material owner-supplied              |
| Roofing         | $14,500          | $13,200           | $15,800          | Same shingle spec                    |
| Plumbing        | $32,000          | $28,500           | $36,000          | C has 25-yr warranty                 |
| Electrical      | $28,000          | $25,000           | $30,500          | All include 200A panel + 2 EV rough  |
| HVAC            | $24,000          | $19,800           | $27,000          | A and C variable-speed; B single-stg |
| Insulation      | $9,500           | $8,200            | $11,000          | C uses dense-pack cellulose          |
| Drywall         | $18,500          | $16,800           | $17,500          | Spray-textured                       |
| **Subtotal**    | **$251,200**     | **$219,300**      | **$261,300**     |                                      |

Cheapest bid (B) is not always the right pick. Check:
- License/insurance current?
- References for similar-size projects in your area?
- What's *excluded*?
- Schedule fit?
- Quality reputation among other tradesmen?

You usually pick neither the cheapest nor the priciest. Often the middle bid with the best references and clearest scope wins.

---

## 8. Construction schedule (Gantt fragment)

```
Week  Activity                                          Critical?
1-3   Site clear, erosion control, utility connect      Yes
4-6   Excavation, foundation, slab cure                 Yes
7-10  Framing (floor, walls, roof)                      Yes
9-11  Roofing (overlaps frame finish)                    Yes
11-14 Windows, exterior wrap, siding rough              Partial
13-16 Plumbing rough, electrical rough, HVAC rough     Yes
16-17 Insulation (after rough inspections)              Yes
17-19 Drywall (board, mud, sand, prime)                 Yes
19-22 Trim, doors, cabinets                             Partial
22-25 Floor finish, paint, fixtures, appliances         Partial
25-26 Final mechanical, electrical, plumbing trim      Yes
26-28 Final inspections, CO                              Yes
```

Critical path = framing → MEP rough → drywall → final. Anything on critical path that slips slips the whole project. Long-lead items (windows, custom cabinets, panel/breakers, HVAC equipment) must be ordered weeks ahead of need.
