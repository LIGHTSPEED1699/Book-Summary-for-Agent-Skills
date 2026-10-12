# Chapter 3: Nonlinear Equations and Stability

## Core Idea
When y′ = f(t, y) is nonlinear, solve qualitatively instead of symbolically: draw the direction field, find steady states, and classify them by linearizing — the Jacobian's eigenvalues (from λ² − Tλ + D = 0) decide sink/source/saddle/spiral/center. The numerical half of the chapter (Euler, Runge-Kutta) turns the same first-order system into computable trajectories, with step-size stability limits that mirror the continuous stability condition.

## Frameworks Introduced
- **Nonlinear y′ = f(t,y) (3.1)**: direction fields and isoclines (curves f = const where all arrows have slope = const); solutions cross isoclines one way only.
- **Phase plane classification (3.2)**: for y″ + By′ + Cy = 0 viewed as a system in (y, y′): real roots both negative = sink (stable); both positive = source; opposite signs = saddle (one leading-in line, everything else exits); complex a ± iω = spiral (sink if a < 0, source if a > 0); pure imaginary = center (closed orbits, e.g. y = sin t circle for y″ + y = 0).
- **Linearization and stability in 2D/3D (3.3)**: near a steady state, replace f by its Jacobian matrix A; eigenvalues from λ² − Tλ + D = 0 (T = trace, D = determinant) — stable when Re λ < 0 (T < 0, D > 0 in 2D); nonlinear stability follows linear when hyperbolic.
- **Euler methods (3.4)**: Y_{n+1} = Yn + Δt·f(tn, Yn), first-order accuracy (global error ∝ Δt); backward Euler (implicit, uses f at n+1) more stable; higher equations reduce to first-order systems y = (y, y′).
- **Runge-Kutta (3.5)**: fourth-order RK uses f four times per step; error ÷16 when Δt halved; stability windows: Euler needs aΔt > −2, improved Euler −2.8ish, RK −2.78 (for y′ = ay, a < 0) — beyond that the numerical solution explodes even though the true one decays.

## Key Concepts
- Isoclines organize direction fields without solving.
- Steady state + eigenvalues = complete local qualitative picture; the trace-determinant parabola T² − 4D separates nodes from spirals, D < 0 gives saddles.
- Center (undamped, B = 0) is the borderline: nonlinear terms decide — not structurally stable.
- Every higher-order ODE becomes a first-order system (the standard form for both theory and codes).
- Numerical stability is a step-size condition on aΔt: explicit methods have finite stability regions; implicit (backward Euler) trades work for unconditional decay capture.
- Accuracy orders: Euler 1, improved 2, RK4 4 — cost per step vs error reduction.

## Mental Models
- "Linearize to know the neighborhood": the Jacobian at the equilibrium is the local truth (hyperbolic case) — the shelf's standard stability reflex.
- "Trace and determinant read the phase portrait": T < 0 & D > 0 stable; D < 0 saddle; T² < 4D spirals — a 2×2 decision tree memorized once.
- "The computer obeys a different stability law than the physics": aΔt inside the method's stability region, or the simulation lies.
- "Halve the step, gain 16×": RK4's fourth-order payoff.

## Anti-patterns
- **Trusting a center from linearization**: pure imaginary eigenvalues are inconclusive for the nonlinear system (borderline case).
- **Explicit Euler with Δt too large on stable systems**: numerical explosion (aΔt < −2) misdiagnosed as physical instability.
- **Classifying nonlinear stability from the wrong point**: linearize at the steady state, not globally.
- **Confusing isoclines with solution curves**: an isocline is a solution only when its slope equals the constant f-value.

## Reference Tables
### 2×2 phase portrait decision (λ² − Tλ + D = 0)
| Condition | Type | Stable? |
|---|---|---|
| D < 0 | saddle | no |
| D > 0, T² − 4D ≥ 0, T < 0 | sink (node) | yes |
| D > 0, T² − 4D ≥ 0, T > 0 | source | no |
| D > 0, T² − 4D < 0, T < 0 | spiral sink | yes |
| D > 0, T² − 4D < 0, T > 0 | spiral source | no |
| T = 0, D > 0 | center | borderline |

### Numerical methods
| Method | Order | Error per Δt halving | Stability (y′=ay, a<0) |
|---|---|---|---|
| Euler | 1 | ÷2 | aΔt > −2 |
| Improved Euler | 2 | ÷4 | wider |
| RK4 | 4 | ÷16 | aΔt > −2.78 |

## Key Takeaways
Qualitative solution = steady states + linearization + eigenvalue signs.
The trace-determinant plane is a complete classifier for 2D linearized systems.
First-order system form unifies theory, phase portraits, and numerical codes.
Numerical stability is its own condition on aΔt — choose the method and step accordingly.
RK4 is the workhorse: 4 evaluations, fourth-order accuracy.

## Connects To
Ch2's characteristic roots are the 1×1/2×2 prototype of this chapter's eigenvalue stability; ch6 generalizes eigenvalues to n×n (stability of y′ = Ay); ch7's boundary-value problems need the same classification for existence. On the control shelf: linearization at operating points, pole locations in the left half-plane, and the aΔt stability limits behind simulation step sizes in every OpenMAIC sim widget and MATLAB ode45 usage.
