# Chapter 5: Limitations on Performance in SISO Systems

## Core Idea
Input-output controllability is a property of the plant alone: a small set of bandwidth inequalities (the 8 controllability rules) tells you *before designing any controller* whether acceptable control is physically possible — and if the required and achievable bandwidths conflict, the fix is process design, not controller design.

## Frameworks Introduced
- **Controllability analysis procedure (feedback)**: scale variables (Ch 1); form scaled G, G_d; then apply Rules 1-8 to get required vs achievable crossover ω_c; conflict ⇒ not controllable.
- **The 8 controllability rules** (necessary conditions, approximate within ~2×):
  1. **Disturbance rejection speed**: ω_c > ω_d (where |G_d| first crosses 1); precisely |S| ≤ 1/|G_d| ∀ω.
  2. **Reference tracking**: |S| ≤ 1/R up to required tracking frequency ω_r.
  3. **Input constraints from disturbances**: acceptable (|e|<1): |G| > |G_d| − 1 where |G_d| > 1; perfect: |G| > |G_d|.
  4. **Input constraints from setpoints**: |G| > R⁻¹ up to ω_r.
  5. **Delay θ in GG_m**: ω_c < 1/θ.
  6. **RHP zero z in GG_m**: tight low-freq control needs ω_c < z/2 (real z), ω_c < |z| (imaginary z); alternative: reverse gain sign and get tight control ABOVE, ω_c > 2z — but never tight control *near* z.
  7. **Phase lag**: ω_c < ω_u (ultimate freq, ∠GG_m = −180°) — subsumes Rules 5-6 in practice (PID-class controllers).
  8. **Unstable real pole p**: ω_c > 2p; plus |G| > |G_d| up to p or saturation prevents stabilization.
- **Ideal ISE / perfect control**: e = 0 requires u = G⁻¹(r − G_d d); possible iff G⁻¹G_d causal and stable (G minimum phase, no delay, relative degree of G_d ≥ G); otherwise perfect control is noncausal and only approximate control is possible.
- **Weighted-sensitivity bandwidth limits (Theorem 5.4 route)**: ‖w_P S‖∞ ≥ |w_P(z)| at any RHP zero z ⇒ weight must satisfy |w_P(z)| ≤ 1; with w_P requiring offset A=0, peak M=2 ⇒ ω_B* < 0.5z (real z), < 0.86|z| (imaginary).
- **Feedforward controllability analysis**: perfect FF u = −G⁻¹G_d d needs G⁻¹G_d proper + stable; check |G⁻¹G_d| for input saturation; FF relaxes feedback bandwidth needs (use both).
- **Margins M_1..M_6 picture**: margins on ω_c for input constraints, performance, RHP pole (below), RHP zero (above), −180° phase (below), delay (below) — draw the allowed ω_c window.

## Key Concepts
- **(Input-output) controllability**: ability to achieve acceptable control performance; quantified by plant-only bounds.
- **ω_d**: frequency where |G_d| first crosses 1 from below — disturbance content edge; Rule 1 says control must be faster.
- **Self-regulating output test**: "control outputs that are not self-regulating" ⇔ |G_d(jω)| > 1 somewhere ⇒ feedback needed.
- **RHP zero is a no-tight-control zone, not a total ban**: tight below z/2 OR above 2z; the forbidden band is around z.
- **Uncertainty is benign in SISO feedback** except where relative uncertainty → 100% (which is equivalent to an imaginary-axis zero, already Rule 6).
- **Integrating/non-self-regulating processes**: |G_d| > 1 at low ω ⇒ need |S| < 1/|G_d| — quantifies "control the non-self-regulating output".

## Mental Models
- "Draw the ω_c window": Rules 1,2,8 push ω_c UP; Rules 5,6,7 push it DOWN; empty window = infeasible plant, go redesign the process (step 0).
- "Bigger disturbance or tighter error spec ⇒ you need more bandwidth" — the one-line content of Rules 1-4.
- "Check |G| vs |G_d| at DC first": if the scaled input can't even beat the disturbance at steady state (|G(0)| ≤ |G_d(0)| − 1), nothing saves you except feedforward or equipment changes.
- "Delay kills the top of the window first": 1/θ is usually the binding ceiling in process control.

## Anti-patterns
- **Tuning harder on an uncontrollable I/O pair**: rules violated ⇒ no controller (any structure) achieves the spec; fix equipment/sensor-actuator placement.
- **Assuming RHP zero = hopeless**: it only forbids tight control near z; slow (ω_c < z/2) or fast-reverse (ω_c > 2z) designs are legal.
- **Ignoring saturation when stabilizing unstable plants**: ω_c > 2p AND |G| > |G_d| up to p, else windup/saturation loses stabilization during transients.
- **Trusting the rules as sufficient**: they're one-effect-at-a-time necessary conditions; margins between them are needed.

## Reference Tables

### Controllability window for ω_c
| Constraint | Bound | Direction |
|---|---|---|
| Disturbance content ω_d | ω_c > ω_d | lower |
| Tracking ω_r, scale R | \|S\| ≤ 1/R to ω_r | lower |
| Unstable pole p | ω_c > 2p (and \|G\|>\|G_d\| to p) | lower |
| Delay θ (incl. measurement) | ω_c < 1/θ | upper |
| RHP zero z (tight low-freq) | ω_c < z/2 real, < \|z\| imag | upper |
| Phase lag ω_u | ω_c < ω_u | upper |

### Perfect control feasibility
| Requirement | Condition |
|---|---|
| Feedback e=0 | G⁻¹G_d stable + causal |
| FF u=−G⁻¹G_d d | G min-phase, no delay, rdeg(G_d) ≥ rdeg(G) |
| Input not saturated | \|G⁻¹G_d\| ≤ 1 at disturbance frequencies |

## Key Takeaways
1. Run the 8 rules before designing anything; they're plant-only and controller-independent.
2. Controllability = nonempty ω_c window; conflict ⇒ process/equipment redesign, sensor/actuator relocation, or feedforward.
3. RHP zeros forbid tight control only near their frequency; delays cap ω_c at 1/θ; unstable poles demand ω_c > 2p.
4. SISO model uncertainty barely affects feedback performance unless ~100% at some frequency.
5. The rules generalize: decentralized MIMO control gets the same rules per loop via CLDG and PRGA (Ch 10).

## Connects To
- **Ch 6**: same rules with directions (RGA, singular values) for MIMO.
- **Ch 1**: scaling is the precondition; step-0 process design is the escape hatch.
- **Ch 10**: CLDG/PRGA extend these rules to decentralized MIMO loops.
- **Ch 7**: uncertainty treated properly for SISO RS/RP.
