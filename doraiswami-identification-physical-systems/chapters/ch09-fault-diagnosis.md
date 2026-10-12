# Chapter 9: Fault Diagnosis

## Core Idea
Fault diagnosis is estimation wearing a detective's hat: model faults as additive changes in a linear regression (or as influence vectors on states/outputs), generate a residual by running the ch6 Kalman filter on the nominal model, and then (a) *detect* — decide fault vs no-fault with a Bayes decision strategy (generalized likelihood ratio test built on the residual's statistics), and (b) *isolate* — classify which fault by matching the residual's direction against the influence vectors of candidate faults. The whole pipeline — residual generation → detection test → isolation classification — is pattern recognition on the innovation sequence.

## Frameworks Introduced
- **Diagnosis pipeline (9.1)**: identification → residual generation → fault detection → fault isolation, as four separable stages.
- **Nominal linear regression model (9.2)**: y = Hθ + v; nominal parameters θ₀ define the healthy system.
- **Fault modeling (9.4)**: a fault changes parameters/adds terms: y = Hθ₀ + Σᵢ hᵢfᵢ + v — each candidate fault i has an *influence vector* hᵢ (or matrix) and magnitude fᵢ; additive faults enter linearly.
- **Diagnostic parameters and feature vector (9.5)**: the estimable quantities that change under fault (θ̂ − θ₀, residual statistics) form the feature vector for classification.
- **Kalman filter residual (9.7)**: e(k) = y − ĉ from the nominal filter; under a fault the residual acquires a deterministic component along the fault's influence signature; key properties (whiteness under nominal, structured drift under fault) are the detection signal.
- **Bayes decision strategy for detection (9.9)**: frame detection as pattern classification (fault vs no-fault); generalized likelihood ratio test (GLT) with unknown fault magnitude estimated by ML inside the test; decision thresholds from priors/costs; alternative test statistics (χ²-type on residual energy).
- **Fault isolation as classification (9.11)**: candidate fault set → classify the observed residual/feature vector to the closest influence direction; isolation tasks formalized (single, multiple, simultaneous).
- **Influence vector estimation and additive faults (9.12)**: estimate fault magnitudes from data (parameter estimation again), enabling fault-size quantification, not just detection.

## Key Concepts
- Residual whiteness is the nominal invariant; faults break it in *known directions* — that structure is what makes isolation possible.
- GLT: maximize the likelihood under fault (over magnitude) vs under no-fault; the ratio is the test statistic — ch3's ML machinery in service of a decision.
- Influence vectors are the fault dictionary: model quality determines the dictionary, hence the diagnosis ceiling.
- Detection vs isolation are different problems: detection is a hypothesis test (sensitivity/false-alarm tradeoff); isolation is classification (separability of influence directions).
- Feature vectors from identification (diagnostic parameters) let model-based and data-driven diagnosis meet.
- Bayes framing: priors and misclassification costs set thresholds — pure significance testing is the special case.

## Mental Models
- "Residuals are testimony": the filter's innovation sequence testifies about model violation; the statistician cross-examines it.
- "Faults have signatures, not just presence": influence vectors turn diagnosis into matching a direction, not reading a magnitude.
- "Detect = test, isolate = classify": two different statistical tools on the same residual.
- "The model is the microscope": better nominal models ⇒ sharper influence vectors ⇒ smaller detectable faults.

## Anti-patterns
- **Thresholding raw residuals** — colored noise and transients swamp naive limits; use whitened/Kalman residual statistics with proper thresholds.
- **Isolation with collinear influence vectors** — unidentifiable fault pairs; check separability (rank/angles between influence directions).
- **Ignoring false-alarm cost in detection thresholds** — Bayes framing exists for this; a "sensitive" alarm that cries wolf is useless.
- **Fault models bolted on post hoc** — the additive-linear structure must be designed with the identification model (ch7) from the start.

## Reference Tables
### Diagnosis pipeline
| Stage | Object | Tool |
|---|---|---|
| Residual generation | e(k) | Kalman filter (ch6) |
| Detection | test statistic T(e) | GLT / Bayes test (9.9) |
| Isolation | feature vector vs influence set | classification (9.11) |
| Magnitude | f̂ᵢ | ML estimation (9.12) |

### Fault model anatomy
| Element | Meaning |
|---|---|
| Influence vector hᵢ | where fault i shows up in data |
| Magnitude fᵢ | size (estimated by ML) |
| Feature vector | estimable signature used for classification |
| Nominal θ₀ | healthy reference for deviations |

## Key Takeaways
Model-based fault diagnosis = Kalman residual + likelihood-ratio detection + influence-vector isolation: one statistical pipeline end to end.
Faults are additive signatures; detection tests their presence, classification identifies their direction.
The nominal model's quality and the influence vectors' separability bound what diagnosis can achieve.
GLT handles unknown fault sizes by estimating them inside the test — ML again.

## Connects To
ch6's filter and mismatch theory is the residual engine; ch3's ML/GLT is the decision engine; ch5's LS estimates fault magnitudes; ch7's identification supplies the nominal model and diagnostic parameters; ch10-12 apply the pipeline to physical systems and sensor networks; ch13 closes the loop with fault-tolerant control.
