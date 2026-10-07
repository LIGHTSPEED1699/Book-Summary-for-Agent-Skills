# Chapter 7: Uncertainty and Robustness for SISO Systems

## Core Idea
Model uncertainty must be described as a frequency-shaped normalized set G_p = G + wΔ (or G(1+wΔ)), and then robustness becomes a clean Nyquist picture: the uncertainty disc around L(jω) must never cover −1 (RS), and the NP/RP circles must stay disjoint (RP) — yielding the design inequalities ‖w_O T‖∞ < 1 and ‖w_P S‖∞ + ‖w_O T‖∞ < 1.

## Frameworks Introduced
- **Uncertainty taxonomy**:
  - *Parametric*: gain k, time constant τ, delay θ variations — real, structured, frequency-coupled.
  - *Nonparametric* (dynamics shape unknown): additive G_p = G + w_A Δ; multiplicative input G_p = G(I + w_I Δ); multiplicative output G_p = (I + w_O Δ)G; inverse multiplicative G_p = (I + w_iI Δ)⁻¹G. All with ‖Δ‖∞ ≤ 1.
- **Weight-shaping rules** (fit weights to the relative error data |G_p−G|/|G|):
  - w_I (input multiplicative): high-pass — small at low ω (actuator gain known), ≥ 1 at high ω (unmodeled dynamics); e.g. w_I(s) = (s/M + ω*)/(s + ω*/A) with A < 1 < M.
  - w_O (output multiplicative): low-pass — ≥1 at low ω when steady-state gain is uncertain, → small at high ω.
  - w_A = |G| w_O (additive inherits plant rolloff); w_iI = w_O/(1−w_O) related forms.
  - Delay uncertainty θ ∈ [θ̄−Δθ, θ̄+Δθ]: w_I(s) = |e^{−Δθ s} − 1| ≈ min(2, Δθ·ω) — high-pass, magnitude → 2.
  - Gain uncertainty k ∈ [k̄(1−r), k̄(1+r)]: w = r constant (real Δ — complex treatment conservative).
- **RS conditions (SISO, exact for complex Δ)**:
  - Multiplicative (input or output): **‖w_I T‖∞ < 1 ⇔ |T| < 1/|w_I| ∀ω** — detune (T small) where relative uncertainty ≥ 1.
  - Additive: ‖w_A K S‖∞ < 1.
  - Inverse multiplicative: **‖w_iI S‖∞ < 1** — the opposite instruction: make S small where pole uncertainty is large (w_iI ≥ 1 allows RHP pole crossings → feedback needed to stabilize).
  - Equivalent Nyquist picture: discs of radius |w_I L| around L must not cover −1.
- **M-Δ structure preview**: RS ⇔ loop MΔ (M = w_I T) never encircles −1 for any ‖Δ‖∞ ≤ 1 ⇔ ‖M‖∞ < 1 — small-gain made exact because Δ's phase is free; the template for Ch 8.
- **NP/RP in the Nyquist plot**: NP with weighted sensitivity |S| < 1/|w_P| ⇔ L(jω) outside disc of radius |w_P L|/(1... ) centered... (equivalently distance from −1 ≥ |w_P L|... ); RP ⇔ NP-disc and RS-disc disjoint for all ω ⇔ SISO condition **|w_P(jω) S(jω)| + |w_O(jω) T(jω)| < 1 ∀ω** (necessary and sufficient for SISO).
- **GM vs complex-multiplicative margin**: real gain margin GM = 1/|L(ω_180)|; representing gain uncertainty as complex w_I gives smaller k_max (GM = 2 → k_max = 1.78) — quantified conservatism of complex Δ for real perturbations.

## Key Concepts
- **Relative vs absolute uncertainty**: multiplicative weights measure relative error (natural for gain/dynamics); additive weights measure absolute error (natural when G → 0 at high ω).
- **w ≥ 1 means "anything goes"**: where relative uncertainty exceeds 100%, the nominal model is meaningless at that frequency — the loop must be designed blind there (T ≈ 0 for RS, unless the uncertainty is pole-type).
- **Pole uncertainty vs zero uncertainty tension**: w_iI ≥ 1 permits unstable plants in the set (need |S| < 1), but a RHP zero forces S(z) = 1 — so large pole uncertainty is incompatible with RHP zeros (w_iI(z) ≤ 1 required).
- **Real vs complex Δ**: complex Δ is analytically convenient and exact for full complex sets; for real parametric uncertainty it's conservative (GM example).
- **Detuning example**: ZN gain K_c = 1.13 nominally stable but fails RS to a 33%-error plant; K_c = 0.31 achieves ‖w_I T‖∞ < 1 with margin to spare (bound is sufficient, not necessary, for a specific plant).

