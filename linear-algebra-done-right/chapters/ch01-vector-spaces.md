# Chapter 1: Vector Spaces

## Core Idea
A vector space is an abstract set with addition and scalar multiplication satisfying eight axioms — nothing more. Everything in the book is built on this minimal algebraic structure, deliberately without coordinates, metrics, or determinants. The chapter's move: generalize from R^n/C^n to arbitrary spaces (function spaces, sequence spaces), then define the lattice of subspaces and the sum/direct-sum machinery that later becomes the book's main decomposition tool.

## Frameworks Introduced
- **F = R or C convention**: every definition/theorem stated over F proves both real and complex versions at once. Scalars are elements of F; vectors are elements of V.
- **Axiom list (1.20)**: commutativity, associativity (vector + and scalar ·), additive identity, additive inverse, multiplicative identity 1v = v, two distributive laws. That's the whole ontology.
- **Subspace test (1.34)**: a subset U is a subspace iff 0 ∈ U, closed under addition, closed under scalar multiplication. Everything else (associativity etc.) is inherited for free from V.
- **Sum vs union**: union of subspaces is almost never a subspace; the right analogue of union is the sum V1 + … + Vm, which is the smallest subspace containing all summands (1.40).
- **Direct sum (1.41)**: sum where every element has a *unique* decomposition. Test: 0 has unique decomposition (1.45); for two subspaces, U + W direct ⟺ U ∩ W = {0} (1.46).

## Key Concepts
- Complex numbers as ordered pairs with i² = −1; arithmetic rederived, not memorized (1.1–1.5).
- Lists vs sets: order matters, repetition matters, length finite (1.8). F^n = length-n lists over F (1.11).
- F^∞ (sequences), F^S (all functions S → F) are vector spaces — F^n is the special case S = {1,…,n} (1.23–1.25). Vectors can be functions; coordinates are optional.
- Unique additive identity (1.26), unique additive inverse (1.27), 0v = 0 (1.30), a0 = 0 (1.31), (−1)v = −v (1.32).
- Subspace examples keyed on "the condition must be homogeneous": {(x,b,c…): b = 0} subspace iff constraint = 0; f′(2) = b subspace iff b = 0; ∫f = b subspace iff b = 0.
- Subspaces of R²: {0}, lines through origin, R²; R³ adds planes through origin (1.35 discussion).
- Direct-sum nonexample (1.44): pairwise intersections {0} is NOT enough for m > 2 — must check 0's decomposition uniqueness across all m at once.
- Complexification V_C = V × V with (u1,v1) + (u2,v2) = (u1+u2, v1+v2), (a+bi)(u,v) = (au−bv, av+bu) (Exercise 1C ch1 §1B ex 8) — real space gains a complex twin.
- Even/odd functions: R^R = V_e ⊕ V_o (Exercise 1C.24) — the archetypal direct sum of function spaces.

## Mental Models
- "Algebra travels": what you can do in R² by arrows, you do in R^5000 by axioms — pictures are scaffolding, not mathematics.
- "Homogeneity is the subspace filter": any constraint of the form L(v) = 0 for a linear condition L gives a subspace; = nonzero constant breaks it.
- "Direct sum = unique coordinates relative to blocks": V = U ⊕ W means every v splits one way only; ⊕ is the vector-space disjoint union (subspaces can never be disjoint — both contain 0 — so intersection {0} replaces disjointness).
- "Prove from axioms only": 1.30 (0v = 0) must use distributivity because it's the only axiom connecting scalars and vectors — a template for the whole book's style.

## Anti-patterns
- **Testing pairwise intersections for m-subspace direct sums** (1.44): V1∩V2 = V1∩V3 = V2∩V3 = {0} does not make the sum direct.
- **Treating union of subspaces as a subspace**: only when one contains the other (Exercise 1C.12).
- **Identifying R² inside C² as a subspace**: R² is not even a subset closed under C-scalar multiplication (i·(1,0) = (i,0) ∉ R²) — subspace depends on the field (Exercise 1C.5).
- **Memorizing the complex product formula**: rederive from i² = −1 + distributivity.
- **Assuming {a³ = b³} behaves the same over R and C**: over R it's a subspace, over C it isn't (Exercise 1C.6) — the field changes geometry.

## Reference Tables
### Vector space axioms (1.20)
| Axiom | Statement |
|---|---|
| commutativity | u + v = v + u |
| associativity | (u+v)+w = u+(v+w); (ab)v = a(bv) |
| additive identity | ∃0: v + 0 = v |
| additive inverse | ∀v ∃w: v + w = 0 |
| multiplicative identity | 1v = v |
| distributive | a(u+v) = au+av; (a+b)v = av+bv |

### Subspace test
| Check | Why enough |
|---|---|
| 0 ∈ U | (or just U nonempty) |
| u,w ∈ U ⟹ u+w ∈ U | addition restricts |
| λ ∈ F, u ∈ U ⟹ λu ∈ U | scalar mult restricts |
| rest | inherited from V |

### Sum vs direct sum
| Notion | Definition | Test |
|---|---|---|
| U + W | all u+w | always a subspace; smallest containing both |
| U ⊕ W | sum with unique decomposition | U ∩ W = {0} (two summands only) |
| m-fold ⊕ | unique v1+…+vm | 0 uniquely 0+…+0 (pairwise ∩ insufficient) |

## Key Takeaways
Vector space = set + two operations + eight axioms; nothing geometric is assumed.
Subspaces are the subsets that matter; sums are the union substitute; direct sums are the ones with unique block coordinates.
Function spaces (F^S) are the general case — F^n is just S finite.
Homogeneous linear conditions carve subspaces; inhomogeneous ones don't.
The field F is part of the data: the same set can be a subspace over R and not over C.

## Connects To
Ch2 adds span/independence/dimension — the finiteness machinery that classifies subspaces of R²/R³ completely. Ch3's null space and range are subspaces, and direct sums become the language of the rank-nullity decomposition. Direct-sum thinking recurs in Ch5 (generalized eigenspaces), Ch7 (orthogonal complements V = U ⊕ U⊥), and Ch9 (tensor products as the "right" product).
