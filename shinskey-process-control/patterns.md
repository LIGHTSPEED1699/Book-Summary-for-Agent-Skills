# Patterns — Shinskey, Process Control Systems (4th ed.)

Cross-chapter design patterns and diagnosis playbooks. Each pattern names when to use it, how, and where the book argues it.

## Design patterns

### 1. Measure the period, infer the process (Ch. 1, 4)
The closed loop resonates at its own natural period; disturbances excite that component and the loop rejects the rest. Pulse or cycle the loop, measure τn, and back out τd and Kp: for integrating processes τn = 4τd and Pu = 63.7·Kp·τd/τ1. Prefer closed-loop identification — the ratios I/τn, D/τn vary less across τd/τ1 than I/τd, D/τd, so a wrong τd/τ1 guess costs less (Table 4.6).

### 2. Dead time sets the floor on error (Ch. 1, 4, 7)
Best possible IE = |Kp·Δq|·Td; best possible peak e_b = Δq·τd/τ1 (integrating). A tuned PI peaks at 1.48·e_b, PID at 1.13·e_b — **tuning can never buy more than ~48%; the rest must come from feedforward or from designing dead time out of the process** (move the sensor, shorten sample lines, kill secondary lags).

### 3. Tune to minimum IAE; diagnose with phase and symmetry (Ch. 1, 4)
Quarter-amplitude decay is obsolete as a target. Minimum-IAE settings sit within ~10% of minimum IE while guaranteeing damping. Field checks: PI phase lag at minimum IAE is < 45° — if your settings imply more, you're mistuned. For PI on integrating processes, I should be 0.75 of the observed damped period; for PID, I ≈ 0.5 and D ≈ 0.18 of it.

### 4. The integral pairing rule (Ch. 4, 10, 12)
**Never put integral action on a non-self-regulating (integrating) process** — two integrators in the loop make phase approach 90° at long periods, windup is guaranteed, and set-point response overshoots. Use P or PD; add integral only when the process self-regulates (or when feedforward carries the load so the integral only trims computation error, Ch. 7). Corollary: a level/pressure loop with a shut-outflow batch valve has become integrating — retune accordingly.

### 5. Match valve characteristic to process gain curvature (Ch. 2, 3, 10)
Process gain falling with load (liquid pressure Kp = 2(p−p0)/F; temperature Kp = −(T0−Tc)/2F) → equal-percentage valve. Gain rising with load → linear or quick-opening. Temperature loops defeat both (gain falls as heat load rises but T0 depression breaks the equal-% match) — that's where a characterizer earns its cost. Always check the **installed** characteristic: system ΔP distorts linear valves toward quick-opening by (Apmin/Apmax)^(−3/2).

### 6. The controller as reversed process model — feedforward (Ch. 7)
Write mass and energy balances; solve for the manipulated variable in terms of loads; substitute set points for controlled variables. Needs a steady-state part (else offset) and a dynamic part (else transient). Integrals-of-flow processes (level, pressure) give **additive** compensation m = r + (Kq/Km)q; property processes (temperature, composition) give **multiplicative** m = r·q·(gq/gm)/Kp. Use the balances, not the heat-transfer coefficient: fouling changes the valve position required, not the steam flow demanded. Feedforward also **fails safe** where feedback fails wide-open.

### 7. Set point in the calculation, not in the loop (Ch. 6, 7, 11)
Dividers and gain-varying elements belong in the set-point circuit (ratio station r = R·q), never inside the feedback loop where loop gain rides the wild variable. Same principle for feedback trim on feedforward: **trim the set point, not the coefficient K** — one knob catches every error source, and the controller output becomes a readout of the forward loop's error.

### 8. Dynamic compensation recipe (Ch. 7)
Order matters: (1) apply dead-time compensation τd = τdq − τdm if τdm < τdq (if not, class III — compensation impossible before the dead time, still worth 3–5× IAE); (2) adjust τ1, τ2 to drive **IE to zero** (fixes τ1 − τ2); (3) adjust ratio τ1/τ2 at constant difference to minimize IAE. Cap τ1/τ2 at 10. Never put the compensator inside the feedback path.

### 9. Cascade: put the fast element inside (Ch. 6, 12)
Secondary loop ≥ 3–5× faster than primary; secondary sensor must see the primary's disturbance early. Watch the two-loop interactions: a lightly damped secondary can go undamped when the primary closes (primary derivative is the usual culprit); if secondary dead time exceeds primary's, the periods merge — flatten the secondary's resonant peak. In a cycling cascade, if the period is too short to be the primary's, widen the **secondary** band first. Batch reactors: cascade reactor temperature → **jacket outlet** temperature (not jacket temperature), feedforward feed rate onto the secondary set point.

### 10. VPC: load constrained resources to their limit (Ch. 6, 10, 11, 12)
When the economic limit is a saturated valve, wrap a slow valve-position controller around it: condenser duty → floating column pressure (I ≈ 1 h); reactor heat-transfer capacity → feed rate; pH reagent → pacing loop at 95% stroke. VPCs on systems with extra lags (reactor feed, exothermic severity) need all three PID modes and, for exothermic severity, **integral only** with a very long time constant (inverse response, Ch. 10).

