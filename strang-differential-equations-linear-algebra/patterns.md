# Patterns — Strang Differential Equations and Linear Algebra

## Pattern: Null + particular split
**Context:** Any inhomogeneous linear problem (y′ = ay + q, Ax = b, BVP).
**Solution:** Solve the homogeneous problem for the free constants; find one particular solution (often with the convention Yp(0) = 0 or free vars = 0); add.
**Consequence:** Initial conditions and inputs live in separate accounts; the same affine picture repeats across the book.

## Pattern: Roots are modes
**Context:** Constant-coefficient ODE or linear system y′ = Ay.
**Solution:** Substitute e^{st} (or e^{λt}x); the characteristic polynomial's roots give the time behaviors; superpose with constants from initial data.
**Consequence:** Stability = left-half-plane roots; ζ/ωn classify second order; eigenvalues generalize to n dimensions.

## Pattern: Impulse response + convolution
**Context:** Forced linear system at rest.
**Solution:** Solve once for the unit impulse (g); answer any forcing by ∫g(t−s)f(s)ds; transform to H(s)F(s).
**Consequence:** One function answers all inputs; transfer function is its transform — the control-shelf bridge.

## Pattern: Linearize, then read eigenvalues
**Context:** Nonlinear system near a steady state.
**Solution:** Jacobian A at the equilibrium; classify by trace/determinant (2D) or Re λ signs; hyperbolic ⟹ nonlinear stability follows.
**Consequence:** No closed-form solution needed; phase portrait from two numbers in 2D.

## Pattern: Elimination as structure finder
**Context:** Solvability, rank, inverses, determinants.
**Solution:** A = LU (or PA = LU); pivots count rank; free variables parametrize the nullspace; consistency = b orthogonal to left-nullspace relations.
**Consequence:** One algorithm answers existence, count, and the four subspaces.

## Pattern: Project when inconsistent
**Context:** More measurements than unknowns (Ax = b unsolvable).
**Solution:** Normal equations AᵀAx̂ = Aᵀb; error ⊥ C(A); x̂ = A⁺b via SVD when rank-deficient.
**Consequence:** AᵀA (symmetric positive (semi)definite) becomes the working matrix; fitting = geometry.

## Pattern: Diagonalize to decouple
**Context:** Coupled linear dynamics or quadratic energies.
**Solution:** Find eigen/singular vectors; change coordinates (V⁻¹AV = Λ, QᵀAQ = Λ, UEVᵀ); dynamics become independent scalars.
**Consequence:** e^{At} = Ve^{Λt}V⁻¹; normal modes; PCA/SVD of data; Fourier = the infinite-dimensional case.

## Pattern: Discretize physics, get AᵀA
**Context:** Heat, springs, networks, Laplace's equation.
**Solution:** Finite differences with boundary conditions; the stiffness/Laplacian matrix is symmetric positive definite, often an incidence product AᵀA.
**Consequence:** Energy methods, Cholesky solves, and least squares all apply to the continuum problem.

## Pattern: Transform to algebra
**Context:** Linear ODE/PDE with simple inputs.
**Solution:** Laplace (initial-value, s replaces d/dt) or Fourier (periodic/eigenfunction expansion); solve algebraically; transform back (partial fractions, coefficient matching).
**Consequence:** Convolution ↔ multiplication; H(s) rational ⟺ finite-dimensional system.

## Pattern: Step-size stability is its own law
**Context:** Numerical integration of stable systems.
**Solution:** Check aΔt against the method's stability region (Euler −2, RK4 −2.78); implicit methods trade cost for unconditional decay.
**Consequence:** Simulations can explode where the physics decays — diagnose numerics before physics.
