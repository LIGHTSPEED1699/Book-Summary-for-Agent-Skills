# Patterns — Linear Algebra Done Right (Axler)

## Argument patterns

### Extend–shrink (the exchange engine)
Any independent list extends to a basis; any spanning list shrinks to a basis.
Use when: you need a basis adapted to a subspace, or a basis where a map looks nice.
The linear dependence lemma (delete a redundant vector, span survives) is the one-line justification every time.

### Flag ⟺ triangular form
T upper-triangularizable ⟺ there is a complete flag {0} ⊂ U1 ⊂ … ⊂ U_{n−1} ⊂ V of invariant subspaces.
Use when: proving "every operator over C is triangular" (build flag by eigenvector + induction) or reading eigenvalues off a diagonal.

### Annihilate, then decompose
Find p with p(T) = 0 (minimal polynomial); factor p; kernels of the factors give invariant pieces.
Use when: diagonalizability (distinct linear factors), generalized eigenspace decomposition, primary decomposition.
This is the book's replacement for determinant-driven arguments.

### Dimension bookkeeping
dim null T + dim range T = dim V; dim U + dim U⊥ = dim V; dim V/U = dim V − dim U.
Use when: proving injectivity/surjectivity, solvability of systems, "right length + one property = basis", equality of two subspaces (containment + equal dimension).

### Adjoint transport
Move T across the inner product to T*, then use null T* = (range T)⊥.
Use when: relating range and kernel geometry, proving normal-operator facts, defining SVD via √(T*T).

### Two-measurements agree (normality)
TT* = T*T ⟺ ‖Tv‖ = ‖T*v‖ for all v ⟺ Re T and Im T commute.
Use when: upgrading Schur's triangular form to a diagonal one; the spectral theorem's hinge.

### Unique representation = independence
Basis ⟺ every vector has exactly one coordinate list; direct sum ⟺ every vector has exactly one block decomposition.
Use when: proving directness (show 0's decomposition is unique), building coordinates relative to subspaces.

### Best approximation = projection
Minimizing ‖v − u‖ over a subspace lands at P_U v with error in U⊥.
Use when: least squares, normal equations, "fit the closest structured object" problems.

### SVD as universal diagonalization
Any T: V → W gets orthonormal bases with T e_j = s_j f_j — built from the spectral theorem applied to T*T, not T.
Use when: norm, rank, pseudoinverse, low-rank approximation, volume, polar decomposition — for ANY map, no normality needed.

### Jordan assembly
On each G(λ,T): T = λI + nilpotent; nilpotent gets strictly-upper-triangular basis; concatenate blocks.
Use when: classifying operators up to similarity; reading minimal/characteristic polynomial exponents.

## Design patterns (choosing the right tool)
- Structure question about T itself → minimal polynomial + invariant subspaces.
- Geometry question about T (sizes, conditioning, approximation) → SVD.
- Solvability of Tx = y → range/null bookkeeping, quotient V/null T.
- Basis-free claim → prove with maps and dimensions; matrices only after.
- Real-field trouble (no eigenvalues) → complexify or accept quadratic factors / 2-planes.

## Anti-patterns (cross-chapter)
- Determinant-first arguments when a dimension count suffices (the book's whole point).
- Confusing similarity (M^{-1}AM) with congruence (M^t A M) transformation laws.
- Reading eigenvalues when singular values are the honest sizes (non-normal T).
- Pairwise-intersection tests for m-fold direct sums.
- Slot-order slips in complex inner products (linear in first slot).
- Trusting Jordan form numerically; use SVD/σmin for robustness work.
