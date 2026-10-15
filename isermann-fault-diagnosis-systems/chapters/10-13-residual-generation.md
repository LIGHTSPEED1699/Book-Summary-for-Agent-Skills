# Isermann Ch10–13 — Residual Generation: Parity, Observers, Closed Loop, PCA

## Ch10 — Parity equations / analytical redundancy relations
- **Primary residuals** from the process model: **input form (unknown-input-effect form)** residuals use measured inputs and outputs directly; **output form** residuals come from output models. Polynomial residuals embed higher derivatives → noise amplification and realizability limits.
- **Parity space with state-space models**: continuous- and discrete-time parity approaches — project the output vector onto the null space of the observability-like matrix so the state drops out; residual = parity violation.
- Example 10.1: first-order process with parameter faults (ΔK, ΔT) — the same fault shows differently in output-error vs equation-error residuals, and the response depends on whether the input is constant or stepping (**excitation dependence of multiplicative faults**).
- **Properties of residuals / enhancement**: low-pass filtering of high-frequency noise; **maximizing fault sensitivity**; **robustness against model errors**; **adaptive thresholds** depending on input excitation.
- **Structured residuals**: design so each fault influences a distinct subset of residuals → **residual patterns**; **directional residuals**: each fault drives the residual vector along a fixed direction (length = size).
- **Isolation taxonomy**: strongly isolating / weakly isolating / not isolating (sign patterns count); with n binary-checked residuals up to **2ⁿ − 1** faults distinguishable; using signs and sizes increases capacity further.

## Ch11 — Observer-based methods
- **State observers**: inject additive input/output fault vectors into the model; observer error dynamics show fault signatures; **residual = output estimation error e = y − ŷ**; Laplace-domain transfer from faults to residual gives frequency shaping (HP/LP behavior per fault type).
- **Multiplicative faults** need state-augmented/parameter-varying treatment.
- **Kalman filter** as stochastic observer: innovation sequence is the residual; whitening violation = fault.
- **Output observers / unknown-input observers**: estimate outputs directly, decoupling unknown inputs (disturbances) — the observer counterpart of parity projection.
- **Parity vs observer equivalence**: same residual information, different realization (Section 11.4 compares residual equations and simulations) — choose by implementation convenience.

## Ch12 — Closed-loop supervision (control performance monitoring)
- Faults in closed loop (Table 12.1): actuator (friction, backlash, stuck), sensor, process parameter, controller parameter faults all produce similar closed-loop symptoms — sluggish, oscillatory, offset behavior — so **closed-loop detection needs model-based methods plus manipulated-variable data**.
- **Signal-based**: IAE between zero crossings; oscillation indices; count load-detections; **cross-correlation phase-shift test**: sinusoidal disturbance/unstable loop → phase ≈ π (even ccf), static friction → different phase; Fourier shape analysis distinguishes sinusoidal vs rectangular/triangular oscillation spectra.
- **Model-based closed-loop supervision**: bias estimation (observer bank), parameter estimation under feedback (identifiability under control), supervisory model in parallel with the control model.

## Ch13 — Principal component analysis (PCA)
- Transform N-variable data to principal components (eigenvectors of the covariance); most process variation lives in a few components.
- **Three detection schemes**: (a) change-detect the transformed variables Tᵢ; (b) change-detect projected variables; (c) **residuals between original and back-transformed variables** (Q-type) — deviations link directly to process variables xᵢ(k).
- Caveat: faults appearing in directions discarded by PCA are missed; interpretation of component changes can be hard.

## Practitioner takeaways (Ch10–13)
- Residual design = sensitivity vs robustness trade; structure residuals for isolation patterns from the start (n residuals → 2ⁿ−1).
- Parity and observer methods are two faces of one projection — pick the one your team can maintain.
- Never supervise a control loop from the controlled variable alone; oscillation diagnosis (IAE + ccf phase + spectrum shape) is cheap and high-yield.
- PCA suits multivariable correlated data (process industries); keep the back-transform residual for interpretability.
