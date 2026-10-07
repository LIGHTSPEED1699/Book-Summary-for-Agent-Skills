# Chapter 3: Analysis of Some Common Loops

## Core Idea
Control loops fall into three physical families, and the family predicts the difficulty. Flow has the manipulated variable equal to the controlled variable, so it is the easiest loop to reason about. Level and pressure are the *integral* of flow: capacity-dominated, rarely dead-time-limited, and the only ones that can be non-self-regulating. Temperature and composition control a *property of a flowing stream*, which must be transported to the sensor — so dead time is always present, and the loop is slow and hard. Everything the rest of the book says about tuning assumes you have first placed the loop in one of these families.

## Frameworks Introduced
- **Loop classification** (do this first, every time):
  - Flow: manipulated variable = controlled variable. Full measure, no dead time, noise always present.
  - Level / pressure: the integral of flow. Dominated by capacity, non-self-regulating possible, pressure waves travel at sonic velocity so dead time is rare.
  - Temperature / composition: controlled variable is a property of the stream, so transportation dead time is unavoidable; usually dead-time dominated.
- **Inertial lag of a flow loop** (why a flow "gain of 1" is not instantaneous):
  - Valve throttling at constant Δp: **τ = LFρ/(2gAΔp)** (3.3) — varies *directly* with flow.
  - Speed control at constant resistance: **τ = LAa²/F** (3.2) — varies *inversely* with flow.
  - Consequence: speed-controlled flow is sluggish near zero flow (long τ) but far more controllable at load; a valve is the reverse. Verified in Fig. 3.1: the motor held with a **30%** proportional band, the same loop through an equal-percentage valve needed **200%**, because of the valve's dead band and velocity limiting.
- **Statistical error combination for a measurement chain**: RMS, not arithmetic, and only for statistically independent sources. σ-figures: a ±3σ spec is exceeded 0.3% of the time; combining two ±3σ signals gives 0.0009% for both at once. To keep the confidence level of a sum, combine by root-mean-square, keep the basis consistent (% of full scale vs % of value), and include every scaling/amplifying function.
  - Non-linearity must be differentiated first: for a head flowmeter, Δp = f² (3.8) so d(Δp) = 2f·df (3.9); square-root extraction inverts it, d√h = dh/(2√h) (3.11); a multiplier contributes d(hp) = √[(ks p·dh)² + (ks h·dp)² + e_m²] (3.13).
- **Hydraulic resonance** (why a level loop is not single-capacity): any open liquid surface with a measuring chamber is a resonant element. Natural period **τn = 2π√{[L₁ + (L₂ − L₁)/a(1 + A₂/A₁)]/g}** (3.21); with a = 1 and A₂ ≪ A₁ it reduces to τn = 1.107√L (familiar π√(L/g) form).
  - It contributes 90° of phase lag at its natural period, which completes the 180° a proportional level controller needs to cycle.
  - **Resonant gain (Q factor)** must be known because it caps controller gain. Estimatad from the decay ratio δ; the refined form is **Gn = Gn1/[1 − 1/(2Gn1)²]** (3.24), usable to three significant figures for δ > 0.25. Gn < 1.0 means the element is overdamped.
  - Amplitude of the resulting limit cycle falls inversely with proportional band, and the longest-period resonance dominates (shorter ones scale down by the 3/2 power of length).
- **Composition mixing model** (incompleteness of mixing as a dead time + lag): with α = completeness of mixing (0 = none, 1 = perfect), a step response is a staircase, and connecting the midpoints gives **τd = (V/F)(1 − α)/2** and **τ₁ = (V/F)(1 + α)/2** (3.46–3.47). Every curve passes through 0.632 at t = V/F, so the measurement point is insensitive to α. The difficulty index **τd/τ₁ = (1 − α)/(1 + α)** (3.48) is independent of vessel volume — a large vessel with good agitation is as easy to control as a small one.

