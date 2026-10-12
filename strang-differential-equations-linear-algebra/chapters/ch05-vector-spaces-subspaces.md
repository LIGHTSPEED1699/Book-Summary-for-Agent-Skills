# Chapter 5: Vector Spaces and Subspaces

## Core Idea
The column picture becomes geometry: the columns of A span a subspace (the column space C(A)), and Ax = b is solvable exactly when b lies in it. The solutions of Ax = 0 form the nullspace N(A), and elimination reveals the master count: rank r pivots, n − r free variables, n − r special solutions spanning the nullspace. The four fundamental subspaces — C(A), N(A), C(Aᵀ), N(Aᵀ) — with dimensions r, n−r, r, m−r, and the dimensions theorem r + (n−r) = n, are the structural heart of linear algebra.

## Frameworks Introduced
- **Vector spaces and subspaces (5.0/5.1)**: closure under addition and scalar multiplication; Rⁿ, planes/lines through the origin as subspaces; column space C(A) = all combinations of the columns.
- **Nullspace (5.2)**: N(A) = solutions of Ax = 0; elimination finds it; special solutions from free variables; rank r = # pivots = # independent columns = # independent rows (the great fact).
- **Complete solution (5.3)**: x = v_p + x_n — one particular solution plus the nullspace; solvability condition on b = the left nullspace membership test (e.g. "b's entries must add to zero" when rows sum to zero).
- **Independence, basis, dimension (5.4)**: independent = no combination gives zero; basis = independent spanning set; dimension = basis length; row rank = column rank = r.
- **Four fundamental subspaces (5.5)**: C(A) (r) and N(A) (n−r) in the domain; C(Aᵀ) (r) and N(Aᵀ) (m−r) in the codomain; dimensions add to n and m; orthogonality of C(A) ⊥ N(Aᵀ) and C(Aᵀ) ⊥ N(A) (fundamental theorem of linear algebra, stated here, used in ch7).
- **Graphs and networks (5.6)**: incidence matrix A of a graph; node equations Av = 0 enforce conservation; nullspace = cycle/loop currents; left nullspace = loops around faces; network interpretation makes the rank count concrete (tree links, loops).

## Key Concepts
- Rank r discovered by elimination: nonzero rows of U, pivots, independent columns — all the same number.
- Special solutions: set one free variable to 1, others to 0, back-substitute; the n − r of them form a basis of N(A).
- Consistency conditions on b come from N(Aᵀ): every combination of A's rows giving zero must give zero on b.
- Complete solution picture repeats y = Yn + Yp from ch1: particular + null.
- Graph Laplacian preview: AᵀA (incidence) gives node equations; currents minimize energy (ch7's least squares connection).
- Subspace membership vs spanning: C(A) is a span; N(A) is a set of solutions — the two ways subspaces appear.

## Mental Models
- "Ax = b is a column-combination question": solvability = b ∈ C(A); uniqueness = N(A) trivial.
- "Pivots count, free variables parametrize": r and n−r are the only two numbers that matter for a linear system.
- "Complete solution = point + subspace": affine geometry everywhere (repeats for ODEs: Yp + Yn).
- "The four subspaces are orthogonal pairs": the fundamental theorem as a picture — domain splits N(A) ⊕ C(Aᵀ), codomain splits N(Aᵀ) ⊕ C(A).
- "Networks visualize the theorem": incidence matrices make rank, loops, and conservation numbers visible.

## Anti-patterns
- **Confusing the nullspace of A with solutions of Ax = b** — the complete solution is affine, not a subspace (unless b = 0).
- **Counting dimension by equation count** — the true equation count is the rank, not m.
- **Ignoring consistency conditions** — b must be orthogonal to every left-null relation.
- **Assuming row and column independence are different numbers** — they're equal (r), and that equality is the theorem, not a definition.

## Reference Tables
### Four fundamental subspaces of m×n A (rank r)
| Subspace | Lives in | Dimension | Basis from |
|---|---|---|---|
| C(A) | Rᵐ | r | pivot columns |
| N(A) | Rⁿ | n − r | special solutions |
| C(Aᵀ) | Rⁿ | r | pivot rows |
| N(Aᵀ) | Rᵐ | m − r | elimination combinations killing rows |

### Complete solution recipe
| Step | Object |
|---|---|
| 1 | Check b ∈ C(A) (consistency vs N(Aᵀ)) |
| 2 | Find one v_p (back substitution, free vars 0) |
| 3 | Find n−r special solutions of Av = 0 |
| 4 | x = v_p + combination of specials |

## Key Takeaways
Rank r from elimination counts independent rows and columns alike; n − r free variables give the nullspace basis.
Solvability is membership in C(A); the complete solution is particular + nullspace.
The four fundamental subspaces and their orthogonality are the fundamental theorem of linear algebra.
Networks give the theorem a physical body (conservation laws = nullspace equations).

## Connects To
Ch1's Yn + Yp and ch2's null/particular split are the ODE shadow of 5.3. Ch6's eigenvalues decompose the domain further; ch7's least squares projects onto C(A) with normal equations AᵀA (and the graph Laplacian returns as AᵀA). Axler ch2-3 (dimension formula, rank-nullity) is the pure proof of the r + (n−r) = n bookkeeping; Hubbard ch2's kernel/image/dimension formula is the applied twin.
