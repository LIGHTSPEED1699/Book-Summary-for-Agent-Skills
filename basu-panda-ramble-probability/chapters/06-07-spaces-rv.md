# Ch6–7 — Probability spaces, Borel-Cantelli, measurable functions, random variables

## Ch6 — The Kolmogorov model lands
- **Probability space (Ω, F, P)**: measure with P(Ω)=1; **events** = measurable sets; the coin-toss space of Ch3 is the prototype (Ω = sequences, F = generated σ-algebra, P = the extension measure).
- **Independence of events**: P(∩Aᵢ) = ∏P(Aᵢ) for finite collections; extension to countable families. Pairwise ≠ mutual independence — the book constructs the standard counterexamples.
- **"Infinitely often"**: {Aᵢ i.o.} = ∩ₙ∪_{i≥n} Aᵢ = limsup Aᵢ — an event only because σ-algebras are countably complete. This construction is the hinge of everything zero-one.
- **First Borel-Cantelli Lemma (Thm 6.3.6)**: ΣP(Aᵢ) < ∞ ⇒ P(Aᵢ i.o.) = 0. No independence; pure subadditivity + continuity from above.
- **Second Borel-Cantelli (Thm 6.5.1)**: independence + ΣP(Aᵢ) = ∞ ⇒ P(Aᵢ i.o.) = 1. (Proof via ∏(1−pᵢ) = 0 when Σpᵢ = ∞.)
- Usage pattern: to prove "event happens eventually with probability 1", bound failures by a summable series; to prove recurrence, exhibit independent sub-events with divergent sum.
- **Tail σ-algebra** (6.6 ✖): ∩ₙ σ(Aₙ, Aₙ₊₁, …) — events insensitive to any finite prefix (limit of averages, convergence of series). Kolmogorov's 0-1 law (proved in 13.5) says tail events for independent sequences have probability 0 or 1: **asymptotic statements are deterministic**.

## Ch7 — Measurable functions and random variables
- **Everything is inverse images.** σ(Y) = {Y⁻¹(B) : B ∈ Borel} is the minimal σ-algebra making Y measurable — read it as "the information Y carries". f is measurable iff f⁻¹(B) ∈ F for all Borel B; enough to check on generating sets (intervals (−∞,x]).
- **Approximation theorem (7.3)**: every nonnegative measurable f ↑ limit of an increasing sequence of **simple functions** (dyadic quantization of the range); general measurable f = f⁺ − f⁻. This is the first rung of every integration/limit proof.
- **Pushforward**: a measurable f induces a measure ν(B) = µ(f⁻¹(B)) on the target space. For r.v. X: **P_X(X≤x) = F_X(x)** — the distribution function; monotone, right-continuous, limits 0/1; conversely every such F is some r.v.'s distribution (via LS measure). Discrete (jumps → atoms), absolutely continuous (density), singular (Cantor) — the trichotomy.
- **Random variables** = measurable maps to ℝ; **random vectors** = to ℝⁿ (measurable iff coordinates are). Composition rule: measurable ∘ measurable = measurable; continuity ⇒ Borel measurability.
- The pattern to internalize: to handle a hard measurable object, approximate it by a simple one (simple functions, cylinders, step functions) and pass to limits using the convergence theorems of Ch8.
