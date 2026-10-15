---
name: isermann-fault-diagnosis-systems
description: Apply Isermann's Fault-Diagnosis Systems (Springer 2006) frameworks - the five supervision tasks (monitoring, protection, detection, diagnosis, tolerance), the fault/failure/malfunction definitions, additive vs multiplicative and abrupt vs incipient fault models, statistical change detection (z/t/chi-square/F tests, run-sum charts, SPRT/GLR/CUSUM, adaptive thresholds), parameter-estimation symptoms via RLS/ELS, parity-equation and observer residual generation with structured/directional residuals and 2^n-1 isolation, closed-loop supervision (IAE, cross-correlation phase, oscillation spectra), PCA multivariable detection, unified fuzzy symptom representation, Bayes/polynomial/geometric/fuzzy/NN classification, diagnostic trees and forward/backward chaining, SELECT, static vs dynamic redundancy with majority voting, analytical sensor redundancy, duplex actuators, CAN, and reconfigurable fault-tolerant control - when designing, analyzing, or debugging process supervision, FDI systems, or fault-tolerant control architectures.
---

# Fault-Diagnosis Systems (Rudolf Isermann, Springer 2006)

500-page, 19-chapter reference from fault detection to fault tolerance: definitions and reliability → fault/process models → statistical and model-based detection (parity, observers, parameter estimation, PCA) → closed-loop supervision → diagnosis (classification + knowledge-based) → fault-tolerant hardware/software design.

Use when: building FDI for a process or vehicle system, choosing residual methods, diagnosing control-loop performance problems, or designing sensor/actuator redundancy.

## Decision index

| Situation | Go to |
|---|---|
| What supervision task am I actually specifying? | chapters/01-06-concepts-models.md Ch2 |
| Fault is additive vs multiplicative; detectability? | Ch5 |
| What to monitor at all | Ch4 (FMEA/FTA) |
| Small mean/variance drift in noisy signal | chapters/07-09-detection-estimation.md Ch7 (z/χ²/t/F, GLR/CUSUM) |
| Rotating machinery symptoms | Ch8 (spectra, vibration) |
| Fault maps to a physical parameter | Ch9 (RLS/ELS + deviation rules) |
| Residual design, isolation patterns | chapters/10-13-residual-generation.md Ch10 (parity, structured/directional) |
| Observer/KF residual, disturbance decoupling | Ch11 |
| Control loop oscillating/sluggish | Ch12 (IAE, ccf phase, spectra) |
| Many correlated process variables | Ch13 (PCA) |
| Which method / how to combine | chapters/14-19-diagnosis-tolerance.md Ch14 |
| Symptom→fault mapping with mixed data+human evidence | Ch15 (fuzzy membership unification) |
| Labeled fault data available | Ch16 (Bayes/NN classification) |
| Interpretable rules, test sequencing | Ch17 (diagnostic trees, chaining, SELECT) |
| Redundancy architecture choice | Ch18 (static voting vs dynamic standby) |
| Sensor/actuator/comms fault tolerance | Ch19 (analytical redundancy, duplex drives, CAN, reconfiguration) |

## The one-paragraph model
Supervision is a pipeline: **faults** (additive/multiplicative, abrupt/incipient) perturb features; **detection** turns feature changes into symptoms using statistics (thresholds, GLR/CUSUM with sample-size math) or analytical redundancy (parity equations and observers generate residuals; structure them for isolation patterns, n residuals → 2ⁿ−1 faults); **diagnosis** maps symptoms to fault hypotheses with classification (Bayes/NN on labeled data) or knowledge (diagnostic trees, fuzzy-unified symptoms, neuro-fuzzy hybrids); **tolerance** closes the loop with redundancy — majority voting (static), standby (dynamic), analytical sensor reconstruction, duplex actuators, and reconfigured control. In closed loops the controller masks faults, so supervise manipulated variables and use closed-loop-aware methods. Model quality and excitation set the limits everywhere: multiplicative faults are invisible at zero input.

## Files
- `chapters/01-06-concepts-models.md` — supervision tasks, terminology, reliability/safety, fault & process models, signals
- `chapters/07-09-detection-estimation.md` — statistical change detection, signal analysis, parameter estimation
- `chapters/10-13-residual-generation.md` — parity equations, observers, closed-loop supervision, PCA
- `chapters/14-19-diagnosis-tolerance.md` — diagnosis, classification, knowledge-based methods, fault tolerance
- `glossary.md`, `patterns.md`, `cheatsheet.md`
