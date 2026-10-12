# Chapter 5: Integration over Manifolds

## Core Idea
Extend integration from flat rectangles to curved k-dimensional pieces: break the manifold into little k-parallelograms, weight each by its k-volume (computed with the Gram determinant), and take limits. Parametrizations need a looser definition than ch3's to cover objects like the circle; volumes of manifolds come from the derivative's Gram-Schmidt geometry; curvature reappears through integration; fractals show that "dimension" itself can be fractional once measure-zero and volume ideas are sharp.

## Frameworks Introduced
- **k-parallelograms and their volumes (5.1)**: spanned by k vectors; volume = √det(Gram matrix) = product of orthogonalized lengths (Gram-Schmidt); Pythagorean proof machinery.
- **Parametrizations, loosened (5.2)**: existence of parametrizations covering manifolds (5.2.6) — pieces with overlaps allowed, boundaries measure zero; the definition that makes the circle integrable.
- **Volumes of k-manifolds (5.3)**: integrate the k-volume density √det(DγᵀDγ) over the parameter domain; surface area as the 2-volume of a 2-manifold in Rⁿ.
- **Integration and curvature (5.4)**: three theorems connecting curvature to integration; Gaussian curvature via the Gauss map (5.4.6) — K as the local area magnification of the normal map; Gauss-Bonnet flavor (total curvature of a closed surface = 2πχ).
- **Fractals and fractional dimension (5.5)**: sets whose k-volume jumps from ∞ to 0 at a non-integer critical k — Hausdorff-flavored dimension; the boundary between measure zero and positive measure as the dimension meter.

## Key Concepts
- Gram determinant: vol_k(v1,…,vk)² = det[vi·vj] — the Pythagorean theorem in k dimensions; equals the product of squared orthogonal-complement lengths.
- The manifold volume density √det(DγᵀDγ) is the "little number" attached to each parameter-space piece — the metric's square root, prefiguring the Riemannian volume form.
- Overlapping parametrizations are harmless because overlaps have measure zero (ch4's filter again).
- Gauss map curvature: K(p) = det of the normal map's derivative — curvature measured as area distortion, hence intrinsic (Theorema Egregium).
- Fractal dimension: dim = critical exponent where k-volume flips; Cantor, Koch, Sierpinski as measure-zero/positive-measure boundary cases.

## Mental Models
- "Integrate = parallelograms + volumes + limit": the same three-step heuristic everywhere; only the "little piece" changes.
- "Gram determinant = the volume meter of flat pieces; √det(DγᵀDγ) = its transport to curved ones".
- "Curvature is where integration meets differentiation a second time": the Gauss map turns bending into area ratios, which integration then totals.
- "Dimension is a phase transition in volume": fractals make the measure-zero machinery visible.

## Anti-patterns
- **Parametrizing a closed manifold with one chart** — the circle needs overlapping pieces; single-chart parametrizations tear (ch3's strict definition fails exactly here).
- **Forgetting the √det(DγᵀDγ) factor** and integrating over the parameter domain naively — parametrization distortion is the whole point.
- **Confusing k-volume of a manifold with k+1-volume of its region** — surface area vs enclosed volume; the change of variables formula belongs to the latter.
- **Treating fractal dimension as topological dimension** — topology stays integer; volume-based dimension is the fractional one.

## Reference Tables
### k-volume toolkit
| Object | Formula |
|---|---|
| parallelogram vol² | det[vi·vj] (Gram) |
| parametrized manifold vol | ∫ √det(DγᵀDγ) dᵏt |
| surface area (2-manifold) | ∫ ‖∂₁γ × ∂₂γ‖ (R³ case) |
| Gauss curvature | det(dN) = area ratio of Gauss map |

## Key Takeaways
k-volumes via Gram determinants make curved integration mechanical: density = √det(DγᵀDγ).
Looser, overlapping parametrizations + measure-zero overlaps = integration over any manifold.
Curvature becomes integrable through the Gauss map — the bridge to Stokes/ch6 and to Gauss-Bonnet.
Fractal dimensions are volume phase transitions — the sharpest illustration of the measure-zero machinery.

## Connects To
Ch6's forms integrate over exactly these parametrized pieces (the √det machinery becomes the pullback of the volume form); ch3's curvature gets its global theorems here; ch4's measure zero is used constantly. On the shelf: surface-area computations in geometry processing; the Gram determinant is the same object as the controllability Gramian (different context, same algebra).
