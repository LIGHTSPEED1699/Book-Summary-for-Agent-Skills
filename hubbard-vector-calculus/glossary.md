# Glossary — Vector Calculus, Linear Algebra and Differential Forms (Hubbard & Burke Hubbard, 5th ed.)

## Spaces and maps
- **Rⁿ**: points (positions) and vectors (displacements); dot product u·v, length ‖v‖, distance.
- **Linear transformation T: Rⁿ → Rᵐ**: represented by matrix [T]; columns = T(eⱼ).
- **ker T / im T**: kernel (null space) and image (range); dim ker + dim im = n (2.5.8).
- **Basis, change of basis**: [T]_new = B^{-1}[T]B (2.6.20); similarity.
- **Manifold S ⊂ Rⁿ**: locally parametrized k-dimensional set; **T_x S** tangent space.
- **Parametrization γ: U → Rⁿ**: smooth map whose (local) image is the manifold; k-manifold needs k independent partials.

## Calculus
- **Df(a)**: derivative — the unique linear map with f(a+h) = f(a) + Df(a)h + o(‖h‖) (1.7.9).
- **[Jf(a)]**: Jacobian matrix, entries Dⱼfᵢ; the matrix of Df(a) (1.7.10).
- **∇f**: gradient; Df for scalar f via the dot product.
- **C¹**: continuous partial derivatives ⟹ differentiable (1.9.8).
- **Taylor polynomial T_k f(a)**: k-th order polynomial approximation; Hessian [Hf(a)] for k=2.
- **Big-O / little-o**: error bookkeeping (A11).

## Linear algebra
- **Row reduction, pivots, echelon form**: the main algorithm (2.1).
- **Elementary matrix**: row operation as matrix; A invertible ⟺ A = product of elementaries.
- **Eigenvalue/eigenvector**: Tv = λv; characteristic polynomial det(T − λI).
- **Perron-Frobenius** (2.7.10): positive matrix ⟹ dominant real eigenvalue with positive eigenvector.
- **Symmetric matrix / quadratic form** Q(x) = xᵀAx; **signature** (p,q) = (#positive, #negative) squares after congruence (3.5.3).
- **Spectral theorem** (3.7.15): symmetric ⟹ orthogonally diagonalizable.
- **SVD** (3.8.1): A = VDU*, singular values σ1 ≥ … ≥ 0.

## Integration
- **Measure zero**: coverable by boxes of arbitrarily small total volume (4.4); the integrability filter.
- **Integrable**: bounded + discontinuities measure zero (4.3.1/4.4.8).
- **Fubini** (4.5.10): iterated integrals equal.
- **Dominated convergence** (4.11.4): |f_k| ≤ g integrable ⟹ limit through ∫.
- **k-volume of parallelogram**: √det Gram matrix (5.1); **manifold volume density** √det(DγᵀDγ) (5.3).
- **det as volume** (4.8–4.9): |det A| = volume scale; change of variables ∫ f∘T |det DT| (4.10).

## Forms
- **k-form φ**: smooth field of alternating k-linear functionals on tangent spaces; integrates over oriented k-pieces.
- **dx^i1 ∧ … ∧ dx^ik**: standard basis; wedge = antisymmetrized tensor.
- **Orientation**: consistent choice of positive k-frames; orientable manifold; boundary orientation "outward first".
- **Exterior derivative d**: raises degree by 1; d² = 0; graded Leibniz d(φ∧ψ) = dφ∧ψ + (−1)^p φ∧dψ.
- **Pullback f*φ**: substitution for forms; commutes with d.
- **Closed / exact**: dφ = 0 / φ = dψ; Poincaré's lemma (6.13.5): closed ⟹ exact on star-shaped domains.
- **Gauss map N: S → Sⁿ⁻¹**; **Gaussian curvature** K = det(dN); principal curvatures κ1, κ2.

## Numerical
- **Newton's method**: x_{k+1} = x_k − [Df]^{-1}f; **superconvergence**: ‖e_{k+1}‖ ≤ C‖e_k‖².
- **Kantorovich** (2.8.13/2.9.8): β = ‖[Df(x0)]^{-1}‖, γ = Lip(Df), η = ‖f(x0)‖; h = βγη ≤ ½ ⟹ convergence.
