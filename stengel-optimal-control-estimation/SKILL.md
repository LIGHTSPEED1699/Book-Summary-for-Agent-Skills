---
name: stengel-optimal-control-estimation
description: Apply Robert F. Stengel's Optimal Control and Estimation (1994) frameworks - cost-function design, calculus of variations and minimum principle, Kalman filtering, LQG separation, algebraic Riccati design, controller structures via state augmentation, and LQR/LQG robustness margins - when designing optimal, LQG, or robust multivariable controllers or building state estimators.
---

# Optimal Control and Estimation (Stengel, McGraw-Hill 1994)

The unified time-domain treatment: trajectory optimization → optimal estimation → stochastic control (LQG) → practical linear multivariable design with robustness audits. Use this skill whenever a design should come from a cost function rather than a template, or when a Kalman filter / LQG loop needs to be built or debugged.

## How to use
- Start with `cheatsheet.md` for the algorithm set (Riccati, Kalman, margins) and quick tables.
- `patterns.md` holds design patterns (augmentation recipes, robustness workflow) and diagnosis playbook.
- `glossary.md` decodes notation (x̂, P, S, Hamiltonian, return difference...).
- `chapters/` has one distilled file per chapter — load the relevant one before deep work.

## The book's spine (6 chapters + epilogue)
1. **Framework** (ch1): seven-family variable model (p,u,w,x,y,η,z); cost-function categories; controllability/observability → stabilizability/detectability.
2. **Math toolkit** (ch2): weighted norms, Lagrange multipliers, eigen/modes, transition matrices, random processes, stability tests, frequency domain.
3. **Trajectories** (ch3): Mayer/Lagrange/Bolza costs; Hamiltonian + costate TPBVP; minimum principle; HJB; singular arcs; numerical methods; **neighboring-optimal Riccati feedback**.
4. **Estimation** (ch4): least squares → Kalman filter (discrete first, Kalman-Bucy as limit); duality; EKF/quasilinear; adaptive filters (parameter/noise/multiple-model).
5. **Stochastic control** (ch5): information sets; dual control/probing (only pays when nonlinear/unknown); **LQG certainty equivalence + cost decomposition**; mode union.
6. **LTI multivariable design** (ch6): ARE via Hamiltonian; equilibrium pairs for commands; **structures by augmentation (PI, filters, model following)**; modal properties; **LQR margins GM≥½, PM≥60°**; LQG margin loss + recovery; adaptive footnote (exogenous scheduling vs endogenous adaptation).
7. **Epilogue**: the theory is literal — pose the problem right.

## When to reach for this skill
- Designing LQR/LQG, Kalman filters, or their discrete-time counterparts
- Trajectory optimization (minimum time/fuel/energy) and neighboring-optimal feedback
- Turning controller structure requirements (integral action, model following) into augmented-cost designs
- Auditing optimal-loop robustness (margins, singular values, LTR)
