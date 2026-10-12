# Chapter 7: Winding Numbers and Topology

## Core Idea
The winding number ν(L, p) — the net revolutions of (z − p) as z traces a closed loop — is the book's great counting tool: it defines "inside" for self-intersecting loops, classifies loops up to continuous deformation (Hopf's Degree Theorem), and culminates in the Argument Principle N = ν[f(Γ), p]: the number of p-points inside a loop is read off the image loop's winding number. Roots of polynomials, the Fundamental Theorem of Algebra, and Rouché's theorem all fall out of counting windings.

## Frameworks Introduced
- **Winding number (I.1)**: ν(L, p) = net count of counterclockwise revolutions of (z − p) around one traversal; integer-valued, constant on each region D_j cut out by the loop.
- **Inside defined (I.2)**: inside = {p : ν(L, p) ≠ 0} — the correct notion even for self-intersecting loops (justified by the next chapter's integration).
- **Crossing rule (I.3)**: crossing the loop from left-to-right (as you move) increments ν by 1, right-to-left decrements; winding numbers computed in seconds for any loop; ray-intersection count ≥ |n| with cancelling pairs.
- **Hopf's Degree Theorem (II)**: a loop K deforms continuously into L without crossing p ⟺ ν(K,p) = ν(L,p); loops = mappings of the circle; standardize by radial projection to the unit circle; archetype Î_ν(z) = z^ν; explicit two-stage deformation (radial pull, then straightening Φ_t = Φ + t(νθ − Φ)); generalizes to surfaces in 3-space and n-dimensions (degree).
- **Argument Principle (III)**: for analytic f inside/on simple loop Γ, N = ν[f(Γ), p] where N counts p-points with multiplicity; polynomial case by angle-addition of factors.
- **Topological Argument Principle (IV)**: for merely continuous h, p-points have topological multiplicity ν(a) = ν[h(Γ_a), p) (local degree); ν[h(Γ), p] = Σ ν(a_j); for analytic f, topological = algebraic multiplicity and always positive; sign of det J for real-differentiable maps; Darboux's theorem (one-to-one on boundary ⟹ one-to-one inside for analytic).
- **Rouché's theorem and FTA (V)**: if |f − g| < |g| on Γ (g dominates on the boundary), f and g have the same number of zeros inside — homotopy of image loops avoiding 0; Fundamental Theorem of Algebra: degree-n polynomial has n roots (compare with leading term); multiplicity via coalescing roots and critical points (f^{(n)} first nonvanishing derivative ⟹ local form Ω(z)Δⁿ).

## Key Concepts
- Winding number is locally constant in p and changes by ±1 exactly at crossings — a continuous integer is constant.
- Multiplicity three ways: algebraic (first nonvanishing Taylor term Δⁿ), geometric (image of small circle winds n times), topological (local degree) — they agree for analytic maps.
- Analytic maps always have positive local degree (orientation-preserving); z̄ has −1; folding maps can give 0 (multiplicity annihilation) — impossible analytically.
- The Argument Principle is topological, not conformal — it holds for continuous maps; analyticity contributes positivity + multiplicity agreement.
- Rouché = homotopy: f_t = g + t(f − g) never hits 0 on Γ, so ν[f_t(Γ), 0] constant.
- FTA proved: leading-term domination on a big circle gives winding n.
- Critical points of analytic maps: multiplicity n > 1 ⟺ critical of order n − 1; roots repel each other's coalescence (slope must vanish).

## Mental Models
- "Count windings, not intersections": the image loop's revolutions count preimages exactly, multiplicities included.
- "Inside = nonzero winding": the honest generalization of Jordan's intuition.
- "Deformation invariance is the whole game": anything true of the archetype z^ν is true of every loop of degree ν (Hopf).
- "Dominance on the boundary fixes the count inside": Rouché as "the boundary's vote decides".
- "Multiplicity is winding in disguise": double roots wind twice — algebra, geometry, and topology agree.

## Anti-patterns
- **Counting preimages naively for non-analytic maps** — multiplicities can be negative or zero and cancel (the folding x + i|y| example).
- **Assuming ν[f(Γ), p] = 0 means no preimages** — only valid for analytic f; continuous maps can cancel.
- **Ignoring multiplicity in root counts** — a double root counts twice; the winding number insists.
- **Applying Rouché with ≤ instead of <** on the boundary — strict inequality needed for the homotopy to avoid 0.
- **Thinking the Argument Principle needs conformality** — it's topological; conformality only guarantees positivity.

## Reference Tables
### Winding toolkit
| Tool | Statement |
|---|---|
| Crossing rule | cross left→right: ν+1; right→left: ν−1 |
| Ray test | intersections ≥ \|ν\|, extras in cancelling pairs |
| Hopf | K ≃ L (avoid p) ⟺ ν equal |
| Archetype | Î_ν(z) = z^ν |
| Argument Principle | N = ν[f(Γ), p] (analytic, with multiplicity) |
| Topological version | ν[h(Γ),p] = Σ local degrees (continuous) |
| Rouché | \|f−g\| < \|g\| on Γ ⟹ same zero count inside |
| Darboux | analytic, 1-1 on Γ ⟹ 1-1 inside |

### Multiplicity meanings
| View | Definition | Analytic value |
|---|---|---|
| Algebraic | first nonzero Taylor term Δⁿ | n |
| Geometric | winding of image of small circle | n |
| Topological | local degree ν[h(Γ_a), p] | n (always > 0) |

## Key Takeaways
Winding numbers turn geometry into arithmetic: inside, deformation class, and preimage count.
The Argument Principle N = ν[f(Γ), p] is the counting engine of complex analysis — roots are windings.
Rouché's theorem (boundary domination) proves the Fundamental Theorem of Algebra in one stroke.
Multiplicity is one concept wearing algebraic, geometric, and topological faces.
Analytic maps are orientation-preserving: their local degrees are positive — the topological signature of analyticity.

## Connects To
Ch8's Cauchy's theorem uses ν (and the deformation invariance of Hopf) to define integrals over loops and prove the general Cauchy theorem; ch9's Cauchy formula counts via the same principle; ch10's index of singular points and Poincaré-Hopf are the vector-field avatar of these multiplicities; ch2's multifunction branches and ch13's mapping theorem both lean on winding. Hubbard's degree theory and Axler's algebraic multiplicity (via the minimal polynomial) are the higher-math cousins of the same counting.
