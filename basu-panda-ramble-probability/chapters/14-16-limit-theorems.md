# Ch14–16 — Weak convergence, characteristic functions, Central Limit Theorems

## Ch14 — Sequences of measures / weak convergence
- **Weak convergence of distribution functions (14.1.1)**: Fᵢ → F at every continuity point of F. Continuity-point relaxation is what makes the WLLN fit (Fₘ(0)=1/2 forever in the odd-m coin example, yet WLLN holds). Limit is unique (14.1.1).
- **Mass can escape**: Fᵢ = χ_{[i,∞)} converges pointwise to 0, which is not a distribution function — weak convergence *to a probability* requires the limit to be one; the failure mode is tightness.
- **Portmanteau (14.1.3, and 14.5.1 ★ in ℝⁿ)**: the equivalent faces of weak convergence — Fᵢ(x)→F(x) at continuity points; Qᵢ(A)→Q(A) for continuity sets (Q(∂A)=0); limsup Qᵢ(F) ≤ Q(F) for closed F; liminf for open G; ∫g dQᵢ → ∫g dQ for bounded continuous g. Test against bounded continuous functions and you have the general definition (extends beyond ℝ).
- **Convergence in distribution (14.2)**: Xᵢ ᵈ→ X means F_{Xᵢ} weakly → F_X; says nothing about the r.v.s themselves, only their laws (contrast with a.s./probability/Lp — the book stresses this).
- **Continuous mapping**: Xᵢ ᵈ→ X, g continuous at mass points of X ⇒ g(Xᵢ) ᵈ→ g(X).
- **Slutsky (14.2.5 ★)**: Xᵢ ᵈ→ X, Yᵢ ᵖ→ c ⇒ Xᵢ+Yᵢ ᵈ→ X+c, XᵢYᵢ ᵈ→ cX, Xᵢ/Yᵢ ᵈ→ X/c (c≠0). The workhorse for standardization: replace a random denominator by its limit.
- **Tightness (14.3.1)**: ∀ε ∃[a,b] with Qᵢ([a,b]) ≥ 1−ε for all i — no mass escapes. **Helly Selection (14.3.1)**: every sequence of distribution functions has a subsequence converging weakly to some right-continuous increasing F (possibly defective); proof = **diagonal argument (14.3.2)** on rationals. **Prokhorov (14.3.4 ★)**: tight ⇒ relatively compact (subsequence converging to a *probability*). Tightness = the compactness substitute in infinite spaces.
- **Scheffé (14.4)**: densities fᵢ → f a.e. + ∫fᵢ→∫f ⇒ ∫|fᵢ−f| → 0 (L¹ convergence — stronger than weak); useful for "the density converged" claims. Counterexample (14.8): weak convergence of distributions with wildly non-converging densities (spikes).

## Ch15 — Characteristic functions
- **φ_X(t) = E e^{itX} = ∫e^{itx}dF(x)** (Fourier-Stieltjes). Always exists, |φ| ≤ 1, φ(0)=1, uniformly continuous (15.2.1); real iff X d= −X; φ_{aX+b} = e^{ibt}φ_X(at). Unlike the MGF it never blows up — complex modulus saves it.
- Catalog: uniform [a,b] (sinc), exp(θ) 1/(1−iθt), **N(µ,σ²): e^{iµt−σ²t²/2}**, Bernoulli, Cauchy e^{−γ|t|}.
- **Independence turns products (15.3.1)**: X⊥Y ⇒ φ_{X+Y} = φ_Xφ_Y. The CLT's engine: standardize, take logs, Taylor expand.
- **Lévy Inversion (15.4.1 ★)**: φ determines F uniquely; at continuity points, F(b)−F(a) = lim (1/2π)∫_{−T}^{T} (e^{ita}−e^{itb})/(it) φ(t)dt. **Uniqueness**: same φ ⇒ same law. **Riemann-Lebesgue (15.4.3)**: densities ⇒ φ(t)→0.
- **Moments ↔ smoothness (15.5)**: E|X|ⁿ < ∞ relates to n-th differentiability of φ (one-sided versions: E Xⁿ = i⁻ⁿ φ⁽ⁿ⁾(0) when it exists; differentiability at 0 with even n gives the moment).
- **Lévy Continuity Theorem (15.6.2 ★)**: Fⱼ ᵈ→ F ⇒ φⱼ → φ pointwise; **conversely, φⱼ(t) → g(t) with g continuous at 0 ⇒ g = φ_F and Fⱼ ᵈ→ F**. Continuity at 0 is exactly the tightness condition — the counterexample: uniform on (−j,j) has φⱼ → χ_{0}, discontinuous at 0, and the mass escapes. This is THE limit theorem: prove a pointwise limit of characteristic functions that's continuous at 0, and weak convergence follows for free.

