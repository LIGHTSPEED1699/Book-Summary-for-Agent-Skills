# Patterns — Vector Calculus, Linear Algebra and Differential Forms (Hubbard & Burke Hubbard)

## Argument patterns

### Linearize, then iterate
Replace the nonlinear map by its derivative at the current point, solve the linear system, step.
Use when: solving f(x) = 0 (Newton 2.8), proving local inversion (A7-A8), superconvergence (2.9).
The Kantorovich certificate (β, γ, η with h ≤ ½) turns iteration into guaranteed existence.

### Classify by signature
Reduce the second-variation quadratic form to a sum of squares; read (p, q).
Use when: critical points (3.6.8), constrained optima (3.7.13 — restrict to the tangent space), curvature (κ1κ2 sign), stability of equilibria.
Completing squares (3.5.3/A13) is the algorithm; congruence, not similarity.

### Measure-zero filter
Boundary/discontinuity sets of measure zero don't affect integrals or theorems.
Use when: integrability (4.3.1/4.4.8), patching parametrizations (5.2), change of variables hypotheses (4.10), fractal dimension thresholds (5.5).

### Volume via Gram determinant
k-volume of flat pieces = √det[vi·vj]; curved pieces carry density √det(DγᵀDγ).
Use when: manifold volumes (5.3), surface area, change of variables (|det DT| is the square-case Gram), the metric in integrals.

### Stokes bookkeeping
∫_S dφ = ∫_∂S φ. Move a derivative from inside the integral to the boundary (or vice versa).
Use when: every integral identity (Green/divergence/classical Stokes 6.11), conservation laws, electromagnetism (dF = 0, d*F = J), showing a quantity is path-independent (φ = dψ via Poincaré 6.13.5).

### d² = 0 conservation
curl grad = 0, div curl = 0, no magnetic monopoles — one identity.
Use when: testing whether a field is a gradient/curl; constructing potentials; obstruction = topology (closed vs exact).

### Compactness converts local to global
Bolzano-Weierstrass / Heine-Borel / uniform continuity (1.6, A3).
Use when: existence of extrema, passing from pointwise to uniform estimates, justifying limit interchanges in proofs.

### Pullback substitution
Changing variables = applying f* to the form; d commutes with f*.
Use when: coordinate changes on manifolds, naturality arguments, functorial proofs.

## Design patterns (choosing the right tool)
- Equation to solve numerically → Newton + Kantorovich (ch2), not fixed-point hand-waving.
- Optimum to classify → Hessian signature on the tangent space (ch3).
- Integral over curved domain → parametrization + Gram density (ch5) or pull the form back (ch6).
- Vector-calculus identity to prove or remember → find its Stokes instance (ch6).
- High-dimensional integral → Monte Carlo (4.6), not grids.
- Limit through an integral → dominated convergence with an explicit dominator (4.11).

## Anti-patterns (cross-chapter)
- Treating partial derivatives as the derivative (ch1's core warning).
- Inverting matrices when you can row-reduce (ch2's algorithmic stance).
- Congruence vs similarity confusion when diagonalizing forms.
- Swapping limits/integrals or sums/integrals without domination.
- Single-chart thinking on closed manifolds (circle needs overlaps).
- Sign errors from boundary orientation — always "outward first".
