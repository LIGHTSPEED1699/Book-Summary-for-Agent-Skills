# Cheatsheet — Differential Equations and Linear Algebra (Strang, 2014)

## Decision procedures

### Solve y′ = ay + q(t)
1. Yn = Ce^{at} (C from y(0)).
2. Yp = ∫₀ᵗ e^{a(t−s)}q(s)ds (or undetermined coefficients for q = e^{st}, sin, poly).
3. y = Yn + Yp.

### Second order Ay″ + By′ + Cy = 0
1. Roots of As² + Bs + C = 0.
2. Real distinct → c1e^{s1t} + c2e^{s2t}; equal → (c1 + c2t)e^{st}; complex a ± iω → e^{at}(C1cosωt + C2sinωt).
3. Stable ⟺ Re s < 0 ⟺ (A,B,C same sign, 2nd order).
4. ζ = B/√(4AC), ωn = √(C/A); ωd = ωn√(1−ζ²).

### Classify 2D steady state (Jacobian A)
1. λ² − Tλ + D = 0 (T = tr, D = det).
2. D < 0 saddle; D > 0 & T < 0 stable (node if T² ≥ 4D, spiral if <); T > 0 unstable; T = 0 center (borderline).

### Solve/count Ax = b
1. Eliminate: A = LU; count pivots r.
2. r = n: unique. r < n & b consistent: n − r parameters. Inconsistent (a left-null combination gives 0 = nonzero): no solution → least squares.
3. Complete solution: v_p + special solutions.

### Least squares
1. Independent columns: AᵀAx̂ = Aᵀb.
2. Rank-deficient: x̂ = A⁺b via SVD (minimum-norm).
3. Error E = ‖b − Ax̂‖²; check e ⊥ columns.

### Solve y′ = Ay
1. Eigenvalues/vectors of A; if diagonalizable: y = Σcᵢe^{λᵢt}xᵢ, c from y(0) = Vc.
2. e^{At} = Ve^{Λt}V⁻¹; defective: t^k e^{λt} terms.
3. Stable ⟺ all Re λ < 0.

### Numerical step choice
1. y′ = ay stable (a < 0): need aΔt > −2 (Euler), −2.78 (RK4).
2. Accuracy: Euler ÷2, improved ÷4, RK4 ÷16 per halving.

## Key formulas
| Object | Formula |
|---|---|
| Yp (constant a) | ∫₀ᵗ e^{a(t−s)}q(s)ds |
| e^{it} | cos t + i sin t |
| Fundamental solution g | Ag″+Bg′+Cg = δ, g(0)=0, g′(0)=1/A |
| Convolution output | y = ∫g(t−s)f(s)ds |
| Transfer function | H(s) = 1/(As²+Bs+C) |
| Impedance RLC loop | Z = iwL + R + 1/(iwC) |
| 2×2 inverse | A⁻¹ = (1/det)[[d,−b],[−c,a]] |
| (AB)⁻¹ / (AB)ᵀ | B⁻¹A⁻¹ / BᵀAᵀ |
| Rank count | dim N(A) = n − r |
| det & eigenvalues | det A = Πλ = Πpivots; tr = Σλ |
| Normal equations | AᵀAx̂ = Aᵀb |
| Pseudoinverse | A⁺ = VE⁺Uᵀ |
| Heat modes | e^{−c(kπ/L)²t}sin(kπx/L) |
| Heat kernel | e^{−x²/4ct}/√(4πct) |
| d'Alembert | ½[u₀(x+ct)+u₀(x−ct)] + (1/2c)∫v₀ |
| FFT structure | F² = NP, F⁴ = N²I |
| Laplace derivative | L{y′} = sY − y(0) |

## Stability quick table
| System | Stable when |
|---|---|
| y′ = ay | a < 0 |
| Ay″+By′+Cy=0 | roots Re < 0 (B, C same sign as A) |
| y′ = Ay | all Re λ(A) < 0 |
| 2×2 y′ = Ay | tr < 0 and det > 0 |
| Discrete u_{k+1} = Cu_k | all |λ(C)| < 1 |
| Euler on a < 0 | aΔt > −2 |

## Subspace dimensions (m×n, rank r)
C(A): r · N(A): n−r · C(Aᵀ): r · N(Aᵀ): m−r; C(A) ⊥ N(Aᵀ), N(A) ⊥ C(Aᵀ).

## Positive definite tests
pivots > 0 ⟺ leading minors > 0 ⟺ λ > 0 ⟺ xᵀAx > 0 ⟺ A = LDLᵀ, dᵢ > 0.

## Transform pairs
| Time | s-domain |
|---|---|
| δ(t) | 1 |
| 1 (step) | 1/s |
| e^{at} | 1/(s−a) |
| cos ωt | s/(s²+ω²) |
| sin ωt | ω/(s²+ω²) |
| ∫₀ᵗ f | F(s)/s |
| f * g | F(s)G(s) |
