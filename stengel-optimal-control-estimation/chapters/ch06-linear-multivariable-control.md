# Chapter 6: Linear Multivariable Control

## Core Idea
Specialize everything to LTI systems: solve the algebraic Riccati equation once (Hamiltonian eigenvectors), shape the design through cost-function structure (integral/augmented states give PI, model following), inspect the resulting modes — and then audit what optimality bought in robustness: LQR carries guaranteed margins (GM ≥ ½, PM ≥ 60°), LQG does not automatically, and recovery is a design action.

## Frameworks Introduced
- **6.1 ARE solution**: Hamiltonian matrix H = [[F, −GR⁻¹Gᵀ],[−Q, −Fᵀ]]; stabilizing solution S = stable invariant subspace (Y X⁻¹ from eigenvectors [X;Y]); iterative alternatives (Newton / squaring-root / doubling) for large systems; discrete-time ARE parallel.
- **6.2 Command response**: **open-loop equilibrium** (x̄, ū, ȳ) solving 0 = Fx̄ + Gū + w̄, ȳ = Hx̄ + Lū for each setpoint — regulation is always about an equilibrium pair; **nonzero-setpoint regulation** = perturbations about (x̄, ū) + equilibrium feedforward; command prefilters shape transients.
- **6.3 Cost-function structure = controller structure** (the chapter's design engine):
  - Weighting matrices as the design interface (Q = output/state penalties, R = control penalties; ratios set bandwidths).
  - **Output weighting** Q_y·(y − y_des)² in the cost → implicit model following (desired closed-loop modes emerge from the cost, not imposed).
  - **State augmentation for dynamic compensation**: add integrator states (u = −C₁x − C_I x_I, ẋ_I = e) → **PI/PID-like compensation from LQR**; proportional-**filter** augmentation (washout/lead states) and **PIF** compensation; filter dynamics chosen in the cost, Riccati sizes the gains.
  - **Explicit model following**: augment reference-model states into the plant, penalize tracking error in J.
  - **Transformed/partitioned solutions**: exploit structure (block-diagonal weights, subsystem partitioning) to shrink the Riccati.
  - **LQG regulator**: combine with Kalman-Bucy; compensator = filter + gain (dynamic compensator of order n).
- **6.4 Modal properties**: optimal closed-loop eigenvalue regions (with Q ≥ 0, R > 0 the modes sit in predictable sectors; cross-over frequency ↔ control-effort weighting); eigenvector freedom as a design resource (disturbance rejection directions); estimator modes (usually faster than regulator modes — the separation gap).
- **6.5 LQR robustness**: return-difference identity I + R^{1/2}L(s)R^{-1/2}... → **SISO LQR: GM ∈ [½, ∞), PM ≥ 60°**; multivariable version via singular values of the return difference (same bounds at the loop input under Q ≥ 0, R = I); spectral characteristics tie margins to cost weights; effects of plant parameter variations on stability; multivariable Nyquist + matrix-norm (σ̄) small-gain tests for structured/unstructured uncertainty.
- **6.6 LQG robustness**: inserting the estimator destroys the guaranteed margins — compensator loop margins can be arbitrarily small (near-unstable/near-unobservable plants); **robustness recovery** = loop transfer recovery (LTR) design: push filter poles to make the compensator loop reproduce the LQR return difference (the technique later formalized as LTR); **probability of instability** under random parameter uncertainty — a stochastic robustness measure beyond worst-case margins.
- **6.7 Footnote on adaptive control**: when parameter variation exceeds what a fixed LQG survives, adaptation (Ch 4.7 filters + re-design) is the way out — one paragraph closing the loop with the Åström-style world.

## Key Concepts
- **Hamiltonian eigenvector method**: the ARE is an invariant-subspace problem — stable subspace = stabilizing solution.
- **Equilibrium pair (x̄, ū)**: every setpoint has one; regulation is linear around it.
- **Augmentation**: integrators, filters, reference models — controller structure is manufactured by extending the state and re-weighting the cost.
- **Return difference**: I + L(s) — the object whose size bounds robustness; margins are its floor.
- **Guaranteed LQR margins**: GM ≥ ½ (infinite gain increase tolerance), PM ≥ 60° at the optimal loop.
- **Margin loss through the filter**: LQG ≠ LQR margins; separation buys performance decomposition, not robustness.
- **LTR / robustness recovery**: design the estimator so the compensator loop regains the regulator's return difference.

## Mental Models
- "Structure comes from the cost, not from a template": want integral action? Add the integrator to the plant and let the Riccati set the gain — never hand-tune a PI inside an optimal framework.
- "Optimality is a robustness certificate only where the theorem says so": LQR margins are guaranteed at the *optimal LTI loop*; add a filter and the certificate is void until recovered.
- "Margins are singular-value floors": GM/PM are the SISO shadows of σ̲(I + L) bounds — the multivariable statement is one inequality, not two numbers.
- "Every setpoint is an equilibrium first": compute (x̄, ū) numerically, then regulate the perturbation — feedforward from the equilibrium, feedback from the Riccati.

## Anti-patterns
- **Assuming LQG inherits LQR margins**: it doesn't — check the compensator loop explicitly (classical failure mode of 1970s optimal design).
- **Hand-tuning Q/R blindly**: use the modal/margin consequences (bandwidth ↔ control weight) to set them; iterate on σ̄ tests.
- **Estimator modes as slow as regulator modes**: separation degrades; keep the estimation gap (but not so wide that unmodeled dynamics bite — the LTR trade).
- **Ignoring discrete-time sampling effects on margins**: sampling delay erodes the guaranteed margins; check at the actual rate.

## Reference Tables

### Robustness guarantees
| Loop | Guarantee | Caveat |
|---|---|---|
| SISO LQR (optimal) | GM ∈ [½, ∞), PM ≥ 60° | at the design loop only |
| MIMO LQR | σ̲ bounds ⇒ same margins at input | Q ≥ 0, R = I conditions |
| LQG compensator | none automatic | recover via LTR |
| Discrete LQ | margins shrink with h | check z-plane |

### Controller structures from augmentation
| Augment | Cost penalizes | Result |
|---|---|---|
| Integrator state(s) | regulation error | PI / PID-like |
| Filter state(s) | filtered outputs | lead/lag, PIF |
| Reference model states | tracking error | explicit model following |
| Output weighting only | y − y_ref | implicit model following |

## Key Takeaways
1. The ARE is a stable-invariant-subspace computation — Hamiltonian eigenvectors (or doubling iterations) are the practical solver.
2. Controller architecture (PI, filters, model following) is produced by state augmentation + cost weighting, with the Riccati setting all gains consistently.
3. LQR's guaranteed margins (GM ≥ ½, PM ≥ 60°) are the book's payoff theorem connecting optimality to robustness.
4. LQG loses those margins through the estimator; LTR/robustness recovery is a first-class design step, not an afterthought.
5. When fixed-coefficient robustness is exhausted, adaptive filtering + redesign (Ch 4.7, 6.7) takes over — the two traditions meet here.

## Connects To
- **Ch 2**: eigen/SVD/Nyquist toolkit; **Ch 3**: Riccati from neighboring-optimal; **Ch 4**: filters; **Ch 5**: separation and the stochastic regulator this chapter hardens into design practice.
