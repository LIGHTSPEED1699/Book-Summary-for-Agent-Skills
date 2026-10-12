# Chapter 0: Preliminaries

## Core Idea
The book's reading kit: quantifiers, sets, functions, real and complex numbers, and the discipline of reading mathematics itself. The unusual move is pedagogical — understanding is allowed to be partial and circular ("go on ahead and then circle back"), and examples may precede definitions. Everything later (derivatives as linear maps, forms as integrands) leans on this chapter's function/set language.

## Frameworks Introduced
- **Reading protocol (0.1)**: understand the statement before the proof; hunt "where δ is such and such"; skip to examples and reconstruct the general statement afterward; read with pencil and paper making small examples.
- **Sum/product notation (0.1)**: two-dimensional reading of Σ and Π indices; translate Σ ai,k bk,j into the explicit dot-product sum.
- **Quantifiers and negation (0.2)**: ∀/∃ order matters; negation flips quantifiers (¬∀ = ∃¬); the template for every counterexample in the book.
- **Set theory (0.3)**: subsets, unions/intersections, images and preimages f(U), f⁻¹(V) — preimages behave well under all operations, images only partially.
- **Functions (0.4)**: domain/codomain/graph; injective, surjective, bijective; inverse functions; composition order.
- **Real numbers (0.5)**: decimals and k-truncation, absolute value, intervals, sup/inf (developed further in Appendix A1).
- **Infinite sets (0.6)**: countability, cardinality comparisons.
- **Complex numbers (0.7)**: arithmetic, conjugate, modulus, Euler's formula e^{iθ} = cos θ + i sin θ.

## Key Concepts
- Theorem = statement + proof; the statement is the load-bearing part.
- Negation drills: "every ε > 0 there exists δ > 0…" negated to "there exists ε > 0 such that for every δ > 0…" — the pattern behind every "not continuous/not integrable" example later.
- Preimage discipline: f⁻¹ commutes with complement/union/intersection; injectivity/surjectivity characterized by f(f⁻¹(V)) and f⁻¹(f(U)).
- k-truncation of decimals as the book's concrete handle on real-number arithmetic (used again in Appendix A for analysis proofs).
- Euler's formula as the workhorse for complex arithmetic in rotations and forms.

## Mental Models
- "Partial understanding is the working state": the rock-climber metaphor — don't demand equilibrium at every hold; understanding arrives retroactively from examples.
- "Quantifier order is the sentence's skeleton": swap or negate carefully; most analysis traps live here.
- "Functions are the atoms, matrices their representations": ch0's function vocabulary (image, preimage, inverse) reappears as rank/kernel language in ch1-2.

## Anti-patterns
- **Refusing to proceed past a half-understood sentence** — the book explicitly argues this blocks learning.
- **Negating quantifiers in place without flipping them**.
- **Assuming images commute with set operations** (they don't; preimages do).
- **Treating ΣΣ as a product of sums** — nested sums bind indices separately.

## Reference Tables
### Quantifier negation
| Statement | Negation |
|---|---|
| ∀x P(x) | ∃x ¬P(x) |
| ∃x P(x) | ∀x ¬P(x) |
| ∀ε ∃δ | ∃ε ∀δ ¬ |

### Function properties
| Property | Test |
|---|---|
| injective | f⁻¹(f(U)) = U; singletons have single preimages |
| surjective | f(f⁻¹(V)) = V |
| bijective | inverse function exists |

## Key Takeaways
Read for statements first, examples as sense-making, partial understanding as normal.
Quantifier discipline and preimage discipline are the two technical habits the whole book reuses.
Complex numbers and Euler's formula arrive before any linear algebra.

## Connects To
Ch1's derivative-as-linear-transformation needs the function/inverse vocabulary; Appendix A rebuilds the reals (A1) and completeness (A2-A3) rigorously when the book switches to proof mode. The quantifier templates reappear verbatim in continuity (4.3), measure zero (4.4), and the inverse function theorem (5.1).
