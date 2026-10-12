# Chapter 9: Multilinear Algebra and Determinants

## Core Idea
Determinants finally arrive — built the hard, honest way from alternating multilinear forms rather than assumed. A determinant is the unique alternating n-linear normalization on matrices; everything else (multiplicativity, eigenvalue product, change of variables) is a consequence. The chapter also opens the multilinear world (bilinear forms, quadratic forms, tensor products) that pure linear algebra otherwise hides.

## Frameworks Introduced
- **Bilinear forms (9.1)**: linear in each of two slots; V^(2) with dim (dim V)² (9.5); matrices of bilinear forms transform by M^t A M under basis change (9.7).
- **Symmetric bilinear forms (9.9)**: diagonalizable — orthonormal basis with diagonal matrix (9.12); quadratic form q_β(v) = β(v,v) (9.18), diagonalization of quadratic forms (9.23).
- **Alternating bilinear forms (9.14)**: β(v,v) = 0 ⟺ alternating (9.16); V^(2)_alt has dimension n(n−1)/2.
- **m-linear forms (9.25)**: V^(m); alternating ⟺ vanishes when inputs dependent (9.28); no nonzero alternating m-forms for m > dim V (9.29).
- **Permutations and sign (9.31–9.35)**: swapping two inputs flips sign; every alternating form evaluated by the signed permutation sum.
- **Determinant (9.39/9.41)**: the alternating 2-form formula generalizes: det A = Σ_{σ} (sign σ) ∏ A_{σ(j),j}; the unique alternating normalization with det I = 1.
- **Determinant properties (9.47–9.67)**: multiplicative (9.49); similarity invariant (9.52); over C det = product of eigenvalues (9.55); det A^t = det A; det of dual/adjoint (9.56); row-operation evaluation tricks (9.57); Cayley-Hamilton (9.64); Hadamard's inequality (9.66); Vandermonde determinant (9.67).
- **Tensor product V⊗W (9.71)**: dimension dim V · dim W (9.72); basis v_j ⊗ w_k (9.74); universal property for bilinear maps (9.77–9.80); tensor product of inner product spaces (9.82+).

## Key Concepts
- Characteristic polynomial (defined in Ch8 via multiplicity) now equals det(zI − A) — the two constructions are welded (9.65 connects trace and determinant to the characteristic polynomial coefficients).
- det(T) = product of eigenvalues (with multiplicity, over C); det = volume scale factor of the parallelepiped (Ch7's singular-value product).
- Cayley-Hamilton: p(T) = 0 where p is the characteristic polynomial — the minimal polynomial divides it.
- Trace = sum of eigenvalues (Ch8), determinant = product: the two spectral aggregates meet.
- Quadratic forms diagonalized by symmetric bilinear form theory — signature/inertia live here (positive ⟺ all diagonal entries > 0 after diagonalization).
- Tensor products: bilinear measurements factor uniquely through a linear map out of V⊗W.

## Mental Models
- "Determinant = the signed volume detector": an alternating form can't see dependent inputs (volume zero); the sign records orientation; uniqueness pins the normalization.
- "Alternating = antisymmetric + characteristic ≠ 2 collapse": swapping inputs flips sign, so the permutation sum is the only possible formula.
- "Multiplicativity is the whole game": det(AB) = det A det B makes det a group homomorphism GL(V) → F×; similarity invariance and eigenvalue product follow for free.
- "Bilinear forms = matrices with two transformation rules": change of basis M^t A M; symmetric/alternating split the space of forms; quadratic forms are the diagonal shadow.
- "Tensor = linearize bilinearity": every bilinear map becomes linear on V⊗W; dimension multiplies because pairs of basis vectors multiply.

## Anti-patterns
- **Computing determinants by expansion for structure questions**: use multiplicativity, row operations, and eigenvalue products (9.57's toolkit) instead of cofactor brute force.
- **Assuming det(A+B) = det A + det B**: det is multiplicative, never additive.
- **Confusing the two matrix transformation laws**: linear maps conjugate (M^{-1}AM); bilinear forms co-conjugate (M^t A M).
- **Forgetting the sign when swapping**: alternating forms flip sign per transposition; the permutation sign is well-defined (9.34).
- **Treating tensor products as Cartesian products**: dim multiplies, and v⊗w is not a pair — most tensors are sums of simple tensors.

## Reference Tables
### Determinant properties
| Property | Statement |
|---|---|
| multiplicative | det(AB) = det A det B (9.49) |
| similarity invariant | det M^{-1}AM = det A (9.52) |
| spectral | det = ∏ eigenvalues over C (9.55) |
| transpose/adjoint | det A^t = det A = det A* |
| volume | |det| = parallelepiped volume = ∏ singular values |
| characteristic | p(z) = det(zI − A) (ties to Ch8 def) |

### Multilinear landscape
| Object | Space | Dimension |
|---|---|---|
| m-linear forms | V^(m) | (dim V)^m |
| alternating m-forms | V^(m)_alt | C(n,m); 0 for m > n |
| bilinear forms | V^(2) | n² |
| symmetric / alternating | split | n(n+1)/2 / n(n−1)/2 |
| tensor product | V⊗W | (dim V)(dim W) |

## Key Takeaways
Determinant = unique alternating normalized multilinear measurement; multiplicativity then does the heavy lifting.
det = product of eigenvalues, trace = sum: the characteristic polynomial's constant and linear coefficients (9.65).
Cayley-Hamilton: every operator annihilates its own characteristic polynomial.
Quadratic forms are symmetric bilinear forms in disguise and diagonalize cleanly.
Tensor products complete the algebra: bilinear becomes linear.

## Connects To
Ch8's characteristic polynomial and multiplicity get their determinant identity here; Ch7's singular-value volume formula equals |det| in the square case; Ch5's minimal polynomial divides the characteristic polynomial (Cayley-Hamilton). In the control shelf: det for characteristic equations of state-space models, RGA (relative gain array uses det), volume/ellipsoid arguments in robustness (σmin already did the heavy lifting in Ch7).
