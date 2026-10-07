# Chapter 12: Batch Process Control

## Core Idea
Batch processes break the two assumptions continuous control rests on: that a load always exists to return the variable to set point, and that overshoot is reversible. At zero load the process becomes non-self-regulating, overshoot is permanent, and the integral mode — which positions the output on accumulated error — guarantees it. Hence the batch controller is a PD controller biased for the known load, and everything else in the chapter (endpoint control, fed-batch, ramp following, reactor cascades, batch distillation, batch drying) is that same idea applied where the load is unknown, variable, or must be driven to a constraint.

## Frameworks Introduced
- **Zero-load tuning rules** (the base case):
  - Proportional band for a two-capacity process with dead time, valid at zero load and good at others: **P = 120τ_d/τ₁** (12.1).
  - Derivative must additionally cover the secondary lag: **D = τ₂ + 0.5τ_d** (12.2).
  - When to use: any filling, heating, or endpoint phase where no outflow exists.
  - How: derivative must act on the **controlled variable**, not the output. A feedback-lag (single-stage pneumatic) derivative gives no action while the output is saturated — exactly when it is needed.
- **Any level/pressure/capacity process becomes non-self-regulating at zero load**: shut the outflow valve (k = 0) in h = (F/V)∫(f_i − k)dt (12.3) and both the time constant and the gain go to infinity; the tuning rules above then apply unchanged to a self-regulating process too.
- **Batch endpoint (titration) control**: the mixing process of Fig. 12.2 becomes an integrator at zero outflow (dx/dt = F₁m x₁/V, 12.6).
  - When to use: neutralization, pH adjustment, any batch made to a composition spec.
  - How: PD control biased for **zero reagent flow** at set point, on an equal-percentage valve (a perfect match if the titration curve is logarithmic). Tune conservatively: undershoot can be corrected by more reagent, overshoot cannot. Pulse the valve at a moderate pH to find dead time + lag; set D to their sum, then narrow P for minimum batch time without overshoot.
- **Fed-batch / variable-volume composition control**: with both streams added concurrently under ratio control, V·dx/dt + (F₁ + F₀)x = F₁x₁ + F₀x₀ (12.7–12.8) is a first-order lag whose time constant is V/(F₁+F₀). The steady-state gain also falls with total flow, so **controller gain should be scheduled on vessel level (volume), not flow** — the bathtub model: early on, flow ratio moves temperature easily; as it fills, ratio changes have almost no effect.
- **Load-compensated tuning** (radiant/slab heating): process time constant = MC/UA; the cooling load k is found from the steady state (dT = 0) and the controller biased to the steady-state heat load for any temperature setting (12.10). Radiant heating replaces temperatures with their fourth powers; core temperature lags surface, so the batch is "soaked".
- **Batch PID with integral preload** (blueprint: Fig. 4.6): integral feedback is opened while the output is saturated and its bias preloaded just below the anticipated load, so integration begins the moment the output leaves its limit — a purpose-built cure for integral windup at startup.
- **Set-point ramping**: any controller that follows a ramp closely overshoots at the end. Best: **PD with both modes on deviation**, P = 120τ_d/τ₁, D = 0.45τ_d → tracks the ramp delayed ~1.2τ_d with no overshoot. If integral cannot be dropped, use **D > I** (P = 360τ_d/τ₁, I = 0.55τ_d, D = 1.9τ_d; Table 12.1) — parallel to the ramp, ~2τ_d late, minimal overshoot, but ~30% worse IAE on load rejection. Where the ramp rate itself is the manipulated-variable index, a slope-feedforward controller (Fig. 12.7) tracks exactly with τ_d delay.

## Key Concepts
- **Optimal switching vs PD**: optimal switching (dual-mode) gives minimum-time-to-set-point because it holds full power to the last moment; but with a secondary lag the load-dependence of the switching point (12.11) makes it **less robust** than PD, it needs a dead zone (offset), and at zero load its deceleration advantage disappears. PD is almost as good even when τ₂ = τ_d. Robustness ranking: PD > dual-mode.
- **Controller table for batch (Table 12.1)**: no-batch two-stage PID (P 360τ_d/τ₁, I 0.55τ_d, D 1.9τ_d) IAE/IAE_b = 2.63; batch one-stage (P 173τ_d/τ₁, I 1.57τ_d, D 0.57τ_d, preload q−4%) = 1.99; batch two-stage (P 110, I 2.0τ_d, D 0.57τ_d, preload q−10%) = 2.48; batch two-stage delayed-I (P 110, I 1.57τ_d, D 0.45τ_d) = 2.47.
- **Delayed integral**: delay integral action until the controlled variable approaches set point (~τ_d after the output leaves its limit, which is also the optimum integral time for load rejection). Removes overshoot from the startup path; costs 22% higher IAE after a load step because the startup-optimal D (0.45τ_d) is below the load-rejection D (0.57τ_d).
- **Self-tuning controllers do not suit batch**: they learn from a disturbance trial, but a batch gets one shot, and each batch may differ. Only simple dynamically-unchanging units (ovens, extruders, water baths) are candidates.
- **Batch reactor temperature**: cascade — primary on reactor temperature, secondary on **jacket outlet temperature** (not jacket temperature) — with feedforward from feed rate or catalyst volume through a dynamic compensator onto the secondary set point (K_F positive for endothermic, negative for exothermic). If a limit is hit (heating valve locked out, coolant saturated), use **secondary temperature for primary feedback** to avoid primary windup and a limit cycle.
- **Auxiliary cooling coordination**: a valve-position controller (VPC) set for 90% open admits coolant to the coil only after the jacket valve is nearly full open; the VPC needs all three modes, is tuned after the cascade, and the jacket loop stays closed throughout. Same VPC pattern overrides feed rate when the product-gas bypass valve or coolant valve saturates (Fig. 12.10) — run the HC station at 100% and let the constraint arbitrate, for maximum constrained production.
- **Batch distillation**: only one product at a time, so composition-loop interaction disappears and **distillate-composition programming** replaces it. Operate at the vapor/liquid traffic limit (fixed heat input or ΔP control); no reflux accumulator (holdup becomes slop); leave pressure uncontrolled and as low as possible, compensating the temperature measurement for pressure.
  - Constant D/V ⇒ constant separation ⇒ variable distillate composition; the controlled variable is the receiver's **average** ȳ (12.14), and withdrawal stops when ȳ reaches spec — poor recovery if D/V is high, slow and wasteful if low.
  - Constant-composition control: D/V starts high and falls to zero; integral action required on the temperature controller.
  - **Optimal policy** lies between the two: y* = kD + y₀ (12.15), implemented as a set point computed from distillate flow (negative-signed sum into the divider, since falling purity means rising temperature); it is a negative feedback loop, so stability is not an issue. Terminate when distillate value rate equals operating cost (Fig. 12.13); each additional cut adds a slop cut, so recovery fraction falls with cut count.
