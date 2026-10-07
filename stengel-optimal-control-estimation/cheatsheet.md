# Cheatsheet — Optimal Control and Estimation (Stengel, 1994)

## Core algorithms

### Deterministic trajectory optimization (Ch 3)
```
J = Φ(x(t_f),t_f) + ∫ Ψ(x,u,t) dt,  ẋ = f(x,u,t)
H = Ψ + λᵀf
ẋ = ∂H/∂λ        (state)
λ̇ = −∂H/∂x       (costate)
∂H/∂u = 0        (or u minimizes H if bounded)
λ(t_f) = ∂Φ/∂x   (transversality)
```
Singular arc: ∂H/∂u ≡ 0 → generalized Legendre-Clebsch (−1)^k d^{2k}/dt^{2k}(∂H/∂u) ≥ 0.

### Neighboring-optimal feedback (Ch 3.7)
```
δu = −S(t) δx,  Ṡ = −SF − FᵀS + SG R⁻¹GᵀS − Q,  S(t_f) = terminal weights
```

### Discrete Kalman filter (Ch 4.3)
```
predict:  x̂⁻ = Φ x̂ + Γ u,   P⁻ = Φ P Φᵀ + Γ Q_c Γᵀ
update:   ν = z − H x̂⁻,     K = P⁻Hᵀ(H P⁻Hᵀ + R)⁻¹
          x̂ = x̂⁻ + K ν,     P = (I − K H) P⁻
```

### Kalman-Bucy (Ch 4.5)
```
ẋ̂ = F x̂ + G u + K(z − H x̂),  K = P Hᵀ R⁻¹
Ṗ = F P + P Fᵀ + G Q_c Gᵀ − P Hᵀ R⁻¹ H P
```

### LQR (Ch 6)
```
u = −C x,  C = R⁻¹ Gᵀ S
0 = FᵀS + S F − S G R⁻¹ Gᵀ S + Q      (ARE)
S = Y X⁻¹ from stable invariant subspace [X; Y] of
H = [[F, −G R⁻¹ Gᵀ], [−Q, −Fᵀ]]
```

### LQG = CE (Ch 5.3)
```
u = −C x̂   (Kalman-Bucy estimate + LQR gain; design separately)
E[J] = J_control + trace-terms(estimation error)
closed-loop modes = {regulator modes} ∪ {estimator modes}
```

### Command response (Ch 6.2)
```
0 = F x̄ + G ū (+ L w̄);  ȳ = H x̄ + L ū     (equilibrium pair)
u = ū − C(x − x̄) (+ command prefilter)
```

## Key formulas & guarantees
| Item | Value |
|---|---|
| SISO LQR margins | GM ∈ [½, ∞), PM ≥ 60° |
| Discrete transition | Φ = e^{Fh}, Γ = ∫₀^h e^{Fτ}dτ · G |
| z-plane mapping | z = e^{sT} |
| Weighted norm | ‖x‖²_Q = xᵀQx |
| Lagrange stationarity | ∇J + λᵀ∇f = 0 |
| Costate = value gradient | λ = ∇_x S (HJB) |

## Failure-mode quick table
| Symptom | Cause | Fix |
|---|---|---|
| Offset under constant disturbance | no integral state | augment + re-solve ARE |
| Filter divergence | overconfident P / bad EKF init | inflate Q,R; better init |
| LQG fragile | margins lost through filter | LTR |
| Wrong control structure (bang-bang) | missed singular arc | gen. Legendre-Clebsch |
| "Optimal" but odd shape | parametric shape bounds | TPBVP methods |
| Parameter drift in adaptive filter | weak excitation | excite / multiple-model |
| Probing "needed" in linear known plant | neutral system | drop probing |

## Design rules of thumb
- Weights are the spec: set R from available control authority, Q from acceptable deviations; iterate on margins.
- Keep estimator modes faster than regulator modes, but not so fast they amplify noise/unmodeled dynamics.
- Check margins on the *implemented* loop (with filter, with sampling), not the design loop.
- Augmentation beats hand-crafted compensators: one Riccati, consistent gains.
- Certainty equivalence is an LQG privilege — justify it or expect coupling.
- Sample fast: 10-20+ samples per dominant closed-loop period; model computational delay.

## Chapter index
1 framework/variables | 2 math toolkit | 3 trajectories + neighboring-optimal | 4 Kalman family + adaptive filters | 5 stochastic control + LQG separation | 6 ARE design, structures, margins, recovery | 7 epilogue (pose the problem right)
