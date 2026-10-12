# Chapter 4: Integration

## Core Idea
Integration built from dyadic pavings: the integral is the limit of sums over a grid, integrability is controlled by measure zero, and the whole theory stays Riemann-based until Lebesgue arrives exactly where it's needed — passing limits through integrals (dominated convergence). Determinants then earn their keep: they measure volume, which makes the change of variables formula a theorem rather than a ritual. Probability rides along from the start (centers of gravity, central limit theorem, Monte Carlo).

## Frameworks Introduced
- **Dyadic paving integral (4.1)**: partition into dyadic cubes, Riemann-type sums; volume of pavings; sum of volumes (4.1.21); the definition is designed so most theorems are easiest to prove.
- **Probability and centers of gravity (4.2)**: density ρ, expectation, variance; **central limit theorem (4.2.7)** stated and used; simulation intuition.
- **Integrability criterion (4.3.1)**: bounded function on a rectangle is integrable iff its discontinuity set has measure zero.
- **Measure zero (4.4)**: countable unions (4.4.4); curves/surfaces in Rⁿ have measure zero; integrable ⟺ discontinuities measure zero (4.4.8).
- **Fubini (4.5.10)**: integrate iteratedly; reduces n-variable integrals to n one-variable integrals; the workhorse computation rule.
- **Numerical methods (4.6)**: Newton-Cotes (trapezoid, Simpson), Gaussian quadrature (optimal nodes via orthogonal polynomials), **Monte Carlo** — dimension-independent convergence O(N^{-1/2}), why randomness beats grids in high dimensions.
- **Other pavings (4.7)**: flexible pavings (more boxes where the function varies fast); Jordan-type content.
- **Determinants (4.8)**: defined via volume characterization — the determinant is the unique alternating multilinear volume scale; cofactor expansion derived, not assumed.
- **Volumes and determinants (4.9)**: volume of parallelepiped = |det|; the determinant's geometric meaning in all dimensions.
- **Change of variables (4.10)**: ∫_T f = ∫_S f∘T |det DT|; proved via measure zero + local linear approximation (the derivative's determinant is the local volume factor).
- **Lebesgue integrals (4.11)**: improper integrals as limits; **dominated convergence for Riemann integrals (4.11.4)**: |f_k| ≤ g integrable ⟹ limit passes through; differentiating under the integral sign (4.11.22); Laplace/Fourier transforms as the motivating playground.

## Key Concepts
- Measure zero is the book's master filter: integrability, curve boundaries, Peano caveats, change of variables hypotheses — all phrased through it.
- Fubini + change of variables = the two computational engines; everything classical (polar, spherical coordinates) is one instance of 4.10.
- |det DT(x)| = local volume magnification — the derivative (ch1) times the determinant (4.8) gives geometry.
- Monte Carlo's convergence rate is dimension-free; grid methods degrade exponentially — the deep probability in high dimensions.
- Dominated convergence is the only limit-interchange tool the book needs; the "dominating function" is the checkable hypothesis.

## Mental Models
- "Integral = organized sum; integrable = discontinuities are negligible": measure zero is the noise threshold.
- "Determinant = volume of the unit cube's image": the algebraic formula is a consequence, not the definition.
- "Change of variables = multiply by the local volume factor": |det DT| is the Jacobian's geometric face.
- "In high dimensions, sample instead of tiling": Monte Carlo trades accuracy for dimension-independence.
- "Limits through integrals need a leash (the dominator)": DCT is the safety certificate, Kantorovich-style.

## Anti-patterns
- **Swapping limits and integrals without domination** — the classic Fourier/series trap the chapter explicitly arms against.
- **Applying change of variables where the map folds** (det DT = 0 sets must be measure-zero handled; injectivity hypotheses matter).
- **Grid quadrature in high dimensions** — exponential node growth; Monte Carlo or sparse pavings instead.
- **Treating improper ∫ as ∫ of a limit** without checking domination or monotone behavior.
- **Defining det by cofactor expansion** — the book defines by volume; formulas follow (and are less error-prone).

## Reference Tables
### Integrability decision
| Situation | Result |
|---|---|
| bounded, discontinuities measure 0 | integrable (4.3.1/4.4.8) |
| discontinuities positive measure | not integrable |
| curve/surface in Rⁿ | measure 0 (so boundaries don't hurt) |

### Numerical integration
| Method | Nodes | Error/convergence |
|---|---|---|
| trapezoid/Simpson | uniform | O(h²)/O(h⁴) low-dim |
| Gaussian quadrature | optimal (orthogonal polys) | exact to degree 2m−1 |
| Monte Carlo | random | O(N^{-1/2}), dimension-free |

### Limit interchange (4.11)
| Tool | Hypothesis | Payoff |
|---|---|---|
| dominated convergence | f_k → f pointwise, |f_k| ≤ g integrable | ∫f_k → ∫f |
| differentiate under ∫ | |∂_t f| ≤ g integrable | d/dt ∫ = ∫ ∂_t |

## Key Takeaways
Measure zero decides integrability and forgives boundaries.
Fubini computes; change of variables transports; |det| is the transport's volume factor.
Determinants are volume — the definition that makes 4.10 natural.
Dominated convergence is the one big limit tool; its dominator is checkable.
Monte Carlo is not a hack: it's the right method in high dimensions, justified by the probability in 4.2.

## Connects To
Ch6 integrates forms over manifolds using exactly this measure/volume machinery; ch5's inverse function theorem supplies the local diffeomorphisms that change of variables consumes. Ch3's curvature meets volume via tubes and coarea-flavored computations. Axler ch9 (determinants as alternating forms) is the algebraic twin of 4.8-4.9. On the control shelf: Monte Carlo for uncertainty propagation, Laplace transforms for linear systems (4.11's playground).
