# Cheatsheet — Linear Algebra Done Right (Axler, 4th ed. 2024)

## Decision procedures

### Is T diagonalizable? (F = C)
1. Compute minimal polynomial (find least-degree relation among I, T, …, T^{n²}).
2. Distinct linear factors ⟺ diagonalizable.
3. Equivalently: Σ_λ dim E(λ,T) = n; equivalently every eigenvalue's geometric multiplicity = algebraic.
Over R: also need all eigenvalues real (minimal polynomial splits over R).

### Eigenvalue existence
- F = C: always (minimal polynomial has a root).
- F = R: guaranteed only when dim V odd; even dim can have none (rotations).

### Solvability of Tx = y
- y ∈ range T ⟺ solution exists; solution set = x0 + null T.
- Matrix form: rank(A) = rank([A|b]); dim solution space = n − rank(A).

### Is a list a basis?
- Check length = dim V plus ONE of: independent, or spanning.
- Or: every vector has unique representation (2.28).

### Is a sum direct?
- Two summands: U ∩ W = {0}.
- m summands: 0 = v1+…+vm only trivially; or dim adds up to dim(U1+…+Um).

### Invariant subspace finds eigenvalue
U invariant, dim U = 1 ⟹ U is an eigenspace direction. Odd-dim real proof: flag of invariant subspaces from complexification.

### Best rank-k approximation
SVD A = UΣV*; truncate to k largest s_j; error in operator norm = s_{k+1}.

### Operator norm / conditioning
‖T‖ = s1; smallest gain = s_n; invertible ⟺ s_n > 0; ‖T^{-1}‖ = 1/s_n.

## Factorization recipes
| Factorization | Form | Exists when |
|---|---|---|
| Schur | A = Q*TQ (T upper-tri) | always over C |
| Spectral | A = Q*ΛQ | A normal (self-adjoint over R) |
| QR | A = QR | always (Q unitary, R upper-tri) |
| Cholesky | A = R*R | A positive definite |
| SVD | A = UΣV* | always |
| Polar | A = UP (P positive) | always; U unique if A invertible |
| Jordan | A = SJS^{-1} | always over C |

## Key identities
- dim null T + dim range T = dim V; range T ≅ V/null T.
- dim(U+W) = dim U + dim W − dim(U∩W); dim U⊥ = dim V − dim U.
- det = ∏ eigenvalues = ∏ singular values; tr = Σ eigenvalues.
- p_char(z) = det(zI − A); p_min | p_char (Cayley-Hamilton: p_min(T) = 0).
- Gershgorin: each λ in some disk |z − A_jj| ≤ Σ_{k≠j} |A_jk|.
- Cauchy-Schwarz |⟨u,v⟩| ≤ ‖u‖‖v‖; parallelogram ‖u+v‖² + ‖u−v‖² = 2‖u‖² + 2‖v‖².
- Hadamard: |det A| ≤ ∏ ‖column_j‖.

## Spectral dictionary (operator class → what you get)
| Class | Test | Spectrum | Form |
|---|---|---|---|
| self-adjoint | T = T* | real | ON eigenbasis |
| normal | TT* = T*T | any | ON eigenbasis (C) |
| positive | self-adj, λ ≥ 0 | ≥ 0 | √T exists unique positive |
| unitary | T*T = TT* = I | \|λ\| = 1 | ON eigenbasis (C) |
| isometry | T*T = I | unit circle | partial unitary |
| nilpotent | T^m = 0 | {0} | strictly upper-tri |

## Minimal vs characteristic polynomial
| | minimal | characteristic |
|---|---|---|
| exponent of (z−λ) | largest Jordan block | Σ block sizes |
| degree | ≤ n | n |
| decides | diagonalizability | total multiplicity, det, trace |

## Quick "done right" moves
- Want det-free eigenvalue existence → minimal polynomial from dim ℒ(V) = n².
- Want canonical complement → orthogonal complement (inner product) or quotient (no inner product).
- Want to compare two bases → change-of-basis M = ℳ(identity).
- Want functional concretely → Riesz vector.
- Want "size" of a non-normal map → singular values, not eigenvalues.
