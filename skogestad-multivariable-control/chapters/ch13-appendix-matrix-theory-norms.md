# Appendix A: Matrix Theory and Norms (Mathematical Toolkit)

## Core Idea
The book's entire argument lives on linear algebra: SVD gives directions and gains, the RGA is a Schur product identity, norms come in matched signal/system pairs, and every interconnection (uncertainty, performance, LFT) is a sensitivity factorization away from a small-gain test.

## Frameworks Introduced
- **A.1 Basics**: complex arithmetic, transpose/conjugate transpose, trace, determinant, minors, **Schur's formula**: det M = det(M₁₁)·det(M₂₂ − M₂₁M₁₁⁻¹) (and the block-inverse formulas) — the workhorse behind pole polynomial (Thm 4.8), decentralized factorizations, and coprime results.
- **A.2 Eigenvalues/eigenvectors**: diagonalization/Jordan form; modal response e^{λt}; eigenvalue continuity; **Gershgorin discs** (used for decentralized stability bounds in Ch 10); Perron root ρ(|E|) of nonnegative matrices.
- **A.3 SVD**: G = UΣVᴴ; rank = number of nonzero σ; σ̄ = max gain, σ̲ = min gain; SVD of inverse (σ_i(G⁻¹) = 1/σ_{n−i+1}); economy-size SVD for rank-r; **condition number κ(G) = σ̄/σ̲** (κ = ∞ if singular); κ(G) ≥ 1, κ = 1 ⇔ all-pass/orthogonal columns; unitarily invariant.
- **A.4 RGA**: Λ(G) = (G⁻¹)ᵀ ⊙ G; full property list (scale invariance, row/col sums 1, Λ(G⁻¹) = Λ(G), Λ(Gᵀ) = Λ(G)ᵀ, Λ diagonal/triangular ⇒ I, 2×2 single-parameter); **non-square RGA** via right inverse (Λ = G ⊙ (G⁻¹_R)ᵀ, G⁻¹_R = Gᴴ(GGᴴ)⁻¹); MATLAB rga command.
- **A.5 Norms**:
  - Vector p-norms; induced matrix norm ‖A‖_p = max ‖Ax‖/‖x‖; **σ̄ = induced 2-norm**; ‖A‖₁ = max column sum, ‖A‖∞ = max row sum; Frobenius ‖A‖_F = √tr(AᴴA) = (Σσ_i²)^½; spectral radius ρ(A) = max|λ_i|; relationships: ρ(A) ≤ σ̄(A) ≤ ‖A‖_F; ρ(A) = lim ‖A^k‖^1/k; ρ(A) ≤ ‖A‖ for any induced norm; for normal A, ρ = σ̄.
  - Signal norms: ‖x‖₂ (energy), ‖x‖∞ (peak); **system norm = induced signal norm**: H∞ = induced 2→2 (peak gain, worst-case sinusoid), H2 relates to energy of impulse response (Parseval); Table A.1/A.2 map input class → output bound → norm (the Ch 4 norm interpretations).
- **A.6 Sensitivity factorization**: comparing two feedback systems G vs G₀: S₀ = S(I + (G₀−G)G₀⁻¹... ) — output-perturbation form S₀ = S(I + ΔG G)⁻¹... and input-perturbation form with T_I; the general template S₀ = S(I + E T̃)⁻¹ used in Ch 10 decentralized analysis and Ch 8 uncertainty interconnections; stability transfer conditions via det(I + E T̃) ≠ 0 encirclements.
- **A.7 LFTs**: upper F_u(M,Δ) = M₂₂ + M₂₁Δ(I − M₁₁Δ)⁻¹M₁₂ and lower F_l(M,Δ) = M₁₁ + M₁₂Δ(I − M₂₂Δ)⁻¹M₂₁; interconnection of LFTs = LFT of interconnection; F_l/F_u duality via permutation; inverse LFT; **star product** M ★ Δ generalizing to partitioned matrices — the formal language of the N-Δ structure in Ch 8.

