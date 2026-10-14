# Cheatsheet — A Ramble through Probability (Basu & Panda)

## Convergence ladder (Ch13-14)
- Lp convergence ⇒ convergence in probability ⇒ (subsequence a.s.); a.s. ⇒ in probability. None of the converses hold in general (unfair coins; typewriter).
- a.s. ⇔ P(limsup{|Xᵢ−X|>ε}) = 0 ∀ε (BC language).
- In probability ⇒ a.s. along a subsequence.
- Convergence in distribution: only laws; Xᵢ ᵈ→ X, Yᵢ ᵖ→ c ⇒ Slutsky (sums/products/quotients); continuous mapping g(Xᵢ) ᵈ→ g(X) at continuity points.
- Weak convergence test set: continuity sets (Q(∂A)=0) or bounded continuous g (Portmanteau).
- Tight ⇒ relatively compact (Prokhorov ★); Helly: subsequence to a possibly-defective F.

## Inequalities (Ch8)
- Markov: P(f ≥ α) ≤ E(f)/α. Chebyshev: P(|X−µ| ≥ ε) ≤ Var/ε². (Special case for piecewise-constant f proved in Ch3 with Riemann integrals.)
- Jensen: φ convex ⇒ φ(EX) ≤ Eφ(X) (and conditional version 12.5.7).
- Hölder: |E XY| ≤ ‖X‖_p‖Y‖_q, 1/p+1/q=1; Minkowski: ‖X+Y‖_p ≤ ‖X‖_p+‖Y‖_p; Lyapunov: (E|X|^r)^{1/r} increasing in r.
- Var(ΣXᵢ) = ΣVar(Xᵢ) + 2Σ_{i<j}Cov(Xᵢ,Xⱼ); independent ⇒ covariances vanish.

## Characteristic function table (Ch15)
| Law | φ(t) |
|---|---|
| δ_c | e^{itc} |
| Bernoulli(p) | 1−p+p e^{it} |
| Uniform[a,b] | (e^{itb}−e^{ita})/(it(b−a)) |
| exp(θ) | 1/(1−iθt) |
| N(µ,σ²) | e^{iµt−σ²t²/2} |
| Cauchy(γ) | e^{−γ|t|} |
- φ_{aX+b}=e^{ibt}φ_X(at); X⊥Y ⇒ φ_{X+Y}=φ_Xφ_Y; |φ|≤1, φ(0)=1, uniformly continuous; real φ ⇔ X d= −X.
- Inversion at continuity points: F(b)−F(a) = lim_{T→∞} (1/2π)∫_{−T}^{T} (e^{ita}−e^{itb})/(it) φ(t) dt.
- Moments: E Xⁿ = i^{−n} φ^{(n)}(0) when E|X|ⁿ<∞ (even n: one-sided suffices).
- **Lévy continuity ★**: φⱼ → g pointwise, g continuous at 0 ⇒ g=φ_F, Fⱼ ᵈ→ F. Discontinuous-at-0 limit = escaping mass (uniform on (−j,j) → χ_{0}).

## CLT conditions (Ch16)
- i.i.d. CLT: finite mean µ, 0<σ²<∞ ⇒ (Sₘ−mµ)/(σ√m) ᵈ→ N(0,1). Proof: (φ(t/√m))^m → e^{−t²/2}.
- **Lindeberg-Feller ★**: independent, centered, variances σ²ⱼ, s²ₘ=Σσ²ⱼ; L(m;ε)=(1/s²ₘ)Σ E[Xⱼ²χ{|Xⱼ|>εsₘ}] → 0 ∀ε ⇒ CLT; converse needs maxⱼσ²ⱼ/s²ₘ → 0.
- u.a.n.: maxⱼ P(|Xⱼ|>εsₘ) → 0 — no single summand dominates.
- Cauchy: Sₘ/m d= X₁ (stable); no CLT because E|X|=∞.
- Delta method ★: aₘ(Xₘ−c) ᵈ→ X, g differentiable at c ⇒ aₘ(g(Xₘ)−g(c)) ᵈ→ g′(c)X; use higher derivative when g′(c)=0.

## LLN roster (Ch13)
- WLLN1: i.i.d., finite variance. SLLN1 ★: i.i.d., finite variance (subsequence ⌊α^j⌋ + BC + maximal inequality). SLLN2 ★: independent, Σσᵢ²/i² < ∞. WLLN2: (1/m²)Σσᵢ² → 0.
- Glivenko-Cantelli ★: sup_x|Fₘ(x)−F(x)| →ᵃˢ 0.
- Kolmogorov convergence criterion: independent mean-zero, ΣVar < ∞ ⇒ ΣXᵢ converges a.s.
- Kolmogorov 0-1 law ★: tail events of independent sequences: probability 0 or 1.

## Measure construction checklist (Ch4-5)
1. Generators (intervals/cylinders) → algebra; µ₀((a,b]) = F(b)−F(a).
2. Countable additivity of µ₀ on the algebra (the hard lemma).
3. µ*(A) = inf Σµ₀(covers); Carathéodory splitting test; restriction is a measure on σ(algebra).
4. σ-finite ⇒ unique extension. Complete if needed.
- F increasing right-continuous ⇔ LS measure µ_F; P_X = µ_{F_X}.

## Conditional expectation quick facts (Ch12)
- E(X|G): G-measurable, ∫_B match ∀B∈G, a.s. unique; exists for E|X|<∞ (via RN).
- Tower: E(E(X|G)|H)=E(X|H), H⊂G. Known factors out. Jensen conditional. E(χ_A|G)=P(A|G).
- E(X|Y)=g(Y) where g minimizes E(X−g(Y))² (best approximation 12.5.8).
- Regular conditional: Φ(ω,B)=P(X∈B|G)(ω) a.s., a true measure in B (ℝⁿ targets ★); disintegration P(A)=∫Φ_y(A)dP_Y(y), Φ_y on fiber Y⁻¹(y).

## KDE (Ch16.6)
- fₘ(x) = (1/mδₘ) Σ ω((x−Xᵢ)/δₘ); kernels: rectangular (=histogram), triangular, Gaussian.
- E fₘ(x) → f(x) at continuity points (Bochner ★); bias ≈ (δₘ²/2)f″(x)ω₂, variance ≈ (1/(mδₘ))f(x)∫ω².
- Choose δₘ → 0 with mδₘ → ∞.

## Book navigation
- Parts: I Nature Trail (1-3), II Foothills (4-9), III Mountain Chain (10-12), IV False Summit (13-16).
- ★ = core sections/theorems; ✖ = optional/advanced (Hausdorff measure, tail σ-algebras early, stochastic processes, Riesz, Bayes section, KDE, weak convergence in ℝⁿ).
- Every chapter ends with Worked problems; Ch1-3 proofs are elementary-but-provisional ("rigorous once Ch4-5 exist").
