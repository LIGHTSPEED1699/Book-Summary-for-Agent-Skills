# Glossary — Shinskey, Process Control Systems (4th ed.)

Notation and key terms as Shinskey uses them. Chapter references are to the 4th edition.

## Controller parameters (ISA form unless noted)
- **P — proportional band**: % change in deviation to drive output 0→100%. Controller gain Kc = 100/P. Shinskey always quotes P, not Kc.
- **I — integral (reset) time**: minutes (or any time unit) for the integral term to repeat the proportional term's action; dm/dt = e/I.
- **D — derivative (rate) time**: D·dc/dt added to output. In the ISA (noninteracting) form P, I, D are independent; in the **interacting (series)** form the effective settings are I_eff = I + D and D_eff = 1/(1/I + 1/D), with steady gain Kc = (100/P)(1 + D/I) (4.29–4.31). D_eff ≤ I_eff/4 always.
- **P on deviation vs P on error**: P-on-set-point adds set-point overshoot; "derivative on measurement" avoids the set-point kick.

## Process descriptors
- **Kp — process (steady-state) gain**: Δc/Δm at steady state.
- **τ1 — dominant time constant**; **τ2 — secondary lag**; **τd (or Td) — dead time** (transport + measurement + valve-stem lag lumped; measure it by step test, don't assume).
- **k — index of self-regulation**: ratio of the change in outflow to change in level at constant valve position (Ch. 1). k ≪ 1 in most tanks; the product k·τ1 stays constant as level changes, so τ1 and gain vary but their product doesn't. k = 0 → pure integrator (non-self-regulating).
- **Self-regulating vs non-self-regulating (integrating)**: the single most consequential classification in the book — it decides whether integral action is allowed (see Integral pairing rule in patterns.md).
- **τn — natural (undamped) period**; **τ0 — damped (observed) period**; **Pu — proportional band at undamped cycle** ("ultimate band", but Shinskey distrusts ultimate-sensitivity tuning).
- **γ — cyclic load sensitivity** (4.15): loop gain at a load period τq; peak γ ≈ 2–3 acceptable; γ peak location diagnoses mistuning (Ch. 4).
- **ti — inversion time** (drum level): time for a step response to recross its starting point; τn = 3.94·ti (9.26–9.28).

## Performance criteria
- **IE — integrated error**: ∫e dt = I·Δm/P (4.4). Economic interpretation: dollars of deviation.
- **IAE — integrated absolute error**: Shinskey's tuning criterion. Minimum-IAE guarantees damping; minimum-IE does not.
- **IAE_b — best possible IAE** for the process (dead-time floor): |Kp·Δq|·Td for load steps; |Δr|·Td for set-point steps (4.8).
- **e_b — best possible peak error**: Δq·τd/τ1 (integrating, 4.2); KpΔq(1−e^(−τd/τ1)) (self-regulating, 4.3). Tuning can never beat e_b by more than ~48% — the rest is feedforward's job.
- **ISE — integrated squared error**: rejected (unbounded in oscillating loops, no economic meaning).
- **σ — standard deviation** of controlled variable: statistical quality criterion; ±3σ spec violated 0.15–0.3% of the time.

## Interaction and structure
- **λ — relative gain (RGA)** (Bristol, Ch. 8): open-loop gain ÷ closed-loop gain of the same pairing. λ = 1 no interaction; 0 < λ < 1 costs period (detune); λ > 1 stiff set-point response; λ < 0 conditionally stable (never pair).
- **μ — relative disturbance gain** (11.20): (dm/m)/(dq/q) — how each candidate manipulated variable inherently rejects each load.
- **RIE — relative integrated error** (11.21): (μ1 + |μ2|)·λ — one-number comparison of pairing configurations.
- **Decoupler**: computation cancelling interaction; error tolerance shrinks as λ grows (Table 8.2: λ = 2 tolerates 41% decoupler error, λ = 16 only 3.3%).
- **Cascade**: secondary loop inside primary; secondary must be ≥ ~3–5× faster; primary never sees the secondary's lag.
- **VPC — valve-position controller**: a slow controller whose measurement is another controller's output (valve stroke); loads constrained resources to their limit (heat exchangers, distillation pressure, pH pacing).
- **Selective (override) control**: min/max selector; all controllers see the **selector output** as feedback — that's what prevents windup and makes transfer bumpless (Ch. 6).
- **Auctioneering**: highest-of-many selection (e.g. peak reactor temperature across catalyst beds).

## Energy and reactors
- **Kt — thermal steady-state gain** (10.20): dT/dTc = −UA/[UA + FρC − HrFx0(dy/dT)x]. Sign is the whole story: + self-regulating, ∞ non-self-regulating, − unstable.
- **τt — thermal time constant** (10.21): Kt·VρC/UA; negative τt = negative resistance (−180° phase lag at steady state).
- **Stability squeeze** (10.22–10.23): steady-state needs P < −100Kt; dynamic needs P > 100Kt·τd/τt; uncontrollable when τd/τt → −1 (practical limit −0.5).
- **Severity**: reactor temperature as the handle on per-pass conversion.
- **S — separation factor** (11.6): (y_i/x_i)/(y_j/x_j); constant S ⇔ constant L/D ⇔ constant V/F (11.15–11.18).
- **E — evaporator economy**, nE — vaporization per unit steam in an n-effect evaporator (≈ 0.94n).

## Hardware and measurement
- **Installed characteristic**: valve's actual gain vs travel once system pressure drop is accounted for; line pressure loss distorts linear valves toward quick-opening, gain factor (Apmin/Apmax)^(−3/2) (2.x).
- **Rangeability / turndown**: max/min controllable flow. Differential meters 6:1, metering pumps ~20:1, valves 35–100:1; two sequenced equal-percentage valves ≈ 2500:1 (Ch. 10).
- **Characterizer**: function generator at controller output to linearize an overall loop (inverse of valve+process curvature).
- **Ratio station**: multiplier in the **set-point circuit** (never a divider in the feedback loop); gain 0.3–3.0 midscale 1.0; with square-root meters set the ratio as the square root of the desired gain.
- **Lead-lag dynamic compensator** (7.29): instantaneous gain τ1/τ2, lag τ2; τ1 < 0 = negative lead approximating dead time; ratio capped at 10 (same reason derivative gain is limited).
- **α — completeness of mixing** (3.46–3.48): τd = (V/F)(1−α)/2, τ1 = (V/F)(1+α)/2; difficulty index τd/τ1 = (1−α)/(1+α) — independent of vessel size.
- **Buffering point**: pH = pKa, flattest part of a weak-acid titration curve (Ch. 10).

## Recurring Shinskey-isms
- "Measure the period, infer the process."
- "Dead time sets the floor on error."
- "Quarter-amplitude decay belongs to the past" (4th ed: tune to minimum IAE).
- "Controllability is a design variable, not a tuning skill."
- "The controller is a model of the process, reversed."
