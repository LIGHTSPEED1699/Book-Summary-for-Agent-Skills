# Chapter 10: Vector Fields: Physics and Topology

## Core Idea
Swap the two-plane mapping picture for a single-plane one: draw f(z) as a vector attached at z. Complex functions become vector fields — and suddenly the whole machinery (winding numbers, argument principle, residues) reads as physics: flows of electricity/heat/fluid, force fields of charges and gravitation, sources and sinks. The index of a singular point (net revolutions of V around a loop) is the winding number in physical dress, and its global version — the Poincaré-Hopf theorem, Σ indices = 2 − 2g — ties analysis to the topology of surfaces.

## Frameworks Introduced
- **Vector field of a function (I.1)**: f(z) drawn as a vector at z; mapping ↔ field are equivalent pictures; phase portraits (streamlines/integral curves) give the "overall behavior" the mapping view lacks.
- **Physical fields (I.2-3)**: steady 2D fields — current in a copper plate, heat flow, ideal fluid flow — all share one phase portrait (same laws); force fields (gravity, electrostatics) reinterpreted as flow fields of an "ideal fluid".
- **Sources, sinks, doublets (I.4)**: source of strength S at origin: V(z) = S/(2π z̄)-type radial field with |V| = S/2πr (flux S across every loop); sink = negative source; doublet = source + sink; flux across a curve = integral of normal velocity.
- **Index of a singular point (II.1)**: ν[V](Γ) = net revolutions of V(z) as z traverses Γ; deformation-invariant; index(s) = topological multiplicity of s as preimage of 0; analytic V: root of order n has index n, pole of order m has index −m; source/sink +1, saddle −1, dipole +2.
- **Poincaré's index recipe (II.2)**: ν[L] = P − N counting places where V points in a chosen direction with positive/negative rotation.
- **Index Theorem (II.3)**: index of outer boundary minus sum of hole-boundary indices = sum of indices of singular points inside (multiply-connected Argument Principle).
- **Poincaré-Hopf Theorem (III)**: for any vector field on a closed surface of genus g, Σ indices = χ = 2 − 2g; index defined intrinsically via comparison with an auxiliary nonsingular field U; Hopf's two-step proof (independence of field + one example); no singularity-free field on the sphere (χ = 2); torus admits none (χ = 0).

## Key Concepts
- Flux: ∫ normal component across a curve; incompressibility ⟹ flux across any loop around a source = S — the physical origin of the residue/winding count.
- Streamline crowding encodes field strength for physical (potential) fields — Faraday's field-line intuition made precise.
- Index = winding number of the image loop V(Γ) about 0 = topological multiplicity as preimage of 0 — ch7's machinery relocated to physics.
- Roots of V are sources/vortices (index = order), poles are sinks with negative index (−order): the residue theorem becomes "sum of source strengths".
- Bendixson's formula: index = 1 + ½(e − h) from elliptic/hyperbolic sector counts around a singularity.
- Euler characteristic χ = 2 − 2g is the conserved "index budget" of a surface: singularities can move and change type but their index sum is fixed.
- Applications: fixed-point results (any two sphere self-maps composition has a fixed point), sphere division formulas (Euler F − E + V).

## Mental Models
- "A function is a wind": read f as the velocity field it defines; zeros are sources, poles are sinks, arguments are streamlines.
- "Flux is a residue in boots": counting flow across a loop = counting windings = 2πi × residue — physics, topology, and analysis are one ledger.
- "Index is conserved under deformation": singularities can't change character without collisions — the integer is the invariant.
- "Topology sets the index budget": you cannot comb a sphere's hair; χ = 2−2g is the tax every flow must pay.
- "One phase portrait, many physics": electricity = heat = ideal fluid in steady state — the mathematics is the same field.

## Anti-patterns
- **Reading a phase portrait as flow direction only** — crowding (for potential fields) carries strength; and force-field lines aren't actual flows.
- **Forgetting poles have negative index** — a sink's index is −(pole order); sign errors flip the Index Theorem sum.
- **Defining index on a surface without a reference field** — rotation needs a fiducial U; the definition via ∠UV is what makes it intrinsic.
- **Assuming index-free fields exist on any surface** — only χ = 0 surfaces (torus) permit them; the sphere forbids.
- **Mixing "singular point of a field" with "singularity of a function"** — same objects, different vocabularies; keep the dictionary straight (root ↔ source, pole ↔ sink).

## Reference Tables
### Singular point zoo (index)
| Type | Picture | Index |
|---|---|---|
| source / sink | radial out/in | +1 / +1 (as field of 1/z: −1) |
| vortex | tangential circulation | +1 |
| saddle (crosspoint) | hyperbolic sectors | −1 |
| dipole | doublet | +2 |
| root of order n (analytic V) | n sources fused | n |
| pole of order m | m sinks fused | −m |

### Topology ledger
| Surface | genus g | χ = 2−2g | singularity-free field? |
|---|---|---|---|
| sphere | 0 | 2 | no |
| torus | 1 | 0 | yes |
| g-holed | g | 2−2g | only if g = 1 |

## Key Takeaways
The vector-field picture converts complex analysis into 2D physics: flux, sources, sinks, streamlines.
Index = winding number = topological multiplicity — one integer, three interpretations.
The Index Theorem is the Argument Principle for multiply-connected regions.
Poincaré-Hopf: Σ indices = 2 − 2g — analysis pays a topological tax.
Roots/poles of analytic fields are sources/sinks with signed strengths; residues are net source strengths.

## Connects To
Ch7's winding numbers and topological multiplicity are reinterpreted here; ch11's complex integrals become flux/circulation of these same fields (the physical explanation promised for why only 1/z has nonzero loop integral); ch12's harmonic potentials are the potentials whose gradients give these fields; ch13's Riemann surfaces (Further Reading: fluid flowing over surfaces) grow directly from this chapter. Hubbard's divergence/curl/Stokes and Strang's source-sink ODE analogies are the vector-calculus cousins.
