# Appendix: Analysis

## Core Idea
The proof engine, kept off the main road: the book runs applied first and proves the hard theorems here — real-number arithmetic via decimals (with a sharp eye on computer arithmetic), chain rule, inverse and implicit function theorems, equality of crossed partials, Taylor with remainder, Heine-Borel, Stirling, and Lebesgue measure. A course can be run as analysis by pairing each chapter with its appendix sections.

## Frameworks Introduced
- **A1 Arithmetic of real numbers**: reals as equivalence classes of decimals (0.999… = 1); k-truncation; why computer arithmetic is non-associative (floating point) — numerical problems demand serious attention to arithmetic itself.
- **A2 Cubic and quartic equations**: explicit formulas; complex numbers forced by real roots (casus irreducibilis).
- **A3 Two results in topology**: Heine-Borel (compact = closed and bounded) and its uses.
- **A4 Proof of the chain rule**; **A6 proof of the superconvergence lemma (2.9.5)**; **A7/A8 proofs of the inverse and implicit function theorems** (Newton/Banach-flavored iteration).
- **A9 Equality of crossed partials** (Clairaut/Schwarz); **A10 functions with many vanishing partials** (flat functions — the C∞ vs analytic gap).
- **A11 Rules for Taylor polynomials + big-O arithmetic**; **A12 Taylor's theorem with remainder** (integral remainder).
- **A13 Completing squares** (the quadratic-form algorithm's proof); **A16 Stirling's formula**; **A21 Lebesgue measure and measurable sets**.

## Key Concepts
- Decimals-as-reals makes completeness elementary: nested intervals/truncation instead of Dedekind cuts.
- Floating-point failure of associativity: (a+b)+c ≠ a+(b+c) on computers — the book's numerical honesty.
- Inverse function theorem proved by constructing the local inverse via Newton iteration — the Kantorovich machinery from ch2 in proof form.
- Flat functions (e^{-1/x²}) show Taylor series need not represent the function — why the book uses Taylor polynomials, not series.
- Heine-Borel is the compactness source behind ch1's five big theorems.

## Mental Models
- "Applied first, proofs on tap": the appendix structure is a pedagogical contract — use the theorem now, see it proved when ready.
- "Iteration proves existence": inverse/implicit/superconvergence all via Newton-type fixed points.
- "Remainder is the honest part of Taylor": polynomials approximate; the remainder bounds the lie.

## Anti-patterns
- **Trusting floating-point algebra laws** in numerical work (A1's warning).
- **Assuming C∞ = analytic** (A10's flat functions refute it; Taylor series can be identically zero at a non-analytic point).
- **Using Taylor series where Taylor's theorem with remainder is what's justified**.

## Reference Tables
### Appendix map
| Section | Proves / develops |
|---|---|
| A1 | decimals, truncation, computer arithmetic |
| A3 | Heine-Borel compactness |
| A4 | chain rule |
| A6 | superconvergence lemma (Newton) |
| A7-A8 | inverse + implicit function theorems |
| A9 | crossed partials equal (C²) |
| A10 | flat C∞ functions |
| A11-A12 | Taylor rules, big-O, remainder |
| A13 | completing squares |
| A16 | Stirling |
| A21 | Lebesgue measure, measurable sets |

## Key Takeaways
The inverse/implicit function theorems are iteration theorems — ch2's Newton is the proof.
Real-number foundations here are computational (decimals, truncation), not set-theoretic.
Flat functions mark the limit of polynomial approximation — use remainders, not series faith.

## Connects To
Justifies ch1's big theorems (A3), ch2's Newton/Kantorovich (A6-A8), ch3's Taylor machinery (A11-A12), ch4's Lebesgue extension (A21). Axler's book stays algebraic; this appendix is the analysis half of the shelf.
