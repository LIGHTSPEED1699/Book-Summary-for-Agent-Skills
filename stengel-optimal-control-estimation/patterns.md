# Patterns — Optimal Control and Estimation (Stengel)

## Design patterns

### 1. Cost function first, controller second
Write J (terminal + integral, weighted norms) before choosing structure. The optimizer's output *is* the controller; weights are the tuning interface (bandwidth ↔ control weight).

### 2. Manufacture structure by augmentation
Need integral action / lead-lag / model following? Add the extra states (integrators, filters, reference model) to the plant model, penalize the right outputs in J, and let one Riccati solve size every gain consistently (PI, PIF, explicit/implicit model following).

### 3. Equilibrium pair, then regulate the perturbation
For any setpoint compute (x̄, ū) from the steady-state equations; design the LQ gain on δx = x − x̄; add equilibrium feedforward. Never regulate absolute states directly.

### 4. Optimize once, feedback locally (neighboring-optimal)
Compute the nominal trajectory, then one Riccati sweep around it gives δu = −S(t)δx valid for the whole perturbation family — trajectory solutions become regulators.

### 5. Model or augment (estimation edition)
Colored noise, cross-correlated noise, unknown constants: extend the state with shaping filters or parameters until the model is white and linear; then plain Kalman applies.

### 6. Design the two halves separately, bill them together (LQG)
Pick Q/R for the regulator and Q_c/R for the filter independently; expected cost = control term + estimation term. But audit the *combined* loop's margins — separation doesn't transfer robustness.

### 7. Margin audit workflow (Ch 6.5-6.6)
1. Check the LQR loop: guaranteed GM ≥ ½, PM ≥ 60° (or σ̲(return difference) multivariable version).
2. Insert the estimator: margins can collapse → apply LTR (estimator bandwidth/gain shaping) to recover.
3. Cross-check uncertainty with σ̄ small-gain / multivariable Nyquist; for random parameter uncertainty, probability of instability.

### 8. Right-size the hierarchy (epilogue + 6.7)
Fixed LQG → scheduled gains on exogenous variables (time, orbit position, Mach) → endogenous adaptation (recursive parameter estimation + redesign) → dual control only when nonlinear + large uncertainty. Use the smallest rung that covers the uncertainty.

### 9. Innovation monitoring as free diagnostics
Whiteness of z − Hx̂ = model consistent; bias/coloring = wrong Q/R/H/F. Route residual statistics into noise-adaptive updates or alarms.

## Diagnosis playbook (symptom → likely cause → chapter)
- **LQ loop oscillatory/overwhelming control** → control weight R too small / Q too big → reweight via crossover-frequency targets (Ch 6.3-6.4)
- **Steady-state offset under constant disturbance** → no integral state in the model → augment + re-solve (Ch 6.3)
- **Kalman filter diverges** → P overconfident (Q/R underestimated), EKF linearization at wrong estimate → inflate covariances, better initialization (Ch 4)
- **Estimate lags / ignores measurements** → R too large or process noise too small → retune second-order stats (Ch 4)
- **LQG loop fragile despite "optimal" design** → compensator margins collapsed after inserting filter → LTR (Ch 6.6)
- **Tracking error to reference model** → explicit model-following augmentation or output-weighting design (Ch 6.3)
- **Bang-bang answer to a minimum-fuel problem** → missed singular arc → check generalized Legendre-Clebsch (Ch 3.5)
- **Parametric optimization "optimal" but odd shape** → shape functions bounded the answer → move to TPBVP methods (Ch 3.3/3.6)
- **Adaptive filter parameter drift** → no excitation / too many parameters → reduce uncertain set, add excitation, multiple-model instead (Ch 4.7)
- **Probing "needed" in a known linear system** → neutral system: probing has no value → drop it (Ch 5.2)

## Algorithm selection tree
- Known trajectory problem, smooth control → calculus of variations / TPBVP (Ch 3.4)
- Bounded control → minimum principle (bang-bang/singular structure) (Ch 3.4-3.5)
- Need feedback around trajectory → neighboring-optimal Riccati (Ch 3.7)
- Noisy partial measurements → Kalman/EKF (Ch 4)
- Linear + Gaussian + quadratic → LQG with margin audit (Ch 5.3, 6)
- Setpoint tracking → equilibrium pair + augmentation structures (Ch 6.2-6.3)
- Parameter drift beyond fixed-gain robustness → scheduled gains, then adaptive (Ch 6.7)
