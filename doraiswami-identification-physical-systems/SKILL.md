---
name: doraiswami-identification-physical-systems
description: Apply Doraiswami/Diduch/Stevenson's Identification of Physical Systems (Wiley 2016) frameworks - the augmented/integrated model principle, signal-class internal models, correlation/spectral/coherence characterization, ML and MMSE estimation, Kalman filtering with model-mismatch accounting, LS/RLS/PEM/subspace identification ladders, closed-loop identification, Kalman-residual fault detection (GLT/Bayes) with influence-vector isolation, sensor-network KF banks, and soft sensors with mixed-sensitivity fault-tolerant control - when identifying models of physical systems, monitoring condition, or diagnosing faults on real plants.
---

# Identification of Physical Systems (Doraiswami, Diduch, Stevenson, Wiley 2016)

Use when working with real plants: identifying models from operating (often closed-loop) data, monitoring condition, detecting/isolating faults, building soft sensors. The book's spine: one augmented model feeds identification, Kalman filtering, diagnosis, and control — a complete practitioner pipeline validated on laboratory rigs (magnetic levitation, two-tank process, mechatronic/velocity systems).

## Chapter map
- [ch01 Modeling of Signals and Systems](chapters/ch01-modeling-signals-systems.md) — signal generating filters, augmented ARMA/state-space models, internal model principle
- [ch02 Characterization of Signals](chapters/ch02-characterization-signals.md) — correlation, PSD, coherence, non-parametric ID
- [ch03 Estimation Theory](chapters/ch03-estimation-theory.md) — bias/variance/CRLB, Fisher information, ML
- [ch04 Estimation of Random Parameter](chapters/ch04-estimation-random-parameter.md) — Bayes/MMSE, conditional mean, Gaussian updates
- [ch05 Linear Least-Squares Estimation](chapters/ch05-linear-least-squares.md) — normal equations, SVD/pseudo-inverse, RLS
- [ch06 Kalman Filter](chapters/ch06-kalman-filter.md) — predict-correct, steady state, information fusion, model mismatch
- [ch07 System Identification](chapters/ch07-system-identification.md) — LS/RLS/high-order+reduction/PEM/subspace ladder, residual analysis
- [ch08 Closed Loop Identification](chapters/ch08-closed-loop-identification.md) — two-stage and direct (KF-based) approaches
- [ch09 Fault Diagnosis](chapters/ch09-fault-diagnosis.md) — influence vectors, KF residual, GLT/Bayes detection, isolation as classification
- [ch10 Modeling and Identification of Physical Systems](chapters/ch10-modeling-identification-physical.md) — maglev/two-tank/mechatronic case studies, gray-box + closed-loop ID
- [ch11 Fault Diagnosis of Physical Systems](chapters/ch11-fault-diagnosis-physical.md) — five-step scheme, fault emulators, diagnosability vs control tradeoff
- [ch12 Fault Diagnosis of a Sensor Network](chapters/ch12-fault-diagnosis-sensor-network.md) — KF bank, path analysis, model-free comparisons (ANN/ANFIS)
- [ch13 Soft Sensor](chapters/ch13-soft-sensor.md) — virtual instrumentation, mixed-sensitivity H∞, fault-tolerant integration

## Top-level references
- [glossary.md](glossary.md) — book's terms (integrated model, influence vector, coherence, GLT, internal model)
- [patterns.md](patterns.md) — recurring moves (augment-then-design, residual-as-instrument, exogeneity hunting)
- [cheatsheet.md](cheatsheet.md) — method ladders, diagnosis pipeline, decision tables

## Core theses (apply as defaults)
1. Model the exogenous signals (reference, disturbance, noise) with generating filters and augment with the plant — the integrated model is the single object for identification, filtering, and control.
2. Exact tracking/rejection requires the signal-class internal model embedded in controller or filter.
3. Every criterion is a likelihood: LS = Gaussian ML; check regressor-noise correlation before trusting any fit.
4. The Kalman residual is the book's instrument: white under matched model; its structured violation carries fault information (detect by GLT/Bayes, isolate by influence vectors).
5. Closed-loop data are the norm, not the exception: identify with two-stage or KF-based direct methods; feedback both enables data and masks faults.
6. Soft sensing + robust control + diagnosis compose on one augmented model: identification error becomes the uncertainty weight; the residual guards everything.

## When to load which chapter
Modeling setup: ch1, ch10. Signal analysis: ch2. Estimation foundations: ch3-5. Filtering: ch6. Identification: ch7 (open loop), ch8 (closed loop). Diagnosis: ch9 (theory), ch11 (rigs), ch12 (networks). Integration: ch13.
