# Glossary — Multivariable Feedback Control (Skogestad & Postlethwaite, 2nd ed. 2005)

## Scaling & signals
- **Scaled variable**: x_scaled = x_physical / x_expected; all gains, weights, and rules below assume scaled variables.
- **Self-regulating output**: disturbance-free output settles to new steady state after input step (vs integrating: level, temperature batch).
- **ω_d**: frequency where |G_d| first crosses 1 — disturbance content edge. **ω_c**: gain crossover of loop L. **ω_u**: ultimate frequency (∠L = −180°). **ω_B**: closed-loop bandwidth (|S| = 1/√2 crossing).

## Plant structure
- **Pole polynomial**: least common denominator of all nonzero minors of all orders of G(s) (Thm 4.8) = poles of minimal realization.
- **MIMO zero**: s = z with rank G(z) < normal rank; has input direction u_z (G u_z = 0) and output direction y_z (y_zᴴG = 0).
- **Normal rank**: rank of G(s) for almost all s.
- **Pinned zero**: RHP zero whose output direction is tied to one output — can't be removed by adding unrelated inputs.
- **Functional controllability**: rank G = number of outputs (independent steady-state control authority).

## Gains & directions
- **σ̄(G(jω)) / σ̲(G(jω))**: max/min singular values — best/worst gain over input directions.
- **γ(G) = κ(G) = σ̄/σ̲**: condition number; large ⇒ direction matters more than magnitude.
- **Minimized condition number κ_O(G)**: min over diagonal output scalings — intrinsic ill-conditioning.
- **RGA Λ(G)**: (G⁻¹)ᵀ ⊙ G; scale-invariant interaction/pairing measure; rows/cols sum to 1.
- **RGA-number**: ‖Λ − I‖ (any induced norm) — pairing quality at a frequency.
- **PRGA Γ**: G ⊙ diag(G⁻¹) — performance RGA for diagonal control; scaling-dependent; sees one-way interaction.
- **CLDG**: closed-loop disturbance gain — disturbance effect on output i with all other loops perfectly closed.
- **QRGA / CLDG / PRGA family**: decentralized-control analysis arrays (Ch 10).

## Closed-loop transfer functions
- **S = (I + GK)⁻¹** sensitivity; **T = GK(I+GK)⁻¹ = I − S** complementary sensitivity.
- **T_I = GK(I + GK)⁻¹ at input break** (for input uncertainty); **KS = S K** (control energy / additive uncertainty).
- **M_s = ‖S‖∞, M_t = ‖T‖∞**: sensitivity/complementary peaks; GM ≥ M_s/(M_s−1), PM ≥ 180° − 2 arcsin(1/(2M_t))... (SISO margins vs M_s).

## Uncertainty
- **w_I, w_O, w_A, w_iI**: multiplicative input/output, additive, inverse-multiplicative uncertainty weights; ‖Δ‖∞ ≤ 1.
- **Relative (multiplicative) uncertainty**: G_p = G(I + w_I Δ) — channel gain/dynamics errors.
- **Diagonal input uncertainty**: E_I = diag(ε_i), always present (~20% in process plants); RGA governs its damage.
- **Coprime uncertainty**: G_p = (M + Δ_M)⁻¹(N + Δ_N) with normalized left coprime M⁻¹N; stability radius α_max = 1/γ_opt.
- **Structured vs unstructured Δ**: block-diagonal (channel-wise, real) vs full complex matrix.

## Analysis tools
- **μ_Δ(M)** structured singular value: 1/min{σ̄(Δ): det(I−MΔ)=0}; exact RS test for structured Δ; μ(full) = σ̄, μ(δI) = ρ.
- **D-scaling**: μ ≤ min_D sup_ω σ̄(DMD⁻¹), D block-diagonal positive; exact for ≤2 blocks.
- **Skewed μ (μ_s)**: one uncertainty block varied, others fixed — "how much can THIS error grow".
- **N-Δ / M-Δ form**: standard interconnection; RS ⇔ μ(N₁₁) < 1; RP ⇔ μ(N with full Δ_P block) < 1.
- **LFT F_u/F_l**: linear fractional transformations — bookkeeping for pulled-out blocks.
- **Hankel singular values σ_i(PQ)^½**: state energy ranking; balanced realization P = Q = diag(σ_i).
- **H2 / H∞ / Hankel norms**: impulse-energy / worst-sinusoid / past-to-future energy system norms.

## Design & synthesis
- **Controllability rules (Ch 5)**: 8 bandwidth inequalities for SISO I/O feasibility.
- **Controllability procedure (Ch 6)**: 14-step MIMO plant-only analysis.
- **DIC**: decentralized integral controllability — stable under independent detuning of each integral loop; negative steady-state RGA element ⇒ not DIC.
- **Integrity**: stability as loops enter/leave service.
- **LTR**: loop transfer recovery (LQG); **stability radius**: coprime robustness margin.
- **D-K iteration**: μ-synthesis via alternating H∞ solves and D-scaling updates.
- **H∞ loop shaping (McFarlane-Glover)**: shape with W1/W2, robustly stabilize normalized coprime factors, K = W1 K_s W2.
- **2-DOF**: separate feedback K_y and prefilter; resolves tracking vs rejection conflict.
- **Cascade / input resetting (valve position control)**: extra measurements / extra inputs via SISO subcontrollers.
- **Partial control**: leave self-regulating outputs open-loop when full control is infeasible.

## 2nd-edition additions
- **SIMC (Simple Model Control)**: Skogestad's IMC-derived tuning — one knob τ_c (closed-loop time constant, τ_c ≥ θ); PI/PID/integrating formulas in cheatsheet.
- **Half rule**: when collapsing higher-order dynamics, split each neglected time constant: half to effective delay θ, half to dominant τ₁. θ_eff = θ + Στ_neg/2.
- **Effective delay θ**: the single number that limits achievable bandwidth; compute via half rule, then ω_c ≲ 1/θ.
- **Self-optimizing control**: acceptable loss with constant controlled-variable setpoints under disturbances (Skogestad 2000); kills the on-line optimization layer for that variable.
- **Loss L**: L(u,d) = J(u,d) − J_opt(d) ≥ 0 — currency of variable-selection decisions.
- **LMI (linear matrix inequality)**: affine Hermitian F(x) ≺ 0; convex feasibility; backend for stability/H∞/μ-bound/multi-objective synthesis (ch12).
- **BMI**: bilinear matrix inequality — appears when controller × Lyapunov variables; nonconvex, needs variable change or iteration.
- **Youla/Q parametrization**: all stabilizing controllers from one K₀ + free stable Q; keeps synthesis convex.
- **Pole polynomial**: (see Plant structure) — 2e ch4 consolidates its computation via minors.
- **Lower gain margin**: GM measured at the −180° crossing from below; binding for integrating/NMP loops (2e ch2).

## Benchmarks & examples in the book
- **Satellite example**: flexible satellite, γ(G) ≈ 500 — per-channel margins fine, simultaneous errors fatal (μ).
- **Distillation column A**: 40-tray equimolar binary, α = 1.5, 99% purities; LV config; κ = 141.7, λ₁₁ = 35.1; CDC benchmark (20% gain + 1 min delay per channel).
- **Aero-engine (Rolls-Royce Spey)**: 15/18-state, 3 inputs (WFE, AJ, IGV); Set 5 outputs (OPR1, LPEMN, NH); 2-DOF loop shaping, γ = 2.9.
- **Helicopter (Westland Lynx / RHM)**: 8-state hover model, S/KS + gust-as-disturbance H∞ design.
