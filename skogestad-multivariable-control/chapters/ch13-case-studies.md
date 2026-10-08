# Chapter 12: Case Studies (Helicopter, Aero-engine, Distillation)

## Core Idea
Three worked industrial designs show the book's pipeline end-to-end — structure selection → shaped synthesis → μ/σ̄ robustness analysis — and each one's lesson is the same: the structure and scaling decisions made before synthesis decide success.

## Frameworks Introduced
- **The 7-step industrial design process** (12.1): (1) plant modelling, (2) plant I/O controllability analysis, (3) control structure design, (4) controller design (formulate → synthesize), (5) control system analysis (analysis + simulation vs specs), (6) implementation (anti-windup, bumpless transfer), (7) commissioning. The book covers 2-5.
- **Helicopter (gust rejection via signal-based weights)**: S/KS mixed-sensitivity H∞ with W1 (loop-shape: finite-gain integrators 500 for tracking, band-pass in rate channels), W2 (high-pass actuator limiter, corner 10 rad/s), W3 (signal weight on r: 1 on primary outputs, 0.1 on fictitious rate demands). Then **add the disturbance model as an extra input**: gusts perturb velocity states via G_d = C(sI−A)⁻¹B_d (B_d = columns of A), add W4 = γI to the cost; γ = 30 halves turbulence effects with same controller order and similar S/KS shapes. Weight-selection reasoning: unmodeled rotor dynamics at 10 rad/s cap W1 bandwidth; 6×6 S with only 4 inputs ⇒ two singular values stuck at 1 (rate channels) — shape what you can.
- **Aero-engine (structure selection + 2-DOF loop shaping)**: 3 inputs (fuel WFE, nozzle AJ, IGV), 6 candidate outputs in 3 subsets, pick one per subset ⇒ 6 candidate sets. Screening ladder: (a) scale outputs to equal "badness" of cross-coupling (7.5% thrust = 1 unit; 5% surge margin = 1 unit), inputs to 10% of range; (b) RGA row-sums of non-square G_all for coarse screening; (c) σ̲(G(0)) per candidate set (bigger = smaller ‖G⁻¹(y−y_opt)‖) — kills sets 1-3; (d) RHP zeros vs 10 rad/s bandwidth target — OPR2 brings slow RHP zeros (30.9, 27.7 rad/s, moving left at higher thrust) — kills sets 3, 6; (e) RGA-number over frequency; (f) tie-break sets 4 vs 5 by **Hankel singular values** (OPR1 carries more state information than NL) ⇒ Set 5 (OPR1, LPEMN, NH). Pairing from steady-state RGA ≈ I. Then 2-DOF H∞ loop shaping: W_p = I/s integrators, align gain W_a at 7 rad/s (only legal because RGA small there), W_g = diag(1, 2.5, 0.3) for actuator rates; γ_min = 2.3 (shaped plant compatible); T_ref slower on NH; settle at γ = 2.9 (slightly suboptimal avoids very fast controller poles for discretization); prefilter scaled for exact DC model matching; 27-state controller; σ̄(S) peak 1.44, small T and T_I peaks ⇒ good input+output uncertainty robustness; nonlinear sims clean.
- **Distillation column (the book's running ill-conditioned example, consolidated)**: 40-tray equimolar binary column, α = 1.5, 99% purities, 82-state model; LV configuration (L, V → y_D, x_B) with levels/pressure already closed. Idealized 2×2 model: κ(G) = 141.7, λ₁₁ = 35.1 at all frequencies — inverse-based control shatters under 20% diagonal input uncertainty (Motivating Example 2 explained by μ RP in 8.11.3; μ-optimal DK design achieves peak μ = 0.974). **CDC benchmark**: 20% gain uncertainty + up to 1 min delay per channel; time-domain step specs (y₁ ≥ 0.9 after 30 min, overshoot ≤ 1.1, interaction |y₂| ≤ 0.01 at steady state, peak |y₁| ≤ 0.5... ) plus σ̄(K_y S̃) < 0.316; solvable with 2-DOF loop shaping or 2-DOF μ-optimal designs. **Detailed 5-state model** (reduced from 82): liquid flow dynamics make G(jω) upper-triangular at higher ω ⇒ RGA elements fall off with frequency — control at crossover easier than the frequency-independent λ = 35.1 idealization suggests; feedforward + partial controllability analyses use it.

## Key Concepts
- **Signal-based vs loop-shaping weights**: W1/W2 shape the loop; W3/W4 encode signals (references, measured disturbance models) directly into the H∞ cost.
- **Disturbance-as-extra-input trick**: model gusts/d_i entering through state matrix columns → G_d → weight W4 → same-order controller, much better rejection.
- **Structure screening ladder** (aero-engine): scaling → RGA row sums → σ̲(G(0)) → RHP zeros vs bandwidth → RGA-number → HSV tie-break.
- **Align gain legality**: only align (set crossover) where RGA is small; ill-conditioned plants break alignment.
- **Slightly-suboptimal γ is engineering-optimal**: near-optimal H∞ controllers hide fast poles; discretization and H2 performance favor backing off.
- **Frequency-dependent conditioning**: an idealized model's constant large RGA can overstate the difficulty; physical fast dynamics (liquid flow) triangularize G at higher ω.

## Mental Models
- "Put the disturbance physics into the plant, not into tighter weights" — the gust redesign beat the standard design by modeling d explicitly.
- "Screen structures with cheap steady-state tools first, save the expensive tie-breakers (HSV, second operating point) for the final two candidates."
- "RHP zeros are structure-dependent": the same engine gains slow zeros just by choosing OPR2 as a controlled output.
- "Benchmark problems are uncertainty descriptions in disguise" — CDC = gain+delay per channel + time-domain specs; translate to w_I via delay-uncertainty weights.

## Anti-patterns
- **Choosing outputs by biggest steady-state gain**: LPPR has the largest gain (11.0) yet every set containing it was eliminated (σ̲ small, ill-conditioned).
- **Taking the idealized distillation model's λ = 35.1 as gospel at crossover** — the detailed model's flow dynamics relax it; but never relax the DC RGA warning.
- **Pushing γ to optimality in H∞ synthesis** — fast controller poles; check sample-rate feasibility.
- **Aligning/crossover-setting an ill-conditioned plant** — alignment is only safe where RGA is benign.

## Reference Tables

### Aero-engine structure screening results
| Set | Outputs | RHP zeros < 100 | σ̲(G(0)) | Verdict |
|---|---|---|---|---|
| 1 | NL, LPPR, NH | none | 0.060 | out (σ̲) |
| 2 | OPR1, LPPR, NH | none | 0.049 | out (σ̲) |
| 3 | OPR2, LPPR, NH | 30.9 | 0.056 | out (both) |
| 4 | NL, LPEMN, NH | none | 0.366 | finalist |
| 5 | OPR1, LPEMN, NH | none | 0.409 | **chosen** (HSV tie-break) |
| 6 | OPR2, LPEMN, NH | 27.7 | 0.392 | out (zeros) |

### Case study → technique map
| Study | Technique showcased | Key result |
|---|---|---|
| Helicopter | mixed-sensitivity + disturbance modeling | gust effect ~halved, same order |
| Aero-engine | structure selection + 2-DOF loop shaping | <10% interaction, M_s 1.44, 27 states |
| Distillation | ill-conditioning + μ | λ=35.1 kills inverse control; μ-opt DK works |

## Key Takeaways
1. The full pipeline is model → controllability → structure → synthesis → analysis → implementation → commissioning; most failures are prevented at steps 2-3.
2. Disturbance models belong in the generalized plant; signal weights (W3/W4) are free performance.
3. Structure screening is a cheap-to-expensive ladder; steady-state σ̲ and RHP-zero location vs bandwidth are the strongest filters.
4. The distillation column is the canonical ill-conditioned MIMO plant: RGA 35 at DC, μ explains the failure, DK-iteration fixes it (μ = 0.974).
5. Engineering-optimal ≠ mathematically-optimal synthesis: back off γ for implementable controllers.

## Connects To
- **Ch 10**: the aero-engine ladder is its toolkit in action; distillation LV/DV/DB configurations from Example 10.6.
- **Ch 9**: loop-shaping procedure and 2-DOF setup used verbatim.
- **Ch 8**: μ RP analysis and DK-iteration on the distillation benchmark.
- **Ch 11**: 82→5 state reduction enabling the 5-state analyses.
- **Ch 3/6**: the distillation model's SVD/directions/RGA introduced there return here.
