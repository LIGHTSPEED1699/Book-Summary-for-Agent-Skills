---
name: astrom-adaptive-control
description: Apply Åström & Wittenmark's Adaptive Control (1st ed. 1989) frameworks - self-tuning regulators, MRAS, recursive estimation, dual control, auto-tuning, gain scheduling, averaging/robustness analysis, and practical implementation guards - when designing or debugging adaptive, self-tuning, or gain-scheduled control systems.
---

# Adaptive Control (Åström & Wittenmark, 1st ed. 1989)

The canonical treatment of adaptive control as estimation + design + classical loops. Use this skill whenever a controller must adjust itself: STR/MRAS design, auto-tuners, gain schedules, or diagnosing why an adaptive loop misbehaves (wind-up, chaos, bias, loss of excitation).

## How to use
- Start with `cheatsheet.md` for algorithms, tuning constants, and failure-mode tables.
- `patterns.md` holds the cross-chapter design patterns and the diagnosis playbook.
- `glossary.md` decodes notation (A/B/C polynomials, φ, θ, Diophantine, hyperstate...).
- `chapters/` has one distilled file per book chapter — load the relevant one before deep work.

## The book's spine (13 chapters)
1. **Five adaptive schemes** (ch1): gain scheduling, auto-tuning, MRAS, STR, dual control; find the *underlying design problem* of any scheme.
2. **Recursive estimation** (ch2): RLS/projection/stochastic approximation; bias from noise-regressor correlation; persistent excitation; forgetting factor.
3. **Deterministic STR** (ch3): Diophantine AR+BS = A_cA_o; indirect vs direct (reparameterization); observer polynomial A_o; integral action by spec.
4. **Stochastic/predictive STR** (ch4): minimum variance via C = AF + q^{-d}G; variance floor; LQ STR (ρ buys margins); GPC horizons.
5. **MRAS/direct methods** (ch5): MIT rule + γ bounds; Lyapunov-designed laws; PR/passivity; MRAS ≡ direct STR.
6. **System properties** (ch6): two-timescale nonlinear structure; chaos at high γ; averaging; turn-off phenomenon; direct schemes converge in behavior, not parameters.
7. **Dual control** (ch7): Bellman/hyperstate; probing; certainty equivalence = delta approximation.
8. **Auto-tuning** (ch8): relay feedback → K_u = 4d/πa, T_u; ZN open/closed-loop rules; describing functions.
9. **Gain scheduling** (ch9): schedule on physics-driven w; implicit scheduling; transformation beats table.
10. **Robust/self-oscillating** (ch10): Horowitz high-gain alternative; robust vs adaptive trade; SOAS forces excitation; sliding modes.
11. **Implementation** (ch11): covariance wind-up fixes (constant trace, directional forgetting, leakage, dead zone, projection); square-root filters; mode management.
12. **Products/applications** (ch12): auto-tuning as the killer app; ship steering as the model success; the abuse test.
13. **Perspectives** (ch13): adaptive signal processing, extremum control, expert supervision, learning.

## When to reach for this skill
- Designing an STR/MRAS/auto-tuner or debugging one that misbehaves
- "Should this loop be adaptive at all?" (abuse test, robust alternative)
- Gain schedule construction and validation
- Estimator failures: wind-up, drift, bias, frozen parameters
