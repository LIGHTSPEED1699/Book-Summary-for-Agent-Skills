# Ch4 — Feedback and Oscillation

## The zoo of feedbacks
- **Ataxia cases** open the chapter: tabes dorsalis (proprioceptive feedback destroyed → cannot stand blindfolded) and cerebellar tremor (feedback present but mis-proportioned → hand swings past the cigarette, oscillation). Purposeful movement requires the effector monitored back.
- Signal tower: every switch/signal has a **telltale**; navy repeats orders. Human link in the feedback chain.
- Thermostat (temperature), Watt's centrifugal governor (velocity, Maxwell's analysis), ship's steering engine (position): **negative feedback** — the returned information opposes the departure of the controlled from the controlling quantity.
- Voluntary motion: "we will, say, to pick up a cigarette. Our motion is regulated by some measure of the amount by which it has not yet been accomplished."

## The linear operator formalism (the chapter's engine)
- Causal, linear, time-invariant operators: output = Σ a_k f(t−τ_k) → ∫₀^∞ a(τ) f(t−τ) dτ. Causality (0 to ∞) is essential — an operator reaching into the future means the system is self-oscillating, not operated.
- e^{zt} are eigenfunctions: delay → multiplication; the operator becomes **A(z)**, holomorphic and bounded in right half-planes; A(iy) is the frequency representation.
- **Stability criterion (Wiener's Nyquist-equivalent)**: plot the curve A(iy) as y runs −∞→∞; define interior/exterior points and the effective boundary. Feedback with multiplier λ gives closed-loop operator **A/(1+λA)**; the system is stable iff **−1/λ is an exterior point** of the A(iy) curve; catastrophic (unrestrained increasing oscillation) if interior; marginal if on the effective boundary. Incipient oscillation frequency = the y at the boundary point furthest right on the negative real axis.
- Worked spectra of admissible feedback:
  - A = z (differentiator): unlimited feedback.
  - A = 1/(1+kz): circle center ½ radius ½ — unlimited feedback.
  - double cascade: cardioid — still unlimited.
  - A with three lags: curve enclosing part of negative axis — **feedback coefficient > 1/8 impossible**.
  - pure delay T: unit circle — feedback limit 1.
- **Ship steering (MacColl's case)**: rudder-rate ∝ course error → operator kz³ → left half-plane interior → **no servomechanism whatever stabilizes it**. Fix: a second feedback loop (valves driven by error minus rudder position) makes rudder position ∝ error (k₁z²+k₂z) → unlimited amplification. The double loop is exactly what gyrocompass autopilots do.
- Human parallel: multi-joint limb = additive complex system, not stabilizable by one feedback → voluntary feedback needs **postural feedbacks** (muscle tone) as backing. Cerebellar purpose tremor (task-dependent) ≠ Parkinson's rest tremor (brain-stem, postural loop disease). Physiological cybernetics' task: disentangle the loci of the feedback complex.

## What feedback buys, and what it costs
- Load insensitivity: fractional change dA/A → dA/A ÷ (1+λA). Heavy negative feedback stabilizes **low frequencies at the expense of high-frequency stability** (boundary must lie inside circle of radius C about −C).
- One feedback can compensate any number of first-order lags (1/(1+kz)) but **not their third-order cascade** 1/(1+kz)³ — a sum of individually-compensable operators may not be compensable. Compensator + feedback combined: anticipatory feedback (add a predictor matched to the input ensemble) — duck shooting and anti-aircraft fire minimize the **anticipated** error, not the present one.
- **Informative feedback** (control by probing): steering a car on ice — small fast steering impulses probe the road's friction without causing a skid; schematized as weak high-frequency dither + filtered pickup + compensator adjustment. Works when load changes are **secular** (slow vs signal) and high-frequency behavior indicates low-frequency behavior (gun turret grease stiffness vs temperature).

## Linear vs non-linear oscillation
- Linear system oscillating: sinusoidal, amplitude independent of frequency, amplitude set by history. **Non-linear (relaxation) oscillation** (van der Pol): determinate amplitude AND frequency, indeterminate phase; organ pipe (energy input from air stream balances dissipation at one level); gas-leak + pilot-light explosion clock (frequency set by flow rates, not by any linear resonance).
- **Secular perturbation method**: systems whose non-linear terms change slowly vs the oscillation period → treat as linear with slowly varying parameters; explains determinate amplitude in physiological tremors (gain that decreases with long-time average input self-limits the oscillation).
- Non-sinusoidal steady oscillation is a **diagnostic sign of non-linearity**.

## Homeostasis
- The body as a chemical plant run by thermostats, pH controls, governors: temperature ±0.5°C, osmotic pressure, H⁺, waste excretion, leucocytes, heart rate, calcium. Homeostatic feedbacks are **slow**: non-myelinated sympathetic/parasympathetic fibers, smooth muscle and gland effectors, hormonal (chemical) messaging.

## Design checklist (practitioner)
1. Write the open-loop operator A(z); plot A(iy); locate −1/λ.
2. Count integrations/lags: three or more cascaded lags → single loop cannot stabilize; add inner loops.
3. Put the compensator (predictor) inside the loop when the effector lags.
4. Dither-probe slowly varying loads (informative feedback).
5. Expect relaxation oscillation (fixed amplitude) when limits/nonlinearities dominate; expect amplitude runaway when linear theory says unstable.
