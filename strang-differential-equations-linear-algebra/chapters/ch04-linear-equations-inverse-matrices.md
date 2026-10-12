# Chapter 4: Linear Equations and Inverse Matrices

## Core Idea
Ax = b from two pictures — rows (equations as lines/planes meeting at x) and columns (b as a combination of A's columns) — and one algorithm: elimination, which factors A = LU and exposes when solutions exist. Inverse matrices answer "for every b, exactly one x"; symmetric (Sᵀ = S) and orthogonal (Qᵀ = Q⁻¹, length-preserving) matrices are the two special classes that recur everywhere later.

## Frameworks Introduced
- **Two pictures (4.1)**: row picture (n hyperplanes intersecting) vs column picture (b in the column space); singular = columns fail to span / determinant zero / lines parallel; three solution cases (unique, none, infinitely many).
- **Elimination (4.2)**: multiply an equation, subtract — forward elimination to upper triangular U, back substitution; multipliers become the entries of L (A = LU); pivots must be nonzero; row exchanges when they aren't (preview of PA = LU); singular detection (no second pivot ⇒ dependent rows).
- **Matrix multiplication (4.3)**: (AB)_{ij} = row i of A · column j of B; AB = A's columns combined by B's columns = columns of A times rows of B summed; A(BC) = (AB)C; AB ≠ BA; rank-revealing: if A is m×r and B is r×n then AB has rank ≤ r (the factorization view).
- **Inverses (4.4)**: A⁻¹ exists ⟺ Ax = 0 has only x = 0 ⟺ n independent columns/pivots; (AB)⁻¹ = B⁻¹A⁻¹ (reverse order); (Aᵀ)⁻¹ = (A⁻¹)ᵀ; Gauss-Jordan on [A I] → [I A⁻¹]; permutation matrices P (Pᵀ = P⁻¹).
- **Symmetric and orthogonal (4.5)**: transpose rules (AB)ᵀ = BᵀAᵀ; symmetric Sᵀ = S; AᵀA always symmetric; orthogonal Q: columns orthonormal, QᵀQ = I, ‖Qx‖ = ‖x‖ (rotations/reflections); second-difference matrix K as the recurring symmetric example.

## Key Concepts
- Column picture is the one that generalizes to vector spaces and Ax = b solvability (ch5).
- Elimination is basis-free Gaussian logic: same operations on equations, recorded as L.
- Singularity trinity: det = 0 ⟺ columns dependent ⟺ Ax = 0 has nonzero solutions ⟺ A⁻¹ doesn't exist.
- Matrix products as combinations of columns — the mental shortcut that makes (AB)C = A(BC) and rank inequalities obvious.
- Orthogonal matrices preserve lengths and angles — the structure behind change of orthonormal basis (ch6 diagonalization).
- 2×2 inverse formula and elimination as the computational core; Gauss-Jordan for explicit inverses.

## Mental Models
- "Rows ask, columns build": row picture = constraints; column picture = spanning question. Solvability is a column-space membership test.
- "Elimination writes the proof as a factorization": A = LU records every step; pivots are the witnesses of independence.
- "Inverses reverse order": socks-shoes (AB)⁻¹ = B⁻¹A⁻¹.
- "Symmetric = self-adjoint, orthogonal = length-keeper": the two matrix personalities that eigenvalue theory (ch6) rewards.

## Anti-patterns
- **Computing A⁻¹b to solve Ax = b** when elimination alone does it cheaper and more stably.
- **Assuming AB = BA** or (A+B)² = A² + 2AB + B² without commutativity.
- **Dividing by a zero pivot without row exchange** — elimination's only failure mode.
- **Treating singular and "nearly singular" as the same** — near-singularity means sensitive solutions (conditioning, previewed by the parallel-lines picture).

## Reference Tables
### Solution cases for Ax = b (square A)
| Picture | Unique | None | ∞ many |
|---|---|---|---|
| Rows | lines meet at one point | parallel | coincident |
| Columns | b unique combination | b outside span | b in span, dependent columns |
| Algebra | A⁻¹ exists | inconsistent | nullspace nontrivial |

### Special matrix classes
| Class | Definition | Property |
|---|---|---|
| Symmetric S | Sᵀ = S | AᵀA is symmetric; real eigenvalues (ch6) |
| Orthogonal Q | QᵀQ = I | ‖Qx‖ = ‖x‖; Qᵀ = Q⁻¹ |
| Permutation P | I with reordered rows | Pᵀ = P⁻¹; row exchange |
| Triangular L, U | elimination factors | A = LU (with PA = LU) |

## Key Takeaways
Two pictures, one algorithm: elimination decides existence and count of solutions; A = LU is its record.
Invertibility = independent columns = nonzero determinant = trivial nullspace — one condition, four faces.
Matrix multiplication is best read columnwise; inverses reverse order.
Symmetric and orthogonal matrices are the classes eigenvalue theory will crown.

## Connects To
Ch5 turns the column picture into column space/nullspace and the four fundamental subspaces; ch6 diagonalizes symmetric matrices with orthogonal Q; ch7's least squares is AᵀA from 4.5 in action. The shelf: LU/elimination underlies every numerical solve; orthogonal transformations are the backbone of SVD, QR, and balanced realizations in Skogestad/Stengel.
