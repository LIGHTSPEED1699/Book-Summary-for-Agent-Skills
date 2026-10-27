# Isermann Ch7-9 — Detection Methods: Limit Checking, Signal Analysis, Parameter Estimation

**Fault-Diagnosis Systems** (Springer 2006). Deep rewrite from the full extraction. OCR caveat: most display equations render as formula-not-decoded in this scan; formulas marked [reconstructed] are standard textbook forms anchored to surviving prose/printed example numbers; [OCR?] marks garbles. Nothing invented.

## Isermann Ch7 — Limit Checking / Statistical Detection

### Ch7 intro (lines ~2429-2433)
- Ch7 = "Fault detection with limit checking". Simplest & most frequently used fault-detection method: limit checking of a directly measured variable Y(t).
- Three flavors: (1) check absolute values vs thresholds, (2) check trends (derivatives), (3) plausibility checks.
- Stray line "755" = [OCR?] page junk (page 75).

### 7.1 Limit checking of absolute values
- Preset two thresholds: max Y_max (OCR "Yq") and min Y_min (OCR "Y,,;,,"). Normal state iff Y_min < Y(t) < Y_max — formula itself <!-- formula-not-decoded -->.
- Staying inside tolerance zone = normal; exceeding either threshold indicates a fault somewhere in the process (Fig 7.1a). Applied in almost all process-automation systems.
- Worked examples (all from text): oil pressure of combustion engines (lower limit); coolant water temp of combustion engines (upper limit); circulation-fluid/refrigerant pressure of refrigerators (lower limit); control error of a control loop.
- Threshold design: chosen from experience, a compromise — trade-off: too narrow -> false alarms from normal fluctuations; too wide -> late detection of faulty deviations. No hard numbers given here; design tension restated in 7.3.
- Fig 7.1: (a) absolute value Y(t); (b) trend = dY/dt.

### 7.2 Trend checking
- Compute first derivative (trend) dY(t)/dt and check it against a threshold (formula not decoded).
- With small thresholds the trend check alarms EARLIER than absolute-value checking (Fig 7.1b) — key advantage.
- Applications named: oil pressure & vibration of oil bearings of turbines; wear measures of machines.
- Combining absolute + trend checks requires mutual coordination of thresholds. One scheme: make absolute thresholds functions of the trend — Y_max = f(dY/dt > 0), Y_min = f(dY/dt < 0) [OCR garble "Ying = /( Y>0) and ae (Y<0)"] so fast-developing deviations alarm early while small trends far from the threshold don't cause false alarms (Fig 7.2: thresholds Y_max/Y_min are functions of the trend). Ref [7.17].
- Signal-prediction upgrade: polynomial regression models + recursive least squares estimation -> predict N samples ahead (k = t/T0 discrete time; formula not decoded). Better than raw trend: shows threshold-exceedance danger earlier, and avoids false alarm if signal returns to normal zone without action. Stochastic difference-equation prediction of the random component also possible, refs [7.17],[7.19].
- Thresholds can be made adaptive (function of other variables, e.g. process input excitation) -> see Section 7.5.

### 7.3 Change detection with binary thresholds (7.3.1 + 7.3.2; lines 2469-2783)
#### 7.3.1 Estimation of mean and variance
- Monitored variables are stochastic Y(t) with pdf p(Y), mean mu and variance sigma^2 as NOMINAL values of the fault-free process; after fault onset time t_f (unknown) they change to mu1, sigma1^2.
- Three change cases (Fig 7.3, normal pdfs, nominal index 0 vs faulty index 1):
  - 1) mean changes mu1 = mu0 + delta_mu, sigma1 = sigma0 constant;
  - 2) mean unchanged, sigma1 = sigma0 + delta_sigma;
  - 3) both change.
- Case 1 rule-of-thumb: if pdfs don't significantly overlap a fixed threshold suffices — detect just by observing mean estimate, threshold factor e.g. k > 2 [formula-not-decoded; form ~ |mu1-mu0| > k*sigma0]. Trade-off again: small-change detectability vs false alarms.
- If delta_mu is small vs sigma (say k < 1) -> statistical tests required.
- Off-line change detection: store all data, test where in a sample of length N the change at unknown t_f occurred. On-line real-time: decide at every sample k -> sequential/recursive tests are the interesting ones for fault detection. Off-line is easier (more measurements).
- Setup: Y(t) scalar sampled at T0; Y(k) random with pdf p(Y), Gaussian assumed; var = E{Y} first moment, D{Y} second central moment; decomposition Y(k) = mu(k) + n(k) with zero-mean noise n, sigma_n = sigma_Y.
- Estimation (ergodicity assumed, one sample function): sample mean mu_hat(N) = (1/N) sum_{k=1..N} Y(k); variance estimate with (1/(N-1)) form [both formulas not decoded]. Recursive forms by subtracting mu_hat(N) from mu_hat(N+1) -> standard increment form mu_hat(N+1) = mu_hat(N) + [Y(N+1) - mu_hat(N)]/(N+1) [reconstructed; source formula not decoded]. Corresponding recursive variance forms exist, ref [7.15],[7.8].
- Sliding window length w: mean over last w samples + recursive form; variance window estimate + recursive [formulas not decoded].
- Higher-order LPFs usable but at the cost of detection time (key design statement).
- Exponential forgetting, forgetting factor lambda < 1 (e.g. lambda = 0.95; OCR "A = 0195"): equivalent to frozen gain k_f = 1 - lambda in eq (7.15) [7.18]; (7.21) = discrete-time first-order low-pass filter for E{Y(k)}: mu_hat(k) = (1-k_f) mu_hat(k-1) + k_f Y(k) [reconstructed; source not decoded]. Fig 7.4: mean AND variance each via first-order LPF (variance needs E{Y^2} also through a first-order LPF).
- Comparing different variables Y_i(k): use variation coefficient V = sigma/mu [7.6] [formula not decoded].
#### 7.3.2 Statistical tests for change detection [7.23],[7.24],[7.4],[7.26],[7.12]
#### a) Hypothesis testing
- Null hypothesis Ho (no fault): Y = Y0; change hypothesis H1 (fault): Y = Y1 [formulas not decoded; named by bullets "null hypothesis (no fault)" / "change hypothesis (fault)"].
- Decision rule: assume Ho true unless sample falls outside region of acceptance -> reject Ho, accept H1.
- Fig 7.5: acceptance/rejection regions of a symmetric (two-sided) test. Significance level alpha = 0.05 or 0.01 (small). Acceptance region: mu_hat within [mu0 - c, mu0 + c]-ish [formulas not decoded; text: acceptance mu_-alpha < mu_hat <= mu_{1-alpha}, rejection mu_hat < mu_-alpha or mu_hat >= mu_{1-alpha}].
- Test classes: parametric (normal distribution assumed: t-test, likelihood/ratio tests) vs distribution-free/nonparametric [7.12]. Book mainly covers parametric; F-test described as nonparametric [note: F-test actually assumes normality - book wording].
#### b) Test quantities
- Mean test quantity (7.32): s = [mu_hat(N) - mu0] / (sigma/sqrt(N)) [reconstructed form; consistent with Ex 7.1 numbers] — t-distributed ("f-distributed" OCR) with degree of freedom f = N - 1; N = number of samples.
- Variance test quantity (7.33): chi^2 = sum_k Y^2(k) / sigma0^2 [reconstructed] — chi-square distributed with N degrees of freedom; reject Ho (variance increased with prob 1-alpha) if chi^2 > chi^2(N, 1-alpha).
- Example 7.1 (mean test, numbers): sigma = 1, threshold s > 1.96 for large N, alpha = 0.05 (95%). Required samples from (7.32): delta_mu = 0.1 -> N > 384; delta_mu = 0.2 -> N > 96; delta_mu = 0.3 -> N > 43 samples to detect with 95% probability. (Matches N = (1.96*sigma/delta_mu)^2; time-to-detection = N samples — the design numbers of the chapter.)
- Example 7.2 (variance test, numbers): test if sigma^2(N) grew from sigma0^2 = 1 to 1.2; chi-square table at alpha = 0.05 (95%) for N = 5, 10, 30 — critical values not decoded [OCR: table missing]; (7.33) result: at N = 30, chi^2 > chi^2(30, 0.05) -> about 30 samples required to detect sigma grew by about 10%.
#### c) Detection of changes in mean: t-test
- Before change: mean Y0, N0 samples; after: mean Y1, N1 samples. Normal distribution, variances before/after unknown but equal [7.4]. Test quantity t = (mu_hat1 - mu_hat0) / (s_d * sqrt(1/N0 + 1/N1)), s_d pooled std dev [reconstructed; formula not decoded].
- Decision: |t| > t(alpha, N0 + N1 - 2) -> change occurred (t from table at level alpha).
- Special case N1 << N0: test quantity reduces to (7.32) form.
#### d) Run/run-sum tests (control charts) [7.22],[7.13]
- Prereq: mu0 and sigma0 known before change, sigma unchanged (sigma1 = sigma0).
- Simple one-sided run test: alarm if one value > 3 sigma OR if 7 or more values [OCR "7 = 7 values"] successively above the mean [7.9].
- Run-sum tests = cumulative sum (CUSUM) of the variable. Score-band scheme (Table 7.1, two-sided): classify Y into deviation bands as multiples v of sigma; band above mean: mu0 < Y < mu0+sigma -> sc = +0?, +sigma..+2sigma -> +1?, +2sigma < Y < +3sigma -> sc = +2 (worked in text), above 3sigma -> +3 [OCR table columns garbled "30 +3 / 20 +2 / lo +1 / Oo +0 / -0 / -1 / -2 / 30"; read: bands at sigma,2sigma,3sigma with scores +/-0..3; band (mu0+2sigma, mu0+3sigma) -> +2 explicit in prose]. [OCR? exact band-to-score mapping partly lost]
- Run sum RS = sum of scores over the run; if RS exceeds threshold RS_max -> change detected. A run terminates when Y crosses to the opposite side of the mean (deviation sign flips).
#### e) Detection of variance change: F-test
- Compare two variances; both samples normal; means need NOT be known and may differ. Test quantity F = sigmahat1^2 / sigmahat0^2 [reconstructed]. F follows F-distribution with (m1, m2) dof, m1 = N1 - 1, m2 = N0 - 1 [OCR "(77;.7772)"]; F(alpha, m1, m2) from table. If F > F(alpha,...) [formula not decoded] then sigma1^2 > sigma0^2 with probability (1-alpha).
- Meta-design caveat (key passage): all classical tests above require BOTH N0 and N1 relatively large; large N1 contradicts early detection -> classical tests generally NOT recommended for fast real-time change detection.
#### f) Likelihood-ratio test for jump detection (SPRT + GLR/CUSUM) [7.25],[7.10],[7.11],[7.21],[7.3],[7.2],[7.1]
- Assumptions: Y(k) statistically independent; pdf type known (e.g. normal); parameters (e.g. mu) estimated; p_Y(Y, theta) = likelihood function (observations fixed, parameters variable).
- Likelihood ratio Lambda(Y) = p_Y(Y|H1) / p_Y(Y|H0) compares densities py(Y|mu0) vs py(Y|mu1) (cf Fig 7.3). Decision: Lambda > Lambda_crit -> H1; Lambda < Lambda_crit -> H0.
- Log-likelihood ratio (7.42): l = ln Lambda; decision sign of l (threshold ln Lambda_crit); simpler computation. This is the sequential probability ratio test SPRT.
- Normal pdf, known mu0, mu1, sigma1 = sigma0 = sigma -> (7.42) simplifies [formula not decoded, form l = (Y-mu0)^2... standard normal-log form] [7.1].
- Generalized LR for unknown jump time: after jump at time k', likelihood ratio over window [formula not decoded]; known jump delta_mu = mu1 - mu0 assumption -> test quantity S = sum over window of (Y(k) - mu0) type [not decoded], computable for window length (N - k'). With s = S/delta_mu a recursive form emerges [not decoded]; change-detection algorithm + incremental quantity [not decoded] that changes sign after a jump in Y(k). Known as Page-Hinkley stopping rule / cumulative sum (CUSUM) algorithm; note different CUSUM variants exist (cf run-sum in d).
- Unknown jump magnitude: run two parallel tests assuming mu0 known, with minimal jump magnitude assumed in both signs +delta_mu_min and -delta_mu_min [7.2].
- Closing caveat of 7.3.2 (explicit design guidance): the statistical tests need strong distributional assumptions that experimental residuals mostly violate (not independent, not normal, non-stationary, unknown mean/variance changes) -> FIRST try simple tests of 7.3.1 plus adaptive thresholds (Sec 7.5); design the feature so it shows strong deflection.

