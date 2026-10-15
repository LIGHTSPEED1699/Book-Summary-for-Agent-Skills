# Patterns — Nguyen et al., Intelligent Fault Diagnosis and Prognosis

## P1. Probabilistic requirements first
**Problem**: PHM systems specified vaguely fail acceptance. **Pattern**: write requirements as probabilities with confidence: detection % of FMECA faults, isolation % to LRU/ORA, incorrect-ID rate, false-alarm rate, BIT end-to-end time, prognosis confidence (threshold/objective), minimum warning time, replacement-at-10%-life. **Rule**: requirements depend on available feature-evaluation and performance metrics — define metrics before demanding them.

## P2. Feature vector as sufficient statistic
**Problem**: raw sensor streams are too big and noisy for diagnosis. **Pattern**: extract φ[x(t)] in time/frequency/wavelet/chaotic domains; features uncorrelated, ranked, normalized; keep only what changes P(z|x). Evaluate with ideal-classifier error, entropy/information gain, distance/dependence measures, two-sample z-test. **Anti-pattern**: piling on correlated features; skipping feature evaluation before classifier tuning.

## P3. Diagnosis method selection by available knowledge
**Pattern**: legacy fault records → alarm bounds + conditional expectation + clustering + CBR; expert heuristics → fuzzy pattern logic; multiple independent sensor opinions → Dempster–Shafer fusion; physical parameters → KF/RLS estimation + deviation rules; known component physics → FEA + physics vibration models; system structure → MBR diagnostic trees; earliest warning → statistical change detection. **Rule**: methods compose — the Navy chiller example runs fuzzy features into D–S fusion.

## P4. Parameter-deviation diagnosis
**Problem**: faults are physical changes, not raw signal changes. **Pattern**: model the component (state-space), run RLS/Kalman to estimate physical parameters (stiffness, damping, leakage), apply IF-parameter-deviation THEN-fault rules. Kalman gives covariance bounds → know when the estimate is trustworthy. **This is the bridge from control-style estimation to diagnosis.**

## P5. Vibration signature lookup for rotating machinery
**Pattern**: map spectral symptom → fault: imbalance 1× shaft speed; misalignment 2× + high axial; looseness higher harmonics; bearing clearance subsynchronous whirl; race defect (n/2)× (n balls); gear bevel defect at natural frequency with running-speed sidebands. Extract via enveloping/Impact Energy; validate independently with oil-debris counts.

## P6. Physics-plus-measurement prognosis (the flagship)
**Problem**: predict RUL of an unmeasurable fault variable (crack length, spall size). **Pattern**: (1) physics growth model (Paris law dα/dN = C₀ΔKⁿ, bearing RCF models); (2) operational profile → loads; (3) recursive Bayesian estimation (particle filter; Kalman if linear-Gaussian) fusing model + online features; (4) learning/correction terms to fix model drift for long horizons; (5) output TTF PDF + confidence bounds. **Rule**: this hybrid beats pure data-driven when physics is known; seeded-fault test rigs provide validation data.

## P7. Weibull for fleet-level time-to-failure
**Pattern**: fit Weibull to failure-time data (MLE or Bayesian with priors on shape/scale); read β: <1 wear-in, =1 random, >1 wear-out; derive RUL with credible intervals. Use when component-level sensing is absent but fleet history exists.

## P8. Data-driven prognosis with confidence machinery
**Pattern**: run-to-failure datasets → DWNN (delayed I/O + wavelet net) as trend predictor; CPNN or bootstrap-style methods for confidence limits; train early (1/100th of record) and extrapolate. **Anti-pattern**: trusting raw NN predictions without bounds — prognosis without confidence is unusable.

## P9. Metrics-driven assessment
**Pattern**: diagnosis → ROC (pick threshold by criticality: strict = few false alarms, lenient = few misses); prognosis → accuracy + precision + timeliness + confidence, evaluated statistically across experiments; report against threshold/objective bands. **Rule**: a prognostic claim without accuracy AND precision AND timeliness is incomplete.

## P10. Monte Carlo maintenance scheduling
**Problem**: convert RUL PDF into actions. **Pattern**: Monte Carlo over predicted TTF (mean ± 2σ) → part/personnel availability curves vs lead time → schedule maintenance where availability meets mission need; feed ULR into supply chain; cost-compare schemes (replacement vs inspection vs CBM) with ground-turn costs.

## P11. Validate on seeded-fault rigs
**Pattern**: engineer a known fault (Brinell indentation on a bearing race), run accelerated tests, collect multi-channel data (vibration at >200 kHz, oil debris), use to develop/validate features and models end-to-end. **Rule**: no prognostic algorithm ships without seeded-fault or historical run-to-failure validation.
