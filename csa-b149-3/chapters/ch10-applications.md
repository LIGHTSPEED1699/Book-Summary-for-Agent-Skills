# Chapter 10 — Applications (Clause 10)

## Overview
Clause 10 is the documentation and approval engine of B149.3: it defines what the assembler must submit for field approval, distinguishes simple vs complex appliances, and adds overpressure-protection and venting rules for special situations.

## Core Content
### 10.1 Field approval documentation
- **10.1.2.3 Simple vs complex**: *Simple* appliances follow the standard component clauses; *complex* appliances (multi-burner integration, custom controls, process integration) require additional engineering documentation — and trigger the enhanced IOM contents of Annex M (M.2.2/M.3.2/M.4.2).
- Documentation package (typical minimum):
  - Description of hazardous conditions affecting the appliance/installation;
  - **P&ID** showing safety control locations;
  - **BOM/component data sheets** — model, manufacturer, materials, ratings, certification, tag numbers cross-referenced to drawings and hardware;
  - **Wiring diagrams** for all control panels;
  - **Burner management system specification**;
  - Operating narrative, shutdown key/cause-and-effect, ladder logic (or equivalent);
  - Electrical area classification spec; venting of appliance/instrument vents to safe location; valve-train overpressure protection;
  - **Commissioning/combustion report** — set points and stack readings at maximum fire;
  - **Fuel switch-over procedure** for multi-fuel appliances (must not exceed max rating).

### 10.5–10.6 special situations
- **Threaded fittings**: acceptable ≤ NPS 4 for field assemblies (larger needs flanged/welded).
- **Minimum schedule**: Schedule 40 pipe baseline for standard gas service.
- **Overpressure protection options** (when inlet pressure can exceed component ratings):
  - Monitoring or series regulator;
  - Relief valve sized to prevent overpressure;
  - **OPCO** (operating pressure control/limit) interlock;
  - High-pressure safety device per Clause 12.5.1.
- **10.6.8 Vent-limiting regulators**: integrated with Clause 4.7/4.8 venting rules.
- Installation-side requirements default to **CSA B149.1** (and B149.2 for propane storage).

## Documentation Package Checklist
| Item | Simple | Complex |
|---|---|---|
| P&ID, BOM, wiring diagrams | ✓ | ✓ |
| BMS spec + operating narrative | ✓ | ✓ |
| Commissioning report | ✓ | ✓ |
| PLC control narrative, purge/ignition/flame-failure set points | — | ✓ |
| VPS design + testing spec (leakage time, min detection, sequence) | — | ✓ |
| Explosion-relief installation drawings (when required, 16.2.4) | — | ✓ |

## Key Takeaways
- Field approval is documentation-driven: no BOM cross-referenced to tags, no approval.
- The simple/complex split decides whether Annex M's enhanced IOM contents apply.
- Overpressure protection has four accepted strategies — pick by inlet pressure and component rating.
- Threaded fittings stop at NPS 4; Schedule 40 is the gas-service floor (Schedule 80 for LP per Clause 9).

## Connects To
- ch01 (scope of field approval), ch09 (LP materials), ch11 Clause 12.5 (pressure safety settings), ch12 Annexes I, J, M (risk program, food trucks, IOM contents).