## Mental Models
- "Draw 1/|w| over T": RS is a one-plot check — T must stay under the inverse weight curve everywhere.
- "Where uncertainty is 100%, you are flying blind: T ≈ 0 (or S ≈ 0 for pole uncertainty)".
- "Crossover must live where uncertainty is small": both w_I and w_O below 1 around ω_c, or RP fails.
- "Fit weights to data, then round up": compute |G_p−G|/|G| over the plant family at each ω, take the max, fit the simplest high/low-pass through it.

## Anti-patterns
- **Checking only the nominal loop**: ZN-tuned example destabilizes on a 33% gain error plant.
- **Using complex-Δ margins as if exact for real parametric uncertainty** — over-conservative (1.78 vs GM 2); fine for design, wrong for claims.
- **Allowing pole uncertainty (w_iI > 1) at frequencies of RHP zeros** — interpolation S(z)=1 makes RS impossible.
- **Ignoring delay uncertainty as "small"**: Δθ = 2 s at ω_c = 1 rad/s is a 2 rad phase error — w_I ≈ 2, RS dead.

## Reference Tables

### RS conditions by uncertainty type (SISO)
| Uncertainty | Description | RS condition | Design action |
|---|---|---|---|
| Input multiplicative w_I | G_p = G(1+w_IΔ) | ‖w_I T‖∞ < 1 | T < 1/\|w_I\|; detune where w_I ≥ 1 |
| Output multiplicative w_O | G_p = (1+w_OΔ)G | ‖w_O T‖∞ < 1 | same (T = T_I = T_O SISO) |
| Additive w_A | G_p = G + w_AΔ | ‖w_A K S‖∞ < 1 | small K where w_A large |
| Inverse mult. w_iI | G_p = (1+w_iIΔ)⁻¹G | ‖w_iI S‖∞ < 1 | S small where w_iI ≥ 1 (pole uncertainty) |
| RP (output unc. + perf) | — | \|w_P S\| + \|w_O T\| < 1 ∀ω (n&s SISO) | crossover in low-uncertainty band |

### Weight fitting cheat
| Physical uncertainty | Weight |
|---|---|
| Gain k ∈ k̄(1±r) | w = r (real) |
| Delay θ̄ ± Δθ | w(s) = \|e^{−Δθ s} − 1\| ≈ min(2, Δθω) |
| Unmodeled fast dynamics (time const τ_u) | w_I ≈ high-pass, ≈1 at ω ≳ 1/τ_u |
| Unknown steady-state gain | w_O(0) = relative error at DC (low-pass) |

## Key Takeaways
1. Describe uncertainty as normalized weighted sets before designing; the weight shapes ARE the robustness spec.
2. RS with relative uncertainty = ‖w T‖∞ < 1: a single overlay plot on the T curve.
3. RP (SISO, output uncertainty) = |w_P S| + |w_O T| < 1 pointwise — NP and RS discs must not touch at any frequency.
4. Inverse multiplicative (pole) uncertainty flips the script: demand S small where w_iI ≥ 1 — and it's incompatible with RHP zeros.
5. Complex-Δ machinery is slightly conservative for real parametric problems but is the price of frequency-by-frequency tractability — μ (Ch 8) recovers the structure.

## Connects To
- **Ch 5**: uncertainty rules of thumb (100% uncertainty ≈ imaginary-axis zero) made rigorous here.
- **Ch 8**: same M-Δ structure for MIMO; ‖·‖∞ conditions become μ for structured Δ.
- **Ch 2**: M_s, GM/PM as crude uncertainty margins this chapter replaces with weights.
- **Ch 9**: weights from this chapter feed H∞/loop-shaping synthesis.
