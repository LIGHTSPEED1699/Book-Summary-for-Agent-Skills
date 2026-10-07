# Chapter 2: The Mathematics of Control and Estimation

## Core Idea
One mathematical toolkit — vectors/matrices with weighted norms, eigen-structure as "modes of motion," state-space solutions via transition matrices, second-order statistics of random processes, and the classical frequency-domain view — underwrites every later chapter; each section is the numerically equivalent prep for its chapter (2.3→Ch 3, 2.4→Ch 4-5, 2.5-2.6→Ch 6).

## Frameworks Introduced
- **2.1 Static optimization groundwork**: vector/matrix algebra, inner/outer products, **weighted norms** ‖x‖²_Q = xᵀQx (the cost-function geometry); stationary points via ∂J/∂x = 0 with ∂²J/∂x² positive definite for minimum; **constrained minima via Lagrange multipliers**: minimize J(x) s.t. f(x) = 0 → ∇J + λᵀ∇f = 0 — the multiplier is the shadow price of the constraint, reused for trajectory optimization in Ch 3.
- **2.2 Matrix machinery**: determinant, adjoint, inverse; **generalized/pseudoinverse** for over/underdetermined systems; similarity transformations (eigenvalue-preserving coordinate changes); matrix calculus (d/dt of matrices, ∂(xᵀAx)/∂x = (A + Aᵀ)x); **eigenvalues/eigenvectors** (diagonalization A = TΛT⁻¹, modal coordinates); **SVD** A = UΣVᵀ (gain directions — the robustness language of Ch 6.5); determinant identities (matrix lemma used in recursive estimators).
- **2.3 Dynamic models & solutions**: nonlinear ẋ = f(x,u,t) with **local linearization** via Jacobians F = ∂f/∂x, G = ∂f/∂u; linear solution x(t) = Φ(t,t₀)x₀ + ∫Φ(t,τ)G(τ)u(τ)dτ with **state transition matrix** Φ̇ = FΦ, Φ(t,t) = I; LTI: Φ(t) = e^{F(t−t₀)}; numerical integration (Runge-Kutta; discrete transition Φ ≈ e^{Fh} or series); data representation (sampled signals).
- **2.4 Random variables/sequences/processes**: pdf, mean, variance, covariance; random sequences and processes; **correlation/covariance functions**; **white noise** (flat spectrum, δ-correlated); spectral densities (Wiener-Khinchin); special densities (Gaussian — everything later assumes it); multivariate statistics. Rule: a random process is characterized by its first two moments when Gaussian.
- **2.5 System properties**: static and **quasistatic equilibrium** (slowly varying equilibrium used for trajectory design); **stability**: eigenvalue test (Re λ(F) < 0 asymptotic; discrete: |λ| < 1), Lyapunov direct method with quadratic V = xᵀPx (FᵀP + PF = −Q); **modes of motion** — response decomposes into eigenvector-weighted modes, each with time constant −1/Re λ and frequency Im λ; **controllability** rank[F^{n−1}G | … | G] = n, **stabilizability** (uncontrollable modes stable); **observability** rank observability matrix = n, **detectability**; discrete-time parallels (z-plane, Φ_d = e^{Fh}).
- **2.6 Frequency domain**: transfer function G(s) = H(sI − F)⁻¹G + L; **root locus** (closed-loop poles vs gain); **Bode plots** with gain/phase margins; **Nyquist criterion** (encirclements of −1 = open-loop RHP poles − closed-loop RHP poles); **effects of sampling**: z = e^{sT}, frequency wrap at Nyquist, computational delay ≈ extra phase lag; rule of thumb: sample fast enough that the mode of interest is well within the Nyquist frequency.

## Key Concepts
- **Weighted norm / quadratic form**: cost functions are weighted norms; the weighting matrices *are* the design spec.
- **Lagrange multiplier**: constraint's marginal cost; becomes the costate in Ch 3.
- **Mode of motion**: each eigenvalue/eigenvector pair is a natural behavior (decay rate + frequency); controllers reshape modes, estimators add observer modes.
- **State transition matrix**: the system's complete free-response memory; e^{Fh} bridges continuous and discrete.
- **Second-order characterization**: means + covariances suffice for Gaussian linear analysis — the Kalman filter's whole input language.
- **Controllability/observability rank tests**: Kalman decompositions; stabilizable/detectable are the usable weakenings.
- **Margins**: GM/PM from Bode; Nyquist gives the MIMO generalization (distance to −1).

## Mental Models
- "Eigenvalues are the budget, eigenvectors are the allocation": performance specs translate to mode placement; eigenvector freedom is a design resource (Ch 6.4).
- "Cost = weighted norm, dynamics = constraint, optimum = Lagrange": the static picture of 2.1 literally becomes Ch 3's multiplier method.
- "Gaussian + linear ⇒ moments close": propagate mean and covariance and you know everything (Ch 4).
- "Discrete is continuous sampled": z = e^{sT}; every s-plane concept has a z-plane twin, with Nyquist wrap as the tax.

## Anti-patterns
- **Linearizing outside the valid region**: Jacobian models are local; large-signal behavior (weathervane sin θ) needs the nonlinear model.
- **Applying rank tests to near-decomposable systems**: numerical rank ≠ structural rank; nearly-uncontrollable modes masquerade until they destabilize.
- **Ignoring sampling delay in the loop**: computation + zero-order hold eat phase margin exactly like extra delay.
- **Treating white noise as physically real**: it's a flat-spectrum idealization valid below the sample rate; continuous-time white noise has infinite power (use spectral density).

## Reference Tables

### Section → chapter support map
| Section | Feeds |
|---|---|
| 2.1 static optimization, Lagrange | Ch 3 |
| 2.2 matrices, eigen, SVD | Ch 3, 6 |
| 2.3 dynamic models, transition matrices | Ch 3, 4 |
| 2.4 random processes | Ch 4, 5 |
| 2.5 stability, controllability, observability | Ch 5, 6 |
| 2.6 frequency domain | Ch 6 |

### Stability tests
| Setting | Test |
|---|---|
| LTI continuous | Re λ(F) < 0 |
| LTI discrete | \|λ(Φ)\| < 1 |
| Lyapunov direct | ∃P > 0: FᵀP + PF = −Q < 0 |
| Nonlinear | linearize (indirect) unless V found directly |

## Key Takeaways
1. The book's math is deliberately self-contained: weighted norms + Lagrange multipliers (2.1) reappear as cost functions + costates.
2. Modes of motion are the atomic units of dynamic behavior; design = reshaping modes within controllability/observability limits.
3. Gaussian second-order statistics make estimation a covariance-propagation problem — the Kalman filter needs nothing more.
4. Controllability/observability rank tests decide what can be controlled/observed; stabilizability/detectability decide what you can get away with not controlling/observing.
5. Frequency-domain tools remain the interpretation layer for LTI designs — margins and Nyquist distance quantify what the Riccati solution bought (Ch 6.5).

## Connects To
- **Ch 3**: Lagrange multipliers → calculus of variations; transition matrices → trajectory optimization.
- **Ch 4**: random processes → optimal estimation.
- **Ch 5**: stability + statistics → stochastic regulator.
- **Ch 6**: eigen/SVD/Nyquist → multivariable design and robustness.
