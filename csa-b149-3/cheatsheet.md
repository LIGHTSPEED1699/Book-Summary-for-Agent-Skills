# Cheat Sheet — CSA B149.3:25 Field Approval of Fuel-Related Components

## What this Code is
Field-approval requirements for fuel-related components (valve trains, controls, pilots, burners) on appliances assembled/modified on site. Starts at the appliance manual shut-off valve (B149.1 6.18.2); AHJ grants approval on documentation.

## Valve train order (typical)
Manual shut-off → pilot takeoff (top/side, 5.1) → pilot manual valve (6.3, first in pilot train) → fuel conditioning (flare: 18.3) → regulator (4.1/4.2, separate pilot reg; lock-up > 0.5 psig, 4.6) → SSOVs (7/8) → test firing valve (6.4-6.5, downstream of SSOVs, near burner) → burner.

## SSOV tiers — pilots (Cl.7)
| Pilot input | Minimum |
|---|---|
| ≤ 20k Btu/h | 1 SSOV or combination/thermocouple control circuit |
| 20k–400k | 2 series (parallel-wired) or 1 C/I |
| 400k–3.5 MMBtu/h | 2 (one C/I) or 1 C/I + proof of closure |
| > 3.5 MMBtu/h | Main-train rules |

## SSOV tiers — main burners (Cl.8)
| Input | Minimum |
|---|---|
| ≤ 400k & ≤ 0.5 psig | 2 series / 1 C-I / combination control (Z21.78/6.20) |
| > 400k–5 MMBtu/h | 2 series or 1 + proof of closure |
| > 5–< 12.5 MMBtu/h | 2 series, one with proof of closure |
| ≥ 12.5 MMBtu/h | 2 series, both with proof of closure |
| Multi-burner | Header SSOV counts as one of each burner's two |

Certification: > 400k or > 0.5 psig → CGA 3.9 or Z21.21/6.5 only. Multiple valves wired parallel. Holding circuit must not defeat proof of closure (8.1.3).

## Numbers to memorize
- Regulator: ±10% outlet; lock-up > 0.5 psig; certified Z21.18/6.3 or high/low pressure switches (4.9)
- Prepurge: 4 air changes; airflow ≥ 80% max input (12.2)
- Low fire start > 3.5 MMBtu/h (12.3)
- Trial for ignition ≤ 10 s (11.2.3/11.3.2); flame loss → ~4 s shutdown (12.1)
- Low gas pressure device ~50% of normal (12.6)
- Threaded fittings ≤ NPS 4; Schedule 40 gas / Schedule 80 LP, Class 300 LP fittings (9, 10)
- Flare pilot: no remote flame front (18.1.3); alarm ≤ 15 min flame loss (18.8.4); records 5 yr (18.9.3)
- Turbine SSOVs > 150 psig & > 12.5 MMBtu/h: close ≤ 5 s, 20k cycles (K)
- H2: LFL 4%/UFL 75%; embrittlement threshold 66 psi; > 25% blend → UV/UV-IR scanners, detection at 20%→alarm/40%→de-energize, 6 ACH or area study (N)
- Oxygen: 2 series SSOVs, no vent valves, oxygen-cleaned, airflow-proven enrichment (F)

## Field approval documentation (Cl.10 + Annex M)
P&ID (safety controls marked) · BOM w/ tag cross-refs · wiring diagrams · BMS spec · operating narrative/cause-effect/ladder logic · area classification · commissioning report (set points, stack readings @ max fire) · fuel switch-over procedure.
**Complex adds:** PLC control narrative (firing method, purge duration/rate, ignition source, pilot mode, trial times, flame-failure response), VPS spec (leakage time, min detection, sequence), explosion-relief drawings (16.2.4).

## Annex A start-up (> 400k Btu/h)
4-cycle dry run, valves closed: ① purge airflow/damper + 4 changes + low-fire return ② simulate airflow failure (no spark) ③ scanner reads zero pre-ignition ④ simulated flame before ignition blocks start; pilot ≤ 10 s; main opens after pilot proof ⑤ pilot turndown test — 3 successful main light-offs at lowest pilot setting.

## Special regimes
- **LP trains:** Sched 80 pipe, Class 300 fittings, LP-certified components (Cl.9)
- **Class A ovens:** LFL-based ventilation calc (size, solvent, temp, altitude) (16.10)
- **Complex facilities:** Annex I risk-based program (QMS, ALARP, audited ITPM) where legislation allows
- **Food trucks:** B51 tanks, vapour withdrawal, QCC1, no valve between relief & tank, accessible shut-off (J)
- **Hazardous locations:** electrical authority jurisdiction; Zones/Groups per CEC (L)