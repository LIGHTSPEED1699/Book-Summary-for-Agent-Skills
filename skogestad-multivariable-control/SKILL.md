---
name: skogestad-multivariable-control
description: Apply Skogestad & Postlethwaite's Multivariable Feedback Control (2nd ed. 2005) frameworks - controllability analysis, RGA, SIMC tuning, singular values, uncertainty weights, mu, H-infinity loop shaping, self-optimizing control, LMIs, model reduction, and control structure design - when analyzing or designing MIMO feedback systems.
---

# Multivariable Feedback Control (Skogestad & Postlethwaite, 2nd ed. 2005)

**Edition**: 2nd (2005, Wiley) — updated 2026-10-07 from the full 589-page scan. 13 chapters + App A (matrix theory) + App B (project work). 1st ed. (1996) had 12 chapters; 2e adds ch3 (multivariable intro, RGA moved in), ch4 (elements of linear system theory), ch12 (LMIs, brand new), and SIMC tuning + half rule in ch2, self-optimizing control in ch10.

The practitioner's bible of MIMO feedback: analysis before synthesis, structure before controller, directions before magnitudes. Use this skill whenever a control problem is multivariable, ill-conditioned, uncertain, or "the PID works but the loops fight each other."

## How to use
- Start with `cheatsheet.md` for the decision procedures and inequality tables.
- `patterns.md` holds the cross-chapter design patterns (the book's actual method).
- `glossary.md` decodes the notation (σ̲, γ(G), Λ, μ, CLDG, ...).
- `chapters/` has one distilled file per 2e chapter (ch01–ch13 + appendix-a); `chapters/legacy-1ed/` holds superseded 1st-edition distills kept for reference.

## Chapter index (2e)
| # | File | Key frameworks |
|---|---|---|
| 1 | [ch01](chapters/ch01-introduction.md) | scaling, model/diagram conventions |
| 2 | [ch02](chapters/ch02-classical-feedback-control.md) | SISO shaping, SIMC, half rule, lower GM |
| 3 | [ch03](chapters/ch03-introduction-to-multivariable-control.md) | SVD directions, RGA, general formulation |
| 4 | [ch04](chapters/ch04-elements-of-linear-system-theory.md) | minimal realization, internal stability, Youla, coprime |
| 5 | [ch05](chapters/ch05-siso-performance-limitations.md) | 8 controllability rules |
| 6 | [ch06](chapters/ch06-mimo-performance-limitations-rga.md) | 14-step procedure, σ̲(G), RGA sensitivity |
| 7 | [ch07](chapters/ch07-siso-uncertainty-robustness.md) | w_I/w_O/w_A, RS/RP tests |
| 8 | [ch08](chapters/ch08-robust-stability-performance-mu.md) | μ, D-scaling, skewed μ, D-K |
| 9 | [ch09](chapters/ch09-control-system-design-lqg-h2-hinf.md) | LQG+integral, coprime radius, loop shaping, 2-DOF |
| 10 | [ch10](chapters/ch10-control-structure-design.md) | variable ladder, self-optimizing, cascade, PRGA/CLDG |
| 11 | [ch11](chapters/ch11-model-reduction.md) | balanced trunc/residualization, optimal Hankel |
| 12 | [ch12](chapters/ch12-linear-matrix-inequalities.md) | LMI form, convex synthesis, BMI escape |
| 13 | [ch13](chapters/ch13-case-studies.md) | helicopter, aero-engine, distillation |
| A | [appendix-a](chapters/appendix-a-matrix-theory-norms.md) | Schur, SVD, RGA algebra, norms, LFTs |

## The book's spine (2e, in order)
1. **Scale everything** (ch1): variables to expected magnitude; without scaling every number below is meaningless.
2. **Classical feedback control** (ch2): |S| < 1/|w_P|, |T| < 1/|w_I|, M_s ≈ 2, bandwidth vs delay; unstable plants, feedback amplifier, lower gain margin; **SIMC tuning rules + half rule for effective delay** (2e addition).
3. **Introduction to multivariable control** (ch3, new in 2e): MIMO transfer matrices, frequency response with directions, **RGA** (moved here from old ch10), multivariable RHP zeros, first look at MIMO robustness, general control problem. → [ch03](chapters/ch03-introduction-to-multivariable-control.md)
4. **Elements of linear system theory** (ch4, new in 2e): state-space, minimal realizations, controllability/observability Gramians, pole polynomial, MIMO zeros with directions, internal stability, stabilizing controllers (Youla), coprime factorizations. → [ch04](chapters/ch04-elements-of-linear-system-theory.md)
5. **SISO limitations** (ch5): the 8 controllability rules — ω_c window from ω_d, 1/θ, z/2, ω_u, 2p; 2e adds sharper RHP-pole/zero limitation results.
6. **MIMO limitations** (ch6): the 14-step controllability procedure; σ̲(G) ≥ 1 where control is needed; RGA as input-uncertainty sensitivity; uncertainty-limitation section rewritten in 2e.
7. **SISO uncertainty and robustness** (ch7): uncertainty weights w_I/w_O/w_A; RS ⇔ ‖wT‖∞ < 1; RP ⇔ |w_P S| + |w_O T| < 1.
8. **MIMO robust stability and performance** (ch8): N-Δ form; RS = μ(N₁₁) < 1; RP = μ(N with Δ_P block) < 1; D-scalings; skewed μ; D-K iteration.
9. **Controller design** (ch9): LQG fragility + **integral-action strategy for LQG** (2e), coprime stability radius γ_opt = √(1+ρ(XZ)), McFarlane-Glover H∞ loop shaping, 2-DOF.
10. **Control structure design** (ch10, reorganized in 2e): variable selection ladder, **self-optimizing control** (new 2e material), cascade & input resetting, partial control, pairing rules, DIC, PRGA/CLDG, rewritten decentralized-control section.
11. **Model reduction** (ch11): balanced truncation/residualization (2×tail bound), optimal Hankel (1×tail), residualize for control models.
12. **Linear matrix inequalities** (ch12, brand new in 2e): F(x) = F₀ + Σ xᵢFᵢ ≺ 0 convex feasibility; stability, H∞, μ upper bounds, Youla parameterization as LMIs. → [ch12](chapters/ch12-linear-matrix-inequalities.md)
13. **Case studies** (ch13): helicopter (disturbance-in-the-plant), aero-engine (structure screening ladder, chs 11+13), distillation (λ₁₁ = 35.1, μ-optimal fix).
- **Appendix A**: Schur, SVD, RGA algebra, norm tables, sensitivity factorization, LFTs. **Appendix B**: project work and sample exam.

## When to reach for this skill
- Pairing/structure questions (RGA, "which valve for which loop")
- "Why does decoupling blow up?" (input uncertainty + large RGA)
- PID tuning with a robustness budget (SIMC: pick τc, get Kc/τI/τD)
- "Which variable should I hold constant?" (self-optimizing control)
- Robustness verification (weights, ‖wT‖∞, μ)
- H∞/loop-shaping design sanity checks
- Controllability verdicts before spending design effort

## Topic index
- **RGA / pairing** → ch3, ch6, ch10, App A
- **SIMC / PID tuning / half rule** → ch2
- **Effective delay** → ch2, ch5
- **Singular values / condition number γ(G)** → ch3, ch6
- **Uncertainty weights / RS / RP** → ch7
- **μ / D-scaling / D-K** → ch8
- **H∞ loop shaping / coprime radius** → ch9
- **LQG + integral action** → ch9
- **Self-optimizing control / variable selection** → ch10
- **Cascade / reset / partial control** → ch10
- **Balanced truncation / residualization** → ch11
- **LMI** → ch12
- **Internal stability / Youla / coprime** → ch4
- **Distillation / aero-engine / helicopter benchmarks** → ch13
