# Cheatsheet — Skogestad & Postlethwaite quick reference

## SISO controllability rules (ch5) — all on scaled variables
| # | Constraint | Bound |
|---|---|---|
| 1 | reject disturbances | ω_c > ω_d (where \|G_d\| crosses 1); \|S\| ≤ 1/\|G_d\| |
| 2 | track reference R | \|S\| ≤ 1/R up to ω_r |
| 3 | input limits vs d | \|G\| > \|G_d\| − 1 where \|G_d\| > 1 |
| 4 | input limits vs r | \|G\| > R⁻¹ up to ω_r |
| 5 | delay θ in G G_m | ω_c < 1/θ |
| 6 | RHP zero z | ω_c < z/2 (real), < \|z\| (imag); or ω_c > 2z for high-freq tight control |
| 7 | phase lag | ω_c < ω_u (∠GG_m = −180°) — subsumes 5-6 for PID |
| 8 | RHP pole p | ω_c > 2p and \|G\| > \|G_d\| up to p |

## MIMO controllability procedure (ch6, condensed)
1 scale → 2 minimal realization → 3 rank G = l → 4 RHP poles (+dirs) → 5 RHP zeros (+dirs, pinned?) → 6 RGA at crossover → 7 σ̄,σ̲ plots → 8 σ̲(G) ≳ 1 where control needed → 9 ‖S y_d‖ ≤ 1/‖g_d‖ per disturbance → 10 saturation: G⁻¹G_d elems < 1 → 11 \|y_zᴴ g_d(z)\| ≤ 1; c₁,c₂ pole/zero combos → 12 γ(G), RGA vs input uncertainty → 13 decentralized: CLDG/PRGA → 14 κ/RGA summary.

## Robustness conditions (ch7-8)
| Condition | Test |
|---|---|
| RS, input mult. w_I | ‖w_I T_I‖∞ < 1 (SISO: \|T\| < 1/\|w_I\|) |
| RS, output mult. w_O | ‖w_O T‖∞ < 1 |
| RS, additive w_A | ‖w_A K S‖∞ < 1 |
| RS, inverse mult. w_iI | ‖w_iI S‖∞ < 1 (pole uncertainty!) |
| RP (SISO) | \|w_P S\| + \|w_O T\| < 1 ∀ω (nec & suf) |
| RS (MIMO structured) | max_ω μ_Δ(N₁₁(jω)) < 1 (+ NS check!) |
| RP (MIMO) | max_ω μ_{diag(Δ,Δ_P)}(N(jω)) < 1, Δ_P full block |
| Coprime RS | γ_opt = √(1+ρ(XZ)); need γ < 1/α (α = uncertainty size) |

## Weight shapes (ch7)
| Uncertainty | Weight |
|---|---|
| gain k̄(1±r) | w = r (real) |
| delay θ̄ ± Δθ | w(s) = \|e^{−Δθ s} − 1\| ≈ min(2, Δθ ω) |
| unmodeled fast dyn (τ_u) | w_I high-pass, → ≥1 for ω ≳ 1/τ_u |
| unknown DC gain | w_O low-pass, w_O(0) = rel. error |
| performance (offset A, peak M, bandwidth ω_B*) | 1/\|w_P\| = (s/M + ω_B*)/(s + ω_B*/A)-type |

## RGA rules (ch3/6/10, App A.4)
- Λ = (G⁻¹)ᵀ ⊙ G; scale-invariant; rows/cols sum to 1; 2×2: Λ = [λ 1−λ; 1−λ λ].
- Pair for λ > 0, prefer λ ≈ 1; λ < 0 at DC ⇒ no integrity/DIC.
- Λ ≈ I at crossover ⇒ decentralized loops safe (Thm 10.4: Λ ≡ I ⇔ triangular ⇒ loop stability ⇒ overall stability).
- Large λ in control band ⇒ inverse-based error ≈ λ·ε (diagonal input uncertainty).
- Sign test: relative-degree-1 plant, det G(0)·det G′(0) < 0 ⇒ some λ < 0 ⇒ diagonal PI can't give zero offset.

## Decentralized control (ch10)
- S = S̃(I + E T̃)⁻¹, E = (G − Ĝ)Ĝ⁻¹.
- Sufficient stability: μ(E) σ̄(T̃) split (Grosdidier-Morari); μ(E) < 1 ⇒ generalized diagonal dominance.
- Per-loop disturbance: \|1 + L_i\| > \|g̃_di\| (CLDG) where \|g̃_di\| > 1.
- References: S ≈ S̃ Γ (PRGA) where feedback effective.

## Model reduction (ch4/11)
| Method | Preserves | H∞ error bound |
|---|---|---|
| Balanced truncation | D | 2 Σ dropped HSVs |
| Balanced residualization | G(0) exactly | 2 Σ dropped HSVs |
| Optimal Hankel (D_o) | — | Σ dropped HSVs (σ_{k+1} once) |
- Unstable: reduce stable part, or normalized coprime factors [N M].
- Control models: keep gain, delay, RHP zeros, integrators, dynamics near ω_c; residualization default.

## Norms (ch4, App A.5)
| Norm | Formula | Answers |
|---|---|---|
| H2 | √tr(CPCᵀ) | impulse energy; rms out to white noise |
| H∞ | sup_ω σ̄(G) | worst sinusoid gain; induced L2 |
| Hankel | √ρ(PQ) | state energy; reduction currency |

## Margins vs peaks (ch2)
- GM ≥ M_s/(M_s − 1); PM ≥ 2 arcsin(1/(2M_t))... use M_s ≈ 2, M_t ≈ 1.4 as design targets.
- Bandwidth-delay: ω_B θ ≲ 0.5-1 for sane response; ω_B < 1/θ hard.

## Synthesis quick (ch9)
- LQG: K_r = BᵀX, K_f = YCᵀ (two AREs); margins only in LTR limit — verify.
- H∞ coprime: two Riccatis + γ-iteration; γ_opt explicit, no iteration for the stability-radius controller.
- Loop shaping: G_s = W1 G W2 → coprime synth → K = W1 K_s W2; check α(G_s).
- D-K: alternate H∞ solve on D N D⁻¹ and D update; local minima — try multiple starts.

## The book's numbers to remember
- Distillation column A: κ(G) = 141.7, λ₁₁ = 35.1; 20% input uncertainty destabilizes inverse control; μ-optimal peak 0.974.
- Satellite: γ(G) ≈ 500 — simultaneous channel errors fatal despite perfect per-channel margins.
- Aero-engine: 15→6 states (HSV cut), ω_c ≈ 7 rad/s, M_s = 1.44, γ = 2.9 (suboptimal by design).
- ZN gain 1.13 → RS fails at 33% plant error; K = 0.31 passes (‖w_I T‖∞ < 1).
