# Chapter 9: Cauchy's Formula and Its Applications

## Core Idea
Cauchy's Formula f(a) = (1/2πi) ∮_L f(z)/(z−a) dz is the precise statement of analytic rigidity: boundary values on a loop *are* the interior values — the interior value equals the average over any circle (Gauss's Mean Value Theorem). Differentiating under the integral sign gives infinite differentiability and Taylor series; expanding at poles gives Laurent series and the full calculus of residues, which then evaluates real integrals by closing contours in the upper half-plane.

## Frameworks Introduced
- **Cauchy's Formula (I)**: two proofs from Cauchy's Theorem — (1) deform L to a tiny circle and read the integral as the circular average of f, which shrinks to f(a); (2) the difference-quotient map F_a(z) = [f(z) − f(a)]/(z − a) is analytic, forcing the formula.
- **Gauss Mean Value Theorem (I.3)**: analytic (indeed harmonic) functions equal their circle averages — the mean-value property characterizes harmonicity (sufficiency in ch12).
- **General Cauchy Formula (I.4)**: for non-simple loops: (1/2πi) ∮ f(z)/(z−a) dz = ν[L,a]·f(a) — winding number as multiplicity.
- **Infinite differentiability (II.1)**: f′(a) = (1/2πi) ∮ f(z)/(z−a)² dz; f⁽ⁿ⁾(a) = (n!/2πi) ∮ f(z)/(z−a)ⁿ⁺¹ dz — differentiate under the integral; analytic ⟹ C^∞ with proof.
- **Taylor series (II.2)**: expand 1/(Z−z) as geometric series inside Cauchy's integral; term-by-term integration justified by the ML estimate; cₙ = f⁽ⁿ⁾(a)/n!; radius of convergence = distance to nearest singularity or branch point.
- **Laurent series at poles (III.1)**: pole of order m ⟹ f = φ(z)/(z−a)^m with φ analytic ⟹ Laurent expansion with finitely many negative powers; residue = coefficient c_{−1} = φ⁽ᵐ⁻¹⁾(a)/(m−1)!.
- **Residue calculus (III.2)**: general Residue Theorem ∮ f dz = 2πi Σ ν[L,aₙ] Res[f,aₙ]; quick formulas: simple pole of P/Q: Res = P(a)/Q′(a); order-m pole: (1/(m−1)!) d^{m−1}/dz^{m−1}[(z−a)^m f] at a.
- **Real integrals (III.3)**: close the real axis with a large semicircle; ∫_{−∞}^{∞} = 2πi Σ residues in upper half-plane (Jordan-type estimates); trigonometric integrals via z = e^{iθ} on the unit circle.

## Key Concepts
- Boundary-to-interior transfer: the loop integral with kernel 1/(z−a) is an "average" that reproduces interior values — rigidity made arithmetic.
- Winding number as the multiplicity factor in every general formula (Cauchy, residue).
- The kernel 1/(z−a) differentiates to produce all derivative formulas — one identity, infinitely many consequences.
- Radius of convergence is geometric: nearest singularity/branch point, not a coefficient mystery.
- Poles have finite principal parts (Laurent); residues are their 1/(z−a) coefficients; essential singularities have infinite principal parts (foreshadowed).
- Real-integral evaluation = contour closure + residue bookkeeping; the semicircle's contribution must be estimated away (ML bound).
- Harmonic functions inherit the mean-value property; the mean-value property is the seed of maximum principle (ch12).

## Mental Models
- "The boundary is a hologram of the interior": Cauchy's formula reconstructs every interior value from loop values.
- "Average on circles = value at centre": harmonic functions are perfectly balanced; deviation from balance detects sources (Laplacian ≠ 0).
- "Differentiate the kernel, not the function": all derivative formulas come from d/da of 1/(z−a).
- "Convergence radius is a wall of singularities": power series stop exactly at the nearest obstacle — analysis reads geometry.
- "Close the contour, sum the residues": real integrals become arithmetic over upper-half-plane poles.

## Anti-patterns
- **Applying Cauchy's formula when f has singularities between a and L** — "inside" must be singularity-free except at a.
- **Forgetting winding numbers for non-simple loops** — the general formulas carry ν[L,a] and ν[L,aₙ].
- **Assuming Taylor series converge past the nearest singularity** — the radius is exactly the distance to it (real-variable intuition fails: 1/(1+x²) looks smooth but radius 1 from ±i).
- **Using the P(a)/Q′(a) residue formula at multiple poles** — it requires a *simple* root of Q.
- **Closing contours in the wrong half-plane** — pick the half-plane where the arc dies (e^{iaz}: upper for a > 0).

## Reference Tables
### The Cauchy ladder
| Object | Formula |
|---|---|
| value | f(a) = (1/2πi)∮ f(z)/(z−a) dz |
| general loop | (1/2πi)∮ f/(z−a) = ν[L,a] f(a) |
| n-th derivative | f⁽ⁿ⁾(a) = (n!/2πi)∮ f(z)/(z−a)ⁿ⁺¹ dz |
| Taylor | f(z) = Σ f⁽ⁿ⁾(a)/n! (z−a)ⁿ, R = dist to nearest singularity |
| residue (order m) | Res = (1/(m−1)!) [d^{m−1}/dz^{m−1} (z−a)^m f]_{z=a} |
| residue (P/Q simple pole) | P(a)/Q′(a) |
| Residue Theorem | ∮ f dz = 2πi Σ ν[L,aₙ] Res[f,aₙ] |

### Series taxonomy
| Type | Negative powers | Where |
|---|---|---|
| Taylor | none | analytic disc |
| Laurent at pole | finitely many (order m) | punctured nbhd of pole |
| Laurent at essential singularity | infinitely many | punctured nbhd |

## Key Takeaways
Cauchy's Formula = rigidity made explicit: interior values are boundary averages (Gauss MVT).
One kernel 1/(z−a) generates derivatives, Taylor, and Laurent theory by differentiation and expansion.
Radius of convergence is the distance to the nearest singularity or branch point — geometry, not algebra.
Residues are Laurent 1/(z−a) coefficients; the Residue Theorem with winding numbers evaluates everything.
Real integrals fall to contour closure plus upper-half-plane residue sums.

## Connects To
Ch7's argument principle becomes the residue-counting form (N = Σ winding × multiplicity) used in ch13; ch8's deformation theorem powers both proofs here; ch10-11's physical integrals (flux/circulation, sources) are residue interpretations; ch12's harmonic functions get their mean-value/max-principle from Gauss MVT; ch13's Riemann mapping theorem uses boundary-interior duality. Hubbard's residue-style partial fractions and Strang's Laplace inversion integrals are applied cousins.
