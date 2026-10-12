---
name: needham-visual-complex-analysis
description: Apply Tristan Needham's Visual Complex Analysis (1997, Oxford) frameworks - amplitwist differentiation, circle-inversion geometry, Möbius-as-matrix classification, winding-number counting, Pólya vector fields, physical potential-flow methods, and conformal problem transport - when doing complex analysis, conformal mapping, potential theory, or needing geometric intuition for analytic functions.
---

# Visual Complex Analysis (Needham, 1997)

Use when reasoning about complex analysis geometrically: derivatives as amplitwists, integrals as work+flux, residues as source strengths, conformal maps as solution transporters, and the whole book's thesis that complex analysis IS plane geometry plus a rigidity miracle.

## Chapter map
- [ch01 Geometry of Complex Arithmetic](chapters/ch01-geometry-complex-arithmetic.md) — complex plane, amplitwist arithmetic, roots, e^z, multifunctions, log
- [ch02 Complex Functions as Transformations](chapters/ch02-complex-functions-transformations.md) — mapping pictures, z²/z̄, nets, branch cuts as fences
- [ch03 Möbius Transformations and Inversion](chapters/ch03-mobius-transformations-inversion.md) — inversion in circles, circle/angle/symmetry preservation, Riemann sphere, matrix classification, cross-ratio
- [ch04 Differentiation: The Amplitwist Concept](chapters/ch04-differentiation-amplitwist.md) — derivative = common amplitwist, Jacobian taxonomy, CR as "squares stay squares", critical points
- [ch05 Further Geometry of Differentiation](chapters/ch05-further-geometry-differentiation.md) — CR in four coordinate dressings, rigidity, visual differentiation, differentiation rules
- [ch06 Non-Euclidean Geometry](chapters/ch06-non-euclidean-geometry.md) — angular excess E = kA, Theorema Egregium, sphere/disc models, hyperbolic distance as log cross-ratio, disc automorphisms as motions
- [ch07 Winding Numbers and Topology](chapters/ch07-winding-numbers-topology.md) — winding numbers, crossing rule, Hopf degree theorem, argument principle, multiplicity, Rouché, FTA
- [ch08 Complex Integration: Cauchy's Theorem](chapters/ch08-complex-integration-cauchy.md) — Riemann sum-paths, area integrals, deformation theorem, residues born from 1/z, Fundamental Theorem
- [ch09 Cauchy's Formula and Its Applications](chapters/ch09-cauchy-formula-applications.md) — boundary-to-interior holography, Gauss MVT, Taylor/Laurent, residue calculus, real integrals
- [ch10 Vector Fields: Physics and Topology](chapters/ch10-vector-fields-physics-topology.md) — functions as vector fields, sources/sinks/dipoles, index, Index Theorem, Poincaré-Hopf Σ = 2−2g
- [ch11 Vector Fields and Complex Integration](chapters/ch11-vector-fields-complex-integration.md) — flux/work/div/curl, Gauss+Stokes, Pólya vector field: ∮H dz = work + i·flux; Cauchy as physics
- [ch12 Flows and Harmonic Functions](chapters/ch12-flows-harmonic-functions.md) — harmonic duals, conformal invariance of Δ, ∂̄ calculus, physics of Riemann's Mapping Theorem, Green's function, Poisson/Dirichlet

## Top-level references
- [glossary.md](glossary.md) — terms with Needham's vocabulary (amplitwist, Pólya field, k-cells, duality)
- [patterns.md](patterns.md) — recurring proof/problem patterns
- [cheatsheet.md](cheatsheet.md) — formulas, theorems, and dictionary tables at a glance

## Core theses (apply as defaults)
1. The complex derivative is an amplitwist: one complex number acting on every infinitesimal vector; CR = the Jacobian being complex multiplication.
2. Analytic functions are rigid crystals: minimal data determines everything (ch5 rigidity → ch9 Cauchy formula → identity theorem).
3. Counting beats computing: winding numbers, indices, and residues turn geometry into arithmetic (N = ν[f(Γ),p]; ∮ = 2πi Σ ν·Res).
4. Möbius = the universal symmetry group: circle inversion generates it; it classifies hyperbolic motions, sphere rotations, and Lorentz transformations.
5. Complex integrals are physical: work + i·flux of the Pólya field; residues are source/circulation strengths; Cauchy = Gauss + Stokes.
6. Conformal maps transport solutions: harmonicity is conformally invariant (Δ scales by |f′|²); Riemann's theorem = matching flow grids; Green's function = −ln|f|.

## When to load which chapter
- Derivative/CR questions: ch4-5. Integrals/residues: ch8-9. Topology/counting: ch7, ch10. Geometry/Möbius/hyperbolic: ch3, ch6. Physics/flows/mapping problems: ch10-12. First-time intuition: ch1-2.
