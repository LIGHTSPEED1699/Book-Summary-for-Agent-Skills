# Patterns — CSA B149.3 Recurring Structures

## Pattern 1 — Input-tier escalation
Every component requirement scales with burner input. Learn the thresholds; most tables resolve instantly.
- **20 000 Btu/h (6 kW)** — pilot SSOV floor; single valve or control-circuit suffices below; test firing valve not required at/below.
- **400 000 Btu/h (120 kW)** — appliance-grade controls (Z21.78/6.20, CAN1-6.4) top out; above this, industrial SSOVs (Z21.21/6.5, CGA 3.9) only; Annex A start-up applies above.
- **3.5 MMBtu/h (1025 kW)** — pilot trains above become main trains; low fire start required.
- **5 MMBtu/h (1500 kW)** — proof of closure becomes mandatory (first of two valves).
- **12.5 MMBtu/h (3660 kW)** — proof of closure on *both* SSOVs; test firing valve end-switch interlock.

## Pattern 2 — Redundancy ladder for fuel shut-off
The Code offers the same three rungs everywhere (pilot Cl.7, main Cl.8):
1. **Two SSOVs in series, wired parallel** — classic double block.
2. **One C/I (manual-reset) valve** — substitutes for the second valve.
3. **Proof of closure** — electronics prove closure for larger inputs; **or approved VPS** proving tightness every cycle (Annex E).
Escalation is driven by input: bigger burner → stronger guarantee of valve tightness before light-off.

## Pattern 3 — Parallel wiring rule
Multiple SSOVs are always **wired in parallel** (each valve energized independently) so a single control failure de-energizes all. Bypassing safety features is prohibited; the only sanctioned "bypass" is inside an approved VPS.

## Pattern 4 — Independent pilot everything
Pilot systems are deliberately isolated: independent regulator (4.2), independent manual shut-off first in train (6.3), takeoff downstream of the appliance manual valve from top/side of pipe (5.1). Pilot failure never propagates to or from the main train.

## Pattern 5 — Fail-safe alarm/wiring convention
Any device whose failure must trigger action is wired failsafe: loss of signal or self-diagnosed instrument failure generates the alarm/trip (flare pilot 18.8, gas detection Annex N, BMS 12.7). Holding circuits must never defeat proof-of-closure switches (8.1.3).

## Pattern 6 — Mandatory-language annexes
Informative annexes (A, D, E, F, G, H, I, J, M, N) are written in "shall" language so an AHJ can adopt them verbatim. When adopted, treat as enforceable; when not, treat as best practice.

## Pattern 7 — Documentation as the approval currency
Field approval is granted on paper first: P&ID + BOM with tag cross-references + wiring diagrams + BMS spec + control narrative + commissioning report. Complex appliances add purge/ignition/flame-failure set points, VPS specs, and explosion-relief drawings (Clause 10, Annex M).

## Pattern 8 — Threshold constants worth memorizing
- 0.5 psig — lock-up regulator / industrial-certification threshold (4.6, 8.1.1)
- ±10% — regulator outlet tolerance (4.4)
- 4 air changes — prepurge (12.2)
- 10 s — trial for ignition (11.2.3, 11.3.2)
- 4 s — flame failure response (pilot typical, 12.1/16.3)
- 80% — purge airflow fraction of max input (12.2, Annex A)
- 66 psi (455 kPa) — hydrogen embrittlement threshold (N.3.1)
- 25% H2 — detection/UV-scanner/ventilation threshold (Annex N)
- 20%/40% LFL — alarm/de-energize set points for gas detection (Annex N)
- 15 min — flare pilot flame-loss alarm (18.8.4)
- 5 years — flare pilot records retention (18.9.3)
- ≤ 5 s — large-turbine SSOV closing time (Annex K)
- Schedule 80 / Class 300 — LP train materials (Clause 9)
- NPS 4 — threaded fitting limit (Clause 10)

## Pattern 9 — Exemption logic
Exemptions always cite a compensating control: 6.7 (end-switch exempt with manual-reset limits), 4.7/4.8 (vent exempt with leak-limiting regulator), 16.1 (NAICS process industries exempt where other regulation governs), Annex J carts (ANSI Z83.11 covers). When you see "except", find the compensating mechanism.