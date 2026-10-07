# Design Patterns — Skogestad & Postlethwaite

The book's actual method, distilled into reusable patterns. Apply top to bottom; each pattern gates the next.

## P1. Scale before you compute
Scale every input, output, disturbance to expected operating magnitude (u, y, d, r ∈ ~[-1,1] in normal operation). Every rule in P2-P10 is meaningless on unscaled data. Choose scalings so "1 unit of error" is equally bad everywhere (aero-engine: 1 unit = 7.5% thrust = 5% surge margin).

## P2. Controllability before controller (plant-only verdict)
Run the SISO rules (ch5) or the 14-step MIMO procedure (ch6) on every candidate I/O set. Output: a feasible ω_c window per loop/output. Empty window ⇒ stop; go to P10 (plant modification), not to tuning.

## P3. σ̲(G) ≥ 1 where control is needed
The single most useful MIMO measure. If σ̲(G(jω)) < 1 at frequencies where |G_d| > 1, unit disturbances need more than unit inputs — bigger/closer actuators or feedforward.

## P4. RGA in two windows
- **Crossover window**: Λ(jω) ≈ I ⇒ diagonal loops interact benignly (stability); Λ far from I ⇒ loop interactions destabilize at crossover.
- **DC window**: any λ_ij < 0 for a pairing ⇒ wrong steady-state direction, no integrity, not DIC.
- **|λ| ≫ 1 anywhere in the control band**: inverse-based/decoupling control is forbidden; worst-case error ≈ ‖Λ‖_i1 · ε under diagonal input uncertainty.

## P5. Directions before magnitudes
For every RHP zero/pole: get location AND directions. Check alignment: |y_zᴴ y_p| ≈ 0 ⇒ pole-zero pair nearly harmless; |y_zᴴ g_d(z)| small ⇒ disturbance invisible to that zero. Pole/zero at same s with different directions do NOT cancel.

## P6. Weights from data, then two overlay checks
Fit w_I (high-pass), w_O (low-pass), w_A to measured |G_p−G|/|G| across the plant family; delay uncertainty → w = |e^{−Δθs}−1|. Then check: ‖w_I T‖∞ < 1 (RS) and |w_P S| + |w_O T| < 1 (RP). Crossover must live where both weights are below 1.

## P7. μ for structured truth
When diagonal (channel-wise) uncertainty is the real threat, replace σ̄ tests with μ: N-Δ form → RS: μ_Δ(N₁₁) < 1; RP: μ_{diag(Δ,Δ_P)}(N) < 1; always check NS separately. Use skewed μ for "how much can this one error grow" questions.

## P8. Shape first, synthesize second (H∞ loop shaping)
W1/W2 carry the classical shape (integrators, slope −1 at target ω_c, rolloff past delay frequency). Robustly stabilize normalized coprime factors of the shaped plant (γ_opt = √(1+ρ(XZ))); verify α didn't collapse. Back off to slightly suboptimal γ for implementable controllers. 2-DOF + prefilter scaling for exact DC model matching.

## P9. Structure ladder for variable selection
Scale → RGA row-sums of G_all (screen) → σ̲(G(0)) per candidate set → RHP zeros vs target bandwidth → RGA-number over frequency → HSV tie-break. Pairing: Λ ≈ I at crossover, no negative λ at DC. Check decentralized fixed modes before diagonal control.

## P10. Infeasible? Modify the plant, not the spec sheet
Menu: relax spec on hopeless outputs (partial control); bigger/closer actuators (fix σ̲); add inputs to push out RHP zeros (unless pinned); fast local/cascade loops near disturbances and uncertain blocks; damp disturbances (buffers); reduce delays; add measured-disturbance feedforward (delay in the d→y path HELPS feedforward).

## P11. Cascade for speed, uncertainty, and linearity
Inner loop on extra measurement y₂ when: (a) big disturbance + NMP outer block, (b) uncertain/nonlinear inner block (fast loop hides it), (c) phase-lag-limited bandwidth (inner loop cuts effective phase). Extra input with limited power/duty → input resetting (valve position control). Tune inner-first.

## P12. Reduce models for control with residualization
Balanced residualization: exact DC match, 2×tail HSV bound, best in the control band. Never reduce away delays, RHP zeros, integrating modes. Unstable plants: reduce stable part or normalized coprime factors. Reduce controllers as [K₁W_iK₂] blocks; residualize, don't truncate+rescale.

## P13. Disturbances belong in the plant
Model measured/known disturbances as extra inputs with G_d into the generalized plant (helicopter gusts: B_d = columns of A; weight W4). Same controller order, large rejection gains. Feedforward handles what feedback bandwidth can't.

## P14. Verify with the closed-loop scoreboard
Final analysis = σ̄(S), σ̄(T), σ̄(T_I), σ̄(KS) plots vs weights + time-domain sims on the nonlinear model. M_s ≤ ~2, small T/T_I peaks, actuator limits respected. μ peak < 1 with margin. If any fail, the failure localizes to a pattern above — go back, not sideways.

## Anti-pattern index
- Tuning on an uncontrollable I/O pair (violates P2)
- Decoupling a large-RGA plant (violates P4)
- Canceling MIMO pole-zero pairs without direction check (violates P5)
- Complex-Δ claims for real parametric problems without acknowledging conservatism (P6/P7)
- Forgetting NS check with μ (P7)
- Over-shaping past the coprime stability radius (P8)
- Pairing by largest |g_ij| alone (P9)
- Truncating controllers then rescaling prefilters (P12)
- Trusting idealized models' frequency-independent conditioning (P12/P14 — distillation 5-state vs 2×2 idealization)
