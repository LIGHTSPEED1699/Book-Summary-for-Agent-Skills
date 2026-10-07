# Chapter 2: Characteristics of Real Processes (Analyzing Real Processes)

## Core Idea
Real processes are combinations of dynamic elements (lags, dead time, capacities) and steady-state gains (valve, process, transmitter). Secondary lags behave almost like dead time; interacting lags reshape time constants; and the whole loop can be characterized quickly with a two-test procedure — open-loop step for effective dead time, closed-loop P-control for natural period — instead of days of frequency-response testing.

## Frameworks Introduced
- **Secondary-lag equivalence (4th ed: expanded)**: a small second capacity in a loop with an integrating capacity affects the loop much as dead time does, as long as τ2 < Td. Natural period barely changes (Table 2.1: τn stays ≈ 4Td for φ2 up to −40°); dynamic gain changes more. Approximating a two-capacity-plus-dead-time process as single-capacity-plus-dead-time gives **safe** controller settings; do not use when τ2/Td > 1.
- **Proportional-plus-derivative (PD) control (4th ed: full treatment incl. multi-derivative filtering)**: derivative contributes phase **lead** (opposite of integration). Ideal derivative gain grows without bound at short periods → practical gain limit of **10–20**, which turns the derivative into a lag of time constant D/(gain limit).
  - When to use: batch heating/composition adjustment where final valve position is known (set bias b there); canceling a known secondary lag; never where integral action is needed for regulation.
  - How: setting D = τ2 cancels the secondary lag but leaves a residual lag τ2/10–τ2/20. To kill overshoot on the controlled variable without slowing response: **D = 0.3τ2**; on the intermediate variable: **D = τ2**; with dead time present, increase D by **0.5Td**.
- **Noninteracting vs interacting lags**:
  - Noninteracting (isolated, e.g., pump-coupled tanks, amplifier in electrical analog): each lag keeps its own time constant; n equal lags each contribute 180°/n phase; τn = 2πτ/tan(180°/n); as n grows, the bank of lags approaches **dead time** (τn → 2πτ, gain product → 1).
  - Interacting (coupled, e.g., gravity-drained tank series, RC ladder): interaction always **increases the largest time constant and decreases the smaller**. Two equal interacting lags τ → 2.618τ and 0.382τ. For n equal interacting capacities: sum of effective time constants = (n²+n)/2·τ; product = τⁿ.
  - Degree of interaction ∝ ratio of smaller to larger **capacity** (not time constant); ratio < 0.1 → treat as noninteracting. Measuring-element lags (thermowell bulb, chamber) are almost always noninteracting.
- **Lumped model of multicapacity processes (Ziegler–Nichols maximum-slope construction)**: draw the tangent at maximum slope of a step response; its intersection with the baseline = **effective dead time**; τn = 4 × effective dead time (holds even with a small secondary lag). For n equal interacting lags, effective τd/τi approaches ~0.133 as n grows; τd + τi = total lag; τd = total lag/(1 + τi/τd). A series of ≥10 interacting lags ≈ one large lag + dead time.
- **Dimension heuristic**: τd/τi ~ length/diameter — a tower indicates dead time; a squat tank indicates lags.
- **Variable time constants**:
  - Tubular heat exchanger: gain, τ, and Td all vary inversely with flow → period and loop gain vary inversely with flow; overdamped at high flow, unstable at low flow. **Tune for the worst case: lowest anticipated flow.** Compensate with equal-percentage valve, adapted settings, or feedforward.
  - Head tank in turbulent flow: τ2 varies **directly** with flow (τ2 = 2A2/k2²·F1) — opposite compensation needed (valve selection or cascade).
  - Growing period over time = fouling/crust (heat exchangers, polymerization reactors, pH electrodes).
- **Steady-state gain chain KvKpKt is dimensionless**:
  - **Transmitter gain Kt = 100%/span** (units %/measurement). Narrowing span raises loop gain — for control, the vessel beyond the transmitter span does not exist.
  - Differential flowmeter: h = f² → Kt = 2f·(100%/span); gain halves at 50% flow → use a square-root extractor.
  - **Linear valve Kv = Fmax/100%**; **equal-percentage valve** f = R^(m−1), gain Kv = lnR · f · Fmax/100% — gain proportional to actual flow, independent of valve size within range. R = 50 → slope 3.9 at full flow.
- **Installed characteristics**: system pressure-drop loss distorts a linear valve toward quick-opening; gain change across travel = (Apmin/Apmax)^(−3/2) → factors 31.6, 11.2, 6.1 for Ap ratios 0.1, 0.2, 0.3. Equal-percentage valves resist distortion (installed curve becomes more linear) — hence their predominant use.
- **Divider linearization of equal-percentage valve**: f(m) = m/[z + (1−z)m]; gain variation over range = 1/z²; match to valve rangeability with **z = 1/√R** (z = 0.141 for R = 50).
- **Simplified two-test procedure** (see Reference Tables) — the chapter's centerpiece.

## Key Concepts
- **Effective dead time**: intercept of the maximum-slope tangent with the baseline; lumps true dead time plus small secondary lags.
- **Rangeability R**: ratio of maximum to minimum controllable flow; equal-percentage gain variation equals its rangeability.
- **Total lag**: sum of effective time constants (Eq. 2.13); conserved by interaction.
- **Loop gain at τn**: what actually matters — the product KpGpKtKvKc at the natural period, not any single steady-state gain.
- **pH process gain**: use the slope of the line from the deviation point to zero (chord), not the local tangent; Kp at the set point sets damping, and gain falls at larger deviations, retarding recovery.

