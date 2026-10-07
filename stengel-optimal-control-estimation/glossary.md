# Glossary — Optimal Control and Estimation (Stengel, 1994)

## Variables & models
- **p, u, w, x, y, η, z**: parameters, controllable inputs, disturbances, states, outputs, measurement errors, observations (z = y + η) — the seven-family taxonomy.
- **F, G, H, L**: state-space matrices (ẋ = Fx + Gu + Lw; y = Hx + …); Jacobians when linearized.
- **Φ (transition matrix)**: Φ̇ = FΦ, Φ(t,t) = I; LTI: e^{F(t−t₀)}; discrete Φ = e^{Fh}.
- **Mode of motion**: eigenvalue/eigenvector pair's natural behavior (decay −1/Re λ, frequency Im λ).
- **Open-loop equilibrium (x̄, ū)**: steady state satisfying the dynamics for a setpoint; regulation happens around it.
- **Quasistatic equilibrium**: slowly moving equilibrium used for trajectory design.

## Optimization
- **Cost function J = Φ(x(t_f),t_f) + ∫Ψ dt**: Mayer (terminal), Lagrange (integral), Bolza (both).
- **Hamiltonian H = Ψ + λᵀf**; **costate λ** (shadow price of state; λ = ∇_x S in HJB).
- **TPBVP**: two-point boundary value problem (state forward, costate backward).
- **Transversality**: terminal costate condition λ(t_f) = ∂Φ/∂x (+ constraint multipliers).
- **Minimum Principle**: bounded-optimal u minimizes H; **switching function** ∂H/∂u.
- **Legendre-Clebsch** ∂²H/∂u² ≥ 0; **generalized** version for **singular arcs**.
- **HJB / dynamic programming**: value function S; u° = argmin H.
- **Neighboring-optimal**: linearized feedback about a nominal extremal via Riccati gain S(t).
- **Quasilinearization**: Newton iteration on the TPBVP.

## Estimation
- **x̂, P**: state estimate and error covariance (P = E[(x−x̂)(x−x̂)ᵀ]).
- **Innovation**: z − Hx̂⁻; white when model consistent.
- **Kalman gain**: K = P⁻Hᵀ(HP⁻Hᵀ + R)⁻¹ (discrete); K = PHᵀR⁻¹ (continuous).
- **Predictor / filter**: pre- vs post-update estimate.
- **Kalman-Bucy**: continuous-time filter; **duality** with LQR (F↔Fᵀ, G↔Hᵀ, Q↔R, Riccati time direction).
- **EKF / quasilinear filter**: Jacobian-along-estimate / linearized-measurement nonlinear filters.
- **Adaptive filters**: parameter-adaptive (state-augmented EKF), noise-adaptive (Q,R from innovation statistics), multiple-model (filter bank + Bayes weights).
- **Information set / derived information set**: data history vs (x̂, P) sufficient statistics.

## Stochastic control
- **Certainty equivalence / separation (LQG)**: u = −Cx̂ with C from deterministic LQ; cost = control term + estimation trace term.
- **Dual control / probing**: control that buys information; pays only for nonlinear/parameter-uncertain systems; **neutral systems** gain nothing.
- **Hyperstate**: full conditional density as state (general stochastic control).
- **Hedging**: estimator suppresses likely-noise deviations before the gain sees them.

## Design & robustness (Ch 6)
- **ARE**: algebraic Riccati equation FᵀS + SF − SG R⁻¹GᵀS + Q = 0; solvers: Hamiltonian eigenvectors (MacFarlane-Potter), Kalman-Englar, Kleinman (iterative), doubling.
- **Hamiltonian matrix**: [[F, −GR⁻¹Gᵀ],[−Q, −Fᵀ]]; stable invariant subspace → S.
- **Return difference**: I + L(s), L = loop transfer; its minimum singular value bounds margins.
- **Guaranteed LQR margins**: GM ∈ [½, ∞), PM ≥ 60° (SISO; multivariable at input under conditions).
- **LTR / robustness recovery**: shape estimator so the compensator loop regains LQR margins.
- **Augmentation structures**: integral state → PI; filter states → PIF; reference model → explicit model following; output weighting → implicit model following.
- **Stabilizable / detectable**: uncontrollable/unobservable parts stable.
- **Probability of instability**: stochastic robustness measure under random parameter uncertainty.
