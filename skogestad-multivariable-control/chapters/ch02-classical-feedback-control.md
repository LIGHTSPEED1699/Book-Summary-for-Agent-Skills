# Chapter 2: Classical Feedback Control (2e; the SISO toolkit + SIMC)

## Core Idea
SISO loop shaping is not superseded by the multivariable chapters — it is their foundation: |S| and |T| tradeoffs, margins as sensitivity peaks, bandwidth limited by delay, and a one-knob tuning rule (SIMC) that turns a model into a robust PID.

## Frameworks Introduced
- **Performance bounds via sensitivity**: |S| < 1/|w_P| (disturbance rejection), |T| < 1/|w_I| (noise attenuation); M_s = ‖S‖∞ ≈ 2 and M_t = ‖T‖∞ ≈ 1.4 as design targets.
  - Use when: translating "reject A% of d up to ω_B" into a shaping spec.
- **Margins ↔ peaks**: GM ≥ M_s/(M_s−1), PM from M_t; 2e adds the **lower gain margin** — for integrating/NMP loops the crossing from below at −180° also binds.
- **Feedback amplifier view**: the loop makes the plant look like G/(1+L) where you want it and like G where L is small — unstable plants can be stabilized by feedback (2e: explicit unstable-plant treatment).
- **SIMC tuning** (Skogestad IMC-based, the book's default PID recipe):
  - Fit scaled model k, τ₁(, τ₂), θ.
  - PI: K_c = 1/(k(τ_c+θ)), τ_I = min(τ₁, 4(τ_c+θ)).
  - PID (2nd-order model): τ_c = max(θ, τ₂/3); K_c = (τ₁+τ₂)/(kτ_c), τ_I = τ₁, τ_D = τ₂/(1+τ₁/τ_c), derivative on measurement.
  - Integrating: K_c = 1/(k(τ_c+θ)), τ_I = 4(τ_c+θ).
  - τ_c = θ default; raise τ_c for robustness, lower for speed — one dial, predictable.
- **Half rule**: collapse higher-order lags by giving half of each neglected τ to θ and half to τ₁: θ_eff = θ + Στ_neg/2. First-order model ⇒ PI; second-order ⇒ PID. PI's performance floor is set by τ₂/2.

## Key Concepts
- **Effective delay θ**: the control-limiting parameter; compute via half rule, then ω_c ≲ 1/θ.
- **Bandwidth-delay trade**: ω_Bθ ≲ 0.5–1 for sane response.
- **Shaping closed-loop T directly**: choose desired T (e.g., 1/(τ_c s+1)·e^{-θs}-like), back out K — the IMC view.

## Mental Models
- τ_c in SIMC is a robustness budget dial, not a "tuning constant": τ_c = θ is the aggressive-but-safe default; τ_c > θ trades speed for margin.
- Every neglected time constant is secretly delay — the half rule just admits it.

## Anti-patterns
- **Ziegler-Nichols as default**: ch2's own example — ZN gain 1.13 fails RS at 33% plant error; SIMC K = 0.31 passes. ZN ignores the model's delay content.
- **Tuning without scaling**: SIMC formulas assume scaled variables (u, y ~ ±1 normal range).
- **Differentiating the setpoint**: derivative on measurement only, or kick.

## Worked Example
Process G = 3(−0.8s+1)/((6s+1)(2.5s+1)(0.4s+1)) (2e Example 2.16-style): half rule → first-order+delay k=3, τ₁ = 6+2.5/2 = 7.25, θ = 0.4+2.5/2+... ≈ 3.65–6.15 depending on order kept. PI from 1st-order (τ_c = θ): K_c = 1/(k(τ_c+θ)), τ_I = min(τ₁, 4(τ_c+θ)). Keep second lag → PID with τ_c = max(θ, τ₂/3). PI floor = τ₂/2; PID recovers it.

## Key Takeaways
1. SIMC: identify k, τ's, θ (half rule) → one knob τ_c → PID. Robust by construction.
2. Delay is king: ω_c ≲ 1/θ; everything else is negotiation.
3. Check lower gain margin for integrating/NMP loops.
4. Feedback amplifier: L reshapes what the plant "looks like" — that's both the power and the fragility.

## Connects To
- **Ch 5**: why ω_c can't escape the delay/NMP window SIMC lives in.
- **Ch 7**: ‖w_I T‖∞ check on the SIMC loop.
- **Ch 9**: SIMC as the classical baseline the H∞ designs are compared against.
