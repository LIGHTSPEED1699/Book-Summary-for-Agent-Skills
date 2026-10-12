# Chapter 3: Linear Maps

## Core Idea
Linear maps are the morphisms of vector spaces, and the whole chapter orbits one result: the fundamental theorem of linear maps — dim null T + dim range T = dim V. Matrices are how linear maps become computable once bases are chosen; invertibility, isomorphism, change of basis, quotients, and duality are all consequences of the same dimension bookkeeping.

## Frameworks Introduced
- **Linear map (3.1)**: additivity + homogeneity. ℒ(V,W) is itself a vector space (3.2); ℒ(V) = ℒ(V,V) is the operator arena.
- **null T and range T (3.13, 3.16)**: both subspaces; injective ⟺ null T = {0} (3.14); surjective ⟺ range T = W (3.19).
- **Fundamental theorem of linear maps (3.21)**: dim null T + dim range T = dim V. Proof template: basis of null T → extend to basis of V → images of the extension span range T and are independent.
- **Linear systems as map analysis (3.25–3.28)**: homogeneous solutions = null space (dimension = #variables − #pivots); inhomogeneous: solution exists iff b ∈ range; all solutions = one particular + null space (affine translate).
- **Matrix of a linear map (3.30)**: ℳ(T) relative to ordered bases; addition/scalar mult/multiplication of matrices defined to make ℳ(S+T) = ℳ(S)+ℳ(T), ℳ(ST) = ℳ(S)ℳ(T) (3.35, 3.43).
- **Column picture (3.48–3.51)**: columns of AB = A times columns of B; matrix product = linear combinations of columns; column rank ≤ min(m,n); column rank = row rank via column-row factorization (A = CR with C m×r, R r×n).
- **Invertible linear map (3.59)**: bijective; inverse unique and linear; T invertible ⟺ T injective ∧ surjective (3.64); matrix invertible ⟺ invertible linear map (3.67); inverse matrix = matrix of inverse map (3.68).
- **Isomorphism (3.70)**: invertible linear map; V ≅ W ⟺ dim V = dim W (3.74) — finite-dim spaces are classified by dimension; ℒ(V,W) ≅ F^{m,n} (3.71).
- **Change of basis (3.84)**: ℳ(T, new) = M^{-1} ℳ(T, old) M with M = ℳ(identity).
- **Product spaces (3.87)**: V1×…×Vm with coordinatewise ops; dim adds (3.92); product ≅ direct sum (3.93); a sum is direct iff dimensions add up (3.94).
- **Quotient space V/U (3.99)**: translates v+U as points; operations well-defined on translates; dim V/U = dim V − dim U (3.105); quotient map π: V → V/U surjective with null π = U (3.104).
- **Dual space V′ (3.110)**: linear functionals φ: V → F; dim V′ = dim V (3.111); dual basis (v′1,…,v′n) picking coefficients (3.112–3.114).

## Key Concepts
- Linear maps take 0 to 0 (3.10) — any map failing that isn't linear.
- Injectivity/surjectivity tests via dimensions (3.22–3.23): a map F^4 → F^3 can never be injective; F^3 → F^4 never surjective.
- Matrix multiplication is composition in disguise: (AB)_{j,k} = row j of A · column k of B (3.46); A·(column combination) = same combination of A's columns (3.50).
- Column rank = row rank = rank r enables A = CR factorization — the rank-r world is m×r times r×n.
- Transpose A^t swaps rows/columns (3.54); (AB)^t = B^t A^t.
- Isomorphic copies: ℒ(V,W) ≅ F^{m,n}; every n-dim V ≅ F^n (via a basis).
- Quotient intuition: collapse U to 0, keep the rest; translates are affine subspaces parallel to U; two translates are equal or disjoint (3.101).
- Fundamental theorem recast: dim range T = dim V − dim null T = dim V/U — range T ≅ V/U (the map "T̃(v+U) = Tv" is an isomorphism, 3.95–3.96 style).
- Null space of a matrix (3.76) and dimension of range T = column rank of ℳ(T) (3.78).

## Mental Models
- "Rank-nullity is conservation of dimensions": domain slots split into killed (null) and surviving (range); every theorem about solvability is this equation in costume.
- "Solutions are affine": inhomogeneous solution sets are null space translated — geometry of linear systems = subspace + offset.
- "Matrix = coordinates of a map, not the map itself": the same T has different matrices in different bases; similarity M^{-1}AM is basis change, not a new operator.
- "Columns are the action on basis vectors": multiply A by e_k to get column k; products act columnwise — rank questions become column-span questions.
- "Quotient = delete a subspace from the vocabulary": V/U has one dimension per direction not in U; the quotient map is the universal surjection killing U.
- "Dual = coordinate extractors": a basis makes functionals that read off coefficients; V′ has the same size as V but no preferred identification (basis-free duality is Ch6's Riesz).

## Anti-patterns
- **Counting pivots wrong for homogeneous systems**: dim null = #columns − rank, not #rows − rank.
- **Treating matrix rank and linear-map rank as different notions**: dim range T = column rank of ℳ(T) (3.78) — one number.
- **Assuming AB = BA because matrices "look symmetric"**: composition order matters; (AB)^t = B^t A^t reverses.
- **Confusing product V×W with sum V+W**: product is external (pairs always direct); sum is internal (may overlap); they coincide exactly when the sum is direct (3.93–3.94).
- **Writing quotient elements without checking well-definedness**: operations on translates are well-defined precisely because U is a subspace — the structure theorem behind every "mod out by" move.
- **Identifying V with V′ without a basis**: dim equal ≠ naturally equal; the identification needs an inner product (comes in Ch6).

## Reference Tables
### Fundamental theorem and corollaries
| Statement | Formula |
|---|---|
| Fundamental theorem (3.21) | dim null T + dim range T = dim V |
| Injective test | null T = {0} ⟺ dim range T = dim V |
| Surjective test | range T = W ⟺ dim range T = dim W |
| Homogeneous system | dim solutions = n − rank(A) |
| Inhomogeneous | solvable ⟺ b ∈ range T; solution set = x0 + null T |
| Quotient | dim V/U = dim V − dim U; range T ≅ V/null T |

### Matrix operations ↔ map operations
| Matrix | Map meaning |
|---|---|
| ℳ(S)+ℳ(T) | S+T |
| λℳ(T) | λT |
| ℳ(S)ℳ(T) | ST (compose) |
| ℳ(T)^{-1} | T^{-1} (if invertible) |
| M^{-1}ℳ(T)M | same T, new bases (3.84) |
| column rank | dim range T |

### Product vs quotient vs dual
| Construction | Dimension | Universal property |
|---|---|---|
| V1×…×Vm | Σ dim Vi | pairs; projections |
| V/U | dim V − dim U | surjection killing U |
| V′ | dim V | all F-valued linear measurements |

## Key Takeaways
One equation — null + range = dim V — powers injectivity/surjectivity tests, linear-system structure, quotient dimension, and rank theory.
Matrices are basis-dependent avatars of basis-free maps; similarity is basis change (the seed of Ch5's diagonalization question).
Invertible = injective + surjective = full rank = matrix invertible = domain and range isomorphic; finite dimension makes all these equivalent.
Quotient spaces make the fundamental theorem exact: range T ≅ V/null T.
Duality turns vectors into coefficient-readers; dim V′ = dim V.

## Connects To
Ch4 applies polynomials to operators (needed to factor p(T)); Ch5 uses null/range of (T − λI) for eigenvectors and the fundamental theorem for the characteristic-polynomial bound. Ch6's Riesz representation replaces the basis-dependent dual with inner-product duality. Ch7's adjoint is the map-side twin of the transpose from 3.54. Ch9's determinants finally measure how much volume a map distorts — the signed version of "how much range fills W".
