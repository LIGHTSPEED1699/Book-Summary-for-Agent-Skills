# Cheatsheet — Adaptive Control (Åström & Wittenmark, 1st ed.)

## Core algorithms

### RLS with forgetting (Ch 2)
```
θ̂(t) = θ̂(t−1) + R(t)φ(t)[y(t) − φᵀ(t)θ̂(t−1)]
R(t) = [R⁻¹(t−1)/λ + φ(t)φᵀ(t)]⁻¹        (λ ∈ (0,1], often 0.95-0.999)
```
Guards: projection θ̂ ∈ D; dead zone on innovation; conditional update; constant-trace or directional forgetting when λ < 1; UDUᵀ form in production.

### Indirect STR (Ch 3)
```
1. Estimate A(q), B(q) by RLS on y = φᵀθ + e
2. Solve Diophantine: A R + B S = A_c A_o   (A_c = desired poles, A_o = observer)
3. Apply: R u = S u_c − T y,  T = B_r B₊/(const) for model matching
```

### Minimum variance / stochastic STR (Ch 4)
```
Model: A₁y(t) = B₁u(t−d) + C e(t)
Solve: C = A F + q^{−d} G   (deg G < d)
Law:   B F u + G y = 0      variance floor = var(F e)
```

### LQ STR (Ch 4)
```
Factor: D D̃ = ρ Ã Ã + B B̃ (outer spectral factor)
Solve:  G + F̃B = ρ̃ D̃ ... ; law G y + F u = 0; ρ > 0 buys gain margin
```

### GPC (Ch 4)
```
Model (CARIM): A(q⁻¹)y = q^{−d}B(q⁻¹)u + C(q⁻¹)e/Δ
Cost: Σ_{j=N1}^{N2}(y−y_m)² + ρ Σ_{j=1}^{Nu}(Δu)²
Solve C = AF_j + q^{−j}G_j; apply first Δu, re-plan each sample
```

### Direct STR (Ch 3.5)
```
Requires minimum phase + known d₀.
Regress auxiliary output y_f on [−y(t−1)… u(t−d₀…)] → R, S directly
Law: R u = (B_r/const) u_c − S y ; guard r̂₀ ≠ 0
```

### MIT rule & Lyapunov MRAS (Ch 5)
```
MIT:      θ̇ = −γ e ∂e/∂θ          (bound γ via average equation)
Lyapunov: V = e² + φᵀΓ⁻¹φ → θ̇ = −Γ e ε; choose filter Q so W(s) PR
```

### Relay auto-tuning (Ch 8)
```
Relay ±d → limit cycle amplitude a, period T_u
K_u = 4d/(πa), ω_u = 2π/T_u
ZN: PID = 0.6K_u, T_i = 0.5T_u, T_d = 0.125T_u (PI: 0.45K_u, 0.83T_u)
```

## Key formulas
| Quantity | Formula |
|---|---|
| Diophantine (pole place) | AR + BS = A_cA_o |
| Min-variance identity | C = AF + q^{−d}G |
| Variance floor | E[(Fe)²] |
| LQ factorization | DD̃ = ρÃÃ + BB̃ |
| Relay DF | N(a) = 4d/(πa) |
| Ultimate gain | K_u = 4d/(πa) |
| ZN open-loop PID | 1.2T/(aL), T_i = 2L, T_d = 0.5L |
| Sampling rule | h ≤ (π/10–20)/ω_n (12-60 samples/period) |
| Comp. delay ignore limit | < ~10% of h |

## Failure-mode quick table
| Symptom | Cause | Fix |
|---|---|---|
| Jump after quiet | covariance wind-up | constant trace / directional forgetting |
| Chaos at high γ | bifurcation | average analysis, lower γ |
| Bias, stable | noise-regressor correlation | output-error model / whitening |
| Blow-up | Diophantine near-singular, r̂₀→0 | conditioning check, projection |
| Drift when quiet | PE lost (integral action starves ID) | dither, excitation schedule |
| Fails with fast unmodeled dynamics | turn-off phenomenon | normalize/filter φ, dead zone, σ-mod |
| Worse than PID | no pre-tune | relay auto-tune first |

## Design rules of thumb
- Find the underlying design problem before touching the adaptation law.
- λ < 1 always pairs with an excitation guard.
- ρ = 0 (min variance/LQ) ⇒ GM = 1: always pay for margins.
- Direct STR only if minimum phase + known relative degree.
- Schedule coarse, adapt fine; robust fixed loop first if range known (abuse test).
- Adaptation gain γ: derive the bound, don't tune it by feel.
- Modes: startup fixed, estimation-only, supervision alarms — never "always adaptive".

## Chapter index
1 five schemes | 2 recursive estimation | 3 deterministic STR | 4 stochastic/predictive STR | 5 MRAS/MIT/Lyapunov | 6 nonlinear dynamics & averaging | 7 dual control | 8 auto-tuning | 9 gain scheduling | 10 robust & self-oscillating | 11 implementation | 12 products | 13 perspectives
