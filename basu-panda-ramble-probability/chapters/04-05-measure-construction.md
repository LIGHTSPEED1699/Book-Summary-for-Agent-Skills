# Part II Ch4–5 (The Foothills) — Constructing measures

## Ch4 — σ-algebras, measure, outer measures, premeasures
- **Algebra** (Def 4.1.1): nonempty collection of subsets closed under complements and *finite* unions. **σ-algebra** (Def 4.1.2): closed under *countable* unions. Countability is the price of admitting limits; the half-open-interval unions on (0,1] form an algebra but not a σ-algebra (a countable union of (aᵢ,bᵢ] can need infinitely many pieces); the same collection on ℝ isn't even an algebra — the master set matters.
- Power set P^X = maximal σ-algebra; {∅,X} = minimal. **σ(E) = minimal σ-algebra containing E** (intersection of all such) — the generation pattern used everywhere.
- **Measure** (Def 4.2.x): µ: M → [0,∞] on a σ-algebra, µ(∅)=0, **countable additivity** µ(∪Aᵢ)=Σµ(Aᵢ) for disjoint. Consequences: finite additivity, monotonicity, subadditivity, **continuity from below** (Aᵢ↑A ⇒ µ(Aᵢ)→µ(A)) and **from above** (Aᵢ↓A with some µ(A_m)<∞ — finiteness is essential; counterexample Aᵢ=[i,∞)).
- **σ-finite** = countable union of finite-measure sets: the standing hypothesis for the extension and RN theorems.
- **Jordan measure** warm-up (4.4): inner/outer content by elementary sets; triangle works (1/2), **Q∩[0,1] is not Jordan measurable** — inner content 0, outer content 1 never match. Jordan's class is too small; that failure is why Lebesgue separated *outer size* from *measurability*.
- **Outer measure** (Def 4.4.x): µ*: P^X → [0,∞], µ*(∅)=0, monotone, countably subadditive — defined on ALL subsets, no additivity. Built from an elementary family by infimum of covers: µ*(A) = inf Σµ₀(covers).
- **Carathéodory's condition**: A is µ*-measurable iff µ*(E) = µ*(E∩A) + µ*(E∩Aᶜ) for **every test set E** — A cleanly splits every E. The µ*-measurable sets form a σ-algebra and µ* restricted to it is a measure (the book's central construction theorem).
- **Premeasure** (4.5): countably additive µ₀ on an *algebra* A. **Carathéodory extension**: a premeasure on an algebra extends to a measure on σ(A); the extension is **unique when σ-finite** (the "good sets"/inheritance argument). Completion: add all subsets of null sets.
- Null sets, "almost everywhere", completion of Lebesgue vs Borel measure (Borel measure is not complete; Lebesgue is).

## Ch5 — Lebesgue and Lebesgue-Stieltjes measure on ℝ
- Strategy: start with the algebra A_hi of finite disjoint unions of half-open intervals (a,b]; premeasure µ₀((a,b]) = b−a; verify countable additivity on the algebra (the hard technical lemma: approximation of open sets, 5.1–5.2); extend via Ch4 to a measure on **B(ℝ)** (Borel σ-algebra). Result: **Lebesgue measure µ_L** — translation invariant, µ_L((a,b])=b−a, regular (open sets approximated from within, 5.6 ✖).
- **Lebesgue-Stieltjes measure µ_F** (5.3): for any increasing, right-continuous F with limits at ±∞, premeasure µ₀((a,b]) = F(b)−F(a) → unique measure (Thm 5.3.5 ★). Distribution functions ARE measures and vice versa — the dictionary that makes probability = measure on ℝ.
- Singular examples: Cantor set (measure zero, uncountable), Cantor function (continuous, increasing, derivative 0 a.e.) → singular measure; mixed decompositions of F (jump + singular + absolutely continuous parts, previewed for Ch11).
- Approximation of µ_F-measurable sets by finite interval unions (5.7 ✖) — the working tool that "measurable sets are approximable by simple sets" is true in practice.

## The construction recipe (use it for any new measure)
1. Pick a simple class (intervals, cylinders, rectangles) that generates the σ-algebra you want.
2. Define µ₀ on the algebra it generates; check finite additivity + **countable additivity on the algebra** (where all the real work hides).
3. Invoke Carathéodory: outer measure from covers → measurable sets → measure on σ(A).
4. Check σ-finiteness for uniqueness; complete if needed.

## Pitfalls the book flags
- Finite vs countable additivity: finite additivity + continuity at ∅ are equivalent to countable additivity — the continuity form is often easier to check.
- Continuity from above needs one finite measure.
- Uniqueness of extension needs σ-finiteness; existence doesn't.
- "Measurable" is not "nice": the σ-algebra is defined by closure, and Carathéodory's condition looks magic until you see it as a splitting test.
