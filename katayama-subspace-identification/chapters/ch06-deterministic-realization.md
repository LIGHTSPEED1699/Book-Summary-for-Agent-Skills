# Chapter 6: Realization of Deterministic Systems

## Core Idea
Realization from data, not from impulse responses: stack input-output samples into past/future block-Hankel data matrices, and the matrix input-output equation W_p = 𝒪_i X_p + T_s U_p says the *state sequence itself* lives inside the data. The fundamental rank lemma (Lemma 6.3) says i block-rows of the output Hankel, after removing rows dependent on the input Hankel, contain exactly n independent rows — the state dimension, read off the data. Superposition (Lemma 6.4) lets column operations (executed as an LQ decomposition) manufacture zero-input responses from arbitrary data, exposing the extended observability matrix. This is the deterministic backbone of MOESP.

## Frameworks Introduced
- **Matrix input-output equations (6.3)**: Y_{[i,s]} = 𝒪_i X_s + 𝒯_{i,s} U_{[i,s]} for past and future blocks; state matrices X_p, X_f collect consecutive states; 𝒪_i = extended observability matrix; 𝒯 = block Toeplitz of Markov parameters.
- **Past/future partition**: U_p/Y_p (past) and U_f/Y_f (future) Hankel blocks — the geometry every subspace method works on.
- **Assumption 6.1 (the open-loop standing assumptions)**: A1) state sufficiently excited (rank X_p = n); A2) input persistently exciting of order i (rank U_p block = i·m); A3) no linear feedback from states to inputs (open-loop data).
- **Fundamental rank lemma (Lemma 6.3)**: rank of [Y_p; U_p] after deleting rows dependent on U_p equals n + i·m — the state dimension is identifiable from data ranks.
- **Superposition lemma (Lemma 6.4)**: any length-i input-output pair is a linear combination of the data matrix columns (given PE input) — data is universal; fictitious inputs/zero-input responses can be synthesized by column operations.
- **LQ decomposition (6.4)**: QR's dual for wide matrices; partitioned LQ of the stacked data produces exactly the column operations that zero the upper-right block, isolating the zero-input response block whose column space = im(𝒪_i).
- **MOESP method (6.5)**: oblique projection of the future output data along the past input block; SVD of the projected matrix splits im(𝒪_i) from the Toeplitz input part; least squares recovers (A, B, C, D).
- **SVD and additive noises (6.7)**: with noise, singular values split into signal/noise clusters; order selection = the gap; projection suppresses noise influence.

## Key Concepts
- The state sequence X_p is a subspace of the data — "the state is in the data matrix" is the book's central slogan.
- Extended observability matrix 𝒪_i: its column space determines the state coordinates up to similarity; range(𝒪_i) = what the future outputs can reveal.
- PE condition: input must excite enough dynamics (order ≥ i); Appendix B formalizes.
- Open-loop assumption A3 is what breaks in closed-loop data — the reason ch11 exists.
- LQ/QR are the computational engine: no optimization, just orthogonal transforms + SVD + least squares.
- Fictitious inputs: column operations synthesize zero-input responses from arbitrary operating data (superposition).

## Mental Models
- "Rank is order, again, but on data": Lemma 2.14's Hankel rank now read from measured Hankel blocks (Lemma 6.3).
- "Project the input out, keep the state in": MOESP's oblique projection annihilates the Toeplitz input term while preserving im(𝒪_i).
- "Data matrices are universal": with PE input, one long record contains every input-output pair the system can produce.
- "Triangularize to separate": LQ's zero block is the algebraic expression of "deterministic input effect removed".

## Anti-patterns
- **Running MOESP on closed-loop data** — violates A3 (feedback makes U_p and X_p dependent); use ch11's two-stage/closed-loop schemes.
- **Choosing i too small** — need i ≥ n and PE of order i; too small i hides the state rank.
- **Picking order by singular-value count without a noise gap** — with noise the rank is full; the gap between clusters is the criterion.
- **Forgetting A1 (state excitation)** — a reachable system still needs an exciting initial state/input combination; rank X_p < n collapses the state space.

## Reference Tables
### Data-matrix anatomy
| Symbol | Object | Meaning |
|---|---|---|
| U_p, Y_p | past Hankel blocks | known history |
| U_f, Y_f | future Hankel blocks | to be explained |
| 𝒪_i | extended observability | state→output map (i steps) |
| 𝒯_{i,s} | block Toeplitz | input→output (Markov params) |
| X_p, X_f | state sequences | the hidden common factor |

### MOESP pipeline
| Step | Operation | Gets |
|---|---|---|
| 1 | stack past/future data | W_p, W_f |
| 2 | oblique projection W_f/U_p along W_p | state-related subspace |
| 3 | SVD + order gap | 𝒪̂_i, n |
| 4 | least squares on state seq | A, B, C, D |

## Key Takeaways
The state sequence lives in the data matrix; rank lemmas turn "how big is the system?" into a rank count on measured Hankel blocks.
LQ decomposition performs the superposition trick numerically: zero-input responses (hence 𝒪_i) fall out of orthogonal transforms.
MOESP = oblique projection + SVD + least squares — the template all later algorithms refine.
Open-loop PE assumptions (A1-A3) are load-bearing; every failure mode of subspace ID is a violation of one of them.

## Connects To
ch2's projections/SVD do all the work; ch3's observability matrices and realization theory set the stage; ch9 ORT replaces the input projection with a state-space-free route, ch10 CCA re-derives via canonical variates; ch11 handles the closed-loop case where A3 fails; Doraiswami ch7 §7.8 presents the subspace method as one of four practical identification tools.
