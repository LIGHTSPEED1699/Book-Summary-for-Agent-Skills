# Appendices A-D

## Core Idea
The reference shelf: least-squares/linear-regression identities (A), the LQ decomposition conventions (B/A.2), the formal persistently-exciting (PE) definition every algorithm assumes (B), and pseudocode tables for every algorithm in the book (D) — Ho-Kalman, MOESP, stochastic realization A/B, and the full subspace identification methods (ORT/CCA, open and closed loop).

## Frameworks Introduced
- **A.1 Linear regressions**: normal equations, projection matrices, the LS estimator's covariance identities — the algebra cited in every realization step.
- **A.2 LQ decomposition**: conventions for the wide-matrix QR dual used throughout Part III.
- **Appendix B PE condition (Def B.1)**: input u is persistently exciting of order k iff the sample covariance of the k-stacked input has full rank (≥ min(k·m, needed)); the precise form of Assumptions 6.1/9.3 A2.
- **Appendix C**: auxiliary matrix-theory results (SVD/LMI support lemmas).
- **D.1 Deterministic realization algorithm**: Ho-Kalman from Markov parameters (rank factorization + SVD balancing).
- **D.2 MOESP algorithm**: the ch6.5 pipeline in pseudocode.
- **D.3 Stochastic realization algorithms**: finite-covariance-window realization (ch7.7/ch8.7 Algorithms A/B).
- **D.4 Subspace identification algorithms**: complete ORT and CCA recipes (ch9-10), including closed-loop variants (ch11) — the copy-paste-ready tables.

## Key Concepts
- PE is a rank condition on stacked input samples — checkable from data before running any algorithm.
- The D-tables fix the notation: LQ blocks, projection symbols, and step order match the chapter derivations exactly.
- Regression identities (A.1) justify the shift-invariance LS steps' unbiasedness claims.

## Mental Models
- "Assumptions are checklists": A/B turn the prose assumptions into rank tests.
- "The algorithms are tables, not folklore": every method in the book has a numbered-step twin in Appendix D.

## Anti-patterns
- **Running any Part III algorithm without the PE rank check** — silent rank deficiency is the most common failure.
- **Reimplementing from chapter prose instead of the D-tables** — the tables encode the exact projection conventions; prose drifts.

## Key Takeaways
PE (Appendix B) is the one assumption you can and must verify from data.
Appendix D is the implementation source of truth: Ho-Kalman, MOESP, stochastic realization, ORT/CCA open/closed loop.

## Connects To
B feeds Assumptions 6.1/9.3; D.1-D.4 implement ch6-11; A supports every least-squares step.
