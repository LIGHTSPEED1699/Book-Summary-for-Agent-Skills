# Chapter 12: Commercial Products and Applications

## Core Idea
Thirty years of applications sort into a clear hierarchy of success: auto-tuning (the killer app), gain-schedule construction, adaptive feedforward, and true adaptation for slow drift — with ship steering as the model success (low-order dynamics, no external dials) and "abuse" as the recurring caution (open-loop variation ≠ need for adaptation).

## Frameworks Introduced
- **Application taxonomy (12.2)**: feasibility studies → auto-tuning (adaptation loop on, then off with fixed parameters) → automatic gain-schedule construction (auto-tuner at each operating point, table built by operation) → true adaptive control (continuous) → adaptive feedforward (identification makes open-loop compensation viable).
- **Product categories (12.3-12.4)**:
  - **Tuners for PID**: parametric (step/PRBS → FOPDT model → empirical rules or pole placement: Hartmann & Braun Protonic, Honeywell UDC 6000); nonparametric (relay → one Nyquist point → modified ZN: SattControl ECA40, Fisher-Rosemount DPR960); external tuners (Supertuner, PIDWIZ, SIEPID); DDC tuning tools (Honeywell Looptune, Fisher Intelligent Tuner).
  - **Adaptive standard controllers**: parametric RLS + pole-placement PID (Bailey CLC04, Yokogawa SLPC); nonparametric continuous Nyquist estimation (SattControl ECA400 band-pass relay tracking); pattern recognition/expert (Foxboro EXACT 1984, Yokogawa SLPC-171/271, Fenwal 570 — 100-200 rules capturing engineer skill, tune on setpoint changes/upsets).
  - **General-purpose DDC toolboxes** (ASEA Brown Boveri 1982, First Control 1986); **PLC implementations** (3M: ~200 loops since 1987, gradient estimation + modified minimum-variance, variable-delay B polynomials).
  - **Special-purpose**: ship steering autopilots, motor drives, robots, missile SOAS.
- **Ship steering success story (12.7)**: self-tuning PID since 1973 full-scale; low-order (Nomoto) dynamics, slow sea states, purpose specifiable a priori ⇒ controller with **no externally adjusted parameters**; commercial since 1980 — the book's exemplar of adaptation done right.
- **Automobile control (12.6)**: cruise control adapting to load/grade changes (early 1980s demonstrations).
- **Ultrafiltration (12.8)**: membrane fouling changes gain by orders of magnitude over run time — adaptive/gain-scheduled control extends productive operation.
- **Process control (12.5)**: pH neutralization (extreme nonlinearity), distillation, dryers — adaptive feedforward + STR where measurable disturbances dominate.
- **Performance-related dials**: expose desired closed-loop bandwidth or LQ weight instead of raw controller parameters — the operator-interface principle that makes true adaptation usable.
- **Abuse test (12.2)**: open-loop dynamics variation does NOT imply adaptation is needed — compare closed-loop responses under a robust fixed controller first (Ch 10).

## Key Concepts
- **Auto-tuning as productized identification**: manual/auto/tune three-position switches; commissioning + routine maintenance use.
- **Parametric vs nonparametric tuners**: model-based vs frequency-point (relay) approaches.
- **Expert/pattern-recognition tuning**: rule bases reacting to observed responses rather than fitting models.
- **No-dial design**: when the purpose of control is specifiable a priori (autopilots), ship a controller with zero external knobs.
- **Adaptive feedforward dependency**: feedforward needs good models ⇒ identification is its prerequisite; underexploited.

## Mental Models
- "The market adopted the cheap halves of adaptive control": estimation + design automation (tuning) won; continuous adaptation stayed niche.
- "Success pattern: low-order plant + slow variation + specifiable purpose" (ship steering) — check all three before selling adaptation.
- "Auto-tuners build gain schedules for free": run the tuner as the plant visits operating points.
- "Expert tuners encode the commissioning engineer; model tuners encode the textbook" — both are identification, different priors.

## Anti-patterns
- **Adapting because open-loop gain varies** — closed-loop response may be fine with fixed control (the abuse test).
- **Continuous adaptation where on-demand tuning suffices** — complexity without benefit.
- **Proprietary black-box adaptive products without supervision story** — the 1980s lesson: users need to see why parameters move.

## Reference Tables

### Product categories
| Category | Mechanism | Examples |
|---|---|---|
| PID tuner (parametric) | step/PRBS → FOPDT → rules | Protonic, UDC6000 |
| PID tuner (nonparametric) | relay → (K_u,T_u) → ZN-mod | SattControl ECA40, DPR960 |
| Adaptive PID | RLS + pole placement / continuous Nyquist / rules | CLC04, ECA400, EXACT |
| Toolbox | STR/GPC blocks in DDC | ABB, First Control |
| Special-purpose | tailored STR/SOAS | autopilots, missiles |

## Key Takeaways
1. Auto-tuning is adaptive control's mass-market success — every modern PID ships with it.
2. The four-step application ladder (tune → schedule → feedforward → adapt) matches increasing need against increasing complexity.
3. Ship steering is the canonical true-adaptive success: low order, slow drift, specifiable purpose, zero dials.
4. Adaptive feedforward is the underexploited high-value direction (feedforward needs models; identification supplies them).
5. Always run the abuse test first: closed-loop evidence, not open-loop variation, justifies adaptation.

## Connects To
- **Ch 8**: the relay methods the nonparametric tuners implement.
- **Ch 3-4**: STR/GPC cores of parametric products.
- **Ch 9**: gain-schedule construction workflow.
- **Ch 10**: the robust-alternative caution formalized.
