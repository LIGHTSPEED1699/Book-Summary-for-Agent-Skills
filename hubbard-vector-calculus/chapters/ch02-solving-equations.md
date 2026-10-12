# Chapter 2: Solving Equations

## Core Idea
Linear algebra built as a solving technology: row reduction is the main algorithm, and its byproducts — kernel, image, dimension formula, change of basis, eigenvalues — are the structure theory. Then the pivot to nonlinear: Newton's method on Df, with Kantorovich's theorem giving checkable hypotheses under which Newton converges (quadratically, "superconverges"). The whole chapter drives toward the inverse and implicit function theorems previewed at 2.10.

## Frameworks Introduced
- **Row reduction (2.1)**: three operations; echelon form; pivots; the algorithm that decides everything about Ax = b.
- **Solution structure (2.2)**: solutions of Ax = b = particular + kernel; homogeneous system solutions = kernel; free variables parametrize.
- **Matrix inverses and elementary matrices (2.3)**: A invertible ⟺ row-reduces to I; E^{-1} explicit; A = product of elementary matrices; [A|I] → [I|A^{-1}].
- **Span, linear independence, basis (2.4)**: columns-as-generators viewpoint; independence = no redundant column; basis = independent spanning set.
- **Kernel, image, dimension formula (2.5)**: ker T and im T; Theorem 2.5.8: dim ker T + dim im T = n — rank-nullity, proved by tracking pivots/free variables.
- **Abstract vector spaces (2.6)**: axioms; subspaces; **change of basis (2.6.20)**: [T]_{new} = B^{-1}[T]B; matrices as coordinate-dependent actors.
- **Eigenvalues/eigenvectors (2.7)**: Tv = λv; distinct-eigenvalue eigenvectors independent (2.7.7); diagonalization; **Perron-Frobenius (2.7.10)**: positive matrices have a real dominant eigenvalue with positive eigenvector — the theorem behind ranking/markov/population models.
- **Newton's method (2.8)**: x_{k+1} = x_k − [Df(x_k)]^{-1} f(x_k); linearize and solve; **Kantorovich's theorem (2.8.13)**: explicit numeric conditions (bound on [Df(x0)]^{-1}, Lipschitz constant of Df, initial residual) guarantee a zero and convergence of Newton from x0.
- **Superconvergence (2.9)**: Newton's error satisfies ‖x_{k+1} − x‖ ≤ C‖x_k − x‖² (2.9.4); stronger Kantorovich version (2.9.8); quadratic convergence = digits double.
- **Inverse/implicit function theorem preview (2.10)**: when Df(a) is invertible, f is locally invertible; implicit = solve some variables for the others.

## Key Concepts
- Row operations = left-multiplication by elementary matrices — algorithm and algebra are the same thing.
- Rank = # pivots; dim ker = # free variables; dimension formula is pivot bookkeeping.
- Similarity: same map, different basis (2.6.20) — eigenvalues are the similarity invariants.
- Perron-Frobenius: spectral radius is an eigenvalue with a positive eigenvector for entrywise-positive matrices; powers of A align with that eigenvector.
- Kantorovich is the book's signature practical theorem: no "sufficiently close" hand-wave — check three numbers at x0 and convergence is guaranteed.
- Newton without Kantorovich can diverge or cycle; the theorem is the safety certificate.

## Mental Models
- "Solve = reduce; structure = what reduction reveals": pivots/free variables ARE rank/kernel dimensions.
- "Newton = replace the nonlinear actor by its derivative, solve, iterate": the derivative-as-linear-map from ch1 becomes an algorithm.
- "Quadratic convergence = correct digits double each step": the payoff of differentiability, not just continuity.
- "Kantorovich: verify at one point, benefit everywhere": a priori convergence from local data + a Lipschitz constant.
- "Eigenvalues are what survives a basis change": matrices change, spectra don't.

## Anti-patterns
- **Inverting [Df(x_k)] numerically each step** instead of solving the linear system (the book's algorithmic stance: row reduce, don't invert).
- **Running Newton without checking Kantorovich-type hypotheses** — no guarantee, classic divergence traps (near critical points, cycles).
- **Confusing "distinct eigenvalues ⟹ independent eigenvectors" with the converse** — diagonalizability needs full eigenspace dimensions (deferred to ch3's SVD-friendly setting).
- **Treating Perron-Frobenius as generic**: positivity (or primitivity) is essential; sign patterns break it.

## Reference Tables
### Ax = b decision tree
| Situation | Outcome |
|---|---|
| pivot in augmented column | no solution |
| no bad pivot | solutions = x_particular + ker A |
| #pivots = n | unique solution |
| dim ker A = n − rank | free-variable count |

### Newton convergence (Kantorovich, 2.8.13/2.9.8)
| Ingredient | Role |
|---|---|
| ‖[Df(x0)]^{-1}‖ ≤ β | conditioning at start |
| ‖Df(x) − Df(y)‖ ≤ γ‖x−y‖ | Lipschitz derivative |
| ‖f(x0)‖ ≤ η | initial residual |
| h = βγ η ≤ ½ (variants sharpen) | convergence certificate |
| conclusion | zero exists; Newton converges, quadratically |

## Key Takeaways
Row reduction is the one algorithm; rank-nullity and invertibility are its bookkeeping.
Change of basis makes matrices secondary to the linear map — eigenvalues are the invariants.
Newton's method is differentiation turned into iteration; Kantorovich turns it into a guaranteed method; superconvergence quantifies the payoff.
Perron-Frobenius is the applied eigenvalue theorem: dominant mode, positive, computable.
Everything here is staged for ch5: invertible Df(a) ⟹ local inversion, implicit solutions.

## Connects To
Axler ch2-3 (dimension formula, change of basis) is the pure version of 2.4-2.6; Axler ch5 (eigenvalues) meets Perron-Frobenius here. Ch3 uses eigenvalues/SVD for quadratic forms and curvature; ch5 proves the inverse/implicit function theorems whose Newton preview is 2.10; ch4's change-of-variables needs determinants from 2.x + 4.8. On the control shelf: Newton-Kantorovich underlies successive linearization and Gauss-Newton identification.
