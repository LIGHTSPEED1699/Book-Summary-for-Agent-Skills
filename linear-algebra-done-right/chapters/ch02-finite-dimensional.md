# Chapter 2: Finite-Dimensional Vector Spaces

## Core Idea
Finiteness enters through one question: how long must a list be to span V, and how short to stay independent? The answer — all bases have the same length — defines dimension. The linear dependence lemma (delete one vector from a dependent list, span unchanged) is the workhorse that makes every exchange/extension argument one line.

## Frameworks Introduced
- **span(v1,…,vm)** = all linear combinations = smallest subspace containing the list (2.4, 2.6); span of empty list = {0}.
- **Linear independence**: the only way to write 0 as a combination is all coefficients 0; equivalently every vector in the span has a UNIQUE representation (2.16).
- **Linear Dependence Lemma (2.18)**: if v1,…,vm is dependent and v1 ≠ 0, then some vk is in the span of its predecessors; deleting vk leaves the span unchanged. The book's most-used tool.
- **Basis (2.26)**: spanning + independent. Criterion (2.28): basis ⟺ every vector has unique representation as a combination.
- **Exchange machinery**: every spanning list contains a basis (2.30); every independent list extends to a basis (2.32); a basis of a subspace U ⊂ V extends to a basis of V (2.33, giving V = U ⊕ W for some W).
- **Dimension (2.35)**: length of any basis (well-defined by 2.34); finite-dimensional = has a finite spanning list.
- **Dimension of a sum (2.43)**: dim(U+W) = dim U + dim W − dim(U∩W).

## Key Concepts
- P(F) = polynomials over F is infinite-dimensional (2.10, 2.14) — the standing counterexample to "everything is F^n".
- Length intuition: no independent list in R^3 has length > 3; no spanning list in R^4 has length < 4 (2.23–2.24) — the exchange principle in action.
- Subspaces of R^3 fully classified by dimension: 0, lines, planes, R^3 (via 2.37 + extension).
- dim U ≤ dim V for U ⊂ V, with equality forcing U = V (2.37, 2.39) — dimension is a sharp detector.
- Direct sums and dimension: V = U ⊕ W ⟹ dim V = dim U + dim W.
- Basis of F^2 with exotic vectors (2.40) — bases are not "the coordinate vectors".

## Mental Models
- "Unique representation = independence": independence is not an abstract no-condition, it's uniqueness of coordinates; a basis is a coordinate system.
- "Delete-and-keep-span": dependence always shows up as one vector redundant to earlier ones — scan left to right, delete the offender, span survives.
- "Extend or shrink": any independent list extends to a basis, any spanning list shrinks to a basis — bases are reachable from any direction.
- "Dimension counts basis slots": dim is the number of free coordinates; a subspace that fills the count IS the space.
- "Inclusion-exclusion for subspaces": dim(U+W) = dim U + dim W − dim(U∩W) mirrors |A∪B| = |A|+|B|−|A∩B|, with sum replacing union.

## Anti-patterns
- **Confusing "spans" with "is a basis"**: spanning lists may be dependent; independence may underspan. Check both (2.28's uniqueness test checks both at once).
- **Assuming infinite-dimensional intuition**: P(F) has independent lists of every length but no finite basis — dimension arguments silently assume finiteness.
- **Using span of a dependent list to count coordinates**: redundant vectors inflate the list length; only independent spanning lists count dimension.
- **Forgetting the intersection term** in dim(U+W) — the naive sum double-counts U∩W.

## Reference Tables
### List-length trichotomy (finite-dim V, dim V = n)
| List property | Max/min length | Consequence |
|---|---|---|
| independent | ≤ n | extends to a basis |
| spanning | ≥ n | contains a basis |
| independent + length n | = n | is a basis (2.38) |
| spanning + length n | = n | is a basis (2.38) |

### Dimension formulas
| Object | Formula |
|---|---|
| subspace U ⊂ V | dim U ≤ dim V; equality ⟹ U = V |
| sum | dim(U+W) = dim U + dim W − dim(U∩W) |
| direct sum | dim(U⊕W) = dim U + dim W |
| F^n / R^m×n as functions | n / mn |
| P_m(F) (deg ≤ m) | m+1 |

## Key Takeaways
Dimension is well-defined because spanning lists always outlast independent ones (exchange argument via the linear dependence lemma).
Every subspace sits in a direct-sum decomposition of V — the extension theorem (2.33) is the seed of every decomposition theorem later.
"Right length + one property = basis" (2.38) is the fastest basis test in the book.
dim(U∩W) = dim U + dim W − dim(U+W) turns geometric intersection questions into arithmetic.

## Connects To
Ch3 applies span/independence to linear maps: null space and range get dimensions, and rank-nullity (dim null T + dim range T = dim V) is the dimension formula for a map. Ch5 uses basis extension to build upper-triangular matrices. Ch6's orthonormal bases replace "some basis" with "nice basis", and dim V = dim U + dim U⊥ is the orthogonal version of 2.43.
