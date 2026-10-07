# Chapter 9: Control System Design (LQG, H2, H∞, Loop-Shaping)

## Core Idea
Practical MIMO design = shaping singular values of closed-loop transfer functions (S, T, KS) through frequency; the synthesis engines are LQG/H2 (optimal but fragile), H∞ (worst-case but shaped), and the McFarlane-Glover H∞ loop-shaping procedure which marries classical loop shape intuition to a guaranteed coprime-uncertainty margin.

## Frameworks Introduced
- **The 6 closed-loop objectives** (one-DOF config, y = Td + ... ): (1) disturbance rejection: σ̄(S) small; (2) noise attenuation: σ̄(T) small; (3) tracking: σ̲(T) ≈ 1; (4) control energy: σ̄(KS) small; (5) RS additive: σ̄(KS) small; (6) RS multiplicative output: σ̄(T) small. Trade-off is over frequency; open-loop shadows: σ̄(S) ≈ 1/σ̲(L) at low ω, σ̄(T) ≈ σ̄(L) at high ω; bandwidth where σ(L) ∈ [0.41, 2.41].
- **LQG**: LQR gain K_r from ARE AᵀX + XA − XBBᵀX + C₁ᵀC₁ = 0 (u = −K_r x, K_r = BᵀX); Kalman filter K_f = YC₂ᵀ from dual ARE; separation theorem (controller = filter + gain, same closed-loop poles as full-state); certainty equivalence. **Fragility**: LQG loop recovery only asymptotic — LTR via ε → 0 (input noise scaling) or θ → ∞ (output noise scaling) recovers LTR target L = G K_r, but robustness margins only in the limit; classic counterexamples (Gladstone) show LQG can have arbitrarily bad margins for finite settings.
- **H2 (LQG with matching conditions)**: D₁₂ = 0, D₂₁ᵀC₁ = 0, D₂₁D₁₂ = 0, D₂₁D₂₁ᵀ = I, D₁₂ᵀD₁₂ = I → LQG solution is the H2-optimal controller; ‖N‖₂² = optimal cost; state-space formulas via two Riccati equations.
- **Coprime-factor robust stabilization (the gem of the chapter)**: normalize left coprime G = M⁻¹N with MᵀM + NᵀN = I; uncertainty G_p = (M + Δ_M)⁻¹(N + Δ_N); RS for all ‖[Δ_N Δ_M]‖∞ < α ⇔ K stabilizes; optimal α_max = 1/γ_opt where **γ_opt = √(1 + ρ(XZ))** with X, Z the two H∞ Riccati solutions of the shaped plant; b = (I + G*G)^{-1/2}, a = (I + GG*)^{-1/2} are the optimal stability-radius weights; the optimal controller comes from two Riccati solves + one γ-iteration (or none for the coprime formula — explicit via aresolv, no γ-iteration needed).
- **H∞ loop-shaping design procedure (McFarlane-Glover 1990)**:
  1. Shape: pick W1 (pre), W2 (post) so σ̄(G_s) of G_s = W1 G W2 has desired classical shape (integrators, slope −1 at target crossover, roll-off).
  2. Robustly stabilize G_s with normalized left coprime H∞ formula → K_s maximizing α(G_s).
  3. K = W1 K_s W2.
  Performance lives in the shaping; robustness guarantee (α) is computed for the shaped plant — check α is not destroyed by shaping (α close to unshaped value = good).
- **2-DOF / mixed-sensitivity synthesis**: generalized plant with w_P S, w_u KS (and w_T T) stacks; γ-iteration H∞ (hinfsyn); steady-state model matching via constant W_i scaling: T_ref(0) matched exactly by pre-scaling r.

## Key Concepts
- **Loop transfer recovery (LTR)**: LQG loop shape at the input break approaches G K_r as ε → 0; recovery imperfect with nonminimum-phase plants.
- **Stability radius**: largest simultaneous normalized coprime perturbation (M,N) the loop tolerates — the H∞ coprime problem's γ_opt; independent of loop shape, destroyed by aggressive shaping.
- **Normalized coprime factors**: M = (I+GG*)^{-1/2}... the "distance" geometry behind why H∞ coprime design is intrinsically balanced.
- **γ-iteration**: H∞ suboptimal problem solved by bisection on γ with Riccati tests (γ > γ_opt for well-posedness).
- **Mixed sensitivity**: stacking specs into one ‖·‖∞ objective; √n conservatism per added spec (Ch 2).
- **Matching conditions**: when the H2 problem equals LQG (D-structure assumptions).

## Mental Models
- "LQG optimizes the nominal, H∞ protects the worst-case; loop-shaping decides what you actually get" — the synthesis method is never the design; the shape is.
- "α (coprime margin) is a free robustness audit of any loop shape": if your shaping drops α far below the unshaped α_max, you've asked for more bandwidth than the plant's uncertainty budget allows.
- "Shape first, synthesize second": W1/W2 carry your classical knowledge (integrators, slope −1, delay rolloff); the H∞ block just realizes it robustly.
- "Tracking and rejection can need different shapes → 2-DOF": put reference shaping outside the feedback loop (F_r / W_i scaling), keep K for robustness.

## Anti-patterns
- **Trusting LQG margins**: separation + optimality ≠ robustness; LTR is a limit result (Gladstone counterexample).
- **Over-shaping in loop-shaping design**: a beautiful σ̄(G_s) with tiny α gives a controller that shatters under coprime uncertainty; verify α(G_s) after shaping.
- **Single-DOF heroics for reference tracking**: forcing both rejection and crisp servo into one K; use prefilter/2-DOF instead.
- **Skipping the NS check after any synthesis** (recurring book warning).

## Reference Tables

### Objective → transfer function to shape
| Objective | Minimize | Open-loop proxy |
|---|---|---|
| Disturbance rejection (low ω) | σ̄(S) | σ̲(L) large |
| Noise attenuation (high ω) | σ̄(T) | σ̄(L) small |
| Tracking | σ(T) − I | σ(L) large |
| Control energy | σ̄(KS) | — |
| RS additive | σ̄(KS) | — |
| RS mult. output | σ̄(T) | — |

### H∞ loop-shaping procedure checklist
| Step | Action | Check |
|---|---|---|
| 1 | W1, W2 → desired σ̄(G_s) shape | slope −1 at target ω_c; integrators for type |
| 2 | coprime H∞ synth of G_s (2 Riccatis) | γ = γ_opt(G_s) |
| 3 | K = W1 K_s W2 | α = 1/γ vs unshaped α_max; NS; σ̄(S), σ̄(T) plots |

## Key Takeaways
1. All design objectives are statements about σ̄ of S, T, KS over frequency — plot them, that's the scoreboard.
2. LQG/H2 give optimal nominal performance but their robustness is a limiting argument; verify margins, don't assume them.
3. The coprime H∞ formula (γ_opt = √(1+ρ(XZ))) gives the exact stability radius of a shaped plant — cheap, two Riccati equations, no iteration.
4. McFarlane-Glover loop shaping = classical intuition + H∞ guarantee; the shaping weights are where your engineering lives.
5. Reference tracking vs disturbance rejection conflict is resolved with 2-DOF, not by straining K.
6. This chapter's H∞ solves are the inner engine of D-K iteration (Ch 8) when structure matters.

## Connects To
- **Ch 2**: loop-shaping fundamentals this chapter automates.
- **Ch 8**: μ-synthesis wraps these H∞ solves in D-K iteration.
- **Ch 7**: the uncertainty models (multiplicative/coprime) these designs guarantee against.
- **Ch 10**: choosing what to control before choosing K.