## Key Concepts
- **Level control serves two different purposes and they want opposite tuning.** (1) Hold level *at set point* — boiler drum, where high level carries water into steam and low level overheats tubes — needs integral action. (2) *Close a material/energy balance* — the set point is meaningless. Integral action then always slows and destabilizes the loop, and for a **surge tank** it is actively wrong.
- **Surge tanks: P = 100%, no integral, no controller needed.** A tank feeding downstream should be full when production is high and empty when it is low, so that its whole volume can absorb the next upset. Returning level to 50% in steady state halves the effective capacity. Wire the level transmitter straight to the valve through an automanual station, use a linear valve at constant Δp, and the closed-loop time constant equals the open-loop one. Reverse-acting valves need a reversing relay for negative feedback.
- **Manipulated-flow time constant under proportional level control: τm = τ₁·P/100** (3.28) — at P = 100% the flow responds with the vessel's own time constant (surge tank); for a reflux accumulator P must be as small as possible because distillate/composition control depends on reflux answering a distillate change immediately.
- **Level cycle vs flow cycle**: level amplitude falls as 1/P but the manipulated-flow amplitude falls as **1/P²** (3.29–3.30). For balance closure (where flow smoothness is what matters) the practical procedure is: widen P until the *flow* cycle is acceptable, then add integral action to shorten the flow time constant — bearing in mind integral time cannot be shortened enough without causing overshoot and slow cycling.
- **Dynamic filtering of level**: a first-order filter of gain Gf = 1/√[1 + (2πτf/τn)²] (3.31) attenuates the limit cycle. To keep the manipulated flow from overshooting, keep **P > 200τf/τ₁** (3.33); filter time determines level cycle, band determines flow cycle (both appear squared in the flow expression). Selection is trial and error: pick τf, solve P from 3.33, estimate the flow cycle, adjust τf, iterate — then compute τm.
- **Gas pressure is single-capacity and easy**: p is the integral of flow (3.14), self-regulating except at zero flow, and a self-contained regulator at ~5% proportional band is often enough. It exhibits **droop**: pressure varies with flow, with extra pressure needed for shutoff near zero flow. Use a **linear** valve — an equal-percentage characteristic is wrong here, because the valve's two pressures are nearly constant.
- **Vapor pressure** needs both balances: mass flow (FiHi − F0H0) and heat flow (Qi − Q0) enter through the heat of vaporization (3.15). Where net enthalpy change is zero (wet-steam letdown), mass flow alone controls.
- **Liquid pressure is flow control**: Kp = 2(p − p₀)/F (3.17) falls inversely with flow → equal-percentage valve for load regulation. Where line resistance is not variable, loop gain is constant and a linear valve is correct.
- **Composition: dead time travels with the stream, so it is always in the loop.** Sample transport dominates the analysis speed; analyzers that avoid sampling (conductivity, density, pH) are the exception. Discontinuous analyzers (chromatographs) periodically interrupt the loop. Sample-line dead time is constant, so the natural period is nearly constant and dynamic gain is nearly constant — except when the process is nothing but a pipeline.
- **Composition process gain**: adding concentrate X to diluent F gives x = X/(F + X) (3.49) and Kp = F/(F + X)² (3.50), which reduces to Kp ≈ 1/F when X ≪ F (low concentration — which is why minor components are measured). Manipulating F instead gives Kp = x(1 − x)/F (3.53), whose variation with x may need nonlinear compensation.
- **Temperature is a heat-transfer problem**: the worked example is deliberately parameter-constant — a stirred-tank reactor with once-through jacket water — yet it is four-capacity plus dead time (reactor contents, wall, jacket contents, bulb; plus circulation dead time). τ₁ = MC/UA (3.56) from the unsteady heat balance (3.55); UA is obtained from a steady-state balance with the log-mean temperature difference, UA = FCc ln[(T − Ti)/(T − T0)] (3.58). Sensor lags run 0.5 s (thermocouple) to 8 s (nitrogen-filled bulb) and a thermowell pushes the pair to 8–100 s; in practice lump all minor elements as dead time and measure it with a step test.
- **Temperature gain moves the wrong way for compensation**: Kp = −(T₀ − Tc)/(2F) (3.59) and T₀ is depressed below the controlled temperature linearly with heat load (3.60), so process gain falls as heat load rises. Neither valve characteristic fits: linear loses gain with load, equal-percentage gains it back too aggressively (over a 3:1 heat-load range, process gain fell 3:1 while the equal-percentage gain product rose 3:1). Ideal compensation lies between, achieved with a divider on an equal-percentage valve or by adapting the proportional band with the measured T₀ − Tc.

