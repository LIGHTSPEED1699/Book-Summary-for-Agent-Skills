# Nguyen et al. Ch6–8 — Prognosis, Metrics, Product Support

## Ch6 — Failure prognosis ("the Achilles' heel of CBM/PHM")
**Four challenges**: (1) infer the unmeasurable fault variable (no "crack length meter") from measurable signals; (2) predict temporal progression accurately and precisely; (3) prescribe uncertainty bounds/confidence limits; (4) improve accuracy/precision/timeliness online via learning.

### Three approach families (Table 6.1 logic)
- **Experience-based**: failure history required, no sensors/model.
- **Evolutionary (feature-based)**: sensors + identified fault patterns, no engineering model.
- **Physics-based**: model + operational profile required, history beneficial — most comprehensive; can produce RUL even without measurable events once the model is identified.

### 6.2 Model-based prognosis
- **Physics-based fatigue**: Paris-law crack growth dα/dN = C₀ ΔKⁿ (α crack length, N cycles, ΔK stress-intensity range); parameters estimated by **nonlinear RLS with forgetting factor**; stochastic variants treat parameters as random → SDE for growth. Operational-profile/load model (steady + transient) drives damage accumulation; microstructural metamodels are the frontier.
- **ARMA/ARMAX/ARIMA**: system-identification loop (experiment → hypothesize model + fit criterion → estimate → validate on unseen data); stationary disturbance spectrum; used when physics is too complex.
- **Particle filtering (recursive Bayesian estimation)** — the book's flagship prognostic method (Orchard et al., Georgia Tech): combines fault-growth model + online observations; avoids Kalman's linearity/Gaussian assumptions; state = fault variable (crack length) as random variable with distribution; **learning/correction terms** adjust model online to keep long-term prediction accurate and precise; yields the TTF PDF and confidence intervals directly. Kalman filtering is the Gaussian special case.

### 6.3 Probability-based prognosis
- Joint/marginal/conditional PDF machinery; **Weibull time-to-failure**: F(t) with shape β (β<1 decreasing hazard = wear-in, β=1 constant, β>1 increasing = wear-out — the bathtub curve), characteristic life η, location γ; fit by parameter estimation or **Bayesian analysis** (α, λ as random variables, posterior joint/marginal densities from failure-time data) → RUL estimate with credible bounds.

### 6.4 Data-driven prediction
- **ANN predictors**: MLP math (weight matrices with thresholds as first columns, augmented input), backprop tuning (discrete/continuous), Hebbian simplification; standard statistical confidence estimation does NOT apply directly to NNs.
- **Dynamic wavelet neural network (DWNN)**: delayed inputs/outputs augment the feature vector; wavelet net as nonlinear predictor; trained with Levenberg–Marquardt or genetic algorithms; handles mixed time/frequency features. Example: Navy centrifugal chiller bearing crack — features (MaxSx/y/z, MaxPSDx/y/z from triaxial vibration windows) → DWNN trained at 1/100th of the record predicts crack growth to failure.
- **CPNN (confidence prediction neural network)**: adds confidence limits to NN predictions — needed because prognosis requires bounds.
- Uncertainty management: reduce growing uncertainty bounds with more data/learning.

### 6.5 Case studies
- **Engine bearings (Allison T63 analog rig)**: seeded spall, vibration + oil-debris channels; early detection features (Impact Energy) → spall initiation/propagation models → **Monte Carlo life distribution** (input uncertainties as normal/lognormal); **Yu–Harris model** for M50 bearing room-temperature rolling-contact-fatigue tests (3600 rpm, 7808K lube) — predicted life distribution from 1M Monte Carlo points matches test histogram.
- Integrated prognosis system: specialized incipient-fault features + physics model + particle filter + learning.

## Ch7 — Requirements and performance metrics
- **Requirements template**: detection (% of FMECA faults monitored), isolation (% to ORA/LRU), identification (incorrect-ID rate), false-alarm rate, BIT end-to-end test time, prognosis confidence (threshold 90% / objective 98%), warning time (1 day / 7 days), replacement at ~10% remaining life.
- **Feature-evaluation metrics**: ideal (Bayes) classifier error as feature predictive accuracy; **information measures** (Shannon entropy, information gain IG(X) — prefer feature that reduces uncertainty, drop irrelevant); distance measures; dependence measures; **two-sample z-test** for whether two feature distributions differ.
- **Diagnosis metrics**: false positives/negatives vs threshold; **ROC curve** — plot true-positive vs false-positive rate across thresholds; area under curve = accuracy index; straight line = coin flip; choose threshold by criticality trade.
- **Prognosis metrics**: **accuracy** = closeness of predicted TTF to actual (normalized |t_pf − t_af|); **precision** = narrowness of the prediction interval (variance across experiments); **timeliness** — failure must occur within/after the predicted horizon usefully; **confidence** from maintainer's view (when to maintain) vs commander's view (asset availability for mission); uncertainty bounds grow with horizon.
- Effectiveness metrics + cost-benefit analysis of CBM/PHM systems.

## Ch8 — Product support and maintenance
- Product support WITHOUT CBM: RCM (reliability-centered maintenance) with scheduled inspections/overhauls.
- CBM changes: maintenance becomes forward-looking optimization; supply chain driven by ULR predictions; engineering feedback on real failure modes.
- **Cost model example (H-60 intermediate gearbox)**: replacement $39.8K; disassembly inspection $2.1K incl. ground-turn cost $1.5K/flight-hour; compare maintenance schemes on cost + elapsed time.
- **Maintenance scheduling**: Monte Carlo simulation with mean + 2σ of predicted TTF → part/personnel availability curves (e.g., 70% available on demand, 95% with 5 time units lead) → schedule decision.
- CBM knowledge base: FMECA, failure history, models, procedures.

## Practitioner takeaways (Ch6–8)
- Prognosis deliverable = TTF PDF + confidence bounds, not a point. Judge it on accuracy AND precision AND timeliness.
- Prefer hybrid physics + measurements (particle filter / Bayesian with learning) over pure data-driven when failure physics is known; pure NN needs confidence machinery (CPNN).
- Weibull β is a quick diagnostic of failure regime (wear-in / random / wear-out).
- Evaluate features before classifiers (entropy/IG, z-test, ROC); set thresholds by criticality.
- Monte Carlo over the predicted TTF distribution converts prognosis into maintenance/supply decisions — that's the product-support payoff loop.
