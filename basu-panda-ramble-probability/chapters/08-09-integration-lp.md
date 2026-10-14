# Ch8–9 — Integration, expectation, Lp spaces

## Ch8 — Integration and expectation
- **Three-step integral**: (1) simple f = Σaᵢχ_{Aᵢ}: ∫f dµ = Σaᵢµ(Aᵢ); (2) nonnegative measurable: ∫f = sup over simple s ≤ f = lim of the approximating sequence (MCT makes this consistent); (3) general: ∫f = ∫f⁺ − ∫f⁻, defined when at least one is finite; **integrable** = ∫|f| < ∞ (⇒ finite a.e., and ∫f = lim ∫sₙ for the approximating simple sequence).
- **The three convergence theorems** (the book's ★ core):
  - **MCT (Thm 8.6.1 ★)**: fₙ ↑ f, fₙ ≥ 0 ⇒ ∫fₙ ↑ ∫f. No domination needed — monotonicity is the license.
  - **Fatou (8.6.3)**: ∫lim inf fₙ ≤ lim inf ∫fₙ (equality under domination). Fatou is the workhorse for "≤" bounds; strict inequality example: escaping/oscillating mass.
  - **DCT (8.6.4 ★)**: fₙ → f a.e., |fₙ| ≤ g integrable ⇒ ∫fₙ → ∫f. **BCT (8.6.5)**: finite measure space + uniform bound + a.e. convergence.
  - Sequence-of-functions pathologies to keep in mind: escaping to infinity, concentrating spikes — exactly what domination/tightness exclude.
- **Expectation = Lebesgue integral of the r.v.**: E(X) = ∫X dP = ∫x dF(x) = ∫x f(x)dx when a density exists. Properties (Thm 8.3.2): linearity (no independence needed), monotonicity, E(χ_A) = P(A).
- **Riemann vs Lebesgue (8.4)**: Riemann integrates by slicing the *domain*; Lebesgue by slicing the *range*. Riemann integrable ⇒ Lebesgue integrable, equal values. **Riemann-Stieltjes ∫g dF vs Lebesgue-Stieltjes**: equal when F is a distribution function and g nice (Thm 8.4.1) — this is why probability notation ∫g(x)dF(x) is safe.
- **Measures induced by integration (8.5)**: ν(A) = ∫_A f dµ defines a measure with density f (dν = f dµ) — the forward direction of Radon-Nikodym, and the seed of Ch11/Ch12.
- **Inequalities (8.7)**: Markov (P(f≥α) ≤ E(f)/α), **Chebyshev** (P(|X−µ|≥ε) ≤ Var/ε²), **Jensen ★** (φ convex ⇒ φ(E X) ≤ E φ(X)), Lyapunov (moments increase log-convexly), Hölder, Minkowski. All are one-line integral tricks; all are load-bearing in the limit theorems.
- **Moments (8.8)**: E(Xⁿ), variance, covariance, correlation; Var(ΣXᵢ) = ΣVar + 2Σcov; uncorrelated ≠ independent (examples given). **MGF (8.10)** M(s)=E e^{sX}: moments by differentiation when it exists — but it may NOT exist; characteristic functions (Ch15) fix that.
- Change of variables (8.9): E(g(X)) = ∫g(x) dP_X(x) — the "transport" identity used constantly; parameter-dependent integrals (8.10): continuity/differentiation under the integral sign via DCT.

## Ch9 — Lp spaces (✖ optional but recommended for the later chapters)
- ‖X‖_p = (E|X|ᵖ)^{1/p}; identify a.e.-equal r.v.s; Minkowski makes it a norm; **L∞ = ess sup**.
- **Completeness (Riesz-Fischer, 9.3)**: Lp is Banach — Cauchy in p-norm ⇒ convergent in p-norm. This is why L² is a safe home for mean-square arguments.
- Simple functions dense (9.4); Lp separable when the base σ-algebra is; **nesting** (9.5): on a probability space L^q ⊂ L^p for q>p (finite measure helps); **convergence in Lp ⇒ in measure ⇒ in probability** (9.6).
- **L² is a Hilbert space** (9.7): ⟨X,Y⟩ = E(XY), orthogonal = uncorrelated, projections, orthonormal systems — the language Ch12.10 uses to characterize conditional expectation as the best approximation.

## Practitioner takeaways
- Every "can I swap limit and integral?" question is answered by exactly one of MCT/Fatou/DCT — find which hypothesis you have; if none, hunt for the counterexample (spikes/escape).
- Domination g is a tightness assumption in disguise; Ch14's tightness and Ch16's Lindeberg condition are the same idea at the level of measures.
- E(g(X)) = ∫g dP_X lets you compute everything from distributions alone — never integrate over Ω when you can integrate over ℝ.
