# Isermann Ch1–6 — Supervision Concepts, Reliability, Models, Signals

**Fault-Diagnosis Systems: From Fault Detection to Fault Tolerance** (Rudolf Isermann, Springer 2006). The reference architecture for model-based FDI: 19 chapters from definitions and reliability through residual generation, diagnosis, and fault-tolerant design.

## Ch1–2 — Supervision architecture and definitions
- **Tasks of supervision** (layered): 1) **monitoring** (limit checking + alarms for the operator), 2) **automatic protection** (auto counteraction to a safe state — fuse, overspeed trip, temperature protector), 3) **fault detection** (find that something deviated), 4) **fault diagnosis** (type/size/location/time), 5) **fault tolerance** (keep operating despite faults).
- **Fault**: "an unpermitted deviation of at least one characteristic property (feature) of the system from the acceptable, usual, standard condition" — a *state* within the system; may be abrupt, incipient (drift), or intermittent; may exist without effect.
- **Failure**: "a permanent interruption of a system's ability to perform a required function under specified operating conditions" — an *event* resulting from one or more faults.
- **Malfunction**: incorrect function. Closed loop hides faults: the controller compensates, so the output looks fine while the manipulated variable carries a permanent offset — **supervise u as well as y**.
- Knowledge-based FDI (symptoms + rules) vs model-based FDI (analytical redundancy); implementation: sampling times, on-board feasibility.

## Ch3 — Reliability, maintainability, availability
- **Reliability R(t)**: probability of failure-free operation; failure rate λ(t) bathtub curve (early failures, constant random, wear-out); MTBF.
- **Maintainability**: MTTR; **availability** A = MTBF/(MTBF+MTTR).
- Fault management over the total life cycle; failure statistics by component class (electronics vs mechanical).

## Ch4 — Safety and risk analysis
- **FTA** (top event → AND/OR gates down to basic events) and **ETA** (initiating event forward to outcomes); **FMEA** (bottom-up failure modes × effects × criticality); hazard analysis; risk classification bands; integrated reliability-and-safety design (this feeds *what to monitor*).

## Ch5 — Fault models and process models
- **Additive fault**: output deviation ΔY independent of the input signal — detectable at any operating point.
- **Multiplicative fault**: ΔY depends on the input (e.g., gain change) — **undetectable when the input is zero**; excitation matters.
- Sensor fault models (offset, drift, gain, precision/noise, short circuit, saturation; first-order lag dynamics; internal vs external disturbances); actuator faults (stuck, friction/backlash, leakage, dead time); process faults (parameter changes: mass, stiffness, resistance, catalyst activity).
- Process models: state-space, transfer functions, input-output polynomial/ARV models, difference equations — the same models later generate residuals.

## Ch6 — Signals
- Harmonic oscillations (amplitude, frequency, phase; sums), stochastic signals (mean, variance, autocorrelation, cross-correlation, PSD, white/colored noise) — the vocabulary for both symptoms and disturbances.

## Practitioner takeaways (Ch1–6)
- Classify the fault first: additive vs multiplicative, abrupt vs incipient — it dictates detectability and the method.
- In closed loops, output-only supervision is blind; instrument and watch manipulated variables.
- Reliability/FMEA work upstream decides *which* features deserve supervision — FDI without FMEA is unfocused.
