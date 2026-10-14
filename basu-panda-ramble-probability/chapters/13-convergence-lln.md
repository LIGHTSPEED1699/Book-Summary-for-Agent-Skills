# Ch13 (Part IV) — Sequences of r.v.s and the Laws of Large Numbers

Part IV's epigraph (Hoffman-Jørgensen): Kolmogorov's model "doesn't say anything about the probability of a given event; nevertheless, the frequential interpretation is the main link between reality and probability theory. Thus, within the framework of Kolmogorov we have to prove the validity of the frequential interpretation, that is, to prove the law of large numbers." (The "False Summit" title: reaching the LLN/CLT feels like the top, but the real mountain — statistics, processes, applications — lies beyond.)

## The convergence ladder (13.1)
- **In probability**: P(|Xᵢ−X|>ε) → 0. **Almost surely**: P(lim Xᵢ = X) = 1. **In Lp**: E|Xᵢ−X|ᵖ → 0.
- **Thm 13.1.1**: a.s. ⇒ in probability; and a.s. ⇔ P(limsup{|Xᵢ−X|>ε}) = 0 for all ε (Borel-Cantelli language). Converse fails: **increasingly unfair coins** (P(Xᵢ=1)=1/i: in probability to 0, but Xᵢ=1 i.o. a.s. by second Borel-Cantelli) and the **typewriter sequence** (traveling indicator on [0,1]).
- Subsequence extraction: in probability ⇒ a.s. along a subsequence.
- Mnemonic: a.s. controls whole sample paths; in probability controls single-time marginals; Lp controls averages of error size.

## The LLN roster (13.2)
- **WLLN 1 (13.2.1)**: i.i.d., finite variance ⇒ S̄ₘ ᵖ→ µ. Chebyshev + Var(S̄ₘ)=σ²/m.
- **SLLN 1 (13.2.2 ★)**: i.i.d., finite variance ⇒ S̄ₘ →ᵃˢ µ. Proof: subsequence S̄_{⌊α^j⌋} via Chebyshev + Borel-Cantelli, then maximal inequality to fill gaps. The truncation/subsequence/BC pattern is the book's signature SLLN technique.
- **SLLN 2 (13.2.3 ★)**: independent (NOT identically distributed), means µᵢ, variances σᵢ², with Σ σᵢ²/i² < ∞ ⇒ (Sₘ−ESₘ)/m →ᵃˢ 0. Markov's variance condition is the checkable criterion.
- **WLLN 2 (13.2.4)**: same setup, in probability, under (1/m²)Σσᵢ² → 0.
- Finiteness of variance is genuinely load-bearing: without finite mean, sample averages can diverge or converge to the wrong thing (Cauchy preview in Ch16).
- The book's warning (epigraph tradition, from Feller): the LLN is **not** a force with memory correcting past imbalances — no "compensation" fallacy.

## Statistics enters (13.3)
- **Empirical distribution** Fₘ(x) = (1/m)Σχ{Xᵢ≤x}: a random distribution function; E Fₘ(x) = F(x); Var = F(1−F)/m.
- **Glivenko-Cantelli (13.3.3 ★)**: sup_x |Fₘ(x) − F(x)| →ᵃˢ 0 — "the fundamental theorem of statistics": the histogram converges *uniformly*, so the empirical measure is a legitimate estimator of the whole law. Proof: grid + BC + monotonicity sandwich at discontinuities.
- Medians/quantiles: convergence of empirical quantiles to true quantiles (generalized inverse machinery).

## Random series and 0-1 laws (13.4–13.5, ✖)
- Convergence of ΣXᵢ a.s.: **Kolmogorov Convergence Criterion (13.4.5)**: for independent mean-zero, ΣVar(Xᵢ) < ∞ ⇒ ΣXᵢ converges a.s.; **Kolmogorov's inequality** (13.4.2/3) is the maximal inequality used; three-series-style decomposition truncates.
- **Kolmogorov 0-1 Law (13.5.2 ★)**: for independent r.v.s, every tail event (in ∩ₙσ(Xₙ,Xₙ₊₁,…)) has probability 0 or 1. Consequence: {ΣXᵢ converges}, {S̄ₘ converges}, etc. are a.s. determined — **no probability strictly between 0 and 1 for asymptotic yes/no questions**. Independence is essential (the unfair-coin chain shows tail triviality can fail when dependent).

## Practitioner takeaways
- Choose the mode of convergence your application consumes: simulation paths need a.s.; single-run error budgets need in probability or Lp; then pick the cheapest theorem that delivers it.
- The universal SLLN proof skeleton: Chebyshev on a sparse subsequence → Borel-Cantelli → maximal inequality to interpolate. Reuse it for new averaging schemes (weighted means, moving windows).
- Before trusting an empirical estimate: Glivenko-Cantelli justifies plug-in estimation of the *distribution*; anything beyond (parameters, tails) needs its own consistency argument.
