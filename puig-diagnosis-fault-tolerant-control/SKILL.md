---
name: puig-diagnosis-fault-tolerant-control
description: Apply Puig & Simani's Diagnosis and Fault-tolerant Control Vols 1-2 (ISTE/Wiley 2021) frameworks - IFAC SAFEPROCESS fault terminology, analytical redundancy, residual generation (observers/UIO, parity equations, parameter estimation), robustification (H-infinity, active/passive decoupling, adaptive thresholds), structural analysis (Dulmage-Mendelsohn, MSO, isolability matrix), set-membership zonotopic FDI, stochastic diagnosis as inverse problem, errors-in-variables/Frisch, TS fuzzy and consistency-based diagnosis (conflicts, possible conflicts), NLGA geometric decoupling, LPV polytopic observers with fault estimation, TS/neural H-infinity FTC, robust neural MPC, and virtual sensor/actuator reconfiguration - when designing, analyzing, or debugging fault detection and diagnosis (FDI/FDD) or fault-tolerant control (FTC) systems.
---

# Diagnosis and Fault-tolerant Control (Puig & Simani, ISTE/Wiley 2021, 2 volumes)

Two-volume edited set: **Vol 1 = Fault Detection and Diagnosis** (model-based, structural, set-based, stochastic, data-driven, AI methods); **Vol 2 = from nonlinear FDI to Fault-Tolerant Control** (nonlinear methods, LPV, fuzzy/NN, MPC, nonlinear FTC modeling, virtual sensors/actuators). Editors: Vicenç Puig (UPC Barcelona) & Silvio Simani (Ferrara).

Use when: designing FDI/FDD for a dynamic plant, choosing residual generators, making residuals robust to model uncertainty, analyzing detectability/isolability structurally, estimating fault magnitudes, or designing active/passive FTC.

## Decision index

| Situation | Go to |
|---|---|
| Need the agreed vocabulary (fault vs failure vs error vs symptom) | Vol1 Introduction |
| Pick a residual generator: observers, parity, parameter estimation | chapters/01-06-vol1-fdi.md Ch1 |
| Residual false alarms under model uncertainty | Ch1 robustness: H∞, active/passive, adaptive thresholds |
| What is detectable/isolable at all, before designing anything | Ch2 structural analysis: DM decomposition, MSO, isolability matrix |
| Unknown-but-bounded noise, guaranteed residual envelopes | Ch3 zonotopic set-membership |
| Uncertain stochastic plant, diagnosis as inference | Ch4 model-driven / data-driven / hybrid inverse problem |
| Both inputs and outputs noisy (low SNR) | Ch5 Frisch scheme / errors-in-variables |
| Component-level, symbolic, multiple-fault isolation | Ch6 Reiter conflicts, hitting sets, possible conflicts |
| Nonlinear plant FDI: EKF banks, NLGA, TS clustering | chapters/07-14-vol2-ftc.md Ch1 |
| Joint state+fault estimation on LPV/descriptor plant | Vol2 Ch2 robust polytopic observer |
| LMI-based FTC with TS/neural models | Vol2 Ch3 TS embedding, H∞ PDC, P-matrix rank test |
| Constrained nonlinear control that survives faults | Vol2 Ch4 robust neural MPC, error models, invariance |
| Estimate fault magnitude, drive reconfiguration | Vol2 Ch5 bank of MISO estimators, FMEA, signature matrix |
| Keep nominal controller, add fault tolerance cheaply | Vol2 Ch6 virtual sensors/actuators (extended separation) |
| Active vs passive FTC, digital-twin validation | Vol2 Ch7–8 |

## The one-paragraph model
Model-based diagnosis = **analytical redundancy**: compute the variable a second way with a software model; the difference is a **residual**. Everything else is engineering around two tensions: (1) the residual must be **insensitive to modeling uncertainty and disturbances but sensitive to faults** (robustness: decoupling, H∞, adaptive/set-based thresholds); (2) the residual structure must give **isolation** (directional residuals, banks of estimators, structural/isolability analysis, conflicts/hitting sets). FTC then either designs around the fault class (**passive**) or diagnoses magnitude and reconfigures (**active**: gain scheduling, MPC model switch, virtual sensor/actuator blocks that leave the nominal controller untouched).

## Files
- `chapters/01-06-vol1-fdi.md` — Introduction terminology + Vol1 Ch1–6 distilled
- `chapters/07-14-vol2-ftc.md` — Vol2 Ch1–8 distilled
- `glossary.md` — IFAC SAFEPROCESS terms + technical vocabulary
- `patterns.md` — residual-generation, robustness, isolation, FTC reconfiguration patterns
- `cheatsheet.md` — design workflow, thresholds, LMI recipes, structural analysis steps

Author naming kept throughout: ARR, MSO, UIO, NLGA, TS, PDC, RPO, possible conflicts, virtual sensor/actuator.