### 11. Selective control with common feedback (Ch. 6)
Feed the **selector output** back to every controller's integral path. Unselected controllers degenerate to proportional (no windup); transfer happens when outputs are equal and the incoming error crosses zero — bumpless by construction. With derivative, e − D·dc/dt must cross zero, allowing early transfer. Variable structuring (condenser problem): move the constraint to a different valve via m_v = K(m_p − m_l), keeping the pressure controller closed throughout.

### 12. Pair loops with the RGA, break ties with disturbance gains (Ch. 8, 11)
Compute λ for every pairing: reject λ < 0 outright; prefer λ near 1 from above (λ > 1 doesn't cost period); 0 < λ < 1 works but needs detuning (Table 8.1: λ = 0.5 → gain product 0.707∠−135°). For columns, a 5×5 RGA is meaningless — reduce to 2×2 composition loops and use λ = 1 − [(dy/dx)1/(dy/dx)2] from operating-curve slopes (11.19). Then rank by RIE = (μ1 + |μ2|)·λ. Decouple only when λ is extreme — and check the decoupler error tolerance (Table 8.2).

### 13. Controllability is a design variable (Ch. 10)
For exothermic reactors, Kt and τt are functions of F, x0, UA. If τd/τt < −0.5 the reactor is uncontrollable **by tuning** — fix it by design: reduce F, reduce x0, raise UA. Same logic as dead time: when the floor is above the spec, change the process, not the controller.

### 14. Endpoint feedback where ratios can't be measured (Ch. 10, 12)
pH, color, titration endpoints: feedback on the final property in a well-mixed vessel with a fast, low-dead-time reagent system beats ratio/feedforward schemes when species vary. Buffering (pH = pKa) is a gift — weak acids are 100× easier than strong. Rangeability, not gain, is the binding constraint: sequence two equal-percentage valves (≈ 2500:1), only one open at a time.

### 15. Batch = PD biased for load (Ch. 12)
At zero load the process integrates and overshoot is permanent, so the integral mode is structurally wrong for the approach phase: P = 120τd/τ1, D = τ2 + 0.5τd, derivative on the controlled variable. If integral is mandatory, preload it just below the anticipated load and/or delay it until ~τd before arrival. Ramp following: PD both-on-deviation (P = 120τd/τ1, D = 0.45τd) tracks ~1.2τd late with no overshoot.

### 16. Inferential control from a model (Ch. 11)
When quality can't be measured (dryer moisture), compute a surrogate set point from measured variables via the mass-transfer model: T*0 = r + R·Ti (11.41). The surrogate loop is positive feedback — steady-state stability requires R's sign right, dynamic stability requires a lag longer than the inner loop's integral time.

## Diagnosis playbooks

### Limit cycle (sustained oscillation, no external periodicity)
1. **Period ≈ loop natural period** → ordinary mistuning or gain drift; check γ peak.
2. **Period much longer than natural, clipped-sine in m, triangular c** → dead band + PI with gain rising as amplitude falls (Table 5.2: cycle onset at A/a ≈ 3.3). Cure: shrink dead band (smart positioners), or P control (gain falls with amplitude — Table 5.1 — stable everywhere).
3. **Period ~2–3× loop period, sawtooth** → velocity limiting or DC-drive stall band (drives stall < 5%, restart at 10%).
4. **Short hot excursion + long cold stretch, coolant loops** → secondary dead time varying with flow + nonlinear temp-flow (Ch. 10 circulating coolant).
5. **Two peaks (near 3τd and 9τd)** → unstable exothermic reactor (negative resistance); widening the band trades one peak for the other — go to design fixes (pattern 13).
6. **Cycle only when cascade closed, period too short for primary** → secondary resonant peak; widen secondary band.

### Overshoot after every set-point step
- Integral action on an integrating process (pattern 4) — set-point changes need no integral there.
- P acting on error instead of deviation; derivative on error instead of measurement.
- Fix: lag the set point by exactly I, or bumpless manual transfer through the step.

### Loop "too slow" at low load, fine at design load
- Gain scheduling failure: process gain ∝ 1/F (liquid pressure) or ∝ F (multiplicative systems) with the wrong valve characteristic.
- Or P was set from an open-loop τd estimate that actually measured τ2 + τd (overestimates P when τ2 > 0.2τd).

### Windup signature: saturation, then overshoot on recovery
Integral feedback through a lag keeps integrating while the output is clamped; control cannot resume until error reverses. Cure: batch unit + preload in the feedback path (Ch. 4), back-calculation from measured flow (Ch. 7 drum boiler), or selector-output common feedback (Ch. 6).

### Composition/purity loop: slow at low impurity, overshoots on upscale
Process gain ∝ impurity concentration (Kp = k·c). Use logarithmic error e = ln c − ln r (11.24); accept that IE of equal-and-opposite upsets is no longer zero.

### pH loop hunting across the neutral point
Strong-acid/strong-base neutralization is a 1-in-10,000 rangeability problem, not a gain problem. Check: electrode lag (precipitate films stretch the period to > 1 h — clean the probe), reagent sequencing (only one valve open), and whether buffering can be added. Don't tune around it.

### Drum level inverse response
Step in feedwater → level first dips (bubble volume collapse). Measure the **inversion time ti**; τn = 3.94·ti sets the tuning. Three-element control = feedforward steam flow + level trim (pattern 6's additive form, bias 0.5).

### Oscillation propagating down a train of identical units
Each unit's γ peak amplifies the load component at ~6τd; the train multiplies it. Detune to peak γ 2–3, or break the periodicity with feedforward/ratio control at the source.
