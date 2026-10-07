# Chapter 5 — Protection and Control (Sections 14 and 16)

## Overview
Section 14 supplements and amends every other Section: it is the default rulebook for overcurrent devices, fuses, breakers, control devices, switches, and solid-state equipment. Section 16 governs Class 1 and Class 2 (low-energy/remote-control/data) circuits — definitions, wiring methods, and separation from power wiring.

## Core Content

### Section 14 — Protection and control (pages 154–165)

**Device requirements**
- 14-010: every circuit needs protective and control devices where the Code requires them; 14-012: device ratings adequate for circuit voltage and current; 14-014: series-rated combinations only where marked/identified.

**Overcurrent protection of conductors (14-100)**
- Protect each ungrounded conductor at the point it receives its supply and at every size reduction. Tap exceptions (14-100 1)): b) ≤3 m tap, ampacity ≥ combined loads and ≥ device rating; c) ampacity ≥ 1/3 of larger conductor, ≤7.5 m, terminating in a single OC device ≤ tap ampacity; e) control-circuit conductors ≥ No. 14 AWG, external to enclosure, OC ≤300% of ampacity (or where opening creates a hazard); f) transformer taps — primary + secondary ≤7.5 m combined, secondary terminates in a single OC device ≤ its ampacity.
- 14-100 2): consumer's service conductors protected by the OC device at the service equipment.

**Ground fault protection (14-102)** — solidly grounded systems:

| System voltage | GFP required when circuit rated |
|---|---|
| >150 V-to-gnd, <750 V phase-to-phase | ≥1000 A |
| ≤150 V-to-gnd | ≥2000 A |

Max setting 1200 A; max 1 s delay at ≥3000 A ground-fault current (14-102 2); series-coordination exception in 14-102 8).

**Ratings (14-104; Table 13, page 460)**
- OC device ≤ conductor ampacity, except next standard size per Table 13 permitted up to 800 A max.
- Hard caps (14-104 2)): 15 A / No. 14 Cu; 20 A / No. 12 Cu; 30 A / No. 10 Cu; 15 A / No. 12 Al; 25 A / No. 10 Al.

**Installation rules**
- 14-106/14-108: readily accessible; enclosed in cut-out boxes/cabinets; breaker handles operable without opening doors to live parts.
- 14-110: >2 lighting branch circuits (1φ 3-wire) or >3 (3φ 4-wire) → panelboard required; fusible switches → all OC devices same rating; multiwire-circuit ungrounded conductors count separately.
- 14-112: no OC devices in parallel at ≤750 V (exception: semiconductor fuses ≥100 kA IR and breakers ≤750 V, factory-assembled in parallel as one unit). 14-114: supplementary protectors never substitute for branch-circuit protection.

**Fuses**
- 14-200: "P" = low-melting-point, "D" = time-delay. 14-202: plug fuses only ≤125 V between conductors (exception: grounded-neutral systems with no conductor >150 V-to-gnd); 14-204 non-interchangeable; 14-206 covered fuseholders in unauthorized areas; 14-208: plug fuses ≤30 A, standard cartridge ≤600 A/600 V.
- 14-212: Class H = 10 000 A IR; CA/CB/CC/G/J/K/L/R/T/HRCI-MISC may replace Class H; Class C and HRCII-MISC = short-circuit protection only (≤85% of max permitted rating where used above load ampacity).

**Circuit breakers**
- 14-300: trip-free + open/closed indication; 14-302: opens all ungrounded conductors by one handle (interlocked single-pole pair permitted on 3-wire grounded-neutral systems); 14-304: non-tamperable unless accessible only to authorized persons; 14-306: tripping elements per Table 25 (page 480); 14-308: battery control power requires continuous battery-voltage monitoring.

**Control devices and switches**
- 14-400 rating ≥ load; 14-402 disconnecting means for fused circuits; 14-404 control devices ahead of OC devices; 14-406/408/410/412/414/416: location, ON/OFF indication, enclosure, grouping, different circuits, switching-only use. 14-508/510 general-use ac/dc and ac switch ratings; 14-512 347 V ac switches; 14-514: >300 V-to-ground — no ganging/grouping in one enclosure unless barriers installed.

**Miscellaneous and solid-state**
- 14-600: receptacle rating ≥ branch-circuit OC rating; 14-602: portable appliances ≤1500 W need no extra control device if readily disconnectable; 14-604: multi-point switching in the ungrounded conductor only; 14-610: circuits >50% cycling load on fuses → time-delay/low-melting-point types.
- 14-606: panelboards protected on the supply side ≤ panelboard rating, except when >90% of its OC devices supply feeders/motor branch circuits (transformer-primary OC allowed with voltage-ratio sizing); 14-612: transfer equipment prevents interconnection of normal and standby sources.
- 14-700: solid-state devices never serve as isolating switches/disconnecting means; 14-702: supplementary disconnect where failure/leakage could transfer energy between sources (integral, or close and in sight); 14-704: warning notices (terminals may be live when open; feedback from alternate sources).

### Section 16 — Class 1 and Class 2 circuits (pages 166–172)

| Decision | Rule |
|---|---|
| Class 1 extra-low-voltage power circuit | 16-004 (defined in 16-002) |
| Class 2 low-energy power circuit | 16-006 |
| PSE / data communication circuits | 16-300 scope; source output ≤100 V·A and ≤60 V dc (16-320) |
| Circuits in hazardous locations | must comply with Section 18 (16-008) |
| Circuits to safety control devices | 16-010; communication cables 16-012 |
| Class 1 wiring | any Section 6/12 method (16-102); OC at supply end (16-104/106); sources/transformers (16-108); conductor size/material (16-110/112); with other circuits in one enclosure (16-114); mechanical protection (16-116); aerial beyond building (16-118) |
| Class 2 supply side | Section 12 methods (16-202); marking (16-204); source-limited OC (16-206/208); conductors/cables (16-210) |
| Class 2 separation | separated from power/lighting circuits (16-212); multiple Class 2 circuits may share a cable (16-214) |
| Special environments | fire separations (16-216); shafts/hoistways (16-218); ducts/plenums (16-220); load-side equipment (16-222); beyond building (16-224); underground (16-226) |
| "-LP" marked cable | limit per marked current rating; <No. 26 AWG or bundles >192 cables over ≥1 m → qualified person + deviation per 2-030 (16-330 2)) |

## Key Takeaways
- Section 14 is the fallback rulebook: when another Section is silent on protective/control devices, 14-xxx applies.
- GFP only for large solidly grounded circuits: ≥1000 A above 150 V-to-gnd; ≥2000 A at/below; capped at 1200 A / 1 s @ 3000 A.
- Table 13 next-size-up stops at 800 A; small-conductor caps (15/20/30 A Cu; 15/25 A Al) always bind.
- Class 2 = energy-limited and kept separated from power circuits; Class 1 = ordinary wiring rules.

## Connects To
- Section 8 (load calculations precondition 14-104 1) a)), Section 10 (grounding; GFP sensor paths), Section 12 (wiring methods referenced by 16-202), Section 18 (via 16-008), Section 26 (transformer/motor protection), Section 28 (motor overloads with Table 25), Section 24 (isolated systems), Diagram 3 (GFP sensor points).