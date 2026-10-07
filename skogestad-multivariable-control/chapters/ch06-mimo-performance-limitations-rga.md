# Chapter 6: Limitations on Performance in MIMO Systems (Controllability + RGA)

## Core Idea
MIMO controllability = the SISO bandwidth rules plus *directions*: RHP zeros/poles constrain S and T only along their output directions, the minimum singular value σ̲(G) measures input authority in the worst direction, and the RGA predicts when inverse-based/decoupling control will be destroyed by always-present diagonal input uncertainty.

## Frameworks Introduced
- **14-step MIMO controllability analysis procedure** (the chapter's crown jewel; plant-only, run before/while choosing structure):
  1. Scale all variables (u, y, d, r; r = R e_r).
  2. Minimal realization.
  3. Functional controllability: m ≥ l and rank G = l (σ̲(G(jω)) ≠ 0 except jω-axis zeros); if not, find the zero-gain output direction.
  4. Poles: locations + output directions of RHP poles ("fast" RHP poles far from origin are bad).
  5. Zeros: locations + directions of RHP zeros; watch zeros pinned to specific outputs ("small" RHP zeros near origin are bad).
  6. RGA Λ(jω) = (G⁻¹)ᵀ ⊗ G (elementwise λ_ij = g_ij (G⁻¹)_ji); large RGA elements at crossover frequencies = difficult plant.
  7. Singular value plots σ̄, σ̲ of G(jω) + singular vectors (scaling critical from here).
  8. σ̲(G(jω)) is THE controllability measure: need σ̲(G) ≳ 1 at frequencies where control is needed (can't make unit output changes in all directions with unit inputs if σ̲ < 1).
  9. Disturbances: columns g_d of G_d; need ‖S y_d‖ ≤ 1/‖g_d‖ in disturbance direction ⇒ at least σ̲(S) ≤ 1/‖g_d‖₂, possibly σ̄(S) ≤ 1/‖g_d‖₂.
  10. Input saturation: (a) elements of G⁻¹G_d < 1 everywhere ⇒ perfect control OK; (b) else check UᴴG_d rows < σ_i(G) + 1 for acceptable control.
  11. Compatibility: |y_zᴴ g_d(z)| ≤ 1 for each RHP zero × disturbance pair; combined RHP pole/zero via c₁, c₂ constants.
  12. Uncertainty: small γ(G) ⇒ no problem; large RGA elements ⇒ strong sensitivity (details: Ch 8 μ).
  13. Decentralized control → CLDG/PRGA (Ch 10).
  14. Condition number/RGA usage summary (Ch 3.6).
- **Interpolation constraints (the direction-aware generalization of SISO integral constraints)**:
  - RHP zero z with output direction y_z: y_zᴴ T(z) = 0 and y_zᴴ S(z) = y_zᴴ (S has eigenvalue 1 in that direction).
  - RHP pole p with output direction y_p: S(p) y_p = 0, y_pᴴ T(p) = y_pᴴ.
  - Consequence: peaks unavoidable — max_ω σ̄(S) ≥ c₁, max_ω σ̄(T) ≥ c₂ with (one RHP zero z + one RHP pole p) c₁ = c₂ = √[(1 + ((1+|p|/|z|)... ] interpolating between SISO value |z+p|/|z−p| (aligned directions, φ=0) and 1 (orthogonal directions, φ=90°: no penalty!). φ = arccos|y_zᴴ y_p|.
  - Blaschke factorization G = B_p G̃ = Ĝ B_z with all-pass B_p, B_z built from directions gives multi-pole/zero bounds (Theorem 6.3).
- **RGA as input-uncertainty sensitivity**: feedforward/inverse-based error e₀ = G E_I G⁻¹ r; for diagonal input uncertainty the diagonal of G E_I G⁻¹ = Λ diag(ε) — RGA elements directly scale the worst error; scaling-independent. Large |λ_ij| in the control bandwidth ⇒ inverse-based control forbidden.
- **Sensitivity bounds under uncertainty (condition numbers)**: σ̄(S₀) ≤ [1 + σ̄(G)σ̄(G⁻¹)] σ̄(S)/(1−σ̄(E_I)σ̄(T_I)) type bounds; a "round" controller (κ(K) ≈ 1) and decentralized control (κ_O(K) = 1) are intrinsically tolerant of diagonal input uncertainty; inverse-based control has lower bound σ̄(S₀) ≥ ‖Λ(G)‖_i1 · |w_I| · |t| at crossover (Theorem 6.7: max row-sum of RGA appears).
- **Feedback vs feedforward under uncertainty**: output uncertainty error with FF = E_O y; with feedback = S₀ E_O y — feedback shrinks uncertainty effect by S₀ at low freq; uncertainty only bites in the crossover region where S, T ~ 1.
- **Plant modification menu when not controllable**: relax specs on hopeless outputs; bigger/closer actuators (fix σ̲ < 1); add inputs to eliminate RHP zeros (unless pinned); add fast local loops near disturbances/inputs (cascade); dampen disturbances (buffer tanks, springs); speed up plant/reduce delays (exception: added lag can help strongly interactive plants; delay in measured-disturbance path helps feedforward).

## Key Concepts
- **Functional controllability**: number of independent steady-state controls = rank G(0); integrator/differentiator structure from first nonzero Markov parameter; need rank = l.
- **RGA**: Λ = (G⁻¹)ᵀ ⊗ G; scale-invariant; rows/cols sum to 1; Λ(G⁻¹) = Λ(G); Λ(Gᵀ) = Λ(G)ᵀ; for 2×2 one parameter λ = λ₁₁ determines all; Λ = I for diagonal/triangular G.
- **RGA pairing rules** (with Ch 3.6/Appendix A.4): pair to keep all λ > 0 (prefer λ ≈ 1); λ < 0 for a pairing ⇒ that single-loop pairing is unstable at high gain / wrong steady-state direction; large λ ⇒ near-singular G, decoupling fragile.
- **Sign test (Yu-Luyben/Hovd-Skogestad)**: for relative-degree-1 plants, det G(0)·det G'(0) < 0 ⇒ some RGA element negative ⇒ instability with any diagonal pairing under integral control (zero steady offset impossible).
- **Pinned zeros**: an RHP zero whose output direction coincides with one output — that output can't be freed by adding inputs elsewhere.
- **Minimized condition numbers**: κ_O(G) = min_{D_O diag} κ(D_O G D_O), κ_I(G) similar — the right measure of "inherently ill-conditioned" vs "badly scaled".
- **Zero directions and disturbances**: |y_zᴴ g_d(z)| ≤ 1 — a disturbance invisible to the RHP zero's direction is harmless.

## Mental Models
- "σ̲(G) ≥ 1 where you need control" is the MIMO version of 'the input must matter'.
- "RGA is a fragility forecast, not a pairing oracle": large λ at crossover ⇒ any inverse-based/decoupling design breaks under ~20% channel gain errors; small λ doesn't guarantee safety (triangular plants: off-diagonal leak g₂₁/g₁₁).
- "RHP pole/zero pairs in orthogonal directions are nearly free" — direction alignment, not just proximity, sets the penalty.
- "When the analysis says infeasible, change the plant": the modification menu is part of the method, not an afterthought.

## Anti-patterns
- **Inverse-based/decoupling control on large-RGA plants** (distillation column: λ₁₁ = 35 → 12% gain error destabilizes; 20% wrecks performance).
- **Pairing by largest |g_ij| alone** — must check RGA signs and magnitudes at the relevant frequencies.
- **Using full-block uncertainty bounds when the uncertainty is diagonal** — loses the structure that RGA/μ capture; overly conservative.
- **Forgetting measurement delay G_m in Rules 5-6 equivalents** — sensor transport delay caps ω_c just like process delay.

## Reference Tables

### RGA quick facts
| Property | Statement |
|---|---|
| Definition | λ_ij = g_ij (G⁻¹)_ji |
| Scaling | invariant to input/output scaling |
| Sums | each row and column sums to 1 |
| 2×2 | Λ determined by λ₁₁; λ₂₂=λ₁₁, λ₁₂=λ₂₁=1−λ₁₁ |
| λ < 0 | that pairing cannot have zero steady offset with integral action (sign test) |
| \|λ\| ≫ 1 | G near singular; inverse-based control fragile; input-uncertainty error ≈ λ·ε |
| Λ = I | diagonal or triangular plant |

### MIMO controllability measures
| Measure | Good | Bad | Where |
|---|---|---|---|
| σ̲(G(jω)) | ≥ 1 at control frequencies | ≪ 1 (shopping cart) | step 8 |
| RGA elems at ω_c | \|λ\| ≈ 1 | \|λ\| ≫ 1 or λ < 0 | step 6 |
| κ(G), κ_O(G) | ~1 | ≫ 1 | step 12 |
| RHP zero z | large z (far right) or orthogonal to disturbances | small z near origin, pinned | steps 5, 11 |
| RHP pole p | slow, orthogonal to zero dirs | fast (ω_c > 2p needed) | step 4 |
| G⁻¹G_d elems | < 1 | > 1 (saturation) | step 10 |

## Key Takeaways
1. Run the 14-step procedure on every candidate I/O set; it's controller-independent and cheap.
2. Directions everywhere: S/T interpolation constraints, disturbance rejection, and pole-zero penalties all act along specific directions — check alignment before panicking at a RHP zero.
3. σ̲(G(jω)) ≥ 1 at control frequencies is the single most useful plant-only measure.
4. RGA large at crossover ⇒ never invert; prefer diagonal/SVD-direction control; the worst-case error scales as ‖Λ‖_i1·ε.
5. Diagonal input uncertainty is always present (~20% in process plants) — it, not full-block uncertainty, is what kills decoupled designs.
6. Infeasibility verdicts are invitations to modify the plant (actuators, extra inputs, local loops, disturbance damping).

## Connects To
- **Ch 5**: these rules with directions removed; decentralized MIMO inherits them via CLDG/PRGA (Ch 10).
- **Ch 3**: RGA/condition-number intro used here in earnest.
- **Ch 8**: μ replaces these plant-only heuristics for exact RS/RP with a given controller.
- **Ch 10**: structure selection (which inputs/outputs) uses these measures at scale.
- **Appendix A.4**: full RGA property list.
