# Chapter 1: Vectors, Matrices, and Derivatives

## Core Idea
The book's thesis in one move: the derivative of a function of several variables is a LINEAR TRANSFORMATION, and its matrix is the Jacobian. Partial derivatives are just the entries of that matrix — they are not the derivative. Everything classical (chain rule, gradient, mean value inequalities, C¹ criteria) becomes linear algebra once you see Df(a) as the unique L with f(a+h) ≈ f(a) + L(h).

## Frameworks Introduced
- **Points and vectors (1.1)**: Rⁿ as positions and as displacements; column-vector notation.
- **Matrices as actors (1.2–1.3)**: matrix multiplication defined so that composition of linear maps = product of matrices; identity, diagonal, transpose; row-column rule.
- **Geometry of Rⁿ (1.4)**: dot product, length, distance, angle, triangle inequality (1.4.9); orthogonal vectors; the metric that everything later measures against.
- **Limits and continuity (1.5)**: sequential and ε-δ limits; limits of compositions (1.5.22); continuous = preserves limits; linear functions are uniformly continuous (1.5.33).
- **Five big theorems (1.6)**: the compactness toolkit — Bolzano-Weierstrass (every bounded sequence has a convergent subsequence, 1.6.3, nonconstructive), extreme value theorem (continuous on compact ⟹ max/min), intermediate value theorem, uniform continuity on compacta (1.6.9: local ⟹ global), and curves have area zero (with the Peano-curve warning that continuity alone isn't enough — topology is needed).
- **Derivative as linear map (1.7)**: Proposition/Definition 1.7.9 — f differentiable at a if a unique linear L with f(a+h) = f(a) + L(h) + o(‖h‖); Theorem 1.7.10 — the matrix of L is the Jacobian [Jf(a)]; partial derivatives exist but are only the matrix entries.
- **Chain rule (1.7)**: D(g∘f)(a) = Dg(f(a)) ∘ Df(a) — composition of linear maps, i.e., matrix multiplication; gradient appears as the row vector Df for scalar f.
- **Computing derivatives (1.8)**: product/quotient/power rules in several variables; directional derivatives; gradient as the representing vector of Df via the dot product.
- **Mean value machinery (1.9)**: MVT for several variables (1.9.1: f(b) − f(a) = Df(c)(b−a) along the segment); corollary ‖f(b)−f(a)‖ ≤ sup‖Df‖·‖b−a‖; criterion for differentiability: C¹ ⟹ differentiable with derivative = Jacobian (1.9.8) — the workhorse test.

## Key Concepts
- Uniqueness of L is proved via the Jacobian columns L(eᵢ) = Dᵢf(a) — the derivative, if it exists, is the Jacobian.
- Partial derivatives alone don't guarantee differentiability; C¹ (continuous partials) does (1.9.8). Non-C¹ functions are "outlaws obeying none of the standard theorems".
- Chain rule as matrix product makes exotic substitutions mechanical (e.g., d/dt f(x(t)) = [Df][x′(t)]).
- Lipschitz ratios previewed (2.8): sup of ‖Df‖ over a segment controls function differences — the seed of contraction arguments in ch2.
- Compactness is the engine behind all existence statements: max/min, uniform continuity, convergent subsequences.

## Mental Models
- "Derivative = best linear approximation": a plane touching a surface, but stated basis-free as a linear map; the Jacobian is its coordinate shadow.
- "Chain rule = multiply the linear maps": never memorize index forms; compose the actors.
- "Partial derivatives are matrix entries, not the actor itself": the common one-variable intuition is the trap this chapter exists to defuse.
- "Compactness converts local to global": continuity → uniform continuity, bounded → convergent subsequence, candidate sequences → actual extrema.
- "Five big theorems are one theorem in disguise": completeness of Rⁿ wearing different hats.

## Anti-patterns
- **Defining the multivariable derivative as "the vector of partials"** — partials can exist everywhere yet the function fail to be differentiable (even continuous).
- **Using the one-variable MVT equality form in several variables** — only the inequality corollary survives (the point c is not constructive and equality fails for vector-valued f).
- **Assuming a continuous curve bounds a nice region** — Peano curves fill triangles; "curve has area 0" needs more than continuity.
- **Trusting nonconstructive existence as computable** — Bolzano-Weierstrass locates nothing (the book flags this explicitly).

## Reference Tables
### Derivative dictionary
| Object | Meaning |
|---|---|
| Df(a) | unique linear map with f(a+h) = f(a) + Df(a)h + o(‖h‖) |
| [Jf(a)] | matrix of Df(a); entries Dⱼfᵢ (partials) |
| ∇f | Df as a column via dot product (scalar f) |
| C¹ | partials exist and are continuous ⟹ differentiable (1.9.8) |

### Chain rule
| Form | Statement |
|---|---|
| Maps | D(g∘f)(a) = Dg(f(a))·Df(a) |
| Matrices | Jacobians multiply |
| Curves | d/dt f(γ(t)) = [Df(γ(t))]γ′(t) |

## Key Takeaways
The derivative is a linear transformation; the Jacobian is its matrix; partials are its entries.
Chain rule is composition of linear maps — matrix multiplication, nothing more.
C¹ is the practical differentiability certificate; without it the standard theorems fail.
Compactness (Bolzano-Weierstrass) powers every existence theorem in the book.
MVT survives as an inequality via sup‖Df‖ — the basis of Lipschitz and contraction estimates in ch2.

## Connects To
Ch2 runs Newton's method on these derivatives (invertibility of Df is the question); ch3's Taylor polynomials iterate the derivative idea; ch5's inverse and implicit function theorems ask exactly when Df(a) is invertible; ch6's forms eat the chain rule for breakfast (d(φ∘f) = f*φ). The linear-algebra shelf (Axler ch3: invertible linear maps, rank) is the standing companion.
