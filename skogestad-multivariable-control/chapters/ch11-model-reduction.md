# Chapter 11: Model Reduction

## Core Idea
Rank states by joint controllability-observability (Hankel singular values) via a balanced realization, then drop the weak ones — with a guaranteed H∞ error bound: twice the sum of the dropped HSVs for truncation/residualization, the plain sum for optimal Hankel norm approximation; and for control-oriented models, residualization's exact steady-state match usually beats the smaller theoretical bounds of the other methods.

## Frameworks Introduced
- **Modal truncation**: diagonalize A, drop fastest |λ_i|; error = Σ dropped C_i(sI−λ_i)⁻¹B_i so residue size c_i b_iᵀ matters as much as λ distance — distance from jω-axis alone is NOT a reliable keep/drop indicator; advantage: kept poles are a subset of the physical modes (phugoid stays named).
- **Residualization**: set ẋ₂ = 0 (singular perturbation), solve for x₂: A_r = A₁₁ − A₁₂A₂₂⁻¹A₂₁, B_r = B₁ − A₁₂A₂₂⁻¹B₂, C_r = C₁ − C₂A₂₂⁻¹A₂₁, D_r = D − C₂A₂₂⁻¹B₂. **Preserves steady-state gain exactly** (G_a(0) = G(0)); truncation instead preserves behavior at s = ∞ (D match); the two are related by bilinear s → 1/s.
- **Balanced realization**: minimal stable realization with controllability Gramian P = observability Gramian Q = Φ = diag(σ_1 ≥ ... ≥ σ_n > 0) (solve the two Lyapunov equations, then a similarity transform); σ_i = Hankel singular values, σ_1 = ‖G‖_H; each σ_i measures state i's joint contribution to I/O behavior; balancing ignores D.
- **Balanced truncation** (Moore 1981): drop states of small σ; reduced model is itself balanced; error bound ‖G − G_a‖∞ ≤ 2(σ_{k+1} + ... + σ_n) ("twice the sum of the tail"; repeated HSV counted once); algorithms exist without forming the balanced realization (Tombs-Postlethwaite, Safonov-Chiang; approximate Lyapunov for very high order).
- **Balanced residualization** (Fernando-Nicholson): residualize the balanced realization; same error bound as balanced truncation (Liu-Anderson 1989).
- **Optimal Hankel norm approximation** (Glover 1984): minimize ‖G − G_k‖_H over degree-k models; optimum error = σ_{k+1} exactly; closed-form construction from the balanced realization with the σ_{k+1}...σ_{k+l} block split and unitary U; with Glover's special D_o choice: ‖G − G_k‖∞ ≤ σ_{k+1} + σ_{k+l+1} + ... + σ_n ("sum of the tail" — half the truncation bound); non-square: augment with zero columns; F(s) anti-stable remainder.
- **Unstable model reduction, two routes**:
  1. **Stable-part reduction** (Enns/Glover): G = G_s + G_u (anti-stable part kept verbatim), reduce G_s only.
  2. **Coprime factor reduction** (McFarlane-Glover): G = M⁻¹N normalized left coprime; balance and reduce the stable stacked [N M]; G_a = M_a⁻¹N_a; Meyer's theorem: balanced truncation of [N M] preserves normalized left-coprimeness and HSVs.
- **Controller reduction subtlety**: reduce [K₁ W_i K₂] as a block (with prefilter) rather than K alone; truncation/Hankel reduce steady-state gain → rescaling the prefilter destroys the guaranteed bound (observed degradation 1.44 → 3.66); residualization keeps it and performs best closed-loop.
- **Frequency-weighted reduction**: emphasize bands, pay elsewhere; bound only for weighted Hankel approximation; weight choice hard; balanced residualization ≈ implicit low/mid-frequency weighting.

## Key Concepts
- **Hankel singular values σ_i(PQ)^½**: the reduction currency; energy of a state's past-input→future-output map.
- **"Twice the sum of the tail" vs "sum of the tail"**: the headline bound comparison (truncation/residualization vs optimal HN).
- **McMillan degree**: model order = states of minimal realization.
- **L∞ norm for unstable systems**: sup_ω σ̄ over imaginary axis (no jω-axis poles) — needed because reduction error of unstable G can be unstable.
- **Steady-state gain preservation**: residualization exact; truncation/HN need rescaling, which can wreck the bound.

## Mental Models
- "Balance first, then the tail tells you the price": the dropped HSV sum IS your error budget before you compute anything.
- "Residualization for plants, truncation for high-frequency fidelity": process models are already inaccurate at high ω; what matters is DC-to-crossover match — residualization wins in practice (aero-engine: error 0.295 vs 0.324, smallest near the 10 rad/s design band).
- "Never reduce away what the loop leans on": unstable modes, integrating modes, delays, RHP zeros (Ch 4 rule) — for unstable plants use stable-part or coprime reduction so those survive structurally.
- "Bounds are worst-case; check the error where you design": compare σ̄(G−G_a) at the control band, not just the peak.

## Anti-patterns
- **Truncating a controller then rescaling the prefilter** — destroys the guarantee; residualize controllers instead (case study: only the residualized 2-DOF controller stayed acceptable).
- **Dropping states by pole distance alone** (modal truncation without residue check).
- **Balanced-reducing an unstable plant directly** — methods assume stability; decompose or use coprime factors.
- **Heavy frequency weighting to force DC match** — blows up errors elsewhere; residualization already does it implicitly.
- **Blindly trusting the 2×tail bound** — actual errors run ~half the bound (0.295 vs 0.635), but the bound's ordering across methods is what you should use.

## Reference Tables

### Method comparison
| Method | Preserves | H∞ error bound | Best at |
|---|---|---|---|
| Modal truncation | poles ⊂ original | Σ‖c_i b_iᵀ\|/\|λ_i\| (loose) | physical mode interpretation |
| (Balanced) truncation | D (high-freq) | 2 Σ tail HSVs | high-frequency match |
| (Balanced) residualization | G(0) exactly | 2 Σ tail HSVs | low/mid freq — default for plants |
| Optimal Hankel norm | — (D_o tunable) | Σ tail HSVs (k+1 counted once) | smallest guaranteed error |
| Coprime-factor | coprimeness (trunc.) | via [N M] tail | unstable plants |

### HSV decision guide (aero-engine example: 15 → 6 states)
| HSV pattern | Action |
|---|---|
| σ_i ≫ σ_{i+1} | cut there |
| σ tail sum × 2 < uncertainty weight at ω_c | safe cut |
| error σ̄(G−G_a) < 1/w_I in control band | good for design |

## Key Takeaways
1. Balanced realization + HSV tail = principled reduction with a computable error budget; residualization is the control-engineer's default (exact DC match, same bound, cheap).
2. Optimal Hankel norm approximation has the best bound (sum vs twice-sum) but loses DC gain — rescaling can void the guarantee.
3. For unstable plants: reduce the stable part or the normalized coprime factors; never the raw unstable model.
4. Judge reduction by error in the design band relative to uncertainty weights, not by the global norm alone.
5. Reduce controllers as [K₁W_iK₂] blocks and residualize them; truncation/HN + rescaling degraded closed-loop performance badly in the book's case study.

## Connects To
- **Ch 4**: Hankel norm/HSV foundations; "keep delays/RHP zeros/integrators" reduction rules.
- **Ch 9**: coprime factors and normalized factorization used for unstable reduction.
- **Ch 12**: aero-engine 15→6 state reduction feeding the μ design.
- **Appendix A.5**: Gramians, Lyapunov equations, norm identities.
