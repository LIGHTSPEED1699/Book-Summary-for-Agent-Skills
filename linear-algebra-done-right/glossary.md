# Glossary — Linear Algebra Done Right (Axler, 4th ed. 2024)

## Standing notation
- **F**: R or C — every definition/theorem proves both versions at once.
- **V, W**: vector spaces over F; **operators** = maps V → V.
- **𝐅^S**: all functions S → F (F^n is the case S = {1,…,n}; F^∞ = sequences).
- **𝒫(F)**: polynomials over F; **𝒫_m(F)**: degree ≤ m (dimension m+1).

## Structure
- **subspace**: nonempty subset closed under + and scalar mult (contains 0).
- **span(v1,…,vm)**: all linear combinations; smallest containing subspace; span( ) = {0}.
- **direct sum U ⊕ W**: sum with unique decomposition; test U ∩ W = {0} (two summands).
- **dim V**: length of any basis; finite-dim = finite spanning list exists.
- **product V×W**: external pairs (always direct); **quotient V/U**: translates v+U as points, dim = dim V − dim U.
- **dual V′**: linear functionals V → F; dim V′ = dim V; **dual basis** reads coefficients.

## Maps
- **ℒ(V,W)**: linear maps V → W (a vector space); **ℒ(V)** = operators (dim n²).
- **null T / range T**: kernel and image; **fundamental theorem**: dim null T + dim range T = dim V.
- **ℳ(T)**: matrix of T relative to ordered bases; change of basis M^{-1}ℳ(T)M.
- **rank**: dim range T = column rank = row rank; column-row factorization A = CR.
- **isomorphism**: invertible linear map; V ≅ W ⟺ dim equal.
- **quotient map π**: V → V/U surjective, null π = U; range T ≅ V/null T.

## Eigen theory
- **eigenvalue λ**: T − λI not injective; **eigenvector** v ≠ 0 with Tv = λv.
- **eigenspace E(λ,T)** = null(T − λI).
- **p(T)**: polynomial in T (z ↦ T).
- **minimal polynomial**: monic annihilating p of least degree; divides all annihilating polynomials; zeros = eigenvalues.
- **invariant subspace**: TU ⊂ U; **restriction** T|_U.
- **generalized eigenspace G(λ,T)** = null(T − λI)^dim V; **multiplicity** = dim G(λ,T).
- **characteristic polynomial**: ∏(z − λj)^{dim G(λj,T)}; later = det(zI − A).
- **nilpotent**: T^m = 0; **Jordan block** J_m(λ): λ diagonal, 1 superdiagonal.
- **trace**: sum of diagonal entries; basis-free; = Σ eigenvalues.

## Inner product
- **inner product**: conjugate-symmetric, linear in FIRST slot (Axler convention), positive definite.
- **norm** ‖v‖ = √⟨v,v⟩; **orthogonal** ⟨u,v⟩ = 0.
- **orthonormal basis**: ON list that spans; exists always (Gram-Schmidt).
- **Riesz**: every φ ∈ V′ is ⟨·, u⟩ for unique u.
- **U⊥**: orthogonal complement; V = U ⊕ U⊥; **P_U** orthogonal projection (best approximation).

## Operators with adjoint
- **adjoint T***: ⟨Tv,w⟩ = ⟨v,T*w⟩; ℳ(T*) = conjugate transpose; null T* = (range T)⊥.
- **self-adjoint** T = T* (real spectrum); **normal** TT* = T*T; **positive** ⟨Tv,v⟩ ≥ 0; **isometry** ‖Tv‖ = ‖v‖; **unitary** surjective isometry (Q*Q = QQ* = I).
- **spectral theorem**: normal (C) / self-adjoint (R) ⟺ orthonormal eigenbasis.
- **singular values s_j(T)**: eigenvalues of √(T*T); **SVD**: T e_j = s_j f_j; A = UΣV*.
- **operator norm** ‖T‖ = max s_j; best rank-k error = s_{k+1}.
- **polar decomposition** T = S√(T*T), S an isometry.

## Multilinear
- **bilinear form**: linear in each slot; matrix transforms M^t A M; **symmetric** / **alternating** (β(v,v)=0).
- **quadratic form** q(v) = β(v,v).
- **m-linear form** V^(m); **alternating**: sign flip on swap, vanishes on dependent inputs.
- **det**: unique alternating normalized n-linear form; det = ∏ eigenvalues (C).
- **tensor product V⊗W**: dim = product; v⊗w; bilinear maps factor through it.
