# Glossary — Nguyen et al., Intelligent Fault Diagnosis and Prognosis for Engineering Systems

## Program-level
- **CBM** — condition-based maintenance: maintenance triggered by measured condition, not schedule.
- **PHM / prognostics and health management** — the full stack: sensing, diagnostics, prognostics, health management decisions.
- **PHM** in this book also "prognostics and health management"; **RUL / ULR** — remaining useful life / useful life remaining.
- **LRU / ORA** — line-replaceable unit / organizational removable assembly: isolation targets.
- **BITE / BIT** — built-in test equipment / capability; **CFDS** — centralized fault display system.
- **FMECA** — failure modes, effects, and criticality analysis: decides what to monitor.
- **RCM** — reliability-centered maintenance: the without-CBM baseline.
- **OSA-CBM / MIMOSA** — open-system software architecture standard for distributed CBM components; virtual data server.
- **ACM** — automated contingency management: mission re-planning from health state.

## Diagnosis
- **FDI** — fault detection and identification (the book's term for the diagnosis task).
- **Feature vector φ[x(t)]** — data set sufficient for determining fault status; formally a **sufficient statistic** for the fault state z(t) given history x(t).
- **Condition indicator** — synonym for feature in PHM practice.
- **Alarm bounds** — prespecified signal boundaries flagging anomaly (Bollinger bands from current signal, or from historical failure data).
- **FPL / fuzzy pattern logic** — IF (feature is linguistic-value) THEN (fault k) rules; firing degrees = fault belief; no defuzzification needed.
- **Dempster–Shafer evidence theory** — frame of discernment X; basic probability number/assignment (BPA m); belief Bel(A) = Σ_{B⊆A} m(B); plausibility; **Dempster's rule of combination** with conflict normalization; explicit ignorance.
- **MBR / model-based reasoning** — qualitative structural+functional models, constraint propagation over intervals, diagnostic trees; efficiency = expected measurements to isolate.
- **CBR / case-based reasoning** — retrieve–reuse–revise–retain cycle; case = condition, measurement, symptom, component, action, outcome, explanation; adaptation challenge.
- **SCD / statistical change detection** — quickest detection of subtle statistical changes (Parker/Barron Associates).
- **Enveloping (high-frequency demodulation)** — vibration feature extraction for bearing faults.
- **Impact Energy** — spectral feature (filtered-impact energy spectrum) for early bearing/spall detection.
- **Virtual sensor** — analytic mapping from available measurements to an inaccessible fault-relevant variable (local physics model or NN); sensor-data validation via parity relations.

## Prognosis
- **Prognosis** — predicting remaining useful life with a time window and confidence; "pro + gnosis", foretelling the course of the disease.
- **TTF** — time to failure; **TTF PDF** — the prognostic deliverable.
- **Paris law** — deterministic fatigue crack growth dα/dN = C₀ ΔKⁿ; stochastic versions randomize parameters.
- **ΔK** — stress-intensity factor range per loading cycle; **K_ISCC** — stress-corrosion threshold.
- **ARMA / ARMAX / ARIMA** — stochastic dynamic model families for trending; identification loop with validation on unseen data.
- **Kalman filter** — recursive Bayesian estimation under linear/Gaussian assumptions; provides state + covariance bounds.
- **Particle filter** — sequential Monte Carlo recursive Bayesian estimation without linearity/Gaussianity; the book's flagship prognostic engine with online learning/correction terms.
- **Weibull distribution** — time-to-failure model: shape β (hazard decreasing/constant/increasing), characteristic life η, location γ; bathtub curve.
- **DWNN / dynamic wavelet neural network** — NN predictor with delayed I/O in the feature vector; wavelet activation; LM or genetic training.
- **CPNN / confidence prediction neural network** — NN predictor that also outputs confidence limits.
- **Monte Carlo life distribution** — propagate input uncertainty distributions through the physics model to a life distribution (e.g., Yu–Harris M50 bearing RCF model).

## Metrics
- **Accuracy (prognostic)** — closeness of predicted TTF to actual, normalized.
- **Precision (prognostic)** — narrowness of the prediction interval (variance across experiments).
- **Timeliness** — failure occurring usefully relative to the predicted horizon.
- **ROC curve** — true-positive vs false-positive rate across decision thresholds; area = diagnostic accuracy index.
- **Information gain / entropy** — feature evaluation: prefer features that reduce class uncertainty; two-sample **z-test** for feature distribution separation.
- **Threshold/objective requirement pairs** — e.g., prognosis confidence 90% threshold / 98% objective; warning time 1 day / 7 days.
