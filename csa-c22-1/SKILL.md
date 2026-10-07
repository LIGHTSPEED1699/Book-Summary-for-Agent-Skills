---
name: csa-c22-1
description: Canadian Electrical Code CSA C22.1:24 (Part I, 2024, 26th ed) distilled - electrical installation rules for Canada - conductors, ampacity, wiring methods, grounding/bonding, services, protection, hazardous locations, motors, EV charging, renewables/ESS. Use when designing, reviewing, inspecting, or troubleshooting Canadian electrical installations.
---

# CSA C22.1:24 — Canadian Electrical Code, Part I (2024)

Distilled from the 2024 (26th) edition, 972 pages. This is a study/assistant aid, NOT the code: for compliance work, verify exact rule text against the CSA source document and provincial amendments.

## What it is

- CSA C22.1:24 covers **electrical installations** in Canada: the wiring from the point of supply (consumer's service) through to the load. It prescribes minimum safety requirements for conductors, protection, grounding/bonding, wiring methods, and equipment installation.
- **Equipment safety standards are the CSA C22.2 series** — C22.1 tells you *where and how* equipment may be installed; C22.2 governs *the equipment itself*. Approval markings (e.g., cUL/cULus/ETL-C) trace to C22.2.
- **Appendix B** carries the explanatory Notes on Rules — the rationale behind the mandatory text. When a rule seems ambiguous, Appendix B usually explains intent.
- Administered/provincialized by local authorities (in Ontario: ESA — Electrical Safety Authority). Provincial amendments can change effective requirements; always check the local AHJ adoption.

## How to use

1. Start with `cheatsheet.md` — the load-bearing numbers (ampacity, voltage drop, bonding sizes, conduit fill) with rule/table references.
2. Use the chapter map below to find the section-specific distill.
3. For definitions, `glossary.md`. For recurring installation patterns, `patterns.md`.
4. Rule citations in this skill use CEC rule numbers (`12-904`, `26-704`). Every number was verified against the source text; still grep the source PDF when accuracy is critical.

## Chapter map

| Chapter | File | Covers (source pages) |
|---|---|---|
| ch01 | foundations — S0 Object/Scope/Definitions + S2 General Rules | 53-75 |
| ch02 | conductors-loading — S4 Conductors + S8 Circuit loading/demand factors | 76-97 |
| ch03 | services-grounding — S6 Services + S10 Grounding and bonding | 83-107 |
| ch04 | wiring-methods — S12 Wiring methods | 108-156 |
| ch05 | protection-control — S14 Protection/control + S16 Class 1/2 circuits | 157-172 |
| ch06 | hazardous-special-locations — S18/20/22/24 | 173-210 |
| ch07 | equipment-motors — S26 Equipment + S28 Motors/generators | 211-244 |
| ch08 | lighting-fire-signs — S30 Lighting + S32 Fire alarm + S34 Signs | 245-264 |
| ch09 | hv-machinery — S36 High voltage, S38 Elevators, S40 Cranes, S42 Welders, S44 Theatre, S46 Emergency power | 265-295 |
| ch10 | media-heating-energy — S52-64 (comms, heating, renewables/ESS) | 296-359 |
| ch11 | occupancy-specific — S66-86 (pools, RV parks, marine, EV charging) | 360-392 |
| ch12 | tables-diagrams — Tables + Diagrams digest | 393-523 |
| ch13 | appendices — Appendices A-M digest | 524-929 |

Deleted sections in this edition: **48, 50, 82**. Appendix B is the largest (notes on rules).

## Non-negotiables (verified against source)

- **Ampacity**: Tables 1-4 (1=Cu free air, 2=Cu raceway/cable, 3=Al raceway/cable, 4=Al free air), base 30 °C ambient, ≤3 conductors. Corrections: Table 5A (ambient >30 °C), Table 5C (more than 3 conductors), Table 5D (spaced cable tray). Rule 4-004 governs.
- **Voltage drop (8-102)**: ≤3% in a feeder or branch circuit; ≤5% total from supply side of consumer's service to point of utilization. Based on connected load, else 80% of OCPD rating. Dwelling-unit 120 V/20 A general-use branch circuits may instead use the Table 68 max-length method.
- **Bonding conductor sizing (Table 16)**: minimum system bonding jumper/bonding conductor size scales with the OCPD rating protecting the conductor — 30 A→12 Cu, 60 A→10 Cu, 100 A→8 Cu, 200 A→6 Cu, 400 A→3 Cu, 600 A→1 Cu, 1000 A→2/0 Cu, 2000 A→250 kcmil Cu (Al one size larger).
- **Grounding electrodes**: Table 43 (field-assembled electrode conductor minimums), Table 51 (bare copper grounding conductors).
- **Conduit fill (Table 8)**: 1 conductor 53%, 2 conductors 31%, 3+ 40%. Box fill: Tables 22/23. Bend radius: Table 7 (rule 12-924).
- **Receptacles (Section 26)**: 26-700 general, 26-702 bonding, 26-704 GFCI Class A protection (including receptacles within 1.5 m of wash basins, bathtubs, shower stalls), 26-706 tamper-resistant, 26-708 weather-exposed.
- **Impedance grounded systems**: Table 17 conditions for alarm/de-energization (rule 10-302).

## Limitations

- Distilled content condenses and may omit subrules; never cite this skill as the code.
- Tables here are decision-useful extracts — full tables (and footnotes) live in the source.
- Provincial amendments (ESA Ontario bulletins, BC, Alberta, Quebec C15.1 harmonization) may alter effective requirements.
- This edition deleted Sections 48/50/82 and many old tables (10A-C, 11, 16A/16B, 20, 26, 38, 39, 42, 46-49, 54, 55 — the last five became Diagrams 1-5).

## Related

- `csa-b149-3` skill — natural gas/propane appliance installation (sister distill)
- CSA C22.2 series — equipment safety standards
- CSA C22.1:24 Appendix B — Notes on Rules (rationale)
- Local AHJ bulletins (e.g., ESA Ontario Bulletins)