# Chapter 12: Flows and Harmonic Functions (incl. Riemann Mapping Theorem & Dirichlet Problem)

## Core Idea
Sourceless, irrotational flows are governed by harmonic potentials, and harmonic functions are exactly the real parts of analytic functions — so complex analysis is a machine for solving potential problems (heat, electrostatics, fluid flow). The dual flow (rotate the field by 90°) swaps streamlines and equipotentials, turning a fluid-flow solution into an electrostatics solution for free. Harmonicity is conformally invariant, which is the deep reason conformal maps solve boundary-value problems: map a hard domain to a simple one, solve there, map back.

## Frameworks Introduced
- **Dual flows (I.1)**: rotate a sourceless irrotational field H by angle θ: H_θ = e^{iθ}H stays sourceless/irrotational with potential Ω_θ = e^{−iθ}Ω; the π/2 dual Ĥ = iH swaps roles: Φ̂ = Ψ, Ψ̂ = −Φ; a source's dual is a vortex; dipole duals are dipoles; superposition H_θ = cosθ·H + sinθ·Ĥ.
- **Harmonic duals (I.2)**: every harmonic Φ has a dual Ψ (harmonic conjugate) with f = Φ + iΨ analytic; construction: Ψ = flux of ∇Φ across a path (line integral); dual may be a multifunction (ln|z| ↔ arg z); existence of duals upgrades analytic facts to harmonic facts (Gauss MVT, maximum principle for all harmonic functions).
- **Recipe for the analytic function**: Ω′(z) = ∇Φ(z, 0) — evaluate the gradient on the real axis, replace x by z (identity theorem).
- **Conformal invariance (II)**: harmonicity is conformally invariant: Φ∘f⁻¹ harmonic iff Φ harmonic; quantitatively ΔΦ(z) = [ΔΦ̃(w)]·|f′(z)|²; geometric proof via the square test-grid for harmonicity (conformal maps preserve squares).
- **Meaning of the Laplacian (II.3)**: ⟨Φ⟩_r − Φ(p) = (r²/4)ΔΦ — the Laplacian measures how much the circle average exceeds the centre value; harmonic ⟺ perfect circular balance at every scale; gives a complex-free proof of Gauss MVT.
- **Complex gradient operator (III)**: ∇ = ∂ₓ + i∂_y and its conjugate: f analytic ⟺ ∇̄f = 0 (Needham's ∇-notation; standard ∂̄), and then ∇f = 2f′; ∇·f + i∇×f unified; Δ = ∇∇̄ = ∇̄∇; chain rules make Laplacian computations one-liners; Gauss+Stokes combine into ∮ f dz = i∫∫ ∇̄f dA (Cauchy's theorem in one line).
- **Complex curvature and harmonic curve families (IV)**: when is a curve family the equipotentials of a harmonic function? geometric criteria via complex curvature of equipotential families; Schwarz-Christoffel mentioned for polygons.
- **Flow around an obstacle (V)**: method of images for the circle (Ω = z + 1/z round C); conformally mapping one flow onto another transports solutions (ellipse flow from circle flow via w = ½(3z + 1/z)); complex potential = the special mapping making the flow uniform.
- **Physics of Riemann's Mapping Theorem (VI)**: construct the conformal map R → D by matching k-cell grids of two physical flows: exterior case = uniform flow round obstacle R vs uniform flow round D with speed v = [Φ]/4 matched by equal square counts along boundary streamlines; interior case = unit dipole at p inside R vs dipole of strength d = [Φ]/4 at 0 in C — the 3 degrees of freedom of the mapping = dipole position p (2) + dipole direction φ (1), i.e. f(p) = 0 and arg f′(p) = φ; vortex version (equal strengths!) and source/heat version give the same family; automorphisms of the disc re-derived physically via w = (z−p)/(pz̄−1)·e^{iδ}.
- **Green's function (VI.6)**: G_p(z) = steady temperature with unit heat source at p and boundary held at 0; G_p = −ln|f(z)| for any mapping f: R → D with f(p) = 0; local form G_p ≈ −ln ρ + g_p; symmetry G_p(q) = G_q(p); conformal invariance (Green's function transports between domains); boundary heat flux Q(z) = |f′(z)|.
- **Dirichlet's Problem (VII)**: find harmonic T with prescribed boundary values; solved by transporting boundary data through the Riemann map: Poisson's formula for the disc T(re^{iθ}) = (1/2π)∫ T(φ)·(1−r²)/(1 − 2r cos(θ−φ) + r²) dφ; half-plane Poisson formula via Möbius; general Green's formula T(a) = −(1/2π)∮ T ∂G/∂n ds; the conformally invariant average: the temperature where you stand equals the Poisson-weighted average of observed boundary temperatures — Gauss, Poisson, and Green are one picture in three domains.

