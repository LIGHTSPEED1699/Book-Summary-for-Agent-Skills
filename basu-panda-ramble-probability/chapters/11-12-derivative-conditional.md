# Ch11–12 — Derivatives of measures, conditional expectation, disintegration

The mountain chain's summit pair: Radon-Nikodym, then conditional expectation as its application.

## Ch11 — Derivatives of measures
- **Countably additive set function / signed measure** φ: M → R (∞ or −∞ but not both); Remark 11.1.2: when φ(∪Aᵢ) is finite the series must converge **absolutely** — order-independence forces it.
- **Hahn Decomposition (11.1.2 ★)**: X = A⁺ ∪ A⁻ disjoint, φ ≥ 0 on subsets of A⁺, φ < 0 on subsets of A⁻. Proof: take a maximizing sequence for sup φ, union it, and the "if a negative piece hides inside A⁺ you'd beat the sup" trick.
- **Jordan Decomposition**: φ = φ⁺ − φ⁻ with φ⁺ ⊥ φ⁻, φ± measures; total variation |φ| = φ⁺+φ⁻.
- **≪ (absolutely continuous)**: µ(A)=0 ⇒ φ(A)=0. **⊥ (mutually singular)**: concentrated on disjoint null-complementary sets. ε-δ characterization of ≪ for finite measures (the compactness lemma that powers the RN proof).
- **Lebesgue-Radon-Nikodym Theorem (11.3.1 ★)**: φ = φ_ac + φ_s; φ_ac(A) = ∫_A f dµ with f = dφ/dµ unique µ-a.e.; φ ≪ µ iff φ_s = 0. Proof route: maximize ∫f dµ over admissible densities, correct the residual on the set where it's positive (the classic "maximal density" argument); σ-finite case by patching finite pieces.
- **Properties (11.4)**: chain rule dφ/dν · dν/dµ = dφ/dµ; densities transform; d(µ₁+µ₂)/dµ = sum; conditional-expectation-style identities.
- ✖ 11.5: differentiating a measure as a limit of ratios µ(B_r)/µ_L(B_r) → density (Vitali covering flavor); ✖ 11.6: Riesz representation — (Lp)* = Lq via RN.

## Ch12 — Conditional expectation and disintegration
- Conditional probability given a σ-algebra: P(A|G) = E(χ_A|G) — a **random variable**, not a number; "not a probability measure in general... a reflection of the need for a kind of smoothness" (the null-set-independence problem that forces regular conditional measures).
- **E(X|G) (12.4.1 via RN)**: the a.s.-unique G-measurable integrable r.v. with ∫_B E(X|G)dP = ∫_B X dP for all B ∈ G. Definition = RN derivative of ν(B)=∫_B X dP restricted to G. **Conditional expectation IS a Radon-Nikodym derivative** — the book's structural spine.
- Computing it: on a partition-generated G, E(X|G) is constant on each cell = the ordinary conditional mean; for G = σ(Y), E(X|Y)(ω) = g(Y(ω)) — find g by requiring matching integrals (smoothing).
- **Properties (12.5)**: linearity, monotonicity, E(E(X|G)|H) = E(X|H) for H⊂G (**tower law**), taking out what's known (Z G-measurable ⇒ E(ZX|G) = Z E(X|G)), Jensen for conditional expectation (12.5.7), E(X|σ(trivial)) = EX, E(X|F) = X.
- **Best approximation (12.5.8)**: E(X|Y) minimizes E((X−g(Y))²) over all measurable g — conditional expectation = **orthogonal projection** onto the closed subspace of σ(Y)-measurable L² functions (12.10 ✖ makes the Hilbert geometry explicit).
- **Regular conditional probability (12.6.1 ★)**: for X into ℝⁿ there is a kernel Φ(ω,B) that is a genuine probability measure in B for a.e. ω, with Φ(ω,B) = P(X∈B|G)(ω) a.s. Proof: choose versions on the countable dense set Qⁿ, intersect the null sets — **countability + right-continuity is what makes a single null set work for all B**.
- **Disintegration (12.7.1 ★)**: the family {Φ_y} with Φ_y concentrated on the fiber Y⁻¹(y) (even though P(Y⁻¹(y))=0!), and P(A) = ∫ Φ_y(A) dP_Y(y). The general "condition on a measure-zero event correctly" machine; the density form (12.7.2) is the familiar ∫ p(x|y)p(y)dy. **Bayes' theorem (12.8 ✖)** = disintegration read backwards (posterior density from likelihood × prior), stated measure-theoretically.
- **Conditional independence and the Markov property (12.9)**: P(A∩B|G) = P(A|G)P(B|G); Markov = future ⊥ past | present — expressible cleanly only in this σ-algebra language.

## Practitioner takeaways
- Any time you "condition on Y=y with P(Y=y)=0", you are implicitly choosing a disintegration; regular conditional probabilities say a canonical choice exists for ℝⁿ-valued Y. Non-ℝⁿ state spaces can genuinely fail to have one.
- Do the Borel-Kolmogorov-style sanity check: conditioning must be on σ-algebras, not on events of measure zero.
- Projection view: conditional expectation is the L²-optimal predictor from the observed information — regression, Kalman filters, and MMSE estimators are all this theorem wearing clothes.
