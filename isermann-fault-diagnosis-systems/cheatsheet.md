# Cheatsheet — Isermann, Fault-Diagnosis Systems

## Chapter locator
1 intro · 2 supervision tasks & definitions · 3 reliability/maintainability/availability · 4 FTA/ETA/FMEA/risk · 5 fault & process models · 6 signals · 7 limit/trend/change detection · 8 signal analysis & vibration · 9 parameter estimation · 10 parity equations/residuals · 11 observers/KF · 12 closed-loop supervision · 13 PCA · 14 method selection · 15 diagnosis framework · 16 classification · 17 knowledge-based (trees, chaining, neuro-fuzzy) · 18 redundancy structures · 19 fault-tolerant systems.

## Statistical tests quick table
- Mean shift, known σ: z-test; detect Δμ=0.1σ → N≈384, 0.2σ → 96, 0.3σ → 43 (95%).
- Variance increase, one sample: χ²-test (~30 samples for +10% σ).
- Two-sample means: t-test; two-sample variances: F-test.
- Online drift: CUSUM/GLR (recursive), SPRT (log-likelihood ratio, sign decides).
- Simple QC: run-sum control chart (σ-band scores, RS threshold, sign flip ends run).
- Always: recursive or windowed mean/variance; adaptive thresholds in varying operating ranges.

## Residual design checklist
1. Model class (state-space vs polynomial) → parity (input/output form) or observer (state/KF/UIO).
2. Structure: structured (patterns) or directional (angles); isolation capacity 2ⁿ−1.
3. Enhance: LP-filter noise, maximize sensitivity, robustify vs model error, adaptive thresholds vs excitation.
4. Check excitation: multiplicative faults invisible at zero input.
5. Verify: simulate ΔK/ΔT faults; compare output-error vs equation-error residuals.

## Closed-loop oscillation triage
- IAE between zero crossings + oscillation index; count load-detections.
- ccf phase: ≈π even function → sinusoidal disturbance or unstable loop; static friction → different phase.
- Spectrum shape: sinusoidal vs rectangular/triangular harmonics.
- Suspects after maintenance: stuck valve, friction, wrong controller parameter.

## Diagnosis method picker
- Labeled data, black-box OK → Bayes (Gaussian) / NN.
- Interpretability, test sequencing → diagnostic trees, backward chaining (interactive) / forward chaining (monitoring).
- Mixed human+sensor evidence → fuzzy membership unification + rules.
- Data + interpretability → SELECT / neuro-fuzzy.

## Fault tolerance picker
- Sensor: analytical redundancy (model reconstruction) + 2oo3 voting; fail-silent switching if switches are reliable enough.
- Actuator: duplex drive (half-load motors), fail-operational; standby (hot = fast but ages; cold = no wear but slow).
- Computer/software: TMR voting; recovery blocks (diverse software); duplex comparators for fail-safe.
- Communication: CAN-style bus.
- Control: reconfiguration after isolation; pre-planned degradation ladder.

## Key formulas (spirit)
- Availability A = MTBF/(MTBF+MTTR); R(t) = exp(−∫λdt).
- Residual evaluation: |r| > r_th with r_th adaptive to input excitation; pattern vector r* for isolation.
- CUSUM-type GLR recursion: s(k) = s(k−1) + (Δμ/σ²)·(y(k) − μ₀) style accumulation; sign/threshold decides.
- PCA: covariance eigendecomposition; keep k components; Q-residual = x − x̂(back-transformed).

## Common pitfalls
- Supervising only y in a closed loop (controller hides faults in u).
- Hard fixed thresholds → false alarms at transients, misses at steady state.
- One unstructured residual → detection without isolation.
- Ignoring excitation: multiplicative fault tests fail at idle/zero input.
- Forgetting voter/switch unreliability in redundancy budgets.
- Diagnosis without priors: skip fault statistics and pay in test count.
- PCA hiding faults in discarded components.
