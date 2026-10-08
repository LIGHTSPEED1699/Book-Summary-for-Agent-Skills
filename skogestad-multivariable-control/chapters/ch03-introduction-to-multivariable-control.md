# Chapter 3: Introduction to Multivariable Control (new in 2e; RGA material moved in from 1e ch10)

## Core Idea
MIMO systems must be analyzed with **directions, not just magnitudes**: gain, phase, poles, zeros, and uncertainty all have input/output directions, and the RGA is the first tool that reveals steady-state interaction structure.

## Frameworks Introduced
- **MIMO frequency response**: G(jω) maps a complex input vector to output vector; singular value decomposition G = UΣVᴴ gives principal gains σ_i(ω) with principal input directions v_i and output directions u_i.
  - Use when: reading Bode/Nyquist plots of a MIMO plant — never plot |g_ij| alone and conclude.
- **RGA Λ = (G⁻¹)ᵀ ⊙ G**: element-wise pairing measure.
  - How: compute at DC and at the gain crossover band; pair for λ > 0, prefer λ ≈ 1; RGA-number ‖Λ − I‖ over frequency.
- **General control problem formulation**: interconnect G (plant), G_d (disturbance path), W's (weights on r/e/u/y), K; the four-block N-Δ picture that ch8's μ tests run on.

## Key Concepts
- **Relative gain λ_ij**: gain g_ij open-loop divided by gain g_ij with all other loops perfectly closed.
- **λ interpretation**: λ ≈ 1 no interaction; λ ≈ 0 pairing useless (another loop owns it); λ < 0 integral action in the other loop destabilizes this pairing; |λ| ≫ 1 extreme sensitivity to model error.
- **Multivariable RHP zeros**: zeros of det G(s) with directions; constrain achievable bandwidth more subtly than SISO z/2 rule.
- **MIMO robustness preview**: per-channel margins can all be perfect while simultaneous perturbations destabilize (satellite: γ(G) ≈ 500) — motivates μ.

## Mental Models
- Think of G(jω) as an ellipse-mapper: σ̄ = longest semi-axis, σ̲ = shortest; the axes rotate with frequency.
- RGA is a **steady-state** interaction statement; interaction at crossover is a different animal (loop coupling) — check both windows.
- Pairing decisions made at DC can be undone by dynamics: always recheck Λ(jω) across the control band.

## Anti-patterns
- **Pairing by largest |g_ij| alone**: ignores direction and sign structure; RGA exists because this fails.
- **One RGA number for the whole problem**: Λ varies with frequency; report it over the band.
- **Trusting Λ = I at DC only**: triangular-ish plants look benign at DC and fight at crossover.

## Reference Tables
| λ_ij | Meaning for pairing (i,u_j) |
|---|---|
| ≈ 1 | good pairing, weak interaction |
| 0.2–1 | usable, check dynamics |
| ≈ 0 | pairing nearly useless |
| < 0 | wrong steady-state direction; not DIC |
| ≫ 1 | pairing possible but fragile to model error |

## Key Takeaways
1. SVD of G(jω) is the multivariable Bode plot: magnitudes + directions.
2. RGA at DC kills bad pairings fast; RGA over the band judges the survivors.
3. Negative steady-state λ + integral action = instability, no tuning fixes it.
4. The ch3 general formulation (weights + interconnection) is the input to every ch7–ch9 test.

## Connects To
- **Ch 6**: RGA as sensitivity to diagonal input uncertainty.
- **Ch 10**: pairing ladder, PRGA/CLDG for decentralized control.
- **App A.4**: RGA algebra, 2×2 closed forms.
