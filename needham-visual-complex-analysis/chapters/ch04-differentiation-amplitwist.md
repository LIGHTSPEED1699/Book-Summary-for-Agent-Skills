# Chapter 4: Differentiation: The Amplitwist Concept

## Core Idea
The complex derivative f′(q) is an "amplitwist": under a complex-differentiable map, every infinitesimal vector at q is enlarged by |f′(q)| and rotated by arg f′(q) — the same complex number for all directions. This is only possible because the real Jacobian happens to be a matrix of the special form [[a,−b],[b,a]] that represents complex multiplication; the Cauchy-Riemann equations are precisely the statement that the Jacobian has this form. Conformality (angle preservation) and analyticity (complex differentiability) are the same phenomenon seen geometrically and symbolically.

## Frameworks Introduced
- **The puzzling phenomenon (II)**: empirically, every "natural" complex function maps infinitesimal squares to infinitesimal squares — the mystery this chapter solves.
- **Local description of plane mappings (III)**: any smooth mapping R² → R² stretches by two principal expansion factors along two principal directions (Jacobian SVD in modern language); general maps turn squares into rectangles.
- **The amplitwist (III.3)**: maps whose local effect is equal enlargement + equal rotation for all infinitesimal vectors — amplification × twist = multiplication by a single complex number.
- **The complex derivative (IV)**: f′(q) = lim [f(z) − f(q)]/(z − q) with z → q from any direction; for z² the quotient → 2q uniformly; the derivative IS the amplitwist of the map at q.
- **Analytic functions (IV.3)**: complex differentiability throughout a region; the derivative's own mapping picture; analytic ⟹ conformal (except where f′ = 0).
- **Conformality and the Riemann sphere (V)**: angle preservation on the sphere via stereographic dictionary; breakdown of conformality: critical points (f′ = 0, angles multiply by k+1 where k = order of zero of f′) and branch points (z^{1/n} type).
- **Geometry of linear transformations (VI-VIII)**: Jacobian matrix J = [[α,β],[γ,δ]]; equal expansion factors in all directions ⟺ J has the rotation-dilation form [[a,−b],[b,a]] ⟺ CR equations α = δ, β = −γ; complex multiplication = this matrix class.

## Key Concepts
- The difference quotient [f(z) − f(q)]/(z − q) is itself a geometric object: the amplitwist taking the infinitesimal vector (z − q) to [f(z) − f(q)]; the derivative exists when this quotient settles to one value independent of direction.
- Real differentiability is not enough: directional derivatives always exist for smooth real maps, but the quotient must be direction-independent — that's CR.
- CR equations: ∂u/∂x = ∂v/∂y, ∂u/∂y = −∂v/∂x — the Jacobian commutes with 90° rotation (i.e., is complex-linear).
- Conformal = angle-preserving (orientation-preserving); anticonformal = angle-preserving with reversal (z̄, conjugation); critical points f′(q) = 0 crush angles (multiply by k+1); branch points are fractional-power angle multiplication.
- Möbius transformations are conformal because they preserve circles and angles (ch3's geometry feeding ch4's analysis).
- The derivative as a map: f′(z) itself maps regions — its zeros are the critical points of f.

## Mental Models
- "Zoom in: the map becomes its derivative" — an amplitwist: one complex number acting on every infinitesimal vector.
- "CR = the Jacobian secretly being a complex number": the matrix [[a,−b],[b,a]] is multiplication by a+ib; CR is the fingerprint.
- "Conformality and analyticity are one fact in two languages": geometry (squares stay squares) ↔ algebra (direction-independent quotient).
- "f′ = 0 is where the map goes degenerate": angle multiplication (critical points) is the failure mode; z² at 0 doubles angles.
- "Squaring's hyperbolas teach orthogonality": preimages of grid lines under z² are orthogonal hyperbolas — conformality visible without derivatives.

## Anti-patterns
- **Assuming real differentiability gives a complex derivative** — directional quotients generally disagree (z̄ fails: quotient e^{−2iθ} depends on direction).
- **Calling f′ = 0 points conformal** — they multiply angles (critical points); z² at 0 doubles.
- **Confusing conformal with "angle magnitude only"** — conformal keeps orientation too; z̄ is isogonal but anticonformal.
- **Treating CR as a formal trick** — it's the statement that the Jacobian is complex-linear; the whole theory of ch5-9 stands on it.
- **Forgetting the derivative's own mapping picture** — f′ as a function locates exactly where f degenerates.

## Reference Tables
### Local mapping taxonomy
| Jacobian type | Local effect | Example |
|---|---|---|
| general 2×2 | rectangle (2 principal factors) | generic smooth map |
| [[a,−b],[b,a]] | amplitwist (conformal) | analytic f, f′ = a+ib |
| [[a,b],[b,−a]] | anticonformal | f(z̄), e.g. conjugation |
| singular | crushing | f′ = 0 critical point |

### Failure modes of conformality
| Feature | Cause | Angle behavior |
|---|---|---|
| critical point | f′(q) = 0 (order k) | angles × (k+1) |
| branch point | z^{1/n} type | angles × 1/n (multivalued) |

## Key Takeaways
The complex derivative is a single complex number — the common amplitwist of all infinitesimal vectors.
CR equations = the Jacobian being a complex multiplication matrix; they are the analytic face of conformality.
Analytic maps preserve infinitesimal squares; conformality breaks exactly at critical and branch points.
Geometry (ch3's circle/angle preservation) and analysis (CR) meet in this chapter and stay merged for the rest of the book.
The derivative f′ viewed as its own map pinpoints where f degenerates.

## Connects To
Ch5 computes amplitwists visually (log, rules of differentiation) and reveals CR in Cartesian/polar form; ch6's non-Euclidean geometry lives on conformal maps; ch8-9's Cauchy theorems exploit analyticity's rigidity first glimpsed here; ch12's harmonic functions are real parts of analytic ones. Hubbard's derivative-as-linear-map is the multivariable generalization (where conformality is the exception, not the rule); Strang's Jacobians are the same matrices without the complex-multiplication miracle.
