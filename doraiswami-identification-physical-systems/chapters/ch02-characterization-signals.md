# Chapter 2: Characterization of Signals - Correlation and Spectral Density

## Core Idea
Correlation measures waveform similarity across lags; its Fourier transform is power spectral density — the same information in frequency. These second-order statistics are the practitioner's workhorse: they detect known signals buried in noise, estimate time delays from correlation peaks, identify systems non-parametrically as the spectral ratio S_yx/S_xx, and quantify how much of a spectrum is real via the coherence spectrum. For random signals the ensemble definitions become single-record time averages under ergodicity — the practical license used everywhere in the book.

## Frameworks Introduced
- **Correlation definitions by signal class**: energy signals (infinite or truncated), power signals, periodic signals (sum over one period), jointly WSS random signals (ensemble average E[x(k)y(k−m)] → time average under ergodicity).
- **Truncation practice**: finite records need an assumption for unavailable edge samples — zero, mean, or periodic extension; N must exceed settling time (transients) or contain several periods.
- **Property table as an algorithm**: white noise autocorrelation = δ; signal+noise autocorrelation = signal's for m ≠ 0; cross-correlation of random with deterministic ≈ 0; similar waveforms accentuate; delay = lag of cross-correlation peak.
- **Wiener-Khinchin**: power spectral density = FFT of autocorrelation; cross-power spectrum = FFT of cross-correlation; correlation = spectral overlap measure.
- **Non-parametric system identification**: Ĥ(f) = S_yx(f)/S_xx(f) (H1) from output-input cross-spectrum over input spectrum; time delay from cross-correlation peak.
- **Coherence spectrum**: γ²_xy(f) = |S_xy|²/(S_xx S_yy) — frequency-domain correlation coefficient in [0,1]; near 1 = trustworthy spectral estimate, near 0 = noise/artifact; restrict analysis to the band of interest.
- **Random signal generation**: filter white noise through chosen LTI to synthesize low/band/high-pass processes (ties back to ch1's generating filters).

## Key Concepts
- Autocorrelation of a rational-spectrum waveform inherits its shape (constant→constant, sinusoid→sinusoid, damped→damped, periodic→periodic).
- Cross-correlation of two periodic signals of different periods = 0 — orthogonal families detected statistically.
- Coherence is the quality flag on every spectral estimate; always plot it with the spectrum.
- Ergodicity in mean and correlation converts one long record into ensemble statistics — the assumption behind every formula in the chapter.
- Truncation choices (zero/mean/periodic) are bias choices; they matter at large lags.

## Mental Models
- "Correlation is a matched filter over lags": detection, delay estimation, and feature extraction are all sliding inner products.
- "Spectrum is correlation wearing a hat": pick whichever domain makes the question cheap.
- "Ratio of spectra = system": non-parametric ID is one division — with coherence as the warranty.
- "Noise decorrelates": randomness vs deterministic structure separates cleanly under correlation — the basis of enhancement and diagnosis.

## Anti-patterns
- **Trusting spectral ratios without coherence** — S_yx/S_xx where γ² ≈ 0 is noise division.
- **Too-short records** — N below settling time/period count corrupts correlation tails and spectra.
- **Silent edge assumptions** — zero-padding vs periodic extension changes large-lag estimates; state the choice.
- **Confusing ensemble and time averages without ergodicity** — non-ergodic data (trends, regime shifts) break the single-record formulas.

## Reference Tables
### Correlation cheat
| Signal pair | Result |
|---|---|
| white noise ⊛ itself | δ(m) |
| (signal+noise) ⊛ itself | R_signal(m) for m ≠ 0 |
| random ⊛ deterministic | ≈ 0 |
| periodic ⊛ periodic (same period) | periodic, accentuated |
| periodic ⊛ periodic (different periods) | 0 |
| two copies offset by d | peak at m = d |

### Spectral toolkit
| Quantity | Definition | Use |
|---|---|---|
| S_xx | FFT of r_xx | power distribution |
| S_yx | FFT of r_yx | input-output coupling |
| Ĥ = S_yx/S_xx | H1 estimator | non-parametric ID |
| γ² = \|S_yx\|²/(S_xxS_yy) | coherence | estimate quality |

## Key Takeaways
Second-order statistics (correlation, PSD, coherence) give a complete non-parametric characterization for WSS signals and a one-division system estimate.
Correlation properties are detection algorithms: noise suppression, delay estimation, periodicity tests.
Coherence is the trust meter — never use a spectral ratio without it.
Ergodicity + adequate record length are the two assumptions that make single-record analysis legal.

## Connects To
ch1's generating filters produce the signals characterized here; ch7 uses correlation/normal-equation views for parametric ID and spectral methods for non-parametric; ch9 uses spectral signatures for condition monitoring; ch12 uses coherence for sensor-network diagnosis. Katayama ch4 is the theory twin (Hilbert-space prediction vs these computational tools).
