# Chapter 8: Complex Integration: Cauchy's Theorem

## Core Idea
Integrating along contours in the plane forces the question "which path?" — and the answer for analytic functions is the book's central miracle: Cauchy's Theorem. The integral between two points depends only on the endpoints (equivalently, loop integrals of analytic functions vanish), and the deeper "Deformation Theorem" says an integral is invariant as the contour is dragged through analytic terrain — singularities are pegs the rubber band can't cross. Everything else (residues, winding-number formulas, the residue theorem) is bookkeeping of how many times the contour winds around the pegs.

## Frameworks Introduced
- **Contour integration (I-II)**: Riemann sums of complex f along a directed contour; sums have a beautiful geometric reading — the Riemann sum is itself a polygonal path (the "sum-path"), and the integral is the vector from its start to its finish.
- **Area interpretation (IV-V)**: ∮ z̄ dz = 2i·(signed area); for general loops ∮ z̄ dz = 2i Σ ν_j A_j over regions with winding numbers ν_j — integration detects winding-weighted area.
- **Power functions (VI)**: ∮ z^m dz evaluated visually: Riemann sums trace circular arcs; for m ≠ −1 the sum-path closes (integral 0 on loops); m = −1 is the exceptional case giving 2πiν — the birth of the residue.
- **Cauchy's Theorem (III)**: if f is analytic in the region between two contours with common endpoints, the integrals agree; loop integrals of analytic functions vanish.
- **Deformation Theorem (VI.3)**: the value of an integral is unchanged while the contour deforms through analytic points — rubber band and peg picture; extends to multiply-connected regions: a loop around several singularities = sum of loops around each (additivity, formula (12)).
- **Residues (VI.5)**: partial fractions / Laurent expansion; only the 1/(z−s) coefficient survives integration: ∮ f dz = 2πi Σ ν(C, s_k) Res[f, s_k] — Cauchy's Residue Theorem in embryo.
- **Exponential mapping (VII)**: ∫ e^z dz = e^B − e^A via sum-path = image arc; singularity-free ⟹ always path-independent.
- **Fundamental Theorem of Contour Integration (VIII)**: if f has an analytic antiderivative F (F′ = f), then ∫ f dz = F(B) − F(A) and the sum-path is the image of the contour under F; antiderivative exists ⟺ path-independence; non-analytic f has no F.
- **Cauchy's Integral Formula (IX, preview)**: f(a) = (1/2πi) ∮ f(z)/(z−a) dz — values inside determined by boundary values (proved next chapter).

## Key Concepts
- The Riemann sum as a path: each term f(z)Δ is a directed segment; the integral is the closing vector. This makes evaluations *visible* (arcs, polygons).
- z̄ dz integrates to area (2i × signed area); z^m dz (m ≠ −1) sum-paths close; 1/z is the unique power whose sum-path fails to close (2πi per winding).
- Cauchy's Theorem is "super-fundamental": path-independence for analytic f; the Fundamental Theorem (antiderivatives) is the downstream convenience.
- Deformation = homotopy through analytic points; winding number about each singularity is the conserved quantity (Hopf's theorem at work).
- Residue = coefficient of the complex-inversion term in the Laurent expansion; integration annihilates every other term.
- Antiderivative existence is equivalent to vanishing of all loop integrals — analyticity of f is necessary for F.
- Multiply-connected additivity: big loop = sum of small loops around each peg.

## Mental Models
- "The sum-path is the answer": draw the Riemann sum as a polygonal curve; the integral is its start-to-finish vector — evaluation becomes geometry.
- "Singularities are pegs, contours are rubber bands": only the winding numbers about pegs matter; shape is irrelevant.
- "Only the 1/z term pays rent": every Laurent term integrates to zero on loops except the inversion coefficient — that's the residue.
- "Cauchy beats Newton": path-independence comes from analyticity itself, not from finding an antiderivative; the Fundamental Theorem is the luxury version.
- "Area is an integral of z̄": non-analytic integrals measure winding-weighted area — the exception that teaches the rule.

## Anti-patterns
- **Assuming path-independence for non-analytic f** — z̄ gives area, which flagrantly depends on the contour.
- **Ignoring winding numbers in the residue theorem** — ∮ = 2πi Σ ν·Res, not just 2πi Σ Res; a loop winding twice pays double.
- **Treating the Fundamental Theorem as the foundation** — antiderivatives may not exist; Cauchy/Deformation is the deeper principle.
- **Deforming across a singularity** — the peg blocks; each crossing changes the value by 2πi·Res.
- **Forgetting m = −1 is special among powers** — all other powers close their sum-paths; the −1 term is the whole story of residues.

## Reference Tables
### Loop integrals of powers (closed contour C)
| f | ∮_C f dz |
|---|---|
| z^m, m ≠ −1 integer | 0 (any loop) |
| 1/z | 2πi ν(C, 0) |
| z^{-n}, n ≥ 2 | 0 (any loop) |
| z̄ | 2i Σ ν_j A_j (winding-weighted area) |

### Theorem hierarchy
| Theorem | Content | Scope |
|---|---|---|
| Cauchy | analytic between paths ⟹ equal integrals | simply-connected |
| Deformation | contour dragged through analytic points preserves value | homotopy |
| Additivity | loop around k pegs = sum of loops | multiply-connected |
| Fundamental | F′ = f analytic ⟹ ∫ = F(B)−F(A) | antiderivative exists |
| Residue | ∮ f = 2πi Σ ν(C,s_k) Res[f,s_k] | isolated singularities |

## Key Takeaways
Contour integrals are vectors closing the Riemann sum-path — evaluation is geometry.
Cauchy's Theorem: analyticity kills contour dependence; loop integrals vanish.
Deformation Theorem: only winding numbers about singularities are conserved.
Residues are the surviving 1/(z−s) coefficients; the residue theorem is winding × residue bookkeeping.
Antiderivatives exist exactly when loop integrals vanish — analyticity is the gatekeeper.

## Connects To
Ch7's winding numbers and Hopf degree theorem are the conserved quantities here; ch9's Cauchy Integral Formula and Laurent series make the residue machinery full-strength (and give the "explicit formula" promised for the area/winding results); ch10-11's vector-field integrals (flux/circulation) are the physical avatar of these same loop integrals; ch12's flows use path-independence as the definition of potential flow. Hubbard's differential forms + Stokes is the general theorem Cauchy's is a special case of; Axler/Strang unaffected — this is analysis, not algebra.
