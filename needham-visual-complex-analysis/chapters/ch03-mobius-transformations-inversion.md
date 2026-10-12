# Chapter 3: Möbius Transformations and Inversion

## Core Idea
The maps z → (az + b)/(cz + d) are the natural complete symmetry group of the extended plane: every one decomposes into translations, dilative rotations, and the star of the show — complex inversion z → 1/z, which is geometric inversion (reflection in a circle) followed by conjugation. Inversion's trinity of miracles — preserves circles (lines = circles through ∞), preserves angles up to sign (anticonformal; complex inversion conformal), preserves symmetry pairs — makes Möbius transformations the conformal automorphisms of the Riemann sphere, and the bridge to hyperbolic geometry (ch6) and even Lorentz transformations in special relativity.

## Frameworks Introduced
- **Definition and decomposition (I)**: M(z) = (az+b)/(cz+d), non-singular iff ad − bc ≠ 0; decompose into translation z → z + d/c, complex inversion 1/z, dilative rotation, translation — so everything reduces to understanding 1/z.
- **Geometric inversion (II.1)**: z → R²/ρ̄ from centre q: swaps interior/exterior of circle K, fixes K pointwise, involutory — "reflection in a circle"; formula Ī_K(z) = (q̄z + (R² − |q|²))/(z − q); deep analogy with line reflection (large circle ≈ line; local inversion ≈ tangent reflection).
- **Preservation of circles (II.2)**: line not through q ↔ circle through q; circle not through q ↔ circle; unified view: lines are circles through the centre/infinity; key similarity lemma [qa][qā] = R².
- **Orthogonal circles & construction (II.3)**: circles orthogonal to K are invariant under inversion; the inverse point ž = intersection of any two circles through z orthogonal to K — same construction as line reflection, deepening the analogy.
- **Angle preservation (II.4)**: conformal (angles with sign), anticonformal (sign reversed), isogonal (magnitude only); inversion anticonformal; complex inversion = inversion + conjugation = conformal; even/odd compositions of reflections conformal/anticonformal.
- **Preservation of symmetry (II.5)**: symmetric pairs (w.r.t. circle K) map to symmetric pairs under any inversion — orthogonality is preserved.
- **Sphere inversion (II.6) + Riemann sphere (IV)**: 3D inversion in a sphere; stereographic projection Σ → C is built from sphere inversion: circles on Σ ↔ circles in C; angles preserved; the point at infinity adjoined; behavior of functions at ∞ via f(1/z); sphere as the natural domain.
- **Möbius as matrices (VI)**: M ↔ [[a,b],[c,d]] up to scale (homogeneous coordinates); fixed points = eigenvectors; multiplier k = λ₁/λ₂ classifies: elliptic (|k|=1, rotations of sphere), hyperbolic (k positive real), loxodromic (general k), parabolic (λ₁ = λ₂, one fixed point); rotations of the sphere ↔ SU(2)/±, linking to quaternions (ch1) and the Hopf map.
- **Cross-ratio (VII)**: [z,a,b,c] = ((z−a)(b−c))/((z−b)(c−a)) — the Möbius invariant; M determined by images of three points; symmetry characterized by cross-ratio on the real line (harmonic/conjugate configurations).
- **Applications (III)**: Ptolemy's theorem via inversion; touching-circles problems; automorphisms of the unit disc z → (az + b)/(b̄z + ā) (preview of hyperbolic motions, ch6); introduction to Riemann's mapping theorem.

## Key Concepts
- ad − bc ≠ 0 ⟺ genuinely one-to-one on the extended plane; coefficients non-unique up to common scale.
- Inversion distance law: [āb̄] = [ab]·R²/([qa][qb]) — the similarity engine behind all preservation results.
- Lines are circles through ∞; Möbius transformations preserve the family of "circles" (generalized circles).
- Conformality of 1/z: two angle reversals cancel; even/odd reflection-counting decides conformal vs anticonformal.
- Stereographic projection is the dictionary between sphere geometry and plane geometry; ∞ becomes an honest point.
- Fixed points + multiplier classify Möbius maps exactly like normal forms of linear maps — eigenvectors ARE the fixed points on the sphere.
- Cross-ratio is THE invariant: everything Möbius-invariant is built from it.
- Lorentz surprise: Möbius group ≅ restricted Lorentz group acting on the light-ray sphere (Penrose's twistors' ancestor).

