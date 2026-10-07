# Chapter 1: What Is Adaptive Control?

## Core Idea
An adaptive controller has adjustable parameters plus a mechanism that adjusts them on-line; there are exactly five ways to do that — gain scheduling, auto-tuning, MRAS, self-tuning regulators, and dual control — and every adaptive scheme hides an "underlying design problem" that reveals what the loop does when the parameters are known.

## Frameworks Introduced
- **The five parameter-adjustment mechanisms** (§1.4):
  - **Gain scheduling**: measurable scheduling variable (Mach/altitude, production rate) maps to controller parameters via function or table; two loops (inner feedback, outer parameter adjustment). Controversially "adaptive" — yes under the informal definition.
  - **Auto-tuning**: controller tuned automatically (often experimentally), then held fixed; the practical workhorse (Ch 8).
  - **MRAS (model-reference adaptive control)**: reference model defines ideal response; outer loop adjusts controller parameters to drive model error e = y − y_m to zero. Original adjustment law = **MIT rule**: dθ/dt = −γ e ∂e/∂θ (gradient of e², sensitivity derivative approximation required). Direct method.
  - **STR (self-tuning regulator)**: recursive parameter estimation + on-line design calculation; controller parameters updated indirectly. **Certainty equivalence principle**: estimates used as if true (uncertainty ignored). Reparameterizing the model in controller parameters kills the design block → "direct" STR.
  - **Dual control**: full stochastic-control treatment — unknown parameters modeled as states (dθ/dt = 0 + noise), augmented state z = (xᵀ, θᵀ)ᵀ, minimize E[G(z(T))] + ∫g(z,u)dt via Bellman equation; solution = nonlinear estimator producing the **hyperstate** (conditional distribution p(z|y,u)) + nonlinear feedback map. Optimal controller **probes** (injects perturbations) when uncertainty is high — the dual (control + estimation) action. Computationally intractable in general; conceptually the benchmark.
- **Underlying design problem**: the design problem solved as if parameters were known; find it for any adaptive scheme — it predicts ideal-condition behavior and is the evaluation handle.
- **Process description convention**: SISO linear, polynomials A(q)u... discrete-time pulse transfer B(q)/A(q) with unknown orders/coefficients; operators p = d/dt, q = forward shift; notation G(p)w(t).
- **Performance-related dials**: adaptive controllers can expose dials labeled with closed-loop bandwidth or LQ trade-off instead of raw parameters — "controllers with no externally adjusted parameters" are achievable for well-specified applications (missile/ship autopilots).

## Key Concepts
- **Adaptive system**: controller with adjustable parameters + an adjustment mechanism (informal definition).
- **Direct vs indirect adaptation**: adjustment rules update controller parameters directly (MRAS, direct STR) vs via process-parameter estimates + design calculation (indirect STR).
- **Certainty equivalence**: separate estimation and control; ignore estimate uncertainty.
- **Hyperstate**: conditional distribution of all states and parameters — the dual controller's state.
- **Probing**: deliberate excitation to improve estimates; automatic in dual control, must be engineered (or avoided) in STR.
- **Scheduling variable**: measured quantity correlating with dynamics changes.

## Mental Models
- "Find the underlying design problem first" — it tells you what the adaptive loop converges to and what specs it implicitly optimizes.
- "STR = automating the modeling + tuning meeting every sample period"; gain scheduling = the same meeting done offline into a table.
- "Certainty equivalence is a deliberate amnesia about uncertainty"; dual control remembers everything and pays Bellman's price.
- "Two-loop picture everywhere": inner classical loop + outer parameter-adjustment loop — analyze each separately.

## Anti-patterns
- **Adapting when a scheduling variable exists**: gain scheduling is simpler, verifiable, and standard in flight control; use it before MRAS/STR.
- **Ignoring the estimation-vs-control interaction**: STRs assume slow parameter variation; fast unmodeled dynamics + adaptation interact badly (Ch 6-10: instability, chaos, "turn-off phenomenon").
- **Expecting probing-free adaptation to identify fast**: without persistent excitation, estimates drift or freeze (Ch 2, Ch 11).
- **Treating adaptive schemes as black boxes**: no externally adjustable dials → operator can't tell the controller what "good" means.

## Reference Tables

### The five schemes
| Scheme | Adjusts via | Needs model? | Certainty equiv? | Used when |
|---|---|---|---|---|
| Gain scheduling | table on scheduling variable | yes (offline) | n/a | measurable dynamics correlate |
| Auto-tuning | experiments, then fixed | yes | n/a | slow drift, commissioning |
| MRAS | error gradient (MIT/Lyapunov) | reference model only | yes | specs as reference model |
| STR (indirect) | estimate + design calc | yes, parametric | yes | unknown SISO linear process |
| Dual control | Bellman/hyperstate | full stochastic | no (optimal) | theory benchmark only |

## Key Takeaways
1. Adaptive = adjustable parameters + adjustment mechanism; five canonical mechanisms, each a two-loop system.
2. Every adaptive scheme has an underlying design problem — identify it; it is the system's ideal behavior.
3. Certainty equivalence (STR) vs dual control (probing) is the fundamental estimation/control trade-off; practice lives at certainty equivalence with engineered safeguards.
4. Gain scheduling is the industrial default when a scheduling variable exists; adaptive schemes handle what it can't.
5. The book's notation: A/B/C polynomials in q (discrete) or p (continuous), unknown orders allowed — the STR design chapters build on it.

## Connects To
- **Ch 2**: the recursive estimation half of STR (least squares variants).
- **Ch 3-4**: STR design in detail (deterministic, then stochastic/predictive).
- **Ch 5**: MRAS theory (MIT rule → Lyapunov → passivity).
- **Ch 7**: stochastic adaptive control, dual control made concrete (self-tuning regulators with loss minimization).
- **Ch 9**: gain scheduling deep dive.