### 7.4 Change detection with fuzzy thresholds (2784-2792)
- Binary normal/faulty decision is artificial — seldom a sharp border (Fig 7.6a). Fuzzy threshold = more realistic alternative.
- Model the stochastic variable Y(t) as fuzzy set z_Y(Y) for normal state (membership fn mu_y, not to be confused with mean mu of earlier sections). Triangular fuzzy set: center = mean, lower width parameter A = k*sigma0, k = 2, 3, ... [OCR "A = xo;, kK = 2.3,...."].
- Separate membership fn mu_y+ for "increased" as fuzzy threshold; match changed fuzzy set z'(Y) against threshold -> exceeding degree [formula not decoded]. Worked number: result mu_Y = 0.6 = threshold reached to 60% — gradual severity info, richer than binary. (Fig 7.6b.)
- Ref [7.20].

### 7.5 Adaptive thresholds (2794-2798)
- Motivation (forward link to model-based chapters): models don't match reality -> residuals deviate from zero even fault-free; deviation depends on amplitude/frequency of input excitation. Residual model: static part proportional to input U(t) + dynamic part (e.g. dependent on dU/dt or U variations).
- Scheme [7.16] (also [7.5],[7.7]): threshold generated from process input: first-order HPF enlarges threshold (captures dynamic part), constant c2 adds proportional/static enlargement, LPF smooths the threshold. Fig 7.7: threshold = f(u) + const threshold = c2*u [OCR "theonst = Cy"].
- Tuning numbers: time constants T1 (HPF) and T2 (LPF, OCR 7;/73) chosen ~ dominating process time constant; ratio T2/T1 [OCR 7/7;] set by model uncertainty of the dynamics. Fig 7.8: example residual r(t) with adaptive threshold.

### 7.6 Plausibility checks (2808-2832)
- Rough supervision: check credibility/compatibility of indicated values. Single measurement: correct sign + value within limits = limit checking with usually WIDE tolerances.
- Multi-sensor consistency via logic rules relating normal ranges [formulas not decoded]. Worked example (prose): circulation pump with rotational speed n and pressure p -> expected relation [formula missing].
- Operating-condition-dependent plausibility: worked example: oil pressure p_oil of combustion engine vs speed and cooling-water temperature theta [formula not decoded, "04470" OCR = theta_Kuehlw].
- Rules built with binary logic AND/OR; violated rule -> either process or sensors faulty; further testing needed for localization.
- Conceptual role: presupposes variable ranges per operating condition = ROUGH process model; shrinking ranges explodes rule count -> then switch to mathematical models; plausibility checks = first step toward model-based fault detection.

### 7.7 Problems (2834-2842)
- Ch7 exercises: 1) advantages of combining absolute-value + trend checking; 2) water-network pressure p(t): mean/variance estimation eqs with time window and with exponential forgetting; 3) which tests for mean vs variance changes, what must be known; 4) which tests suitable for on-line real-time detection; 5) binary vs fuzzy thresholds comparison; 6) plausibility rules for pneumatic flow valve, ranges: p_air = 0.2...1.0 bar, valve position u_valve = 1%...100%, mass flow m_flow = 0.1...10 m^3/h [OCR "9.1... 10m?/h" -> 0.1 likely, marked uncertain].

### Boundary note
- Line 2844 "## Fault detection with signal models" + intro (vibration features: imbalance, bearing faults, knocking, chattering; nonparametric spectra/correlation vs parametric amplitude/ARMA models) is the Ch8 title page bleeding inside the window; Ch8 proper section 8.1 starts at line 2854. Ch7 content ends at 2842.

## Isermann Ch8 — Dynamic Signal Analysis-based Fault Detection

> Source: /home/hongbin/.knowledge/isermann-fault-diagnosis/pi/full_text.txt lines 2854-3691. Ch9 starts 3692.

### Ch8 intro — "Fault detection with signal models" (OCR heading; task calls it "dynamic signal analysis"; intro starts ~L2820)
- Many process signals oscillate: harmonic, stochastic, or both. Signal changes traceable to actuator/process/sensor faults -> signal-model-based FD applies.
- Machine vibration (position/speed/accel measurement) detects: imbalance, bearing faults (turbo machines); knocking (gasoline engines); chattering (metal grinding machines).
- Other sensors too: electrical current, position, speed, force, flow, pressure — carry oscillations at frequencies well above process dynamics.
- Scheme (Fig 8.1): assume math model of measured signal (cf. Ch6) -> compute features (amplitudes, phases, spectrum frequencies, correlation functions) over band wmin < w < wmax -> compare vs features observed in normal behavior -> feature changes = analytical symptoms.
- Signal models split: NONPARAMETRIC (frequency spectra, correlation functions) vs PARAMETRIC (amplitudes at distinct frequencies, ARMA-type models).
- Fig 8.2 survey: periodic signals -> bandpass filtering / Fourier analysis / correlation analysis [OCR? garbled column]; stochastic -> spectrum analysis; non-stationary -> (short-time) Fourier + wavelet analysis.
- Signal model: measured = steady-state Y00 + periodic part; after removing Y00 analyze y(t) only. y(t) = usable part yu(t) + noise n(t); n zero-mean, uncorrelated with yu.
- Fourier-series view: any periodic signal = superposition of harmonic components; each set by amplitude y0i, frequency w_i, phase phi_i, damping factor d_i (decaying sinusoids). For fault detection often only w_i and y0i (frequency + amplitude) suffice.
- NOTE: nearly all displayed equations in this chapter are `<!-- formula-not-decoded -->` in OCR; equation numbers (8.3)...(8.13) etc. survive. Do not trust any specific formula transcription.

### 8.1 Analysis of periodic signals
- Setup (L2856-2900): periodic y(t) superimposed on steady-state value Y00 (abs. signal = Y00 + y(t), see Sec 6.1). Component params y0i, w_i, phi_i, d_i to be determined by analysis method; usually only y0i and w_i needed.

#### 8.1.1 Bandpass filtering (L2902-2910)
- Classical way to get amplitude-vs-frequency spectrum: pass signal through bank of analog bandpass filters w/ different center freqs (Fig 8.3), or one filter whose center freq sweeps a range.
- Filter specs: bandwidth = width between 3-dB frequencies; flank steepness e.g. band at 60-dB attenuation. Analog or digital (A/D + recursive filter algos -> real-time filtering).
- Constant ABSOLUTE bandwidth -> uniform resolution on linear freq scale; use when range limited (~2 decades). Constant PERCENTAGE bandwidth -> uniform on log scale; use for wide ranges (>=3 decades).
- Power spectrum: filtered signal -> detector -> square + integrate over time = average power; sqrt of mean-square = RMS amplitude.
- Discrete-stepped bandpass analyzer: stepped center freqs, detector switched sequentially over filter outputs, amplitude/power per band, pen recorder/printer. Narrow-band: single tunable filter better; spectrum appears continuously vs frequency.

#### 8.1.2 Fourier analysis (L2912-2936)
- Sinusoidal phase-shifted oscillations (Eq 8.3) expand into Fourier series (Eq 8.4 [formula missing]).
- If freqs v*omega0 known, amplitudes from Fourier coefficients (Eqs 8.5-8.7: a_n, b_n type [formula missing]); complex form (Eq 8.8-8.9?) with complex Fourier coefficients.
- Limit: T0 -> infinity => omega0 -> dw, v*omega0 = w continuous => periodic fn becomes non-periodic => Fourier transform y(iw) (Eq 8.13).

