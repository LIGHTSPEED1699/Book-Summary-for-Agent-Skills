# Chapter 3: Manifolds, Taylor Polynomials, Quadratic Forms, and Curvature

## Core Idea
Second-order structure. Manifolds are curves/surfaces in Rⁿ with tangent spaces; Taylor polynomials upgrade the derivative to quadratic approximation; quadratic forms classify what happens at critical points (min/max/saddle) via signature; Lagrange multipliers do the same on constraints; the SVD appears (via the spectral theorem) as the tool that makes all of this computable — and pays an unexpected visit to probability. The chapter ends with curvature: how a manifold bends, measured by second-order data.

## Frameworks Introduced
- **Manifolds (3.1)**: subsets of Rⁿ locally the image of a parametrization γ: U → Rⁿ (or zero set of a submersion — implicit function theorem preview); dimension, charts, examples (spheres, tori, graph manifolds).
- **Tangent space (3.2)**: T_x S = span of velocity vectors of curves in S through x; the linear approximation of the manifold itself.
- **Taylor polynomials (3.3–3.4)**: T_2 f(a) = f(a) + Df(a)h + ½ hᵀ[Hf(a)]h; Taylor's theorem without remainder (3.3.1); computation rules including Taylor polynomial of an implicit function (3.4.7 — differentiate the equation, don't solve it).
- **Quadratic forms (3.5)**: Q(x) = xᵀAx with A symmetric; **3.5.3: every quadratic form is a sum of squares after change of variables** (completing squares = congruence diagonalization); signature (#positive − #negative) and positive/negative/semi-definiteness.
- **Critical point classification (3.6)**: Df(a) = 0 at extrema (3.6.3); second-derivative test via the Hessian's quadratic form (3.6.8): positive definite ⟹ local min, negative ⟹ max, indefinite ⟹ saddle with the explicit behavior of 3.6.10; degenerate cases need higher order.
- **Lagrange multipliers (3.7)**: constrained critical points of f|_S: Df(a) = λ DG(a) (normal to the constraint); the constrained second-derivative test uses the **signature of the Hessian restricted to the tangent space** (3.7.13); **spectral theorem (3.7.15)**: symmetric matrices orthogonally diagonalizable — the engine.
- **Probability and SVD (3.8)**: SVD (3.8.1) A = VDU*; applications to covariance: Gaussian distributions, principal component analysis, why the SVD directions are the axes of probability ellipses.
- **Curvature (3.9)**: curvature of curves (κ = ‖dT/ds‖); osculating circle; surfaces: normal curvature, principal curvatures κ1 ≥ κ2, Gaussian curvature K = κ1κ2; sphere K = 1/r²; saddle K < 0; **Theorema Egregium flavor**: K is intrinsic (measurable on the surface).

## Key Concepts
- Signature is the complete invariant of quadratic forms under change of variables (Sylvester's law, via 3.5.3).
- Completing squares = congruence A ↦ PᵀAP (contrast with similarity P^{-1}AP — different chapter, different equivalence).
- The Hessian is a quadratic form on the tangent space; extrema classification = signature reading.
- Lagrange multiplier λ has meaning: rate of change of the optimum value w.r.t. the constraint level.
- SVD from the spectral theorem applied to AᵀA; singular values = square roots of eigenvalues; PCA = SVD of the data/covariance matrix.
- Curvature of a manifold at x is the second-order shape of the manifold itself — the Gauss map's derivative.

## Mental Models
- "First order = where you are going; second order = how you bend": Df for position of the graph, quadratic form for its shape.
- "Classify = reduce the quadratic form to squares": every second-variation question (extrema, stability, curvature) becomes signature arithmetic.
- "Constrained = restrict the form to the tangent space": Lagrange finds the point, signature on T_x S decides its type.
- "SVD is the universal measuring stick": axes of ellipses, principal components, condition numbers — any quadratic/probabilistic blob gets its axes from SVD.
- "Manifold ≈ its tangent space, to first order": do calculus in T_x S, then push back.

## Anti-patterns
- **Second-derivative test when the Hessian is degenerate** — inconclusive; go to higher order or perturb.
- **Using similarity invariants for quadratic forms** — congruence preserves signature, not eigenvalues (eigenvalues of the Hessian are basis-dependent numbers; the signature is the invariant).
- **Lagrange without checking constraint qualification** (DG(a) surjective / tangent space well-defined).
- **Confusing mean and Gaussian curvature**: K = κ1κ2 is intrinsic; mean H = (κ1+κ2)/2 is not the invariant that matters for bending without stretching.
- **Treating probability ellipses as data-independent**: the axes come from the covariance's SVD — recompute after any linear change of coordinates.

## Reference Tables
### Second-order classification
| Hessian signature at critical point | Type |
|---|---|
| positive definite (n,0) | strict local min |
| negative definite (0,n) | strict local max |
| indefinite (p,q), p,q>0 | saddle (3.6.10 behavior) |
| semidefinite degenerate | test inconclusive |

### Constrained test (3.7.13)
| Step | Object |
|---|---|
| 1 | Df = λ DG (Lagrange) |
| 2 | tangent space ker DG(a) |
| 3 | signature of Hessian of f − λG restricted to ker DG |
| 4 | (k,0) min, (0,k) max on the constraint |

### SVD fact sheet (3.8)
| Object | SVD content |
|---|---|
| A = VDU* | singular values σ1 ≥ … ≥ 0 |
| covariance Σ = AAᵀ | axes = columns of V, variances = σ² |
| PCA | top-k right singular directions |
| ellipse axes | σj of the whitening map |

## Key Takeaways
Quadratic forms + signature = the classification engine for extrema, saddles, constrained optima, and curvature.
Spectral theorem ⟹ SVD ⟹ computable axes for everything quadratic, including probability.
Manifolds get calculus by working in their tangent spaces.
Taylor polynomials compose and differentiate implicitly — compute the polynomial, not the function.
Gaussian curvature is the intrinsic second-order invariant of a surface.

## Connects To
Ch4 integrates over these manifolds (volume via determinants); ch5's implicit function theorem is the manifold definition in motion; ch6's Stokes theorem integrates forms over manifolds with curvature showing up in the classical vector-calculus identities. Ch2's eigenvalues meet the spectral theorem here; Axler ch6-7 (inner products, self-adjoint operators, SVD) is the pure-math companion.
