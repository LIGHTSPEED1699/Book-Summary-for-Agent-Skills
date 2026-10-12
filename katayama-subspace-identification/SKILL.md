---
name: katayama-subspace-identification
description: Apply Katayama's Subspace Methods for System Identification (Springer 2005) frameworks - the state-lives-in-the-data-matrix principle, Hankel rank = system order, LQ/QR+SVD+least-squares pipelines (MOESP/ORT/CCA), stochastic realization via positive-realness and Riccati/LMI families, balanced canonical coordinates from CCA of past/future, and closed-loop joint input-output identification - when identifying state-space models from input-output data or reasoning about realization theory.
---

# Subspace Methods for System Identification (Katayama, 2005)

Use when identifying LTI state-space models from data, choosing model order, or understanding what MOESP/ORT/CCA/N4SID actually do. Katayama's unique contribution: a single self-contained route from numerical linear algebra → realization theory → stochastic realization → subspace algorithms, with consistency guarantees and no optimization.

## Chapter map
- [ch01 Introduction](chapters/ch01-introduction.md) — identification triple, PEM's MIMO wall, the four subspace pillars
- [ch02 Linear Algebra](chapters/ch02-linear-algebra.md) — QR, SVD, projections (idempotent = projector), Hankel rank lemma
- [ch03 Discrete-Time Systems](chapters/ch03-discrete-time-systems.md) — Z-transform, reachability/observability, balanced realization, Ho-Kalman
- [ch04 Stochastic Processes](chapters/ch04-stochastic-processes.md) — Hilbert-space prediction, innovations, spectral factorization, backward Markov models
- [ch05 Kalman Filter](chapters/ch05-kalman-filter.md) — projection-made-recursive, ARE/stationary filters, forward/backward duality
- [ch06 Deterministic Realization](chapters/ch06-deterministic-realization.md) — data matrices, fundamental rank lemma, superposition, LQ, MOESP
- [ch07 Stochastic Realization (1)](chapters/ch07-stochastic-realization-1.md) — Faurre: positive realness, LMI for state covariance, Riccati boundary models
- [ch08 Stochastic Realization (2)](chapters/ch08-stochastic-realization-2.md) — Akaike: CCA of past/future, canonical variates = states, balanced stochastic realization
- [ch09 ORT Method](chapters/ch09-subspace-ort.md) — full open-loop pipeline: split deterministic/stochastic, realize, stitch
- [ch10 CCA Method](chapters/ch10-subspace-cca.md) — CCA route; Algorithm B "state first, then regress" (N4SID template)
- [ch11 Closed-loop](chapters/ch11-closed-loop.md) — joint input-output approach when feedback breaks A3
- [Appendices A-D](chapters/appendices.md) — PE definition, algorithm pseudocode tables

## Top-level references
- [glossary.md](glossary.md) — data matrices, projections, PE, PR, canonical variates
- [patterns.md](patterns.md) — recurring moves (rank-is-order, project-then-realize, split-stitch)
- [cheatsheet.md](cheatsheet.md) — algorithm pipelines and assumption checklists

## Core theses (apply as defaults)
1. The state sequence lives inside the data matrix: W_p = 𝒪X_p + 𝒯U_p; subspace methods read it off with orthogonal transforms.
2. Rank is order: Hankel/data-matrix rank (or the singular-value gap under noise) = McMillan degree — no search, no canonical form, no optimization.
3. Every estimator is an orthogonal projection (ch2 matrices, ch4 Hilbert spaces, ch5 recursion); innovations make the past an orthogonal basis.
4. Stochastic realization = deterministic realization on the covariance Hankel + an LMI for the state covariance; positive realness is the existence certificate; Riccati gives the boundary models.
5. CCA of past/future is the master geometry: canonical variates are balanced states, canonical correlations are Hankel singular values.
6. Open-loop assumptions (state excitation, PE input, no feedback) are load-bearing; closed-loop data demand the joint input-output approach.

## When to load which chapter
Tooling refresh: ch2. Systems/realization foundations: ch3, ch6. Probability/prediction foundations: ch4, ch5. Stochastic realization theory: ch7-8. Running algorithms: ch9 (ORT/MOESP flavor), ch10 (CCA/N4SID flavor), ch11 (closed loop), appendices D for pseudocode.
