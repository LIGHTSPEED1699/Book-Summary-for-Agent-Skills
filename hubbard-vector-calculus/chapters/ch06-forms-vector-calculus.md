# Chapter 6: Forms and Vector Calculus

## Core Idea
Differential forms are integrands: a k-form eats an oriented k-parallelogram and returns a number. That single geometric reading makes the entire vector-calculus circus — grad, curl, div, Green, Stokes, Gauss, and even Maxwell's equations — one theorem: ∫_S dφ = ∫_∂S φ. The exterior derivative d is the unique operator making this true, and the pullback makes it coordinate-free. This is the book's title payoff.

## Frameworks Introduced
- **k-forms (6.1)**: fields of alternating k-linear functionals on tangent spaces; 1-forms as "things you integrate along curves", 2-forms over surface patches; dx^i, wedge products dx^i1∧…∧dx^ik as the standard basis.
- **Integrating form fields (6.2)**: pull the form back to the parameter domain via the parametrization, integrate the resulting top-form density over the parameter rectangle.
- **Orientation (6.3)**: consistent choice of "which side is positive" on a manifold; orientability (Möbius as the non-example); orientation-preserving reparametrization invariance (6.4.10) — why the integral of a form doesn't need a metric.
- **Integration over oriented manifolds (6.4)**: patch together with parametrizations; forms, not volumes, are the natural integrands.
- **Forms ↔ vector calculus dictionary (6.5)**: 1-forms ↔ vector fields (dot with dr), 2-forms in R³ ↔ flux fields; the classical line and surface integrals are form integrals.
- **Boundary orientation (6.6)**: "outward normal first" (or the right-hand rule) convention making ∂S an oriented manifold with corners.
- **Exterior derivative (6.7)**: dφ defined by its integral behavior / computed by the antiderivative-style formula (6.7.4); graded Leibniz for the wedge (6.7.9: d(φ∧ψ) = dφ∧ψ + (−1)^deg φ φ∧dψ); **d² = 0**.
- **grad/curl/div unified (6.8)**: d on 0-, 1-, 2-forms in R³ = grad, curl, div; the identities curl grad = 0 and div curl = 0 are d² = 0.
- **Pullback (6.9)**: f*φ, the chain rule for forms; d commutes with pullback: d(f*φ) = f*(dφ).
- **Generalized Stokes's theorem (6.10)**: ∫_S dφ = ∫_∂S φ for oriented manifolds with boundary.
- **Classical theorems as corollaries (6.11)**: Green, divergence/Gauss, Stokes-for-surfaces (6.11.4), all one instance.
- **Electromagnetism (6.12)**: F = 2-form of fields; dF = 0 (no magnetic monopoles) and d*F = J (sources) — Maxwell's equations as two lines; the language's conceptual simplification is the book's central motivation.
- **Potentials and Poincaré's lemma (6.13)**: dφ = 0 (closed) ⟹ φ = dψ (exact) on star-shaped domains (6.13.5); when potentials exist and when topology obstructs them.

## Key Concepts
- Forms integrate without a metric; volumes (ch5's √det) need one — the distinction explains why form integrals are reparametrization-invariant.
- Alternating = sign under swap = orientation sensitivity; that's why forms and orientation are inseparable.
- d is defined by generalized Stokes (or equivalently the coordinate formula); its three magic properties: linear, graded Leibniz, d² = 0.
- The de Rham sequence in R³: 0 → functions → 1-forms → 2-forms → 3-forms → 0 with grad/curl/div; exact ⟹ closed; Poincaré lemma makes closed ⟹ exact locally.
- Pullback = substitution done right: changing variables in an integral is applying f* to the form.
- Maxwell: F = E dx∧dt + … ; the homogeneous equations are dF = 0, inhomogeneous are d*F = J; potentials A with F = dA exist exactly because dF = 0 (Poincaré).

## Mental Models
- "A form is an integrand, d is its boundary accountant": every integral theorem is bookkeeping between a region and its edge.
- "d² = 0 is the only conservation law you need": curl grad = 0, div curl = 0, no monopoles — all one identity.
- "Closed vs exact = topology's fingerprint": potentials exist locally (Poincaré) but global failures (angle form dθ on the circle) measure holes.
- "Pullback is the chain rule wearing a hat": substitution in integrals = f*; naturality d f* = f* d is the coordinate-free chain rule.
- "One theorem to end the circus": generalized Stokes swallows Green/STokes/divergence — learn one, own five.

## Anti-patterns
- **Integrating forms over non-orientable or unoriented domains** — orientation is part of the data (Möbius strips break the integral).
- **Confusing closed and exact globally** — Poincaré's lemma needs star-shaped (or contractible) domains; dθ is closed not exact on R²∖{0}.
- **Mixing forms and vector fields without the dictionary** — curl is d on 1-forms in R³ with the metric used to identify; in curvilinear coordinates the identification changes.
- **Computing d with memorized formulas instead of the wedge rules** — 6.7.4 + graded Leibniz regenerate everything.
- **Applying Stokes with mismatched boundary orientation** — the "outward first" convention is where sign errors live.

## Reference Tables
### Forms ↔ vector calculus (R³)
| k-form | Vector object | d on it | Classical |
|---|---|---|---|
| 0-form f | scalar | df | grad f |
| 1-form ω | vector field F | dω | curl F |
| 2-form ψ | flux field | dψ | div F |
| 3-form | density | d = 0 | — |

### Integral theorems as Stokes
| Classical theorem | Form statement |
|---|---|
| FTC | ∫_[a,b] df = f(b) − f(a) |
| Green | ∫_D d(P dx + Q dy) = ∮_∂D |
| Stokes (surfaces) | ∫_S dω = ∮_∂S ω |
| Divergence | ∫_V dψ = ∮_∂V ψ |
| Maxwell homogeneous | dF = 0 |

## Key Takeaways
Forms are oriented integrands; the integral needs no metric, only orientation.
d is the boundary's dual: ∫_S dφ = ∫_∂S φ is the whole book's punchline.
d² = 0 unifies curl grad = 0, div curl = 0, and the absence of magnetic charge.
Potentials exist iff closed (locally — Poincaré); global obstructions detect holes.
The pullback makes all of this coordinate-free: substitution is functorial.

## Connects To
Ch5's parametrized manifolds and volumes are the domains; ch4's measure zero handles the patching; ch3's tangent spaces are what forms act on; ch1's chain rule becomes d f* = f* d. Axler ch9 (alternating multilinear forms, determinants) is the algebraic foundation of k-forms. On the control shelf: energy/storage functions as 0-forms, passivity/port-Hamiltonian systems use exactly this d-structure; the shelf's loop calculus and geometric control lean on it.
