# CSA C22.1:24 Cheatsheet — Load-Bearing Numbers

All values verified against the 2024 edition source text (Tables section, pp. 393-523). Full tables in the source PDF; the extracts below cover the most-used rows.

## Voltage drop — Rule 8-102

- Basis: connected load of the feeder/branch if known; otherwise **80% of the OCPD rating**.
- Limits: **3%** in a feeder OR branch circuit; **5%** total from supply side of consumer's service to point of utilization.
- Dwelling units: general-use branch circuits ≤120 V or 20 A may instead comply via **Table 68** (max insulated conductor length, 90 °C Cu, 120 V 2-wire, from service to furthest utilization point).
- Industrial (qualified persons, supervised): design shall ensure utilization voltage per equipment requirements (8-102 4)).

## Ampacity base tables — Rule 4-004

Table 2 — Copper, ≤3 insulated conductors, raceway or cable, 30 °C ambient (A):

| Size | 60 °C | 75 °C | 90 °C |
|---|---|---|---|
| 14 | 15 | 20 | 25 |
| 12 | 20 | 25 | 30 |
| 10 | 30 | 35 | 40 |
| 8 | 40 | 50 | 55 |
| 6 | 55 | 65 | 75 |
| 4 | 70 | 85 | 95 |
| 3 | 85 | 100 | 115 |
| 2 | 95 | 115 | 130 |
| 1 | 110 | 130 | 145 |
| 1/0 | 125 | 150 | 170 |
| 2/0 | 145 | 175 | 195 |
| 3/0 | 165 | 200 | 225 |
| 4/0 | 195 | 230 | 260 |
| 250 kcmil | 215 | 255 | 290 |
| 500 | 320 | 380 | 430 |
| 1000 | 455 | 545 | 615 |

- Table 1 = Cu in free air; Table 3 = Al in raceway/cable; Table 4 = Al in free air. Aluminum is roughly one size larger for the same ampacity.
- Higher-temperature columns (110/125/200 °C) exist in Tables 1-4 for special insulations.
- Table 14 = watts/m² demand factors for services/feeders by occupancy. Table 13 = OCPD rating/setting for conductor protection (standard sizes: 15/20/30/40/50/60/70/80/90/100/110/125/150/175/200/225/250/300/350/400/450/500/600/700/800/1000/1200/1600/2000/2500/3000/4000/5000/6000 A).

## Ambient correction — Table 5A (apply to Tables 1-4 above 30 °C)

| Ambient | 60 °C | 75 °C | 90 °C |
|---|---|---|---|
| 35 °C | 0.91 | 0.94 | 0.96 |
| 40 °C | 0.82 | 0.88 | 0.91 |
| 45 °C | 0.71 | 0.82 | 0.87 |
| 50 °C | 0.58 | 0.75 | 0.82 |
| 55 °C | 0.41 | 0.67 | 0.76 |
| 60 °C | — | 0.58 | 0.71 |
| 65 °C | — | 0.47 | 0.65 |
| 70 °C | — | 0.33 | 0.58 |

## More-than-3-conductor correction — Table 5C (Tables 2 and 4)

| # conductors | Factor |
|---|---|
| 1-3 | 1.00 |
| 4-6 | 0.80 |
| 7-24 | 0.70 |
| 25-42 | 0.60 |
| 43+ | 0.50 |

Cable tray spacing factors: Table 5D. Free-air/bare conductor at 40 °C: Table 66.

## Bonding & grounding sizes

**Table 16 — Minimum size of system bonding jumper / bonding conductor (by OCPD rating):**

| OCPD (A) | Cu | Al |
|---|---|---|
| ≤20 | 14 | 12 |
| 30 | 12 | 10 |
| 60 | 10 | 8 |
| 100 | 8 | 6 |
| 200 | 6 | 4 |
| 300 | 4 | 2 |
| 400 | 3 | 1 |
| 500 | 2 | 1/0 |
| 600 | 1 | 2/0 |
| 800 | 1/0 | 3/0 |
| 1000 | 2/0 | 4/0 |
| 2000 | 250 | 400 |

Also: Table 41 bonding jumper for service raceways; Table 43 field-assembled grounding electrode conductor minimum; Table 51 bare copper grounding conductors; Table 59 communications protector grounding.

## Raceway & box fill

- **Table 8 fill %**: 1 conductor **53%**, 2 conductors **31%**, 3+ **40%** (non-lead-sheathed).
- Table 9A/9B: conduit internal diameters; 9C-9H: max conductor area at 53%/31%/40% fill per trade size.
- Tables 6A-6K: conductor dimensions for fill calc (per insulation type).
- Box fill: Table 22 (space), Table 23 (number of conductors).
- Bend radius: **Table 7** (rule 12-924): 16mm→102, 21mm→114, 27mm→146, 35mm→184, 41mm→210, 53mm→241, 63mm→267, 78mm→330, 91mm→381, 103mm→406 mm.
- Vertical run support: Table 21.

## Receptacles & GFCI — Section 26

- 26-700 general; 26-702 bonding of receptacles.
- **26-704**: GFCI Class A protection — Appendix B notes receptacles within **1.5 m** of wash basins, bathtubs, shower stalls.
- 26-706 tamper-resistant; 26-708 weather-exposed receptacles.

## Grounding systems

- Solidly grounded, resistance/impedance grounded systems: Section 10, rules 10-1xx/10-3xx.
- **Table 17**: alarm/de-energization conditions for impedance grounded systems (rule 10-302) — 4-wire with line-to-neutral loads: immediate alarm AND de-energize on first fault; 3-wire: time-graded schemes permitted.
- Table 52: tolerable touch/step voltages (safety engineering).

## Where things moved (2024 edition)

- Former Tables 46/47/49/54/55 → **Diagrams 1-5**. Diagram 1 referenced from receptacle rules (26-700 etc.).
- Deleted: Tables 6, 9, 10A-C, 11, 16A/16B, 20, 26, 38, 39, 42; Sections 48/50/82.
- Flexible cords/equipment wire ampacity: Table 12 (Cu) with 11A/11B conditions-of-use.
- Motors: Tables 27/28/29 (conductor sizing, OCP), 44/45 (3-phase/single-phase motor tables), 37 (insulation temp rating).
- Welders: Tables 42A/B/C conductor multipliers.
- Hazardous areas: Table 18 (equipment suitability), 18A (Zone↔Division equivalence), 63/64/69 (propane/NGV/bulk plants).
- Voltage-drop max length: Table 68. Working space: Table 56. Buried cover: Table 53. Pool separations: Table 61.