#### 8.1.3 Correlation functions (L2938-2962)
- Autocorrelation function (ACF)/autocovariance for stationary zero-mean (disturbance + periodic) signals: general form Eq 8.14 [formula missing].
- For periodic signals average over INTEGER periods (Eq 8.15).
- For sinusoidal phase-shifted oscillation with w_i = 2*pi/T (Eq 8.16): ACF is again periodic (Eq 8.17) and INDEPENDENT of phase shift phi_i.
- Key robustness: stationary disturbance n(t) and oscillations with w != n*w_i (n->inf) have no influence on ACF => ACF suitable for periodic signals w/ stochastic disturbance.
- Cross-correlation between input u(t) = u0*sin(w t) of a linear system and output y(t) (Eq 8.18): only components of y(t) at w (equal to driving freq) contribute — similarity to Fourier coefficient b_n (Eq 8.5). (Basis of frequency-response estimation / lock-in detection.)

#### 8.1.4 Fourier transformation (L2964-3003)
- FT of non-periodic y(t): Eq 8.19 [forward, formula missing]; convergence condition: integral of |y(t)| finite (Eq 8.20 [formula missing]).
- Fig 8.4 amplitude densities of finite-duration signals: (a) decaying oscillation; (b) growing+decaying oscillation; (c) finite periodic signal; (d) rectangular signal time course. FT of oscillation of finite duration T -> peak at w = w_i; longer T => higher, narrower peak; steady-state oscillation T->inf => |y(iw)| delta-like, convergence condition no longer fulfilled.
- Sampling y(t), sampling time Ts, y(t)=0 for t<0: discrete approx of FT (Eq 8.22 [formula missing]); dropping constant Ts -> DFT (Eq 8.23); restrict to finite measuring interval 0 <= k <= N-1 (Eq 8.24).
- Discrete amplitude spectrum Eq 8.25; discrete phase spectrum Eq 8.26 [formulas missing]; abbreviation -> z-transform (Eq 8.27?).

#### 8.1.5 Fast Fourier transformation (FFT) (L3008-3132)
- Plain DFT cost: per angular freq w_l: 2N multiplications + 2(N-1) additions -> too slow. FFT exploits cyclic properties of oscillation pointers in complex plane: only re-sorting data + multiplications with precalculated sin/cos values.
- Discretized angular freqs spacing Dw. Finite measuring duration T = N*Ts: lowest describable w_min = 2*pi/T = 2*pi/(N*Ts) [OCR shows "20/T = 22/NTpo"]; highest w_max = 1/Ts per Shannon sampling theorem. Frequency resolution Eq 8.29 [formula missing].
- Complex precomputable factors w_N^(...), Eq 8.30-8.31; symmetry property Eq 8.32 (conjugate symmetry of spectrum). Even/odd sample decomposition of y(k) -> two half-length subsequences (Eq 8.33-8.35); recurse while subsequence length even.
- Perfect symmetry utilization needs N = 2^p (power of two). Then FFT = rearrangement + multiplications by precomputable complex values; effort ~ 4N*log2(N)?? real multiplications+additions [OCR garbled: "each 4N /gN//g2" -> read as ~ (N/2)log2 N class; DO NOT quote exact constant].
- Algorithm families: Cooley-Tukey (re-sort then multiply) vs Sande-Tukey (multiply then re-sort) [8.41].
- Table 8.1 required calculations DFT vs FFT (multiplications/additions; columns garbled by OCR):
  - N=128: DFT 33282 / 256(?) vs FFT 3584 / 3584  [OCR? — 33282 looks like 2*128^2=32768-ish mis-OCR; additions col shifted; treat with caution]
  - N=1024: DFT ~2101250?/2048 vs FFT 40960 / 40960 [OCR? likely 1,048,576 ops class; numbers as printed: 2101250, 2048, 40960]
  - N=4096: DFT 33570818?/8192 vs FFT 196608 / 196608 [OCR? 33570816=2*4096^2 fits pattern; printed 33570818]
- Example 8.1 (numbers): DSP32C (AT&T) signal processor, clock f_c = 50 MHz (Ts' = 20 ns) per calculation step (one floating-point add and/or multiply); multiplier-adder cascade -> add+mul run in ONE step -> for FFT (equal counts of both ops) half the computing time saved; for DFT only minor effect.
  - Table 8.2 computing times (as printed, some OCR noise): N=128: DFT ~26.8 ms vs FFT 2.85 ms, factor DFT/FFT = 94 [OCR shows "/26.8 ms"; Fig 8.7 caption later reuses 26.8 for N=4096, so 128-row value may be 12.68 ms [OCR?]]; N=1024: DFT 1.68 s vs FFT 32.75 ms, factor 513; N=4096: DFT 26.86 s vs FFT 0.1575 s, factor 1705.
  - Lesson: time-saving factor grows with N.
- FFT data-length caveat: N must be power of 2 (often N = 1024 = 2^10 [OCR "2!°"]); otherwise truncate or zero-pad to next power of 2 = corruption of raw data.
- Leakage: finite record = multiplication by rectangular window f_rec(k) (Eq 8.36, Fig 8.5); y_win(k) = y(k)*f_win(k) (Eq 8.37). In freq domain -> convolution of true spectrum with FT of rectangular window = sinc fn of length N -> sharp spectral lines smear over whole freq range = LEAKAGE effect.
- Mitigation: windowing f_win(k) (Eq 8.38, Fig 8.6) that tapers continuously from 1 mid-record to 0 at edges; reduces leakage but DEGRADES resolution (edge values corrupted).
- Example 8.2 (worked): sinusoidal oscillation y(k) = sin(2*pi*f0*k*Ts) [Eq 8.39 formula missing] with f0 = 1 Hz (per Fig 8.7/8.8 captions: "sinusoidal oscillation with 1 Hz"), sampled (Ts = 200 us? OCR shows "79 = 2005" [OCR? — likely Ts = 200 us]) over k = 0..N-1; amplitude spectrum via FFT.
  - a) NO extra window: for small N (N = 128) significant estimation error of amplitude AND frequency (Fig 8.7, several N).
  - b) WITH Hanning window: improvement of frequency & amplitude estimation for small N (N = 128) (Fig 8.8); leakage influence decreases as N grows.
- Periodogram (power spectrum from DFT): compute discrete amplitude spectrum |y_D(i w)| via FFT, then periodogram relation Eq 8.40 [formula missing] (|amplitude|^2 type).

#### 8.1.6 Maximum entropy spectral estimation (L3134-3150)
- Motivation: FFT problems would vanish if signal outside measuring interval were known; Burg [8.6] approach: PREDICT unknown signal course from known measured values with NO a-priori assumptions -> maximum uncertainty/entropy => "maximum entropy" spectral estimation, substantially better resolution, esp. suitable for fault detection with few distinct frequencies.
- a) Parametric signal models in frequency domain: fictitious FORM FILTER F(z) / F(iw) excited by Kronecker-delta pulse (Eq 8.41) generating steady-state oscillations y(k) (Fig 8.9). Choose filter dynamics so its frequency response equals measured signal's amplitude spectrum (Eq 8.42); same for power spectral density (Eq 8.43).
- Three parametric model approaches [8.4]: MA (moving average) model = starts Eq 8.44 (continues next chunk).

#### 8.1.6 b) Determination of the coefficients (L3192-3252)
- Trick for suppressing stochastic components: estimate from the AUTOCORRELATION Ryy(t) (Eq 8.45-8.46) instead of raw y(t). Ryy of a periodic signal is again periodic (type 8.43) -> form-filter model can be assumed for Ryy itself (Eq 8.47).
- ACF carries eigen-behavior: m characteristic freqs w_i and damping d_i; PHASE INFORMATION IS LOST; ACF amplitudes become y0i^2-type (Eq 8.48, ~ squares of signal amplitudes [formula missing, inferred from "amplitudes of the ACF become" + Eq 8.46 relation]).
- ARMA form-filter model on ACF with m eigenfreqs -> filter-difference eq of order n = 2m (Eq 8.47); additive zero-mean uncorrelated disturbance n(t) included; its autocorrelation Rnn(t) contributes only at t = 0 (constant, Eq 8.48-ish spike).
- ARMA signal model (8.47) reaches steady state after tr = 2m steps; after that all B-parameters drop out -> ACF proceeds as stationary steady-state oscillation describable by AR part alone. Key structural fact: for ACF of harmonic signal, AR model of order 2m suffices.
- AR eigen-behavior of ACF: Eq 8.49 (homogeneous difference eq on Ryy). For different shifts t -> linear system of equations for a_i and beta0 (Eq 8.50, Yule-Walker-type). beta0 = measure of mean-square model error (Eq 8.51) with e(k) model prediction error of y(k) (Eq 8.38 ref [OCR ref inconsistent]).
- To solve (8.50): estimate ACF values Ryy(t), t = 0..2m from data y(k), k = 0..N-1 (Eq 8.52).
- BURG algorithm recommended for efficient solution [8.41],[8.6]: interpret model (8.49) as predictor filter for unknown Ryy(t); start order mu = 1, alternately estimate coefficients and ACF values up to final order 2m.
- Eigenfreqs of discrete components: POLE DECOMPOSITION of denominator polynomial of AR model (Eq 8.53: A(z) = prod(1 - z_i z^-1)... or factorization into real quadratic parts) — or search maxima of |1/A*(z)|. Conjugate-complex poles z_i1, z_i2 -> factorization into square parts; z-transform table [8.16] gives angular frequency w_i of each sinusoidal partial oscillation (Eq 8.54-ish): w_i from argument of complex pole. All significant partial oscillation freqs of y(t) computable this way.