## Ch16 — Central Limit Theorems
- **CLT (i.i.d., 16.2)**: Xᵢ i.i.d., mean µ, 0<σ²<∞ ⇒ (Sₘ−mµ)/(σ√m) ᵈ→ N(0,1). Proof: characteristic functions, Taylor expand log φ near 0 to second order, (1−t²σ²/2m+o(1/m))^m → e^{−t²/2}, Lévy continuity.
- **Counterexample gallery the book insists on**: non-identical independent variables can still be CLT (wiggly exponential rates); **dependent** AR(2) sums fail to look normal (Q-Q plots betray skew/heavy tails); **Cauchy**: Sₘ/m d= X₁ exactly (stable law), no finite mean — no contradiction, the assumptions bite.
- **Lindeberg-Feller (16.2.1 ★)**: for independent (not identically distributed) Xⱼ with variances σ²ⱼ, s²ₘ = Σσ²ⱼ: **Lindeberg's condition** L(m;ε) = (1/s²ₘ)Σ E[(Xⱼ−µⱼ)²χ{|Xⱼ−µⱼ|>εsₘ}] → 0 for all ε ⇒ standardized sum → N(0,1); **Feller's necessity**: CLT + maxⱼ σ²ⱼ/s²ₘ → 0 ⇒ L(m;ε) → 0. Interpretation (book's): **no single summand may dominate the total variance** — **uniform asymptotic negligibility (u.a.n.)**: maxⱼ P(|Xⱼ−µⱼ| > εsₘ) → 0.
- **Triangular arrays (16.4)**: rows of independent r.v.s with m-dependent distributions — the natural habitat of Lindeberg-Feller (weighted sums, regression errors).
- **Delta method (16.5.2 ★)**: if aₘ(Xₘ−c) ᵈ→ X and g is differentiable at c, aₘ(g(Xₘ)−g(c)) ᵈ→ g′(c)X; higher-order version when g′(c)=…=g^{(m−1)}(c)=0. Built from a general perturbation theorem (16.5.1). This is how CLTs get transported through estimators (variance-stabilizing transforms, plug-in functionals).
- **Kernel density estimation (16.6 ✖)**: naive estimate f̂ₘ(x) = (F(x+δₘ)−F(x−δₘ))/2δₘ from the empirical F — rough, rarely used (ill-conditioned ratio). **Kernel estimate**: fₘ(x) = (1/mδₘ)Σ ω((x−Xᵢ)/δₘ) with kernel ω (rectangular = histogram, triangular, Gaussian) and bandwidth δₘ. **Bochner's theorem (16.6.1 ★)** (approximate-identity): ω integrable, |xω(x)|→0, δₘ→0 ⇒ ∫ω_δ(x−y)f(y)dy → f(x) at continuity points ⇒ E fₘ(x) → f(x). Bias ≈ curvature term (δₘ² f″/2 when f is C²), variance ≈ (1/(mδₘ))∫ω²f — **bias shrinks with δₘ, variance blows up as 1/(mδₘ)**: the bandwidth tradeoff, proved with the book's own tools (Binomial law of 2δₘfₘ(x), Theorem 13.3.2).

## The limit-theorem playbook
1. Standardize the quantity; identify the target law's characteristic function.
2. Compute log φ of the standardized sum; Taylor expand to the first surviving order; check the remainder vanishes.
3. Verify continuity at 0 (equivalently tightness / no dominating summand / Lindeberg).
4. Invoke Lévy continuity; move through continuous mapping / Slutsky / delta method to the quantity you actually care about.
5. When assumptions fail (dependence, infinite variance), the book's counterexamples show what replaces normal: stable laws, or nothing.
