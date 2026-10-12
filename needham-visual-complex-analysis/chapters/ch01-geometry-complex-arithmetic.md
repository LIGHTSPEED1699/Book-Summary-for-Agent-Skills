# Chapter 1: Geometry and Complex Arithmetic

## Core Idea
A complex number is a single, indivisible point in the plane — and multiplication by a complex number is a "amplitwist" in embryo: rotation through its angle plus expansion by its modulus, applied to the whole plane at once. Everything in the chapter (Euler's formula, trig identities, Cotes' factorization, roots of unity, dot/cross products, rigid motions) is the geometric multiplication rule R∠φ · r∠θ = Rr∠(φ+θ) working through different problems.

## Frameworks Introduced
- **History as warning (I.1-2)**: Cardano dismissed complex numbers ("subtle as they are useless"); Bombelli's "wild thought" (∛(2+11i) = 2+i) forced the symbolic rules because the *cubic* (not the quadratic) demands them — real problems need complex arithmetic. The block was philosophical: nobody knew *what* a complex number is until Wessel/Argand/Gauss gave the plane.
- **Two labellings (I.3)**: Cartesian x+iy is natural for addition; polar r∠θ is natural for multiplication; polar labels are non-unique up to 2π — a theme that returns as winding numbers and multivalued functions.
- **Euler's formula (II)**: e^{iθ} = cosθ + i sinθ by two heuristics — the moving-particle argument (velocity = iZ = position rotated 90°, so the path is the unit circle at unit speed) and the power-series spiral (terms at right angles; C′ = −S, S′ = C gives |e^{iθ}| = 1 and angle θ without Taylor's theorem). Consequence: cosθ = (e^{iθ}+e^{−iθ})/2, sinθ = (e^{iθ}−e^{−iθ})/2i.
- **Applications (III)**: trig identities as one complex equation saying two things at once; nth derivatives of e^{ax}sin bx via V = (a+ib)Z geometric differentiation ("ultimately equal" infinitesimal bookkeeping); Cotes' factorization of xⁿ−1 via regular n-gons (roots of unity e^{2πik/n}); Descartes' factor theorem and the Fundamental Theorem of Algebra (proved later in ch7); dot and cross products subsumed by complex multiplication (Re(āb) = dot, Im(āb) = cross).
- **Klein's geometric viewpoint (IV)**: geometry = study of invariants under a group of transformations; classify plane motions (translations, rotations, reflections); the Three Reflections Theorem; similarities as z → az + b (direct) and a z̄ + b (opposite).
- **Spatial complex numbers? (V)**: the plane's arithmetic doesn't extend to 3-space consistently; quaternions as the price of 3D rotation arithmetic (preview of ch3's sphere rotations).

## Key Concepts
- Multiplication by A = R e^{iφ}: rotation φ + dilation R about the origin; distributivity follows because rotations/dilations preserve parallelograms (geometry proving algebra).
- iz = z rotated 90° — the derivative-as-rotation seed of the whole book.
- Roots of unity are regular n-gons; conjugate pairs give the real quadratic factors z² − 2cos(2πk/n)z + 1.
- Complex equation = two real equations at once (cos+sin identities come paired).
- "Ultimately equal" = rigorous infinitesimal shorthand: X = Y for infinitesimal δ iff lim X/Y = 1.
- Motions composed as complex functions: T_v(z) = z + v, R^a_θ(z) = e^{iθ}z + k; two rotations compose to one rotation (or a translation when angles sum to 2πm).

## Mental Models
- "Complex numbers were invented to solve cubics, legitimated by the plane": algebra first, geometry as the rescue of understanding.
- "Multiply = amplitwist the whole plane": every multiplication fact is a similarity of the plane.
- "e^{iθ} is a particle on the unit circle": dynamics makes Euler's formula obvious; velocity = i·position.
- "One complex equation says two real things": never separate real and imaginary parts prematurely.
- "Even avoiding complex numbers you can't avoid their geometry": Cotes' n-gons discovered by pure distance geometry.

## Anti-patterns
- **Defining e^{iθ} := cosθ + i sinθ by fiat** — Needham calls it "a low blow to Euler", a tautology that hides the content; derive it.
- **Thinking the quadratic forced complex numbers** — it's the cubic; the quadratic's "impossible" roots genuinely mean no intersection.
- **Treating polar labels as unique** — angle is multi-valued mod 2π; this is the root of branches and logarithms later.
- **Extending complex arithmetic naively to 3D** — no consistent system; quaternions (non-commutative) are the answer.
- **Trusting "impossible numbers" as useless** — Bombelli's paradox (real root hiding inside complex radicals) is the whole lesson.

## Reference Tables
### Notation (I.3)
| Symbol | Meaning |
|---|---|
| \|z\|, arg z | modulus r, angle θ |
| Re z, Im z | Cartesian coordinates |
| z̄ | conjugate = reflection in real axis; z z̄ = \|z\|² |
| r∠θ → r e^{iθ} | polar label via Euler |

### Motion algebra
| Motion | Complex function | Composition |
|---|---|---|
| Translation | T_v(z) = z + v | T_w T_v = T_{w+v} |
| Rotation about a | e^{iθ}(z−a)+a = e^{iθ}z + k | R^b_φ R^a_θ = R^c_{θ+φ} (or T_v if θ+φ ≡ 0) |
| Direct similarity | z → az + b | amplitwist + shift |
| Opposite similarity | z → a z̄ + b | includes reflection |

## Key Takeaways
Complex numbers are points; multiplication is a rotation-plus-dilation of the entire plane.
Euler's formula is dynamics: e^{iθ} moves on the unit circle with velocity iZ.
Roots of unity are regular polygons; Cotes' factorization is their geometry.
Dot/cross products and rigid motions are all complex arithmetic in disguise.
Geometry through Klein: study what a transformation group leaves unchanged.

## Connects To
Ch2 develops e^z fully (dynamics of e^{iz}); ch3's Möbius transformations are the full symmetry group this chapter's motions preview; ch4's amplitwist is multiplication-by-derivative; ch7 proves the Fundamental Theorem of Algebra via winding numbers; ch10-12 use the dot/cross ↔ complex multiplication bridge for physics. Hubbard's derivative-as-linear-map is the multivariable cousin of "multiplication = amplitwist"; Strang's complex exponentials (ch1.5) are the engineer's version of Euler's formula.
