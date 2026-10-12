# Chapter 6: Eigenvalues and Eigenvectors

## Core Idea
Ax = λx finds the directions a matrix only stretches: eigenvalues λ (roots of det(A − λI) = 0) and eigenvectors x. When A has n independent eigenvectors, A = VΛV⁻¹ diagonalizes it, and the ODE y′ = Ay becomes n decoupled scalar equations with solution y(t) = Σ cᵢe^{λᵢt}xᵢ — stability is exactly Re λᵢ < 0. The matrix exponential e^{At} packages the solution for all initial conditions, and symmetric matrices get the best deal: orthogonal diagonalization and real eigenvalues, which makes second-order systems M y″ = −Ky solvable as normal modes.

## Frameworks Introduced
- **Eigenvalues/eigenvectors (6.1)**: Ax = λx; characteristic polynomial det(A − λI) = 0; trace = Σλ, determinant = Πλ; eigenvectors for distinct eigenvalues are independent; 2×2 stability: T = trace < 0 and D = det > 0; companion matrix for y″ + By′ + Cy = 0 (trace −B, det C — recovers ch2's characteristic equation).
- **Diagonalization (6.2)**: A = VΛV⁻¹ with V = eigenvector matrix; powers Aᵏ = VΛᵏV⁻¹; eigenvalues of Aᵏ are λᵢᵏ; Markov matrices (columns sum to 1: λ = 1 eigenvalue, convergence to steady state).
- **Systems y′ = Ay (6.3)**: solution combination of e^{λᵢt}xᵢ; constants from y(0) = Vc; stability ⟺ all Re λ < 0; repeated eigenvalues with missing eigenvectors give te^{λt} terms (defective case).
- **Matrix exponential (6.4)**: e^{At} = Ve^{Λt}V⁻¹; the single matrix carrying all solutions y(t) = e^{At}y(0); e^{At}e^{Bt} = e^{(A+B)t} only when AB = BA; series definition e^{At} = I + At + (At)²/2! + …; for defective A, extra t-terms from Jordan blocks.
- **Second-order systems & symmetric matrices (6.5)**: M y″ = −Ky with M, K symmetric (K from springs, M mass); normal modes: solve Kx = ω²Mx; symmetric A orthogonally diagonalizable (spectral theorem): real eigenvalues, orthonormal eigenvector matrix Q, A = QΛQᵀ; coupled oscillators' frequencies from eigenvalues.

## Key Concepts
- det(A − λI) = 0; trace and determinant as the first two symmetric functions of eigenvalues.
- Distinct eigenvalues ⟹ independent eigenvectors; diagonalizable ⟺ n independent eigenvectors (symmetric matrices always are).
- Stability of y′ = Ay = left-half-plane eigenvalues — the multi-dimensional generalization of ch2's root test and ch3's linearization.
- e^{At}: the flow map; commutativity condition for splitting exponentials (planted since ch1).
- Markov/steady-state: λ = 1 with all other |λ| < 1 gives convergence to the steady vector (columns-sum-1 convention).
- Spectral theorem (symmetric case): A = QΛQᵀ, orthogonal eigenvectors — the engine of normal modes and (ch7) SVD.
- Defective matrices: repeated λ with fewer eigenvectors → te^{λt} solutions (the Jordan shadow, kept light here).

## Mental Models
- "Eigenvalues are modes, eigenvectors are shapes": each λᵢxᵢ is an independent pure behavior; the solution is their superposition with constants set by y(0).
- "Diagonalize = find coordinates where the matrix is a scalar per direction": V⁻¹AV = Λ turns coupled dynamics into n independent exponentials.
- "Stability = all modes decay": Re λ < 0 everywhere — the shelf's pole condition.
- "e^{At} is the system's memory operator": one matrix, all initial conditions; commutativity is the price of splitting.
- "Symmetric = honest": real eigenvalues, perpendicular eigenvectors, orthogonal change of coordinates — nature's matrices (mass/stiffness, covariance, Laplacian) are symmetric.

## Anti-patterns
- **Assuming every matrix diagonalizes** — defective matrices (fewer eigenvectors than dimension) need t·e^{λt}/Jordan terms.
- **Splitting e^{(A+B)t} into e^{At}e^{Bt}** for noncommuting A, B.
- **Confusing eigenvectors of A with those of Aᵀ** — different directions, same eigenvalues.
- **Reading stability from det or trace alone in n > 2** — need all eigenvalues' real parts (Routh-Hurwitz is the shelf's shortcut for low order).
- **Forgetting Markov eigenvalue λ = 1 is the steady state**, not a growth mode.

## Reference Tables
### Eigenvalue toolkit
| Fact | Statement |
|---|---|
| Characteristic equation | det(A − λI) = 0 |
| Trace/det | Σλ = tr A, Πλ = det A |
| Distinct λ | ⟹ independent eigenvectors |
| Diagonalization | A = VΛV⁻¹ (n independent eigenvectors) |
| Powers | Aᵏ = VΛᵏV⁻¹ |
| Symmetric A | A = QΛQᵀ, real λ, orthonormal Q |

### Dynamics dictionary
| System | Solution | Stable when |
|---|---|---|
| y′ = Ay | Σcᵢe^{λᵢt}xᵢ = e^{At}y(0) | all Re λ < 0 |
| 2×2 y′ = Ay | — | T < 0 and D > 0 |
| y″ + By′ + Cy = 0 (companion) | ch2 roots | B > 0, C > 0 |
| M y″ = −Ky | normal modes cos(ωt), ω² = eig(K,M) | all ω² > 0 |
| Markov step u_{k+1} = Pu_k | → steady state | λ=1 simple, rest |λ|<1 |

## Key Takeaways
Eigen-decomposition turns linear dynamics into independent exponentials; stability is a left-half-plane test on eigenvalues.
e^{At} = Ve^{Λt}V⁻¹ is the complete solution operator for y′ = Ay.
Symmetric matrices are orthogonally diagonalizable — real modes, perpendicular shapes, the spectral theorem.
Second-order mechanical systems solve as normal modes from Kx = ω²Mx.
Defective eigenvalues add polynomial t-factors — the boundary between clean and Jordan behavior.

## Connects To
Ch2's characteristic roots are the 2×2 case; ch3's linearization stability is this chapter's eigenvalue test applied to Jacobians; ch7's SVD is the spectral theorem applied to AᵀA; ch8's Fourier series diagonalizes the derivative operator (eigenfunctions e^{int}). Axler ch5/7-8 is the determinant-free deep theory of the same objects; Hubbard ch3's spectral theorem/SVD is the calculus-side twin. On the control shelf: state-space stability, modal decomposition, LQR's symmetric P, and balanced truncation all run on this chapter.
