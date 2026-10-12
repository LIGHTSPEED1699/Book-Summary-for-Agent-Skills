# Chapter 1: Modeling of Signals and Systems

## Core Idea
Everything downstream — identification, Kalman filtering, fault diagnosis, soft sensing — runs on one move: model the *signals* (reference, disturbance, noise) as outputs of LTI systems driven by delta functions (deterministic) or white noise (random), then augment that model with the plant into a single integrated model. Difference-equation (AR/MA/ARMA) form feeds identification; state-space form feeds observers and Kalman filters. Setting the driving input to zero yields a model of the *class* of signals — the internal model that guarantees tracking/rejection when embedded in a controller or filter.

## Frameworks Introduced
- **Two characterization approaches**: non-parametric (FFT/frequency response, correlation/spectral density — macroscopic, fast) vs parametric (discrete-time models of plant, signal, noise — microscopic, detailed); they complement each other.
- **Signal taxonomy**: deterministic vs random; bounded/unbounded; energy vs power signals (finite N ⇒ energy signal); causal/anti-causal/non-causal signals and systems.
- **Deterministic signal model**: constants, exponentials, sinusoids, damped sinusoids, periodic waveforms = outputs of an LTI system driven by δ(k); the model is the z-transform of the signal.
- **Random signal model**: output of an LTI filter driven by zero-mean white noise; low-pass/band-pass/high-pass random signals by filter choice.
- **Integrated (augmented) model**: plant ⊕ disturbance model ⊕ measurement-noise model → high-order AR/MA/ARMA difference equation (for identification) or augmented state-space (for Kalman filter/observer).
- **Internal model principle (preview)**: embed the zero-input model of the signal class in controller/observer/filter and drive it by the error ⇒ exact steady-state tracking/rejection.
- **Three uncertainty philosophies**: worst-case deterministic, fuzzy logic, probabilistic — the book commits to probabilistic.

## Key Concepts
- Signal vs noise is intent-based (desired vs unwanted waveform), not spectral.
- A deterministic signal's "model" is its generating filter; future values computable from past — that's why deterministic components can be predicted and subtracted.
- Random signals need ensembles/statistics; single realizations only under ergodicity (ch2).
- Augmentation is the book's signature construction: the same physical setup yields an ARMAX-style model (identification) or an augmented-state Kalman filter (estimation) depending on which form you write.
- Causality of system ⟺ impulse response zero for k < 0.
- Energy signals (transients) vs power signals (persistent); finite data records are energy signals — relevant to FFT leakage and LS conditioning.

## Mental Models
- "Model the exogenous, not just the plant": references, disturbances, and noise each get a generating model; performance claims depend on them.
- "Same physics, two forms": ARMA for identification, state-space for filtering — choose the form by the task, convert freely.
- "Zero the input, get the class": a model of all signals of a type is the generating filter with input removed; that's the internal model.
- "Uncertainty is a signal source": fictitious random inputs mimic model error — treat ignorance as an input to be modeled.

## Anti-patterns
- **Designing without the signal-class model** — steady-state tracking/rejection fails unless the internal model is embedded (the book's recurring design law).
- **Treating a finite record as a power signal** — spectral estimates need window/length care (ch2).
- **Parametric vs non-parametric tribalism** — the book uses FFT views for diagnosis and parametric models for everything else; pick per task.
- **Ignoring measurement noise structure** — low-pass/band-pass noise models change the optimal filter; white-noise assumption is a modeling choice, not a fact.

## Reference Tables
### Signal → generating model
| Signal class | Driver | Generating filter |
|---|---|---|
| constant/step | δ(k) | 1/(1−z⁻¹) |
| sinusoid | δ(k) | resonant 2nd-order |
| damped sinusoid | δ(k) | stable 2nd-order |
| periodic | δ(k) | comb (z^N−1) |
| low-pass random | white noise | low-pass LTI |
| band-pass random | white noise | band-pass LTI |

### Two model forms, two uses
| Form | Object | Used in |
|---|---|---|
| AR/MA/ARMA difference equation | integrated model | identification (ch7) |
| augmented state-space | plant+disturbance+noise | Kalman filter (ch6), diagnosis (ch9) |

## Key Takeaways
Model every exogenous signal with a generating filter; augment with the plant; the integrated model is the single object all later chapters consume.
Difference-equation form is for identification; state-space form is for estimation — same content, different interface.
The internal model principle (signal class embedded, driven by error) is the condition for exact tracking/rejection.

## Connects To
ch2 characterizes these signals statistically (correlation/spectra); ch6 builds the Kalman filter on the augmented state-space; ch7 identifies the ARMA form; ch9 injects fault models into the same augmented structure; ch13's soft sensor is the full pipeline. Katayama ch3/ch4 is the theory twin of this chapter's toolbox.
