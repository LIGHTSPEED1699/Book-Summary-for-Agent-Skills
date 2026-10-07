# Chapter 10: Control Structure Design (Variables, Configuration, Decentralized Control)

## Core Idea
Before choosing K, choose the structure: which outputs to control, which inputs to manipulate, how to measure them, and how to decompose the controller — the structure decision dominates achievable performance, and the RGA (plus PRGA/CLDG for diagonal control) is the workhorse analysis tool.

## Frameworks Introduced
- **Optimal-control context (10.2)**: the control layer serves an economic optimizer; cost error splits into optimization error e_opt = r − y_opt (setpoint from the optimizer is not the true optimum) and control error e = y − r. Controlled outputs should be chosen to make BOTH small.
- **Controlled-output selection criteria (10.3)**: pick y so that (1) G⁻¹ is small (σ̲(G) large — inputs have large effect), (2) e_opt small (y_opt(d) depends weakly on disturbances — the cake example: control oven temperature, not heat input), (3) e small (easy to keep at setpoint). Practical rule: **control non-self-regulating outputs** (|G_d| > 1 somewhere); self-regulating outputs may be left open-loop (partial control). Output controllability index (Cao 1995): projection of output i onto the reachable output space of G (e_iᵀ U_r) — rank-deficient G ⇒ some outputs uncontrollable.
- **Manipulated-input/measurement selection (10.4)**: for input subsets, maximize σ̲(G_subset); QR decomposition with column pivoting on the steady-state gain matrix ranks candidate inputs; row-sums of the RGA of the full "large" model G_all (all candidates) give input/output screening (input projection index e_jᵀ V_r).
- **Non-square RGA (10.5)**: Λ = G ⊙ (G⁻¹_R)ᵀ with right inverse G⁻¹_R = Gᴴ(GGᴴ)⁻¹ for wide plants (more inputs than outputs); guides which inputs to keep.
- **Control configuration elements (10.6)**: cascade (extra measurements — conventional cascade; extra inputs — **input resetting / valve position control**), decentralized (diagonal K), feedforward, decoupling, selectors; **vertical decomposition** (hierarchical cascades, sequential design fast-loop-first) vs **horizontal decomposition** (independent loops). Closing a SISO loop trades input u_i for reference r_i as degree of freedom.
- **Cascade justification (Morari-Zafiriou a/b/c)**: (a) significant disturbance d₂ + nonminimum-phase G₁ ⇒ measure y₂; (b) uncertain/nonlinear inner block G₂ ⇒ fast inner loop removes uncertainty (L₂ ≈ I where K₁ acts); (c) simple-controller bandwidth limited by ω_u ⇒ inner cascade cuts phase lag (Example: factor-5 faster with inner loop).
- **Partial control (10.7)**: leave self-regulating outputs uncontrolled when interactions make full control infeasible; check open-loop disturbance effect on uncontrolled output ≤ 1 (scaled); feedforward can shrink it further.
- **Decentralized control machinery (10.8)**:
  - Return-difference factorization: **S = S̃(I + E T̃)⁻¹**, E = (G − Ĝ)Ĝ⁻¹ (Ĝ = diag of paired elements) — interactions enter as multiplicative perturbation E on the diagonal loop T̃; almost everything derives from this.
  - **PRGA** Γ = G ⊙ diag(G⁻¹) (scaled inverse; off-diagonals depend on output scaling; measures one-way interaction; S ≈ S̃Γ at effective-control frequencies) — performance relative gain array for reference tracking under diagonal control.
  - **CLDG** (closed-loop disturbance gain) G̃_d: disturbance gains with all other loops under perfect feedback; per-loop condition |1 + L_i| > |g̃_di| where |g̃_di| > 1 — the decentralized version of Ch 5 Rule 1.
  - Stability: sufficient conditions ρ(E T̃) < 1; μ(E)·σ̄(T̃) test (Theorem 10.2, Grosdidier-Morari) — μ(E) < 1 defines **generalized diagonal dominance**, allows tight control σ̄(T̃) ≤ 1 there; Gershgorin per-loop bounds.
  - **Pairing rules**: (1) RGA ≈ I at crossover frequencies (G near triangular ⇒ loop stability ⇒ overall stability, Theorem 10.4); (2) avoid negative steady-state RGA elements (integrity/DIC).
  - **DIC** (decentralized integral controllability): exists diagonal integral controller stable under independent detuning ε_i ∈ [0,1]; negative steady-state RGA element ⇒ not DIC (Theorem 10.6); MDIC conjecture (DIC ⇒ any stable diagonal PI works — false in general).
  - RGA and RHP zeros: negative steady-state RGA element for a pairing ⇒ odd number of RHP zeros in that loop's open loop (structural, can't tune away).
  - Decentralized fixed modes: unstable modes appearing only in off-diagonal elements (triangular plant) cannot be stabilized by ANY diagonal controller — check before pairing.

