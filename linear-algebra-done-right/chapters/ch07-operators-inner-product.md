# Chapter 7: Operators on Inner Product Spaces

## Core Idea
With an inner product in hand, every operator gains a twin — its adjoint T* — and the operators that commute with their adjoint (normal, in particular self-adjoint) get orthonormal bases of eigenvectors: the spectral theorem. Pushing the same idea through sqrt(T*T) yields the singular value decomposition, the chapter's (and arguably the book's) most applied object: it diagonalizes any map between possibly different spaces, and its consequences run from operator norms and best low-rank approximation to polar decomposition and volumes.

## Frameworks Introduced
- **Adjoint (7.2)**: ⟨Tv, w⟩ = ⟨v, T*w⟩ (Riesz makes T* linear); ℳ(T*) = conjugate transpose (7.7–7.8); null T* = (range T)⊥ and range T* = (null T)⊥ (7.11).
- **Self-adjoint (7.10)**: T = T*. Eigenvalues real (7.12); eigenvectors for distinct eigenvalues orthogonal (7.13).
- **Normal (7.18)**: TT* = T*T. Self-adjoint, isometries, positive, unitary are all normal; eigenvectors for distinct eigenvalues orthogonal (7.22); T normal ⟺ Re T and Im T commute (7.23).
- **Spectral theorem (7.29 real / 7.31 complex)**: T self-adjoint (real case) or normal (complex case) ⟺ orthonormal basis of eigenvectors ⟺ diagonal matrix w.r.t. some orthonormal basis. Proof route: Schur + normality forces the triangular matrix diagonal (7.24–7.26).
- **Positive operator (7.34)**: ⟨Tv,v⟩ ≥ 0 ⟺ self-adjoint with nonnegative eigenvalues (7.38); every positive T has a unique positive square root (7.39); T*T is always positive (7.40).
- **Isometry / unitary (7.44, 7.51)**: preserves norms ⟺ preserves inner products ⟺ T*T = I (7.49); surjective isometry = unitary: TT* = T*T = I (7.53); unitary eigenvalues on unit circle (7.54); real unitary = orthogonal matrix.
- **QR factorization (7.58)**: A = QR with Q unitary, R upper triangular — Gram-Schmidt in matrix dress. **Cholesky (7.63)**: positive matrix A = R*R — Gram-Schmidt on the columns of the square root.
- **Singular values (7.65)**: eigenvalues of sqrt(T*T); for matrices, square roots of eigenvalues of A*A. Count with multiplicity = dim range T nonzero ones (7.68); isometry ⟺ all singular values 1 (7.69).
- **SVD (7.70 map version / 7.80 matrix version)**: orthonormal bases with T e_j = s_j f_j (maps) / A = UΣV* with nonnegative diagonal Σ (matrices); SVD of T* and pseudoinverse (7.75).
- **Operator norm (7.86)**: ‖T‖ = sup ‖Tv‖/‖v‖ = largest singular value (7.87–7.88); ‖ST‖ ≤ ‖S‖‖T‖.
- **Best low-rank approximation (7.91)**: truncating SVD to k terms gives the closest rank-≤k map in operator norm — Eckart-Young in the book's language.
- **Polar decomposition (7.94)**: T = S sqrt(T*T) with S an isometry; matrix A = UQ with U unitary, Q positive.
- **Geometry consequences (7.96–7.100)**: T maps the unit ball to an ellipsoid with semiaxes = singular values; volume of parallelepiped = product of singular values; invertibility/diagonalizability/trace read from eigenvalues.

## Key Concepts
- Adjoint exchanges range/null with orthogonal complements — the fundamental theorem in inner-product dress: dim range T = dim range T*.
- Normality is exactly the condition that makes Schur's triangular form diagonal: off-diagonal Frobenius mass of a triangular normal matrix is zero.
- Positive = "self-adjoint with nonnegative spectrum", not "⟨Tv,v⟩ > 0 pointwise nonzero"; the square root is unique inside positive operators.
- Singular values are always real nonnegative and exist for ANY map (no normality needed) — that's why SVD travels farther than the spectral theorem.
- rank T = number of nonzero singular values; ‖T‖ = s1; dist to rank-k maps = s_{k+1}.
- Unitary matrices: columns and rows orthonormal; Q* = Q^{-1}.

