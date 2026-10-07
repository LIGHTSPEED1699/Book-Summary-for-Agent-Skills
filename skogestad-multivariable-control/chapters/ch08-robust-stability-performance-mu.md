# Chapter 8: Robust Stability and Performance Analysis (μ framework)

## Core Idea
Everything — RS, RP, any weighted H∞ objective — reduces to one object: the structured singular value μ_Δ(M(jω)). Unstructured uncertainty gives the small-gain test ‖M‖∞ < 1; real channel-wise (diagonal) uncertainty is measured exactly by μ, which is why NP+RS can pass while RP fails on large-RGA plants; and μ-synthesis (D-K iteration) designs controllers that minimize it.

## Frameworks Introduced
- **N-Δ / M-Δ standard form**: pull out all uncertainties from the generalized plant P → N with partition [N₁₁ N₁₂; N₂₁ N₂₂]; RS ⇔ stability of MΔ loop with M = N₁₁ (given NS: N stable).
- **Exact RS tests (Theorems 8.1-8.2)**:
  - General convex perturbation set: RS ⇔ det(I − MΔ(s)) never encircles/touches 0 ⇔ det(I − MΔ) ≠ 0 ∀s∈D, ∀Δ.
  - Complex Δ: RS ⇔ max_Δ ρ(MΔ) < 1 ∀ω (phase of eigenvalue always adjustable with complex scalar).
  - Full complex Δ: RS ⇔ ‖M‖∞ = max_ω σ̄(M) < 1 (small gain, exact).
- **μ definition (Definition 8.5)**: μ_Δ(M) = 1̄ / min{σ̄(Δ̃) : Δ̃ ∈ Δ, det(I − MΔ̃) = 0}; μ(M) = 0 if no Δ makes I−MΔ singular. RS ⇔ max_ω μ_Δ(M(jω)) < 1 (Theorem 8.6).
- **μ properties that make it usable**:
  - Full block: μ = σ̄. Scalar repeated block: μ = ρ.
  - Unitary invariance: μ(M) = μ(UMUᴴ) for block-diagonal unitary U ⇒ lower bound μ = max_U ρ(MU) (always exact as a max over unitaries).
  - D-scaling upper bound: μ_Δ(M) ≤ min_{D∈D} sup_ω σ̄(D M D⁻¹) where D = block-diagonal positive scalars matching Δ structure; exact for ≤ 2 blocks (and some 3-block cases), gap ≤ 3−√5 ≈ 0.764 for 3 full blocks; gap can grow with more blocks.
  - Structure matters enormously: M = [[0,a],[b,0]] → μ(full) = √(|a|²+|b|²)·√2-ish = σ̄, μ(diag Δ) = |a|+|b|, μ(Δ = δI) = ρ = |a+b|... and a diagonal Δ may make μ = 0 where full-block μ = 2.
  - Real vs complex Δ: μ differs (real gain uncertainty is less dangerous than complex).