#### 8.1.6 c) Estimation of the amplitudes (L3254-3288)
- Amplitudes from AR model alone: only INACCURATE — y0i from (8.42) evaluated at pole z_i (Eq 8.55), with A(z_i)=A*(z_i); depend on denominator coeffs a_i AND numerator const beta0; slightest coefficient errors -> large amplitude variations.
- Hence SECOND estimation level dedicated to amplitudes [8.33],[8.31]: for periodic oscillations ACF = sum of cosines w/ damping envelopes (Eq 8.57); damping term negligible for small damping (condition Eq 8.58: d_i * t << 1 type) without hurting accuracy -> with known w_i (level 1) get linear system for ACF amplitudes R-theta_i (Eq 8.59: matrix of cos(w_i * t_l)); signal amplitudes recovered from ACF amplitudes via relation (Eq 8.60, half-amplitude type [formula missing]) by inverting NON-SINGULAR matrix (8.59).
- Result: parametric PSD model Syy(w): AR model = set of (freq, amplitude) pairs of significant sinusoids. User must supply only: sampling time Ts, data set length N, order m (number of expected significant partial oscillations).
- Fig 8.10 WORKED APPLICATION: amplitude spectrum y0i of the motor CURRENT of an asynchronous motor driving a hacksawing machine, nine frequencies; worn-out saw blade -> HIGHER frequencies in motor current; settings m = 0(?), N = 100 [OCR: "m = 0, N = 100" — likely m = 9 (nine freqs) with 0 as OCR artifact [OCR?]]. Intact vs worn blade compared. More examples [8.32]; grinding-machine applications [8.21],[8.22],[8.18].
- Advantage vs FFT: directly estimates few (e.g. 5) distinct frequencies + amplitudes precisely, instead of smearing many amplitudes over freq range -> advantageous for FD based on periodic signals.

#### 8.1.7 Cepstrum analysis (L3290-3303...)
- Use case: detecting harmonic signals with SMALL amplitudes riding among harmonics with larger amplitudes.
- Definition (power cepstrum, one of several definitions [8.43]): inverse Fourier transform of the LOGARITHM of the power spectrum of y(t) (Eq 8.61).

#### 8.1.7 Cepstrum (cont., L3304-3322)
- Power spectrum from Fourier series coeffs c_n at discrete freqs v*omega0 (Eq 8.62-8.63), period T0 (e.g. T0 = 1/f0): discrete amplitude spectrum [amplitude] + phase spectrum; power of each harmonic = square of Fourier-coefficient amplitude (Eq 8.64) -> dimension [(amplitude)^2]. Evaluate Eq 8.61 by sampling P(w).
- COMPLEX cepstrum (Eq 8.65): inverse FT of ln y(iw) (complex log incl. phase) — contains phase info, can invert back to time domain; more powerful but harder; applications: echo removal, speech synthesis.
- Etymology/history: cepstrum = "spectrum of a logarithmic spectrum" [8.3], better than ACF for detecting ECHOES in seismic signals; word = spectrum with letters swapped. Kin terms: quefrency (from frequency), saphe (from phase). Cepstrum C(quefrency) is function of quefrency t with dimension [s].
- Side note (Eq 8.66): ACF of stationary stochastic signal = inverse FT of power spectral density S'yy(iw) (cf. Eq 6.21) — FFT analyzers compute spectrum first, then inverse FFT for ACF instead of time-domain operation.
- WHY cepstrum beats ACF for this job: log power spectrum amplifies small peaks (log attenuates big values relative to small), so harmonic families with SMALL amplitudes appear that linear-scale spectrum hides => cepstrum shows harmonic periods in [s] for small amplitudes; example: ball bearing fault [8.43]. Suitable for periodic effects in log spectrum: HARMONIC FAMILIES, SIDEBANDS, ECHOES. Used in speech analysis, seismic analysis, machine fault detection [8.25].

### 8.2 Analysis of non-stationary periodic signals (L3324-3374)
- Signals whose freq content changes over time must NOT be Fourier-analyzed conventionally -> only time-averaged results not tied to time instants. Two tools: STFT, wavelet transform.

#### 8.2.1 Short-time Fourier transform (L3328-3334)
- STFT (Eq 8.67 [formula missing]): window f(t - tau) around time of interest tau; measures similarity of y(t) vs f(t-tau)*exp(i*w*t); window is short-time; sweep tau -> how freq content evolves.
- Window length choice = compromise between time resolution Dt and spectrum resolution Dw (uncertainty condition [8.42]). Small Dw (fine freq resolution) => LONG window.

#### 8.2.2 Wavelet transform (L3336-3374)
- Prototype/basis functions with damped oscillatory behavior of finite duration = wavelets, from mother-wavelet W(t) [8.42],[8.2],[8.52]. Fig 8.11 mothers: (a) Haar; (b) Daubechies 2nd order [OCR "Daubechie"]; (c) Mexican hat.
- Scaled/shifted wavelets (Eq 8.68): W((t-tau)/a)/sqrt(a); 1/sqrt(a) keeps power-density scaling correct; mean freq w0 of mother -> scaled mean freq w0/a. Scaling a = dilatation, tau = translation.
- CWT (continuous wavelet transform, Eq 8.69): real-valued for real y and wavelet (vs STFT usually complex).
- Example wavelets (as printed):
  - 1) Morlet wavelet W(t) = ... [OCR garbled "Ps oe ie eon foit"; standard Morlet is exp(-t^2/2)*exp(i*w0*t) — DO NOT quote from this OCR]
  - 2) Mexican-hat W(t) = (1 - 2t^2) * exp(-t^2/2) [as printed "(1-2?) et /?" [OCR? — verify]]
  - 3) One-cycle-sine wavelet (Eq after, formula missing).
- Wavelet advantage: signal-adapted basis fn, better simultaneous time+freq resolution. Wavelet fns act as bandpass filters: reducing mean freq via a also reduces BANDWIDTH — vs STFT constant bandwidth [8.50].
- Example 8.3 (worked, qualitative numbers): periodic signal with changing frequency (overlap note truncated by OCR, Eq 8.7x missing); Mexican-hat wavelet used [8.50]. Fig 8.12: (a) signal; (b) scaled/shifted Mexican hats for a = 9 and a = 25 [OCR "fora = 9 anda = 25"]; (c) scalogram W(a,tau) for a = 1...41 and tau = 0...1000 (bright = large amplitude); (d) wavelet coefficient Y(a,tau) vs time for a = 25; (e) same for a = 9. Maxima of Y(a,tau) (marked square & circle) = best agreement signal/wavelet => changed frequencies detected directly from CWT maxima.
- DETECTION RULE: sudden changes in amplitude/frequency of periodic signals detected when CWT exceeds thresholds. Application: MISFIRE detection in 6-cyl gasoline engine via exhaust-gas pressure + wavelet analysis [8.50].

### 8.3 Analysis of stochastic signals (uses signal models of Sec 6.2)
#### 8.3.1 Correlation analysis (L3380-3404)
- Sampled ACF estimator (Eq 8.70) [formula missing: (1/N) sum y(k)y(k+|tau|) type]; if mean known use auto-COVARIANCE (Eq 8.71). Assume y-bar = 0.
- BIAS caveat: finite N gives only N-|tau| products in (8.70) -> bias b (Eq 8.72) that vanishes as N -> inf (consistent estimate). Alternative normalizing by N-|tau| removes bias but INCREASES variance [8.17] -> prefer (8.70) with N >> |tau|.
- Real-time on-line use: recursive correlation estimator (Eq 8.73-8.74, exponential-forgetting recursion type [formulas missing]).

#### 8.3.2 Spectrum analysis (L3406-3416)
- PSD = FT of auto-covariance fn: apply Sec 8.1.4 results to Ryy(t) instead of y(t). Two-sided discrete FT (Eq 8.75, cf 6.21); since Ryy(t) symmetric for large N, one-sided cosine-type transform (Eq 8.76) also usable -> then FFT applies directly. (Periodogram route: ACF first, then FFT.)

