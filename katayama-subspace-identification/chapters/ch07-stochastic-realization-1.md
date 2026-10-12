# Chapter 7: Stochastic Realization Theory (1)

## Core Idea
Given only the covariance sequence (or spectral density) of a stationary process, build all minimal Markov models that simulate it — Faurre's stochastic realization problem. The covariance Hankel matrix factorizes as observability × reachability exactly like the deterministic case, so deterministic realization supplies the skeleton; the remaining freedom is the state covariance Σ, which must satisfy a linear matrix inequality (LMI). Positive realness of the spectral density is equivalent to existence of a Markov model; the LMI's boundary solutions are computed by matrix Riccati equations, giving the minimal and maximal models. This is the theory that makes subspace identification of stochastic systems principled.

## Frameworks Introduced
- **Stochastic realization problem (Faurre, 7.2)**: find all stationary Markov models x⁺ = Ax + w, y = Cx + v (w, v white, covariances Q, R, S) whose output covariances match prescribed R_y(k).
- **Covariance Hankel factorization (7.1)**: ℋ = 𝒪̄ R̄ with infinite observability/reachability matrices of (A, [w;v]-driven model) — identical structure to deterministic realization; rank ℋ = n.
- **Positive realness (Def 7.1)**: spectral density Φ(z) is (strictly) positive real ⟺ Φ(e^{jω}) ≥ 0 (> 0) on the circle plus analyticity outside; coercive = uniformly positive. Positive realness ⟺ existence of a Markov model (Faurre's equivalence).
- **Spectral density additive decomposition (7.10)**: Φ = C(zI−A)⁻¹ Σ Cᵀ + symmetric remainder — state contribution plus direct noise.
- **The LMI for Σ (7.3)**: a state covariance Σ > 0 admits a Markov model iff [Σ − AΣAᵀ, −AS; −SᵀAᵀ, R] ≥ 0 (structure: process-noise covariance must complete a PSD block); every Σ satisfying the LMI yields a valid model — all solutions come from the LMI.
- **Boundary solutions via Riccati (7.4-7.5)**: the LMI's extreme points solve discrete algebraic Riccati equations (Faurre's approach); minimal/maximal Σ bound the whole family.
- **Strict positive realness and finite-data algorithm (7.6-7.7)**: with coercive spectrum, a practical algorithm realizes from a finite covariance window (the theoretical basis for the sample-covariance algorithms in ch9-10).

## Key Concepts
- Forward Markov model: state = "present summary of the past"; its covariance Σ links the Hankel factorization to noise covariances.
- The realization set is a convex family parameterized by Σ in an LMI — not a single model (unlike deterministic minimal realization, unique up to similarity).
- Boundary models: Riccati solutions = minimum-variance innovations model and its dual; interior points = mixtures with extra feedback of the output into the state noise (the "non-unique" stochastic realizations).
- Positive realness is the exact solvability certificate: no PR, no Markov model.
- Covariance data plays the role impulse-response data played in ch3/ch6 — same Hankel rank theory, new semantics.

## Mental Models
- "Covariances are the new impulse responses": run the deterministic realization machine on the covariance Hankel.
- "A convex family, bounded by Riccati": when data is stochastic, the answer isn't one model but an LMI-feasible set; the extremes are Riccati fixed points.
- "PR = existence": before writing any algorithm, check the spectrum is positive real — that's the theorem saying a model can exist.
- "State covariance is the gauge": different Σ = different internal noise split with identical output statistics.

## Anti-patterns
- **Assuming uniqueness** — stochastic realizations are a family; algorithms silently pick a boundary point (usually the innovations model); know which one you got.
- **Realizing non-PR spectra** — no Markov model exists; sample spectra from short data often violate PR — regularize (coercive check, 7.6).
- **Using finite covariance windows without the strict PR condition** — the finite-data algorithm needs coercivity to be well-posed.
- **Ignoring the S (cross-covariance) term** — models with S ≠ 0 vs the innovations model S = 0 behave differently under feedback; the LMI tracks this.

## Reference Tables
### Deterministic vs stochastic realization
| Aspect | Deterministic (ch3/6) | Stochastic (ch7-8) |
|---|---|---|
| Data object | impulse response / Markov params | covariance sequence / spectrum |
| Hankel factorization | 𝒪 R̄ (unique up to similarity) | 𝒪̄ R̄ (family via Σ) |
| Solvability | finite rank | positive realness |
| Freedom | similarity transform | LMI-feasible Σ |
| Extremes | balanced realization | Riccati boundary models |

### LMI → model map
| LMI object | Meaning |
|---|---|
| Σ feasible | state covariance of some Markov model |
| boundary Σ | Riccati solution (innovations / dual) |
| Φ coercive | strictly PR; finite-data algorithm valid |

## Key Takeaways
Stochastic realization = deterministic realization applied to the covariance Hankel, plus an LMI for the state covariance that parameterizes all solutions.
Positive realness of the spectrum is necessary and sufficient for a Markov model to exist (Faurre).
The LMI's boundary solutions come from Riccati equations — the innovations model is one extreme.
Finite covariance data suffices when the spectrum is coercive — the license for the sample-based algorithms in ch9-10.

## Connects To
ch4's Hilbert-space prediction and backward models supply the past/future geometry; ch5's stationary Kalman filter is the Riccati boundary model in disguise; ch8 adds balancing and reduced models; ch9 ORT and ch10 CCA implement stochastic realization from input-output data (with exogenous inputs); Doraiswami ch3-4 (estimation theory) is the statistical companion.