- **Batch drying ending by inference**: x = K·x_c·ln[(T_i − T_w)/(T_0 − T_w)] (12.16); estimate T_w from the constant-rate plateau T_oc, then compute T_0f = T_oc + K_x(T_i − T_oc) (12.17), storing it before the batch. Constant-rate drying: rate ∝ (T − T_w), independent of moisture, until the critical moisture x_c; then falling-rate, where outlet temperature rises as the driving force rises. End the batch when T_0 reaches the stored T_0f. K_x is a per-product calibration (particle size, drying curve): too wet ⇒ K_x too low. Air humidity and dew point offset T_w and T_0c together, so it is self-compensating; surface-area change is only partly compensated (worked example: half area ⇒ 170.4°F termination and 0.028 final moisture vs 0.02 spec, instead of 0.04 had T_0f not been recalculated).
- **Drying lumber (kiln)**: hold a constant inlet–outlet temperature **difference** (rate limit against case-hardening) by manipulating steam; the difference controller manipulates steam flow until falling rate begins, then the inlet temperature controller takes over through a low-signal selector. Airflow reverses every 3 h with signal selectors (high-to-positive, low-to-negative) so the subtractor is always right; controllers go to manual during fan reversal. Heat recovery by recycling exhaust on a dew-point-controlled basis; do not change dew point mid-batch.

## Mental Models
- **Zero load ⇒ integrator ⇒ overshoot is forever**: every batch rule follows from one physical fact. Ask "what happens to the output when the error reaches zero with no outflow?" before choosing modes.
- **Bias is the batch analogue of reset**: a PD controller's bias is the steady-state load; if the load is zero, bias is zero. The whole point of the preload in a batch PID (and of the feedforward term on a reactor) is to hand the integral mode a correct starting point instead of one accumulated from startup error.
- **Favor the exotherm**: where a reaction changes character, configure the controls for the exothermic case and degrade them for the milder ones.
- **Time beats precision under a constraint**: run the constrained variable at its limit (VPC at 90%, HC at 100%) and let whichever constraint binds take over feed rate — maximum production inside the physical envelope.

## Anti-patterns
- **Integral action on a zero-load or batch startup phase** — guarantees overshoot; the error accumulated during the approach is large and the output cannot be zero when it arrives.
- **Using the ramp to fix overshoot** — reducing ramp rate only shrinks overshoot, never removes it; pick the right controller first, then tune it.
- **Controlling temperature directly from feed rate (no VPC)** — two large lags in series, plus accumulation of unreacted feed if the reaction is not yet initiated; dangerous and difficult.
- **Optimizing an exothermic reactor by manipulating temperature set point** — inverse response; the VPC needs only integral action and such a long integral time that the valve crawls. Use periodic (sampled) set-point increments instead, with the sample interval 2–3× the temperature loop period.
- **Controlling batch-column pressure** (by flooding or any means) — wastes cycle time and distillate yield, which fall linearly with rising pressure; float it low and compensate the temperature reading instead.
- **Changing air dew point or inlet conditions mid-batch** — invalidates the stored T_0f calculation.
- **Leaving the reflux accumulator in a batch still** — holdup becomes a slop cut; a slop cut is lost production and cost.

## Reference Tables
Table 12.1 — Batch controller settings and load-rejection IAE (all P in units of τ_d/τ₁):

| Controller | P | I | D | Preload | IAE/IAE_b |
|---|---|---|---|---|---|
| No batch, two-stage | 360 | 0.55τ_d | 1.90τ_d | none | 2.63 |
| Batch, one-stage | 173 | 1.57τ_d | 0.57τ_d | q − 4% | 1.99 |
| Batch, two-stage | 110 | 2.00τ_d | 0.57τ_d | q − 10% | 2.48 |
| Batch, two-stage, delayed I | 110 | 1.57τ_d | 0.45τ_d | q | 2.47 |

## Worked Example
**Batch fluid-bed dryer**: product moisture 0.40 → 0.10 with inlet air at 250°F, constant-rate outlet T_oc = 123°F and final outlet T_0f = 180°F. Solve 12.17 for K_x: 180 = 123 + K_x(250 − 123) → **K_x = 0.449**. To reach a slightly wetter 0.12 spec (wet-bulb 93°F) the required outlet temperature drops, so K_x and T_0f are recalculated from the same averaging relation with the new moisture ratio — the sensitivity of termination temperature to the spec is what makes K_x recalibration, not hardware, the servicing action for a dryer.