#### 8.3.3 Signal parameter estimation with ARMA models (L3418-3444)
- ARMA model (6.30): params c_i (AR side) and d_i (MA side) to estimate [note: this book's ARMA notation uses c,d; white-noise input u(k)]. If AR order p known, rewrite model in regression form (Eq 8.77-8.78).
- u(k) = equation error, statistically independent by definition = white noise. If past noise values u(k-1)...u(k-p) were known, plain RLS works (Sec 8.1 ref likely wrong, should be Ch10 estimation; treat ref as given).
- Practical: past y known; assume estimates of past u (printed as v/o symbols) and theta(k-1) available -> predict current y(k) via (8.76) and get current equation error -> iterate recursive LS (Eq 8.79-8.81). Extended/self-iterating LS on ARMA. Works for stationary signals + special types of non-stationary ones. Details [8.19].

#### Ch8 wrap-up before machine section (L3446)
- Summary of signal-model FD chain: generate features from measured signal -> compare observed vs normal features (Fig 8.1) -> differences exceeding thresholds = SYMPTOMS -> detection of threshold exceedance done with limit checking + change detection methods of CHAPTER 7. This is the join point between Ch7 statistics and Ch8 signal features.

### 8.4 Vibration analysis of machines
#### 8.4.1 Vibrations of rotating machines (L3448-3478)
- Drive trains: motors, clutches, gears, shafts, belts/chains, ball/rolling + oil bearings. Vibration sources (bullet list as printed):
  - inherent machine oscillations (piston-crankshaft, toothed machine-tool cutting, axial piston pumps, induction motors)
  - shaft oscillations w/ radial or axial displacement
  - irregular shaft speed (Cardan [OCR "Kardan"] joint, eccentric gears)
  - torsional shaft oscillation
  - impulsewise excitation (backlash, cracks, pittings, broken gear teeth)
- Some vibrations = NORMAL state; CHANGES + additional appearances = fault-caused -> vibration analysis well-established for machine monitoring [8.43],[8.54],[8.53],[8.25],[8.13].
- Measurement: acceleration a(t) via lateral accelerometers in 1/2/3 orthogonal dirs (horizontal, vertical, axial) on the casing -> machine TRANSFER behavior Gm(iw) between source & sensor, contains one or several structural resonances w_0i, zeta_i (mass-spring-damper systems).
- Accelerometer principles: piezoelectric (force measurement) or inductive (seismic-mass displacement). HIGH-PASS after accelerometer to damp low-freq disturbance, cutoff e.g. 100-200 Hz.
- Alt measurands: velocity v(t), displacement d(t). For sinusoidal displacement (Eq 8.82): v, a related by w and w^2 factors (Eq 8.83-8.84) => acceleration measurement represents HIGH-freq components best and needs no non-oscillating reference (v,d do) BUT amplifies HF noise (SNR penalty) -> low-pass filter for very high freqs (Fig 8.13). Analyzed signal generically y(t) = a/v/d.

#### 8.4.2 Vibration signal models (L3480-3535)
- Faults generate ADDITIONAL STATIONARY HARMONIC or PULSEWISE signals. Harmonic causes (linear superposition): unbalance, misalignment/centering error, deformed shafts, tooth faults, ball-bearing faults, electrical flux differences in motors, changed periodic operation. Additive vibration model (Eq 8.85-8.86 [formula missing]).
- TYPICAL MACHINE FREQUENCIES (key table as bullets):
  - w_s = basic rotational shaft angular frequency
  - w_z = tooth contact frequency = z * w_s (z = number of teeth)
  - w_or = outer-race frequency (rolling over uneven point of outer ring)
  - w_ir = inner-race frequency
  - w_c = cage frequency
  - w_b = roller/ball spin frequency [OCR "@ roller or ball spin"]
- Bearing freqs computable from GEOMETRY assuming NO slip [8.53],[8.13],[8.9]; change under significant thrust loads / internal preloads (different contact angles + slip) [8.54].
- Additional (nonlinear) frequencies: nonlinear characteristics, backlash, mechanical looseness (foundation cracks, broken mountings), hysteresis from dry friction / stick-slip (cf. Sec 6.1).
- AMPLITUDE MODULATION worked model (Fig 8.14): one gear in pair not centered, eccentricity e; non-centered gear rotates w_s (rotation freq), has z = 22 teeth [printed "22", also "2"/"22" OCR noise; example uses 22] -> tooth-contact impacts = 22 per rev -> carrier w_z = 22*w_s (amplitude y0z); contact force oscillates as gear nears/farthers => modulation frequency = w_s (modulation amplitude x0s). Resulting signal (Eq 8.87): SPECTRUM = carrier w_z PLUS SIDEBANDS (w_z - w_s) and (w_z + w_s); the modulation freq w_s itself does NOT appear in spectrum (ideal AM fact).
- FREQUENCY modulation also from eccentric gear (effective radius varies) -> w_z oscillates (Eq 8.88) -> SAME sideband frequencies as AM [8.10]. Similar sidebands at rolling-element bearings and electrical motor-bar defects.
- PERIODIC IMPULSES (ball/roller bearing defects): impact each time ball hits raceway defect or defective ball hits raceway -> excites short transient at STRUCTURAL natural freqs (rigid-body modes) (Fig 8.15a). One dominant mass-spring-damper w_0e: each impact -> damped impulse response of displacement d(t) (Eq 8.89), decay const sigma [OCR "5"], repeating with period T_imp, impact angular freq w_imp = 2*pi/T_imp (Eq 8.90-8.91); Fourier transform of repeated damped response is PERIODIC in freq (Eq 8.92, sampled-data-like) -> spectrum peaks at v * w_imp (harmonics of impact freq).
- Superposition caveat: several bearings/gears -> many distinct freqs + sidebands via linear+nonlinear superposition -> spectra get complex, isolation/diagnosis not straightforward.
- Fig 8.15b: envelopes |x-(t)| of x(t) after low-pass filtering + rectification (basis of envelope analysis).

#### 8.4.3 Vibration analysis methods (L3537-3579)
- Goal: features from x(t) or x(k*Ts); sampling: Shannon w_s > 2*w_max (w_max = highest frequency of INTEREST); anti-alias low-pass with cutoff w_c = w_s/2 > w_max (printed "woy; = @p/2 > Wmax"). Methods grouped: time domain / frequency domain / time+frequency (Fig 8.13).
- a) TIME DOMAIN:
  - ACF/autocovariance (Eq 8.9) separates vibration signal from noise; vibration shows as periodic Ryy(t + v*T_per) for harmonics; visual interpretation only for few harmonics -> better use ACF as PREPROCESSING for frequency methods.
  - CREST FACTOR (Eq after "crest factor is defined as" — formula missing; standard: peak/RMS) and KURTOSIS FACTOR (formula missing; standard: 4th moment / RMS^4) on x(k): weight peaks & outliers strongly vs normal components -> detect changes/abnormalities. [OCR: definitions not decoded; standard formulas exist but not transcribed here.]
  - Power cepstrum (8.61): FT-backtransformation of log power spectrum w -> quefrency [s]; for small-amplitude harmonics among dominating ones (ball bearing faults) [8.43],[8.25]; defect impulses appear as distinct peaks at distance of ONE ROTATION TIME.
- b) FREQUENCY DOMAIN:
  - Fourier/FFT of stationary harmonic signals: peaks intuitive; compare vs EXPECTED freqs (bearing/gear formulas above) to isolate faults. CAUTION: observed freqs not always uniquely tied to one fault [8.53].
  - Maximum entropy spectral estimation (8.1.6): recommended for AUTO finding few (2 to 5) distinct freqs at cost of computation; good results grinding machine [8.20], hacksawing machine [8.31].
  - ENVELOPE ANALYSIS for damped impulse responses (bearings/gears): suppress structural eigenfreqs w_0e by low/band-pass filter INCLUDING them [OCR wording: filter includes the eigenfreqs — intent: band selected around resonance], take magnitude |x-(t)| (rectified envelope, Fig 8.15b), then FFT (Eq 8.93-ish) -> impact freq w_imp + harmonics much clearer than FFT of raw signal (where masked by machine-mode contributions).
- c) TIME-FREQUENCY:
  - Preprocess in time domain to raise SNR or emphasize freq ranges: ACF for noise removal; cross-correlation when relation to another signal's freq matters; then FFT of result.
  - Non-stationary periodic signals: STFT or wavelet (Sec 8.2).
  - Rotor systems: identify fault models w/ equivalent forces + optimal sensor placement for position/accel -> lab tests showed imbalances AND larger axle cracks (rents [OCR "rents" = Risse]) detectable [8.39],[8.38].
- Design caution: filter design, Ts, record length, method choice + combination, and instrumentation all need good knowledge of the individual machine; method comparison [8.9] -> results relatively similar, practical recommendations given.

#### 8.4.4 Speed signal analysis of combustion engines (L3581-3643; footnote: section compiled by Frank Kimmich)
- Motivation/legal: OBD II introduced by California Air Resources Board (CARB) 1996; EOBD by EU 1998 -> supervision of all emission-relevant components. Stats [8.30]: most emission/performance increases caused by faults in INJECTION or MIXTURE preparation.
- Misfire hazard chain: no/incomplete combustion -> unburned fuel enters exhaust -> burns in hot catalytic converter -> thermal overload can destroy cat. If misfire RATIO exceeded -> cut fuel to misfiring cylinders (cat protection + emissions). Detection route: engine speed signal at FLYWHEEL.
- Signal structure: combustion batch behavior vs crank angle (CA). Four-stroke: each cylinder fires every 720°CA = engine base period; all spectral components are multiples of base freq. Four-cyl: one combustion every 180°CA. Speed oscillation freq at flywheel = ignition frequency f_I (Eq 8.94 relates f_I to engine speed omega_e [formula missing]).
- Fig 8.16 (numbers): SI engine at idle, NO misfires: speed oscillations at ignition freq around mean speed approx. 800 rpm.
- Fig 8.17: four-cyl, CONTINUOUS MISFIRE cylinder 1 -> significant speed drop + additional LOW-frequency oscillations (visible on low-pass filtered speed); components = harmonics of engine base freq; different cylinders -> different frequency patterns.
- Fig 8.18 (FT of both signals): no-misfire -> only the FOURTH engine harmonic (firing every 180°CA = 4th harmonic of base) in spectrum; misfire -> extra components; evaluating them detects AND LOCALIZES the misfiring cylinder. FFT-based evaluation literature [8.44].
- DFT real/imag method [8.11] (numbers): four-stroke four-cyl; successfully implemented on six-cyl SI engine up to 6000 rpm, loads > 20%. Engine is TIME-VARIANT -> data acquisition crank-angle synchronous (no sampling-time adaptation). Sample every 90°CA = double ignition frequency (satisfies Shannon). 8 sampling points per combustion cycle (720/90) -> tiny N -> easy real-time. Speed-dependent Ts follows from ignition freq (uncaptured eq). Amplitude + phase from DFT real/imag parts (Eq formulas missing); m [OCR "11"] = harmonic order. Non-cyclic combustion variations -> average over several working cycles.
- FAULT PATTERN TAXONOMY (six patterns for relative position of faulty cylinders):
  - P0: no fault
  - P1: one cylinder oversupplies
  - P2: one cylinder undersupplies
  - P3: two subsequent (adjacent) cylinders undersupply
  - P4: two opposite cylinders undersupply
  - PX: undetectable
- Diagnosis scheme (Fig 8.19): evaluate ONLY 1st and 2nd engine harmonics (m = 1, 2); Re/Im components at those freqs ~ 0 for no misfire, != 0 for misfire; compare amplitudes + Re/Im vs TWO speed- and load-dependent thresholds T1, T2; resulting vector pattern identifies defective cylinder(s) -> PATTERN RECOGNITION on DFT amplitudes+phases.
- Limits: acquisition errors, overlaid disturbances; usable for misfire + smooth-running monitoring over whole operating map EXCEPT too-low loads and high speeds; similar approach on exhaust-gas pressure by [8.51].

### 8.5 Problems (L3645-3655) — exam items with numbers
- 1) Three typical signal-model FD tasks: machine tools / turbo engines / car suspensions — measurements + analysis methods.
- 2) Strong steering-wheel vibration around 80 km/h — candidate fault + measurements. (OCR printed out of numeric order 3 before 2.)
- 3) Truck seat accelerometer: which signal-analysis methods locate sources of fluctuations.
- 4) Advantage FFT vs DFT.
- 5) Wavelet vs STFT advantages.
- 6) Lowest frequency of speed signal of 6-cyl four-stroke engine with one misfiring cylinder at n = 3000 rpm.
- 7) Features from stochastic-signal FD: correlation analysis + ARMA parameter estimation.
- 8) Rotating machine basic displacement vibration f = 5 Hz, amplitude 2 mm -> compute v(t), a(t) (apply w and w^2 scaling of Eq 8.83-84: v0 = w*d0, a0 = w^2*d0).
- 9) Gear pair 20 & 50 teeth, 20-tooth wheel at n = 3000 rpm: tooth contact freq f_z and omega_z; frequencies if SMALLER wheel not centered (sidebands f_z -/+ f_rotation); detection methods from casing acceleration.