## Mental Models
- **Think "dead time vs lag" from geometry**: long-and-thin equipment (towers, exchangers, pipelines) = dead-time dominant; squat vessels = lag dominant.
- **Interaction redistributes, never destroys, lag**: the sum of effective time constants is fixed; one grows, others shrink.
- **A bank of 10+ interacting lags is a lag + dead time; a bank of 10+ noninteracting lags is dead time.** Pick your lumped model accordingly.
- **Test at the natural period, not at rest**: closed-loop P-control probes the process exactly where stability lives; open-loop step-response tests waste time and lie about nonlinear processes.

## Anti-patterns
- **Frequency-response plant testing** (objections: unbelievably time-consuming; assumes linearity and invariance — misleading on real processes). Reserve it for fast linear devices (instruments, controllers).
- **Testing for steady-state gain or time constants alone**: both vary with flow while their product stays constant; tests on nonlinear processes are meaningless.
- **Equal-percentage valve on a pH loop**: the valve acts on the controller output, not the measurement — it cannot correct the pH curve's nonlinearity and makes loop gain worse (gain = lnR·f; at f > 0.25 it exceeds a linear valve; at f = 0.5 it doubles the required proportional band).
- **D = τ2 with an unfiltered derivative**: the gain limit leaves a residual lag; and derivative on noisy measurements amplifies noise (gain limit 10–20 exists for this reason).
- **Tuning at design flow**: heat-exchanger loops go unstable at low flow; tune for the worst (lowest) flow.

## Reference Tables
**Diagnosis from the two-test procedure** (Td = effective dead time from open-loop test; τn = natural period from closed-loop P test):

| τn / Td | Process |
|---|---|
| = 2 | Pure dead time |
| 2 – 4 | Dead time dominant; estimate τd/τ1 from Fig. 1.20 |
| = 4 | Single dominant capacity |
| > 4 | More than one capacity |

Pu (undamped proportional band) = gain product of all other loop elements at τn; then KpKvKt = Pu/(100·G₁…).

**Table 2.1 (two-capacity + dead time)**: φ2 = −10°/−20°/−30°/−40° → τn/(Td+τ2) = 3.995/3.962/3.868/3.671 — natural period nearly constant; G₁G₂ falls 0.626→0.448.

**Table 2.2 (n equal noninteracting lags)**: n = 3 → τn/τ = 1.21, ΠG = 0.125; n = 10 → 1.93, 0.605; n = 100 → 2.00, 0.952 (→ dead time).

**Interacting equal lags**: n = 2: 2.618τ + 0.382τ (sum 3τ, product τ²); n = 3: 5.0505τ + 0.6405τ + 0.3090τ (sum 6τ, product τ³).

## Worked Example
**Neutralization loop case history (3ed, pp. 69–71)**: pH controller stuck in manual.
1. Open-loop test: effective Td = 40 s (15 s sample piping + mixing lag).
2. Closed-loop P test: uniform oscillation at Pu = 150%, τn = 2.8 min → τn/Td = 2.8/0.67 = 4.2 ⇒ single capacity + dead time.
3. Known: V/F = 200 gal / 2.5 gpm = 80 min → G₁ = 2.8/(2π·80) = 0.004.
4. KpKvKt = Pu/(100·G₁) = 150/0.4 = **375**; Kt = 100%/10 pH = 10%/pH → KpKv = **37.5 pH/%** — extreme process gain, typical of neutralization.
5. Fix 1: repipe sample line → Td = 30 s → period and required band scale down by 30/40 (τn → 2.1 min, band × 0.75).
6. Fix 2 (diagnosis): loop got sluggish at lower load — equal-percentage valve at constant ΔP made loop gain ∝ flow; at 50% fractional flow its gain is 2× a linear valve. Replace/resize accordingly (a valve cannot linearize the pH curve itself).
Total test time: minutes, with two actionable recommendations.

## Key Takeaways
1. Small secondary lags ≈ dead time (if τ2 < Td); lump them and the approximation is safe.
2. Interaction: bigger lag gets bigger, smaller gets smaller; sum of effective time constants is conserved.
3. Two tests — open-loop step (Td) + closed-loop P (τn, Pu) — characterize any troublesome loop; τn/Td diagnoses the element mix.
4. Loop gain = KvKpKtKc; transmitter span and valve style are tuning parameters, not innocent hardware choices.
5. Equal-percentage valve: gain ∝ flow (lnR·f); use it to cancel processes whose gain ∝ 1/flow (heat exchangers); never to "fix" pH.
6. Variable time constants are the rule; tune for the worst-case operating point.
7. Derivative lead cancels a known lag: D = 0.3τ2 (controlled variable) or τ2 (intermediate), +0.5Td if dead time present.

## Connects To
- **Ch 1**: element gains/periods used throughout this chapter; Fig. 1.11/1.20 corrections for damped tests.
- **Ch 3**: applies this analysis to the five common loops.
- **Ch 4**: PID tuning rules for second-order-lag-plus-deadtime (4th ed develops these fully here).
- **Ch 5**: nonlinear elements (pH curve, negative resistance) that the test procedure exposes.
- **Ch 6**: cascade as compensation for variable time constants; valve positioners vs amplifiers.
- External: Ziegler & Nichols (1942) maximum-slope method; RC ladder networks.
