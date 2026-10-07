# Chapter 3: Deterministic Self-Tuning Regulators

## Core Idea
An indirect self-tuner is just "identify ARX, solve the Diophantine equation, apply the regulator" every sample — and the Diophantine identity, used as an operator identity on y(t), reparameterizes the plant in controller parameters so the design step can be eliminated entirely (direct STR), at the cost of requiring minimum phase and known relative degree.

## Frameworks Introduced
- **Regulator with known parameters (pole placement)**: process A(q⁻¹)y(t) = B(q⁻¹)u(t); controller R(q⁻¹)u(t) = S(q⁻¹)u_c(t) − T(q⁻¹)y(t) (usually T = R). Closed-loop characteristic polynomial from **Diophantine equation (Bezout identity)**: A R + B S = A_c A_o, solvable iff A, B coprime; poorly conditioned when A and B have nearly common factors (near pole-zero cancellation). A_o = observer polynomial (filters estimates, doesn't affect regulation); A_c = desired closed-loop poles; T set by model matching: T = B_r B_+ / (leading const) with B = B₊B₋ (stable/unstable or min/max phase split) to get reference model B_r/A_c.
- **Indirect STR (Algorithm 3.2)**: Step 1 estimate A, B by RLS (regression vector φ(t) = [−y(t−1)... −y(t−n) u(t−1)... u(t−m)]ᵀ); Step 2 solve AR + BS = A_cA_o for R̂, Ŝ; Step 3 apply Ru = Su_c − Ty. Certainty equivalence.
- **Continuous-time self-tuners (3.4)**: same via filtered-signal regression (Ch 2) + Diophantine in p; derivative-operator pitfalls; sampling: STR works when sampling is fast relative to closed-loop dynamics; slow sampling degrades via zeros introduced by sampling (B(z) zeros from ZOH — can be nonminimum phase for systems with relative degree ≥ 2 and slow sampling).
- **Direct STR (3.5, Algorithm 3.3)**: run the Diophantine identity on y(t): A_c(q⁻¹)y(t) = B̃(q⁻¹)[Bu? ...] → model y_f = φ_Dᵀθ_D with auxiliary output y_f = A_cA_o(q⁻¹)... (filtered reference/output), regressor [−y(t−1)... u(t−d...)] containing controller parameters directly; RLS gives R, S with no design solve. Requires: **minimum phase** (all process zeros canceled, B₋ = b₀ constant) and **known relative degree d₀**; guard r₀ = b₀ ≠ 0 (estimate can hit zero → noncausal control law — protection needed).
- **Hybrid algorithms**: estimate some process params, some controller params (e.g., estimate delay's B̂ but solve RS) — interpolate direct/indirect.
- **Disturbances with known characteristics (3.6)**: measurable disturbance → feedforward (predict disturbance effect d̂ = G_d u_d, cancel via extra term in regulator: Ru = Su_c − Ty + S_d u_d^pred); load disturbances modeled as filtered white noise → integral action: choose A(1) factor / set A_c(1) = A(1) so regulator has integral action ⇒ zero offset for step-like disturbances; generalized minimum variance (GMV) with polynomial C(q⁻¹) on the noise.
- **Prediction/preview**: STR with command signal prefiltering (model matching B_r/A_c) gives setpoint response independent of estimation.

## Key Concepts
- **Diophantine equation**: AR + BS = A_cA_o — the algebraic heart of pole placement; ill-conditioned near common factors.
- **Observer polynomial A_o**: low-pass on the estimation side; slows parameter updates, filters noise; doesn't change regulation poles.
- **Certainty equivalence**: estimated parameters plugged into the design as if true.
- **Auxiliary output**: filtered combination y_f used as the "output" in direct STR regression.
- **Relative degree d₀**: must be known for direct STR; r₀ = b₀ ≠ 0 causality guard.
- **Integral action via A_c(1) = A(1)**: pole placement at z = 1 built into the Diophantine spec.
- **Sampling-rate effect**: fast sampling + relative degree ≥ 2 ⇒ ZOH zeros near z = 1 (nonminimum phase) — STR cancels them (dangerous if RHP).

## Mental Models
- "STR = automating the identification-and-retuning meeting every sample"; the underlying design problem is plain pole placement.
- "Direct vs indirect is a choice of coordinates": same closed loop, different parameterization; direct saves the Diophantine solve but inherits minimum-phase + known-delay assumptions.
- "A_o is your noise budget knob": heavier filtering = smoother parameters, slower adaptation.
- "Disturbance rejection = put a unit pole in A_c at z = 1 (integral action) or predict and cancel if measurable."

## Anti-patterns
- **Canceling RHP/slow sampling zeros with STR** (direct STR assumes cancellation): minimum-phase requirement is not cosmetic.
- **Ignoring Diophantine conditioning**: near pole-zero cancellation in the plant ⇒ wild R, S even with perfect estimates.
- **Letting r̂₀ → 0 in direct STR**: noncausal/infinite gain control law — clamp or protect.
- **Adapting every sample with a noisy estimate and no A_o**: parameter chatter propagates straight into the control signal.

## Reference Tables

### Indirect vs direct STR
| Aspect | Indirect | Direct |
|---|---|---|
| Estimates | process A, B | controller R, S |
| Design solve | Diophantine each sample | none |
| Needs | coprime A,B | minimum phase, known d₀ |
| Conditioning | Diophantine ill-conditioning possible | avoids it |
| Noise amplification | moderate | A_cA_o filtering can amplify — use filtered form (3.27) |

### Disturbance handling
| Disturbance type | STR mechanism |
|---|---|
| Measurable | feedforward term from predicted effect |
| Step/load (unmeasurable) | integral action: A_c(1) = A(1) |
| Colored noise | GMV with C(q⁻¹), LQG-flavored (Ch 4) |

## Key Takeaways
1. The STR loop = RLS + Diophantine + regulator, repeated every sample; its ideal behavior is exactly the pole placement you specified.
2. The Diophantine equation used as an operator identity yields direct STR — design block disappears, but minimum phase + known relative degree become the price.
3. A_o (observer polynomial) is the practical knob for noise vs adaptation speed.
4. Integral action is a design choice inside the pole placement spec, not a separate PID feature.
5. Sampling zeros from ZOH can be nonminimum phase — STR's zero cancellation is then a liability, not a feature.

## Connects To
- **Ch 2**: RLS supplies the estimates.
- **Ch 4**: stochastic/predictive versions replace pole placement with variance minimization.
- **Ch 5**: the same reparameterization links STR and MRAS.
- **Ch 11**: numerics of solving Diophantine equations in real time.
- **Ch 6**: convergence of the combined estimation+control loop.
