# Chapter 2 — Conductors and Circuit Loading (C22.1:24)

Source: CSA C22.1:24 Section 4 (pp. 76–82) and Section 8 (pp. 90–97), plus cross-refs to 12-108 and 10-602. Distilled — consult the Code for full rule text.

## Overview
- **Section 4** sizes and protects conductors: ampacity tables, termination temperatures, neutral sizing, flexible cords, identification.
- **Section 8** turns connected loads into **calculated loads**: voltage divisors, voltage drop, continuous-load limits, demand factors, dwelling/apartment/school/hospital/hotel calcs, EV energy management.
- **Parallel conductors live in Section 12, not Section 4** — Rule **12-108**.

## Core Content

### Section 4 — Conductors
- **4-000 Scope** / **4-002 Size of conductors**.
- **4-004 Ampacity of wires and cables** — ampacities from **Tables 1–4** (copper/aluminum, insulated conductors); correction for ambient temperature and conductor count via **Tables 5A–5D**; flexible cords via **Table 12E**; special cases in Annex D tables (D8A–D11B, D17A–D17N).
- **4-006 Temperature limitations** — termination defaults: **60°C column** for circuits ≤100 A or **No. 1 AWG and smaller**; **75°C column** above that, unless equipment is marked for a higher temperature; **1.2 m** transition allowance for higher-temperature conductor at terminations. Ampacity never exceeds conductor temperature rating.
- **4-008** Induced voltages/currents in metal armour/sheaths of single-conductor cables.
- **4-010 Sizes of flexible cord** / **4-012 Ampacity of flexible cords** (Table 12E). **4-014 Equipment wire** (factory/field wiring of equipment). **4-034 Ampacity of portable power cable**. **4-036 Busbar**.
- **4-016 Insulation of neutral conductors**; **4-018 Size of neutral conductor** — neutral may be smaller than ungrounded conductors **except**: no reduction where the load includes electric-discharge lighting or data-processing (non-linear) loads on 3-phase 4-wire systems (harmonic-rich neutrals); where unbalanced load exceeds **200 A**, apply **70%** demand factor; minimum **No. 10 AWG Cu / No. 8 AWG Al**.
- **4-020 Common neutral conductor** — permitted for two or three sets of 3-wire single-phase feeders, or two sets of 4-wire 3-phase feeders, with all conductors in the same enclosure (metal enclosures).
- **4-022 Installation of identified conductor**; **4-024/4-026/4-028** identification of insulated neutral conductors (≤ No. 2 AWG Cu / larger / Type MI).
- **4-030 Use of identified conductors**; **4-032 Identification of insulated conductors**.
- **Parallel conductors — Rule 12-108 (Section 12)**: permitted only for **No. 1/0 AWG or larger** (Cu or Al) with conditions a)–f): no splices in raceways/underground, same circular-mil area, same insulation, same termination, same material, same length; subrule 5) permits smaller conductors in parallel for control/interlocking power. Grounding conductor parallel runs: **10-602**.

### Section 8 — Circuit Loading and Demand Factors
- **8-000 Scope**; **8-002 Special terminology** — Basic load, Calculated load, **Demonstrated load** (measured 24-month history), **EV energy management system (Δ)**.
- **8-100 Current calculations** — divide watts/V·A by **120, 208, 240, 277, 347, 416, 480, or 600** V as applicable.
- **8-102 Voltage drop** — based on connected load, else **80% of the O/C device rating**; max **3%** in a feeder or branch circuit, **5%** from service to point of utilization; subrule 3) dwelling 120 V/20 A general-use branch circuits: conductor lengths per **Table 68** acceptable.
- **8-104 Maximum circuit loading** — circuit rating = lesser of O/C device or conductor ampacity (1); calculated load ≤ rating (2); **continuous load** = persists >1 h in any 2 h (≤225 A) or >3 h in any 6 h (>225 A) (3); cyclic/intermittent counts as continuous unless it meets (3) (4); device marked 100% → continuous ≤ **100%** of conductor ampacity (**85%** for single conductors) (5, Δ); device marked 80% → ≤ **80%** (**70%** single conductors) (6, Δ).
- **8-106 Use of demand factors** — non-coincident loads → use greatest (2); heating/cooling interlock → greater of the two (3); cyclic feeders sized to max coincident load (4); motor/A/C demand factor only via **2-030** deviation (5); feeder need not exceed its supply ampacity (7); added loads = most recent **12-month** max demand + additions (8); demonstrated loads by a qualified person for loads outside 8-200/8-202 (9); **10)** EVEMS-controlled EVSE demand = max load the system allows; **11) Δ** EVSE loads omitted from dwelling/school/hospital/hotel/other calcs (8-200 1) a) vi), 8-202 1) a) vii), 8-202 3) d), 8-204 1) d), 8-206 1) d), 8-208 1) d), 8-210 c)) when an EVEMS monitors the service/feeders/branches and controls EVSE per 8-500.
- **8-108 Panelboard spaces** — single dwelling: ≥**4** spare spaces (with two-pole provision); each apartment dwelling unit: ≥**2**.
- **8-110 Determination of areas (Δ)** — living area = 100% ground floor + 100% above-ground living area + **75%** of below-grade areas with ceiling height **>1.8 m**.
- **8-200 Single dwellings** — greater of a) or b):
  - a) basic **5000 W** for first **90 m²** + **1000 W** per additional 90 m² + space heating (Section 62 demand factors) and A/C at 100% + range **6000 W** + **40%** of amount >12 kW + **100%** tankless/tank water heaters (steamers, pools, hot tubs, spas) + **100% EVSE** (Δ, except 8-106 11)) + other loads >1500 W: **25%** each (with range) or **100% up to 6000 W + 25% of excess** (without range);
  - b) flat **24 000 W** (living area ≥80 m² excl. basement) or **14 400 W** (<80 m²);
  - row housing per 8-202 demand factors; total **not treated as continuous** (3)).
