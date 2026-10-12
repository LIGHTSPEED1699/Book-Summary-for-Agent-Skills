# Chapter 10: Subspace Identification (2) - CCA Method

## Core Idea
The second route to the same model: canonical correlation analysis between the past and future of the data, with the exogenous input projected out. The oblique projection of the future output along the past input (along the past output's complementary direction) is exactly the state estimate whose singular structure CCA reveals; the canonical variates are the balanced state coordinates. Two practical algorithms close the chapter: a realization-based one (SVD of the projected block, like ORT) and a regression one (estimate the state sequence first, then regress everything onto it — the N4SID/CVA flavor).

## Frameworks Introduced
- **Predictor spaces with exogenous inputs (10.2-10.3)**: past/future spaces conditioned on the input; the input is projected out of both, leaving the stochastic predictor geometry of ch8 with inputs handled by projection.
- **Oblique projection as state estimate (10.3)**: W_p^⊥ = Y_f projected along U_p (annihilating the deterministic term while keeping the state term) — the state sequence estimate, in the same row-space identities as ch9 but derived from CCA's inner product.
- **Innovation representation with inputs (10.4)**: the joint model's innovations form; Kalman gain from the canonical state's covariances.
- **Finite-data stochastic realization (10.5)**: sample past/future blocks replace the Hilbert-space objects; consistency as N → ∞.
- **CCA method (10.6)**: whiten the (input-projected) past and future blocks, SVD of the whitened cross-covariance = canonical correlations/variates; state dimension from the singular gap; balanced realization directly from the variates.
- **Algorithm A: realization-based** — SVD of the projected block → 𝒪̂ → (A,C) by shift invariance → (B,D) by LS (mirrors ORT's route, CCA-justified).
- **Algorithm B: regression using the state vector** — compute the canonical state estimate X̂_f explicitly, then solve the joint least-squares problem [X̂_f⁺; Y_f] = [A B; C D][X̂_f; U_f] + noise — one big regression gives all four matrices plus K (the N4SID-style "state then regress" recipe).
- **Numerical examples (10.7)**: demonstrate order selection via the singular-value gap and compare with ORT.

## Key Concepts
- Oblique projection = CCA's first step: projecting future onto past *along the input* keeps the state and kills the deterministic response.
- Canonical correlations between projected past/future = Hankel singular values of the stochastic subsystem with inputs.
- Balanced canonical coordinates: both predictor Gramians diagonal and equal — reduction and weighting become trivial.
- Algorithm A vs B: same state subspace, different extraction — factor-based (observability SVD) vs state-sequence regression; B is numerically simpler and the N4SID ancestor.
- The two chapters' methods (ORT ch9, CCA ch10) are asymptotically equivalent; they differ in which projection identities they exploit.

## Mental Models
- "CCA is the inner product speaking": ORT manipulates row spaces; CCA manipulates correlations — same projection, different bookkeeping.
- "Estimate the state, then everything is linear": once X̂ exists, (A,B,C,D,K) is one least-squares solve — Algorithm B's whole trick.
- "Project the input out before correlating": canonical correlations computed without input projection mix deterministic and stochastic memory.
- "Balanced coordinates are free with CCA": the variates *are* the balanced basis; no extra Gramian solve.

## Anti-patterns
- **Canonical correlations on raw past/future** — input effects leak in; project first (the chapter's whole setup).
- **Using Algorithm B's state estimate without its whitening** — the regression's conditioning depends on the canonical scaling; skip it and the LS is badly weighted.
- **Expecting CCA and ORT to agree sample-by-sample** — they differ at finite N (different projection identities); asymptotically identical.
- **Order selection by count of "large" singular values without a documented gap** — the gap is the criterion; noise floors blur it.

## Reference Tables
### CCA method pipeline
| Step | Operation | Gets |
|---|---|---|
| 1 | LQ/QR: project U out of past & future | input-free blocks |
| 2 | whiten both blocks | Σ ≈ I coordinates |
| 3 | SVD of cross-covariance | ρᵢ, canonical variates |
| 4 | gap → n; state estimate X̂ | balanced state |
| 5A | SVD-factor realization | A,C,B,D (Algorithm A) |
| 5B | joint LS on [X̂; U] | A,B,C,D,K (Algorithm B) |

### ORT vs CCA (ch9 vs ch10)
| | ORT | CCA |
|---|---|---|
| Geometry | row-space projections | correlations of projected blocks |
| State access | observability factor | canonical variates |
| Assembly | staged LS | one joint regression (B) |
| Ancestor | MOESP family | CVA/N4SID family |

## Key Takeaways
CCA between input-projected past and future yields the state, its balanced coordinates, and the order — all from one SVD.
Algorithm B ("state first, then regress") is the simplest complete subspace algorithm and the N4SID template.
ORT and CCA are two projections of the same theorem; choose by taste, not by accuracy, at large N.

## Connects To
Implements ch8's CCA theory on data with ch6's data matrices and ch9's input handling; ch11 extends both methods to closed-loop data; Doraiswami ch7 §7.8 and ch8 use the resulting algorithms in practice.
