# Chapter 4: Polynomials

## Core Idea
A one-page toolkit on polynomials that the operator theory in Ch5 will run on: every polynomial over C splits into linear factors (FTA), every polynomial over R splits into linear plus irreducible quadratic factors. The degree bounds the number of zeros, and the division algorithm lets you peel off factors one at a time — exactly the moves later used on p(T).

## Frameworks Introduced
- **𝒫(F)**: polynomials with coefficients in F; degree m has at most m zeros (4.8).
- **Zero ↔ factor (4.6)**: λ is a zero of p ⟺ p = (z − λ)q.
- **Division algorithm (4.9)**: p = q·(z − λ) + p(λ) — remainder is the evaluation.
- **FTA v1 (4.12)**: every nonconstant p ∈ 𝒫(C) has a zero. **FTA v2 (4.13)**: p ∈ 𝒫(C), deg m ⟺ p factors into m linear factors (counting multiplicity).
- **Real factorization (4.14–4.16)**: nonreal zeros of real-coefficient polynomials come in conjugate pairs; every p ∈ 𝒫(R) factors into linear and quadratic (irreducible, complex-conjugate pair) factors.

## Key Concepts
- Multiplicity of a zero: how many times (z − λ) divides p.
- Real quadratic factors have no real zeros — they are the atoms over R (later: the atoms of real operators' minimal polynomials, driving 2-dimensional invariant subspaces).
- FTA is used as a black box; Axler's proof-free reliance on it keeps the book elementary.

## Mental Models
- "Evaluate = remainder": p(λ) is what's left after dividing by (z − λ); zero ⟺ exact division.
- "C is algebraically closed, R is only half-closed": over R you must keep quadratic atoms; every real operator story has a "pair of complex conjugate eigenvalues" shadow.
- "Factor first, then act": later, p(T) = ∏(T − λj I)^{mj} — the factor structure of p controls the kernel structure of p(T).

## Anti-patterns
- **Assuming real polynomials split over R**: x² + 1 is irreducible over R — real theory must carry quadratic factors.
- **Counting distinct zeros instead of multiplicity**: degree m bounds distinct zeros by m, but factorization counts multiplicity.

## Reference Tables
### Factorization atlas
| Field | Atoms | Zeros |
|---|---|---|
| C | linear (z − λ) | m zeros with multiplicity |
| R | linear + irreducible quadratics | nonreal zeros in conjugate pairs |

## Key Takeaways
Over C: polynomial = list of roots with multiplicity.
Over R: polynomial = real roots + conjugate pairs.
Division algorithm turns "is λ a root?" into "is the remainder p(λ) zero?" — the computational hinge.

## Connects To
Ch5A applies polynomials to operators (p(T)); the minimal polynomial's factorization (5B) is exactly this chapter's atlas with λj = eigenvalues; over R, quadratic factors ↔ invariant 2-planes when no real eigenvalue exists (5B's odd-dimensional real space result). Ch9C's characteristic polynomial and Ch8's Jordan form consume the multiplicity language.
