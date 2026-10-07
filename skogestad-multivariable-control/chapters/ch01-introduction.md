# Chapter 1: Introduction

## Core Idea
Control system design is a structured, iterative procedure where most of the leverage lies in the early steps — model scaling, variable selection, and controllability analysis — not in the controller formula itself; "even the best control system cannot make a Ferrari out of a Volkswagen."

## Frameworks Introduced
- **14-step design procedure**: plant study → model & simplify → analyze model → choose controlled outputs → choose measurements/manipulated variables → select control configuration → choose controller type → set performance specs → design controller → analyze → simulate → iterate → implement → validate/tune online.
  - When to use: any control project; the book's distinctive contribution is systematic support for steps 3-7 (controllability analysis and structure design), which most texts skip.
  - How: work the steps in order; many working industrial designs (cascaded SISO loops) succeed via steps 1, 4-7, 13-14 alone — but then you need the book's tools to pick the structure.
- **Step 0 — process design for controllability**: equipment design and control design form a unit (Ziegler & Nichols 1943 quote); "controllability" = the process's ability to achieve and maintain the desired equilibrium. Quantified in Ch 5-6.
- **NS/NP/RS/RP taxonomy** (the book's central vocabulary):
  - **Nominal Stability (NS)**: stable with no model uncertainty.
  - **Nominal Performance (NP)**: specs met with no uncertainty.
  - **Robust Stability (RS)**: stable for all plants within the worst-case uncertainty.
  - **Robust Performance (RP)**: specs met for all plants within the worst-case uncertainty.
- **Variable scaling**: divide every variable by its maximum expected/allowed change so all signals are O(1); scaled objective: given |d| ≤ 1 and |e_r| ≤ 1, find u with |u| ≤ 1 such that |e| ≤ 1.
  - When to use: always, before analysis or weight selection. MIMO: use diagonal scaling matrices D_e, D_u, D_d so all errors have comparable importance.
  - How: d̃ = d̂/d̂_max, ũ = û/û_max, ẽ = ê/ê_max (scale outputs by allowed error, not reference, usually). Asymmetric ranges: use largest variation for d̂_max, smallest for û_max and ê_max.
- **Reference-as-disturbance trick**: with r = R·e_r, a normalized reference step is a disturbance with G_d = -R (R usually diagonal, R ≥ 1). Unifies servo and regulator problems.

## Key Concepts
- **Regulator problem**: manipulate u to counteract disturbance d. **Servo problem**: keep y near reference r. Both: make e = y - r small.
- **Model uncertainty**: G_p = G + E with bounded E; express E = w·Δ with normalized ‖Δ‖ ≤ 1 via weighting functions w(s).
- **Transfer function G(s)**: ratio of Laplace transforms with zero initial conditions; deviation variables; independent of input signal for linear systems.
- **Properness**: strictly proper (G→0 as s→∞; all practical systems), semi/bi-proper (G→D≠0; used for high-frequency D-terms and derived functions like S), improper (G→∞; nonphysical).
- **Pole excess / relative order**: n - n_z (denominator order minus numerator order).
- **Deviation variables**: all Laplace signals are deviations from a nominal operating point/trajectory; initial conditions zero.
- **Notation contract**: S = (I+L)^-1 sensitivity at output, T = L(I+L)^-1 complementary sensitivity, L = GK (or GKG_m with measurement dynamics); S_I, T_I at plant input with L_I = KG. RHP includes the jω-axis (so integrators are "RHP poles"). G_p = perturbed plant set, G' = one perturbed plant, Δ = normalized uncertainty.

## Mental Models
- "Scale first, then design" — every interpretation in the book (especially Ch 5-6 controllability measures and S for MIMO) is only valid with correct scaling; MIMO S is meaningless unless output errors are comparable magnitude.
- "Feedback design = shaping S and T" — keep ‖S‖ small where disturbances/reference live, ‖T‖ small where noise and uncertainty live; S + T = I forces the tradeoff.
- "Uncertainty is a set, not a number" — analyze the worst member of {G + wΔ : ‖Δ‖ ≤ 1}, not just the nominal G.
- "Controllability is decided before the controller exists" — sensor/actuator location and process design bound achievable performance.

## Anti-patterns
- **Skipping steps 3-7**: designing the controller before checking controllability and pairing; a well-tuned controller on an un-controllable structure still fails.
- **Designing on unscaled variables**: weight selection and controllability measures become arbitrary; MIMO S misused when outputs have wildly different magnitudes.
- **Trusting a single nominal model**: plant inaccuracy inside the feedback loop is the main failure source; NS does not imply RS.

## Reference Tables

### NS/NP/RS/RP at a glance
| Property | With uncertainty? | Requirement |
|---|---|---|
| Nominal Stability | no | closed loop stable for G |
| Nominal Performance | no | specs met for G |
| Robust Stability | yes | stable for all G_p in uncertainty set |
| Robust Performance | yes | specs met for all G_p in set |

### Scaling rules
| Variable | Scale by | Note |
|---|---|---|
| disturbance d̂ | d̂_max (largest expected) | asymmetric → largest variation |
| input û | û_max (largest allowed) | asymmetric → smallest variation |
| output/error ê, r̂ | ê_max (largest allowed error) | same factor for y, e, r; if selecting outputs, scale by expected variation instead |

### Model validity check (room heating example)
| Quantity | Value | Meaning |
|---|---|---|
| k (input gain, scaled) | 20 | input authority |
| k_d (disturbance gain, scaled) | 10 | \|k_d\|>1 ⇒ feedback/feedforward needed |
| \|k\| > \|k_d\| | yes | steady-state perfect rejection possible with \|u\|≤1 |

## Key Takeaways
1. Work the 14-step procedure explicitly; the controller formula (steps 9-10) is rarely where designs fail.
2. Scale all variables to O(1) before any analysis; MIMO sensitivity analysis is invalid otherwise.
3. State NS/NP/RS/RP requirements separately — they are different properties with different tests.
4. Model uncertainty as a weighted normalized set G_p = G + wΔ, ‖Δ‖ ≤ 1.
5. Treat reference changes as disturbances (G_d = -R) to unify the design problem.
6. Controllability is a property of the process + sensor/actuator structure, not of the controller.

## Connects To
- **Ch 2**: SISO version of the S/T loop-shaping ideas introduced here.
- **Ch 3**: turns "specs" (step 8) into quantitative S/T constraints.
- **Ch 5-6**: quantify input-output controllability (the "step 0" promise).
- **Ch 7-8**: the machinery for NP/RS/RP analysis (SISO then MIMO/μ).