## Mental Models
- **Ask what the controlled variable IS.** A stream, the integral of a stream, or a property travelling with a stream. That single question sets the dead time, the capacity, and the achievable period.
- **Resonance, not capacity, is what limits a level loop.** The integrator gives 90°; the surface gives the other 90°. Level controller gain is capped by the resonant gain, not by the vessel.
- **A set point is a decision, not a default.** Boiler drum, reflux accumulator: the level matters. Surge tank: it does not, and forcing it to 50% throws away half the tank's usefulness.
- **Volume is not difficulty.** With equivalent agitation, τd/τ₁ depends only on the completeness of mixing, so scale is irrelevant to controllability.
- **Droop is proportional control on a pressure regulator**, exactly as offset is proportional control on any loop: it is the same physics wearing a different name.

## Anti-patterns
- **Adding derivative to a flow loop** — flow noise is always present and too fast to correct; derivative acts on it.
- **Using integral action on surge-tank level** — defeats the purpose and destabilizes; a surge tank wants P = 100% and nothing else.
- **Assuming a linear valve is right because the process "seems linear"** — liquid pressure with variable line resistance needs equal-percentage (gain ∝ 1/F), gas pressure needs linear.
- **Estimating a measurement chain's error by adding the accuracies** — that overstates the error badly; combine statistically and only after differentiating any nonlinear relation.
- **Treating a level loop as single-capacity** — the measuring chamber and the free surface add a resonant element that will cycle at its own natural period.

## Reference Tables
Table 3.3 — Properties of common loops (the chapter's summary):

| Property | Flow / liq. press. | Gas & vapor press. | Liquid level | Composition | Temperature |
|---|---|---|---|---|---|
| Dead time | No | No | No | Constant | Variable |
| Capacity | Multiple | Single | Single | 1–100 | 3–6 |
| Period | 1–10 s | 0–2 min | 1–10 s | min–hours | min–hours |
| Linearity | square/linear | linear | linear | linear/log | nonlinear |
| Noise | always | none | **always** | often | none |
| Proportional band | 100–500% | 50–200% | 0–5% | 5–50% | 100–1000% |
| Integral | essential | unnecessary | seldom | essential | yes |
| Derivative | no | unnecessary | no | if possible | essential |
| Valve | linear / equal-% | linear | linear | linear | equal-% |

Table 3.1 — error estimate for a 1% orifice with a 0.25% Δp transmitter (all in % of full-scale flow): f = 100 → df 1.00, d(Δp) 2.00, dh 2.02, d√h 1.01; f = 20 → 0.20, 0.08, 0.26, 0.66; f = 10 → 0.10, 0.02, 0.25, **1.25**; f = 5 → 0.05, 0.005, 0.25, **2.50**. The flow element dominates at high flow, the transmitter at low flow — that is the rangeability limit of a head flowmeter, and the reason for a second, lower-range transmitter.

## Worked Example
**Ex. 3.2 + 3.3, a level loop with a measuring chamber** (180 gal vessel, 2.0 ft diameter, normal level L₁ = 3.6 ft, chamber 0.5 ft diameter at L₂ = 4.4 ft, a = 0.5, maximum flow 50 gal/min): A₂/A₁ = 0.0625 → **τn = 2.50 s**; the resonant coefficient gives Kn = 1.93; vessel time constant τ₁ = (180/50)·60 = 216 s. With P = 10%, the limit cycle is |h₁ − h₂| = 1.93·(100/10)·(2.50/(2π·216)) = **0.036 ft**.
Adding a filter: with τf = 3 s, Gf = 0.131, P from 3.33 = **2.8%**, and the manipulated-flow cycle |dm| = 13.9 (%/ft) · 1.93 · (100/2.8) · 0.0018 · 0.131² = **1.06%** — the filter plus a narrow band holds a tight flow cycle that proportional control alone could not.
