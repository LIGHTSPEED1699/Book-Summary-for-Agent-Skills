# Cheatsheet — Vector Calculus, Linear Algebra and Differential Forms (Hubbard & Burke Hubbard, 5th ed.)

## Decision procedures

### Classify a critical point (3.6/3.7)
1. Solve Df(a) = 0 (or Lagrange: Df = λDG).
2. Form the Hessian (of f, or of f − λG).
3. Reduce the quadratic form to squares (complete squares / eigenvalues).
4. Signature (k,0) min, (0,k) max, mixed saddle, degenerate → higher order.
Constrained: restrict the form to ker DG(a) first (3.7.13).

### Newton with guarantee (2.8/2.9)
1. β = ‖[Df(x0)]^{-1}‖, γ = Lip(Df) near x0, η = ‖f(x0)‖.
2. h = βγη ≤ ½ (sharper variants 2.9.8) ⟹ zero exists, Newton converges.
3. Error: ‖x_{k+1} − x‖ ≤ C‖x_k − x‖² — digits double.

### Integrate over a manifold (5.3/6.2/6.4)
1. Parametrize (overlaps allowed, boundaries measure zero).
2. Flat piece volume: √det(DγᵀDγ) dᵏt (scalar integrals) or pull the form back (form integrals).
3. Sum/integrate over parameter domain; orientation matters for forms.

### Change variables (4.10)
∫_T f(x) dⁿx = ∫_S f(T(u)) |det DT(u)| dⁿu; T one-to-one off a measure-zero set.

### Is a field a gradient / does a potential exist? (6.8/6.13)
1. Check closed: dω = 0 (curl F = 0).
2. Domain star-shaped/contractible ⟹ exact: ω = df (Poincaré 6.13.5).
3. Not contractible ⟹ test periods around holes (∮ ω ≠ 0 obstructs).

### Integrability (4.3/4.4)
Bounded on a rectangle + discontinuity set measure zero ⟺ integrable.
Curves/surfaces in Rⁿ: measure zero — boundaries never obstruct.

## Key formulas
| Object | Formula |
|---|---|
| Derivative | f(a+h) = f(a) + Df(a)h + o(‖h‖) |
| Chain rule | D(g∘f)(a) = Dg(f(a))Df(a) |
| MVT bound | ‖f(b)−f(a)‖ ≤ sup_[a,b]‖Df‖ · ‖b−a‖ |
| Taylor 2 | f(a+h) ≈ f(a) + Df h + ½ hᵀ[Hf]h |
| Dimension formula | dim ker T + dim im T = n |
| Change of basis | [T]_new = B^{-1}[T]B |
| Gram volume | vol_k² = det[vi·vj] |
| Manifold volume | ∫ √det(DγᵀDγ) dᵏt |
| Surface area (R³) | ∫ ‖∂₁γ × ∂₂γ‖ dA |
| Gauss curvature | K = κ1κ2 = det(dN) |
| Stokes | ∫_S dφ = ∫_∂S φ |
| Graded Leibniz | d(φ∧ψ) = dφ∧ψ + (−1)^p φ∧dψ |
| Maxwell | dF = 0, d*F = J |

## Forms ↔ vector calculus (R³)
| k-form | Field | d | Identity |
|---|---|---|---|
| 0 f | scalar | df | grad |
| 1 ω | F | dω | curl |
| 2 ψ | F (flux) | dψ | div |
| — | — | d² = 0 | curl grad = 0, div curl = 0 |

## Numerical integration
| Method | Best for | Rate |
|---|---|---|
| Simpson | smooth, low-dim | O(h⁴) |
| Gaussian quadrature | smooth, weighted | exact deg 2m−1 |
| Monte Carlo | high-dim | O(N^{-1/2}) dim-free |

## Five big theorems (1.6)
Bolzano-Weierstrass · extreme value · intermediate value · uniform continuity on compacta · curves have area zero (Peano caveat: needs more than continuity).

## Quick identities
- Perron-Frobenius: positive A ⟹ ρ(A) eigenvalue, positive eigenvector, powers align.
- SVD: A = VDU*; covariance axes = V, variances = σ².
- det as volume: |det A| = parallelepiped volume; change-of-variables factor.
- DCT: |f_k| ≤ g integrable ⟹ lim ∫ = ∫ lim.
- Kantorovich h = βγη ≤ ½.
