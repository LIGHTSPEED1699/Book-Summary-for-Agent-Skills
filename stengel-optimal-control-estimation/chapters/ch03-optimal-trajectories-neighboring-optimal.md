# Chapter 3: Optimal Trajectories and Neighboring-Optimal Solutions

## Core Idea
Solve the deterministic trajectory problem once (calculus of variations → minimum principle → HJB), then linearize *around the optimal trajectory* and a single time-varying Riccati feedback law keeps perturbed systems neighboring-optimal — the bridge from open-loop trajectories to feedback control.

## Frameworks Introduced
- **Problem statement (3.1)**: minimize J = Φ(x(t_f), t_f) + ∫Ψ(x,u,w,p,t)dt subject to ẋ = f(x,u,w,p,t); cost types: **Mayer** (terminal only), **Lagrange** (integral only), **Bolza** (both) — interconvertible.
- **Cost function design (3.2)**: minimum time (Ψ = 1), minimum fuel/energy (weighted ‖u‖²), terminal error penalties, tradeoffs — the shape of J dictates the solution's character.
- **Parametric optimization (3.3)**: fix u(t) = Σcᵢφᵢ(t) shape functions, optimize coefficients cᵢ by static methods (Lagrange multipliers for endpoint constraints); no optimality guarantee, but works when control shape is known a priori; gradient and Newton variants.
- **Necessary conditions (3.4)**: augment with costate λ: Hamiltonian **H = Ψ + λᵀf**; extremals satisfy ẋ = ∂H/∂λ, **λ̇ = −∂H/∂x**, **∂H/∂u = 0**; **transversality** λ(t_f) = ∂Φ/∂x (+ multiplier terms for terminal constraints); Weierstrass-Erdmann corner conditions; two-point boundary value problem (TPBVP).
- **Sufficient conditions**: Weierstrass E-function ≥ 0; **Legendre-Clebsch** ∂²H/∂u² ≥ 0 along the extremal.
- **Pontryagin Minimum Principle (3.4)**: for bounded u, the optimal control *minimizes* H over the admissible set (not ∂H/∂u = 0) — bang-bang structure when H is linear in u.
- **Hamilton-Jacobi-Bellman (3.4)**: S(x,t) value function; −∂S/∂t = min_u[H + Sᵀ_x f]; optimal feedback u° = argmin H; dynamic programming is the global version — costate λ = ∇S.
- **Constraints (3.5)**: terminal equality ψ(x(t_f)) = 0 (extra multipliers in transversality); isoperimetric integral constraints; state/control inequality constraints (costate jumps at entry/arc structure); **singular control**: when ∂²H/∂u² = 0 on an interval (H linear in u with vanishing switching function), use **generalized Legendre-Clebsch** (−1)^k d^{2k}/dt^{2k}(∂H/∂u)·(−1)^k ≥ 0 for minimization; classic: minimum-fuel with bounded thrust = bang-singular-bang.
- **Numerical methods (3.6)**: penalty functions; dynamic programming on grids (curse of dimensionality); **neighboring extremal** (linearized TPBVP); **quasilinearization** (Newton on the TPBVP — quadratic convergence when close); gradient methods (steepest descent in u with step control).
- **Neighboring-optimal feedback (3.7)**: perturb the extremal; the linearized TPBVP solved with **Riccati gain S(t)**: δu = −S(t)δx (+ feedforward for disturbances); continuous LQ differential Riccati Ṡ = −SF − FᵀS + SGQ⁻¹GᵀS − Q̃; discrete-time version for digital implementation; **small-disturbance/parameter-variation robustness**: the same law handles off-nominal conditions near the trajectory.

## Key Concepts
- **Costate λ**: shadow price of the state (Lagrange multiplier density along trajectory); λ = ∇_x S in HJB language.
- **Switching function**: ∂H/∂u; its sign (or zeros) determines bang-bang/singular structure.
- **TPBVP**: state forward + costate backward + boundary conditions — the computational core.
- **Singular arc**: control determined by higher-order conditions, not ∂H/∂u = 0.
- **Neighboring-optimal law**: one Riccati sweep around the nominal trajectory = feedback valid for the whole perturbation family.
- **Quasilinearization**: Newton's method lifted to functionals.

## Mental Models
- "Optimize once, regulate locally": the trajectory is open-loop optimal; the neighboring-optimal Riccati gain is what makes it survive reality.
- "The costate prices the states": λ tells you what one more unit of each state is worth at the end — that's why ∂H/∂u = 0 balances control cost against state value.
- "H linear in u ⇒ bang-bang or singular": the Hamiltonian's u-structure predicts the control's time structure before any computation.
- "Parametric optimization is shape-function guess + coefficient fit": fine when you know the shape, silently wrong when you don't.

## Anti-patterns
- **Trusting parametric optimization as truly optimal**: shape functions bound the answer; no necessary-condition check.
- **Applying ∂H/∂u = 0 under control saturation**: use the Minimum Principle — stationarity is replaced by H-minimization over the admissible set.
- **Missing singular arcs**: minimum-fuel/bounded-thrust problems have them; the naive bang-bang answer is wrong (check Legendre-Clebsch).
- **Dynamic programming for high-dimensional states**: grid explosion; use neighboring-extremal or quasilinearization instead.
- **Re-solving the full TPBVP for every disturbance**: the neighboring-optimal gain handles small perturbations — compute it once.

## Reference Tables

### Optimality condition ladder
| Condition | Statement | Use |
|---|---|---|
| ∂H/∂u = 0 | stationarity | unconstrained interior |
| Minimum Principle | u° minimizes H | bounded u |
| Legendre-Clebsch | ∂²H/∂u² ≥ 0 | sufficiency/min check |
| Gen. Legendre-Clebsch | (−1)^k d^{2k}/dt^{2k}(∂H/∂u) ≥ 0 | singular arcs |
| HJB | S solves PDE; u° = argmin H | global feedback |

### Numerical trajectory methods
| Method | Mechanism | Caveat |
|---|---|---|
| Parametric | shape functions + static opt | not guaranteed optimal |
| Penalty | constraint → cost weight | ill-conditioning as weight → ∞ |
| Dynamic programming | grid on S(x,t) | dimension curse |
| Neighboring extremal | linearized TPBVP | small perturbations |
| Quasilinearization | Newton on TPBVP | needs good initial guess |
| Gradient | descent in u | slow, robust |

## Key Takeaways
1. The deterministic optimum is a TPBVP: state + costate + boundary conditions; the Hamiltonian organizes everything.
2. Control structure (smooth/bang-bang/singular) is read off the Hamiltonian's dependence on u before solving.
3. HJB/dynamic programming gives the global feedback view; the costate is the value-function gradient.
4. Neighboring-optimal design converts one trajectory into a time-varying Riccati feedback — the conceptual ancestor of LQR.
5. Numerical choice follows problem size: parametric for known shapes, quasilinearization for sharp trajectories, gradient for robustness of convergence.

## Connects To
- **Ch 2**: Lagrange multipliers, transition matrices, TPBVP machinery.
- **Ch 4**: estimation needed because x isn't measurable — the other half of the loop.
- **Ch 5**: stochastic version of neighboring-optimal control.
- **Ch 6**: LTI + LQ specialization where the Riccati equation goes algebraic.
