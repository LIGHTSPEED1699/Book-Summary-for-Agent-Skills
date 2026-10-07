# Chapter 4: Stochastic and Predictive Self-Tuning

## Core Idea
Replace pole placement with variance minimization and the STR becomes the stochastic-optimal family: minimum-variance control (the discrete-time LQG regulator, computable by one polynomial division), its self-tuning version, LQ self-tuners, and receding-horizon predictive control — all the same two-loop STR skeleton with a different underlying design problem.

## Frameworks Introduced
- **Minimum-variance control (4.2)**: model A₁(q)y(t) = B₁(q)u(t−d) + C(q)e(t) (e white); **polynomial identity C = A F + q^{−d} G** (unique solution with deg G < d); optimal regulator **B₁F u(t) + G y(t) = 0**; achieved output variance = var of filtered noise F(q)e(t) (the floor); nonminimum-phase zeros of B₁ become closed-loop poles (unavoidable). Moving-average (deadbeat) control: C = 1 case, output is a moving average of noise.
- **Adaptive minimum variance / stochastic STR (4.3)**: estimate A, B, C by RLS (ARMAX regression), solve C = ÂF̂ + q^{−d}Ĝ each sample, apply B̂F̂u + Ĝy = 0. Certainty equivalence again; self-tuning minimum variance is the discrete-time "integral of the first chapter of LQG".
- **Unification of direct STRs (4.4)**: the minimum-variance regulator identity reparameterized gives a *direct* stochastic self-tuner — estimate the controller polynomial pair directly from an auxiliary-output regression; shows deterministic direct STR (Ch 3) and stochastic direct STR are the same construction with different C.
- **Linear quadratic STR (4.5)**: criterion E[y²(t) + ρu²(t)]; solution via spectral factorization D(q)D(q⁻¹) = ρA(q)A(q⁻¹) + B(q)B(q⁻¹) (outer factor) and Diophantine G + F̃B = ρ̃... ; control law Gy + Fu = 0 (discrete LQG); ρ → 0 recovers minimum variance; self-tuner = ARMAX estimates + on-line spectral factorization. Robustness margins: LQ loop has GM = 1 (no margin!) at the input — ρ buys margins.
- **Adaptive predictive control (4.6)**: receding-horizon family on CARIM model A(q⁻¹)y = q^{−d}B(q⁻¹)u + C(q⁻¹)e/Δ (Δ = difference operator):
  - **One-step (d-step-ahead) control**: drive ŷ(t+d) to reference; **minimum control effort** variant minimizes Σu² subject to hitting the target — closed-loop poles → zeros of q^{d−1}A(q) as d grows; long horizons slow unstable/slow systems (Example 4.9/4.10: horizon 5-10 samples typically sufficient).
  - **Generalized predictive control (GPC, Clarke)**: cost J = Σ_{j=N1}^{N2} [y(t+j) − y_m(t+j)]² + ρ Σ_{j=1}^{Nu} [Δu(t+j−1)]²; Diophantine C = AF_j + q^{−j}G_j per step; solve for Δu sequence, apply first element (receding horizon); N1/N2/Nu/ρ are the tuning knobs; integrating C(1) factor gives offset-free tracking; adaptive GPC = STR wrapper (estimate, recompute G_j/F_j).
- **Prediction horizon vs stability**: long horizons with minimum-effort assumptions can produce slow/unstable closed loops; GPC's control weighting ρ restores stability margins.

## Key Concepts
- **Polynomial (Diophantine) division C = AF + q^{−d}G**: the computational core of minimum variance and GPC predictions.
- **Variance floor**: min achievable output variance = σ²‖F‖² — set by noise model C and delay d; a benchmark for any controller.
- **Receding horizon**: optimize over a window, apply the first move, re-plan every sample.
- **CARIM/CARMA models**: controlled autoregressive integrated moving average — the GPC model class with Δ for offset-free behavior.
- **Spectral factorization**: the LQ design step (D outer factor) — replaces pole placement in LQ STR.
- **Implicit GPC**: reparameterization eliminating the F/G solves (direct STR flavor for GPC).

## Mental Models
- "Minimum variance is the yardstick": whatever you build, compare its output variance to the F-filtered-noise floor — the gap is your design/estimation loss.
- "The underlying design problem of STR variants": pole placement (Ch 3) → minimum variance (4.3) → LQ (4.5) → receding horizon (4.6); the estimation loop never changes.
- "ρ is the stability purchase": ρ = 0 minimum variance/LQ has zero gain margin at the input; any control weighting buys robustness.
- "Horizon length is a robustness knob, not just a performance knob": long horizons + cheap control = slow unstable modes.

## Anti-patterns
- **Minimum-variance control of nonminimum-phase plants without understanding**: B₁ zeros land on closed-loop poles; ringing guaranteed; use GMV/LQ instead.
- **ρ = 0 LQ STR**: GM = 1 — the loop is on the stability edge with model error.
- **Very long GPC horizons with tiny ρ on integrating/unstable plants**: closed-loop poles crawl toward unstable locations (Example 4.9 analysis).
- **Estimating C(q) without excitation and expecting variance floors**: C is only identifiable under excitation; frozen Ĉ silently degrades the design.

## Reference Tables

### Underlying design problem by STR variant
| STR variant | Design step | Key equation |
|---|---|---|
| Deterministic (Ch 3) | pole placement | AR + BS = A_cA_o |
| Minimum variance (4.3) | variance minimization | C = AF + q^{−d}G; B̂Fu + Ĝy = 0 |
| LQ (4.5) | spectral factorization | DD̃ = ρÃÃ + BB̃; Gy + Fu = 0 |
| GPC (4.6) | receding horizon | C = AF_j + q^{−j}G_j; cost with N1,N2,Nu,ρ |

### GPC knobs
| Knob | Effect |
|---|---|
| N1 | dead-zone in horizon (avoid over-aggressive near-term moves) |
| N2 | prediction horizon; longer = more preview, slower modes |
| Nu | control horizon; moves after Nu frozen |
| ρ | control effort weight; robustness/stability dial |

## Key Takeaways
1. Minimum-variance control is one polynomial division away and defines the performance floor (F-filtered noise variance) every adaptive design should be judged against.
2. Nonminimum-phase zeros are not designable away — they become closed-loop poles in any minimum-variance solution.
3. LQ STR adds ρ and spectral factorization; ρ = 0 means zero gain margin — always pay for margins.
4. Predictive/GPC control is the same STR skeleton with receding-horizon optimization; horizons and ρ set both performance and stability character.
5. Direct/indirect duality (4.4) unifies the families: reparameterize by the design identity and the design block vanishes.

## Connects To
- **Ch 3**: same STR skeleton, deterministic design problem.
- **Ch 7**: stochastic theory justifying certainty equivalence here.
- **Ch 11**: numerics — solving the polynomial equations robustly on-line.
- **Ch 12**: GPC self-tuners in industrial products.
