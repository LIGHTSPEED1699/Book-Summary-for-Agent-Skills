# Chapter 8: Stochastic Realization Theory (2)

## Core Idea
Akaike's route to stochastic realization: the mutual information between a stationary process's past and future is captured by canonical correlation analysis (CCA) between the two Hilbert spaces. The canonical variates are optimally predictive summaries of past and future; their correlations are the process's Hankel singular values; the canonical state (either variate, matched) is the balanced state. Balanced stochastic realization, model reduction, and two finite-data subspace algorithms (A and B) all fall out of this one picture — this is the theoretical ancestor of CVA/N4SID.

## Frameworks Introduced
- **CCA (8.1)**: maximize correlation between linear combinations of two random vectors under unit-variance constraints; solved as a generalized eigenvalue problem; canonical correlations ρᵢ ∈ [0,1] = singular values of the whitened cross-covariance Â = Σ_xx^{-1/2}Σ_xy Σ_yy^{-1/2}; canonical variates = the maximizing coordinates.
- **Past/future spaces and predictor spaces (8.2-8.3)**: H⁻ (past), H⁺ (future); orthogonal projections of future onto past and past onto future; the two predictor spaces intersect in the minimal state.
- **Forward and backward innovation representations (8.5.2)**: the process driven by forward innovations (from past) and backward innovations (from future); the two Markov models of ch4/ch7 glued together through the state.
- **Forward/backward state vectors (8.5.1)**: x_f = predictive summary of past, x_b = of future; E[x_f x_fᵀ] and E[x_b x_bᵀ] are the stochastic Gramians; their product's eigenvalues = squared canonical correlations.
- **Stochastic balanced realization (8.5)**: coordinates where the two predictor Gramians are equal and diagonal = diag(σᵢ); σᵢ = canonical correlations between past and future — the process's own Hankel singular values.
- **Reduced stochastic realization (8.6)**: truncate small σᵢ; the reduced model still simulates the covariance data to within the discarded canonical correlations.
- **Stochastic realization Algorithms A and B (8.7)**: from finite covariance/output data — Algorithm A: SVD of the sample covariance Hankel (deterministic-style); Algorithm B: CCA of sample past/future blocks (the subspace-identification route); numerical results included.

## Key Concepts
- CCA as the geometry of prediction: canonical variates are the coordinates in which past predicts future with maximal, decoupled correlations.
- The state of a stationary process = the overlap between past and future; its dimension = rank of the past-future correlation (Hankel rank again).
- Canonical correlations = Hankel singular values of the stochastic process = the quantities subspace algorithms read off SVDs of projected data.
- Balanced = past-predictive and future-predictive states coincide; reduction by σ-gap is statistically meaningful.
- Algorithms A/B work on finite covariance windows — the bridge from ch7's existence theory to data.

## Mental Models
- "State = correlation between past and future": not a substance, a sufficient statistic; CCA finds its coordinates.
- "CCA = whitened cross-covariance SVD": one line of algebra behind all the prediction theory.
- "Two predictors, one state": projecting future→past and past→future gives two views; where they agree is the state space.
- "Canonical correlations are mode energies of memory": σᵢ near 1 = perfectly predictable mode; near 0 = noise-like; truncate accordingly.

## Anti-patterns
- **CCA without whitening checks** — Σ_xx, Σ_yy must be positive definite; sample estimates from short records can be singular.
- **Reading order from raw SVD of data instead of projected/canonical quantities** — input effects and noise inflate singular values; use the algorithmic projections (ch9-10).
- **Confusing orthogonal projections (this chapter's predictor spaces) with the oblique projections of ORT** — both compute state estimates; the geometry differs (ch9 explains the equivalence).
- **Reducing below the noise floor and expecting covariance fidelity** — discarded σᵢ bound the covariance misfit.

## Reference Tables
### CCA machinery
| Object | Formula | Meaning |
|---|---|---|
| Â | Σ_xx^{-1/2} Σ_xy Σ_yy^{-1/2} | whitened cross-covariance |
| ρᵢ | singular values of Â | canonical correlations |
| αᵢ, βᵢ | left/right singular vectors (unwhitened) | canonical variates |

### Algorithms A vs B (8.7)
| | A | B |
|---|---|---|
| Input | covariance Hankel window | sample past/future blocks |
| Core | SVD (Ho-Kalman style) | CCA / oblique projection |
| Ancestor of | covariance realization | CVA / N4SID |

## Key Takeaways
CCA between past and future is the master theory: canonical variates are states, canonical correlations are Hankel singular values, balancing and reduction are immediate.
The stochastic state is the overlap of past and future predictor spaces — dimension = Hankel rank, coordinates = CCA's choice.
Algorithms A and B turn the theory into finite-data procedures; B is the direct ancestor of the CCA-based subspace method in ch10.

## Connects To
Builds on ch4 (Hilbert spaces, innovations, backward models) and ch7 (Markov models, LMI family); ch9's ORT computes the same state via oblique projection instead of CCA — the two are shown equivalent; ch10 implements CCA on data matrices with exogenous inputs; Doraiswami ch7 §7.8 uses the resulting method practically.
