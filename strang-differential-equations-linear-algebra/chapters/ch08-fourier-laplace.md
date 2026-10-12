# Chapter 8: Fourier and Laplace Transforms

## Core Idea
Periodic inputs decompose into eigenfunctions e^{ikx} of the derivative operator; the PDEs of physics (heat, wave) then solve mode by mode — each Fourier mode decays or oscillates at its own rate (e^{-k²t} for heat, e^{iωt} for wave). The FFT makes the decomposition fast (F² = NP, F⁴ = N²I), and the Laplace transform extends the exponential-response idea of ch2 to full transfer-function algebra: Y(s) = H(s)F(s), with convolution in time as the twin.

## Frameworks Introduced
- **Fourier series (8.1)**: periodic u(x) = Σ cₖe^{ikx}; coefficients by orthogonality (inner product with e^{ikx}); real form with aₖcos + bₖsin; smoothness ↔ decay of cₖ; Gibbs phenomenon at jumps.
- **Fast Fourier Transform (8.2)**: DFT matrix F with roots of unity w = e^{2πi/N}; F² = NP (permutation), F⁴ = N²I; FFT splits even/odd coefficients — N log N instead of N²; the butterfly structure.
- **Heat equation (8.3)**: uₜ = cu_xx on a bar: separation of variables u = X(x)T(t) gives X″ = −λX (sines with the boundary conditions) and T′ = −cλT; solution Σ bₖ(0)e^{−λₖt}sin(kπx) — high modes die fast (smoothing); heat kernel e^{−x²/4ct}/√(4πct) on the line = response to a point source, built by superposing e^{ikx}e^{−ck²t} over all k.
- **Wave equation (8.4)**: one-way uₜ = cu_x translates the profile u₀(x+ct); two-way u_tt = c²u_xx: d'Alembert solution (u₀(x+ct) + u₀(x−ct))/2 + integral of v₀; Fourier version with ω = kπc/L from separation of variables; energy conserved (contrast with heat).
- **Laplace transform (8.5)**: Y(s) = ∫₀^∞ e^{−st}y(t)dt turns y′ into sY − y(0): differential equations → algebra; transfer function H(s) = output/input; partial fractions back to time; step and impulse responses.
- **Convolution (8.6)**: (c*d)ₙ = Σcₖdₙ₋ₖ — multiplying functions multiplies coefficients via convolution; multiplication theorem: F(fg) = (Fc)*(Fd) style dualities; cyclic convolution from circulant matrices: (Fc).*(Fd) componentwise.

## Key Concepts
- e^{ikx} are the eigenfunctions of d/dx (eigenvalue ik); of d²/dx² (eigenvalue −k²) — diagonalizing the operator is what Fourier does.
- Heat: modes decay e^{−ck²t} — smoothing, irreversible; wave: modes rotate e^{iωt} — oscillation, reversible. The sign of the operator decides the physics.
- Separation of variables = eigen-expansion of the spatial operator with boundary conditions setting the spectrum (λₖ = (kπ/L)²).
- Heat kernel = continuous superposition of modes; the fundamental solution of ch2 generalized to PDE.
- FFT: roots-of-unity symmetry (F⁴ = N²I) is the computational leverage; permutation P from F²/N.
- Laplace: s replaces d/dt with initial conditions built in; H(s) rational ⟺ finite-dimensional ODE system (ch2's transfer function completed).
- Convolution theorem: transform of a product ↔ convolution of transforms (and vice versa); circulant matrices diagonalized by F.

## Mental Models
- "Fourier = change to the operator's eigenbasis": the PDE becomes infinitely many decoupled ODEs, one per mode — ch6's diagonalization for differential operators.
- "Mode decay rates are the physics": read off e^{−λₖt} vs e^{iωt}; smoothing vs oscillation is one sign.
- "Point source → kernel → everything": heat kernel as the PDE impulse response; convolution rebuilds arbitrary data.
- "Laplace is the ODE's transfer function made systematic": algebra in s, partial fractions back — the control-shelf bread and butter.
- "Convolution is multiplication wearing a hat": polynomials, Fourier, Laplace all trade product ↔ convolution.

## Anti-patterns
- **Differentiating Fourier series term-by-term past its smoothness** — coefficients must decay fast enough (jumps → Gibbs, k⁻¹ decay).
- **Confusing one-way and two-way wave equations** (translation vs two traveling waves; first vs second order in t).
- **Forgetting initial conditions hide inside sY − y(0)** when transforming.
- **Assuming FFT speed without the root-of-unity structure** — generic DFT is N²; the symmetry is the algorithm.
- **Applying the heat kernel to wave problems** — different kernels, different physics (decay vs propagation).

## Reference Tables
### PDE → mode behavior
| Equation | Spatial eigenproblem | Mode time factor | Character |
|---|---|---|---|
| uₜ = cu_xx (bar, u=0 ends) | X″=−λX, sines, λₖ=(kπ/L)² | e^{−cλₖt} | smoothing |
| u_tt = c²u_xx | same sines | cos(√cλₖ t), sin | oscillation |
| uₜ = cu_x | e^{ikx} | e^{−ick t} | translation |

### Transform dictionary
| Time domain | Laplace/Fourier domain |
|---|---|
| y′ | sY − y(0) / ik·ĉₖ |
| convolution ∫g(t−s)f(s)ds | G(s)F(s) |
| impulse δ(t) | 1 (transfer function H alone) |
| step 1(t) | 1/s |

## Key Takeaways
Fourier series diagonalize derivative operators; PDEs become decoupled modal ODEs with rates set by the eigenvalues.
Heat smooths (e^{−k²t}), wave oscillates (e^{iωt}) — the operator's sign is the story.
The FFT exploits F² = NP, F⁴ = N²I for N log N transforms.
Laplace transforms turn ODEs into transfer-function algebra with initial conditions built in.
Convolution is the universal twin of multiplication across all three transforms.

## Connects To
Ch2's transfer function and impulse response are the finite-dimensional prototype of 8.5/8.6; ch6's diagonalization is the matrix version of Fourier's eigen-expansion; ch7's orthogonal projections build the Fourier coefficients. On the control shelf: frequency response and Bode plots are Fourier/Laplace evaluation of H(s); SIMC's first/second-order models are partial-fraction shapes from 8.5; heat/wave mode decay underlies the process models in the OpenMAIC sim widgets.
