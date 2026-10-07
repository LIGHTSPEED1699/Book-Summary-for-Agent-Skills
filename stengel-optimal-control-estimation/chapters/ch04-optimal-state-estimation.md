# Chapter 4: Optimal State Estimation

## Core Idea
Build the estimator the same way you built the trajectory: least squares for static vectors → propagate mean and covariance through the dynamics → minimize posterior error variance and the Kalman filter pops out, in discrete time first with Kalman-Bucy as the continuous limit — and the filter is the exact control/estimation **dual** of the regulator.

## Frameworks Introduced
- **4.1 Least squares for constant vectors**: measurement model z = Hx + η; unweighted LS x̂ = (HᵀH)⁻¹Hᵀz (minimum error when η white); **weighted LS** x̂ = (HᵀR⁻¹H + …)⁻¹(HᵀR⁻¹z + prior term) incorporating measurement covariances and prior information; **recursive LS** — update the estimate and its covariance one measurement at a time (matrix inversion lemma) — the template for the filter.
- **4.2 Propagation**: propagate mean x̂ and covariance P through dynamics: prediction x̂⁻ = Φx̂ + Γu, P⁻ = ΦPΦᵀ + ΓQΓᵀ; sampled-data representations (Φ = e^{Fh}, Γ from ∫e^{Fτ}dτ·G); continuous limit Ṗ = FP + PFᵀ + GQGᵀ; simulating cross-correlated white noise correctly (correlated process noise and measurement noise arise from common sources).
- **4.3 Discrete Kalman filter & predictor**: update upon measurement: innovation ν = z − Hx̂⁻; x̂ = x̂⁻ + Kν with **optimal gain K = P⁻Hᵀ(HP⁻Hᵀ + R)⁻¹** minimizing trace(P); covariance update P = (I − KH)P⁻ (or Joseph form for numerical hygiene); **predictor** = filter output one step ahead; alternative forms (information form, sequential measurement updates); fading memory via process-noise inflation.
- **4.4 Correlated noise**: process noise correlated with measurement noise (cross-covariance M) → modified gain/update; **time-correlated (colored) measurement noise** → augment the state with the noise model (shaping filter) — "model the noise or be suboptimal."
- **4.5 Continuous-time**: **Kalman-Bucy filter** ẋ̂ = Fx̂ + Gu + K(z − Hx̂), K = PHᵀR⁻¹, Ṗ = FP + PFᵀ + GQGᵀ − PHᵀR⁻¹HP; **duality**: estimator equations (F, G→Hᵀ, Q→R) map to the regulator's (F, H→G, Q→R, Riccati backward vs forward); predictor and smoothing forms.
- **4.6 Nonlinear estimation**: conditional-mean is not the linear solution in general; **neighboring-optimal linear estimator** (linearize about nominal trajectory); **extended Kalman-Bucy filter (EKF)** — Jacobians along the estimated trajectory, workhorse of nonlinear estimation; **quasilinear filter** — linearize the measurement equation instead; both optimal to first order, sensitive to linearization errors and initialization.
- **4.7 Adaptive filtering**: when F/G/H/Q/R are uncertain:
  - **Parameter-adaptive**: augment state with p (x̃ = [x; p], ṗ = 0 or random-walk model) and run EKF — nonlinear, convergence not guaranteed; success depends on parameter count, excitation, output sensitivity to p, measurement quality.
  - **Noise-adaptive**: estimate Q_c and R from the measurement residual (innovation) statistics — e.g., match observed innovation covariance to predicted; gain K depends on them so the filter becomes nonlinear in the residual.
  - **Multiple-model estimation**: run a bank of filters with different parameter hypotheses, weight by likelihood — covers discrete/structural uncertainty.

## Key Concepts
- **Innovation ν = z − Hx̂⁻**: the new information; white when the model is right — the residual is both the correction signal and the model-checking signal.
- **Gain K = P⁻Hᵀ(HP⁻Hᵀ + R)⁻¹**: optimal trust in measurement vs model, computed from covariances.
- **Covariance propagation**: P is the filter's self-knowledge; it evolves independently of measurements (LTI case) → steady-state gain.
- **Duality**: Kalman-Bucy ↔ LQR (Riccati forward vs backward; H↔Gᵀ, R↔Q) — reuse one solver for both.
- **Augmentation**: colored noise, unknown parameters — extend the state until the model is white and linear-in-the-states.
- **EKF**: Jacobians along the estimate; first-order accuracy, divergence risk with bad initialization or weak excitation.

## Mental Models
- "Estimation = weighted least squares that never stops": every Kalman update is one weighted-LS step with the propagated covariance as the prior.
- "The innovation is the truth serum": white residuals = model consistent; colored/biased residuals = model wrong — monitor it.
- "Model or augment": any non-whiteness or unknown constant is a state you haven't added yet.
- "Estimator gain is a covariance ratio": trust the measurement exactly as much as its variance warrants relative to prediction uncertainty.
- "Adaptive filters are nonlinear even when the plant is linear": products of estimates (p̂x̂, K(residual)) break linearity — no free lunch.

## Anti-patterns
- **Filter divergence from overconfident P**: underestimated Q or R makes the filter believe itself; inflate covariances rather than shrink.
- **EKF with poor initialization or weak observability**: linearization about a wrong estimate compounds; parameter estimates need excitation.
- **Ignoring process/measurement noise cross-correlation**: common physical sources create M ≠ 0; naive filter is biased.
- **Colored measurement noise filtered naively**: whiten by augmentation, don't pretend it's white.
- **Adaptive filter without persistent excitation**: parameter estimates drift; the augmented filter can diverge (same lesson as Åström Ch 2/6).

## Reference Tables

### Filter family
| Filter | Handles | Mechanism |
|---|---|---|
| (Weighted) LS | static vector | one-shot normal equations |
| Recursive LS | streaming static | matrix inversion lemma updates |
| Kalman (discrete) | linear, white noise | predict + innovation update |
| Kalman-Bucy | continuous | limit of discrete as h→0 |
| EKF | nonlinear | Jacobians along estimate |
| Quasilinear | nonlinear measurement | linearized measurement eq. |
| Adaptive (parameter) | unknown p | state augmentation + EKF |
| Adaptive (noise) | unknown Q,R | innovation-statistics matching |
| Multiple-model | structural uncertainty | filter bank + likelihood weights |

### Duality map (regulator ↔ estimator)
| Regulator | Estimator |
|---|---|
| F, G | Fᵀ, Hᵀ |
| Q (state weight), R (control weight) | GQGᵀ (process), R (measurement) |
| Riccati backward in time | Riccati forward in time |
| u = −C x̂ | ẋ̂ = ... + K(z − Hx̂) |

## Key Takeaways
1. The Kalman filter is recursive weighted least squares on propagated covariances — nothing more mysterious.
2. The optimal gain is fully determined by covariances; tune Q/R (and their cross-correlation) honestly or the filter lies to you.
3. Duality lets one Riccati machinery serve control and estimation — the LQG architecture of Ch 5-6 rests on it.
4. Nonlinear/adaptive estimation = linearize or augment, at the price of guaranteed convergence; excitation and initialization decide success.
5. The innovation sequence is the free model-validation signal: whiteness = consistency, structure = error.

## Connects To
- **Ch 2**: random processes, covariance algebra, matrix identities.
- **Ch 3**: the trajectory whose neighborhood the estimator tracks.
- **Ch 5**: filter + optimal control = stochastic regulator; certainty equivalence.
- **Ch 6**: steady-state Kalman gain, observer modes, LQG robustness.
