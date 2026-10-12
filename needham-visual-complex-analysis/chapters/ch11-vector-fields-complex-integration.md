# Chapter 11: Vector Fields and Complex Integration

## Core Idea
Every complex integral ∮ H dz is secretly two real line integrals — the work and the flux of a single physical field: the **Pólya vector field** (draw H̄(z) at z, not H(z)). With this dictionary, Cauchy's Theorem becomes physics: analyticity ⟺ the Pólya field is divergence-free and curl-free (CR equations in vector-calculus dress), so loop integrals vanish by Gauss/Stokes; residues become the source strengths and circulation densities of the Pólya field at singularities.

## Frameworks Introduced
- **Flux (I.1)**: F[X,K] = ∫ (X·N) ds — normal flow across a curve; incompressibility ⟺ vanishing flux around sourceless loops; 3D flux across surfaces.
- **Work / circulation (I.2)**: W[X,K] = ∫ (X·T) ds — tangential component; ice-puck thought experiment gives sign and meaning; conservative fields (W = 0 on all loops); Feynman's frozen-fluid picture of circulation; irrotational = W vanishes on all loops.
- **Divergence and curl as local densities (I.3)**: infinitesimal square: F = (∇·X)·area, W = (∇×X)·area; divergence = flux per unit area, curl = work per unit area = twice the angular velocity of a floating disc (ω = 2∇×X).
- **Geometric divergence/curl (I.4)**: ∇·X = ∂_s|X| + κ_P|X| (speed growth + streamline spreading); ∇×X = −∂_p|X| + κ_S|X| — formulas along streamlines and orthogonal trajectories.
- **Gauss and Stokes theorems (I.5)**: F[X,C] = ∫∫ ∇·X dA, W[X,C] = ∫∫ ∇×X dA — grid-gluing proof; deformation theorems for flux (div-free sweeps) and work (curl-free sweeps); local ⟺ global on simply-connected regions.
- **Pólya vector field (II.1)**: draw H̄ at z; then H dz = [H̄·T + i H̄·N] ds, so ∮ H dz = W[H̄,K] + i F[H̄,K] — the complex integral is literally work + i·flux; index flips sign under conjugation (roots → index −n, poles → +m).
- **Physical Cauchy Theorem (II.2)**: ∇·H̄ = 0 and ∇×H̄ = 0 ⟺ CR ⟺ H analytic — Cauchy's Theorem = no sources, no circulation inside; Gauss/Stokes give the integral 0.
- **Residues as sources/circulation (II.3+)**: at a singularity, the residue's real part = circulation density, imaginary part = source strength of the Pólya field; 1/z is a pure source + vortex of strength 2π; the residue theorem is the index/source theorem in complex notation.

## Key Concepts
- CR equations as one complex equation: i∂ₓH − ∂_y H = ∇×H̄ + i∇·H̄ — vanishing ⟺ analyticity.
- The Pólya field preserves all information (H ↔ H̄) but makes integrals visual: flow along/across the contour.
- Gauss/Stokes are the real counterparts of Cauchy's Theorem; complex notation unifies them (dz and d z̄ pairings).
- Conservative = path-independent work = potential exists; sourceless+irrotational fields are gradients of harmonic potentials (ch12).
- Index of Pólya field at singularities: root order n → −n, pole order m → +m; flux/circulation around a loop = 2π × (residue components).
- Deformation theorems: flux conserved sweeping through div-free points; work conserved sweeping through curl-free points — physical twins of Cauchy's deformation.

## Mental Models
- "An integral is work + i·flux": draw the Pólya field; read the answer off how the field flows along and across the contour.
- "CR = no sources, no whirlpools": analyticity is incompressible, irrotational flow — the physics is the analysis.
- "Residues are source strengths": a pole's residue is the fluid injected (imag part) and the circulation pumped (real part) per circuit.
- "Gauss/Stokes are Cauchy in real clothes": the grid-gluing proof is identical; complex notation halves the bookkeeping.
- "Local kills global": vanishing divergence/curl at every point ⟹ vanishing loop integrals (simply-connected) — the infinitesimal square is the whole proof.

## Anti-patterns
- **Drawing H instead of H̄ for integration** — the Pólya field is the conjugate; the phase portraits of zⁿ as Pólya fields look like 1/z̄ⁿ-type flows.
- **Confusing the ordinary vector field's index with the Pólya index** — conjugation flips the sign.
- **Applying "local ⟹ global" on multiply-connected regions** — a curl-free field around a source is not globally conservative (1/z̄ flow around the origin).
- **Reading streamline pictures as strength-blind** — for potential (div/curl-free) fields, crowding encodes |X|.
- **Forgetting the i**: flux is the imaginary part of the integral, work the real part — swapping them misreads every example.

## Reference Tables
### Pólya dictionary
| Complex object | Pólya field physics |
|---|---|
| Re ∮ H dz | work W[H̄, K] |
| Im ∮ H dz | flux F[H̄, K] |
| H analytic | div H̄ = 0, curl H̄ = 0 |
| Res[H, s] | (circulation + i·source)/2π at s |
| root order n | singular point of index −n |
| pole order m | singular point of index +m |

### Real ↔ complex theorems
| Physics | Complex analysis |
|---|---|
| Gauss: ∮ X·N ds = ∫∫ div X dA | Cauchy/deformation (flux part) |
| Stokes: ∮ X·T ds = ∫∫ curl X dA | Cauchy/deformation (work part) |
| conservative + sourceless ⟹ potential | analytic ⟹ antiderivative |

## Key Takeaways
∮ H dz = work + i·flux of the Pólya field H̄ — complex integration is two real line integrals in one costume.
Analyticity ⟺ Pólya field divergence-free and curl-free; Cauchy's Theorem is Gauss+Stokes.
Residues are physical source/circulation strengths at singularities.
Gauss, Stokes, and Cauchy share one proof: glue infinitesimal squares.
Local densities (div, curl) control global loop integrals on simply-connected regions.

## Connects To
Ch10's sources/sinks/indices become quantitative here (flux = strength); ch8's Cauchy theorem gets its physical twin; ch12's harmonic potentials are exactly the potentials of div-free curl-free fields, and complex potentials unify them; ch13's mapping theorem uses conformality = flow-net preservation. Hubbard's divergence/curl/Stokes and generalized Stokes is the full real-geometry framework this chapter previews; Strang's Laplacian/potential sections are the applied cousin.
