# Chapter 5: Linear Least-Squares Estimation

## Core Idea
The workhorse estimator: given an over-determined linear model z = Hθ + e, choose θ to minimize the squared residual ‖z − Hθ‖². The normal equations HᵀHθ̂ = Hᵀz give the unique solution when H has full column rank; when they don't (rank deficiency, under-determined systems), the SVD and pseudo-inverse sort out existence and uniqueness — minimum-norm solutions for under-determined problems, least-squares solutions otherwise. Recursive least squares makes the same estimate update sample-by-sample, the online form used in adaptive identification.

## Frameworks Introduced
- **Linear algebraic model (5.2.1)**: stack measurements into z = Hθ + e; θ the parameter vector to estimate.
- **Objective function (5.2.3)**: J(θ) = Σ e²(k) = ‖z − Hθ‖²; quadratic, convex; stationary point = normal equations.
- **Over-determined case (5.10.1)**: more equations than unknowns, full column rank ⇒ unique LS solution θ̂ = (HᵀH)⁻¹Hᵀz.
- **Under-determined case (5.10.2)**: fewer equations than unknowns ⇒ infinitely many exact fits; pick minimum-norm via pseudo-inverse.
- **SVD and eigendecomposition (5.12.1)**: H = UΣVᵀ; pseudo-inverse H⁺ = VΣ⁺Uᵀ; rank, conditioning (σ_max/σ_min), and the geometry of the LS solution.
- **Matrix norms (5.12.2)**: Frobenius and spectral norms; error sensitivity of LS to data/model perturbation.
- **Recursive least squares (5.6)**: gain-updated running estimate — the covariance-form recursion reused in ch7's RLS identification.

## Key Concepts
- LS = ML for Gaussian errors (ch3) and the flat-prior limit of MMSE (ch4) — three roads, one estimator.
- Normal equations square the condition number; SVD/QR are the numerically honest routes (Katayama ch2's warning, echoed here).
- Conditioning is identifiability in practice: tiny singular values = parameter directions the data can't see.
- Over vs under-determined: LS picks the closest fit vs the smallest explanation; pseudo-inverse handles both.
- Residual analysis (foreshadowed here, used in ch7/ch9): a good model leaves white residuals.

## Mental Models
- "Fit the residual, not the data": minimize what's left over; the residual's behavior validates the model.
- "Singular values are visibility": each parameter direction is estimable in proportion to its σ; near-zero σ = blind spot.
- "Pseudo-inverse is the universal answer": θ̂ = H⁺z covers over/under/rank-deficient cases uniformly.
- "Recursive = same math, streaming": RLS is the batch LS with the covariance carried forward — online identification inherits it.

## Anti-patterns
- **Forming HᵀH explicitly with ill-conditioned H** — use SVD/QR; the book's own SVD section exists for this.
- **Trusting LS with correlated noise** — biased (ch7's correlated-error appendix makes this precise); whiten or use PEM.
- **Reading parameters off an under-determined fit** — minimum-norm is a convention, not physics.
- **Skipping residual checks** — colored residuals mean the model missed structure.

## Reference Tables
### LS solution map
| Case | Condition | Solution |
|---|---|---|
| Over-determined | rank H = p | (HᵀH)⁻¹Hᵀz |
| Rank-deficient | rank H < p | H⁺z (via SVD) |
| Under-determined | m < p, full row rank | min-norm Hᵀ(HHᵀ)⁻¹z |

### Conditioning
| Quantity | Meaning |
|---|---|
| κ = σ_max/σ_min | error amplification factor |
| σ small | unidentifiable direction |
| Frobenius norm | total energy of matrix |
| Spectral norm | max gain (σ_max) |

## Key Takeaways
LS is the default estimator: quadratic objective, normal equations, pseudo-inverse for the general case.
Singular values decide what's estimable; conditioning is the practical identifiability test.
RLS streams the same solution for online identification (ch7).
LS is Gaussian-ML — its optimality claims inherit that assumption.

## Connects To
ch7 applies this directly to ARX/ARMAX identification (data matrix = regressors); ch6's Kalman filter is a recursive LS with a prior; ch9's diagnostic parameter estimation reuses it; Katayama ch2.7 + A.1 is the same machinery with the numerics-first discipline.
