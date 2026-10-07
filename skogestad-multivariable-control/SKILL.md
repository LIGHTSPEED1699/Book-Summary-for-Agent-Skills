---
name: skogestad-multivariable-control
description: Apply Skogestad & Postlethwaite's Multivariable Feedback Control (1st ed. 1996) frameworks - controllability analysis, RGA, singular values, uncertainty weights, mu, H-infinity loop shaping, model reduction, and control structure design - when analyzing or designing MIMO feedback systems.
---

# Multivariable Feedback Control (Skogestad & Postlethwaite)

The practitioner's bible of MIMO feedback: analysis before synthesis, structure before controller, directions before magnitudes. Use this skill whenever a control problem is multivariable, ill-conditioned, uncertain, or "the PID works but the loops fight each other."

## How to use
- Start with `cheatsheet.md` for the decision procedures and inequality tables.
- `patterns.md` holds the cross-chapter design patterns (the book's actual method).
- `glossary.md` decodes the notation (σ̲, γ(G), Λ, μ, CLDG, ...).
- `chapters/` has one distilled file per book chapter — read the relevant one before deep work in an area.

## The book's spine (in order)
1. **Scale everything** (ch1): variables to expected magnitude; without scaling every number below is meaningless.
2. **SISO loop shaping fundamentals** (ch2): |S| < 1/|w_P|, |T| < 1/|w_I|, M_s ≈ 2, bandwidth vs delay.
3. **Design requirements** (ch3): stability margins, performance weights, directionality (SVD), γ(G) = σ̄/σ̲ as the interaction alarm.
4. **Plant dynamics & reduction** (ch4): poles/zeros WITH directions, delays, H2/H∞/Hankel norms, keep gain+delay+RHP zeros+integrators.
5. **SISO limitations** (ch5): the 8 controllability rules — ω_c window from ω_d, 1/θ, z/2, ω_u, 2p.
6. **MIMO limitations** (ch6): the 14-step controllability procedure; σ̲(G) ≥ 1 where control is needed; RGA as input-uncertainty sensitivity.
7. **SISO robustness** (ch7): uncertainty weights w_I/w_O/w_A; RS ⇔ ‖wT‖∞ < 1; RP ⇔ |w_P S| + |w_O T| < 1.
8. **μ framework** (ch8): N-Δ form; RS = μ(N₁₁) < 1; RP = μ(N with Δ_P block) < 1; D-scalings; skewed μ; D-K iteration.
9. **Synthesis** (ch9): LQG fragility, coprime stability radius γ_opt = √(1+ρ(XZ)), McFarlane-Glover H∞ loop shaping, 2-DOF.
10. **Structure design** (ch10): output/input selection, cascade & input resetting, partial control, pairing rules, DIC, PRGA/CLDG.
11. **Model reduction** (ch11): balanced truncation/residualization (2×tail bound), optimal Hankel (1×tail), residualize for control models.
12. **Case studies** (ch12): helicopter (disturbance-in-the-plant), aero-engine (structure screening ladder), distillation (λ = 35.1, μ-optimal fix).
13. **Appendix A**: Schur, SVD, RGA algebra, norm tables, sensitivity factorization, LFTs.

## When to reach for this skill
- Pairing/structure questions (RGA, "which valve for which loop")
- "Why does decoupling blow up?" (input uncertainty + large RGA)
- Robustness verification (weights, ‖wT‖∞, μ)
- H∞/loop-shaping design sanity checks
- Controllability verdicts before spending design effort
