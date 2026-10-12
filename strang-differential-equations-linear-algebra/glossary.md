# Glossary — Strang Differential Equations and Linear Algebra

**complete solution** — null solution + particular solution (y = Ce^{at} + Yp; x = x_n + v_p); the affine family solving an inhomogeneous linear problem.
**characteristic equation** — polynomial from substituting y = e^{st}: As² + Bs + C (second order) or det(A − λI) (systems); its roots are the modes.
**impulse response g(t)** — solution at rest with unit kick; every forced response is the convolution ∫g(t−s)f(s)ds; its transform is the transfer function.
**transfer function H(s)** — Laplace transform of g; output = H(s)·input in the s-domain; poles = characteristic roots.
**damping ratio ζ / natural frequency ωn** — ζ = B/√(4AC), ωn = √(C/A); roots −ζωn ± iωn√(1−ζ²); organizes second-order behavior (under/critical/overdamped).
**resonance** — forcing at a characteristic root; response grows (linearly undamped, unbounded at exact pole).
**isocline** — curve where f(t,y) = const in a direction field; all solution curves cross it with the same slope.
**sink / source / saddle / spiral / center** — phase-plane types from eigenvalue signs: stable node / unstable node / mixed signs / complex with Re ≠ 0 / pure imaginary borderline.
**linearization** — replace nonlinear f by Jacobian A at a steady state; local stability = eigenvalue test when hyperbolic.
**Euler method** — Y_{n+1} = Yn + Δt f(tn, Yn); first order; stability needs aΔt > −2; **backward Euler** implicit variant; **RK4** fourth order, ÷16 error per halving.
**row picture / column picture** — equations as hyperplanes vs b as a combination of columns; the column view generalizes.
**elimination / LU** — forward elimination to U with multipliers stored in L; pivots nonzero; PA = LU with exchanges.
**rank r** — number of pivots = independent columns = independent rows; the true equation count.
**column space C(A) / nullspace N(A)** — all Ax; all solutions of Ax = 0; dimensions r and n − r.
**four fundamental subspaces** — C(A), N(A), C(Aᵀ), N(Aᵀ) with dims r, n−r, r, m−r; orthogonal pairs (fundamental theorem).
**special solutions** — nullspace basis from free variables (one free var = 1, rest 0).
**eigenvalue / eigenvector** — Ax = λx; λ from det(A − λI) = 0; distinct λ ⟹ independent x.
**diagonalization** — A = VΛV⁻¹ when n independent eigenvectors exist; powers and exponentials become scalar per mode.
**matrix exponential e^{At}** — Ve^{Λt}V⁻¹; solution operator of y′ = Ay; commutes split only if AB = BA.
**stability (systems)** — all Re λ(A) < 0; 2×2 shortcut: trace < 0 and det > 0.
**Markov matrix** — columns sum to 1; λ = 1 steady state, convergence when the rest are inside the unit circle.
**spectral theorem** — symmetric A = QΛQᵀ: real eigenvalues, orthonormal eigenvectors.
**normal modes** — eigenvector shapes of M y″ = −Ky; frequencies ω² = eigenvalues.
**least squares x̂** — minimizer of ‖Ax − b‖²; normal equations AᵀAx̂ = Aᵀb; error ⊥ column space.
**projection p = Ax̂** — closest point of C(A) to b.
**positive definite** — xᵀAx > 0; tests: pivots > 0, leading minors > 0, eigenvalues > 0; AᵀA is semidefinite always.
**SVD** — A = UEVᵀ with U, V orthogonal, σ₁ ≥ … ≥ 0; V eigenvectors of AᵀA; ‖A‖ = σ₁; pseudoinverse A⁺ = VE⁺Uᵀ.
**graph Laplacian** — AᵀA of an incidence matrix; networks, conservation, diffusion.
**boundary value problem** — conditions at both ends; discretizes to symmetric positive definite systems (vs initial-value flow).
**Fourier series** — u = Σcₖe^{ikx}; eigen-expansion of the derivative operator; smoothness ↔ coefficient decay.
**FFT** — fast DFT via roots of unity; F² = NP, F⁴ = N²I; N log N.
**heat equation / heat kernel** — uₜ = cu_xx; modes decay e^{−ck²t}; kernel e^{−x²/4ct}/√(4πct) = point-source response.
**wave equation / d'Alembert** — u_tt = c²u_xx; f(x+ct) + g(x−ct); energy conserved.
**Laplace transform** — Y(s) = ∫e^{−st}y dt; y′ → sY − y(0); ODEs become algebra.
**convolution** — (c*d)ₙ = Σcₖdₙ₋ₖ; transform of products ↔ convolution of transforms; circulant matrices diagonalized by F.
