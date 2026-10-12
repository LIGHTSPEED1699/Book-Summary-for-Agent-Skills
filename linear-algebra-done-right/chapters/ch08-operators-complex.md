# Chapter 8: Operators on Complex Vector Spaces

## Core Idea
Drop the inner product and normality, and diagonalization fails exactly when eigenvectors run short. The fix: generalized eigenvectors — vectors killed by a power of (T − λI). The generalized eigenspaces always decompose V completely (over C), the characteristic polynomial finally appears (defined via multiplicity, still determinant-free), and the Jordan form packages everything into explicit blocks.

## Frameworks Introduced
- **Null spaces of powers (8.2)**: null(T − λI)^j grow and stabilize; generalized eigenspace G(λ,T) = null(T − λI)^dim V (8.7).
- **Generalized eigenvector (8.6)**: (T − λI)^j v = 0 for some j ≥ 1.
- **Nilpotent operator (8.14)**: T^m = 0; has only eigenvalue 0; has a basis where the matrix is strictly upper triangular (8.16).
- **Generalized eigenspace decomposition (8.22)**: over C, V = G(λ1,T) ⊕ … ⊕ G(λm,T) with λj distinct eigenvalues; T restricted to G(λj,T) = λj I + nilpotent.
- **Multiplicity (8.10/8.31)**: dim G(λ,T) = number of times λ appears on the diagonal of any upper-triangular matrix of T.
- **Characteristic polynomial (8.24)**: p(z) = ∏(z − λj)^{dim G(λj,T)}; degree = dim V; zeros = eigenvalues with multiplicity (8.28).
- **Block diagonal matrices (8.35)**: T has a block-diagonal matrix with upper-triangular blocks ⟺ each generalized eigenspace picture assembled (8.37).
- **Square roots of operators (8.38–8.41)**: invertible operator over C has a square root; count of square roots governed by how many distinct square roots each Jordan block admits.
- **Jordan form (8.42–8.45)**: basis in which the matrix is Jordan blocks J_{mj}(λ) — λ on diagonal, 1s on superdiagonal; block sizes from the nilpotent structure of (T − λI) on G(λ,T).
- **Trace (8.46–8.52)**: sum of diagonal entries of the matrix; basis-independent; equals sum of eigenvalues with multiplicity; tr(ST) = tr(TS).

## Key Concepts
- The chain {0} ⊂ null(T−λI) ⊂ null(T−λI)² ⊂ … stabilizes at dim V power; G(λ,T) is the stable kernel.
- Eigenvectors = first layer of G; missing eigenvectors are replaced by Jordan chains (v, (T−λI)v, … read backwards).
- Diagonalizable ⟺ every G(λ,T) = E(λ,T) ⟺ minimal polynomial has distinct roots (ties back to 5.62).
- Minimal polynomial: p_min(z) = ∏(z − λj)^{size of largest Jordan block for λj}; characteristic polynomial uses ALL block sizes.
- Every invertible complex operator has a square root (8.38); real operators may not (negative rotations); count of square roots = 2^{#distinct eigenvalues} for diagonalizable invertible case.
- Trace is the first spectral statistic that survives without diagonalization: sum of eigenvalues with multiplicity.

## Mental Models
- "Generalized eigenvectors = eigenvectors of the stable kernel": don't ask what T−λI kills, ask what some power kills; stabilization is guaranteed by dimension.
- "λI + nilpotent on each block": the local structure theorem — every complex operator is diagonal plus a strictly-upper-triangular nuisance on each generalized eigenspace.
- "Jordan blocks are the atoms": similarity classification of complex operators = block sizes per eigenvalue; minimal polynomial reads the biggest block, characteristic polynomial reads all blocks.
- "Multiplicity has three faces": dim G(λ,T) = diagonal count in triangular form = root multiplicity of the characteristic polynomial — 8.31 welds them together.
- "Trace before determinant": the sum of eigenvalues arrives here with no determinant machinery; the product (det) waits for Ch9.

## Anti-patterns
- **Expecting a Jordan basis of eigenvectors**: Jordan chains are not eigenvectors beyond the first element; only the chain heads live in E(λ,T).
- **Confusing minimal and characteristic polynomials**: same zeros, different exponents (largest block vs all blocks); diagonalizability reads the minimal one.
- **Assuming square roots always exist**: over C only invertibility guarantees one; over R, operators without real log/sqrt structure fail (rotation by π with negative eigenvalue pairs).
- **Using Jordan form numerically**: it's discontinuous in the entries (defective matrices are dense boundaries); the shelf's robustness arguments use SVD/σmin instead.
- **Forgetting the field**: over R the decomposition needs the real/imaginary pair handling from Ch4's quadratic factors; the clean statement is a complex-field statement.

## Reference Tables
### Polynomial twins
| Object | Exponent of (z − λ) | Reads |
|---|---|---|
| characteristic polynomial | dim G(λ,T) (all blocks) | total multiplicity |
| minimal polynomial | size of largest Jordan block | nilpotent depth |
| diagonalizable ⟺ | both square-free | blocks all 1×1 |

### Structure ladder (complex V)
| Always true | With more hypotheses |
|---|---|
| generalized eigenspace decomposition | diagonalizable iff eigenvectors fill |
| Jordan form basis exists | normal ⟺ Jordan blocks 1×1 (Ch7) |
| block upper-triangular matrix | nilpotent ⟺ single block λ=0 shape |

## Key Takeaways
Over C every operator splits into λI + nilpotent pieces on generalized eigenspaces — the complete structure theorem without inner products.
The characteristic polynomial and multiplicity arrive determinant-free via generalized eigenspaces; Jordan form makes the classification explicit.
Minimal polynomial (largest blocks) vs characteristic polynomial (all blocks) is the sharpest diagnostic pair in the book.
Trace is basis-independent and spectral: sum of eigenvalues with multiplicity.
Diagonalization is the generic-looking but non-generic case; nilpotent defect is measured by Jordan block sizes.

## Connects To
Ch5's minimal polynomial governs the block sizes here; Ch7's spectral theorem is the special case where all blocks are 1×1 and bases orthonormal. Ch9's determinant finally gives the product-of-eigenvalues companion and an alternative route to characteristic polynomials. In the control shelf: state-space modal forms, defective modes and Jordan blocks in margin analysis, and trace formulas (e.g., sum of closed-loop poles) are direct applications.
