# Cheatsheet — Puig & Simani, Diagnosis and Fault-tolerant Control

## FDI design workflow
1. Classify the fault: additive vs multiplicative; abrupt (step) / incipient (ramp) / intermittent (impulse); location = actuator | process | input sensor | output sensor | controller.
2. Choose residual engine: accurate model → UIO/parity/observer bank; noisy I/O both → Frisch/EIV + KF; nonlinear → TS/PWA clustering or EKF bank or NLGA; complex structured → structural analysis first; no model → classifier (data-driven).
3. Robustify: fixed threshold → adaptive (passive) → decoupling/H∞ (active) → zonotopic envelope (set-based).
4. Isolate: directional residuals / bank signatures / isolability matrix / conflicts + hitting sets.
5. Evaluate: |r| > δ·σ with δ≥2 (false-alarm/detection trade-off); moving averages; likelihood-ratio, run-sum for change detection.

## Structural analysis steps (Vol 1 Ch2)
1. Write DAE model → structure graph (equations × variables).
2. Maximal matching; unmatched equations = redundant relations → eliminate unknowns → ARRs.
3. DM decomposition → G−/G0/G+; fault detectable iff ef ∈ M+.
4. For each fault fj: DM of M \ {efj} → faults in (M \ {efj})+ are isolable from fj → fault isolability matrix.
5. MSO sets = minimal residual candidates; select tests (hitting-set/selection methods).
6. Sensor placement: diagnosability ceiling set by sensors, not algorithms.

## Reiter CBD steps (Vol 1 Ch6)
1. Model correct behavior only: ¬AB(c) ⇒ behavior.
2. Assert observations; find conflicts (sets where at least one member must be AB).
3. Minimal diagnoses = minimal hitting sets of minimal conflicts.
4. Dynamic systems: MEC → causal assignment → MEM → Possible Conflict = executable monitor; PC violation = conflict.

## Zonotopic FDI recipe (Vol 1 Ch3)
- Model x(k+1)=Ax+Bu+w, y=Cx+v with w∈〈0,Dw〉, v∈〈0,Dv〉.
- Observer: x̂(k+1)=Ax̂+Bu+G(y−Cx̂); propagate zonotopes.
- Robustness LMI: find P≻0, Y, diagonal Γ,Υ with contraction γ ⇒ gain G=P⁻¹Y, steady size V(X∞)≤ε/(1−γ).
- Zonotopic Kalman gain: minimize Frobenius norm of H (independent of weighting W).
- Fault sensitivity LMI (H−): residual center responds to sensor faults.
- Alarm: y(k) ∉ predicted output zonotope interval set.

## FTC decision (Vol 2)
- Fault class small/known → **passive**: H∞/robust design, invariant sets, LPV robust control.
- Need continued operation after real faults → **active**:
  1. Estimate magnitude: RPO (LPV descriptor), TS H∞ observer, dead-beat (check block P-matrix rank), bank of MISO estimators with signature matrix.
  2. Reconfigure: scheduled gains (LPV), MPC model switch + error model, or **virtual sensor (M) / virtual actuator (N)** via LMIs — nominal K, L untouched (extended separation principle).
- Pole hierarchy: keep virtual-block dynamics slower than dominant closed-loop poles to avoid hiding fast modes.

## Actuator/sensor fault parameterization
- Actuator loss of effectiveness: f(t) = −γ(t)u(t), γk ∈ [0,1[ (0.5 = 50% loss); virtual actuator effectiveness φi.
- Sensor: ŷ = γi y + f, γi ∈ [0,1] (1 healthy, 0 dead); virtual sensor effectiveness Ĉf.
- Additive equivalent faults at I/O: u = u* + fu + noise, y = y* + fy + noise — the unified design handle.

## NLGA quick steps (Vol 2 Ch1)
1. Compute maximal (C,A)-invariant ΣP∗ ⊂ ker dh (Lie-bracket recursion, involutive closure).
2. Ω∗ = o.c.a.((ΣP∗)⊥) (observability codistribution algorithm).
3. Check Ω∗ ∩ span{dh} = span{d(Ψ1∘h)} (surjection) → diffeomorphism exists.
4. In new coordinates the x̄1-subsystem sees only fault f, decoupled from d → design residual (filter form ṙf = −kf rf + …; tune kf by mixed H−/H∞).

## TS embedding quick steps (Vol 2 Ch3)
1. Expand each nonlinear row into summands fij = αij/βij + κij.
2. Classify: constant/non-factorizable vs containing inputs/state powers.
3. Assign summands to A/B entries; derive premise variables (superposition or direct).
4. Blend vertex models by convex weights hi(vk); design PDC K(hk) + fault compensation by LMIs.

## Benchmarks used in the book
- Electric motor (structural analysis running example), quadruple-tank (Johansson; set-based FDI + virtual sensors), three-tank (possible conflicts), twin-rotor system TRS (TS fault estimation), anaerobic bioreactor (LPV FTC), gas turbine / DAMADICS actuator (FDI application line), pneumatic cylinder (robust MPC).

## Common pitfalls
- Assuming scheduling/decision variables measurable when they're state-dependent (use quasi-LPV on x̂).
- Designing residuals without structural analysis → discover later the fault is structurally undetectable.
- Fixed thresholds on nonlinear plants → false alarms at extreme operating points (use adaptive/set-based).
- Confusing Vol 1's "AI approach" (symbolic CBD) with "data-driven" (identification/NN): different isolation machinery (conflicts vs signatures).
- Skipping FMEA/digital-twin validation before deploying FTC on industrial plants.
