# Chapter 5: Further Geometry of Differentiation

## Core Idea
Drop the R² crutch and differentiate directly in the complex plane with infinitesimal geometry. The Cauchy-Riemann equations are just "the image square is spanned by i times its side-vectors", and they take four forms depending on coordinates (Cart-Cart: i∂ₓf = ∂_y f; Polar-Cart: ∂_θf = ir∂_r f; Cart-Polar; Polar-Polar). The payoff is rigidity: an analytic function is forced by startlingly little data — e.g. the logarithm is THE unique conformal map sending concentric circles to parallel lines — and derivatives can be read off pictures (visual differentiation).

## Frameworks Introduced
- **CR revealed (I.2)**: a fine Cartesian mesh of squares maps to squares; image side-vectors ε∂ₓf and ε∂_y f must satisfy i∂ₓf = ∂_y f — CR as a restatement of "squares stay squares"; derivative formulas f′ = ∂ₓf = −i∂_y f.
- **Polar form (I.3)**: polar mesh (dr, r dθ) maps to square ⟹ ∂_θf = ir∂_r f; derivative f′ = e^{−iθ}∂_r f = −(i/z)∂_θf; Polar-Polar form for f = R e^{iΨ}: ∂_θR = −rR∂_rΨ, R∂_θΨ = r∂_rR; cross-checking two formulas proves analyticity (z³ example).
- **Rigidity (II)**: analytic functions are crystals — behavior on a tiny region (or even just a closed curve's image) determines everything inside; worked gem: circles → vertical lines forces f = A log z + B via the "impossible equation" ∂_θV = r∂_rU (LHS θ-only, RHS r-only ⟹ both constant).
- **Visual differentiation (III)**: compute amplitwists from pictures: log z's perpendicular arrow at z maps to vertical displacement δ ⟹ amplification 1/r, twist −θ ⟹ (log z)′ = 1/z, branch-independent.
- **Rules of differentiation (IV)**: chain rule (amplitwists multiply: (g∘f)′ = g′(f)·f′), inverse functions (f⁻¹′ = 1/f′), sums/products — all immediate from the amplitwist picture.
- **Polynomials, power series, rational functions (V)**: term-by-term differentiation of power series is valid inside the disc of convergence; rational functions analytic except at poles; derivatives of the elementary maps (1/z → −1/z², Möbius M′ = (ad−bc)/(cz+d)²).

## Key Concepts
- Four coordinate forms of CR — choose the one adapted to the geometry of the problem (Polar-Cart when circles map to lines).
- f′ = ∂ₓf = −i∂_y f = e^{−iθ}∂_r f = −(i/z)∂_θf: the derivative is any side-vector ratio of the image square.
- Rigidity/identity theme: analytic functions determined by vanishingly small data; "crystal grown from a seed" — the preview of Cauchy's formula (ch9) and analytic continuation.
- Uniqueness characterization of log: conformal + circles→parallel lines ⟹ A log z + B — geometric definitions pin down functions.
- Visual differentiation: find the image of one convenient infinitesimal arrow; amplification × twist = f′; works for multifunctions branch-independently.
- Chain rule as multiplication of amplitwists — composition of local rotations+dilations.
- Local area magnification = |f′|² (Jacobian determinant of the amplitwist matrix).

## Mental Models
- "CR = the image of a square is a square": every form of CR is one mesh choice; pick coordinates matching the picture.
- "Analytic functions are rigid crystals": partial information → total information; never trust that a mapping pattern admits many analytic solutions (it usually admits one).
- "Differentiate by looking": one arrow's image gives the whole amplitwist.
- "Two formulas agreeing proves analyticity": computing f′ two ways (∂_r vs ∂_θ) and getting the same answer is a certificate.
- "Amplitwists multiply under composition": the chain rule is just complex multiplication of local effects.

## Anti-patterns
- **Checking CR at a single point** — must hold throughout a neighborhood (the xy/|z|² counterexample satisfies CR at 0 yet isn't differentiable there).
- **Assuming conformal-looking behavior implies analyticity** — non-analytic maps can mimic many conformal signatures (the (x²+y²) + i(y/x) example).
- **Using one coordinate form of CR when the geometry begs another** — polar data with Cartesian CR is fighting the problem.
- **Fearing term-by-term differentiation of series** — legitimate inside the disc of convergence.
- **Tracking branches when differentiating log** — the amplitwist is branch-independent; m never appears.

## Reference Tables
### CR in four dressings
| Domain coords | Image coords | Compact form | Derivative |
|---|---|---|---|
| Cartesian | Cartesian | i∂ₓf = ∂_y f | f′ = ∂ₓf = −i∂_y f |
| Polar | Cartesian | ∂_θf = ir∂_r f | f′ = e^{−iθ}∂_r f = −(i/z)∂_θf |
| Cartesian | Polar (f = Re^{iΨ}) | ∂ₓR = R∂_yΨ, ∂_yR = −R∂ₓΨ | — |
| Polar | Polar | ∂_θR = −rR∂_rΨ, R∂_θΨ = r∂_rR | — |

### Derivatives by picture
| Map | Visual input | Amplitwist |
|---|---|---|
| log z | perpendicular arrow → vertical δ | 1/z (all branches) |
| 1/z | arc + radial arrow | −1/z² |
| Möbius M | normalized coefficients | (ad−bc)/(cz+d)² |
| zⁿ | n-gon wrapping | nz^{n−1} |

## Key Takeaways
CR equations are "squares stay squares" in whatever coordinates you like; four forms, pick the adapted one.
Analytic rigidity: minimal data (a curve's image, circle-to-line behavior) forces the whole function — log characterized geometrically.
Visual differentiation computes amplitwists from single arrows, branch-independently.
Chain/inverse/sum/product rules are immediate geometry: amplitwists multiply, invert, add.
Agreement of two derivative formulas doubles as an analyticity certificate.

## Connects To
Ch6 applies rigidity to build non-Euclidean geometry (disc automorphisms characterized by conformality + circle preservation); ch7's winding numbers and ch8-9's Cauchy theory make rigidity quantitative (the explicit "curve determines interior" formula is Cauchy's); ch11's Laurent series extend term-by-term calculus to annuli; ch12's harmonic functions read CR in Polar-Polar dress. Hubbard's implicit/visual calculus and Strang's chain-rule bookkeeping are the real-analysis cousins.
