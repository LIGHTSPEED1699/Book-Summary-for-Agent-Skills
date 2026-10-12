---
name: linear-algebra-done-right
description: Apply Sheldon Axler's Linear Algebra Done Right (4th ed. 2024, open access) frameworks - vector spaces, dimension bookkeeping, the minimal polynomial, spectral theorem, SVD, generalized eigenvectors and Jordan form, determinant-free structure theory - when analyzing linear maps, diagonalizing operators, decomposing inner-product spaces, or reasoning about eigenvalues and matrix factorizations.
---

# Linear Algebra Done Right (Sheldon Axler, 4th ed. 2024)
**Edition**: 4th (2024, Springer Undergraduate Texts in Mathematics, open access CC BY-NC).
9 chapters; determinants deliberately postponed to Ch9 — structure theory runs on the minimal polynomial instead.

The book's thesis: linear algebra is the study of linear maps, and better theorems emerge when you refuse to compute with determinants until the structure is understood. The spine is one equation (dim null T + dim range T = dim V) and one object (the minimal polynomial), upgraded by an inner product into the spectral theorem and the SVD.

Use this skill whenever the task is diagonalizing an operator, deciding what a matrix "really is" up to change of basis, decomposing a space into invariant/orthogonal pieces, or choosing between eigenvalue and singular-value reasoning.

## How to use
- Start with the chapter file for the topic (chapters/), then the cheatsheet for the decision procedures.
- patterns.md holds the reusable argument shapes (extend-shrink, annihilate-then-decompose, adjoint-transport).
- glossary.md maps Axler's notation (𝒫(F), ℒ(V,W), G(λ,T), V′, V⊗W) to standard terms.

## Chapter map
1. **Vector spaces** (ch01): axioms, subspaces, sums and direct sums.
2. **Finite-dimensional spaces** (ch02): span, linear dependence lemma, bases, dimension, dim(U+W).
3. **Linear maps** (ch03): null/range, fundamental theorem, matrices, rank, invertibility, isomorphism, quotients, duality.
4. **Polynomials** (ch04): zeros, division algorithm, FTA, real vs complex factorization.
5. **Eigenvalues** (ch05): invariant subspaces, minimal polynomial, triangularization, diagonalizability, Gershgorin, commuting families.
6. **Inner product spaces** (ch06): Cauchy-Schwarz, Gram-Schmidt, Riesz, orthogonal complements, projections, minimization.
7. **Operators on inner product spaces** (ch07): adjoint, self-adjoint/normal, spectral theorem, positive/unitary, QR/Cholesky, SVD, operator norm, low-rank approximation, polar decomposition.
8. **Operators on complex spaces** (ch08): generalized eigenvectors, characteristic polynomial, Jordan form, square roots, trace.
9. **Multilinear algebra and determinants** (ch09): bilinear/quadratic forms, alternating forms, determinants, Cayley-Hamilton, tensor products.

## The one-page spine
- dim null T + dim range T = dim V powers injectivity/surjectivity tests and solvability of linear systems.
- Minimal polynomial: roots = eigenvalues; distinct linear factors ⟺ diagonalizable; largest Jordan block exponent.
- Over C every operator is triangularizable; over R only odd dimensions guarantee an eigenvalue.
- Inner product: orthonormal bases always exist; Riesz makes every functional an inner product; V = U ⊕ U⊥.
- Spectral theorem: normal (real: self-adjoint) ⟺ orthonormal eigenbasis.
- SVD: every map, two bases, one diagonal of singular values; answers norm/rank/approximation/volume.
- Jordan form: the non-normal remainder; λI + nilpotent on each generalized eigenspace.
- Determinants arrive last: unique alternating normalization; det = ∏ eigenvalues; Cayley-Hamilton.
