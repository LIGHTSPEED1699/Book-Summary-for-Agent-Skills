# Glossary — Adaptive Control (Åström & Wittenmark, 1st ed.)

## Models & notation
- **p = d/dt, q = forward shift**: continuous/discrete operators; G(p)w(t), H(q)u(t) notation (zero initial conditions assumed).
- **A(q), B(q), C(q)**: monic A polynomial (process dynamics), B (input dynamics, may be delayed q^{-d}), C (noise/disturbance dynamics) — ARMAX structure A(q)y = B(q)u + C(q)e.
- **CARIM**: controlled autoregressive integrated moving average (GPC model with Δ = 1 − q^{-1}).
- **θ / φ(t)**: parameter vector / regression vector; y(t) = φᵀ(t)θ + e(t).
- **Relative degree d₀ = deg A − deg B**; **d**: pure delay in steps.
- **Underlying design problem**: the design performed as if parameters were known — reveals what an adaptive scheme converges to.

## Estimation
- **RLS (covariance form)**: recursive least squares with covariance R(t); forgetting factor λ ∈ (0,1].
- **Projection algorithm / stochastic approximation**: normalized-gradient and LMS-like (γ(t) → 0) estimators.
- **Persistent excitation (PE)**: average of φφᵀ positive definite — necessary for parameter convergence.
- **Equation error vs output error methods**: ARX LS (unbiased only if noise enters the difference equation) vs prediction-error/output-error (unbiased under output noise).
- **Covariance wind-up**: P growth under λ < 1 without excitation, then parameter jumps.
- **Directional forgetting / constant trace / leakage (σ-mod)**: wind-up cures.
- **Square-root algorithms**: Cholesky/UDUᵀ/QR covariance propagation preserving symmetry/PD.
- **Dead zone / conditional updating / projection**: outlier and safety guards; θ̂ constrained to compact D.

## STR & design
- **STR (self-tuning regulator)**: estimation + on-line design (indirect) or reparameterized direct variant; certainty equivalence.
- **Diophantine equation / Bezout identity**: AR + BS = A_cA_o (pole placement); C = AF + q^{-d}G (minimum variance/prediction); solvable iff coprime; ill-conditioned near common factors.
- **A_c / A_o / A_r**: closed-loop, observer (estimation filter), reference-model polynomials.
- **Auxiliary output**: filtered signal serving as regression output in direct STR.
- **Minimum variance control**: B̂Fu + Ĝy = 0; variance floor = var(F e); nonminimum-phase zeros → closed-loop poles.
- **Spectral factorization**: DD̃ = ρÃÃ + BB̃ — LQ STR design step.
- **GPC**: generalized predictive control; horizons N1/N2/Nu, control weight ρ, receding horizon.
- **Implicit GPC / direct STR**: design-block-free reparameterizations.

## MRAS
- **MIT rule**: θ̇ = −γ e ∂e/∂θ (gradient of ½e²); sign-sign variant.
- **Sensitivity derivative ∂e/∂θ**; **adaptation gain γ**.
- **Average equation**: fast dynamics averaged → parameter-error dynamics; bounds γ.
- **Positive real (PR)**: Re W(jω) ≥ 0; the filter-design certificate for MRAS stability.
- **Hyperstability / monotone operators**: passivity-based MRAS analysis.
- **Model matching**: e = y − y_m → 0.

## Analysis & robustness
- **Certainty equivalence**: estimates used as if true; = delta-approximation of the hyperstate.
- **Hyperstate**: conditional distribution of states + parameters (dual control's state).
- **Dual control / probing**: optimal balance of control and information; myopic controllers ignore it.
- **Averaging (Krylov-Bogoliubov / ODE method)**: small-γ approximation of adaptive dynamics.
- **Turn-off phenomenon**: robustness → 0 as unmodeled dynamics speed up.
- **SOAS (self-oscillating adaptive system)**: relay-forced limit cycle ⇒ guaranteed excitation + continuous identification.
- **Describing function N(a)**: harmonic balance for relays/nonlinearities; relay N = 4d/(πa).
- **Variable structure / sliding mode**: switching feedback, sliding surface, chattering.
- **Horowitz (QFT) design**: Nichols-chart loop shaping under gain/phase templates; constant-phase (straight-line Nyquist) trick.

## Practice
- **Ultimate gain/period (K_u, T_u)**: relay-measured stability-boundary pair; K_u = 4d/(πa).
- **ZN rules**: open-loop (K,L,T) and closed-loop (K_u,T_u) tuning constants.
- **Computational delay / anti-alias filter delay τ_F**: must be in the model when > ~10% of h.
- **Mode management**: startup/estimation-only/adaptation-off/supervision modes beyond manual/auto.
- **Performance-related dials**: user interfaces labeled with bandwidth or LQ weight, not raw parameters.
