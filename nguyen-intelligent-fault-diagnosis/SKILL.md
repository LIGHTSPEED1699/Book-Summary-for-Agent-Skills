---
name: nguyen-intelligent-fault-diagnosis
description: Apply Vachtsevanos/Lewis/Roemer/Hess/Wu's Intelligent Fault Diagnosis and Prognosis for Engineering Systems (Wiley 2006) frameworks - CBM/PHM system architecture, feature-vector-as-sufficient-statistic diagnosis, fuzzy pattern logic and Dempster-Shafer evidence fusion, Kalman/RLS parameter-deviation diagnosis, FEA-assisted model-based diagnosis, model-based reasoning with diagnostic trees, case-based reasoning, statistical change detection, physics-based prognosis (Paris law, Weibull), particle-filter Bayesian prognosis with learning, ARMA/ARMAX trending, dynamic wavelet neural networks and CPNN, prognostic metrics (accuracy/precision/timeliness/ROC), and Monte Carlo maintenance scheduling - when designing condition-based maintenance, fault diagnosis, remaining-useful-life prediction, or PHM systems for machinery and engineering assets.
---

# Intelligent Fault Diagnosis and Prognosis for Engineering Systems (Vachtsevanos, Lewis, Roemer, Hess, Wu — Wiley 2006)

The CBM/PHM (condition-based maintenance / prognostics & health management) systems textbook: sensing → signal processing → diagnosis → prognosis → maintenance decisions, with aircraft/industrial case studies throughout.

Use when: building PHM/CBM for machinery, choosing diagnosis algorithms from sensor features, predicting remaining useful life (RUL), specifying prognostic requirements/metrics, or turning RUL predictions into maintenance schedules.

## Decision index

| Situation | Go to |
|---|---|
| What is a PHM system, what to require of it | chapters/01-04-cbm-phm-framework.md Ch1 |
| Sensor choice, placement, WSN/smart sensors | Ch3 |
| Denoise/compress/extract features from vibration | Ch4 (wavelets, enveloping, FFT) |
| Feature vector design (sufficient statistic) | Ch5 §5.2 |
| Legacy fault data available | Ch5 §5.3 (alarm bounds, conditional expectation, clustering) |
| Explainable rules / multiple sensor evidence | Ch5 §5.4 (fuzzy pattern logic, Dempster–Shafer) |
| Estimate physical parameters as features | Ch5 §5.5 (KF, RLS + deviation rules) |
| Crack/component diagnosis from physics | Ch5 §5.6 (FEA, planetary gear vibration models) |
| Component-level isolation, qualitative | Ch5 §5.7–5.8 (MBR diagnostic trees, CBR) |
| Earliest possible detection | Ch5 §5.9 (statistical change detection) |
| RUL with known failure physics | chapters/06-08-prognosis-metrics-support.md Ch6 §6.2 (Paris law + particle filter) |
| Time-to-failure statistics only | Ch6 §6.3 (Weibull, Bayesian fit) |
| Big historical run-to-failure datasets | Ch6 §6.4 (DWNN, CPNN) |
| Judge a diagnosis/prognosis system | Ch7 (feature metrics, ROC, accuracy/precision/timeliness) |
| Turn predictions into maintenance plans | Ch8 (Monte Carlo scheduling, cost models) |

## The one-paragraph model
A PHM system turns sensor streams into a **feature vector that is a sufficient statistic for the fault state**, classifies it (fuzzy rules, D–S evidence fusion, NNs, KF/RLS parameter deviations, qualitative models), then **projects the fault's growth dynamics forward** — with physics (Paris-law crack growth, bearing RCF models) driven by the operational profile and corrected online by recursive Bayesian estimation (Kalman as Gaussian special case, **particle filter** as the general tool) — to output a **time-to-failure PDF with confidence bounds**; those bounds feed Monte-Carlo maintenance scheduling. Requirements and metrics (detection %, false alarms, ROC, prognostic accuracy/precision/timeliness) are specified probabilistically from the start.

## Files
- `chapters/01-04-cbm-phm-framework.md` — CBM/PHM frame, sensing, signal processing
- `chapters/05-diagnosis.md` — the diagnosis method zoo
- `chapters/06-08-prognosis-metrics-support.md` — prognosis, metrics, product support
- `glossary.md`, `patterns.md`, `cheatsheet.md`

Author naming kept throughout: CBM/PHM, FDI, LRU/ORA, FMECA, OSA-CBM/MIMOSA, FPL, BPA, SCD, MBR, CBR, DWNN, CPNN, Impact Energy, RUL/ULR.
