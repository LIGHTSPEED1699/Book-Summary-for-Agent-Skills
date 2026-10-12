# Chapter 5: Kalman Filter

## Core Idea
For Gaussian systems, optimal estimation is finite-dimensional: the conditional mean is the optimal estimator (any sense of optimal, for Gaussians), and it can be computed recursively by orthogonal projection — the Kalman filter. The gain comes from the innovation covariance; the prediction error covariance obeys a Riccati recursion that converges to the stabilizing solution of the algebraic Riccati equation (ARE) in the stationary case. The stationary filter and its backward twin supply the state estimates that subspace identification methods ultimately reproduce from data.

## Frameworks Introduced
- **Multivariate Gaussian (5.1)**: density, conditioning formula — E[x|y] and cov[x|y] in closed form (the Gaussian conditioning lemma used everywhere).
- **Optimal estimation by orthogonal projection (5.2)**: linear MMSE via projection; orthogonality principle; recursive update as projection onto data span.
- **Prediction and filtering recursions (5.3)**: time update (predict) + measurement update (correct); innovation form: x̂(t+1|t) = Ax̂(t|t−1) + K[y − Cx̂]; K = AΣCᵀ(CΣCᵀ+R)⁻¹.
- **Kalman filter with inputs (5.4)**: deterministic inputs enter through known B terms; filter runs on the deterministic and stochastic parts separately — the exact structure of subspace methods with exogenous inputs (ch9-10).
- **Prediction covariance recursion (5.5)**: Σ(t+1|t) = AΣ(t|t−1)Aᵀ + Q − K(CΣCᵀ+R)Kᵀ; Riccati difference equation.
- **Stationary Kalman filter (5.6)**: constant gain from ARE solution Σ̄; filter becomes LTI; connection to innovations representation and spectral factorization.
- **Stationary backward Kalman filter (5.7)**: filtering the process backward in time; backward gain and covariance — the backward Markov model made recursive.
- **Numerical solution of ARE (5.8)**: Schur/method-of-squaring style iteration; symplectic matrix eigenstructure; why the stabilizing solution is the right one.

## Key Concepts
- For Gaussians, linear estimator = optimal estimator; conditional mean = projection.
- Innovation form decouples design (gain) from estimation (state); innovations are white by construction.
- Separation of known inputs: estimate the deterministic response and the stochastic response independently, then add — Katayama leans on this in every subspace algorithm with exogenous input.
- ARE stabilizing solution: the stationary filter's covariance is the unique stabilizing solution; the filter is stable because (A − KC) is Schur.
- Forward/backward stationary filters share the same state-space geometry; their error covariances are the forward/backward Gramians.

## Mental Models
- "Predict, then correct": every recursive estimator is time-update + measurement-update; the gain is just the regression coefficient of state on innovation.
- "Riccati convergence = stationarity": after transients, the Kalman gain freezes; the frozen gain is the ARE's stabilizing solution.
- "Inputs don't confuse the filter": run the filter on residuals after removing the known input response — the two-stage logic that reappears as ORT/MOESP's projection of inputs out.
- "The filter has a twin running backwards": backward filtering is not a metaphor; it's the same recursion on the time-reversed process.

## Anti-patterns
- **Filtering with colored noise as-is** — augment the state or whiten first (ch4's innovations representation).
- **Using a non-stabilizing ARE solution** — numerically reachable but wrong; enforce stabilizing selection.
- **Ignoring the input terms in the filter** — with exogenous inputs, omitting B u terms biases the state estimate; Katayama's ch5.4 exists precisely because subspace methods need this.
- **Trusting the filter without innovation checks** — residual whiteness is the free consistency test (Doraiswami ch9 turns this into fault diagnosis).

## Reference Tables
### Kalman recursions (stationary form)
| Step | Equation |
|---|---|
| Predict | x̂(t+1\|t) = A x̂(t\|t−1) + B u(t) |
| Innovate | ε(t) = y(t) − C x̂(t\|t−1) − D u(t) |
| Update | x̂(t+1\|t) = A x̂(t\|t−1) + K ε(t) |
| Gain | K = A Σ Cᵀ (C Σ Cᵀ + R)⁻¹ |
| Covariance | Σ⁺ = A Σ Aᵀ + Q − K(CΣCᵀ+R)Kᵀ (ARE at fixed point) |

### Gaussian conditioning
| Given | Then |
|---|---|
| [x;y] Gaussian, cov [[P, P₁₂],[P₂₁, P_y]] | E[x\|y] = μ_x + P₁₂ P_y⁻¹(y − μ_y) |
| — | cov[x\|y] = P − P₁₂ P_y⁻¹ P₂₁ |

## Key Takeaways
The Kalman filter is orthogonal projection made recursive; for Gaussians it is optimal, period.
The Riccati recursion converges to the ARE's stabilizing solution — stationary filters are LTI.
Filters with known inputs split deterministic/stochastic — the template for subspace methods with exogenous inputs.
Stationary forward and backward filters bracket the state from both time directions — subspace methods estimate that state from Hankel data instead.

## Connects To
Projection machinery from ch2/ch4; stationary filter's Gramians reappear as the balanced realization's covariance in ch8; ch9 ORT and ch10 CCA effectively estimate Kalman-filter state sequences from data (the "filter-free" route); ch11 closed-loop identification is motivated by the filter running on closed-loop data; Doraiswami ch6 develops the same filter with model-mismatch analysis feeding fault diagnosis.