## Mental Models
- "Adjoint = the inner product's way of moving T to the other slot": every identity with ⟨T·,·⟩ becomes one with T*; null/range orthogonal complements are its signature.
- "Normal = the two ways of measuring ‖Tv‖ agree": TT* = T*T means T and T* have the same singular structure — that's the hinge of the spectral theorem.
- "Spectral theorem = simultaneous diagonalization of Re T and Im T": commuting self-adjoint pairs (7.23) diagonalize together; normality is exactly commutativity of the parts.
- "SVD = spectral theorem applied to T*T, transported": sqrt(T*T)'s eigenvectors are the input basis; T carries them to the output basis scaled by s_j — two bases, one diagonal.
- "Singular values are the honest sizes of a map": operator norm, best rank-k truncation, ellipsoid axes, volume factor — every "how big is T" question answers with the s_j.
- "Polar = polar coordinates for operators": T = (rotation)(stretch), stretch = sqrt(T*T) positive, rotation = isometry — unique when T invertible.

## Anti-patterns
- **Claiming real eigenvalues for normal (not self-adjoint) operators**: normal operators can have complex eigenvalues (e.g. unitaries); only self-adjoint guarantees real.
- **Confusing isometry and unitary over R/C**: over C isometry = unitary automatically; over R an isometry need not be surjective in infinite dimensions — in finite dimensions the characterizations (7.49, 7.53) are the safe route.
- **Taking any square root of T*T**: the SVD/polar machinery uses the unique POSITIVE square root.
- **Reading singular values as eigenvalues**: s_j are eigenvalues of sqrt(T*T), not of T; for non-normal T the lists are unrelated (e.g. nilpotents have s_j > 0 but all eigenvalues 0).
- **Applying the complex spectral theorem over R**: real normal operators (rotations) may have no real eigenvectors — the real theorem needs self-adjoint.
- **Forgetting conjugation in unitary matrix conditions**: Q*Q = I with conjugate transpose; real case drops the conjugate.

## Reference Tables
### Operator taxonomy (finite-dim inner product space)
| Class | Definition | Spectrum | Matrix form (some ON basis) |
|---|---|---|---|
| self-adjoint | T = T* | real | diagonal real |
| normal | TT* = T*T | any | diagonal (complex case) |
| positive | ⟨Tv,v⟩ ≥ 0 | real ≥ 0 | diagonal ≥ 0 |
| isometry | ‖Tv‖ = ‖v‖ | unit circle | Q*Q = I |
| unitary | isometry + surjective | unit circle | Q*Q = QQ* = I |

### SVD fact sheet
| Quantity | SVD expression |
|---|---|
| rank T | #{s_j > 0} |
| ‖T‖ (operator norm) | s1 |
| best rank-k approx error | s_{k+1} |
| det / volume factor | ∏ s_j (square case) |
| pseudoinverse | VΣ⁺U* |
| polar stretch | sqrt(T*T) = VΣV* |

### Factorizations
| Factorization | Form | Built from |
|---|---|---|
| QR | A = QR | Gram-Schmidt |
| Cholesky | A = R*R (A positive) | Gram-Schmidt on sqrt |
| SVD | A = UΣV* | sqrt(T*T) spectral thm |
| Polar | A = UQ (Q positive) | SVD |

## Key Takeaways
Adjoint + normality + spectral theorem: the self-adjoint/normal world is exactly the diagonalizable-with-orthonormal-basis world.
Positive operators have unique positive square roots — the bridge from T to the singular values.
SVD exists for every map, needs no eigenvalue of T itself, and answers norm, rank, approximation, and volume questions in one shot.
QR/Cholesky/polar are the same orthogonalization machinery in matrix clothing.
The control shelf's H2/H∞ norms, balanced truncation, and model reduction are operator-norm + SVD applications of this chapter.

## Connects To
Ch8 handles the non-normal complex case via generalized eigenvectors and Jordan form — the complement of the spectral world. Ch9's determinant = product of singular values (square case) and quadratic forms are self-adjoint/positive geometry. Ch3's adjoint-free matrix transpose and Ch6's Riesz are the prerequisites. In the Skogestad/Stengel shelf: SVD gains, singular-value robustness margins (σmin for stability margins), balanced truncation (Hankel SVD), and LQR's P = P* all instantiate this chapter.