## Mental Models
- "Inversion is reflection with the circle in place of the line": same fixed set, same involution, same symmetry pairs — orthogonal circles are the mirror construction.
- "One 1/z unlocks all of Möbius": decompose, then track circles/angles/symmetry through the single nontrivial step.
- "The sphere is where Möbius lives": stereographic dictionary turns wild plane maps into rotations and nice sphere maps; ∞ demoted to a point.
- "Three points determine a Möbius map; cross-ratio measures what's left": normalize to 0, 1, ∞ and the map is done.
- "Eigenvalues wear fixed-point clothing": matrix picture of (a,b;c,d) classifies dynamics (elliptic/hyperbolic/loxodromic/parabolic) exactly as linear algebra classifies normal forms.

## Anti-patterns
- **Forgetting ad − bc = 0 collapses M to a constant** (singular case).
- **Treating lines and circles as different species** — under inversion they morph into each other; always ask "does it pass through q?".
- **Confusing inversion (anticonformal) with complex inversion (conformal)** — the conjugation matters.
- **Applying Möbius maps to z = ∞ carelessly** — use the sphere or the decomposition; M(∞) = a/c, M(−d/c) = ∞.
- **Assuming every conformal self-map of the plane is Möbius** — true on the sphere, false on C (that's the content of later chapters; disc automorphisms are Möbius, half-plane ones too, but general domains have none).

## Reference Tables
### Möbius classification (multiplier k = λ₁/λ₂)
| Type | k | Fixed points | Sphere action |
|---|---|---|---|
| elliptic | \|k\| = 1, k ≠ 1 | 2 | rotation |
| hyperbolic | k ∈ ℝ⁺, k ≠ 1 | 2 | stretch along axis |
| loxodromic | general k | 2 | rotate + stretch |
| parabolic | k = 1 (λ₁=λ₂) | 1 (double) | limit rotation/translation |

### Inversion dictionary
| Object | Image under Ī_K |
|---|---|
| circle through q | line not through q |
| line not through q | circle through q |
| circle not through q | circle |
| line through q | itself |
| circle orthogonal to K | itself |
| symmetric pair wrt K | symmetric pair wrt image |

### Matrix picture
| Concept | Matrix side | Geometry |
|---|---|---|
| M(z) | [[a,b],[c,d]] up to scale | plane map |
| fixed points | eigenvectors | 0, 1, or 2 points on sphere |
| multiplier | λ₁/λ₂ | normal form z → kz |
| disc automorphisms | (az+b)/(b̄z+ā) | hyperbolic motions (ch6) |

## Key Takeaways
Möbius = translations + dilative rotations + one 1/z; all its magic reduces to circle inversion.
Inversion preserves generalized circles, angle magnitudes, and symmetry pairs — anticonformally; complex inversion restores orientation.
Stereographic projection makes the Riemann sphere the natural stage, with ∞ as an ordinary point.
Matrices classify Möbius maps: fixed points are eigenvectors, multiplier λ₁/λ₂ gives the normal form.
Cross-ratio is the complete invariant; three points determine the map.
The same group governs Lorentz transformations of space-time — geometry feeding physics.

## Connects To
Ch4's conformality question starts where this chapter's angle-preservation leaves off; ch6 builds hyperbolic geometry entirely from Möbius transformations and the disc automorphisms; ch7's winding numbers count preimages under these maps; ch13's Riemann mapping theorem is foreshadowed by the disc automorphisms. Hubbard's change-of-variables and Axler's projective/eigenvalue language meet here in the matrix picture; Penrose's twistors (his own book!) are the payoff of the Lorentz-Möbius bridge.