### Boundary note
- L3657 "## Fault detection with process-identification methods" + intro (3659-3669) and the upside-down rotated Table 9.1 (3671-3687, fully mirrored OCR gibberish — do NOT attempt to read) + Fig 9.1 belong to CHAPTER 9 (9.1 starts L3692). Not part of Ch8 distillation.
- Ch9 intro gist (one line, for continuity): identification precedes model-based FD when models unknown/imprecise; correlation methods -> impulse-response features; parametric estimation -> up to ~6 parameters from one SISO I/O pair; step/frequency-response matching only for special cases.

### Cross-cutting cautions collected in Ch8
- Nearly all equations are `<!-- formula-not-decoded -->` — feature extraction described by role + equation numbers only; verify any formula against the book before use.
- FFT: leakage from rectangular window; windowing trades leakage vs resolution; N=2^p requirement forces zero-padding (data corruption).
- Cepstrum: use log spectrum to expose small-amplitude harmonic families/sidebands/echoes (bearing faults); peaks at quefrency = rotation period.
- Sideband logic: AM and FM both produce w_carrier +/- w_modulation; modulation frequency itself absent from ideal AM spectrum.
- Bearing/gear frequencies from geometry assume NO slip; thrust loads/preloads shift them.
- Frequency peaks are NOT unique fault signatures [8.53]; combine time/freq/envelope methods + machine-specific design of filters, sampling, record length.
- Detection = compare feature vs normal feature + threshold; hand off to Ch7 limit checking / change detection.

## Isermann Ch9 — Parameter-Estimation-Based Fault Detection Applications

Ch9 = toolbox chapter: identification/estimation methods that Ch4-5 symptom generation builds on. Heavy formula OCR loss (almost every formula is `<!-- formula-not-decoded -->`); recursions below given in standard textbook form, labeled [reconstructed].

### 9.1 Identification with correlation functions
- Setting: stationary stochastic signals, linear process, OPEN loop. Impulse response g(v) recoverable from input ACF + input-output CCF alone.
- 9.1.1 ACF/CCF estimators: finite-sample sums over N points; recursive CCF update by subtracting the N vs N-1 equations [reconstructed: φ_yu^N(τ) = φ_yu^(N-1)(τ) + (1/N)[y(k)u(k-τ) − φ^(N-1)(τ)]]. Bias present at finite N but vanishes as N→∞; variance also →0 ⇒ **consistent in mean square** (ref [9.30]).
- 9.1.2 Convolution link (zero-mean signals): φ_yu(τ) = Σ_v g(v) φ_uu(τ−v) [reconstructed]. Truncate g at l+1 taps, stack τ = 0..l → linear system Φ_uu · ĝ = φ_yu; deconvolution ĝ = Φ_uu⁻¹ φ_yu.
- Identifiability condition: Φ_uu invertible ⇒ input must be **persistently exciting of order l+1** (process stable too).
- Special case: white-noise input, φ_uu = σ_u² δ(τ) ⇒ g(τ) = φ_yu(τ)/σ_u² — impulse response ∝ CCF.
- Consistency conditions with output noise n(k): n,y stationary; E{u}=0; u persistently exciting; n uncorrelated with u. (Refs [9.12],[9.30].)

### 9.2 Parameter estimation for linear processes
- Process model: ARX difference eq y(k) + a₁y(k−1)+...+a_n y(k−n) = b₁u(k−d)+...+b_{m+1}u(k−d−m) [reconstructed, standard ARX]; u,y are deviations from operating point (u₀,y₀); To sampling time; d = τ₀/To discrete dead time. Transfer function H(z) = B(z⁻¹)/A(z⁻¹) with dead-time factor z⁻ᵈ. Measured ỹ = y + n (stationary stochastic disturbance). Task: get a_i, b_i from N I/O samples (Fig 9.2).

#### 9.2.1a Equation-error (prediction-error) LS
- Model written with equation error e(k): ỹ(k) = −Σa_i ỹ(k−i) + Σb_i u(k−d−i+1) + e(k); e linear in parameters ⇒ "linear-in-the-parameters" structure (Fig 9.2a).
- One-step-ahead predictor ŷ(k|k−1) = ψᵀ(k)θ with data/regression vector ψᵀ(k) = [−ỹ(k−1) ... −ỹ(k−n), u(k−d) ... u(k−d−m)] and θᵀ = [a₁..a_n, b₁..b_{m+1}] [reconstructed].
- Batch form: e = ỹ − Wθ, W = (N+1)×2ℓ data matrix; minimize V = eᵀe ⇒ **θ̂_LS = (WᵀW)⁻¹Wᵀỹ** [reconstructed, eq 9.22-ish]. Inverse exists iff WᵀW positive definite ⇔ persistent excitation + stability (loss minimum too).
- Bias analysis: bias b = E{θ̂} − θ₀ nonzero in general; substituting gives b ∝ E{(WᵀW)⁻¹Wᵀe}. Unbiased iff W and e uncorrelated, E{e(k)}=0. That holds if disturbance generated by disturbance filter H_d(q)·v(k), v = white noise (Fig 9.3) — filter not known in practice ⇒ **LS usually biased**. Bias grows with noise-to-output variance ratio σ_e²/σ_y².
- Covariance: if θ̂ unbiased, E{(θ̂−θ₀)(θ̂−θ₀)ᵀ} = σ_e²(WᵀW)⁻¹ [reconstructed, eq 9.32]; σ_e² = var of e(k); WᵀW elements are correlation functions; E{P} ∝ covariance matrix of parameter errors — key hook for confidence-intual testing later.
- Verdict: LS ok only for small/no disturbance; big plus = one batch calculation, no iteration (linear in params).

#### 9.2.1b Output-error methods
- Error defined as output error e′ = y_model_true_input − model output (Fig 9.2b); e′ **nonlinear** in params ⇒ numerical optimization of loss (e.g., downhill simplex). Higher compute, generally no online real-time; but comparatively accurate estimates [9.10],[9.50].

#### 9.2.1c Recursive least squares (RLS) — the workhorse for diagnosis
- Derivation: subtract nonrecursive LS equations for θ̂(k+1) vs θ̂(k) ⇒
  [reconstructed standard RLS:]
  - gain:        k_g(k) = P(k−1)ψ(k) / [λ + ψᵀ(k)P(k−1)ψ(k)]
  - update:      θ̂(k) = θ̂(k−1) + k_g(k)[ỹ(k) − ψᵀ(k)θ̂(k−1)]
  - covariance:  P(k) = [P(k−1) − k_g ψᵀ P(k−1)]/λ
- Correction vector = prediction residual times gain; start: θ̂(0) from prior guess or zeros, **P(0) = w·I with w = 100...1000** (large).
- E{P} ∝ covariance of parameter estimates: diag(P) gives **variances (standard deviations σ_θi = √P_ii) available online** — directly usable for parameter-deviation tests (±2σ, ±3σ confidence intervals, eq 9.38 relation).
- Numerical problems of basic RLS → modified versions (Sec. 9.2.3).

#### DC value estimation (u∞, y∞ handling)
Measured absolute signals contain unknown steady offsets; u,y in the model are deviations. Options:
- **Differencing**: use Δu(k)=u(k)−u(k−1), Δy likewise; equivalent to high-pass (1−z⁻¹) applied to both I/O ⇒ parameters estimable unchanged, just replace u,y by Δu,Δy in the algorithm. Simplest; no explicit DC values.
- **Averaging**: U∞ ≈ (1/N)ΣY(k); recursive: Û∞(k) = (1−1/k)Û∞(k−1) + Y(k)/k [reconstructed]; for slowly varying DC use exponential forgetting Û∞(k) = λÛ∞(k−1) + (1−λ)Y(k), λ<1.
- **Implicit constant**: substitute deviation defs into ARX ⇒ extra parameter C (lumped DC offset) in model Y(k)=...+C; extend θ̂ by C and regression vector by 1 → estimate DC from within RLS; given one DC the other follows from the algebraic relation (eq 9.51, OCR-failed). Convenient for closed-loop ID.
- (Explicit estimation of a constant: next block.)

#### DC values (cont.) — Explicit estimation of a constant
- Two-stage: first dynamic params via differencing, then constant C by LS on the mean equation; for large N, Ĉ ≈ Ȳ − (1−Σa_i)⁻¹(Σb_i)Ū-type relation [reconstructed; eq 9.56 OCR-failed]. If Y∞ of interest and U∞ known, back out Y∞ from Ĉ. One-way coupling: θ̂ does not depend on C. Downside: differencing worsens noise/signal ratio. Choice depends on application.

### 9.2.2 Extended least squares (ELS)
- Motivation: LS assumes uncorrelated e; for **correlated** equation error use ARMAX: A(z⁻¹)y(k) = B(z⁻¹)u(k) + D(z⁻¹)e(k), with e(k)=D(z⁻¹)·white [9.61],[9.47].
- Extended regression vector ψ̄ᵀ includes past outputs, inputs AND past equation errors ê(k−i); extended parameter row includes d_i [reconstructed]. RLS recursions identical in form to (9.39)-(9.40) with ψ̄.
- Past errors ê are regenerated recursively ⇒ requires roots of D(z)=0 inside unit circle (stability of noise model).
- Unbiased & consistent in mean square if LS convergence conditions transfer to model eq, plus positive-realness condition on A/D − ½I [reconstructed] (strictly positive real).
- Alternatives noted: instrumental variables, maximum likelihood [9.12],[9.37],[9.62],[9.30].