- **Skewed μ (μ_s)**: keep all but one uncertainty block at nominal, ask how large one block can grow before instability ⇒ 1/μ_s; also computes worst-case performance levels (e.g. worst-case σ̄(S₀) with fixed uncertainty = skewed-μ of the augmented N).
- **RP as structured RS (Theorem 8.8)**: RP (‖F_u(N,Δ)‖∞ < 1 ∀Δ) ⇔ μ_Δ̃(N) < 1 ∀ω with Δ̃ = diag(Δ, Δ_P), Δ_P a FULL complex block of the same size as Fᵀ. RP ⇒ RS and NP automatically (μ_Δ(N₁₁) ≤ μ_Δ̃(N), σ̄(N₂₂) ≤ μ_Δ̃(N)) — but NOT nominal stability: always check NS separately ("common mistake: great RP, unstable design").
- **μ-synthesis / D-K iteration (8.12)**: min_K max_ω μ_Δ(N(P,K)) via alternating: (1) fix D(ω) scalings from μ analysis, solve H∞ problem min_K ‖D N(P,K) D⁻¹‖∞; (2) update D from the resulting loop; iterate. Converges to local minima; each step is a standard H∞ solve (state-space formulas).
- **Loop-shaping bound transfer (Skogestad-Morari, 8.9.1 #12-13)**: given μ_Δ(M) < 1, sufficient bounds on any R (S, T, L, K) follow by solving μ_{diag(Δ,R̃)}(N₁₁ + N₁₂R(I−N₂₂R)⁻¹N₂1) = 1 — the machinery that turns μ conditions into σ̄(T) < 1/|w_I|-style loop-shaping rules.

## Key Concepts
- **Structured singular value μ**: worst-case inverse perturbation size that breaks det(I−MΔ) = 0 at some frequency; the exact RS test for structured Δ.
- **D-scalings**: frequency-independent block-diagonal similarity transforms shrinking σ̄(DMD⁻¹); the computational handle on μ's upper bound; also the bridge to H∞ synthesis.
- **Δ_P fictitious performance block**: the trick that makes RP an RS problem — performance spec = "a full uncertainty block fits in the loop".
- **μ gap**: upper−lower bound separation; small in practice for few blocks; motivates checking both.
- **Input uncertainty is diagonal**: E_I = diag(ε_i) with |ε_i| ≤ r always present; μ with diagonal blocks is typically much smaller than σ̄ — but for ill-conditioned plants (large RGA) μ still exceeds 1 at moderate r, formalizing Ch 6's RGA warnings.
- **RP with input uncertainty needs σ̲(S) large at low ω**: performance under simultaneous channel gain errors requires sensitivity small in ALL directions — RGA-large plants can't deliver it (μ > 1 at low ω with r ~ 1/λ).

## Mental Models
- "μ < 1 everywhere + NS checked = done" — one number per frequency answers RS or RP exactly for the structure you declare.
- "Declare the structure honestly": diagonal for channel gains, full for unmodeled dynamics, repeated real blocks for real parameters — μ's value (and your conservatism) depends entirely on it.
- "σ̄ is the lazy bound, μ is the honest one": ‖wT‖∞ < 1 suffices but can be very conservative for diagonal uncertainty; μ recovers the difference (satellite example: per-channel margins ∞, μ says fragile).
- "D-K iteration = H∞ design with a moving ruler": each iteration reshapes the weight scalings toward the true worst-case direction.

## Anti-patterns
- **Forgetting the NS check with μ** (RP condition doesn't imply it — the book flags this as the classic μ-toolbox trap).
- **Using σ̄ (unstructured) conditions as if necessary** for diagonal uncertainty — kills achievable performance on well-behaved MIMO plants.
- **Trusting a single μ upper bound** when the D-scaling gap is large; compute lower bound too.
- **Real Δ modeled as complex** without acknowledging conservatism (or using real-μ tools when available).

## Reference Tables

### Which test for which problem
| Problem | Test | Exactness |
|---|---|---|
| RS, full complex Δ | ‖N₁₁‖∞ < 1 | exact |
| RS, structured Δ | max_ω μ_Δ(N₁₁) < 1 | exact |
| NP | σ̄(N₂₂) < 1 | exact |
| RP | max_ω μ_{diag(Δ,Δ_P)}(N) < 1, Δ_P full | exact (given NS) |
| RS sufficient w/o structure | ‖w_I T_I‖∞ < 1 etc. | conservative for diagonal Δ |

### μ quick values (constant M)
| Structure of Δ | μ |
|---|---|
| full complex | σ̄(M) |
| Δ = δ I (repeated scalar) | ρ(M) |
| diagonal, M = [0 a; b 0] | \|a\| + \|b\| |
| diagonal, M = [a 0; 0 b]-type couplings | can be 0 (det = 1) |

## Key Takeaways
1. Put the problem in N-Δ form once; then RS = μ(N₁₁) < 1, RP = μ(N with Δ_P block) < 1, NP = σ̄(N₂₂) < 1 — and NS separately.
2. μ captures exactly what σ̄ misses: simultaneous structured (channel-wise) perturbations — the satellite and distillation failures.
3. Compute μ by D-scaling upper bound + unitary lower bound; watch the gap.
4. Skewed μ answers "how much can THIS uncertainty grow" — great for what-if engineering questions.
5. Design by D-K iteration when μ analysis says the H∞ design isn't exploiting structure.
6. The RGA/σ̲ heuristics of Ch 6 are μ's low-frequency shadows: large RGA ⇒ μ > 1 for RP at realistic input uncertainty levels.

## Connects To
- **Ch 6**: RGA fragility predictions made exact by μ.
- **Ch 7**: SISO |w_P S| + |w_O T| < 1 is the SISO RP = μ condition.
- **Ch 9**: H∞ and loop-shaping synthesis are the inner loop of D-K iteration.
- **Ch 3**: satellite/distillation motivating examples resolved.
- **Appendix A**: determinant/Schur identities used throughout.
