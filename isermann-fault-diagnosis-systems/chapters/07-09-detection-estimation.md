# Isermann Ch7–9 — Change Detection, Signal Methods, Parameter Estimation

## Ch7 — Simple supervision and statistical change detection (the workhorse chapter)
- **Limit checking** of absolute values; **trend checking** (slope/derivative limits).
- **Change detection with binary thresholds**: model Y(k) = nominal + fault + noise; test whether mean and/or variance changed.
  - Estimate mean/variance online: recursive averaging or sliding-window estimates.
  - **z-test** on the mean: for 95% confidence, detecting a mean shift of 0.1σ needs N≈384 samples; 0.2σ → 96; 0.3σ → 43 (detectability ∝ 1/Δμ²).
  - **χ²-test** on variance: ~30 samples detect a 10% σ increase.
  - **t-test** (two-sample mean comparison), **F-test** (two-sample variance comparison).
  - **Run-sum / control charts**: score deviations in σ-bands, accumulate; alarm when run sum RS exceeds threshold; run ends when sign flips.
  - **Likelihood-ratio / SPRT**: compare p(Y|H0) vs p(Y|H1); log-likelihood ratio accumulates, sign change decides; for known jump size Δμ the recursive test quantity is the **GLR (generalized likelihood ratio)** form; **CUSUM** as the standard recursive variant.
- **Fuzzy thresholds** (soft bands, membership-weighted alarms) and **adaptive thresholds** (depend on operating point/input excitation — essential in closed loop).
- **Plausibility checks**: rate-of-change, range, gradient consistency between related sensors.

## Ch8 — Signal-based methods
- Periodic signal analysis: FFT, amplitude/phase spectra, harmonic signatures; non-stationary periodic signals (order tracking); stochastic signal analysis (correlation functions, PSD, cepstrum).
- **Vibration analysis of machines**: bearing/machine fault signatures in spectra and envelope spectra — signal methods as symptoms for rotating machinery.

## Ch9 — Parameter estimation methods (model-based symptoms)
- **Least squares → recursive LS (RLS)** for online parameter estimates; **extended least squares (ELS)** for colored noise (model the noise polynomial D(z), roots inside unit circle); instrumental variables / maximum likelihood variants.
- Numerical robustness: **square-root filtering** (Cholesky factor S of P), **U-D factorization** — avoid covariance blowup on embedded hardware.
- **Symptom generation with identification models**: estimate physical parameters (mass, stiffness, resistance, time constant) online; **parameter deviation = fault symptom**; sensitivity matrix links parameter changes to faults.
- Trade-off: window length vs speed vs noise; persistent excitation required for identifiability (multiplicative faults!).

## Practitioner takeaways (Ch7–9)
- Pick the statistical test by what changes: mean (z/t/GLR-CUSUM), variance (χ²/F), both (likelihood ratio).
- Sample-size math is design data: incipient fault size sets the detection delay — state it in requirements.
- Parameter-estimation diagnosis is Isermann's signature: prefer estimating physical parameters over raw residual thresholds when the fault maps to parameters.
