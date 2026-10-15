# Patterns — Isermann, Fault-Diagnosis Systems

## P1. Name the supervision task before choosing the method
**Problem**: "we need fault detection" requests conflate five different jobs. **Pattern**: classify as monitoring (alarm), automatic protection (safe state), detection, diagnosis, or tolerance — each has different requirements (speed, false alarms, action authority). **Rule**: protection must be automatic and simple; detection/diagnosis may be sophisticated.

## P2. Classify the fault model first
**Pattern**: additive vs multiplicative × abrupt vs incipient × single vs multiple. Multiplicative faults need input excitation to be detectable; incipient faults need statistical tests with sample-size math; intermittent faults need memory (run-sums). **Rule**: the fault model dictates the detector — never start with the algorithm.

## P3. Statistical change detection with explicit detectability
**Pattern**: recursive mean/variance estimates → z/χ²/t/F tests at significance α; GLR/CUSUM for online drift; run-sum control charts for simplicity. Compute the sample size needed for the smallest fault of interest (0.1σ → ~384 samples at 95%) and put detection delay in the requirements. **Anti-pattern**: fixed hard thresholds at every operating point — use adaptive/fuzzy thresholds instead.

## P4. Parameter-deviation symptoms (Isermann's signature)
**Pattern**: run RLS/ELS online on a physical parameterization; deviations of K, T, mass, stiffness from nominal become symptoms with sensitivity-based fault mapping. Use square-root/U-D forms on embedded hardware. **Rule**: prefer this when faults map to parameters; prefer parity/observer residuals when they map to signals.

## P5. Design residuals for isolation from day one
**Pattern**: choose structured residuals (fault → subset pattern) or directional residuals (fault → direction); count capacity: n binary residuals → 2ⁿ−1 faults; add signs and sizes to extend. Enhance with low-pass filtering, sensitivity maximization, robustness to model error, adaptive thresholds. **Anti-pattern**: one generic residual and hope.

## P6. Parity and observers are interchangeable — pick maintainability
**Pattern**: same residual information via parity projection or observer error; unknown-input observers = observer-side disturbance decoupling. Choose whichever the team can build and certify; compare residual equations when migrating.

## P7. Closed-loop supervision needs u, not just y
**Pattern**: the controller masks faults into manipulated-variable offsets and performance degradation. Monitor IAE/oscillation indices; use the ccf phase test (disturbance ≈π vs friction vs instability); Fourier shape analysis for oscillation type; model-based bias/parameter estimation under feedback. **Rule**: a loop that oscillates after a maintenance change is a friction/stuck-actuator suspect first.

## P8. Unified fuzzy symptoms enable mixed-evidence diagnosis
**Pattern**: represent every symptom — residual flags, parameter deviations, operator impressions (noise, smoke) — as membership γ(sᵢ) ∈ [0,1]; feed one rule/inference engine. Combine with fault statistics as priors. **This is the cheap bridge between model outputs and human knowledge.**

## P9. Diagnosis method by data availability
**Pattern**: labeled fault data → Bayes/NN classification; interpretable rules needed → diagnostic trees + forward/backward chaining; both → neuro-fuzzy/SELECT (learn rules, keep interpretability). Efficiency metric: expected number of measurements/tests to isolate.

## P10. Redundancy budget: analytical where cheap, hardware where necessary
**Pattern**: sensors → analytical redundancy (model reconstruction + 2oo3 voting of measured+reconstructed values); actuators → hardware duplex (split the least reliable part, half-load units, fail-operational preferred); communication → protocol-level (CAN); software → recovery blocks/diverse standby. **Rule**: switches and voters add their own unreliability — count them.

## P11. Combine detection methods for reliability
**Pattern**: run 2–3 complementary detectors (limit checks + parameter estimation + parity residuals) and fuse decisions; detection probability rises, false alarms fall. Ch14's suitability tables guide the pairing by fault class and on-board cost.

## P12. Tolerance closes the loop
**Pattern**: fault-tolerant control = detection + isolation + reconfiguration (retune/reshape the controller after actuator/sensor loss); degradation steps define the fail-operational → fail-safe ladder in advance. Aircraft heritage: plan the ladder, don't improvise it.