### 9.2.3 Modifications of basic recursive estimators
- Purpose: numerical robustness for short word length (8/16-bit µC) AND for **small input changes as in adaptive control or fault detection** — both produce ill-conditioned normal equations. Fix: never form P with squared signals; work with square-root/factorization forms, starting from P (covariance form) or P⁻¹ (information form) [9.33],[9.6],[9.34]; treatment follows [9.31].
- a) **DSFC (discrete square-root filter, covariance form)**: P = S·Sᵀ (S Cholesky factor); RLS rewritten on S; start S(0)=√w·I, θ̂(0)=0; drawback: n square-roots per step.
- **U-D factorization (Joseph/Bierman, [9.6])**: P = U·D·Uᵀ, U unit upper triangular, D diagonal; recursions for U,D (eqs 9.67-9.74 OCR-failed); no square-root routines, cost comparable to plain RLS; numerical properties ≈ DSFC but U,D elements may grow larger than S's.
- Invariance-property fast algorithms [9.36]: save compute only for order n>5, cost = more memory + more sensitivity to starting values.
- b) **DSFI (information form)**: P⁻¹ = RᵀR (R upper triangular, R=S⁻¹); θ̂ by backsubstitution of Rθ = b from QR factorization Q·W = [R;b] of the data matrix; Q orthonormal preserves norms ⇒ solving normal equations directly bounds parameter error by cond(W)·(measurement error), orthogonal form bounds it by cond(R)-type with cond much smaller ⇒ **far less sensitive to measurement errors** [9.15].
- Batch: Householder transforms on (W,y). Recursive DSFI: append one row per step; R(k+1), b(k+1) updated via **Givens rotations** zeroing m'_{i+1,i}; rotation params c= m11/√(m11²+m21²), s= m21/√(...) [reconstructed]; product of Givens = Q(k). Advantages: **no starting values needed, R(0)=0**; good when θ̂ not needed every sample. Fast Givens / recursive Gram-Schmidt variants avoid square roots but elements may grow. No essential numerical difference DSFC vs DSFI.

### 9.2.4 Parameter estimation of time-varying processes
- Motivation: parameters drift with operating point (linearization changes); if nonlinearity mild + operating point changes slowly → linear difference eq with **time-varying parameters** works. Treatment for RLS.
- a) **Exponential weighting / constant forgetting**: weighted LS cost V = Σ λ^(k−i) e²(i) [reconstructed]; recursion gets P(k) = [P(k−1) − kg·ψᵀP]/λ form; λ<1 ⇒ inflate covariance each step ⇒ old data forgotten, new data keeps constant weight.
- Memory length **M = 1/(1−λ)** (effective averaging horizon).
- Table 9.2 (weights at N′=50, λ=0.99): 10→0.67? garbled [OCR?] — clean values: λ=0.99: k-offsets 20/30/40/47/48/49/50 → 0.82/0.90/0.97/0.98/0.99/1; λ=0.95: 10→0.60, 40→0.90? garbled row [OCR?] — gist: weights grow exponentially to 1 at N′.
- λ=1 with large k: P⁻¹ elements → ∞ ⇒ new measurements ignored (estimator "freezes", dead to parameter changes). λ<1 ⇒ P⁻¹ converges (convergent geometric series Σλ^i), P stays finite nonzero ⇒ estimator **remains sensitive to parameter changes** forever. Cost: smaller effective averaging ⇒ noise influence up, parameter variances up.
- λ selection rule of thumb:
  - λ small (≈0.90) if parameter changes fast — only then small noise allowed;
  - λ large (≈0.98) if parameter changes slow — tolerates larger noise.
- ML/ELS slow initial convergence → use smaller weights (smaller λ) at start.
- **Failure mode (critical for FDI)**: λ<1 + poor input excitation ⇒ wᵀ(k)→0, P⁻¹ decays, P blows up ⇒ correcting vector gain explodes; tiny disturbance/numerical error triggers wild parameter jumps → estimator unstable (observed in adaptive control). Countermeasures: **monitor input excitation** or use time-varying λ. Same warning applies to fault-detection operation where u is nearly constant.

### 9.2.5 Parameter estimation for continuous-time signals
- Motivation explicitly includes **fault diagnosis** and theoretical-model validation: need ct-domain (s) models, not just z.
- Model: y⁽ⁿ⁾ + a₁y⁽ⁿ⁻¹⁾ + ... + aₙy = b₀u⁽ᵐ⁾ + ... + bₘu [reconstructed]; derivatives of measured u,y must exist; ỹ = y + n.
- Sample at kTo, **generate derivatives numerically**, stack N+1 equations → same LS machinery: θ̂ = (WᵀW)⁻¹Wᵀỹ; WᵀW/(NT₀) elements = correlation functions of signal derivatives at zero shift ⇒ almost all discrete-time results (RLS, square-root forms, forgetting) transfer.
- Convergence result: ct LS estimates biased in general even if e statistically independent (disturbed processes).
- Derivative problem is the crux: plain numerical differentiation (splines/Newton) **cannot suppress noise**. Working solutions:
  - **State variable filter (SVF)** (Fig 9.4): low-pass filter whose states ARE the filtered derivatives; damped low-pass, parameters f_i free; **Butterworth design recommended** [9.48];
  - FIR approach: convolve signal with derivatives of a low-pass impulse response [9.46],[9.59],[9.60].
- Good results for large signal/noise; for large disturbance use consistent methods (instrumental variables).

### 9.2.6 Parameter estimation in closed loop
- Problem: feedback correlates u with noise ⇒ correlation methods fail without external excitation. But LS/RLS only need e(k) uncorrelated with data vector ψᵀ(k) ⇒ less restrictive. Details [9.31],[9.17]. Fig 9.5: closed loop with optional perturbation signal ws.
- a) **No external excitation** (loop driven only by n(k), r=0): direct LS on u,y works iff u(k−d−1) not linearly dependent on other ψ elements ⇒ identifiability: **controller order must be high enough**: need p ≥ n_p or v ≥ n_g − d (garbled [OCR?] but gist: with n_p=3,n_g=3,d=0 → controller order ≥3; d=1 → =3 or >2). If satisfied, one-step-ahead LS/ELS applies directly.
- b) **With external perturbation w(k)/r(k) sufficiently exciting**: u no longer dependent on ψ ⇒ identify exactly as open loop, but process model orders must be known a priori.

### 9.3 Identification of nonlinear processes
- Motivating examples (also the diagnosis targets later): **vehicles, aircraft, combustion engines, thermal plants, all processes with Coulomb friction and magnetic hysteresis**.
- Two families: classical polynomial models; ANN-derived architectures. Non-continuously differentiable case handled last (9.3.5).

#### 9.3.1 Nonlinear static processes (polynomial characteristic)
- Static model: y(k) = c₀ + c₁u + c₂u² + ... + c_p uᵖ (Fig 9.6), ỹ = y + n. Regression vector = [1, u, u²,...] ⇒ still **linear in parameters** ⇒ θ̂ = (UᵀU)⁻¹UᵀY batch; exists iff input U(k) actually changes (persistent variation). E{n}=0 ⇒ consistent in mean square [9.30].
- **Fault-detection hook (verbatim gist)**: "For fault detection one directly compares the estimated parameters c_i or the nonlinear characteristic curves, e.g. for pumps." — pump curves as diagnosis signature.

#### 9.3.2 Classical nonlinear (dynamic) models
- Polynomial approximators two classes: general (**Volterra series, Kolmogorov-Gabor polynomials**) vs structured (**Hammerstein, Wiener, nonlinear difference equation (NDE)** models) [9.12],[9.18],[9.30],[9.31]. Shift-operator form q^{-i}y(k)=y(k−i).
- Named forms (formulas OCR-failed, standard shapes): generalized Hammerstein (static poly → LTI), parametric Volterra, nonlinear NARX-type model [9.35].
- Key point: with **equation-error** formulation these stay linear in parameters ⇒ LS/RLS/RELS apply directly, avoiding expensive iterative optimization — the big computational win.

#### 9.3.3 Artificial neural networks for identification
- Why: no a priori process structure needed, widely applicable; ANN training = system-identification problem (supervised learning); universal approximation of nonlinear maps; static first, then dynamic [9.19],[9.51],[9.2],[9.44],[9.32].
- Neuron model (Fig 9.8): input operator = similarity measure: scalar product x = wᵀu (large = similar) OR Euclidean distance x = ||u − c|| (small = similar); activation y = φ(x − Θ), Θ threshold shift (Fig 9.9).
- Structure (Fig 9.10): input layer (scaling only, not counted) + hidden layers + output layer; link types feedforward/backward/lateral/recurrent; continuous-valued signals for identification, binary/discrete for classification.
- **MLP** (Figs 9.11-9.13): perceptrons = scalar product + sigmoid/tanh activation (differentiable ⇒ global effect, extrapolation capability); hidden layer K perceptrons × P inputs weights; output neuron linear activation. Training: quadratic loss V = ½Σe², e = y_measured − f(ANN); nonlinear in weights ⇒ gradient **error back-propagation ("delta rule")**; learning rate η must be tuned/tested; gradient methods = **slow convergence for many parameters**.
- **RBF net** (Figs 9.14-9.15): neurons compute Euclidean distance → Gaussian activation exp(−(u−c)²/2σ²); centers c_j, widths σ_j chosen **a priori** (e.g. uniform spread in input space); local support only ⇒ weak extrapolation; 2-layer net, output = Σ w_i·y_i with perceptron-type summing neuron ⇒ output-layer weights **behind** nonlinearities ⇒ error linear in them ⇒ explicit LS solvable ⇒ **much faster convergence than MLP gradients**; but tuning c,σ too needs nonlinear optimization again.
- **Local linear model network LOLIMOT** [9.42],[9.43]: RBF extended — output-layer weights replaced by linear functions of inputs: ŷ = Σᵢ Φᵢ(u)·(w_iᵀu + w_i0); **normalized** Gaussian validity functions Φᵢ (sum = 1), axis-orthogonal input-space partition ⇒ interpretable as **Takagi-Sugeno fuzzy model**. Centers/σ = nonlinear params (heuristic, no explicit nonlinear optimization); local model params w = linear params. Training LOLIMOT algorithm: outer loop = input-space decomposition (start with 1 global linear model; each iteration split the single **worst** local model into two; try all axes, take best split; σ ∝ hyperrectangle extent). Hinging hyperplane trees [9.11],[9.56]: axis-**oblique** splits, needed for strong nonlinearity/high dimension, more construction effort.
- Advantages: inherent structure identification, very fast robust training, no nonlinear optimization, structure adapts to process complexity. Training data must cover input space evenly; result = parametric model usable for arbitrary u.

