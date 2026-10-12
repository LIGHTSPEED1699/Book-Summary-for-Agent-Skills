# Appendix: Determinants and Matrix Factorizations

## Core Idea
Determinants are the existence test — det A ≠ 0 ⟺ invertible — with a small rule book (det AB = det A·det B, det Aᵀ = det A, cofactor expansion, Cramer's rule) — and the book's factorizations (A = LU, A = QR, A = QΛQᵀ, A = UEVᵀ, A = AᵀA Cholesky-style) are the periodic table of linear algebra: each one is a change of coordinates that makes a matrix simple.

## Frameworks Introduced
- **Determinant rules**: product rule |AB| = |A||B|; transpose invariance; cofactor expansion (along any row/column); 2×2 and 3×3 formulas; Cramer's rule (explicit but computationally slow); det = product of eigenvalues = product of pivots.
- **Factorization zoo (Matrix Factorizations / Linear Algebra in a Nutshell)**: A = LU (elimination), PA = LU (with exchanges), A = QR (orthogonal columns — least squares), A = QΛQᵀ (spectral theorem, symmetric), A = UEVᵀ (SVD, every matrix), Cholesky A = CᵀC (positive definite), Cayley-Hamilton (A satisfies its own characteristic equation).
- **Big-picture map**: the four fundamental subspaces + eigenvalues + SVD assembled into one picture (Strang's "six pictures" of a matrix).

## Key Concepts
- det as volume scale and singularity detector; product rule makes det a homomorphism GL → ℝˣ.
- Cofactors and Cramer: explicit formulas exist but elimination beats them computationally.
- Every factorization = choosing a basis: pivots (LU), orthonormal (QR), eigenvectors (Λ), singular vectors (SVD).
- Eigenvalue–pivot–determinant bridges: Πλ = det = Πpivots; Σλ = tr.

## Mental Models
- "Factorization = coordinates that flatten the matrix": each letter pair (L,U / Q,R / Q,Λ / U,E,V) says which geometric structure is being exploited.
- "det is a product of pivots": the elimination you already did hands you the determinant free.

## Anti-patterns
- **Using Cramer's rule numerically** — O(n!) flavor vs elimination's O(n³).
- **Expanding determinants to prove eigenvalue facts** when the factorization picture is cleaner (Axler would approve).

## Reference Tables
### Factorization cheat sheet
| Form | Needs | Gives |
|---|---|---|
| A = LU | square, pivots nonzero | solve Ax=b in one pass |
| PA = LU | any square | + row exchanges |
| A = QR | independent columns | least squares, orthogonality |
| A = QΛQᵀ | symmetric | real modes, orthonormal eigenvectors |
| A = UEVᵀ | any matrix | gains, rank, pseudoinverse |
| A = CᵀC (Cholesky) | positive definite | fast stable solve, energies |

## Key Takeaways
Determinants certify invertibility and multiply, but the factorizations carry the structural content.
The factorization table is the book's summary: every matrix has a coordinate system that makes it diagonal or triangular.
Eigenvalues, pivots, and singular values are three lenses on the same object.

## Connects To
Ch4 (LU), ch5 (subspaces), ch6 (Λ), ch7 (SVD, Cholesky via AᵀA). Axler ch5/7-8 and Hubbard ch3 cover the same factorization theory with different emphasis; the shelf uses QR in identification, SVD in balanced truncation/H∞, Cholesky in Riccati/Kalman numerics.