## Key Concepts
- **Schur complement** M₂₂ − M₂₁M₁₁⁻¹: determinant factorization, matrix inverse blocks, and the pole polynomial theorem all rest on it.
- **Singular values vs eigenvalues**: σ̄ is the gain you can excite (direction-optimized); ρ is modal growth; ρ ≤ σ̄ with equality only for normal matrices — the reason "spectral radius conditions" need complex free phases (Thm 8.2).
- **Unitarily invariant norms**: σ̄, ‖·‖_F, H2, H∞ — why SVD-aligned arguments are clean.
- **Perron root** ρ(|E|): bounds μ(E) for diagonal structures (Ch 10 diagonal dominance).
- **Gershgorin**: eigenvalues in discs centered at diagonal entries with off-diagonal radii — per-loop decentralized stability margins.
- **Induced-norm duality**: H∞ system norm = worst-case signal amplification — the bridge that turns "spec" into "norm < 1".

## Mental Models
- "When stuck on a block matrix, Schur it" — one identity powers poles, decentralized loops, and LFT algebra.
- "σ̄ is the honest gain, ρ is the modal truth; small-gain tests use σ̄, exact complex-Δ tests use ρ" (Ch 8's two theorems).
- "Every robustness question is S₀ = S(I + E T̃)⁻¹ + a determinant check" — learn the factorization once, reuse everywhere.
- "κ ≫ 1 means direction matters more than magnitude" — the algebraic root of the book's directionality theme.

## Anti-patterns
- **Confusing ρ(A) with σ̄(A)** for non-normal A — can differ by orders of magnitude (the satellite's γ(G) = 500 vs ρ story).
- **Using Frobenius where induced norm is required** (or vice versa) in uncertainty bounds — the small-gain theorem needs induced norms.
- **Dropping conjugate transposes in complex MIMO algebra** (H vs T) — direction computations silently wrong.

## Reference Tables

### Norm cheat sheet
| Object | Norm | Formula | Meaning |
|---|---|---|---|
| Matrix | σ̄ (induced 2) | √λ_max(AᴴA) | worst gain |
| Matrix | ‖·‖₁ / ‖·‖∞ | max col / row sum | Gershgorin-style bounds |
| Matrix | ‖·‖_F | (Σσ_i²)^½ | total energy |
| Matrix | ρ | max\|λ\| | modal growth |
| Signal | L2 / L∞ | energy / peak | input classes |
| System | H∞ | sup_ω σ̄(G) | induced L2 gain |
| System | H2 | (Σσ_i² of Gramian)^½ | impulse energy / rms to white noise |
| System | Hankel | √ρ(PQ) | past→future energy |

### LFT identities used in the book
| Identity | Use |
|---|---|
| F_u(M,Δ) well-posed ⇔ det(I−M₁₁Δ) ≠ 0 | RS tests |
| F_l(M,Δ) = F_u(P,Δ) with block permutation | N-Δ ↔ general P |
| F_u(M,Δ)⁻¹ = F_u(M⁻¹-permutation, Δ⁻¹) | inverse-based controller analysis |
| star product associativity | pulling out blocks in Ch 8 |

## Key Takeaways
1. Schur's formula is the single most-used identity in the book — memorize it.
2. SVD is the coordinate system of the whole text: gains, directions, conditioning, balancing, Hankel.
3. Norms must match the question: induced norms for worst-case signal amplification, Frobenius/H2 for energy, ρ for modal structure.
4. The sensitivity factorization + determinant/encirclement test is the universal robustness engine.
5. LFT algebra (F_u/F_l/star product) is just bookkeeping for "pull out this block and look at the loop".

## Connects To
- **Ch 4**: pole polynomial via minors (Schur), Gramians, norms.
- **Ch 6/10**: RGA properties (A.4), sensitivity factorization (A.6), Gershgorin/Perron (A.2).
- **Ch 8**: LFTs (A.7) = the N-Δ formalism.
- **Ch 11**: Gramians/SVD for balanced realizations.