- **8-202 Apartments** — per unit: greater of basic calc (**3500 W** first 45 m² + **1500 W** second 45 m² + **1000 W** per additional 90 m² + heating/A/C + range + **100% EVSE if panelboard in unit** (Δ) + other loads at 25%/25%+6000 W scheme) or **60 A**.
  - Service for ≥2 units (3) a) Δ): **100%** heaviest unit + **65%** next 2 + **40%** next 2 + **25%** next 15 + **10%** remaining; + space heating (Section 62 factors) + A/C 100% + EVSE outside dwelling-unit panelboards at **100%** (Δ, except 8-106 10)/11)) + non-dwelling loads at **75%**.
- **8-204 Schools** — **50 W/m²** classroom + **10 W/m²** remaining area + equipment ratings + EVSE (Δ 1) d)); demand factors: area ≤900 m² → **75%**; >900 m² → 75% of first 900 m² + **50%** of excess.
- **8-206 Hospitals** — **20 W/m²** general areas + **100 W/m²** high-intensity areas; EVSE item (Δ). **8-208 Hotels** — **20 W/m²** + special areas; EVSE item (Δ). **8-210 All other installations** — basic load per **Table 14** W/m² by occupancy; EVSE at 100% (c), EVEMS path via 8-106 11)).
- **8-212 Show windows** — **650 W per linear metre**.
- **8-300 Range branch circuits** — demand **8 kW** (≤12 kW rating); **8 kW + 40% of excess** >12 kW; separate built-in units count as one range; commercial ≥ full rating; excludes cord-connected hotplates/rangettes.
- **8-302 Data processing** — branch circuits feeding data-processing equipment are **continuous** loads for 8-104.
- **8-304 Maximum outlets per 2-wire circuit**:

  | O/C device marked | 15 A | 20 A |
  |---|---|---|
  | 80% continuous | **12** | **16** |
  | 100% continuous | **15** | **20** |

  Counting: duplex = 1, triplex = 1.5, quadruplex = 2; exception where connected load is known (3); multi-outlet assemblies: 1 outlet per **1.5 m**, or per **300 mm** where appliances used simultaneously.
- **8-400 Vehicle heater receptacles** — ≥1 branch circuit with O/C ≤ **20 A** per duplex (or two singles) receptacle (26-700 2)); separate circuit per unrestricted space. Demand per space — unrestricted: 15 A/20 A = **1200/1800** W (first 30), **1000/1500** (next 30), **800/1200** (over 60); restricted/controlled: **650/975**, **550/825**, **450/675**; fully-occupied lots use higher values.
- **8-500 EV energy management systems (Δ)** — may monitor loads and control EVSE loads; must not cause any circuit/feeder/service to exceed **8-104 5)/6)**; remote control permitted.

## Key Takeaways
- Ampacity chain: **Tables 1–4 → 5A–5D corrections → 4-006 termination temperature → 8-104 continuous-load caps**. The 60/75°C termination default (≤100 A / No. 1 AWG boundary) usually governs.
- Continuous-load math: >1 h in 2 h (≤225 A) or >3 h in 6 h (>225 A); 80%-marked devices cap continuous at 80% of conductor ampacity.
- Memorize the dwelling ladder: 5000 W/90 m² + 1000 W per extra 90 m², range 6000 W + 40% over 12 kW, alternate flat 24 kW/14.4 kW; apartment service 100/65/40/25/10%.
- **Neutral harmonic trap (4-018)**: no downsizing with discharge-lighting/data-processing loads; 70% factor above 200 A unbalanced.
- **EVSE/EVEMS (Δ 2024)**: default 100% everywhere; 8-106 10)/11) + 8-500 let an energy management system replace the EVSE demand.

## Connects To
Ch. 1 (definitions; AWG = copper per 2-120) · Section 12 (wiring methods; **12-108** parallel) · Section 10 (**10-602** parallel grounding runs) · Section 26 (O/C device ratings, receptacles) · Section 62 (heating demand factors) · Section 86 (86-302 continuous loads) · Tables 1–5D, 12E, 14, 56, 68; Annex D (D8A–D11B).