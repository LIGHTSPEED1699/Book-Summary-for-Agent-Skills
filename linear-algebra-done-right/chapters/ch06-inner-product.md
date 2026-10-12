# Chapter 6: Inner Product Spaces

## Core Idea
Add one extra structure — an inner product — and geometry (length, angle, distance, orthogonality) appears inside a bare vector space. The payoff trio: Gram-Schmidt turns any basis into a nice one, Riesz identifies every linear functional with an inner product against a fixed vector, and orthogonal projection solves the least-distance problem and gives V = U ⊕ U⊥.

## Frameworks Introduced
- **Inner product (6.2)**: conjugate-symmetric, additive, homogeneous in first slot, positive definite; inner product space (6.4). Dot product is the default; function spaces get integral inner products (6.3).
- **Norm ‖v‖ = √⟨v,v⟩ (6.7)**: homogeneity, triangle inequality (6.8); Pythagoras for orthogonal lists (6.12–6.13); parallelogram law (6.18) characterizes inner-product norms.
- **Cauchy-Schwarz (6.14)**: |⟨u,v⟩| ≤ ‖u‖‖v‖, equality ⟺ dependent — the engine behind the triangle inequality.
- **Orthogonal / orthonormal lists (6.10, 6.22)**: orthogonal lists of nonzero vectors are independent; orthonormal lists preserve norms and inner products under coordinate maps (6.24–6.25); Bessel's inequality (6.26).
- **Orthonormal basis (6.27)**: every inner product space has one (6.35) via **Gram-Schmidt (6.32)** — orthogonalize while keeping spans of initial segments identical; every orthonormal list extends to an orthonormal basis (6.36).
- **Schur's theorem (6.38)**: over C, T has an upper-triangular matrix with respect to some orthonormal basis.
- **Riesz representation theorem (6.42)**: every φ ∈ V′ equals ⟨·, u⟩ for a unique u — duality made concrete (revisited at 6.58 via projections).
- **Orthogonal complement U⊥ (6.46)**: dim U + dim U⊥ = dim V (6.51); (U⊥)⊥ = U (6.52); V = U ⊕ U⊥ (6.49).
- **Orthogonal projection P_U (6.55)**: P_U v = the unique point of U nearest v; range P_U = U, null P_U = U⊥; properties (6.57).
- **Minimization (6.61)**: distance to a subspace minimized uniquely at the projection — least squares in embryo.

## Key Concepts
- Conjugate symmetry: ⟨v,w⟩ = overline{⟨w,v⟩}; linearity in the FIRST slot (Axler's convention — watch order when computing).
- Orthogonality to 0: 0 is orthogonal to everything (6.11); "orthogonal" never means the zero vector relation.
- Gram-Schmidt keeps span(v1,…,vk) at every step — the resulting orthonormal basis is triangularly related to the original.
- With an orthonormal basis, ℳ(T) entries are ⟨Te_j, e_k⟩ (6.30) — matrices become measurements.
- Riesz: functionals are "inner product with something"; the representing vector is unique.
- Projection characterization (6.57): P is an orthogonal projection ⟺ P² = P and null P = (range P)⊥.
- Minimization: ‖v − u‖ minimized over u ∈ U exactly at u = P_U v — the geometry behind normal equations.

## Mental Models
- "Inner product = the machine that turns pairs into geometry": norm, angle, distance, orthogonality are all derived; different inner products = different geometries on the same space (integral vs dot).
- "Gram-Schmidt = triangular cleanup": never changes the filtration of spans, only rotates inside each new direction — the flag from Ch5 becomes an orthonormal flag.
- "Riesz = no free functionals": once geometry exists, every linear measurement is a shadow of some vector; the dual V′ from Ch3F becomes V itself (conjugately).
- "Projection = best approximation": every "fit the closest element of a subspace" problem is one projection; the error is orthogonal to the model space (normal equations).
- "V = U ⊕ U⊥": the Ch2 extension theorem (2.33) upgraded to a canonical, orthogonal choice of complement.

## Anti-patterns
- **Slot-order slips with complex inner products**: linear in first slot, conjugate-linear in second (Axler); swapping silently breaks adjoint formulas in Ch7.
- **Assuming every norm comes from an inner product**: check the parallelogram law (6.18) — ‖·‖∞ fails it.
- **Confusing orthogonal list with orthonormal**: independence needs nonzero; coordinates/norm formulas (6.24–6.26) need unit length.
- **Forgetting conjugate symmetry when applying Riesz**: the representing vector sits in the second slot; φ(v) = ⟨v, u⟩.
- **Using projections before proving U is a subspace**: U⊥ and P_U are defined for subspaces; affine sets need the translate trick.

## Reference Tables
### Geometry from the inner product
| Object | Formula |
|---|---|
| norm | ‖v‖ = √⟨v,v⟩ |
| distance | dist(u,v) = ‖u − v‖ |
| orthogonal ⟂ | ⟨u,v⟩ = 0 |
| projection | v = P_U v + (v − P_U v), P_U v ∈ U, v − P_U v ∈ U⊥ |
| Riesz | φ = ⟨·, u⟩ for unique u |

### Dimension facts
| Relation | Value |
|---|---|
| dim U + dim U⊥ | dim V (6.51) |
| (U⊥)⊥ | U (6.52) |
| range P_U / null P_U | U / U⊥ |
| V | U ⊕ U⊥ (6.49) |

### Gram-Schmidt invariants
| Property | Kept? |
|---|---|
| span(e1,…,ek) = span(v1,…,vk) | yes, every step |
| orthonormality | built |
| uniqueness | up to signs/phases (with positive first coefficient: unique) |

## Key Takeaways
An inner product upgrades linear algebra to geometry without coordinates: norms, angles, best approximations.
Orthonormal bases always exist (Gram-Schmidt) and make matrices honest measurements.
Riesz kills the abstract dual: every functional is "inner product with a fixed vector".
Orthogonal projection is the universal solver of subspace-fitting problems, and V = U ⊕ U⊥ is the canonical direct sum.
Schur: with an orthonormal basis, every complex operator is upper triangular — Ch5's flag made geometric.

## Connects To
Ch7 is the payoff: adjoints T* defined by ⟨Tv,w⟩ = ⟨v,T*w⟩ (Riesz-powered), then spectral theorems for self-adjoint/normal operators — diagonalizability replaces Schur's triangular form. Ch7's SVD and Ch6's minimization combine into least squares; Ch9's quadratic forms and Ch8's complex-operator theory both lean on this chapter's geometry. In the control shelf: H2/H∞ norms, balanced truncation, and least-squares identification all live in this chapter's language.
