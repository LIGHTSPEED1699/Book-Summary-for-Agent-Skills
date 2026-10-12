# Chapter 6: Non-Euclidean Geometry

## Core Idea
Spherical and hyperbolic geometry are the intrinsic geometries of surfaces of constant positive/negative curvature — and both live natively in the complex plane: the sphere's motions are Möbius maps z → (az + b)/(−b̄z + ā) (rotations via stereographic projection), and the hyperbolic plane's motions are exactly the disc automorphisms z → (az + b)/(b̄z + ā) (Poincaré's discovery). The complex plane, which seems "flat", secretly contains all three two-dimensional geometries as conformal maps of constant-curvature surfaces, with the metric ds scaled by a position-dependent factor.

## Frameworks Introduced
- **The parallel axiom and its denials (I)**: Euclid's fifth; Saccheri's two alternatives — spherical (no non-meeting lines) and hyperbolic (at least two); both are consistent geometries; angle sum ≠ π characterizes them.
- **Angular excess (I.2)**: E(T) = (angle sum) − π = k·A(T) with k constant; k > 0 spherical, k < 0 hyperbolic; no similar triangles in non-Euclidean geometry; absolute unit of length exists; k = ±1/R².
- **Intrinsic vs extrinsic (I.4-5)**: stretch-free bending preserves intrinsic geometry; Gaussian curvature k = κmin·κmax is extrinsic in definition but intrinsic in value (Theorema Egregium); E(infinitesimal triangle) = k(p)dA; E(T) = ∫∫k dA.
- **Surfaces of constant curvature (I.6)**: plane/sphere/pseudosphere model the three geometries (Beltrami); constant curvature ⟺ a group of motions exists (triangles slide freely).
- **Spherical geometry (II)**: geodesics = great circles; E(T) = A(T)/R² proved by the wedge argument (Harriot/Euler); all direct motions are rotations (two reflections in intersecting lines); rotation composition rule ψ = θ + φ − kA (area correction!); sphere motions ↔ Möbius (az+b)/(−b̄z+ā) ↔ quaternions/SU(2) (ch3's rotations of the sphere).
- **Conformal maps and metrics (II.3)**: a map of a surface carries metric d = Λ(z)ds (conformal ⟺ direction-independent Λ); stereographic projection's metric Λ = 2/(1 + |z|²) (unit sphere); geometry = plane + metric factor.
- **Hyperbolic geometry (III)**: Poincaré disc model: hyperbolic lines = circles orthogonal to the boundary; distance from the cross-ratio with the two ideal points (Bolyai-Lobachevsky formula d = (R/2)|log[z₁,p;z₂,q]|); motions = disc automorphisms (az + b)/(b̄z + ā); hyperbolic trigonometry (cosh rules); triangle area bounded by πR² (E = −A/R²); upper half-plane model; the full Möbius group = motions of 3D hyperbolic space (Poincaré 1883).

## Key Concepts
- Curvature k as the proportionality between angular excess and area — the single number distinguishing the three geometries.
- Theorema Egregium: k is intrinsic; bending doesn't change the geometry an ant measures.
- Conformal map + metric factor Λ(z) = complete intrinsic data; angles faithful, distances scaled.
- Stereographic metric Λ = 2/(1+|z|²): the sphere's geometry as the plane with a "lens".
- Hyperbolic lines meet the boundary circle orthogonally; ideal points (on the boundary) are at infinite distance; distance = log cross-ratio with the ideal endpoints.
- Disc automorphisms are exactly the hyperbolic motions — ch3's classification (elliptic/hyperbolic/parabolic) is now a classification of hyperbolic isometries.
- Hyperbolic trig: cosh rules replace cos rules; as R → ∞ hyperbolic → Euclidean (the "subsumption" theme).
- 3D payoff: general Möbius transformations = isometries of hyperbolic 3-space; Lorentz connection again.

## Mental Models
- "Geometry = surface + metric lens": any constant-curvature geometry is the plane with Λ(z) telling you true distances; changing geometry is changing the lens, not the paper.
- "Curvature is the angle tax": every triangle pays E = kA — measure angles, read curvature.
- "The boundary is infinity": in the disc model, the circle is not part of the plane; orthogonal circles are lines because they're the geodesics an ant would trace.
- "Distance is a cross-ratio": the hyperbolic distance to the ideal endpoints — ch3's invariant becomes a ruler.
- "Möbius is the universal motion group": sphere rotations, disc isometries, 3D hyperbolic motions, Lorentz transformations — one group, four avatars.

## Anti-patterns
- **Drawing hyperbolic triangles "wrong" by intuition** — angles are Euclidean in the conformal model; it's the sides (orthogonality to boundary) and distances (log cross-ratio) that are non-Euclidean.
- **Confusing the pseudosphere with the whole hyperbolic plane** — it's only a local patch (Hilbert: no complete constant-negative-curvature surface in R³); the disc is the complete model.
- **Treating boundary points as points** — they're ideal, infinitely far; disc automorphisms map interior to interior.
- **Expecting similar triangles** — angle sum detects area; equal angles force equal size.
- **Forgetting the rotation composition area correction** on the sphere (ψ = θ + φ − kA) — the group is non-commutative in a measurable, area-weighted way.

## Reference Tables
### The three geometries
| | Euclidean | Spherical | Hyperbolic |
|---|---|---|---|
| k | 0 | +1/R² | −1/R² |
| angle sum | π | > π | < π |
| E(T) | 0 | +A/R² | −A/R² |
| lines through p ∦ L | 1 | 0 | ≥ 2 |
| model | plane | sphere | Poincaré disc |
| motions | az + b | (az+b)/(−b̄z+ā) | (az+b)/(b̄z+ā) |

### Disc model dictionary
| Hyperbolic object | Disc picture |
|---|---|
| line | circle ⊥ boundary |
| ideal point | boundary point |
| distance | (R/2)\|log cross-ratio w.r.t. ideal endpoints\| |
| motion | disc automorphism (ad − bc ≠ 0 normalized) |
| triangle area | R²(π − angle sum) ≤ πR² |

## Key Takeaways
Non-Euclidean geometries are intrinsic geometries of constant-curvature surfaces; angular excess measures curvature (E = kA).
Theorema Egregium: curvature is intrinsic — bending changes nothing an ant can measure.
Conformal maps reduce surface geometry to the plane plus a metric factor Λ(z).
Sphere motions and hyperbolic motions are both Möbius families — the disc automorphisms ARE hyperbolic geometry.
Hyperbolic distance is a logarithm of a cross-ratio; hyperbolic trig replaces cos by cosh.
The full Möbius group is the isometry group of 3D hyperbolic space — and of space-time (Lorentz).

## Connects To
Ch3's Möbius classification and cross-ratio become the ruler and taxonomy here; ch4-5's conformality is the language of the maps; ch9's Cauchy applications and ch12's flows use the disc/upper-half-plane models; ch13's Riemann mapping theorem is the grand generalization (any domain ≅ disc). Hubbard's curvature/quadratic forms and Penrose's twistors (Lorentz-Möbius) meet this chapter directly; Strang's orthogonal groups are the linear-algebra shadow of the motion groups.
