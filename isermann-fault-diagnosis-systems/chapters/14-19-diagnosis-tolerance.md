# Isermann Ch14–19 — Diagnosis, Classification, Knowledge-Based Methods, Fault Tolerance

## Ch14 — Choosing and combining detection methods
- Suitability analysis: each method (limit checking, signal-based, parameter estimation, parity, observer, PCA) has strengths by fault type, speed, model quality, and on-board cost; no universal winner.
- **Combine methods**: parallel use raises reliability (detection probability up, false alarms down); decision fusion across methods.

## Ch15 — Fault diagnosis framework
- Diagnosis = determine **fault type, size, location, time** from symptoms; procedure: feature extraction → change detection → **symptom-to-fault mapping** → decision.
- **Symptom classes**: analytical symptoms (limit checks, residuals, parameters), **heuristic symptoms** (operator observations: noise, smoke, color), process history/fault statistics.
- **Unified symptom representation**: attach fuzzy membership γ(sᵢ) ∈ [0,1] to every symptom (analytical and heuristic alike) so one inference mechanism can consume them all.
- **Fault–symptom relationships**: physical cause-effect propagation fault → events → symptoms; diagnosis inverts it; encode as relations with confidence measures; prior knowledge (fault statistics, testability) prunes the search.

## Ch16 — Pattern classification for diagnosis
- **Bayes classification**: Gaussian class-conditional densities p(s|fᵢ) from labeled reference data (maximum likelihood estimates of centers + covariance); decide max posterior.
- **Polynomial and geometric classifiers** (decision boundaries, hyperplanes); **fuzzy classifier** (rule-based, interpretable); **neural networks** (learned boundaries when data-rich).
- Practical issues: training data availability, symptom distribution assumptions, interpretability trade.

## Ch17 — Knowledge-based diagnosis
- **Fault trees as diagnostic trees**: binary/discrete-event example (pump–valve–filter system with limit switches): fault-symptom trees enumerate measurement patterns → component hypotheses; efficiency = expected number of measurements/tests to isolate.
- **Approximate reasoning**: **forward chaining** (data → rules → conclusions, good for monitoring) vs **backward chaining** (hypothesis → test goals, good for interactive diagnosis); comparison table.
- **Hybrid neuro-fuzzy systems**: structures combining NN learning with fuzzy rules; identification of membership functions; rule identification with predefined MFs; optimization methods; **SELECT self-learning classification tree** — learns interpretable rule trees from data.

## Ch18 — Fault tolerance: redundancy structures
- **Static redundancy**: n-out-of-m modules with **majority voting** (TMR/2oo3) — fault masking, no switchover, but cost/power/weight and cannot tolerate permanent wrong outputs beyond voting capacity; redundant voters too.
- **Dynamic redundancy**: standby modules — **hot standby** (fast switchover, standby ages) vs **cold standby** (no wear, switch + startup time); duplex with comparator-and-switch (fail-safe); hybrid combinations.
- **Software fault tolerance**: repeated runs, **recovery blocks** (diverse standby software), duplex synchronized processors with comparator software.
- Mechanical/electrical redundancy: dual gears/belts/valves/cylinders/motors at half load.
- **Degradation steps**: graceful performance reduction as faults accumulate (fail-operational → fail-safe ladder).

## Ch19 — Fault-tolerant systems in practice
- **Analytical sensor redundancy**: reconstruct the measured variable from process models (e.g., two outputs + known model, or one output + input sensor); need **≥3 independent values** (measured + reconstructed) for voting → fault-tolerant measurement; automotive **ESP yaw-rate sensor** example (steering angle + model as analytical backups); fail-silent sensor switching (but switches add unreliability).
- **Fault-tolerant actuators**: parallel complete actuators (static or standby); **duplex drive** — split the least reliable part (motor) into two half-load units (aircraft cabin-pressure flap: two DC motors on one planetary gear); fail-operational duplex preferred for actuators (cost/weight vs sensors).
- **Fault-tolerant communication**: **CAN bus** (event- and time-triggered, high reliability, used since 1983 in automobiles) as the backbone for distributed fault-tolerant management.
- **Fault-tolerant control**: early aircraft work; detection + isolation + **control system reconfiguration** (controller re-tuning/structure change after actuator/sensor fault); supervision + tolerance as one loop.

## Practitioner takeaways (Ch14–19)
- Diagnosis is a data problem (classification) and a knowledge problem (trees/rules) — hybrid neuro-fuzzy or SELECT gets both.
- Fuzzy membership on every symptom is the cheap unification trick that lets rules mix sensor math and operator impressions.
- Fault tolerance budget: sensors can be made redundant analytically (cheap), actuators need hardware duplex (expensive), communication gets protocol-level redundancy — design the ladder deliberately.
