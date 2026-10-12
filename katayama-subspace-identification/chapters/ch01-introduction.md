# Chapter 1: Introduction

## Core Idea
System identification chooses the best model from a model set given input-output data — the triple (data set, model set, criterion). Classical prediction-error methods (PEM) work well for SISO but hit a wall for MIMO state-space models: nonlinear optimization, identifiability/canonical-form headaches, and ill-conditioning. Subspace methods sidestep all of it: they build state-space models directly from data via linear algebra (QR, SVD, projections) — no nonlinear optimization, no canonical parametrization, no initial guess — and their theoretical backbone is stochastic realization theory.

## Frameworks Introduced
- **The identification triple (1.1)**: data set Z, model set M, criterion V — every identification problem is specified by these three; experiment design (test signals, sampling) is part of the data element.
- **Model taxonomy**: parametric (transfer functions, state-space, time-series) vs non-parametric (impulse/frequency responses, spectral densities); black-box vs gray-box (physics-embedded structure, unknown parameters); model-order selection via Akaike's AIC.
- **Classical methods (1.2)**: ARX/ARMAX/Box-Jenkins time-series models; ARMA noise models.
- **PEM for state-space models (1.3)**: prediction-error criterion over parametrized state-space families; why it's painful for MIMO (nonlinear optimization, identifiability, near-insensitive parameters → ill-conditioning).
- **Why subspace methods (1.4)**: four pillars — QR decomposition, SVD, canonical correlation analysis (CCA), stochastic realization theory; direct, numerically stable, optimization-free construction of state-space models from input-output data.
- **Historical arc (1.5)**: Åström-Bohlin (ML → ARMAX, 1965) and Ho-Kalman (realization, 1966) as the twin origins; Ljung/Söderström-Stoica culminated PEM; Faurre/Akaike started stochastic realization; mid-1980s QR/SVD wave in signal processing → subspace ID (Van Overschee-De Moor book as the first synthesis).
- **Book roadmap (1.6)**: Part I preliminaries (linear algebra, systems, stochastic processes, Kalman filter), Part II realization theory (deterministic + stochastic), Part III subspace methods (ORT, CCA, closed-loop).

## Key Concepts
- Identification = model selection under data; the criterion V[θ] makes it an optimization only after parametrization — subspace methods avoid parametrization entirely.
- PEM's MIMO failure modes: canonical-form constraints, nonlinear search, poor identifiability.
- Subspace methods' defining move: estimate the state sequence (or its oblique projection) directly from Hankel data matrices, then realize by least squares.
- Stochastic realization theory is the missing theory that explains subspace algorithms (Katayama's own research program).
- AIC and information criteria for order selection; PE (persistently exciting) inputs for identifiability.

## Mental Models
- "Three questions define the problem": what data, what model class, what yardstick — everything else is algorithm.
- "Optimization is optional": for LTI state-space models, linear algebra (QR/SVD/projections) reaches the model directly; optimization is the fragile detour.
- "Realization theory is the bridge": data → Hankel/covariance matrices → realization theorems → algorithms with guarantees.
- "Black-box with physics guardrails": gray-box when principles are known; AIC when order is not.

## Anti-patterns
- **Applying PEM to MIMO without identifiability analysis** — near-insensitive parameters produce ill-conditioned criteria (the historical motivation for subspace methods).
- **Collecting data without experiment design** — data must be informative (PE inputs); passive operating data can be rank-deficient.
- **Fixing model order by taste** — use AIC-type criteria.
- **Treating subspace methods as black magic** — they are realization theory applied to data matrices; the theory (Parts I-II) is what makes them trustworthy.

## Reference Tables
### Method families
| Family | Machinery | MIMO state-space? |
|---|---|---|
| PEM/ML | nonlinear optimization over θ | fragile |
| IV | instrumental variables | linear but parametrized |
| Subspace (ORT/CCA/MOESP/N4SID) | QR, SVD, projections, CCA | direct, optimization-free |

### The four subspace pillars
| Tool | Role |
|---|---|
| QR decomposition | orthogonal projections, rank revealing |
| SVD | balanced realization, order selection |
| CCA | oblique projections / canonical variates |
| Stochastic realization | theory of models from covariances |

## Key Takeaways
Identification is the (data, model set, criterion) triple; experiment design is part of it.
PEM's nonlinear optimization is the weak link for MIMO state-space models.
Subspace methods = realization theory + QR/SVD/projections: direct, stable, optimization-free.
Stochastic realization theory (Faurre, Akaike) is the theoretical foundation Katayama builds through Parts I-II.

## Connects To
Ch2 supplies QR/SVD/projections used everywhere; ch3-5 build the systems/stochastic/Kalman machinery; ch6 deterministic realization (Hankel SVD, Ho-Kalman, MOESP flavor) and ch7-8 stochastic realization are the theory; ch9 (ORT) and ch10 (CCA) are the two subsspace algorithms this introduction promises; ch11 extends to closed-loop data. Doraiswami's ch7-8 cover the PEM/LS/closed-loop side from a practitioner's angle.