- Practical bonus vs look-up tables: ANN training accepts arbitrarily distributed data (no fixed grid positions needed) → far less measurement effort.
- **Example 9.1: ANN for static behavior of a combustion engine** (worked, with numbers):
  - 6-cyl **SI (spark-ignition) engine, 2.5 L V6**; identify **engine torque** vs **throttle angle + engine speed** (2 inputs, 1 output).
  - **433 measured data points** from engine test stand, unevenly distributed (Fig 9.18).
  - **MLP (2-6-1) topology → 31 parameters** after training (Fig 9.19); good interpolation AND extrapolation — approximates well even in data-sparse regions [9.25].

#### 9.3.3b Dynamic ANNs
- Two families: **external dynamics** (static NN + input filters F_i(q⁻¹) and output filters G_i(q⁻¹)) vs **internal dynamics** (dynamic elements inside neurons).
- External, simplest case = pure time delays → shifted samples as network inputs:
  - measured y fed back to NN inputs = **series-parallel model** (= equation-error analogue, training-friendly);
  - NN's own output fed back = **parallel model** (= output-error analogue) — Fig 9.20.
  - Pros: reuse static training methods. Cons: enlarged input-space dimension, possible stability problems, static behavior only via iterative simulation (run step input, wait for steady state).
- Internal dynamics: recurrent / partially recurrent / **LRGF (locally recurrent globally feedforward)** [9.44]; LRGF keeps static layout, dynamic neurons: local synapse feedback / local **activation** feedback / local output feedback (Figs 9.21-9.22). Simplest = local activation feedback [9.2]: each neuron gets 1st/2nd-order linear transfer function, dynamic params a_i, b_i adapted; static vs dynamic behavior separable, **stability can be guaranteed**. Usually MLP; RBF with dynamic output layer works for Hammerstein-structure processes [9.2]. Training via extended gradient methods [9.44].
- LOLIMOT + external dynamics ⇒ locally valid linear input/output models.

#### 9.3.3c Semi-physical models (LPVM / local models with distinct input spaces)
- Split inputs into **manipulated u** vs **operating-point variables z**; local linear models with z-dependent parameters = **linear parameter variable models (LPVM)** [9.5].
- Global nonlinear model ŷ = Σ_{i=1}^K Φ_i(z)·g_i(u) [reconstructed gist of 9.156]; validity/membership functions Φ_i partition input space [9.45],[9.3],[9.41],[9.43].
- Local models ⇒ transparent structure mappable to **physical laws** ⇒ better training/generalization, lower complexity.
- **Distinct input spaces**: submodels act on u-vector, weighting functions on reduced vector z containing **only the inputs with significant nonlinear effects** (the directions needing splitting) ⇒ fewer gate inputs, structure identification simplified (Fig 9.23).
- Rearrangement: ŷ = Σ w_i(z)·x_i ⇒ **linear in parameters with operating-point-dependent w_i(z)** ⇒ process coefficients keep **physical meaning** → "semi-physical" [9.57]. This is the direct bridge to parameter-change fault signatures in nonlinear plants.
- Trade-off: submodel complexity vs count. Known nonlinear input transforms (e.g. x→x², √x) can be baked in via input pre-processing (Fig 9.24) → far fewer submodels. Fully physical submodels and **inhomogeneous structures per operating regime** allowed.

### 9.3.4 Grid-based look-up tables (static)
- Most common nonlinear static model in practice; **automotive ECUs contain ~100 grid-based look-up tables** (engine + emission control) [9.8] — hard compute/storage limits + real-time make LUTs the default.
- Structure: nodes on multidimensional grid; node height = function estimate at that grid position; grid positions fixed a priori; store in ROM (Fig 9.25 shows a 6-cyl SI-engine torque map). Placing measurements directly on grid points avoids optimization.
- 2-D evaluation: find enclosing 4 nodes → **bilinear area interpolation**: each height weighted by the OPPOSITE sub-area, sum, divide by total area (Fig 9.26, eq 9.143-ish) [9.54],[9.56] — cheap, widely used in real-time. Accuracy ← grid density (smooth maps = coarse grid; strong nonlinearity = fine grid); assumes all heights available over full grid range (often violated).
- LUTs = **nonparametric** models; easy subsequent adaptation of single node heights to changing environment (= re-trainable for drift/fault compensation). Fatal limit: **node count grows exponentially with inputs** ⇒ practical 1-D/2-D only. Not suitable for dynamic behavior.
- Parametric alternatives (poly/NN/fuzzy) need far fewer parameters/storage but costlier online evaluation. Fitting LUT heights at arbitrary measurement coords via parameter estimation: [9.40].

#### 9.3.5 Friction & backlash identification (non-continuously-differentiable nonlinearities)
- Domain: mechanical systems — **dry (Coulomb) + viscous friction, backlash/dead zone**; electrical: magnetization hysteresis. These are also wear/fault signatures (see problem 11).
- a) Friction: dry friction = constant with velocity-dependent sign; steady state → hysteresis curve. Two ID routes:
  1. **Nonparametric**: trace hysteresis curve pointwise by slow continuous/stepwise input u=y₁, measuring y=y₂.
  2. **Parametric**: ODE/difference models with dry+viscous friction are **linear in parameters** ⇒ direct LS over NM−1 measured points; differential or difference equations both fine.
- Direction-dependent parameters: difference-equation model with **K₀₊ / K₀₋ offsets** per motion direction; estimate offsets either implicitly (append to θ) or explicitly via Δy/Δu differencing with direction-independent a_i,b_i + separate K₀₊, K₀₋ per direction.
- **Identifiability caveat**: direction-dependent estimation needs data from **one-directional motion without reversal** (sign condition on velocity, eqs 9.16x OCR-failed; tested with e=0). Test signal [9.38] (Fig 9.27): linear ramp (one-direction motion at set velocity) → step (excite higher freq) → steady state; **at reversals (points 1,2,3...) stop estimation**, restart or continue with same-direction data only.
- Model-based hysteresis curve computable from static behavior of the fitted dynamic model; **verification: compare computed curve vs directly measured static curve**.
- Rotary drives: [9.23],[9.22] method correlating measured torque with rotational acceleration → **estimate moment of inertia**, then nonparametric friction-torque characteristic. (Inertia J estimate = diagnosis-relevant parameter.)
- Status: methods proven in practice + used for friction-compensated digital control [9.38],[9.52]; further [9.1],[9.9].
- b) Backlash/dead zone (oscillator with dead zone width 2·l_s? [OCR?] "21"): outside dead zone the backlash acts as a **sign-dependent constant offset on the input** (force c·sign(...)); inside dead zone force = 0 and system runs its own eigenbehavior if contact point fixed; if the point floats (e.g. unmodeled friction), set y₂=y₃, c=0 in (9.161). Simplified block diagram (Fig 9.29): backlash = **offset shift of input with changing sign** for |...| > |...|.

### 9.4 Symptom generation with identification models ← THE chapter's punchline for FDI
#### a) Parameter estimation as symptom source
- Premise (from Ch1): faults change process parameters — one or several deviate from normal set θ_N [eq OCR-failed: θ̂ ≠ θ_N].
- Because estimates fluctuate from noise + unmodeled dynamics, define **thresholds ±Δθ_i,th for normal low/high** and run **limit checking (Ch7)**; exceedance = **symptom s_θi** (eq OCR-failed, gist: s = 1 if |θ̂_i − θ_Ni| > Δθ_th).
- Ct models: estimates map to **physical process coefficients** via inverse algebraic relations θ→physical (see eq 5.24) IF identifiability condition for coefficients holds (Sec 5.2.3, and 'Chapter 23.4' [OCR?]).
- BUT: recovering physical coefficients is **not necessary** — certain faults produce certain **patterns of parameter changes Δθ**, and diagnosis follows from those patterns; Part V examples + classification methods formalize this. (parameter-change → fault mapping = signature/pattern approach)
- Discrete-time caveat: z↔s parameter relations complicated (z-transform tables); converting to ct parameters only recommended for 1st order; for n>2 rely on classification/other diagnosis methods — but **simple Δθ patterns often suffice in practice**.
#### b) Neural networks as symptom source
- NN weights = many, physically uninterpretable ⇒ **unsuitable as parameter-deviation symptoms**.
- Nonlinear static case: **look-up tables allow direct output comparison — LUT differences ΔZ(u₁,u₂,...)** (node-height drift map).
- Identified NN models are mostly used to generate **output-signal symptoms** (residuals), not parameter symptoms.
#### c) Input excitation requirements
- Dynamic ID needs excitation. Processes that excite themselves in normal operation — **servo control systems, actuators, machine tools, robots, vehicles, mobile systems** — admit direct application if persistent excitation is met [9.30],[9.31].
- Otherwise inject test signals: **steps, harmonic, PRBS**; tolerable occasionally for e.g. **pumps**, or no problem at all for **end-of-line quality control of assembled products**.

### 9.5 Problems (exercises — keep the worked-number one)
- P1: LS estimation eqs for y(k)+a₁y(k−1)=b₁u(k−1); what changes for dead time d=5.
- P2: LS estimate of impulse-response weights g(k), k=0..l from I/O data (convolution-param form).
- P3: **worked numeric**: 1st-order system, measurements k=0..10, u(k) = 0,1,−1,1,1,1,−1,−1,0,0,0 and y(k) = 0,0,0,0,0,0,1,0,0,0,0 [table garbled, values as read: y=1 at k=6 and possibly k=7,0; row OCR-shifted] — compute â₁, b̂₁ by batch LS.
- P4: recursive LS (RLS) equations for 1st-order process; modifications for d=2.
- P5: ct LS equations for first-order ODE (uses measured ẏ at samples).
- P6: conditions for direct LS on polynomial nonlinear models (→ input must vary; E{n}=0).
- P7-8: sketch MLP vs RBF neuron; compare MLP training (gradient/backprop, slow) vs RBF output-layer training (explicit LS, fast).
- P9: weight count for 2-layer perceptron P inputs / K hidden / M outputs = P·K + K·M (+ thresholds).
- P10: 1-D LUT interpolation = **linear interpolation**.
- P11: **friction fault symptom**: Coulomb friction of 2nd-order oscillator increases due to **missing lubrication** → generate symptom via equations (fit friction model / K₀ or hysteresis-curve area growth ⇒ parameter-deviation symptom).
- (Line 4895-4899 stray text = Ch10 intro lead-in on residuals/parity equations, belongs to Ch10 notes, not Ch9.)

