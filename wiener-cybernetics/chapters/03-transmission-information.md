# Ch3 — Transmission of Information

## Wiener's definition of information (independent of Shannon, 1948)
- A message is one member of an **ensemble** of messages with a probability distribution. Information conveyed by choosing among messages with probabilities p_i:
  **I = −Σ p_i log₂ p_i** bits (additive for independent messages; maximal log₂ n for n equally likely choices).
- Continuous version with density p(x): −∫ p(x) log p(x) dx (with the usual caveats about the zero of the scale).
- **Information = negative entropy.** Boltzmann: S = −k ∫ p log p dΓ. The Maxwell demon pays for its information; "the information of a system is its negative entropy" — measure organization of a system by how far its entropy is below maximum. (Cybernetics = the statistical theory of the organization of the system.)
- Meaning vs information: engineering information is purely statistical — "so well adapted to convey our desires" — semantic content is irrelevant to the channel problem.

## Message, noise, and the general problem
- **Noise** = an independent ensemble corrupting the message. The general problem of communication engineering: observations y depend arbitrarily on message + noise with known joint distribution; **how much information do the observations carry about the message?** (mutual information — Wiener gives the change-of-variables formula for the information gained by fixing y's.)
- This framework evaluates modulation schemes: with flat static on the ether and fixed bandwidth/power, **no transmission means beats amplitude modulation** in information efficiency (though other schemes may suit the receiver better); coding for compression (Bell Labs Vocoder) and decoding matched to the receptor are the complementary arts.
- Carrier waves add no information rate: all its information is delivered in an arbitrarily short interval; it is an "extra message" already known.

## Time series in statistical equilibrium (stationarity)
- A message homogeneous in time: an ensemble of functions f(t) whose probability distribution is invariant under f(t) → f(t+λ). The time-translation group T_λ.
- **Ergodic assumption** (Wiener's working hypothesis, proved where possible): time average = ensemble average. Justified for the processes at hand; without it, statistics from a single record is impossible.
- Almost-periodic functions and the harmonic analysis of non-decaying signals: the power spectrum exists as a distribution; **Wiener–Khinchin: the power spectrum is the Fourier transform of the autocorrelation** φ(τ) = lim (1/2T)∫ f(t+τ)f*(t)dt. (Wiener's own theorem — the chapter's mathematical core.)

## Filtering and prediction (the Wiener problem)
- Physical operators on a signal are **causal**: output = ∫₀^∞ a(τ) f(t−τ) dτ — integration over the past only. Any apparent operator using the future signals an unstable/self-oscillating system, not a true operator.
- **Filtering problem**: recover f(t) from f(t)+noise(t) using a causal linear operator. **Prediction/extrapolation**: estimate f(t+λ) from the past — same machinery; the optimal filter's coefficients come from the autocorrelations of signal and noise (the Wiener–Hopf problem, solved in Ch9's context).
- Prediction is possible only where the signal has regularity (correlation extending into the future); a genuinely random component is irreducible. Anti-aircraft aiming: predict the target's future position from its past — the best predictor is the one matched to the ensemble of all flights, not to the single track.

## Speculative coda: resonance and reproduction
- Molecular resonance as the basis of biological specificity and template reproduction (genes/viruses copying by resonant attraction) — Wiener flags it as hypothesis; revisit with Ch10's frequency-attraction machinery.

## Fallacies
- Treating a single record as self-explanatory without an ensemble model (no stationarity assumption → no statistics).
- Confusing semantic meaning with channel information; the theorems are about signal ensembles.
- Believing a predictor can beat irreducible noise: the error floor is set by the noise spectrum.
