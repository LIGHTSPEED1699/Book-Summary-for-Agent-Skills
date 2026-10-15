# Cheatsheet — Nguyen et al., Intelligent Fault Diagnosis and Prognosis

## PHM design workflow
1. FMECA → candidate fault modes; trade studies → which are worth monitoring.
2. Requirements: detection %, isolation %, false-alarm rate, warning time, prognosis confidence (threshold/objective).
3. Sensor suite + placement for the feature vector; consider WSN/smart sensors.
4. Signal chain: denoise (wavelet soft-threshold) → compress (wavelet) → features (FFT, enveloping, wavelet coefficients, Impact Energy, RMS/kurtosis/crest).
5. Feature evaluation: entropy/IG, distance, z-test; keep uncorrelated ranked set.
6. Diagnosis: pick per P3 (fuzzy/D-S/KF-RLS/MBR/CBR/SCD).
7. Prognosis: physics+particle filter (preferred) / Weibull / DWNN+CPNN.
8. Metrics: ROC for diagnosis; accuracy/precision/timeliness for prognosis.
9. Maintenance: Monte Carlo availability curves → schedule + supply chain; cost-benefit.

## Vibration symptom table (rotating machinery)
- Imbalance → 1× shaft speed
- Misalignment → 2× + high axial vibration
- Mechanical looseness → higher harmonics
- Bearing clearance → subsynchronous whirl
- Bearing race defect → (n/2)× shaft speed, n = ball count
- Gear bevel defect → gear natural frequency, sidebands at bad gear's running speed
- Broken motor bars → sidebands in vibration FFT around line frequency

## Kalman filter (discrete)
- Time: x̂⁻ = A x̂ + B u; P⁻ = A P Aᵀ + G Q Gᵀ
- Gain: K = P⁻ Hᵀ (H P⁻ Hᵀ + R)⁻¹
- Meas. update: x̂ = x̂⁻ + K (z − H x̂⁻); P = (I − K H) P⁻
- RLS = KF over parameter vector; use forgetting factor for time-varying params.

## Paris law + stochastic growth
- dα/dN = C₀ (ΔK)ⁿ; ΔK = stress-intensity range; estimate C₀, n by nonlinear RLS.
- Stochastic: parameters random → SDE; propagate distribution; particle filter fuses with measured features (crack length from virtual sensor).

## Weibull quick facts
- F(t) = 1 − exp(−((t−γ)/η)^β); β<1 decreasing hazard (wear-in), β=1 constant (exponential), β>1 increasing (wear-out).
- Bayesian fit: treat (α, λ) random; posterior from Π f(tᵢ|α,λ) × prior; marginals → RUL credible bounds.

## Dempster–Shafer quick recipe
1. Frame X = fault modes; each feature → BPA mᵢ (from membership functions).
2. Bel(A) = Σ_{B⊆A} m(B); ignorance lives in subsets, not forced onto singletons.
3. Combine: m(A) = [Σ_{Ai∩Bj=A} m₁(Aᵢ)m₂(Bⱼ)] / (1 − K), K = Σ_{Ai∩Bj=∅} …
4. Assume independence of evidence; distrust if features share a sensor.

## ROC reading
- Curve = TP-rate vs FP-rate over thresholds; diagonal = coin flip; area = accuracy.
- Strict threshold (bottom-left): few false positives, many misses. Lenient (top-right): opposite. Pick by fault criticality.

## Prognosis metric formulas (spirit)
- Accuracy_i = 1 − |t_pf − t_af| / D₀ (normalized distance).
- Precision = 1 − (confidence-interval width)/R₀ (narrower = better).
- Timeliness: failure must fall inside/after the predicted window usefully.
- Report statistically across many runs; separate maintainer view (when to fix) from commander view (mission availability).

## Benchmarks/case studies in the book
- UH-60 intermediate gearbox + main transmission (MBR, FEA crack diagnosis, maintenance cost model), CH-47D combiner transmission (SCD), Allison T63-analog bearing rig (seeded spall, enveloping, oil debris, Yu–Harris M50 RCF Monte Carlo), Navy centrifugal chiller (fuzzy + D–S diagnosis; DWNN bearing-crack prognosis), helicopter fuel system (JSF structural/functional models), motor drives (FPL broken-bar rules).

## Common pitfalls
- Point-estimate RUL without confidence bounds → unusable for decisions.
- Feature sets correlated/unevaluated → classifier overfits, ROC mediocre.
- D–S on evidence from the same physical sensor → independence violated, overconfident fusion.
- NN prognosis without CPNN-style confidence → precision invisible.
- Skipping seeded-fault validation → algorithms fail on real incipient faults.
- Requirements without metrics → acceptance disputes; define metrics first.
