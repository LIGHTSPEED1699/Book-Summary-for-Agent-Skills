---
name: csa-b149-3
description: >
  CSA B149.3:25 — Code for the field approval of fuel-related components on
  appliances using gaseous or liquid fuels. Valve trains, safety shut-off
  valves, pilots, burners, regulators, safety controls, process appliances,
  flare pilots, annex procedures. Use when designing, reviewing, approving, or
  troubleshooting field-assembled gas/LP fuel systems in Canada.
---

# CSA B149.3:25 — Field Approval of Fuel-Related Components

## How to use this skill
- **Sizing a valve train / picking SSOVs** → cheatsheet.md tier tables (fastest) or ch07/ch08.
- **"What does clause X require?"** → chapters/chXX file (see map below).
- **Threshold numbers** → patterns.md §8 or cheatsheet.md.
- **Definitions** → glossary.md.
- **Procedures** (start-up, VPS, oxygen, H2) → ch12-annexes.md.

## The Code in one paragraph
B149.3 governs **field approval**: fuel-related components assembled or modified on site, from the appliance manual shut-off valve downstream. The AHJ approves based on documentation (P&ID, BOM, wiring, control narrative, commissioning report). Component safety scales with input rating; the rest is discipline about redundancy, failsafe wiring, and independent pilot systems.

## Chapter map
| File | Contents |
|---|---|
| ch01-scope.md | Clause 1 — scope, field-approval concept, exclusions |
| ch02-reference-publications.md | Clause 2 — certification standards table |
| ch03-definitions.md | Clause 3 — field approval, valve train, VPS, tiers |
| ch04-pressure-regulators.md | Clause 4 — ±10%, lock-up, pilot venting |
| ch05-pilot-supply.md | Clause 5 — takeoff position/pressure |
| ch06-manual-valves.md | Clause 6 — shut-off/isolation/test firing + end-switch |
| ch07-pilot-ssovs-burners.md | Clause 7 — pilot SSOV tiers, pilot burners |
| ch08-main-ssovs-burners.md | Clause 8 — main SSOV tiers, flow control, burners |
| ch09-lp-valve-trains.md | Clause 9 — Sched 80, Class 300, LP certification |
| ch10-applications.md | Clause 10 — documentation, simple vs complex, overpressure |
| ch11-clauses-11-20.md | Ignition, safety controls, electrical, rating plate, start-up, process appliances (16), generators (17), flare pilots (18), complex facilities (19), portable (20) |
| ch12-annexes.md | A start-up · B/C diagrams · D FARC · E VPS · F oxygen · G liquid · H solid · I risk program · J food trucks · K turbines · L hazardous locations · M IOM manuals · N hydrogen |

## Non-negotiables (most-cited requirements)
1. **Regulators**: separate pilot regulator; ±10% tolerance; lock-up > 0.5 psig; no bypassing (Cl.4).
2. **SSOVs**: certified (Z21.21/6.5 or CGA 3.9 above 400k Btu/h or 0.5 psig); series piping, **parallel wiring**; no safety bypass; proof of closure scales with input — both valves ≥ 12.5 MMBtu/h (Cl.7/8).
3. **Timing**: pilot and main trial for ignition ≤ 10 s; flame loss → ~4 s fuel shut-off; prepurge 4 air changes at ≥ 80% airflow; low fire start > 3.5 MMBtu/h (Cl.11/12).
4. **Pilot supply**: takeoff downstream of appliance manual valve, top/side of pipe; independent valving/regulation end-to-end (Cl.5/6.3).
5. **Documentation**: P&ID + BOM (tag cross-referenced) + wiring + BMS spec + commissioning report; complex appliances add PLC narrative, VPS spec, explosion-relief drawings (Cl.10, Annex M).
6. **LP service**: Schedule 80 pipe, Class 300 fittings, LP-certified components (Cl.9).
7. **Flare pilots**: ignition only at the tip (no remote flame front); fuel conditioning with plugging indication; alarm ≤ 15 min on flame loss, failsafe; 5-year records (Cl.18).

## Common workflows
**Specify a new field-assembled train:** determine input tier → pick SSOV arrangement (cheatsheet tables) → regulator (lock-up check) → pilot supply/regulation → test firing valve (end-switch if > 12.5 MMBtu/h) → assemble documentation package (ch10).

**Prepare for AHJ field approval:** assemble ch10 checklist; classify simple vs complex; if complex, add Annex M.2.2 items; verify every component's certification against Clause 2 (ch02 table).

**Commission/start up high-input equipment:** run Annex A 4-cycle dry run + pilot turndown test (ch12), separately per burner; record all set points for the commissioning report.

**Evaluate a special regime:** oxygen (F), liquid (G), solid (H), complex facility risk program (I), food truck (J), turbine > 150 psig (K), hazardous location (L), hydrogen blend (N) — each has a threshold-driven checklist in ch12.

## Reading the Code's style
- Requirements are tiered by input; find the tier first, the answer follows.
- "C/I", proof of closure, and VPS are interchangeable redundancy devices in defined ratios.
- Informative annexes are written in mandatory language so AHJs can adopt them verbatim.
- Exemptions always cite a compensating control — trace the "except".

## Related codes
B149.1 (installation), B149.2 (propane), B149.5 (sibling field-approval code), B139/B140 (oil), C22.1 (electrical), NFPA 85/86 (boilers/ovens, good-practice overlays).