# Chapter 6: Kalman Filter

## Core Idea
The Kalman filter is the recursive MMSE state estimator for the augmented (plant + disturbance + noise) model of ch1: a predict-correct loop whose gain is the ch4 measurement update and whose prediction step is the plant model. The chapter builds it from the necessary structure (why an observer-like recursion is the right form), derives the optimal gain (scalar then vector, finite-time and steady-state), and then does the practitioner-critical parts: the internal model principle for tracking/rejection, comparison of filters built on integrated vs plant models, multi-sensor information fusion, and — the bridge to fault diagnosis — exact accounting of estimation error under model mismatch.

## Frameworks Introduced
- **Observer structure first (6.6.2)**: the estimator must have a model-driven recursion plus an error-injection term — the Luenberger form — before optimality is discussed.
- **Optimal Kalman filter (6.6.5-6.6.8)**: minimize E[‖x − x̂‖²]; gain K = P̄Cᵀ(CP̄Cᵀ+R)⁻¹; Riccati recursion for P̄; scalar case worked explicitly.
- **Steady-state filter (6.6.7.3, 6.6.10)**: Riccati converges, gain freezes; precomputed constant-gain filters.
- **Internal model principle in filters (6.3)**: embed the signal-class model (ch1) in the filter to get exact tracking/rejection of references, disturbances, noise types.
- **Integrated vs plant-model filters (6.6.9)**: filtering the augmented model vs the bare plant — different gains, different disturbance rejection; the integrated model is the honest one.
- **Optimal information fusion (6.6.12)**: combining estimates from multiple sensors/filters — weighted by error covariances; the multi-sensor case used in ch12.
- **Orthogonality theorems (6.4-6.5)**: the estimation error is orthogonal to past residuals, past estimates, reference, and initial condition — the innovation property made explicit.
- **Model mismatch (6.7.1)**: when the filter's model differs from the plant, the error no longer satisfies the nominal Riccati; the chapter computes the actual error statistics — the mathematical basis of residual-based fault diagnosis (ch9).

## Key Concepts
- Predict-correct: time update carries the model, measurement update carries the data; the gain splits their information by relative covariance.
- Innovation/residual e(k) = y − ĉ: white under matched model; the orthogonality theorems are exactly its whiteness.
- Steady-state gain = ARE fixed point (same object as Katayama ch5.6).
- Internal model in the filter ⇒ zero steady-state error for that signal class (the same principle as in controllers).
- Fusion = inverse-covariance weighting: the optimal combination of unbiased estimates.
- Mismatch makes residuals colored and biased in computable ways — that's a feature: faults show up as structured residual deviations.

## Mental Models
- "The filter is a two-speed machine": model runs fast (predict), data corrects slowly (gain) — the balance is the Riccati solution.
- "Residual whiteness is the health check": orthogonality theorems are theorems only under matched models; their failure is your detector.
- "Embed what you must track": performance specs on signal classes translate into internal-model structure, not bigger gains.
- "Fuse by confidence": covariance is currency; combine estimates by inverse covariance.

## Anti-patterns
- **Filtering the plant model while disturbances/noise are colored** — use the integrated model (6.6.9); white-noise shortcuts bias everything.
- **Ignoring mismatch analysis** — nominal Riccati covariance wildly understates error when the model is wrong; ch9's diagnosis depends on knowing the true error behavior.
- **Constant gain where adaptation is needed** — steady-state filters assume convergence and stationarity; check both.
- **Fusing without covariance accounting** — averaging sensors equally ignores their quality.

## Reference Tables
### Filter anatomy
| Piece | Equation | Source |
|---|---|---|
| Predict | x̂⁻ = Ax̂ + Bu | plant model |
| Residual | e = y − Cx̂ − Du | data vs model |
| Correct | x̂⁺ = x̂⁻ + Ke | ch4 update |
| Gain | K = P̄Cᵀ(CP̄Cᵀ+R)⁻¹ | MMSE |
| Covariance | P⁺ = P̄ − K(CP̄Cᵀ+R)Kᵀ | Riccati |

### Mismatch consequences (6.7)
| Nominal claim | Under mismatch |
|---|---|
| e white | e colored, structured |
| P from Riccati | actual P̃ ≠ P |
| stability (A−KC) Schur | may degrade |
| diagnosis basis | residual statistics become the signal |

## Key Takeaways
The Kalman filter = ch4's MMSE update iterated on ch1's augmented model; the gain is the information split.
Orthogonality theorems = residual whiteness under matched models; their violation is the fault-detection signal.
Internal model embedding, integrated modeling, and covariance-weighted fusion are the three design laws.
Model mismatch has exact, computable error statistics — the book turns this from a caveat into an instrument (ch9).

## Connects To
ch1's augmented model and internal model; ch4's update formulas; ch7 identifies the A,B,C used here; ch9 turns the residual machinery into fault diagnosis; ch12 fuses sensor-network estimates; Katayama ch5 is the theory twin (projection-derived, stationary filters, backward filters).
