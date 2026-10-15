# Glossary — Isermann, Fault-Diagnosis Systems

## Supervision and terminology
- **Supervision** — umbrella: monitoring, automatic protection, fault detection, fault diagnosis, fault tolerance (the five tasks, Ch2).
- **Fault** — "unpermitted deviation of at least one characteristic property (feature) of the system from the acceptable, usual, standard condition"; a state; abrupt / incipient (drift) / intermittent.
- **Failure** — "permanent interruption of a system's ability to perform a required function"; an event caused by faults.
- **Malfunction** — incorrect function without interruption.
- **Reliability R(t)** — probability of failure-free operation; **λ(t)** failure rate (bathtub); **MTBF**, **MTTR**, **availability** A = MTBF/(MTBF+MTTR).
- **FMEA / FTA / ETA** — failure mode & effects analysis (bottom-up), fault tree (top-down), event tree (forward).
- **Monitoring** — limit checks + operator alarms; **automatic protection** — automatic counteraction to a safe state (fuse, overspeed trip).

## Fault models
- **Additive fault** — deviation independent of the input signal (sensor offset, disturbance); detectable at any operating point.
- **Multiplicative fault** — deviation proportional to an input (gain change, parameter change); invisible when the input is zero → **excitation required**.
- Sensor faults: offset, drift, gain error, precision loss, short circuit, saturation; first-order lag dynamics; internal vs external disturbances.
- Actuator faults: stuck, friction/backlash, leakage, dead time; process faults: parameter changes (mass, stiffness, resistance, time constant, catalyst activity).

## Detection
- **Symptom** — binary/graded statement that a feature deviated; **feature** — extracted value (signal-based or model-based: parameters, residuals).
- **Limit checking / trend checking** — threshold on value / derivative.
- **Change detection** — statistical tests on mean/variance: **z-test**, **t-test**, **χ²-test**, **F-test**; **run-sum (control chart)**; **SPRT** (sequential probability ratio test), **GLR** (generalized likelihood ratio), **CUSUM** (recursive cumulative-sum variant).
- **Adaptive threshold** — threshold varying with operating point/input excitation; **fuzzy threshold** — soft band with membership.
- **Plausibility check** — consistency of rate/range/gradient with related signals.

## Model-based FDI
- **Analytical redundancy** — a model of the same process replaces hardware redundancy to produce cross-checks.
- **Residual** — signal generated to be zero (nominal) and fault-sensitive: r = f(measured, model); **primary residual** from direct model forms.
- **Parity equation / ARR** — projection of measured I/O data onto a null space eliminating unknown states; **input form** vs **output form** residuals; discrete-time parity approach.
- **Structured residuals** — each fault affects a designed subset → residual **patterns** for isolation; **directional residuals** — fault → fixed direction in residual space, length = size.
- **Strongly/weakly isolating** — pattern separability classes; n binary residuals → up to **2ⁿ − 1** faults.
- **Sensitivity vs robustness** — maximize fault effect, minimize model-error/noise effect; the central residual-design trade.
- **Observer methods** — state observer, **Kalman filter** (innovation = residual), **unknown-input/output observers**; equivalent to parity methods.
- **Parameter estimation methods** — LS, **RLS**, **ELS** (extended LS for colored noise), instrumental variables, ML; **square-root / U-D factorization** for numerical robustness; parameter deviation as symptom.
- **PCA** — principal component analysis; detection via transformed variables or **back-transformation residuals** (Q-type).

## Closed-loop supervision
- **Control performance monitoring** — detecting degraded loop performance (oscillation, sluggishness, offset).
- **IAE** — integral of absolute error between zero crossings; oscillation indices; **ccf phase test** — cross-correlation phase shift distinguishes load disturbance (≈π), friction, instability.
- **Bias estimation / observer bank** — model-based closed-loop detection.

## Diagnosis
- **Fault diagnosis** — determine type, size, location, time of detection from symptoms.
- **Analytical symptoms** (from limits/residuals/parameters) vs **heuristic symptoms** (operator: noise, smoke, color); **unified symptom representation** via fuzzy membership γ(sᵢ) ∈ [0,1].
- **Fault–symptom relationship** — physical cause-effect propagation inverted by diagnosis.
- **Bayes classification** — Gaussian class-conditional densities, maximum-likelihood parameters, decide max posterior; polynomial/geometric/fuzzy/NN classifiers.
- **Diagnostic (fault) trees** — symptom-pattern → component hypotheses; efficiency = expected measurements to isolate.
- **Forward chaining** (data-driven) vs **backward chaining** (hypothesis-driven) inference; **neuro-fuzzy hybrids**, **SELECT** self-learning classification tree.

## Fault tolerance
- **Static redundancy** — parallel modules + **majority voting** (TMR, 2-out-of-3), fault masking, no switchover.
- **Dynamic redundancy** — standby: **hot standby** (ages, fast switchover) vs **cold standby** (no wear, slower); **duplex** with comparators + switches; hybrid schemes.
- **Fail-safe vs fail-operational** — go to safe state vs keep functioning; **degradation steps** — graceful ladder as faults accumulate.
- **Analytical sensor redundancy** — reconstruct measurement from models + other sensors; ≥3 values for voting (ESP yaw-rate example); **fail-silent** sensor switching.
- **Duplex actuator** — split least-reliable part into half-load units (cabin-pressure flap, two motors one gear).
- **CAN bus** — Controller-Area Network, fault-tolerant serial communication since 1983.
- **Fault-tolerant control** — detection + isolation + **reconfiguration** of the control system (aircraft heritage).
