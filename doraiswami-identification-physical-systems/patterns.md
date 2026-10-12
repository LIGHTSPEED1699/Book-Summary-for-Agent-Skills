# Patterns — Identification of Physical Systems (Doraiswami et al.)

Recurring reasoning moves across the book.

## 1. Augment, then design once
Model plant + disturbance + noise + reference as one integrated object (ARMA or state-space); identification, filtering, control, and diagnosis all consume it. **Use when:** starting any plant problem — build the augmented model first (ch1).

## 2. Model the exogenous signals
References, disturbances, noise each get a generating filter; embed the signal-class model (internal model) where exact tracking/rejection is required. **Use when:** steady-state error matters (ch1, ch6.3).

## 3. Second-order statistics as instruments
Correlation for detection/delay/periodicity; PSD for signatures; coherence as the trust flag. **Use when:** characterizing or diagnosing signals without a parametric model (ch2).

## 4. Every criterion is a likelihood
LS = Gaussian ML; PEM = general ML; GLT = likelihood ratio for decisions. Ask "which noise model makes this criterion ML?" **Use when:** choosing or auditing any estimator (ch3, ch5, ch7, ch9).

## 5. Check regressor-noise correlation before trusting a fit
E[Hᵀe] ≠ 0 ⇒ bias. This single test explains ARX failure under output-error noise and under feedback. **Use when:** any identification result looks too easy (ch7.10, ch8).

## 6. Hunt for exogeneity under feedback
Two-stage prediction, KF innovations, external references — closed-loop methods manufacture decorrelated handles. **Use when:** data come from a running loop (ch8).

## 7. The residual is the instrument
White under matched model; structured violation = information. Tune to whiteness, test against whiteness, diagnose by violation direction. **Use when:** monitoring anything (ch6, ch9, ch11-13).

## 8. Detect by test, isolate by direction
Detection = GLT/Bayes hypothesis test; isolation = match residual against influence vectors (fault dictionary). **Use when:** fault diagnosis (ch9, ch11).

## 9. Emulate faults to build the dictionary
Influence vectors come from offline perturbation experiments (fault emulators), not from real failures. **Use when:** deploying diagnosis on hardware (ch11).

## 10. Topology does the isolating
In networks, one filter per signal pair; intersect path verdicts to locate faults. **Use when:** sensor networks (ch12).

## 11. Identification error becomes the uncertainty weight
Robust control (mixed-sensitivity) designs on the identified model with uncertainty bounded by identification quality. **Use when:** closing the loop on identified models (ch13).

## 12. Soft-sense the unmeasurable
Identified model + Kalman filter = virtual sensor; guard its validity with the residual. **Use when:** the controlled variable is slow/expensive/unmeasurable (ch13).

## Anti-patterns (cross-chapter)
- ARX-LS on output-error or closed-loop data (ch7-8).
- Thresholding raw residuals instead of whitened statistics (ch9).
- Judging diagnosability by tracking performance (ch11).
- Forcing physical model order onto weak data (ch11).
- Using spectral ratios without coherence (ch2).
- Robust design ignoring identification-derived uncertainty (ch13).
