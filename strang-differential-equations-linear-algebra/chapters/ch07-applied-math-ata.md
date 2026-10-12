# Chapter 7: Applied Mathematics and AᵀA

## Core Idea
When Ax = b has no solution (more measurements than unknowns, inconsistent data), the right answer is the least-squares solution: project b onto the column space, giving the normal equations AᵀAx̂ = Aᵀb. The matrix AᵀA — symmetric, positive (semi)definite — is the recurring hero: it powers least squares, positive-definite theory (pivots/determinants/energy), the SVD (A = UEVᵀ), and the discretized physics of boundary-value problems (Laplace's equation, network Laplacians).

## Frameworks Introduced
- **Least squares and projections (7.1)**: minimize ‖Ax − b‖²; the error e = b − Ax̂ must be orthogonal to C(A) ⟹ AᵀA x̂ = Aᵀb; projection p = A x̂ of b onto C(A); averaging as the 1-column case (pulse example: v = average); line/curve fitting with design matrix V.
- **Positive definite matrices and SVD (7.2)**: xᵀAx > 0 for all x ≠ 0; tests: pivots > 0, leading determinants > 0, eigenvalues > 0; AᵀA always positive semidefinite (xᵀAᵀAx = ‖Ax‖²); **SVD A = UEVᵀ**: U, V orthogonal, E = diag(σᵢ) singular values; columns of V/U are eigenvectors of AᵀA/AAᵀ; A = Σσᵢuᵢvᵢᵀ rank decomposition; ‖A‖ = σ₁.
- **Boundary conditions replace initial conditions (7.3)**: second-order BVPs (−u″ = f with u(0)=u(1)=0) as linear algebra: finite differences give a symmetric positive definite K (the second difference matrix); Green's function/inverse is the impulse-response table.
- **Laplace's equation and AᵀA (7.4)**: discretize u_xx + u_yy = 0 on a grid; the 5-point stencil matrix is again symmetric positive definite, built as sums of AᵀA-type differences; mean value property.
- **Networks and the graph Laplacian (7.5)**: incidence matrix A (edges→nodes), currents obey conservation (Aᵀ-ish node equations), potentials minimize energy xᵀAx; Laplacian L = AᵀA (or incidence product); Kirchmann/graph laws as linear algebra.

## Key Concepts
- Least squares = orthogonality of error to the model space; normal equations are the coordinate form.
- AᵀA positive definite ⟺ A has independent columns (then x̂ unique); semidefinite when dependent.
- Positive definiteness trinity: pivots > 0 ⟺ leading principal minors > 0 ⟺ eigenvalues > 0 (energy xᵀAx > 0).
- SVD diagonalizes every matrix (not just symmetric) via two orthonormal bases; singular values = sqrt of AᵀA eigenvalues; rank-r truncation = best low-rank piece.
- BVP discretization: boundary conditions make the difference matrix square and invertible (vs initial-value ODE flow); inverse = Green's function.
- Graph Laplacian = AᵀA of the incidence matrix: physics (networks, diffusion) is discrete least squares energy.

## Mental Models
- "No solution → closest column combination": least squares is projection, and projection is orthogonality — the same picture as Yp in ch1, now in data form.
- "AᵀA is where math lives": normal equations, covariance, stiffness, Laplacians, Gram matrices — all AᵀA or its kin.
- "Positive definite = energy > 0": three equivalent tests (pivots, minors, eigenvalues) give three ways to verify a model is physical.
- "SVD = two bases making A diagonal": the universal factorization; σ₁ is the gain, σ_min the robustness margin.
- "Discretize physics, get a symmetric positive definite matrix": the shelf's bridge from PDEs to solvable linear algebra.

## Anti-patterns
- **Forming AᵀA numerically when QR would do** (squaring the condition number — Strang teaches normal equations for insight; numerics prefers better routes).
- **Confusing projection p onto C(A) with the data b** — the error e is the perpendicular, not the answer.
- **Assuming AᵀA invertible without checking independent columns**.
- **Treating semidefinite as definite** — nullspace directions mean non-unique minimizers (add regularization or constraints).
- **Forgetting σ_min = 0 at rank deficiency** — the margin that tells you the model is degenerate.

## Reference Tables
### Least squares pipeline
| Step | Object |
|---|---|
| Model | Ax ≈ b (m > n, independent columns) |
| Normal equations | AᵀA x̂ = Aᵀb |
| Fit | p = Ax̂ = projection of b on C(A) |
| Error | e = b − p ⊥ C(A); E = ‖e‖² |

### Positive definite tests (symmetric A)
| Test | Condition |
|---|---|
| Energy | xᵀAx > 0 for all x ≠ 0 |
| Pivots | all n pivots > 0 |
| Determinants | all leading principal minors > 0 |
| Eigenvalues | all λ > 0 |
| Factorization | A = LDLᵀ with dᵢ > 0 (or AᵀA form) |

### SVD facts
| Fact | Statement |
|---|---|
| A = UEVᵀ | U (m×m), V (n×n) orthogonal, E = diag σ₁ ≥ … ≥ 0 |
| Singular vectors | V: eigenvectors of AᵀA; U: of AAᵀ |
| Action | Avᵢ = σᵢuᵢ — diagonal between orthonormal bases |
| Norm | ‖A‖ = σ₁; rank = #σᵢ > 0 |
| Pseudoinverse | A⁺ = V E⁺ Uᵀ (least-squares solution x̂ = A⁺b) |

## Key Takeaways
Least squares = projection onto C(A); normal equations AᵀAx̂ = Aᵀb are its coordinate identity.
Positive definiteness (energy/pivots/minors/eigenvalues) certifies well-posed models.
The SVD gives every matrix orthogonal input/output bases and a diagonal of gains.
Boundary-value problems discretize to symmetric positive definite systems — physics is least squares energy.
The graph Laplacian AᵀA unifies networks, diffusion, and discretized PDEs.

## Connects To
Ch5's column space is the projection target; ch6's spectral theorem builds the SVD from AᵀA; ch8's Fourier series is least squares with orthogonal basis functions (and FFT is fast transforms of the same kind). Axler ch6-7 (inner products, adjoints, SVD) is the pure theory; Hubbard ch3 (quadratic forms, SVD, PCA) the calculus twin. On the control shelf: least-squares identification, H2/H∞ norms (σ₁/σ_min), balanced truncation (Hankel SVD), and LQR's Riccati energy are all this chapter's AᵀA world.