## Key Concepts
- Complex potential Ω = Φ + iΨ: Φ potential (work), Ψ stream function (flux); equipotentials ⊥ streamlines; k-work tubes.
- Dual = 90° rotation = swap (Φ, Ψ) → (Ψ, −Φ): one solution, two physics.
- Harmonic conjugates exist (locally always; globally up to multifunctions on non-simply-connected domains — ln|z|'s dual arg z is multivalued).
- Maximum principle: harmonic functions attain max/min on the boundary (from analytic version via duals).
- Laplacian = circle-average defect: ΔΦ = 4·lim (⟨Φ⟩_r − Φ(p))/r² — the coordinate-free meaning.
- Conformal scaling of the Laplacian by |f′|²: harmonicity (Δ = 0) survives because the factor can't create zeros.
- Complex gradient calculus: ∂̄-notation (Needham ∇) compresses div/curl/Laplacian/Cauchy-Riemann into one operator algebra.
- Minimal surfaces miracle: analytic H(z) ⟷ minimal surface; rotating θ bends helicoid ↔ catenoid stretch-free.
- Riemann mapping theorem (existence, 3-parameter family): any simply connected R ≠ ℂ maps conformally onto D; physical construction via matched flow grids; uniqueness fixed by f(p) = 0 plus twist arg f′(p).
- Green's function = the mapping's log-modulus: G_p = −ln|f|; it encodes the map, is conformally natural, symmetric in (p, q), and its normal derivative on the boundary is |f′|.
- Poisson kernel = the disc's Green's-function normal derivative; boundary-value problems are conformally invariant — solve once on the disc, transport everywhere.

## Mental Models
- "Solve the flow, get electrostatics free": rotate by 90° — streamlines become equipotentials.
- "Harmonic = perfectly balanced at every circle": the Laplacian is the balance defect; harmonicity is zero defect.
- "Conformal maps are solution transporters": boundary-value problems move between domains with the |f′|² metric factor; Δ = 0 is invariant.
- "∂̄ is the analyticity detector": ∂̄f = 0 says "analytic" in one character; Δ = ∂∂̄ says "harmonic" in two.
- "Real and imaginary parts are twins": each determines the other (up to constant) — knowing one harmonic function means knowing an analytic function.

## Anti-patterns
- **Expecting single-valued harmonic conjugates on annuli** — ln|z| needs multivalued arg z; global duals require simply-connected domains.
- **Confusing Needham's ∇ (∂ₓ + i∂_y) with the standard ∂̄ (½(∂ₓ + i∂_y))** — factors of 2 differ; his ∇̄f = 0 is the standard ∂̄f = 0.
- **Applying conformal invariance at critical points** — f′ = 0 breaks the conformal dictionary (|f′|² = 0 degenerates).
- **Assuming any equipotential family admits a harmonic potential** — the curves must pass the geometric (square-tube/curvature) test; |z| on circles fails, ln|z| succeeds.
- **Forgetting the maximum principle's strictness** — interior max forces constant; boundary data controls everything (uniqueness of Dirichlet solutions).

## Reference Tables
### Flow dictionary
| Object | Meaning | Dual (×i) |
|---|---|---|
| Φ potential | work of force field | Ψ |
| Ψ stream function | flux across curves | −Φ |
| source | radial outflow | vortex |
| dipole | source+sink | dipole (rotated) |
| Ω = Φ + iΨ | complex potential | e^{−iθ}Ω |

### Operator calculus (Needham notation)
| Operator | Definition | Action |
|---|---|---|
| ∇ | ∂ₓ + i∂_y | ∇̄f = 0 ⟺ f analytic |
| ∇̄ | ∂ₓ − i∂_y | analytic f: ∇f = 2f′ |
| Δ | ∇∇̄ = ∇̄∇ | Laplacian |
| Gauss+Stokes | ∮ f dz = i∫∫ ∇̄f dA | Cauchy in one line |
| Laplacian transform | ΔΦ(z) = |f′|² ΔΦ̃(f(z)) | conformal invariance |

## Key Takeaways
Harmonic functions = real parts of analytic functions; duals = imaginary parts — one object, two physics.
The 90° dual flow converts flow solutions to electrostatic solutions (streamlines ↔ equipotentials).
The Laplacian is the circle-average defect; harmonicity is perfect circular balance.
Harmonicity is conformally invariant (Δ scales by |f′|²) — the engine behind conformal problem-solving.
Complex gradient (∂̄) calculus unifies CR, div/curl, Laplacian, and Cauchy's theorem.
Riemann's Mapping Theorem is physical: match flow grids (dipoles/vortices/sources) between domains; the 3 degrees of freedom are the dipole's position and direction.
Green's function G_p = −ln|f| encodes the mapping itself; Poisson's formula is its boundary flux — and Gauss/Poisson/Green are one conformally invariant average.

## Connects To
Ch11's Pólya fields and div/curl feed directly in; ch6's hyperbolic geometry (disc automorphisms re-derived physically here via w = e^{iδ}(z−p)/(p̄z−1)) uses conformal invariance of harmonicity; ch3's Möbius machinery powers the disc/half-plane Poisson transfers; ch9's Gauss MVT gets its harmonic generalization and Cauchy's formula its physical twin. This is the book's finale: ch1–11 all reappear in the mapping-theorem physics. Hubbard's Laplacian/Laplace equation sections and Strang's potential-flow/Laplace examples are the real-variable counterparts; Penrose's twistors and field equations lean on the same conformal-Laplacian structure.
