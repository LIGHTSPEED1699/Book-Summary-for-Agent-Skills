# Nguyen et al. Ch1–4 — CBM/PHM Framework, Sensing, Signal Processing

**Intelligent Fault Diagnosis and Prognosis for Engineering Systems** (Vachtsevanos, Lewis, Roemer, Hess, Wu; Wiley 2006). The CBM/PHM (condition-based maintenance / prognostics and health management) systems textbook.

## Ch1 — Introduction: the CBM/PHM frame
- Historical arc: aircraft BITE (built-in test) → digital BITE → centralized fault display (CFDS) — one fault lights up many systems; the diagnostic goal evolved to isolating the single LRU (line-replaceable unit) responsible.
- **Requirements must be probabilistic from day 1**: probability of anomaly detection (with false-alarm rate), probability of specific-fault classification with confidence bounds and severity, and for prognosis: a defined degradation threshold beyond which operation is unsatisfactory, a minimum warning time, and a minimum probability that remaining useful life ≥ that warning time.
- **"Designed-in" health management**: sensors → signal conditioning → data acquisition → data processing → reasoning/decision support integrated from the start, not bolted on.
- Diagnosis vs prognosis boundary (from the Preface): prognosis = providing **lead/warning time to failure**; any method giving a sufficient time-window answer counts (trending, life-usage counting, physics models — inclusive spectrum).
- PHM functional capability list: fault detection, isolation, advanced diagnostics, predictive prognosis, life-usage tracking, degradation trending, false-alarm mitigation, health reporting, decision support, fault accommodation, information fusion, information management.
- Failure progression timeline: incipient fault → detection → failure → system failure → mission loss; diagnosis operates between detection and failure; prognosis predicts the rest of the timeline.

## Ch2 — Business case and maintenance impact
- FMECA (failure modes, effects, criticality analysis) drives what to monitor; trade studies decide where CBM pays.
- CBM test-plan design and performance assessment precede adoption; case studies quantify maintenance/operations impact.
- CBM in control and contingency management: health info feeds mission re-planning (ACM-style).

## Ch3 — Sensors and sensing
- Transduction principles; vibration (accelerometers piezoelectric/triaxial), temperature, pressure, flow, acoustic, fiber-optic, MEMS.
- **Sensor placement** matters for observability of fault features.
- **Wireless sensor networks** (architecture, power, networking) and **smart sensors** (on-board ADC, filtering, FFT, self-calibration, temperature compensation).
- Feature extraction is "an art": features live in time, frequency, wavelet, or chaotic domains; features should be uncorrelated, ranked, normalized; final feature vector optimal for discriminating the fault under computational constraints.

## Ch4 — Signal processing and data management
- Preprocessing: denoising (wavelet soft-thresholding / shrinkage — signal energy concentrates in few coefficients, white noise disperses), compression (wavelets beat FFT on nonstationary signals; 10–20× ratios on vibration).
- Processing: FFT, short-time FFT, wavelets as feature extractors, cepstrum, enveloping (high-frequency demodulation for bearing faults), Impact Energy features.
- **Vibration monitoring**: the workhorse for rotating machinery — RMS, kurtosis, crest factor, spectral sidebands, harmonic/subsynchronous patterns.
- **Virtual sensor**: map available measurements to an inaccessible "fault measurement" via a local model (orifice example: Q = K√ΔP) or NN (engine combustion virtual sensor); sensor-data validation via parity relations.
- Image feature extraction for defect classification (snake segmentation etc.).
- **Fusion/integration**: Dempster–Shafer for combining feature-level evidence (each feature = an "expert" with possibility → basic probability assignment; Dempster's combination rule).
- Usage-pattern tracking; databases and OSA-CBM/MIMOSA open-architecture data server standards.

## Practitioner takeaways (Ch1–4)
- Specify detection/isolation/prognosis requirements as probabilities with confidence bounds before choosing algorithms.
- Feature vector = sufficient statistic for the fault state; invest in feature evaluation (Ch7 metrics) before classifier design.
- Wavelets do three jobs in this stack: denoise, compress, extract features.
- Virtual sensors turn available I/O into estimates of the unmeasurable fault variable — the bridge from sensing to model-based diagnosis.
