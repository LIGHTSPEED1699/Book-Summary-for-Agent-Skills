# Chapter 5: Eigenvalues and Eigenvectors

## Core Idea
An eigenvalue is a λ for which T − λI kills something nonzero; the minimal polynomial — the monic polynomial of least degree annihilating T — is the chapter's master object: its zeros are exactly the eigenvalues, and its factorization decides triangularizability and diagonalizability. No determinants anywhere: existence of eigenvalues comes from the minimal polynomial built out of dim ℒ(V) = n².

## Frameworks Introduced
- **Operator** = linear map from V to itself (5.1); **invariant subspace** U: TU ⊂ U (5.2); restriction T|_U (5.4).
- **Eigenvalue/eigenvector (5.5, 5.8)**: Tv = λv, v ≠ 0 ⟺ T − λI not injective ⟺ null(T − λI) ≠ {0} (5.7). Eigenvector lists are automatically independent (5.11); ≤ n eigenvalues (5.12).
- **p(T) (5.14)**: plug z = T into a polynomial; (ST = TS ⟹ (ST)m = S^m T^m for polynomials in one operator).
- **Minimal polynomial (5.24)**: monic (5.21) p of least degree with p(T) = 0; exists because I, T, …, T^{n²} are dependent in ℒ(V) (dim n²); divides every annihilating polynomial (5.25); zeros of minimal polynomial = eigenvalues (5.27).
- **Existence without determinants**: over C every operator has an eigenvalue (5.28 — minimal polynomial has a root); over R, every odd-dimensional space's operator does (5.34), and even-dimensional real operators can have none (rotation; null-space parity result 5.32–5.33).
- **Upper-triangular criterion (5.39)**: T has upper-triangular matrix ⟺ there are invariant subspaces {0} ⊂ U1 ⊂ … ⊂ U_{n−1} ⊂ V with dim Uj = j. Eigenvalues = diagonal entries (5.41). Over C: every operator triangularizable (5.47).
- **Eigenspace E(λ,T) = null(T − λI) (5.52)**; eigenspaces sum is direct (5.54).
- **Diagonalizability (5.55, 5.62)**: T diagonalizable ⟺ V = E(λ1,T) ⊕ … ⊕ E(λm,T) (λj all distinct eigenvalues) ⟺ minimal polynomial of T has distinct linear factors (over C: distinct roots).
- **Gershgorin disk theorem (5.67)**: each eigenvalue lies in some disk centered at A_{j,j} with radius Σ_{k≠j}|A_{j,k}| — eigenvalue localization from matrix entries.
- **Commuting operators (5.66–5.81)**: ST = TS; eigenspaces of T invariant under S; commuting families are simultaneously diagonalizable iff each is diagonalizable (5.76); simultaneously upper-triangularizable always over C (5.80); eigenvalues of S+T and ST pair up (5.81).

## Key Concepts
- Characteristic polynomial appears here only as a counting device (each eigenvalue's multiplicity ≤ n; sum of multiplicities ≤ n) — the determinant-based version waits for Ch9.
- Minimal polynomial with distinct linear factors = diagonalizable; repeated factors measure the nilpotent defect (seed of Ch8's Jordan form).
- Real operators without eigenvalues (rotations of R²) still have invariant 2-planes = whole space; quadratic factors of the minimal polynomial are the real shadow of conjugate pairs.
- Eigenspace dimension ≤ multiplicity; equality per eigenvalue ⟺ diagonalizable.
- Gershgorin: diagonally dominant matrices have eigenvalues near the diagonal — the practical read of 5.67.

## Mental Models
- "Minimal polynomial is the operator's DNA": its roots are the eigenvalues, its factor pattern decides diagonal/triangular/Jordan structure; annihilate first, decompose after.
- "Invariant subspace ladder = triangular form": upper-triangular matrix ⟺ a complete flag of invariant subspaces; diagonalizable ⟺ the flag can be made from eigenspaces.
- "Eigenvalue = failed invertibility": T − λI loses injectivity; everything else (eigenspaces, directness) is null-space bookkeeping.
- "Commuting = respecting each other's eigenspaces": S preserves E(λ,T), so on each eigenspace recurse — simultaneous triangularization is induction on flags.
- "No determinants needed for existence": dim ℒ(V) = n² forces a polynomial relation on T; over C it must have a root. The book's namesake trick.

## Anti-patterns
- **Expecting real eigenvalues in even dimensions**: rotations on R² have none; over R only odd dimension guarantees one (5.34).
- **Confusing algebraic and geometric multiplicity**: dim E(λ,T) can be strictly less than the eigenvalue's multiplicity; diagonalizability is exactly the equality case.
- **Assuming distinct eigenvalues are necessary for diagonalizability**: they're sufficient, not necessary — the test is the minimal polynomial's distinct linear factors (5.62).
- **Adding eigenvalues of S and T when S,T don't commute**: 5.81's pairing needs commutativity.
- **Using det(T − λI) arguments**: available only from Ch9; the chapter's whole point is that the structure theory precedes determinants.

## Reference Tables
### Structure ladder (F = C)
| Property of minimal polynomial | Structure of T |
|---|---|
| any (splits) | upper-triangular matrix exists (5.47) |
| distinct linear factors | diagonalizable (5.62) |
| (z − λ1)^{m1}…(z − λm)^{mm} | generalized eigenspace decomposition (Ch8) |

### Eigenvalue bookkeeping
| Quantity | Bound / formula |
|---|---|
| # distinct eigenvalues | ≤ dim V (5.12) |
| dim E(λ,T) | ≤ multiplicity of λ |
| diagonalizable ⟺ | Σ dim E(λj,T) = n |
| Gershgorin | λ ∈ ∪j {z: |z − Ajj| ≤ Σ_{k≠j}|Aj,k|} |

### Commuting family (F = C)
| Statement | Condition |
|---|---|
| simultaneous diagonalization | each diagonalizable (5.76) |
| simultaneous upper triangularization | automatic (5.80) |
| common eigenvector | always (5.78) |

## Key Takeaways
The minimal polynomial replaces determinants as the eigenvalue engine: roots = eigenvalues, factor pattern = structure.
Triangularizable over C always; diagonalizable iff the minimal polynomial has no repeated factors.
Eigenspaces always give a direct sum; whether it fills V is the diagonalizability question.
Commuting families share eigenspaces and flags — simultaneous forms follow.
Gershgorin is the only entry-level eigenvalue localization in the book, and it's determinant-free.

## Connects To
Ch6-7 add inner products: self-adjoint/normal operators are automatically diagonalizable (spectral theorem), making the minimal-polynomial test look easy in hindsight. Ch8 finishes the non-diagonalizable case: generalized eigenspaces and Jordan form read off the repeated factors of the minimal polynomial. Ch9's characteristic polynomial gives the determinant-based multiplicity count this chapter avoided. In the control shelf: Skogestad/Stengel diagonalization and modal decompositions are the diagonalizable case; Jordan blocks are the defective case.