## Key Concepts
- **Structure dominates**: a poor base-layer configuration (e.g. LV distillation pairing with large RGA, aero-engine cascade creating RHP zeros) imposes fundamental limits no higher-layer design overcomes.
- **Integrity**: stability preserved as loops are taken in/out of service (ε_i ∈ {0,1}); DIC is the strong version (any detuning factor).
- **RGA = two-way interaction; PRGA = one-way too** (PRGA sees the triangular-plant leak the RGA misses).
- **CLDG = what disturbances look like once the OTHER loops close** — interactions can amplify or shrink apparent disturbance effects (distillation example: F disturbance amplified, z_F reduced on y_D).
- **Sequential tuning order**: fast/inner loops first (K₂ inner cascade → K₃ input reset → K₁ primary).

## Mental Models
- "Choose outputs you can keep at setpoint cheaply and whose optimum barely moves" — the three-criteria filter beats intuition.
- "Non-self-regulating ⇒ must control; self-regulating ⇒ candidate for partial control" — the cheapest structure decision.
- "RGA at crossover for stability, RGA at DC for integrity" — two frequency windows, two questions.
- "Diagonal control = nominal loops + interaction perturbation E": every decentralized question becomes a μ/small-gain question on E.
- "Extra measurement near the disturbance/input, extra input reset slowly" — cascade and valve-position-control in one line.

## Anti-patterns
- **Designing K before fixing structure** — the configuration sets the ceiling; synthesis only reaches toward it.
- **Pairing with negative steady-state RGA elements** — breaks integrity/DIC; loop flips sign when others close.
- **Assuming RGA ≈ I everywhere is needed** — only the crossover window matters for stability; DC window for integrity.
- **Forgetting decentralized fixed modes** — triangular plant with unstable mode only off-diagonal: no diagonal controller stabilizes it, period.
- **Full control of an infeasible output set** — partial control + feedforward beats a strained multivariable design.

## Reference Tables

### Structure design checklist
| Decision | Tool | Criterion |
|---|---|---|
| Which outputs | 3 criteria + self-regulation test | σ̲(G) large; e_opt small; control non-self-regulating |
| Which inputs | QR column pivoting / σ̲ of subsets | maximize σ̲; input projection index |
| Pairing | RGA at crossover + at DC | Λ ≈ I at ω_c; no λ < 0 at DC |
| Cascade? | Morari-Zafiriou a/b/c | big d₂ + NMP G₁; uncertain G₂; phase-lag-bound speedup |
| Partial control | open-loop \|G_d\| on uncontrolled output | ≤ 1 (scaled), else feedforward |
| Diagonal OK? | μ(E), CLDG, PRGA | μ(E) < 1 where tight control needed; \|1+L_i\| > \|g̃_di\| |

### Decentralized stability ladder (least → most conservative)
| Condition | Source |
|---|---|
| ρ(E T̃) < 1 ∀ω | exact for the factorized loop |
| μ(E) σ̄(T̃)-split (Thm 10.2) | Grosdidier-Morari |
| Gershgorin row/col bounds | per-loop individual bounds |
| \|E\|_max σ̄(T̃) < 1 | norm bound |

## Key Takeaways
1. Control structure design (outputs, inputs, pairings, configuration) is where most performance is won or lost; do it before synthesis.
2. The RGA earns its keep in two windows: crossover (stability of diagonal loops) and DC (integrity/DIC).
3. PRGA and CLDG extend the analysis to performance: references and disturbances under diagonal control.
4. Cascade loops buy speed (phase), uncertainty rejection, and linearity — tune inner-first; input resetting (valve position control) handles extra inputs.
5. Partial control is a legitimate design choice: leave self-regulating outputs open-loop, cover them with feedforward if needed.
6. Check decentralized fixed modes and negative-RGA structural obstructions before spending time on tuning.

## Connects To
- **Ch 6**: controllability analysis feeds every selection criterion here.
- **Ch 5**: CLDG condition is Rule 1 per loop; ω_c < ω_u per loop.
- **Ch 8**: μ(E) stability test is the M-Δ template applied to interactions.
- **Ch 12**: distillation LV/ DV configurations and aero-engine cascade case studies.
- **Appendix A.4**: RGA properties; Gershgorin theorem.
