---
name: strang-differential-equations-linear-algebra
description: Apply Gilbert Strang's Differential Equations and Linear Algebra (2014, Wellesley-Cambridge) frameworks - the Yn+Yp solution split, characteristic roots as modes, impulse response and transfer functions, phase-plane stability, elimination and the four fundamental subspaces, eigenvalues e^{At}, least squares A^TA, SVD, Fourier/FFT and Laplace transforms - when solving ODEs, analyzing linear dynamical systems, fitting data, or connecting differential equations to linear algebra.
---

# Strang: Differential Equations and Linear Algebra (2014)

Gilbert Strang's 18.06 book unifies the differential-equations course with linear algebra: every ODE idea has a matrix twin (null + particular solutions, characteristic roots → eigenvalues, convolution → matrix exponential, Fourier → diagonalization). Use this skill when solving or analyzing linear systems, continuous or discrete, and when the control-shelf books (Skogestad, Stengel, Åström) need their ODE/linear-algebra foundations made explicit.

## When to use
- Solving first/second-order ODEs, or systems y′ = Ay; stability questions (roots, eigenvalues, trace-determinant).
- Transfer functions, impulse responses, convolution, resonance, damping ratio ζ and natural frequency ωn.
- Least squares fitting, projections, normal equations, SVD of data matrices.
- Elimination, rank, the four fundamental subspaces, diagonalization, matrix exponentials e^{At}.
- Fourier series/FFT, heat/wave equations, Laplace transforms and H(s) algebra.

## Files
- `chapters/ch01-first-order-equations.md` — y′ = ay + q, Yn + Yp, exponentials, logistic, separable
- `chapters/ch02-second-order-equations.md` — characteristic roots, ζ/ωn, impulse response, transfer function, impedance
- `chapters/ch03-nonlinear-stability.md` — phase plane, sink/source/saddle/spiral, linearization, Euler/RK4
- `chapters/ch04-linear-equations-inverse-matrices.md` — two pictures, elimination LU, inverses, symmetric/orthogonal
- `chapters/ch05-vector-spaces-subspaces.md` — column/nullspace, rank, complete solution, four fundamental subspaces, networks
- `chapters/ch06-eigenvalues-eigenvectors.md` — diagonalization, y′ = Ay, e^{At}, spectral theorem, normal modes
- `chapters/ch07-applied-math-ata.md` — least squares, positive definite, SVD, BVPs, graph Laplacian
- `chapters/ch08-fourier-laplace.md` — Fourier series, FFT, heat/wave, Laplace transform, convolution
- `chapters/appendix-determinants-factorizations.md` — determinant rules, factorization zoo
- `glossary.md` · `patterns.md` · `cheatsheet.md`

## The book in one paragraph
Solve y′ = ay + q as Ce^{at} + ∫e^{a(t−s)}q(s)ds; second order adds the characteristic polynomial whose roots are the modes (ζ, ωn organize them); nonlinear stability = linearize + eigenvalue signs; the matrix half (elimination → rank → subspaces → eigenvalues → SVD) is the same story in finite dimensions: null + particular, modes and stability (Re λ < 0), and AᵀA/least squares as the applied heart; Fourier and Laplace diagonalize the operators and turn calculus into algebra.

## Start here
- Dynamics problem → `ch02` (roots, ζ, transfer function) then `ch06` (e^{At}, eigen-modes).
- Data/fitting → `ch07` (least squares, SVD).
- Structure question (solvability, dimension) → `ch04` + `ch05`.
- Qualitative/nonlinear → `ch03`.
- Signals/PDEs → `ch08`.
