# Part I (Ch1–3) — The Nature Trail: probability before measure

The book's gambit: **build probability from coin tosses first, prove the limit laws there with only polynomials, then show the questions outgrow the tools and measure theory is forced.** Part I is deliberately elementary but rigorous "provided we develop a rigorous theory for measure later" — the author flags the uneasiness honestly.

## Ch1 — Probability, coin tosses, and polynomials
- Experiment = repeatable procedure, one result from a specified set of possible results; **sample space**, **trial**. One experiment admits many sample spaces (52 cards / 2 colors / 13 ranks; "Hot/Cold" vs 1° thermometer intervals) — elements of coarse spaces are sets of elements of fine ones. Precision is a choice of sample space, not a property of the world.
- Discrete probability = finite/countable sample space; probabilities p_i ≥ 0, Σp_i = 1; events are subsets; P(A∪B) = P(A)+P(B) for disjoint.
- Coin-toss counting: P(exactly k heads in m tosses) = C(m,k)/2^m via binomial polynomials (x+y)^m; Stirling bounds; the relative frequency of heads concentrates — proved with algebra alone.

## Ch2 — Sets and Functions
- "Admittedly very dry, but very important to everything that follows." Measure theory and probability are structures for analysis on **spaces whose points are sets**.
- Toolkit: sets, complements, De Morgan, countable vs uncountable (Cantor diagonal), Dedekind completeness of ℝ (stated, not constructed), sequences/limits, functions, inverse images (the operation that will run the whole book: measurability is about f⁻¹).

## Ch3 — The coin-toss model and the first limit laws
- **Bernoulli sequence** (Def 3.1.1): independent trials of a two-outcome experiment. Space B of all infinite H/T sequences.
- **Key correspondence**: infinite coin sequences ↔ unit interval via binary expansion (H=0, T=1); a condition on the first m tosses = a union of m-cylinders = a union of dyadic intervals of length 2⁻ᵐ. Probability = total length. **But**: natural questions ("do we go broke?", "is the frequency normal?") correspond to *complicated* sets of reals — this is the motivation bomb for Chapters 4–5.
- **Rademacher functions** R_i(ω) = ±1 on dyadic intervals: the i-th bet's payoff as a function on [0,1]. W_m = Σᵢ Rᵢ = net winnings after m bets.
- **WLLN (Thm 3.2.1)** proved by pure polynomial integration: special Chebyshev for piecewise-constant f (measure of {f>α} ≤ (1/α)∫f), then ∫W_m² = m because ∫Rᵢ² = 1 and **∫RᵢRⱼ = 0 by cancellation** (Rⱼ oscillates an even number of times on each interval where Rᵢ is constant). P(|W_m|/m > δ) ≤ 1/(mδ²) → 0.
- **Normal numbers**: the set where frequency → 1/2; "probability zero = corresponding set of reals has Lebesgue measure zero" (Def 3.3.2, provisional). Nonnormal sequences exist — probability zero ≠ impossible.
- **SLLN (Thm 3.4.1)** via fourth moments: ∫W_m⁴ = 3m²−2m by counting the five kinds of products RᵢRⱼRₖRₗ (m terms of type R⁴, 3m(m−1) of type Rᵢ²Rⱼ², everything else cancels), Borel-Cantelli-style subsequence + monotonicity. The combinatorics of cancellation is the whole proof.
- Numerical-simulation framing: SLLN is what licenses using **one** generated sequence to answer statistical questions.

## Practitioner takeaways
- The dyadic correspondence is the standard bridge from discrete simulation to Lebesgue measure on [0,1] — every PRNG-based Monte Carlo silently uses it.
- Orthogonality of Rademacher functions = independence expressed as vanishing cross-integrals; the same identity reappears as E[XY]=E[X]E[Y] in Ch6–8.
- Expect the "complicated sets" problem: any event defined by an infinite condition on a sequence (ruin, recurrence, normality) is not a finite union of cylinders — you need the σ-algebra machinery before you can even ask for its probability.
