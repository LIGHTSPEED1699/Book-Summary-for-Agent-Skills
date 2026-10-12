# Chapter 2: Linear Algebra and Preliminaries

## Core Idea
The entire book runs on four linear-algebra moves: QR decomposition (orthogonal bases and projections), SVD (rank, balancing, order selection), projection theory (orthogonal and oblique — oblique is the heart of subspace ID), and least squares (realization from estimated states). The chapter's payoff is Lemma 2.14: an infinite Hankel matrix has finite rank n **iff** the impulse-response sequence satisfies an n-th order linear recursion — the seed of Ho-Kalman realization and hence of every subspace algorithm.

## Frameworks Introduced
- **QR via Householder (2.4)**: reflect x to αe₁; product of Householder transforms triangularizes A = Q̂R̂; numerically reliable (only first component modified); sign choice opposite to x₁ avoids cancellation.
- **QR as Gram-Schmidt, matrix-style**: if rank(A)=m, columns of Q̂ give orthonormal basis of im(A); columns of Q̂_R basis of the orthogonal complement; with column pivoting, rank-deficient case handled too.
- **Projection theory (2.5)**: projection onto E along F for direct sum R^l = E ⊞ F; projection matrix is exactly an **idempotent** matrix (Π² = Π); im(Π) ⊕ ker(Π) = R^l; Π = C Ĉ (C nonsingular pairing) ⇒ rank(Π) = trace(Π).
- **Orthogonal projection (2.5)**: Π = A(AᵀA)⁻¹Aᵀ; Π symmetric idempotent; Π = I − projection onto ker(Aᵀ).
- **SVD (2.6)**: A = ÛΣV̂ᵀ; four fundamental subspaces from U/V blocks; rank from nonzero σ; spectral norm = σ_max; Eckart-Young style truncation for reduced-rank approximation.
- **Least squares (2.7)**: min ‖Ax − b‖ ⇒ normal equations AᵀAx = Aᵀb; solution x = (AᵀA)⁻¹Aᵀb; projections are the geometry behind it.
- **Hankel rank (2.8)**: Hankel matrix H (constant anti-diagonals); finite rank n ⟺ Markov/impulse sequence obeys y_{k+n} = Σ p_i y_{k+i} (linear recursion); rank = minimal recursion order = system order.

## Key Concepts
- Idempotent = projection; eigenvalues of a projection are 0/1; rank = trace.
- Oblique projection: not symmetric; determined by pair (along-space, onto-space); appears as W_⊥ in subspace algorithms.
- Orthogonal invariance of ℓ₂ and Frobenius norms — justifies QR/SVD-based error analysis.
- Spectral radius ≤ any matrix norm (Lemma 2.1).
- Square-root matrices of PSD matrices (non-unique); used for covariance factorizations later.
- Toeplitz ↔ Hankel via backward identity J: H = T J.
- Cayley-Hamilton, block-matrix inverses, matrix inversion lemma (problems) — everyday tools in later derivations.

## Mental Models
- "Rank is order": the rank of a data/Hankel matrix IS the system's McMillan degree — SVD on data reads off model order.
- "Project, then realize": subspace identification = oblique projection of future output onto future input along past, then least-squares realization; this chapter defines both verbs.
- "Orthogonal transforms are free": QR/SVD never distort distances — that's why they replace normal equations in numerically serious code.
- "Idempotence test": any matrix claimed to be a projector must satisfy Π² = Π; use it to verify algorithm derivations.

## Anti-patterns
- **Normal equations for least squares in production** — square the condition number; use QR (the book itself computes projections via QR/SVD, never AᵀA directly).
- **Householder sign choice same as x₁** — catastrophic cancellation; choose opposite sign.
- **Plain QR for rank-deficient bases** — diagonal zeros in R̂ break the basis claim; use column pivoting or SVD.
- **Confusing oblique with orthogonal projections** — the "along" subspace matters; W_⊥ ≠ W^⊥.

## Reference Tables
### Decomposition → what it gives you
| Tool | Output | Used later for |
|---|---|---|
| QR (Householder) | orthonormal basis, triangular R | LQ of data matrices (ch6, 9, 10) |
| SVD | singular values + 4 subspaces | order selection, balanced realization (ch6, 8) |
| Oblique projection W_⊥ | state estimate from Hankel data | ORT (ch9), CCA (ch10) |
| Least squares | A from estimated states | realization step in every algorithm |

### Projection identities
| Property | Orthogonal | Oblique |
|---|---|---|
| Idempotent | yes | yes |
| Symmetric | yes | no |
| Formula | A(AᵀA)⁻¹Aᵀ | C Ĉ, Π² = Π |
| rank = trace | yes | yes |

## Key Takeaways
QR, SVD, projections, least squares are the book's whole toolkit — learn them as verbs: orthogonalize, rank-reveal, project, fit.
Idempotent matrices are exactly projections; oblique projections are the signature object of subspace identification.
Finite Hankel rank ⟺ linear recursion in the impulse response ⟺ finite-dimensional system (Lemma 2.14, the bridge to realization theory).

## Connects To
Directly feeds ch3 (Hankel/Markov realization), ch5 (orthogonal-projection derivation of Kalman filtering), ch6 (LQ decomposition of data matrices, Ho-Kalman), ch9-10 (oblique projections and CCA as the algorithms' core), and ch11 (closed-loop needs all four tools again). Doraiswami ch5/ch7 use the same least-squares/SVD machinery from the practitioner side.
