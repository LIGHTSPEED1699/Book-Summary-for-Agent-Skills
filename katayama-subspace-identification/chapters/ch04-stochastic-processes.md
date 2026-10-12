# Chapter 4: Stochastic Processes

## Core Idea
A stochastic process is a vector of random variables indexed by time, and prediction is just orthogonal projection in a Hilbert space of random vectors: the best estimate of the future given the past is the projection, the error is orthogonal to everything known, and the innovation (one-step prediction error) is white. Every stationary process has a whitening filter and an innovations (ARMA) representation; every Gaussian process is fully described by mean and covariance; and any process can be run backwards in time with a backward Markov model. Subspace identification's "past/future" Hankel geometry is exactly this forward-backward decomposition applied to data.

## Frameworks Introduced
- **Process basics (4.1)**: Markov property (future independent of past given present); mean/covariance matrices; Gauss-Markov processes.
- **Stationarity & ergodicity (4.2-4.3)**: wide-sense stationarity (constant mean, covariance depends on lag only); ergodic theorems justify replacing ensemble averages with time averages — the license for doing identification from one long record.
- **Spectral analysis (4.4)**: autocovariance ↔ power spectrum (Fourier pair); cross-spectrum and coherence; spectral factorization Φ(z) = Ψ(z)Ψ(z⁻ᵀ) with Ψ minimum phase (Wold decomposition).
- **Hilbert space prediction (4.5)**: random vectors as points in a Hilbert space with inner product E[xᵀy]; estimate = orthogonal projection; orthogonality principle E[(y − ŷ)ᵀx] = 0; optimal linear predictor = causal part of z⁻¹Φ (delete anti-causal/polynomial part); minimum prediction variance via contour integral; innovations representation y = Ψ(z)e with e white.
- **Stochastic linear systems (4.6)**: x(t+1) = A(t)x(t) + B(t)w(t), y(t) = C(t)x(t) + D(t)v(t) with Gaussian white noises — a "Markov model" of the process; state covariance recursion Σ(t+1) = Φ(t,t)Σ(t)Φᵀ + noise terms; observation covariance R(t,t+κ) = C Φ Σ … (covariance Markov parameters).
- **Stochastic LTI systems (4.7)**: stationary ARMA processes; spectral density from (A,B,C) covariance; innovations representation of the spectrum.
- **Backward Markov models (4.8)**: the same process represented running backward in time: x̄(t) = state built from the past; backward innovations white; forward/backward state covariances Σ and Σ̄ — the two Gramians that subspace methods estimate from data.

## Key Concepts
- Orthogonal projection in the Hilbert space of second-order random vectors = optimal linear estimation; the error is orthogonal to the data subspace.
- Innovation process: one-step prediction error; always white; the fundamental noise driving the innovations representation.
- Spectral factorization is unique up to signature when minimum phase — this is why whitening filters exist.
- Covariance sequence of a stochastic LTI system obeys the same linear recursion as Markov parameters (Lemma 2.14 again): rank of the covariance Hankel = state dimension.
- Ergodicity is what lets sample covariances from one record estimate the true ones (with N → ∞).
- Backward model: prediction of the past from the future is equally well-defined; forward and backward states span the same state space.

## Mental Models
- "Estimation = projection": every estimator in the book (Wiener, Kalman, subspace) is the same picture — project the target onto the span of what you know.
- "Innovations are the new coordinates": replace the raw past by its innovations (orthogonal basis of the past subspace) and all projections become trivial sums.
- "Run the tape backwards": a stationary process has a backward Markov model with white backward innovations; past and future Hankel blocks are two views of one state.
- "Covariances are Markov parameters": stochastic realization treats covariance sequences exactly like impulse responses.

## Anti-patterns
- **Assuming ergodicity without checking** — identification from a single record presumes it; short or non-stationary records break the sample-covariance foundation.
- **Non-minimum-phase whitening filters** — inverse unstable; always take the causal, minimum-phase spectral factor.
- **Treating correlated noise as white** — the innovations representation is the fix; raw colored noise invalidates LS unbiasedness (see Doraiswami ch7).
- **Forgetting the orthogonality principle when auditing estimators** — if the error isn't orthogonal to the data, the estimator is wrong.

## Reference Tables
### Prediction toolkit
| Object | Definition | Role |
|---|---|---|
| Past subspace H_t | span of {y(s), s ≤ t} | what we know |
| Innovation e(t) | y(t) − ŷ(t|t−1) | white driving noise |
| Optimal predictor | causal part of z⁻¹Φ | Wiener filter here |
| Backward state x̄ | from H_t backward | past Hankel block |

### Forward/backward duality
| Forward | Backward |
|---|---|
| state from past | state from future |
| innovations e | backward innovations ē |
| Σ = E[xxᵀ] | Σ̄ = E[x̄x̄ᵀ] |
| Wold/ARMA | anti-causal ARMA |

## Key Takeaways
Prediction = orthogonal projection; the orthogonality principle generates every optimal filter in this book.
Innovations whiten the past into an orthogonal basis — the trick that makes subspace projections computable.
Stationary processes have forward and backward Markov models whose state covariances are the two Gramians subspace methods estimate.
Ergodicity converts one long data record into ensemble statistics — the bridge from theory to sample covariances.

## Connects To
Hilbert-space projection (4.5) is the infinite-dimensional twin of ch2's matrix projections; ch5 computes the same projections recursively (Kalman filter); ch7-8 stochastic realization builds models from the covariance Hankel; ch9-10 estimate forward/backward state estimates from data matrices; Doraiswami ch2-3 cover correlation/spectra and estimation from the practitioner angle.
