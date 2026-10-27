# Nguyen et al. Ch6-8 — Prognosis, Performance Metrics, Product Support (complete)

**Intelligent Fault Diagnosis and Prognosis for Engineering Systems** (Wiley 2006). Full distillation: prognosis (particle filters, Weibull, Yu-Harris/Kotzalas-Harris bearing life with rig numbers), the complete metrics chapter 7.1-7.7 (requirement targets, ROC/POD-POFA, alpha-lambda, RUL confidence examples, total-value cost model, CINCLANTFLT NPV/IRR case), and product-support/scheduling (H60 gearbox and helicopter-LRU worked examples). [reconstructed]/[OCR?]/[derived] tags; nothing invented.

## Nguyen Ch6 — Prognosis (source lines 4353-5340)

### 6.1 INTRODUCTION (lines 4353-4413)
- Prognosis = predict accurately AND precisely the remaining useful life (RUL) of a failing component/subsystem. Called the "Achilles' heel" of CBM/PHM; main challenge = LARGE-GRAIN UNCERTAINTY.
- Two pillars: UNCERTAINTY REPRESENTATION (model various forms of uncertainty from many sources) vs UNCERTAINTY MANAGEMENT (methodologies/tools to continuously "shrink" uncertainty bounds as more data arrive).
- Accurate prognosis demands good probabilistic models of fault growth + statistically sufficient failure-data samples for training/validating/fine-tuning prognostic algorithms. Research targets: prognosis performance metrics, robust algorithms, test platforms.
- Etymology: Greek pro + gnosis = acquire knowledge about events before they occur. Delphic oracle ambiguity: "Ibis redibis non morieris in bello" (you will go, you will return, you will not die in war [or: you will go, you will not return, you will die in war]). Medical usage = foretelling probable course of a disease (Taylor 1953). Industrial question: "What is the remaining useful lifetime of a machine/component once an impending failure condition is detected, isolated, and identified?"
- Fig 6.1 fault propagation economics: catch fault at 4% severity → replace component; at 10% severity → replace subsystem; at failure → replace entire system.
- Running example: helicopter main transmission gearbox, crack on gear plate (Fig 6.2). Instrumented with accelerometers on frame; faults = bearing race crack, missing gear tooth, shaft imbalance; fault isolated to a specific LRU.
- No such thing as a "crack length meter" → FOUR CHALLENGES:
  - Challenge 1: infer actual crack dimension over time from measurable quantities (accelerometer, temperature, speed) = virtual/soft sensor mapping available measurements to hard-to-measure quantifiers.
  - Challenge 2: predict temporal progression of the fault — algorithm takes sensor measurements + system models, outputs fault evolution to failure in a probabilistic sense.
  - Challenge 3: prescribe uncertainty bounds/confidence limits — probability distribution/uncertainty envelope as time progresses.
  - Challenge 4: improve prediction accuracy/confidence/precision via learning strategy using streaming new data (corrections from predicted vs actual fault state); must also account for usage patterns, operating modes, manufacturing variability.
- 6.1.2 Notional framework — enabling tech cited: multistep adaptive Kalman filtering (Lewis 1986), ARMA (Lewis 1992), stochastic ARIMA (Jardim-Goncalves & Martins-Barata 1996), Weibull models (Groer 2000), forecasting by pattern/cluster search (Frelicot 1996), parameter estimation (Ljung 1999); AI side: case-based reasoning (Aha 1997), intelligent decision-based models, min-max graphs, Petri nets, neural nets, fuzzy, neuro-fuzzy (Studer & Masulli 1996); physics-based fatigue models (Ray & Tangirala 1996).
- Fig 6.3 fault trend & failure prediction: feature of interest evolves; prescribed alarm bounds / fault tolerance limits beyond which failure is declared; when predicted feature's CONFIDENCE LIMITS reach the tolerance limits, an alarm is declared.
- Chapter taxonomy (the big three): MODEL-BASED, PROBABILITY-BASED, DATA-DRIVEN prognosis schemes.
- Fig 6.4: prognosis approaches plotted vs applicability and relative implementation cost. Prognosis uses measured/inferred features + data-driven and/or physics-based models to predict future condition; applies to failure modes governed by material condition OR functional loss; algorithms generic in design but specific in application; fidelity range: simple historical/usage models → advanced feature analysis / physics-of-failure models.
- TABLE 6.1 Prognostic Accuracy ladder (Experienced-Based → Evolutionary → Physics-Based), as bullets:
  - Engineering model: Not required / Beneficial / Required
  - Failure history: Required / Not required / Beneficial
  - Past operating conditions: Beneficial / Not required / Required
  - Current conditions: Beneficial / Required / Required
  - Identified fault patterns: Not required / Required / Required
  - Maintenance history: Beneficial / Not required / Beneficial
  - In general: No sensors/no model / Sensors/no model / Sensors and model

### 6.2 MODEL-BASED PROGNOSIS TECHNIQUES (lines 4414-4440)
- Definition: schemes employing a DYNAMIC MODEL of the process being predicted: physics-based models, ARMA techniques, Kalman/particle filtering, empirical-based methods.
- Physics-based models compute damage to critical components as function of operating conditions, assess cumulative effects as component life usage. Integrating physical + stochastic modeling → distribution of RUL as function of uncertainties in component strength/stress properties, loading, lubrication for a particular fault.
- Statistical representations of HISTORICAL OPERATIONAL PROFILES are the basis for computing future damage accumulation; results used for real-time prognostic prediction with specified confidence bounds (Fig 6.5: physics model at core uses critical life-dependent uncertainties so health assessment + RUL projections are examined w.r.t. a RISK LEVEL).
- KEY differentiator vs feature-based approaches: model-based can make RUL estimates IN THE ABSENCE of any measurable events; when diagnostic feature info IS present, model can be calibrated on it. FUSION of feature-based + model-based = full prognostic ability over the entire component life → informs which components to inspect during specific overhaul periods; methodology stays consistent across different critical components/LRUs even though failure modes differ.
- Procedure: develop operational profile prediction from steady-state + transient loads, temperatures, other online measurements; probabilistic critical-component models are "run into the future" via statistical simulations of future operating profiles built from statistics of past (or expected) profiles.
- Authors' experience claim: nonlinear damage mechanisms depend on BOTH inherent profile characteristics AND operational mix types; component lives driven by fatigue are often dominated by unique usage profiles or a FEW RARE SEVERE randomly occurring events (abnormal operating conditions, random damage occurrences). → RECOMMEND statistical characterization of loads, speeds, conditions for projected future usage (Fig 6.6 operational profile/loading model).

### 6.2.1 Physics-Based Fatigue Models (lines 4442-4467)
- Recap of Ch5 §5.6.1 notions: in aircraft/industrial processes, defect (crack/anomaly) INITIATION and PROPAGATION must be estimated for effective prognosis. Dynamic fatigue/fault-progression models derived from physics principles.
- Microstructural models (down to single-particle level; Friedman & Eidenoff 1990) are NOT suitable for real-time treatment (immense computational complexity). REDUCED-ORDER MODELS = METAMODELS derived from microstructural characterization → near-real-time crack initiation/propagation estimation on conventional platforms (Newman 1992).
- Crack INITIATION models must account for: temperature variations, cycle frequency, stress ratio, sustained load hold time, and interactions of damage mechanisms (fatigue, environment, creep). Constitutive equations detail: Chestnut (1965).
- Crack PROPAGATION models split into two categories: DETERMINISTIC and STOCHASTIC. Fatigue crack growth in bearings, gears, shafts, aircraft wings affected by stress states, material properties, temperature, lubrication, environment.
- PARIS FORMULA (deterministic basis): da/dN = C0 (ΔK)^n  [OCR: formula not decoded at line 4454; reconstructed from variable list — standard Paris law]
  - a = instantaneous length of dominant crack
  - N = running cycles
  - C0, n = material-dependent constants
  - ΔK = range of stress-intensity factor over one loading cycle
- Model parameters typically estimated via NONLINEAR RECURSIVE LEAST SQUARES with a forgetting factor (Ljung 1999).
- STOCHASTIC crack growth models: treat ALL parameters as random quantities → growth equation becomes a STOCHASTIC DIFFERENTIAL EQUATION. Means to estimate parameter distributions: Monte Carlo simulations, probabilistic neural networks, others.

### 6.2.2 ARMA, ARMAX, and ARIMA Methods (lines 4468-4528)
- Motivation: for complex systems, deriving dynamic models from all physical processes is hard/impossible → ASSUME a model form, fit parameters from observed input-output data = MODEL IDENTIFICATION (surrogate model). Classic problem: given I/O data, develop model predicting future behavior.
- Fig 6.7 generalized system: input u_k, output y_k, unmeasured disturbance v_k. Fig 6.8 system identification loop: prior knowledge guides experiment design → test runs → hypothesize model + criterion of fit → compute parameters from test data → VALIDATE on previously unseen data → if OK use it, else loop back.
- Setup [all formulas OCR "not-decoded"; structure from variable text, reconstructed labels marked]:
  - Disturbance v_k assumed STATIONARY with spectrum Phi_v(z) [formula missing].
  - R(z) assumed to have NO poles and NO zeros on or outside the unit circle (stability condition).
  - Transfer function R(q) = C(q)/A(q), ratio of two polynomials in q; q^-1 = unit delay [polynomial definitions OCR-missing].
  - ARMA: discrete-time recursion relating v_k at time k to its PAST HISTORY plus time history of white noise e_k up to time k; e_k white noise with variance lambda. Interpretation: projecting/predicting value of v at time k from past histories of v_k and e_k. Good modeling framework for data/disturbances derived from the spectrum only. [recursion formula not decoded: standard form A(q^-1) v_k = C(q^-1) e_k]
  - EQUATION ERROR MODEL (Ljung 1999): input-output relation y_k = ... relating u, y [formula missing]; unknown coefficients collected in theta = [a1...a_na, b1...b_nb]^T; write y_k = theta^T h_k where h_k = REGRESSION VECTOR containing all observed data incl. past values of input u_k and output y_k.
  - ARMAX: equation error model lacks freedom to fully describe disturbance properties (ARMA needs current + previous noise values) → ARMAX describes equation error as MOVING AVERAGE of white noise: A(q^-1) y_k = B(q^-1) u_k + C(q^-1) e_k [reconstructed; OCR formula missing]. Unknown parameters now include c_i; regression vector h now ALSO contains previous values of e_k.
  - ARIMA: ARMA version with ENFORCED INTEGRATION — useful for describing systems with SLOW DISTURBANCES.
- Parameter identification: problem boils down to determining theta from observed I/O sequences; with sufficient test measurements use LEAST SQUARES (Ljung 1999); techniques mature, available e.g. in MATLAB toolboxes.
- Prognosis use: ARMA & derivatives as PREDICTORS — estimate theta from data up to time t (least squares), then run the fitted dynamic (ARMAX) model forward to predict future outputs → predict states to estimate fault progression.

### 6.2.3 The Particle Filter Framework for Failure Prognosis (lines 4530-4597)
- Georgia Tech methodology (Orchard et al., 2005). Employs state dynamic model + measurement model to predict the POSTERIOR PDF of the state = predict time evolution of a fault or fatigue damage.
- Beats Kalman filtering: AVOIDS linearity and Gaussian-noise assumptions; robust framework for LONG-TERM prognosis while accounting for uncertainties. Correction terms estimated in a LEARNING paradigm to improve long-term accuracy/precision. Applied to crack fault; robustness and superiority supported. (Particle filter for DIAGNOSIS covered in Ch5.)
- Core idea: critical-state variables (crack length, corrosion pitting...) are RANDOM VARIABLES with probability distribution vectors; once failure PDF estimated, confidence intervals and other prognosis attributes computable → recursive BAYESIAN estimation combining fault-growth model info + online sensor data on key fault parameters (observations).
- Prognosis = accurate current-state estimation + fault-progression model. If incipient failure detected early, sensor data available for a time window allowing corrective measures = improve model parameter estimates; at END of observation window prediction is passed to user (operator/maintainer), further adjustment NOT feasible because action must be taken to avoid catastrophe.
- Fig 6.9: sensors + feature-extraction module feed sequential observations z_k of the fault growth process. State-evolution + measurement model: x_k = f_k(x_{k-1}) + w_k ; z_k = g_k(x_k) + v_k [reconstructed; OCR formula missing] where x_k = fault dimension state (crack size) + changing environment parameters affecting fault growth; w_k, v_k NON-GAUSSIAN noises; f_k, g_k NONLINEAR functions.
- Two-part approach: (1) STATE ESTIMATION — estimate current fault dimension + changing environment parameters (same as diagnosis, Ch5). (2) LONG-TERM PREDICTION — from current fault-dimension estimate + fault-growth model with parameters refined in the a posteriori state estimation. Novel RECURSIVE INTEGRATION process based on IMPORTANCE SAMPLING + PDF APPROXIMATION THROUGH KERNEL FUNCTIONS generates state predictions from (k+1) to (k+p) [formula missing].
- HAZARD ZONE defined by lower/upper bounds H_lb and H_up; long-term predictions estimate probability of failure w.r.t. hazard zone; prognosis CONFIDENCE INTERVAL + expected TIME TO FAILURE (TTF) deduced from the TTF PDF [formula missing]. Uncertainty usually INCREASES the farther into the future you predict.
- LEARNING PARADIGM for TTF correction (Fig 6.10): correction term C_n = difference between current TTF estimate and previous one, at every iteration. Once p correction terms obtained, build a LINEAR REGRESSION MODEL relating all past correction terms; linear model estimates all FUTURE corrections to be applied IF the process is WIDE SENSE STATIONARY (WSS) → improves long-term prediction accuracy.
- EXAMPLE 6.1 Crack length growth in turbine engine blades: fault-growth model [formulas OCR-missing; state-space/L(N) evolution]: L = crack length (inches), N = number of stress cycles applied to material, P = random variable with KNOWN expectation, f = FIFTH-ORDER POLYNOMIAL derived from a FRANC-3D model (LOW-CYCLE-FATIGUE assumption), w(N) = I.I.D. white noise. Measurement model corrupted with Gaussian noise v(N): y(N) = L(N) + v(N). Result (Fig 6.11): TTF estimate corrected by learning paradigm (lighter shaded line) — prognosis CONVERGES TO TRUE VALUES as time increases. (No numeric error figures in text.)
- EXAMPLE 6.2 Crack growth in a planetary GEARBOX PLATE (helicopter): ANSYS used to determine crack-tip stress intensity factors for different crack sizes → crack growth rate via empirical equation based on PARIS model with an UNKNOWN parameter: dL/dN = C [ΔK_eff]^n [reconstructed; OCR formula missing] where n = material constant from tables. ΔK = "crack tip stress", often denoted ΔK_eff.
  - Stress profile: ΔK computed at different TORQUE values considering stress variations from combined effect of GROUND-AIR-GROUND (GAG) cycle shape + FIRST-HARMONIC component (magnitude validated with test baseline data).
  - Offline procedure generates long-term predictions from ONLY plate dimensions + material properties + initial crack condition; uncertainty of unknown parameter strongly reflected in predictions.
  - FIX: feed features from VIBRATION DATA into particle-filter framework (Fig 6.12): feature→crack-length NONLINEAR MAPPING generates noisy crack-length estimates from vibration data → identifies trend of failure evolution; with load profile knowledge + initial crack length, particle filter UPDATES ESTIMATION OF THE UNKNOWN PARAMETER → improves current crack-length estimate + long-term prediction from current particle population.
  - Measurement equation given: Feature(k) = L(k) + n(k).
  - Result: VERY ACCURATE crack-growth prediction after inclusion of 100 DATA POINTS (GAG cycles) of the vibration-based feature. Particle population evolution generates TTF PDFs for a given hazard zone (Fig 6.13) or for SEVERAL thresholds of interest (Fig 6.14); latter PDFs reflect directly the weight distribution among particles → also reveals the MOST PROBABLE PATHS the system will follow as time passes.

### 6.3 PROBABILITY-BASED PROGNOSIS TECHNIQUES (lines 4598-4614)
- When a complete dynamic model (differential equations relating I/O) is unnecessary or impractical: historical failure data for a given class of machinery has statistical form (Fig 6.15, each point = one previous failure instance). Probabilistic methods very effective there.
- Why: need LESS detailed info than model-based — prognosis info resides in PROBABILITY DENSITY FUNCTIONS (PDFs), not dynamic differential equations. PDFs obtainable from observed statistical data; PDFs sufficient to predict prognosis quantities of interest; methods generally also give CONFIDENCE LIMITS (feel for accuracy/precision).
- Hazard function (Chestnut 1965) = typical probability-of-failure curve = BATHTUB CURVE (Fig 6.16): very early life = relatively HIGH failure rate ("infant mortality"); after components settle = relatively CONSTANT and LOW rate; after some operation = rate increases again ("wearout failures") until all components failed.
- Complications: must account for MANUFACTURING VARIABILITY, MISSION HISTORY VARIATIONS, LIFE DEGRADATION (Fig 6.17, from Chestnut 1965) — all probabilistic effects. Must also take into account and REDUCE FALSE-ALARM PROBABILITY as far as possible.

### 6.3.1 Bayesian Probability Theory (lines 4616-4652)
- Uncertainty-handling families: Bayesian methods, Dempster-Shafer theory, fuzzy logic. Probability methods generally based on BAYES' THEOREM (Lewis 1986):
  - f_Y/X(y/x) = f_X,Y(x,y) / f_Y(y)  [reconstructed; OCR formula missing — Bayes rule for conditional PDFs]
  - Notation: f_X,Y(x,y) = JOINT PDF; marginals f_X(x), f_Y(y); conditionals f_X/Y(x/y), f_Y/X(y/x).
  - Marginals from joint: f_X(x) = ∫ f_X,Y(x,y) dy, f_Y(y) = ∫ f_X,Y(x,y) dx [reconstructed], integrals over ENTIRE region of definition of the PDF.
  - Mean/expected value of a random variable from PDF: E[x] = ∫ x f_X(x) dx [reconstructed]; conditional mean analogous with f_X/Y [formula missing].
  - CONSEQUENCE: all these quantities computable from the JOINT PDF → in applications, computing the joint PDF given available data is HIGH PRIORITY.
  - Fig 6.18 geometric meaning of marginalization ("integrate over x to project to y axis"); Fig 6.19 conditional PDF geometry.
  - Estimation interpretation (Fig 6.20): unknown quantity of interest = x, measured output = y; many decision-making techniques rely on f_Y/X(y/x) = LIKELIHOOD FUNCTION.

### 6.3.2 The Weibull Model: Analysis of Time to Failure (lines 4658-4724)
- Time-to-failure data for wide variety of engineered products fit WELL a Weibull distribution (Groer 2000; Schömig & Rose 2003) → considerable appeal in fault-prognosis community; used to predict RUL.
- THREE-PARAMETER Weibull (Weibull 1951), range gamma ≤ t < infinity [PDF formula OCR-missing; standard form F or f(t) with parameters]:
  - eta = CHARACTERISTIC LIFE; beta = SHAPE FACTOR; gamma = LOCATION PARAMETER.
  - gamma = 0 → two-parameter distribution.
- Definitions to keep straight: HAZARD RATE / instantaneous failure rate = failure rate normalized to number of equipment SURVIVING; FAILURE DENSITY / failure distribution function = failure rate normalized to ORIGINAL number of equipment.
- SHAPE FACTOR MEANING (memorize):
  - beta < 1 → hazard rate DECREASING
  - beta = 1 → hazard rate CONSTANT
  - beta > 1 → hazard rate INCREASING
- Bathtub curve = Weibull hazard with beta < 1 at wear-in, beta = 1 at steady, beta > 1 at wearout stages.
- Alternative two-parameter version (Groer 2000) with parameters alpha, lambda [formula missing]; related to first form by lambda = 1/eta and alpha = beta.
- Fitting failure data (times-to-failure or hazard rates) to Weibull: (a) parameter estimation methods (Lees 1996) — three principal methods: (1) LEAST SQUARES, (2) MOMENTS, (3) MAXIMUM LIKELIHOOD; or (b) BAYESIAN analysis treating model parameters as RANDOM VARIABLES.
- CAUTION: parameter estimation is a challenge for large-scale dynamic systems (gearboxes, gas turbines) — requires SUFFICIENT SAMPLE of actual failure data (time-to-failure recordings from extensive testing or actual historical operating records).
- EXAMPLE 6.3 (Groer 2000) Bayesian Weibull RUL estimation: failure-time data set D given as a list [list OCR-missing — numbers not recoverable]. Two-parameter Weibull failure density; likelihood of D given parameters alpha, lambda = product over all failure times [formula missing].
  - Bayesian step: treat alpha, lambda as random variables with PRIOR joint distribution p(alpha, lambda); posterior p(alpha, lambda | D) ∝ likelihood × prior [reconstructed]; integrate posterior over alpha → marginal for lambda and vice versa.
  - Fig 6.21: joint posterior density over grid alpha in [1, 15], lambda in [0.0003, 0.0004]. Fig 6.22: marginal densities for shape (a) and scale (b) parameters.
  - PREDICTIVE DENSITY: integrate posterior over BOTH parameters → predictive density of future failure time t_f conditioned on D [formula] (Fig 6.23). Parameter uncertainty incorporated because the integral considers ALL possible values of alpha and lambda weighted by p(alpha, lambda | D).
  - KEY NUMBERS: probability future failure occurs by t_f = 2500 is 0.34; EXPECTATION of t_f is 2650. Integrating predictive density over t_f over an interval = predicted failure probability for that interval.

### 6.3.3 Remaining Useful Life Probability Density Function (lines 4726-4758)
- Complete probabilistic viewpoint: ENGEL ET AL. (2000) — seminal paper clarifying RUL prediction. Key concept: REMAINING USEFUL LIFE FAILURE PDF.
- Component must be removed from service PRIOR to attaining a high probability of failure. Fig 6.24: RUL PDF with a JUST-IN-TIME removal point = 95 PERCENT probability that the component has NOT YET failed.
- KEY ISSUE: the RUL PDF is a CONDITIONAL PDF that CHANGES as time advances. Recompute the RUL PDF at EACH time t based on new information that the component has not yet failed (Fig 6.25): start with a PRIORI PDF similar to hazard function → recompute A POSTERIORI RUL PDF given failure has not occurred → involves RENORMALIZING the PDF at each time so area = 1.
- As time passes, VARIANCE of the RUL PDF DECREASES (PDF narrows): approaching the failure point → more and more certain about time of failure, prediction becomes more accurate (Fig 6.26 time evolution of RUL PDF).
- EXAMPLE 6.4 RUL prediction for SH-60 HELICOPTER GEARBOX (Engel et al. 2000) — full numbers:
  - Context: Navy program HIDS (Helicopter Integrated Diagnostic Systems) assisted evolution of automated diagnosis for helicopter mechanical systems.
  - Testbed: IRON BIRD test stand (SH-60). Fault seeded by implanting an ELECTRONIC DISCHARGE MACHINE (EDM) NOTCH in the GEAR TOOTH ROOT → localized stress concentration → crack formation & growth.
  - Run: 100 PERCENT TAIL POWER, total of 2 MILLION CYCLES. Terminated prior to gearbox failure when a GROSS CHANGE in raw FFT spectra observed on an HP36650 spectrum analyzer.
  - Data: recorded at 100 kHz, 16-BIT INTEGER precision, from TWO nearby accelerometers. TOTAL 36 RECORDINGS during run-to-failure, each 30 SECONDS long, spaced 15 MINUTES apart = rare nearly continuous view of gear damage progression from healthy to condemnable.
  - Postmortem: crack extended from tooth root THROUGH THE GEAR WEB, stopped at the BEARING SUPPORT DIAMETER.
  - Features: FOUR prognostic features traditionally used for gear fault detection; preprocessing: time-synchronously average accelerometer data (reduce noise + incoherent vibration from unrelated sources) → remove normally occurring frequencies (primary gear mesh frequencies + harmonics) → residue = TSAR (TIME SYNCHRONOUS AVERAGE RESIDUE). Four features: NORMALIZED KURTOSIS, RMS of TSAR signal, VARIANCE, PROPORTIONAL ENERGY — different ways of characterizing the residue.
  - Repeatability analysis: within each 30-s recording, 21 NONOVERLAPPING windows of 5 s each compute features; error bars = spread of these 21 values. If values not close → feature too brittle to extrapolate without further processing. Spread + uniqueness of value range = robustness measure.
  - TSAR PROPORTIONAL ENERGY (Fig 6.27): reasonably well behaved, LARGELY MONOTONIC, favorable first derivative throughout damage progression. RUL estimates computed at each recording time via BOOTSTRAP statistical methods; errors and distributions derived.
  - Temporal analysis: sequence of values healthy→failure for each feature modeled as a POLYNOMIAL; a SUBSEQUENCE OF FOUR CONSECUTIVE VALUES fit to polynomial model (least-squares sense) → expected remaining life. Fig 6.28: just-in-time point (using MAXIMUM LTI) for TSAR proportional energy vs time + actual remaining life; expected RUL and 95% CONFIDENCE INTERVALS vs time from PDF distributions of feature-generated predictions. Conclusion: as data accumulate and indications become easier to interpret, expected remaining life and leadtime estimates APPROACH the actual remaining life. (No numeric RUL error stated in text.)

### 6.4 DATA-DRIVEN PREDICTION TECHNIQUES (lines 4760-4772)
- Situation: historical fault/failure data as time plots of signals leading to failure, or statistical data sets; very difficult to determine any predictive MODEL → use NONLINEAR NETWORK APPROXIMATORS tuned by formal algorithms to map data → desired outputs directly.
- Two families: NEURAL NETWORKS (signal-processing in biologic nervous systems) and FUZZY-LOGIC SYSTEMS (linguistic/reasoning abilities of humans); both provide structured nonlinear function mappings with desirable properties.
- Fig 6.29: prognosis needs fault evolution prediction + CONFIDENCE LIMITS of prediction + prescribed HAZARD ZONES beyond which alarm activates; both prediction and confidence obtainable directly from data using neural networks.
- Evidence for ANNs in forecasting: Sharda 1994; Werbos 1988 — ANNs trained with backpropagation OUTPERFORM traditional statistical methods (regression, Box-Jenkins); Weigend & Gerhenfeld 1993 Santa Fe Institute forecasting competition — ALL WINNERS of each data set used ANNs.
- ANN character: data-driven, self-adaptive, very few assumptions about models; learn from examples, capture subtle functional relationships; well suited where data are easier to come by than knowledge; view as multivariate nonlinear NONPARAMETRIC statistical method (Cheng & Titterington 1994). MAIN PROBLEM: decisions not always evident (black box).
- CAUTION: standard statistical confidence estimation NOT directly applicable to neural networks. Confidence-estimation approaches surveyed:
  - Chryssolouris et al. 1996: assume normally distributed NN error → confidence interval.
  - Veaux et al. 1998: nonlinear regression for prediction intervals using weight decay to fit the network.
  - Leonard et al. 1992: "VALIDITY INDEX NETWORK" — extension of RBF networks that calculates confidence of its output.
  - Specht [Spetch in OCR] 1990/1991: PROBABILISTIC NEURAL NETWORK and GENERALIZED REGRESSION NEURAL NETWORK — built-in confidence estimation.
  - CONFIDENCE PREDICTION NEURAL NETWORK (CPNN) (Khiripet 2001): unique CONFIDENCE ESTIMATOR NODE takes confidence level from each pattern sample, constructs POSSIBILITY DISTRIBUTION (method similar to Parzen's distribution estimator); SPLITTING ALGORITHM splits a multimodal distribution into branches; ITERATED TIME-SERIES PREDICTION of branches → PREDICTION TREE whose branches = possible prediction trends; uncertainty managed via additional learning scheme that PRUNES the tree by eliminating unnecessary/inactive branches.

### 6.4.1 Neural Network (lines 4774-4844)
- Static feedforward two-layer NN (Fig 6.30; two layers of adjustable weights): inputs x_k, outputs y_i; activation function sigma( ) in HIDDEN layer; hidden weights v_jk, output weights w_ij; hidden thresholds theta_vj, output thresholds theta_wi; L = number of hidden neurons.
- Math form [formulas OCR-missing; standard structure from the text]: y = W^T sigma(V^T x) with weight matrices containing THRESHOLDS AS FIRST COLUMNS; input vector must be AUGMENTED BY A 1 for that to work; sigma( ) applied as augmented hidden-layer function vector = [1, sigma(w_1), ..., sigma(w_L)]^T type construct. y = [y_1 ... y_m]^T.
- Geometry: thresholds SHIFT activation function at node j; hidden weights SCALE the function. Typical activation functions in Fig 6.31 (sigmoid etc.; OCR fragment "1 + x 2" = tanh-family artifact). More detail: Lewis, Jagannathan & Yesildirek 1999.
- Learning = modifying weights so ANN accomplishes prescribed goals; without learning, no generalization from observed data.
- BACKPROPAGATION / gradient algorithm based on backpropagated error (Werbos 1988) — discrete-time tuning with time index t [formula OCR-missing; standard form]: desired output y_d in R^m for reference input x_d in R^n; NN output error E_t = y_d - y_t; F and G = designer-selected weighting matrices determining SPEED OF CONVERGENCE.
- sigma_d( ) = derivative of activation (easy to compute); sigmoid → hidden-layer output gradient = diag{sigma(.)[1 - sigma(.)]} form [formula missing; diag{} = diagonal matrix].
- Continuous-time backpropagation version exists [two formulas missing].
- HEBBIAN ALGORITHM (simplified tuning, continuous-time) [formula missing]: no need to compute sigma_d; weights in each layer tuned on OUTER PRODUCT of that layer's input and output signals. CAUTION: difficult to guarantee NN learning performance with Hebbian tuning.
- Practical: learning/tuning algorithms well understood, efficient, available in MATLAB. LEVENBERG-MARQUARDT used with feedforward networks for nonlinear estimation (Hagan & Menhaj 1994).
- LAZY/EAGER learning classification (Aha 1997):
  - EAGER (backprop, Hebbian etc.): data compiled into intermediate form (synaptic weights), then DISCARDED; description responds to requests.
  - LAZY (Atkeson et al. 1997): data NEVER discarded; the data ARE the model description; processing deferred until explicit request; based on NEAREST-NEIGHBOR + nonparametric statistics; aliases: memory-based, exemplar-based, case-based (Aha 1997), just-in-time learning (Cybenko 1996).
- REINFORCEMENT LEARNING: term from 1961 (Minsky 1961; Waltz & Fu 1965); mappings situations→actions maximizing a SCALAR REWARD criterion; learner not told which action, must DISCOVER which actions yield highest reward by trying (Sutton 1992). Combined with DYNAMIC PROGRAMMING (Bertsekas 1995): learner can take actions affecting not just immediate reward but next situation and through it all subsequent rewards (Sutton 1992). Variants: Q-LEARNING (Watkins [Watins in OCR] & Dayan 1992), TEMPORAL DIFFERENCES (TD) (Sutton 1988), ADVANTAGE LEARNING (Harmon et al. 1995). Bottleneck: enormous state/action space sizes → NNs approximate the reinforcement "COST TO GO" function = NEURODYNAMIC PROGRAMMING (Bertsekas & Tsitsiklis 1996).

### 6.4.2 Dynamic Wavelet Neural Networks (lines 4846-4857)
- Wavelet NN (WNN, Ch5) is a STATIC model (static input-output relation, signals flow forward only). Prognosis needs DYNAMIC/RECURRENT NNs modeling TIME EVOLUTION: signals flow forward AND backwards (feedback from output to input nodes).
- DWNNs proposed for prediction/classification; precedent: multiresolution dynamic predictor for multistep prediction of INTRACRANIAL PRESSURE signal (Tsui et al. 1995) using discrete wavelet transform + recurrent NNs.
- Structure (Fig 6.32) [formula OCR-missing]: DELAYED VERSIONS of input and output AUGMENT the input feature vector: y_k = WNN(u_k, u_{k-1..k-N}, y_{k-1..k-M}) [reconstructed] where u_k = external input, y_k = output, M = number of past OUTPUT values retained in memory, N = number of past external INPUTS retained in memory; WNN = the static wavelet NN.
- Example mapping: measuring angular velocity of a servo motor — y_k = velocity to be measured, u_k = regulating voltage controlling motor rotation at time k. Forms a RECURSIVE EVOLVING/PREDICTION MODEL dynamically mapping historical + current data into the future.
- Vs ARIMA/traditional: DWNNs offer more flexibility systematically in NONLINEAR MAPPING, PARALLEL PROCESSING, HEURISTICS-BASED LEARNING, EFFICIENT HARDWARE IMPLEMENTATION.

### 6.4.2 continued + EXAMPLE 6.5 Bearing Crack Size Prediction and RUL for an Industrial Chiller (lines 4858-4912)
- DWNN training: time-dependent way via gradient descent (LEVENBERG-MARQUARDT) or evolutionary (GENETIC ALGORITHM) (Wang 2001).
- Major DWNN advantage: input vector can mix SIGNALS OF DIFFERENT SORTS, even mixed TIME SIGNALS + FREQUENCY SPECTRA as functions of time → DWNN is a kind of INFORMATION FUSION DEVICE of great value in prognosis. Fig 6.33: DWNN fault predictor takes time-dependent features from sensor data + other info (fault dimensions, failure rates, trending info, temperature, component ID) → generates fault growth output.
- TESTBED: U.S. NAVY CENTRIFUGAL CHILLER (Fig 6.34) and its fault modes. Industrial chillers support electronics/communications on navy ships, computing/comms in commercial enterprises, refrigeration in food processing; diverse common components (pumps, motors, compressors); many failure modes (vibration-induced, electrical, process-related); well instrumented (vibration, temperature, fluid pressure, flow).
- Vibration symptoms: water pump vibrates if motor bearing defective, shaft misaligned, or mounting loose.
- FAILURE TYPE: rolling-element bearing with a CRACK IN ITS INNER RACE. Triaxial vibration collected via accelerometers (data from Shiroishi et al. 1997). Procedure: crack SEEDED → run motor, collect vibration → STOP motor, INCREASE crack size → second run → repeat until bearing FAILED. Crack sizes organized ascending; TIME information ASSUMED UNIFORMLY DISTRIBUTED among crack sizes. (Figs 6.35 vibration good vs defective; 6.36 PSDs top good/bottom bad.)
- FEATURES: raw vibration windowed, each window = 1000 TIME POINTS; features = MAX VALUE of vibration signal in each window (Fig 6.37) + PEAK/MAXIMUM VALUES OF PSD (Fig 6.38). Crack sizes during run-to-failure in Fig 6.39; intermediate crack sizes generated via INTERPOLATION to reduce number of test runs.
- Feature vector: (MaxSx MaxSy MaxSz) and (MaxPSDx MaxPSDy MaxPSDz) — max signal values and max PSDs on all three axes. MEXICAN HAT mother wavelets in WNN and DWNN.
- VIRTUAL SENSOR: WNN with SEVEN hidden nodes; inputs = max signal amplitudes + max PSDs; output = virtual crack size measurement (width and length) — matches true values very well (Fig 6.40).
- PREDICTION: DWNN trained using fault data UP TO THE 100th TIME WINDOW, then predicts feature evolution until final bearing failure; WNN maps feature evolution → crack growth. Predicted values match true values well (Figs 6.41 within 100th window; 6.42 beyond).
- HAZARD THRESHOLD (empirical evidence): CRACK WIDTH = 2000 µm OR CRACK DEPTH = 1000 µm. Crack reaches hazard condition at the 174th TIME WINDOW; the CRACK DEPTH criterion is reached FIRST.
- CAUTION: results illustrative only; practice requires a SUBSTANTIALLY LARGER DATABASE for storage, feature extraction, training, validation → sensitivity studies for conclusive DWNN capability claims.

### 6.4.3 The Confidence Prediction Neural Network (CPNN) (lines 4914-4974)
- Standard ANNs predict but do NOT provide confidence limits. GRNN (general regression neural network) basis: for known joint continuous PDF f(X,y) of vector input X and scalar output y, expected value E[y|X] computable [formula missing].
- PARZEN ESTIMATOR: GRNN estimates joint PDF with Parzen windows centered at training-set points. Estimated density from n samples: f_hat(x) = (1/n) sum_i W((x - X_i)/sigma) form [formula OCR-missing] where X_i = sample, sigma = SCALING parameter, W(d) = KERNEL function with largest value at d = 0. Kernels most often used: GAUSSIAN and CAUCHY.
  - Gaussian kernel joint-PDF estimate f_hat(X,y) [formula missing]: involves product of Gaussians over P = dimension of vector X.
  - Expected value y_hat(X) = E[y|X] evaluated as ratio of sums [formula missing] = WEIGHTED AVERAGE of all observed values y_i; scalar distance function D_i^2 = (X - X_i)^T (X - X_i).
- EXAMPLE 6.6 Parzen estimator for joint PDF: historical fault data (x, y) where e.g. point (13, 5) means: if vibration reaches 13 UNITS, time to failure = 5 HOURS; as vibration increases, time to failure decreases (Figs 6.43-6.46: data, Gaussian kernels at points, summed joint-PDF estimate, contour plot).
  - CAUTION: PDF estimate HIGHLY SENSITIVE to choice of variances of Gaussian basis functions. Basis functions Gaussian but estimated joint PDF NOT NECESSARILY Gaussian.
  - From joint-PDF estimate compute: conditional expected time to failure given current vibration, marginal PDFs, and the RUL PDF.
- GRNN CONFIDENCE INTERVAL via CONDITIONAL VARIANCE: variance LOW where training-set points have values similar to input; INCREASES where training-set points vary greatly from input values; confidence in estimate varies with variances of the points creating it [conditional variance formula OCR-missing].
- CPNN extends single number + confidence interval to full CONFIDENCE DISTRIBUTION:
  - One-step-ahead prediction: buffer of finite number P of recent values X = input vector; compared with patterns from historical data; each comparison gets degree of matching c(X, y_i) + candidate output y_i (same first step as GRNN's PDF estimate). Each candidate output weighted by degree of matching → final scalar confidence output.
  - CONFIDENCE DISTRIBUTION FUNCTION CD(X,y) defined via Parzen-estimator idea [formula missing]. Can be MULTIMODAL.
  - To simplify: keep the PEAKS of the distribution, one-step-ahead, as prediction outputs; iterate → MULTISTEP PREDICTION showing MULTIPLE TRENDS (prediction tree, Fig 6.47).

### 6.4.4 Managing Uncertainty via Neurodynamic Q-Learning (lines 4976-4986)
- CPNN output uncertainty GROWS WIDER in later prediction steps. Precision (narrowness of prediction distribution) = major prognostic performance metric → manage uncertainty using newly arrived actual data to validate most recent prediction step.
- EXTRA LEARNING MODULE prunes the prediction tree by eliminating unnecessary/inactive branches → fewer branches, less complex tree, BETTER PREDICTION PRECISION, and LONGER-STEP prediction possible.
- Analogy: CPNN prediction tree ~ GAME TREE; game state → set of actions; best actions → victory. Q-LEARNING (modified game-learning algorithm, reinforcement scheme): reward/punish an action after result observed; handles CONTINUOUS state and CONTINUOUS action space via NEURODYNAMIC approach.
- Wiring: CPNN serves as the "COST TO GO" FUNCTION of Q-learning; Q-learning updates CPNN by rewarding correct output branches. New actual data → correct branches EMPHASIZED, incorrect ones DEEMPHASIZED or ELIMINATED.
- REWARD constructed from FOUR performance measures: (1) ACCURACY = closeness of predicted to actual value; (2) PRECISION = narrowness of prediction distribution (narrower = less uncertainty); (3) CONFIDENCE = confidence level (0 to 1) AT the actual value; (4) COMPLEXITY = density of the prediction tree (how many branches). OVERALL performance measure = WEIGHTED SUM of the four; used both for improving CPNN prediction via Q-learning and for measuring CPNN effectiveness at end of prediction horizon.
- RL background: combination of dynamic programming + supervised learning; biggest advantage = MODEL-FREE aspect — applicability independent of the structure of the system considered.
- Maintenance interpretation: maintainer facing problem/symptom with multiple candidate solutions; RL system RECORDS problem–solution relationships + outcomes; over time leads maintainer to the most effective solution.

### 6.4.4 continued: RL formalism + Q-learning (lines 4988-5028)
- Primitives: S = discrete set of ENVIRONMENT states; A = discrete set of AGENT actions; R = set of SCALAR reinforcement signals.
- Loop: agent receives indication of current state s → chooses action a → action changes state s → during transition, scalar reinforcement r rewards/penalizes based on outcome → after numerous interactions, agent gains experience leading to optimal action for each state → a POLICY maps state → actions once learned. VALUE of a state = SUM of reinforcements over discrete number of interactions. OPTIMAL POLICY = mapping state→action maximizing sum of reinforcements.
- Q-learning advantage: while optimal state-action relationships unknown, agent may RANDOMLY select actions (arbitrary experimentation) while PRESERVING current best estimate state values; final results not contaminated by exploratory actions — they only ultimately reward/penalize state-action pairs. Requirement: agent must try each action in every state MULTIPLE TIMES for meaningful values.
- Q-LEARNING EQUATION [formula OCR-missing; standard form Q <- Q + alpha(r + gamma max Q' - Q) reconstructed with the paper's parameter semantics]:
  - Q = sum of all reinforcements for state-action pair (s,a) at time t
  - alpha = LEARNING-RATE parameter in [0,1]; gamma = DISCOUNT parameter in [0,1].
- alpha semantics: weights current vs previous knowledge. alpha→1: new experience outweighs previous; alpha→0: previous outweighs new. FOR MAINTENANCE TASK-EFFECTIVENESS state-action pairs: alpha set CLOSER TO 0 (previous maintenance-task history outweighs new experience).
- gamma semantics: weights the new state-action pair; in this application FIXED to a constant, only provides SCALING of state-action pair values, does not affect overall Q-learning results.
- Q-matrix: n × m matrix, n = number of possible states, m = number of possible actions (Fig 6.48 shows Q(s_i,a_j) grid, 3 states × 4 actions). Q(s,a) = task effectiveness of maintenance action a directly connected to failure mode s.
- STATE TRANSITIONS after a maintenance action (Fig 6.49 decision process flowchart):
  - Case 1: given failure mode s, if selected action SUCCESSFUL → transition from current fault state to HEALTHY state.
  - Case 2: if action NOT successful → transition from current fault state BACK to same fault state OR to a DIFFERENT fault state (transition to different faulty state may indicate the failure mode was not clearly identified until after the maintenance action was performed).

### 6.5 CASE STUDIES — 6.5.1 Gas Turbine Performance Prognosis (lines 5030-5062)
- Failure mode: FOULING DEGRADATION of gas turbine engine COMPRESSORS → significant efficiency loss → operational losses via increased fuel usage or reduced power output. Prognosis value: schedule maintenance on predicted condition → MINIMIZE UNNECESSARY WASHES, save maintenance dollars. Fig 6.50: effects of washing and overhaul on engine efficiency.
- Algorithm structure: data preprocessing + algorithms for current/future compressor condition. Data preprocessor examines engine operating data, automatically calculates key CORRECTED performance parameters (pressure ratios, efficiencies) at specific power levels.
- Classification: as fouling occurs in service, PROBABILISTIC CLASSIFIERS match parameter shifts to fouling severity levels from existing models/tests, with degrees of confidence.
- Parameter space = two multivariate PDFs / 3-D statistical distributions: (1) CURRENT CONDITION, (2) EXPECTED DEGRADATION PATH. BEST ESTIMATE of fouling = HIGHEST DEGREE OF OVERLAP between the two distributions (Fig 6.51: top view; top two plots = pressure ratio & fuel flow distributions; bottom two = joint probability distributions; dotted line = degradation path current/projected).
- Compressor efficiency inputs: compressor inlet temperature (CIT), outlet temperature (CDT), inlet total pressure (CIPT), discharge total pressure (CDPT); if total-pressure measurements unavailable, approximations with other sensor sets [efficiency formula OCR-missing].
- PREDICTION: actual engine-specific fouling rate combined with historical fouling rates via DOUBLE-EXPONENTIAL SMOOTHING — time-series technique weighting the TWO MOST RECENT data points over past observations (Bowerman & Koehler 1993) [smoothing equations OCR-missing].
- UNCERTAINTY HANDLING: MONTE CARLO simulation with mean and 2-SIGMA (measurement + modeling) uncertainties → resulting distribution = range of TIME-TO-WASH predictions; statistical confidence intervals identify the mean predicted value; estimate updated with WEIGHTED FUSION of predicted value + historical degradation level from fouling data (Fig 6.52). No numeric accuracy figures given in this case study.

### 6.5.2 Bearing Prognosis (lines 5064-5117)
- INTEGRATED approach: advanced OIL-DEBRIS monitoring + VIBRATION analysis + empirical/physics-based modeling; flexible enough to accept many diagnostic/prognostic input sources for better fault isolation + bearing RUL prediction.
- Architecture (Fig 6.53): oil-condition/debris monitor outputs + vibration signatures → ANOMALY-DETECTION/DIAGNOSTIC FUSION CENTER → triggering points in prognostic module enable TRANSITIONS between failure-mode models (spall INITIATION model → spall PROGRESSION model). Model-based + feature-based prognostic integration algorithms combine diagnostic sources via a PROBABILISTIC UPDATE PROCESS. Also ingested: bearing LOADING knowledge, historical failure-mode info, INSPECTION data feedback. Output: RUL + associated RISK passed to operations & maintenance decision support.
- Implementation diagram (Fig 6.54): oil-analysis monitor features + vibration features → anomaly/diagnosis module → PHYSICAL STOCHASTIC MODEL determines current "state of health" in terms of failure-mode progression → health rating probabilistically weighs current "LIFE-LINE LOCATION" in overall RUL; fused features ALSO serve as INDEPENDENT RUL measure incorporated in the "update" process → continuously updated health description + projected RUL estimate based on individual "signature" usage profile.
- EARLY FAULT DETECTION for rolling-element bearings (continuity with Ch5 §5.11 engine bearing case study): specialized features that detect INCIPIENT SPALL formation on race/rolling element = critical step.
- TEST RIG numbers: ball-bearing test rig (Fig 6.55), originally designed for lubrication testing, used for ACCELERATED bearing failures via spalling. Fault seeded in INNER RACEWAY via small hardness indentation (BRINNELL MARK). Load: approximately 14,234 N (3200 lbf). Constant speed: 12,000 rpm (200 Hz). Vibration: cyanoacrylate-mounted ("Super Glue") accelerometer sampled at OVER 200 kHz. Oil debris measured with MAGNETIC CHIP COLLECTOR (Eateon Tedeco [OEM spelling as printed]); oil data used to determine SEVERITY of spall progression.
- Bearings identical to NUMBER 2 MAIN SHAFT BEARING of an ALLISON T63 GAS TURBINE engine. TABLE 6.2 Test rig bearing dimensions (mm):
  - Bearing 1: ball diameter B_d = 4.7625; number of balls z = 8; pitch diameter P_d = 42.0624; contact angle = 18.5°
  - Bearing 2: ball diameter B_d = 7.9375; number of balls z = 13; pitch diameter P_d = 42.0624; contact angle = 18.5°
- Bearing characteristic frequencies computable from standard equations; FFT amplitude extraction at these frequencies often isolates fault to a specific bearing; high amplitude at any → fault in associated component. Frequency labels: BSF = ball spin frequency; BPFI = inner raceway frequency; BPFO = outer raceway frequency; Cage = cage frequency (Table 6.3 next chunk).
- HIGH-FREQUENCY ENVELOPING: characteristic frequencies easy to calculate but NOT easy to detect by conventional FFT — incipient-fault vibration amplitudes at those frequencies indistinguishable from background noise or obscured by much-higher-amplitude sources (engine rotors, blade passing, gear mesh). Bearing faults produce IMPULSIVE FORCES exciting frequencies WELL ABOVE background noise.
- IMPACT ENERGY feature (enveloping-based) four steps: (1) BAND-PASS FILTER raw vibration; (2) FULL-WAVE RECTIFY to extract envelope; (3) LOW-PASS FILTER to remove high-frequency carrier; (4) REMOVE DC content.
- Result numbers: applied to seeded-fault rig data with multiple band-pass/low-pass filters to probe possible rig resonances. Sample Impact Energy spectrum early in test (Fig 6.56) — data collected PRIOR to spall initiation (per oil-debris data), response due to the indentation alone. Conventional FFT (10 frequency-domain averages, Fig 6.57): NO peak at inner-race ball pass frequency (1530 Hz). Impact Energy plot: CLEARLY DEFINED peaks at 1530 Hz and second through fourth harmonics of inner-race ball pass. Peaks defined using a detection window of ±?5? Hz [OCR garbled "H115065 Hz" about the theoretical frequency — account for BEARING SLIPPAGE]. Conclusion: from the ONSET of the test there is an indication of a fault.

### 6.5.2 continued: tables, spall models, validation (lines 5118-5247)
- TABLE 6.3 Test rig bearing fault frequencies (Hz), at shaft speed 200: BSF = 512, BPFI = 1530, BPFO = 1065, Cage = 82.
- (Model-based analysis paragraphs at 5127-5133 repeat §6.2 intro text verbatim — note variant: combined model+feature methodology "consistent across different types of OIL-WETTED components"; Fig 6.58 prognostic bearing model approach.)
- SPALLING PHYSICS: rolling-element CONTACT FATIGUE = primary failure cause in properly loaded, well-aligned, adequately lubricated uncontaminated bearings. Contact fatigue flakes material off load-bearing surfaces of rolling elements and raceways → pit or SPALL (Fig 6.59). Spall starts as crack BELOW the load-carrying surface, propagates up to surface. Once initiated, spall grows RELATIVELY QUICKLY → high vibration + oil debris. Short remaining life after initiation → appearance of a spall = FAILURE CRITERION for bearings in critical applications.
- SPALL INITIATION model lineage: many theories predict initiation from bearing dimensions, loads, lubricant quality + few empirical constants:
  - LUNDBERG-PALMGREN (L-P), developed 1940s — basis of many modern theories.
  - IOANNIDES & HARRIS (I-H) 1985 — improved L-P by accounting for evidence of FATIGUE LIMITS in bearings.
  - YU & HARRIS (Y-H) 2001 — STRESS-BASED theory: simple equations determine fatigue life purely from induced stress; less dependence on empirical constants; remaining constants obtainable from ELEMENTAL testing (not complete bearing tests as L-P requires).
  - Y-H fundamental equation: relates SURVIVAL RATE S of bearing to a STRESS-WEIGHTED VOLUME INTEGRAL [formulas OCR-missing]; introduces new material property = STRESS EXPONENT c (material fatigue strength) + conventional WEIBULL SLOPE parameter for dispersion in number of cycles N. Fatigue initiating stress tau: via SINES multiaxial fatigue criterion (combined alternating + mean stresses) OR simple HERTZ stress.
  - Simple Hertz stress power law for stress-weighted volume: lambda = circumference of contact surface; a, b = major/minor axes of contact-surface ellipse. Yu-Harris exponent values for b/a ≈ 0.1: x = 0.65, y = 0.65, z = 10.61 (assumed INDEPENDENT of bearing material).
  - Y-H life L10 = function of basic dynamic capacity Q_c and applied load; LUBRICATION-EFFECT FACTOR accounts for film-thickness variation with temperature, viscosity, pressure [formulas missing]. Variables: A1 = material property; T = function of contact-surface dimensions; T1 = T when a/b = 1; u = stress cycles per revolution; D = ball diameter; rho = curvature (inverse radii of component); d = component (raceway) diameter; a*, b* = functions of contact ellipse dimensions.
  - STOCHASTIC Y-H model: based on Y-H theory, predicts probability of spall initiation in BALL/V-RING test; accounts for uncertainty in loading, misalignment, lubrication, manufacturing NOT in Y-H; inputs as NORMAL and LOG-NORMAL distributions → output = probability distribution over lives.
- SPALL PROGRESSION model: growth produces increased oil debris, high vibration, elevated temperatures → failure. Progression faster than initiation, BUT Kotzalas & Harris: 3 TO 20 PERCENT of a particular bearing's useful life remains AFTER spall initiation. Two progression regions: STABLE (gradual growth, LOW broadband vibration amplitudes) and UNSTABLE (onset coincides with INCREASING broadband vibration amplitudes).
  - Kotzalas-Harris model: spall progression rate dSp/dN related to SPALL SIMILITUDE W_sp via two constants C and m [formula missing]; W_sp defined via maximum stress sigma_max, average shearing stress tau_avg, and spall length Sp.
  - Data: ball/V-ring test device at PENNSYLVANIA STATE UNIVERSITY (Fig 6.60 "phase I" data): each line = one ball bearing's spall progression; one ball with multiple markers had test SUSPENDED periodically to measure spall length; other balls had only TWO measurements (initial + final). Figure shows LARGE DISPERSION of spall INITIATION life (lowest point of each line) and of spall PROGRESSION life (slope of lines).
  - Applied to the rig data: correlation between recorded OIL-PARTICLE QUANTITY and spall size determined from initial/final quantities + spall sizes → scaling oil-particle quantity to APPROXIMATE spall size; model agreed well with test spall progression (Fig 6.61).
  - STOCHASTIC Kotzalas-Harris model: same uncertainty accounting pattern (loading, misalignment, lubrication, manufacturing via distributions) → probability distribution of lives.
- PROGNOSIS MODEL VALIDATION: needs actual fatigue-life values vs predicted. CAUTION: bearing life under normal conditions often exceeds 100 MILLION CYCLES → normal run-to-failure testing impractical. ACCELERATED-LIFE TESTING: high speed, load, and/or temperature induce rapid failure; ball- and rod-type rigs.
  - RIG: UES, Inc. at AIR FORCE RESEARCH LABORATORY (AFRL), WRIGHT-PATTERSON AFB, Dayton OH (Figs 6.62 schematic, 6.63 photo): THREE 12.7-mm-diameter balls contacting a 9.5-mm ROTATING CENTRAL ROD; balls radially pressed by two TAPERED bearing races THRUST-loaded by three COMPRESSIVE SPRINGS. Two accelerometers on top: LARGER one auto-shuts-down test at threshold vibration level; other measures vibration for analysis.
  - TABLE 6.4 RCF tester dimensions (mm): rod diameter D_r = 9.52; ball diameter D_b = 12.70; pitch diameter D_m = 22.23.
  - LOADS: 222 N (50-lb) spring load → 942 N (211-lb) PER BALL on center rod (geometry). Hertzian contact, M50 bearing steel, 942 N radial → maximum stress ≈ 4.8 GPa (696 ksi). Stress so high that spall can initiate in LESS THAN 100 HOURS (depends on lubrication, temperature) → statistically significant failure counts quickly.
  - Validation tests: M50 rods + balls at ROOM TEMPERATURE 23°C. TABLE 6.5 RCF fatigue life results: 29 failures; 1 suspension (labeled "ball failed"); suspension time 83.33 [units as printed "cycles"; Fig 6.64/6.66 x-axis is millions of cycles, so almost certainly million cycles — OCR ambiguity].
  - MONTE CARLO bearing life distribution: inputs as normal/log-normal distributions (sample input distributions Fig 6.65); stochastic techniques account for model assumptions/simplifications/unknown variables.
  - YU-HARRIS model simulated the room-temp M50 RCF tests: test run at 3600 RPM, room temperature, 7808K lubricant [lubricant designation as printed]; y axis = number of central rod failures, x axis = millions of cycles to failure; PREDICTED life distribution superimposed (lighter shaded curve) computed with 1 MILLION MONTE CARLO POINTS (Fig 6.66).
  - Fig 6.67: median ranks of ACTUAL lives (dots) vs CDF of PREDICTED lives (solid line): model slightly MORE CONSERVATIVE (predicted life SHORTER than observed) once cumulative probability of failure EXCEEDS 70 PERCENT. Since bearings critical, main interest is the LEFT-MOST region (first failures) where model correlates BETTER.
  - MEDIAN RANKING: standard procedure for plotting failure data; handles tests stopped prematurely or failures of non-test-specimen components (suspensions) — those data give LOWER BOUND on fatigue life for the failure mode of interest. Method used: BENARD'S median ranking [equation OCR-missing]. On the RCF rig: significant portions of tests terminated WITHOUT failure after reaching 10 TIMES the L10 life; several tests ended because of spall on one of the BALLS rather than on the central rod (both count as suspensions w.r.t. the rod-spall failure mode of interest).

### 6.5.2 closing (lines 5258-5270)
- Median-rank bookkeeping variables [Benard formula OCR-missing]: AR = ADJUSTED RANK; N = number of SUSPENSIONS AND FAILURES. Adjusted-rank equation given separately [also missing]. Suspensions handled by adjusted ranking because time-to-suspension = LOWER BOUND on test-article life for the failure mode of interest (spall on inner rod).
- External-validity argument: rig does NOT simulate an actual bearing assembly in an engine, but simulates SIMILAR CONDITIONS — materials, bearing geometry, and lubricants are the SAME as in the T63 engine → rig results validate the model's ability to predict fatigue life of the MATERIAL under engine-like conditions.
- EXAMPLE BEARING PROGNOSIS DISCUSSION (synthesis of the whole chapter's fusion logic):
  - MODEL-BASED info predicts fault INITIATION before ANY diagnostic indicators exist → prompts "JUST IN TIME" maintenance to prevent development.
  - But modeling uncertainties mean incipient faults occasionally develop EARLIER than predicted → SENSOR-BASED diagnosis complements model prediction by UPDATING the model to reflect that fault initiation has occurred.
  - Sensor-based approaches = direct condition measures → update modeling assumptions, REDUCE RUL-prediction uncertainty. Subsequent RUL predictions then switch from fault INITIATION models to fault PROGRESSION models.

### 6.6 REFERENCES (lines 5272-5332) — SKIPPED per scope; anchors only
- Full citation list occupies 5272-5332 (Engel et al. 2000 IEEE Aerospace; Ioannides & Harris 1985 J Tribology 107(3):367-378; Kotzalas & Harris 2001 J Tribology 123(2):238-242; Yu & Harris 2001 Tribology Trans 44:11-18; Orchard/Wu/Vachtsevanos WTC2005; Wang & Vachtsevanos AI EDAM 15(4):349-365 2001; Shiroishi et al. MSSP 11(5):693-705 1997; Specht PNN 1990 / GRNN 1991; Weibull 1951; Werbos 1988; Watkins & Dayan Q-Learning 1992; Sutton TD 1988; Bertsekas & Tsitsiklis Neuro-Dynamic Programming 1996; Ljung 1999; Engel et al. "Prognosis, the Real Issues Involved with Predicting Life Remaining").
- Ch7 header "FAULT DIAGNOSIS AND PROGNOSIS PERFORMANCE METRICS" begins at 5334 (7.1 Introduction 355).

### META / OCR QUALITY NOTES
- Formula rendering: every display formula in this chapter came through as "<!-- formula-not-decoded -->" — no formula was OCR-readable. Structures above reconstructed from variable lists only, each flagged. Figures 6.1-6.67 all collapsed to "<!-- image -->".
- Tables 6.1-6.5 survived as OCR markdown tables and were transcribed (6.2 bearing dimensions, 6.3 fault frequencies, 6.4 RCF tester dims, 6.5 RCF results, 6.1 prognostic accuracy ladder).
- Garbles flagged: "H115065 Hz" (Impact Energy detection-window width, illegible); "7808K lubricant" (plausible FZG/MIL lubricant name but printed oddly); "Watins" = Watkins; "Spetch" = Specht; "Titerington" = Titterington; "Lees 1996"; Table 6.5 suspension time "83.33" printed under "(cycles)" but x-axis elsewhere is millions of cycles.
- Example 6.3 failure-time data list was inside a formula block → LOST, not recoverable from this text layer.
- Chapter ends mid-reference-free zone: last prose at 5270; 6.5.2 is the FINAL case study — 6.5 contains exactly two case studies (6.5.1 gas turbine compressor fouling, 6.5.2 bearing/spall), each captured above with all printed numbers.
- Duplication flag: paragraphs 5127-5133 (Model-Based Analysis for Prognosis) are a near-verbatim repeat of §6.2 ¶¶4416-4432 — the only new twist is "oil-wetted components".

## Nguyen Ch7 — Performance Metrics (source lines 5341-6104)

### 7.1 Introduction (5341-5352)
- Core question of Ch7: **How do we assess performance and effectiveness of CBM/PHM systems?**
- Key stance: no accepted metrics/specifications exist; must consider COMBINED impact of diagnostic + prognostic routines + cost/performance of the integrated system (monitoring of key process variables).
- Integrated CBM/PHM architecture elements: sensing; feature selection/extraction (characteristic indicators of fault presence); diagnosis of impending failure; prediction of remaining useful life (RUL)/time to failure (TTF).
- Three technical priorities: (1) select best features for the fault at hand; (2) diagnostic algorithms that detect/isolate/identify at earliest initiation stage; (3) accurate AND precise RUL prediction.
- Prognosis has unique challenges: inherent uncertainty of long-term predictions; metrics must account for uncertainty and confidence bounds on the prediction profile.
- Economic benefit anticipated from fleet-wide / system-wide practice where on-board + off-board share common equipment, data, methods.
- No military/commercial standards exist yet; reliance on "avoided cost" techniques to estimate potential costs/benefits; authors invite community dialogue toward standard metrics.

### 7.2 CBM/PHM Requirements Definition (5354-5371)
- Candidate generic requirement list for embedded CBM/PHM modules in critical military/industrial processes:
  - Enhanced maintainability, safety, reduced operations & maintenance (O&S) costs over life of critical system.
  - Open-system architecture: maximize ease of subsystem/component change, upgrade, replacement; minimize system/process interface change.
  - Weight must be closely controlled.
  - Reliability, availability, maintainability, durability (RAM-D) must be met; e.g. MTBF of the CBM/PHM system itself > x hours.
  - Health monitoring requirements: which faults, monitoring, display, communications, types/protocols tied to the process at hand.
  - Structural and environmental requirements.
  - Scalability requirements.
  - Cost requirements.
  - User requirements (display, GUI, etc.).
  - Power requirements.
  - Compatibility with existing sensors, components, devices.

#### 7.2.1 Fault Diagnosis and Prognosis Requirements (5373-5386)
- **Fault detection** requirement phrasing: system shall detect no less than a specific % of all mechanical system failures identified via Reliability Centered Maintenance (RCM) and Failure Modes Effects Criticality Analysis (FMECA). Detect degradation below required performance levels (incipient/impending failure) due to physical property changes through detectable phenomena.
- **Fault isolation** requirement: fault isolation rate to one or multiple organizational removable assemblies (ORAs) of x percent (e.g., 2 percent) for all faults detected by CBM/PHM. [2% example in source appears anomalously low for isolation-to-ORA rate; possible OCR/typo [OCR?] — usually phrased "isolate to x percent".]
- **Fault identification** requirement: defined w.r.t. impact of a particular fault on system's operating characteristics.
- **False-alarm rate** requirement: demonstrated mean operating range (e.g., flight hours for aircraft) between false alarms of a specific number of hours.
- **Built-in test (BIT)**: if system (avionics) has BIT, CBM/PHM diagnostic test shall complete end-to-end test within x-minute test period.
- **Prognosis requirements** phrasing:
  - Predict impending failures at 90% (threshold) and 98% (objective) confidence level (example numbers).
  - Prognostic module shall predict failures on life-limited components to enable part replacement with 10% (example) remaining life.
- **Critical Prediction Horizon (CPH)**: time between when prognostic system predicts impending failure (within required confidence limits) and when operator/maintainer can effectively act on failure and its consequences.
- Requirement: prognostic system shall function with maximum false prediction rate of x% (threshold) and y% (desirable).
- Diagnostic/prognostic requirements assembled into spreadsheet/matrix = Table 7.1 (content not in extracted lines 5341-5387; likely follows at 5388+ as table; check next chunk).

### 7.3 Feature-Evaluation Metrics (5388-5479)
- Premise: feature selection/extraction is the foundation of effective Dx&Px; raw sensor data → information processed accurately & expeditiously is a requirement, not a nicety. Questions: What are good features? How to compare features under varying operating conditions? Establish metrics BEFORE selecting "optimal" feature set.
- Challenge: feature set is a vector function of control variables/parameters (load, environmental conditions...).
- Objective of feature selection for fault classification and prediction: maximize classification accuracy (distinguish a fault condition from others and from healthy state as unequivocally as possible) while providing maximum prediction accuracy and precision.

#### TABLE 7.1 Diagnostic/Prognostic Requirements (5392-5398)
- Fault detection — Threshold: <75% of mechanical system failures monitored, <90% of mechanical systems identified through FMECA; Objective: NA. [Note: table rows read "less than" in OCR; requirement intent is presumably detect NO LESS THAN these % — table phrasing ambiguous [OCR?]]
- Failure diagnosis — Threshold: <75% subsystem isolation, <5% subsystem incorrect identification; Objective: <75% failure mode isolation, <5% failure mode incorrect identification. [same OCR caveat]
- Failure prognosis — Threshold: >1 day, >90% confidence; Objective: >7 days, >98% confidence. (i.e., prognostic horizon at least 1 day at 90% conf for threshold; 7 days at 98% conf for objective.)

#### 7.3.1 The Ideal Classifier (5400-5416)
- Need an "ideal classifier" to estimate predictive accuracy of a feature. Bayesian setup: true class C random variable over {c1..cd}; prior P(c_i); initial uncertainty = prior.
- Classification rule [reconstructed]: choose class c_i with greatest posterior probability: for feature value x_k, pick c_i such that P(c_i | X = x_k) = max_j P(c_j | X = x_k). (MAP / Bayes decision rule.)
- Error of feature X [reconstructed]: E[X] = Σ_k P(X = x_k) * (1 − max_i P(c_i | X = x_k)) — expected probability of misclassification under the Bayes rule (E = expectation over all values of X).
- Ranking features by this error is possible, BUT the Bayes error CANNOT be reduced by eliminating a feature → the technique cannot shrink a feature set to minimum size nor exclude redundant features.
- Obstacle: finite sample sizes rarely sufficient to estimate all probabilities/statistics → rely on nonideal classifiers to evaluate features and remove redundant ones.

#### 7.3.2 Information Measures (5418-5434)
- Uncertainty function U over true class: larger U = higher uncertainty (Liu & Motoda 1998 reference).
- Information gain of feature X [reconstructed]: IG(X) = U[P(c_i)] − Σ_i E[posterior uncertainty using X] i.e. IG(X) = U(prior) − Σ_k P(X = x_k) U[P(c_i | X = x_k)].
- Preference rule: choose feature X over Y iff IG(X) > IG(Y). A feature that cannot reduce uncertainty is irrelevant → remove from set.
- Common uncertainty function = Shannon entropy [reconstructed]: U = − Σ_i P(c_i) log P(c_i) (entropy formula, line 5432-5434 says "Shannon's entropy, that is," followed by undecoded formula).

#### 7.3.3 Distance Measures (5436-5452)
- AKA separability, divergence, distinguishability measures. Derived from distances between class-conditional density functions.
- Two-class preference [reconstructed]: choose X over Y iff D(X) > D(Y), where D(X) = distance/divergence between P(X|c1) and P(X|c2).
- Alternative: quantify overlap area of the two class-conditional pdfs (Fig. 7.1). Distinguishability measure d of feature X in two-class case [reconstructed for Gaussians]: d(X) = (μ1 − μ2)^2 / (σ1^2 + σ2^2) — squared mean difference normalized by combined variance [reconstructed; source says μ and σ^2 are mean/variance of feature distribution assumed Gaussian].
- Preference: X over Y if d_Y < d_X (line 5452 reads "Feature X is preferred over Y if d_Y > d_X" — direction implies d here measures overlap/dissimilarity inverse [OCR?]; interpret with care: prefer the feature whose two-class distributions are more separated).

#### 7.3.4 Dependence Measures (5454-5462)
- AKA association/correlation measures: quantify how strongly two variables are associated so knowing one predicts the other.
- Use #1: evaluate feature by how strongly it associates with class C (choose feature closely associated with C).
- Use #2: measure correlation between two features → remove redundant features.
- Example [reconstructed]: correlation between features X, Y (linear association): ρ(X,Y) = E[(X − μ_X)(Y − μ_Y)] / (s_X s_Y), with s_X sample standard deviation [undecoded formulas at 5458-5460].
- Worked example: if Y = X + 1, correlation = 1 (highest).

#### 7.3.5 Feature Evaluation: Two-Sample Z-Test (5464-5479)
- Assesses whether means of two groups statistically differ → measures distance between two distributions.
- Distance = difference between group means NORMALIZED by group variability (not raw mean difference).
- Fig. 7.2 (three scenarios, same mean difference, different variances): low-variability case → most distinct (little overlap); high-variability case → least striking (distributions overlap significantly).
- Z-test framed as **signal-to-noise ratio of the distributions** [reconstructed formula, standard two-sample Z]:
  Z = (μ_X1 − μ_X2) / sqrt(s_X1^2/n1 + s_X2^2/n2)
  (source text garbles: "s_X and are the standard deviation and mean of a distribution... n is number of incidences for each distribution").
- The computed Z value defines the distance between the distributions of a feature for two classes in a classification problem.

#### METRIC INVENTORY & LINKAGE
*(closing block; compiled from this file's content only — no new source reads)*
- **Fault detection rate** — % of mechanical-system failures detected, scoped by RCM/FMECA; TABLE 7.1 threshold row: <75% monitored / <90% FMECA-identified [OCR: requirement intent is "no less than"].
- **Fault isolation rate** — % of CBM/PHM-detected faults isolated to one or multiple ORAs (example x = 2 percent [OCR?]).
- **Fault identification accuracy** — defined vs. impact of the fault on operating characteristics; TABLE 7.1: <75% isolation, <5% incorrect identification (subsystem and failure-mode rows) [same OCR caveat].
- **False-alarm rate** — demonstrated mean operating range (e.g. flight hours) between false alarms.
- **BIT test completion** — end-to-end diagnostic test must complete within an x-minute test period (avionics with built-in test).
- **Prognosis confidence level** — predict impending failure at 90% (threshold) / 98% (objective) confidence; TABLE 7.1 horizon: >1 day @ >90% conf vs >7 days @ >98% conf.
- **Remaining-life replacement point** — prognostics predict life-limited-part failure to enable replacement with 10% (example) remaining life.
- **CPH (Critical Prediction Horizon)** — time from confident impending-failure prediction to when operator/maintainer can act on it.
- **False prediction rate** — prognostic module max x% (threshold) / y% (desirable) false predictions.
- **Bayes classification error E[X]** (7.3.1) = Σ_k P(X=x_k)(1 − max_i P(c_i|X=x_k)) — expected misclassification under the MAP rule; cannot be reduced by feature elimination.
- **Information gain IG(X)** (7.3.2) = U(prior) − Σ_k P(X=x_k)·U(posterior | X); X preferred iff IG(X) > IG(Y); uncertainty function = **Shannon entropy** U = −Σ_i P(c_i) log P(c_i).
- **Distance/divergence measure D(X)** (7.3.3) — distance between class-conditional densities P(X|c1) and P(X|c2); prefer larger separation (overlap area is the alternative).
- **Distinguishability d(X)** (7.3.3) = (μ1 − μ2)² / (σ1² + σ2²) [reconstructed for Gaussians] [OCR? preference direction d_Y vs d_X ambiguous at 5452].
- **Correlation/dependence ρ(X,Y)** (7.3.4) = E[(X − μ_X)(Y − μ_Y)]/(s_X s_Y) — used feature-vs-class and to prune redundant features (Y = X + 1 → ρ = 1).
- **Two-sample Z-test** (7.3.5, reconstructed) Z = (μ_X1 − μ_X2)/sqrt(s_X1²/n1 + s_X2²/n2) — inter-class feature distance as signal-to-noise ratio of the distributions.
- ⚠ **Coverage gap:** this file holds only 7.1–7.3.5 (ends at file line 82) although the header claims source 5341–6104; sections 7.4–7.7 are absent and the 7.7 public datasets are named nowhere in the file — deliberately NOT listed here (would be invented); follow-up pass over source ~5480–6104 needed to complete the inventory.
- **Link, diagnosis metrics → Ch5:** detection/isolation/identification %, false-alarm rate and BIT requirement score the Ch5 reasoners — fuzzy-logic + Dempster-Shafer fusion and wavelet-NN/filter-bank classifiers (5.4.x), Kalman/RLS parameter-deviation + particle-filter FDD (5.5.x), statistical change detection (5.9.1).
- **Link, prognosis metrics → Ch6:** 90%/98% confidence levels, >1-day/>7-day horizons, CPH and false-prediction rate score Ch6's TTF/RUL machinery — Weibull TTF (6.3.2), RUL-PDF (6.3.3), particle-filter failure prognosis (6.2.3), CPNN confidence prediction (6.4.3).
- **Link, feature metrics → Ch5/Ch6 intake:** IG/entropy, d(X), ρ and the Z-test grade the feature vectors those Ch5 pattern-library/classifier methods (5.3–5.4) and Ch6 data-driven predictors (6.4) consume — 7.3's premise that features are the foundation of effective Dx&Px.

## Nguyen Ch7 pt.2 — §7.4-7.5 Diagnosis & Prognosis Performance Metrics (source lines 5480-6008)

### 7.4 FAULT DIAGNOSIS PERFORMANCE METRICS

#### 7.4.1 Performance Metrics for Diagnostic Systems
- Headline metrics: false positives; false negatives; time delay (span between fault initiation and detection); percent isolation to one line-replaceable unit (LRU).
- Requirements phrased as % of total faults over subsystem life, e.g. "no more than 5% false positives and no more than 3% false negatives." Tradeoff favors STRICTER false-negative limit: missed faults risk catastrophic failure/loss of life; false positives only erode operator confidence.
- Time delay matters as early warning AND as the time window a prognosis algorithm needs to do its job.
- Decision matrix (Table 7.2, hypothesis-testing, after Liu & Motoda 1998), rows = Positive D1 (detected) / Negative D0 (not detected), cols = Fault F1 / No Fault F0:
  - a = detected faults; b = false alarms; c = missed faults; d = correct rejections.
  - row/col totals: a+c = all faults; b+d = all fault-free cases; a+b = all alarms; c+d = all non-alarms; a+b+c+d = all cases.
- Probability of detection POD = a/(a+c), given a fault (a.k.a. sensitivity) [reconstructed; formula OCR-not-decoded, terms per Table 7.2].
- Probability of false alarm POFA = b/(b+d) — fraction of fault-free cases that alarm [reconstructed; OCR gap].
- Accuracy metric uses ALL data (fault + no-fault): acc = (a+d)/(a+b+c+d) [reconstructed; OCR gap].
- Fault isolation = distinguishing failing-unit candidates after detection; metric = percent isolation to one LRU; coupled with fault identification (severity of fault impact) it tells the operator criticality + corrective action.

#### 7.4.2 The Receiver Operating Characteristic
- ROC answers "how well is a fault diagnosed?" as the detection threshold varies. Limitation: 2-D curve; higher-dimensional attributes can't be shown.
- Worked example (temperature diagnosis), 4 steps: (1) aggregate healthy vs faulty population histograms vs temperature; overlap band (book: 10-40 range) cannot conclusively separate. (2) For each threshold compute fraction correctly diagnosed — at threshold 20: 90% of truly failed parts diagnosed right (true positives), 50% of healthy wrongly alarmed (false positives). (3) Plot ROC: true-positive rate vs false-positive rate per threshold; straight line = 50/50 coin-flip; curves bowing left = better; accuracy A indexed by area under curve (AUC), grows as curve bends. (4) Pick threshold on curve: bottom-left strictest (few false positives, many missed), top-right most lenient (max discovery, many false alarms).
- Optimal threshold depends on: criticality of failure condition, prevalence in population, availability of corrective measures, financial/other costs of false alarms.

#### 7.4.3 Fault Severity, Detection Threshold/Confidence, and Complexity Metrics
- CBM/PHM performance is a function of fault severity; incipient faults/mild degradation are hardest. Ground-truth severity scale: 0 = healthy, 1 = unacceptable degradation.
- Success function S(s) = function of (average confidence − average severity) over time; works for Boolean or continuous confidence (Figs 7.7-7.8).
- Detection threshold metric: Detection threshold = 1 − S(s), success function normalized (stated in text). Confidence levels 67% and 95% (1σ, 2σ) used in its calculation.
- Overall detection confidence: computed from S(s) and C(s) (detection confidence at severity s) over full severity range [formula OCR-not-decoded]; high-confidence incipient detection scores high, detect-only-when-severe scores low.
- Stability metric: penalizes wildly fluctuating confidence; integrates peak-to-peak difference over the fault transition: ~ ∫ [C_H(s) − C_L(s)] ds with C_H/C_L = high/low confidence at each transition point [reconstructed; OCR gap].
- Detection duty sensitivity metric: difference between outputs under two load/duty conditions C1(s) vs C2(s), formulated over severity [formula OCR-not-decoded]; system must detect anomalies over full duty range (loads, speeds).
- False-positive confidence metric: frequency + upper confidence limit of false anomaly reports; based on false-positive function of Orsagh et al. (2000).
- Noise sensitivity metric: |C1(s) − C2(s)| where C1, C2 = success functions under two noise conditions [reconstructed from definitions; formula OCR gap].
- Implementation cost metric: cost to acquire + implement on a single application; shared costs divided across equipment. O&M cost metric: annual running cost (manual data collection, inspections, lab testing, archival, relicensing, repairs).
- Computer resource metric: normalized sum of CPU time (floating-point ops), static+dynamic RAM and source-code space, static+dynamic disk storage.
- System complexity metric: source lines of code (SLOC) + number of inputs required.

#### 7.4.4 Diagnostic System Classifier Performance Metrics
- Confusion matrix: square table, rows = classified-as, cols = actual defect; shaded diagonal = correct classifications (should dominate); entries in % or actual counts.
- Table 7.3 example (27 cases, 4 faults) as bullets: Collector Gear Crack row: 5/1/1/0 (tot 7); Quill Shaft Crack Prop.: 0/6/0/1 (7); Spiral Bevel Input Pinion Spalling: 1/0/5/0 (6); Input Pinion Bearing Corrosion: 0/0/1/6 (7); col totals 6/7/7/7=27.
- Probability of isolation / fault isolation rate (FIR) = % of all component failures isolated unambiguously: FIR = ΣA_i / Σ(A_i + C_i), A_i = diagonal (isolated), C_i = off-diagonal (not unambiguously isolated) [reconstructed; OCR gap]. For Table 7.3: Σdiag = 5+6+5+6 = 22 of 27 → FIR ≈ 81% [derived from table, not stated in book].
- Misclassification cost metric (general, handles unequal class costs and multiclass): MC = Σi Σj C(i,j)·CM(i,j) (normalized by case count per surrounding equations, not decoded) [reconstructed; OCR gap; C = cost matrix, CM = confusion matrix]. Downside: requires evaluating a cost matrix.
- Example 7.1 (IMATE aircraft-engine advisor, Ashby & Scheuren 2000): 6 hot-gas-path faults — FAN damage, COM compressor, HPT, LPT, CDP discharge pressure, VBV variable bleed valve leak; classifiers compared: multilayer NN (NN20/25/30 variants), fuzzy NN (FNN), CART.
- Fault criticality rank vector R (Table 7.4): NF 0, FAN 0.9, COM 0.8, HPT 0.8, LPT 0.8, CDP 0.1, VBV 0.1. Cost matrix (Table 7.5) built with m = 0.9, S = 100; off-diagonal costs run ~2.6-25.7 (e.g. NF→Fan 23.1, Fan→NF 25.7, CDP→Comp 18.0).
- Table 7.6 confusion matrices (per classifier, 7 classes incl. NF; diagonal = correct): CART diag 2074/2781/2577/2419/1864/2539/2547 (Σ=16801, big LPT↔NF/LPT↔HPT leaks); FNN diag Σ=14476 (LPT row worst: only 914 correct, 908 misread as HPT); NN20 Σ=17925; NN25 Σ=17979; NN30 Σ=17979 [diagonal sums derived by me from table; book ranks them in Tables 7.7-7.8].
- Tables 7.7/7.8: different R rankings → different cost matrices → different misclassification-cost and accuracy measures per classifier (results tables follow at 5735+).

#### 7.4.5 Statistical Detection Concepts
- Detection rests on feature separability between no-fault and faulted PDFs; POD ≥ 0.9 desirable but not always attainable. POFA and POD are COUPLED: both measured on the high side of the threshold — raising the threshold to cut POFA necessarily cuts POD (Fig. 7.12).
- Limited-data regime: assume Rician (noncentral chi) distribution for magnitude data — real/imaginary parts with means αQ, αI corrupted by independent Gaussian noise variance σ² → Rician PDF (Papoulis 1984) via modified 0th-order Bessel I0 [PDF formula OCR-not-decoded].
- Small samples (Westland seeded-fault set, Cameron 1993: 5 fault/no-fault sets per sensor): variance estimated with chi-squared (noncentral) approximation with user-defined confidence bounds; interval between (n−1)s²/χ² Upper and Lower bounds around true σ² [reconstructed; OCR gap]. Noncentral chi-squared PDF uses I_r(u), rth modified Bessel function; Impact Technologies implemented these PDFs in C++ (Bessel code adapted from Numerical Recipes in C; 0th-order Bessel used in chi-squared PDF, error < finite-arithmetic error).
- Worked results, Table 7.7 (R = [0, .9, .8, .8, .8, .1, .1]): misclassification cost / accuracy — CART 13.03 (#4)/85.57%; FNN 22.54 (#5)/73.73%; NN20 7.02 (#3)/91.29%; NN25 6.61 (#1)/91.57%; NN30 6.72 (#2)/91.57%.
- Table 7.8 (R = [0, .95, .01, .1, .01, .01, .2]): CART 6.29 (#2)/85.57%; FNN 14.25 (#5)/73.73%; NN20 6.68 (#3)/91.29%; NN25 6.75 (#4)/91.57%; NN30 5.83 (#1)/91.57%. Lesson: rankings shift with criticality vector R even though accuracy is classifier-invariant.

#### 7.4.6 An Architecture for Diagnostic Metrics Assessment
- MET (metrics evaluation tool): Impact Technologies + Sikorsky + Penn State ARL, under Boeing RITA HUMS project; demo = seeded-fault H-46 aft transmission data (Westland set) with gear/shaft/bearing algorithms; Oracle 8i + MATLAB, TCL glue over TCP/IP, client-server (data too big for client-side storage; algorithms stored as BLOBs like raw data; external-file pointers faster at scale).
- Westland 22-s data at 100k samples/s parsed into 4-s segments; ~98,000 field updates to raw-data table alone → automation mandatory. Directory scheme: ../CH46-Chinook/Aft Transmission/6 1 1992/Test ID/Raw.
- MET client tabs: metrics calculation (select algorithms/aircraft/systems/components/faults/features/loads/sensors); detection window (feature discriminability plot, thresholds from false-alarm criteria + user confidence bounds, then POD/POFA/accuracy computed at that threshold); sensitivity window (ROC = POD vs POFA vs threshold family; dark lines = theoretical Rician at various SNRs, light = analyzed data); summary window (save/print).

### 7.5 PROGNOSIS PERFORMANCE METRICS
- No agreed standard set of prognostic metrics; this class stems from prognosis objectives + the statistical (uncertain) nature of the algorithms. An algorithm must output predicted failure time (expected value) AND a confidence interval; measures weigh both interval width and closeness to truth, over many experiments; measures improve as data accumulate.
- Two dominant measures: ACCURACY (closeness of predicted to actual value) and PRECISION (how clustered the predictions are; involves confidence level + distribution of predictions across experiments).

#### 7.5.1 Accuracy
- Per experiment i: actual failure time t_af(i), predicted t_pf(i). Distance D_i = |t_pf(i) − t_af(i)|; D0 = application-scaled normalizing constant; N experiments.
- Accuracy at predicting time t_p: mean over i of an exponential exp(−α·D_i/D0) [reconstructed; OCR garbled fragment "e^(−αD_i/D_0)"; exponential chosen for smooth monotone decrease: =1 at D_i=0, →0 as D_i→∞; steepest slope near D_i≈0 → high measurement sensitivity around the truth, low sensitivity for gross deviations].
- Fig. 7.20: three evolution curves split at predict time; accuracy = 1 exactly when predicted = actual failure time.

#### 7.5.2 Precision
- Narrowness of the interval containing remaining life; high when predictions cluster, low when scattered over output range; average confidence-interval width counts too (narrower CI = higher precision).
- Prediction error E_i = t_pf(i) − t_af(i); mean and variance of E_i computed over N experiments [standard sample mean/variance; formulas OCR-not-decoded].
- Precision at t_p: exponential in normalized prediction variance (normalizer σ0²) and per-experiment confidence-interval width R_i (normalizer R0) [reconstructed; OCR gap]. Precision ∈ [0,1]: 1 = highest. Narrower confidence bounds + tighter clustering → higher value (Figs. 7.21-7.22).

#### 7.5.3 Timeliness of the Predicted Time to Failure
- Accuracy/precision ignore the TTF PDF's position on the time axis vs the actual failure event. Fig. 7.23, three cases: (a) failure occurs AFTER the predicted TTF PDF; (b) failure occurs DURING the prediction horizon = the desirable outcome for declaring the algorithm accurate; (c) failure occurs much EARLIER than predicted = undesirable, potentially catastrophic without immediate post-detection action (Hannah, 2004).
- Conclusion: accuracy and precision must be augmented with severity requirements on prediction timing — achieve case (b), at minimum avoid case (c).

#### 7.5.4 Prediction Confidence Metrics
- Two viewpoints: maintainer ("when to maintain, given spares etc.") needs RUL estimate + uncertainty bounds on the trending curve = earliest/latest maintenance windows + risk factor for delay; field commander ("are assets available for mission duration?") needs confidence of mission completion, or given confidence level → expected TTF.
- Prognostic curve must be modulated by a time-dependent distribution: statistical/Weibull or possibilistic/fuzzy. At t0: mean time to failure T_fm, earliest T_fe, latest T_fl; hazard line = fault magnitude where component ceases to be operational (Barlas et al. 2003).
- Confidence for mission length T′: ∫ from T′ to ∞ of the distribution = probability/possibility the asset survives the mission. Reverse problem: pick confidence (e.g. 95%), solve ∫ from T″ to ∞ = 0.95 for T″ = available time at that confidence. Dynamic evolution: new confidence limits as data arrive; uncertainty bounds shrink via learning routines. Future metrics: reliability of confidence limits, risk assessment, safety specs.
- Example 7.2 (bearing RUL, worked numbers): 2300 bearings; crack size at failure ~ discrete triangular (Table 7.9): 300 fail @0.7", 500 @0.85", 700 @1.0", 500 @1.15", 300 @1.3"; failure time ~ continuous normal; crack grows linearly from 0 at three rates. At T′ = 90 min, 2200/2300 had failed → confidence of NOT failing = 100/2300 ≈ 0.043 (4.3%). For 90% confidence: 0.9×2300 ≈ 2100 survive → T″ ≈ 40 minutes.

#### 7.5.5 Other Prognosis Metrics
- Similarity: compares multiple predicted time series against the real series from a start point to a future point; built from per-element differences of series x_i, y_i normalized by range (max_i − min_i over all ith elements) [reconstructed skeleton; formula OCR-not-decoded; Fig. 7.32].
- Sensitivity: response to input changes/external disturbances = ΔOut/ΔIn, distance measures of two successive outputs vs two successive inputs [ratio reconstructed; OCR gap].
- Prediction-to-failure times: mean TTF = (1/N)·Σ t_pf(i) over N experiments; standard deviation of prediction-to-failure time = sqrt of mean squared deviation from that mean [reconstructed; OCR gap].

### 7.6 DIAGNOSIS AND PROGNOSIS EFFECTIVENESS METRICS (source 6009-6051)
- Technology value = benefits across all failure modes it covers, minus implementation, O&M, and consequential costs of wrong assessments (Fig 7.33 grouping).
- Total value equation (formula block undecoded; structure from variable definitions [reconstructed]): TechnicalValue = Σ_modes [ P_f·(D·α + I·β) − P_D·φ − P_I·θ ]; TotalValue = TechnicalValue − ( A + O + P_c·δ ).
  - P_f = time-based probability of failure-mode occurrence; D = overall detection confidence score; α = savings from detecting before failure; I = overall isolation confidence score; β = savings from automated isolation; P_D = false-positive detection score; φ = cost of a false-positive detection; P_I = false-positive isolation score; θ = cost of a false-positive isolation; A = acquisition/implementation cost; O = life-cycle O&M cost; P_c = computer-resource requirement score; δ = cost of a standard computer system.
- Scoring convention: LOW score = undesirable, HIGH = desirable; hence a HIGH computer-resource score means the algorithm uses only a small share of resources.

### 7.7 COMPLEXITY / COST-BENEFIT ANALYSIS OF CBM/PHM SYSTEMS (source 6053-6104)
- Honest caveat in-book: no historical data yet exist for thorough economic analysis (technologies too new, few full-scale implementations) — studies use "avoided cost" reasoning instead.
- Overall performance = combination of (1) a complexity measure (formula undecoded; involves t_p = moment RUL is predicted and t_d = moment fault is detected), (2) cost-benefit analysis (maintenance frequency, downtime, dollar cost, etc.), (3) weighted overall performance (w_i weights, formula undecoded).
- Cost-benefit recipe, 6 steps: baseline condition from maintenance logs (BM/TBM costs + qualitative operational impact via interviews) → BM-cost reduction counted as CBM benefit → avoided time-based events (threshold failure probabilities + approximate TTF) counted as benefit → intangible benefits indexed (severe/moderate) via interviews → projected CBM cost estimate (instrumentation, computing, training, installation, upkeep) → aggregate life-cycle costs vs benefits.
- **Example 7.3 CINCLANTFLT "value of prognosis" study (numbers as printed):** U.S. Atlantic Fleet I&D maintenance cost $2.6B/yr (FY96$); fully integrated CBM assumed to yield 30% reduction; full realization in 2017 (S&T sunk cost included); full implementation costs 1% of asset acquisition cost; IT-21 (or equivalent) assumed already in place. Financial factors: inflation 4%, investment hurdle rate 10%, technology maintenance 10% of installed cost. **Results: NPV $337M over 15 yr, $1,306M over 20 yr; IRR 22% (15 yr) / 30% (20 yr).**
- NOTE for downstream: no public-dataset tables and no "60-second rule" exist anywhere in this chapter (an earlier distillation report falsely claimed Table 7.9 C-MAPSS datasets — that is NASA post-2008 literature, not this book). Datasets appear in later NASA papers, not here.

## Nguyen Ch8 — Product Support, Knowledge Base, CBM Scheduling (source lines 6137-6454)

### 8.1 Introduction (6137-6150)
- Product support & logistics = all processes, personnel, equipment, facilities needed to support a system during its intended life. Commercial usage: "customer/product support"; US defense/military: "logistics" — terms used interchangeably.
- Every system has design objectives: up-time (useful operating time) + cost targets. Tradition: preventive (scheduled) maintenance periods forcing shutdown or "standby" → downtime hurts commercial profitability / military "not ready" time. Rising pressure in both sectors to minimize downtime, operate cost-effectively.
- Enabler: operator needs continuous, accurate performance assessment + earliest possible awareness of performance-degrading faults → condition-based maintenance (CBM): sustain system/components WITHOUT arbitrary constraints of calendar time or operating cycles. Promise: higher up-time, lower cost — unnecessary preventive tasks eliminated.
- [OCR?] lines 6143-6146 are a mid-paragraph TOC fragment with chapter page numbers: 8.4→p405, 8.5 Maintenance Scheduling Strategies→p409, 8.6 A Simple Example→p410, 8.7 References→p416.

### 8.2 Product-Support Architecture, Knowledge Base, Methods for CBM (6152-6187)
- Product support = "system of systems" delivering information, material, and skilled labor to sustain operations of a (itself system-of-systems) supported system.
- Architecture (Figs. 8.1-8.2, notional): data developed from components/subsystems of supported system (aircraft, industrial process) shared across 4 support disciplines: ENGINEERING, MATERIAL DISTRIBUTION, MAINTENANCE, OPERATIONS.
- THREE ZONES OF ACTION (Fig. 8.2): (1) at the system/equipment; (2) at the support base for the equipment; (3) at the basic design engineering / product support center (OEM or cognizant technical organization responsible for life-cycle support). Capability for maintenance and modification gets DEEPER and BROADER further out the zones.
- Systems analysis + comprehensive FMECA (failure modes effects criticality analysis) determine how much/what extent of action is appropriate in each zone; intent: cost-effectively sustain system, optimal up-time level.
- KNOWLEDGE BASE (Fig. 8.3), three key sources:
  - Design engineering: initial system/component data — failure modes, failure MODELS (behavior of faults over time), operating mode behavior, data from development and operational testing.
  - Operations: data gathered during use — sensor/operational data (operating modes: speed, rpm, etc.), maintenance history, material consumption history.
  - Teardown analysis: detailed observations of failed equipment undergoing repair at service centers/repair providers.
- Diagnosis + prognosis only useful when turned into ACTION. First objective: give operator/technician the facts — fault in a specific component + system degrades beyond useful limits within a given period. But facts matter to full logistics spectrum: right information, material, equipment, skilled personnel at right place at right time.
- Accurate condition predictions affect 5 enterprise areas (named):
  - Operational planning/scheduling: enough life to complete next scheduled mission? industrial equipment last until weekly orders complete?
  - Spare parts/material procurement: is predicted useful-life-remaining notice sufficient for order-and-receipt lead time? if not, how much and which local inventory?
  - Operator training: failures from improper operation/servicing? what new procedures eliminate the failure mode?
  - Design: did actual life of failed components match design engineers' expectations? usage as anticipated? redesign required?
  - Financial performance: failures/out-of-service following operation estimates? system operating economically?
- Without structured condition assessment, support processes CANNOT predict future requirements. Current mode: gather what has happened + near-term scheduled events from enterprise/maintenance information systems; statistical analysis + data mining to discern failure/maintenance patterns → primary route to root causes → mitigation via new processes, training, more spares inventory, and last resort design change. Multidiscipline, multiorg → improvements incremental and generally slow.

### 8.3 Product Support Without CBM (6189-6195)
- Best current product-support systems often lack effective diagnosis/prognosis → lean on reliability-centered maintenance (RCM) (Moubray 2001; Narayan 2004).
- RCM: extensive statistical analysis of components (or similar designs) → set of maintenance processes + inspections minimizing unscheduled/corrective maintenance; well-established procedures for optimal inspection/maintenance INTERVALS from an assumed set of operating parameters.
- RCM weakness: reliance on average life expectancies + "average"/STATIC operating-profile estimates → maintenance sometimes performed BEFORE needed. Accepted widely because it does reduce unscheduled emergency repairs and aids planning/scheduling. Needs ongoing data collection/analysis to stay synchronized as system ages and usage changes.
- Three data impediments in current practice: (1) significant LAG between (increasingly automated, often manual) collection and analysis → weakens root-cause tracing; (2) data FLAWED — collection accuracy always secondary to repairing and restoring operation; (3) FRAGMENTED support network — operators + maintainers (often third-party labor/spares) + original design/support team → degraded or absent cross-boundary information sharing. Decisions based on flawed data → ineffective action.
- Summary: RCM & similar = calendar- or event-based task series; scheduled by operating hours/cycles REGARDLESS of system condition; scheduling optimizes downtime and cost (Helm et al., 2002). Works well with few operating modes + well-understood failure mechanisms; also NECESSARY for systems lacking sensors/data collection to understand condition.

### 8.4 Product Support With CBM (6197-6201)
- With reliable robust sensor + data collection + analysis network: replace calendar/event-based program with continuous condition assessment; maintenance/shutdown decisions = optimization of system condition vs operational requirements = CBM.
- CBM must be TESTED for effectiveness before adoption as established method for a specific system. Cost/complexity of sensors, signal processing, data management architecture must be weighed against up-time benefits and specific response times allowed by diagnosis/prognosis of components and failure modes.
- Some stable/durable systems need only a handful of sensors → CBM cheap. Others (fighter aircraft: highly complex, many interrelated failure modes) → CBM cost large, economic only via costly-inventory reduction or much smaller fleet size. Selection = positive economic analysis + meeting customer requirements.

### 8.4.1 How CBM Changes Operation and Product Support (6203-6213)
Four transformation vectors:
- Operational scheduling: CBM aware of failure modes × operating modes → can re-employ system to slow damage. Example: vehicle transmission flaw accelerated by high power settings / rapid power cycling → assign missions minimizing those accelerants → extend useful life remaining in the short run until corrective action demanded. Also modifies operator behavior: mandate smooth acceleration / minimal power changes; collected data VERIFY correct operation.
- Maintenance execution: accurate ULR predictions + associated maintenance actions → forward-looking optimization of resources/material. Instead of fix-after-discovery and racing with at-hand resources, tasks scheduled at OPTIMAL time matching operational requirements with personnel, parts, tool availability. "Maintenance control": reactive → resource optimization incl. time and money. Current maintenance information systems have limited optimization capability; optimization routines available off-the-shelf (cited web sites: cogz.com, maintstar.com, keeptrak.com).
- Supply-chain management (SCM): ULR as input to forecast algorithms in enterprise requirements planning (ERP) — insert forecast ULR as the LEAD TIME for the degrading component + dependent material needs. Coupled with serial-number tracking → break from average monthly/quarterly demand forecasts → targeted material requirements by operating location/unit, rolled up to total-requirement forecast. Failure-mode × operational-tempo data → less pipeline inventory without sacrificing availability. For repair-and-return-to-stock items (large portion of defense materiel): linking failure-mode data to serial-numbered component → faster repair turnaround, more effective piece-part consumption at designated repair point.
- Engineering/technical support: far more accurate failure-mode data to design/support engineers; systemic information sharing via CBM data-management architecture; nearly real-time engineering analysis shortens maintenance-process evaluation, material substitution, system redesign cycle.

### Example 8.1 + Tables 8.1/8.2: H60 Intermediate Gearbox Cost Analysis (6213-6260)
- Setup: maintenance replacement cost ≈ $39,800 (reorder cost with carcass credit of returned defective gearbox + labor + system checks). Three premature-failure-elimination methods: (A) disassembly + physical/visual checks; (B) periodic vibration sampling/analysis during ground ops; (C) installed HUMS data collection + condition analysis.
- TABLE 8.1 Component cost model (H60 intermediate gearbox) — all dollars:
  - Replacement: Material $37,500; Labor $800 (40 mhrs @ $20/hr, ground + flight crew); Other $1,500 ground turn (nominal $1500/flt hr); TOTAL $39,800; elapsed 12 hr average.
  - Method A disassembly/physical check: Material $200; Labor $400 (20 hr @ $20/hr); Other $1,500 ground turn; TOTAL $2,100; 8 hr average.
  - Method B special ground turn for vibration analysis: Material $20; Labor $120 (6 mhrs ground + flight crew); Other $1,550 (ground turn $1500 + 0.5 hr AED/AMC support); TOTAL $1,690; 3 hours.
  - Method C HUMS analysis: Material $10 (incidentals for data system); Labor $10 (0.5 maint mhr); Other $30 (amortized UH-60 fleet infrastructure cost per acft flt hr); TOTAL $50; 1 hour.
- TABLE 8.2 comparison of inspection methods (frequency in flight hours / annual cost / annual downtime hrs / availability / cost ratio):
  - A: 50 hr → 25,200 / 96 / 0.98904 / 0.633; 100 hr → 12,600 / 48 / 0.99452 / 0.317; 200 hr → 6,300 / 24 / 0.99726 / 0.158; 300 hr → 4,200 / 16 / 0.99817 / 0.106.
  - B: 50 hr → 20,280 / 36 / 0.99589 / 0.510; 100 hr → 10,140 / 18 / 0.99795 / 0.255; 200 hr → 5,070 / 9 / 0.99897 / 0.127; 300 hr → 3,380 / 6 / 0.99932 / 0.085.
  - C (HUMS): 50 hr → 600 / 12 / 0.99863 / 0.015; 100 hr → 300 / 6 / 0.99932 / 0.008; 200 hr → 150 / 3 / 0.99966 / 0.004; 300 hr → 100 / 2 / 0.99977 / 0.003.
- Punchline: HUMS gives substantially better up-time AND lower inspection cost (cost ratio 0.003-0.015 vs 0.106-0.633 for A). [reconstructed: cost ratio = annual inspection cost / $39,800 replacement cost; e.g. 4200/39800≈0.106 checks out for A@300hr, 100/39800≈0.0025≈0.003 for C@300hr.]

### 8.5 Maintenance Scheduling Strategies (6262-6266, start)
- Objectives: maximize equipment up-time, minimize mean time to repair (MTTR), optimize maintenance costs; optional extras: minimize logistics footprint/transportation if dictated by requirements + logistics network.
- Current logistics practice does NOT fully implement CBM: many orgs forbid ordering parts before removing defective ones (cost control + control of retrograde/defective parts for repair); orgs that do allow advance orders set them at much LOWER priority → effectively impede delivery at time of need.
- With CBM both objectives shift: LOGISTICIAN plans from prediction of asset condition (not updated historical material demands); MAINTAINER looks for optimal ways to COMBINE maintenance tasks — beyond the failing-component task, bundle other tasks worth doing while system is already inactive for repair.
- Prognostic algorithm supplies a PDF — probabilistic distribution of time to failure — and CBM data architecture adds availability of parts, technical data, maintenance personnel, special equipment/facilities. CBM objective: optimize up-time and availability, minimize maintenance cost, preserve system's operational integrity.
- Maintenance scheduling = CONSTRAINED OPTIMIZATION problem; widely researched, effective optimization tools exist. Challenges named: probabilistic/statistical inputs (TTF PDF, probability of parts availability, labor), multiobjective and possibly conflicting criteria, dynamic/evolving set of components in the optimization; objective function may NOT be smooth, differentiable, or unimodal; multiple constraints hard to account for and quantify.

### 8.5 cont. — Genetic Algorithms (6268-6270)
- Logistician's objectives are HYBRID: easily quantitative terms (MTTR, cost) + harder-to-quantify qualitative terms (e.g., repair quality) → calls for unconventional optimization methods. Off-the-shelf routines abound for fairly simple optimizations (many commercial).
- At higher complexity (more constraints, more complex input relationships): genetic algorithms (GAs) — emerging class that handles MULTIMODAL, possibly nondifferentiable objective functions; viable schedulers. Strength: search for global max/min; weakness: considerable time to solution. Differ from brute force by selectively rewarding most promising candidates → faster convergence toward global optimum. Mechanics: population members scored by a FITNESS FUNCTION; intelligent SELECTION decides survivors to next generation; genetic operators CROSSOVER and MUTATION combine/change members to generate new ones. Cited resources: lancet.mit.edu/ga/ (GA component library); Wikipedia GA article. NOT suitable for real-time applications where response speed is essential.

### 8.6 A Simple Example (6272-6346)
- Scenario: helicopter needs replacement of a line-replaceable unit (LRU) / drive-system component, replaceable by flight-line personnel. Required resources named: correct replacement PARTS, technical DATA (repair steps), TOOLS & special equipment, trained AVAILABLE PERSONNEL, a designated maintenance "SPOT"/place.
- Without CBM: logistician + maintenance supervisor REACT to unplanned replacement need → suboptimized patchwork preparation; repair task steps often INTERRUPTED while some other resource is obtained → longer MTTR + greater opportunity for error. With CBM: resources are lined up for the MOST OPPORTUNE time, arriving in SYNCHRONIZATION with task execution → more effective repair, shorter repair times.
- Modeling assumption: CBM data management architecture provides HIGH-CONFIDENCE remaining-useful-life prediction whose time span lets logistics + maintenance subsystems respond.
- THREE realistic constraints added to the scheduling optimization:
  1. Maintenance scheduled so there is 90 PERCENT certainty maintenance completes successfully in time for helicopter availability at a specified time (operational scheduling).
  2. At least TWO available maintenance "spots"/facilities at the specified time.
  3. Personnel availability limits how many people can be assigned to a task at any given time.
- Inputs = Figs. 8.4-8.8; generic time scale (operating hours vs calendar time not differentiated in example; real case must correlate/synchronize the two timelines).
  - Fig. 8.4 time-to-failure PDF from diagnostic/prognostic routines: failure predicted between t = 7 and t = 9; estimated time to failure set to the MEAN, t = 8. Hard schedule requirement for helicopter up-time: t = 10.
  - Fig. 8.5 current available personnel estimate; Fig. 8.7 available workbenches — curves show CURRENT availability, likely to change with other maintenance demand for this/other helicopters in the unit.
  - Fig. 8.6 logistic response time curve = probability needed parts are available PLANESIDE when maintenance is performed: 70% chance all parts available ON DEMAND (no prior notice); 85% available with 5 time units of LEAD TIME; rising to 95% at t = 10.
  - Fig. 8.8 probability task is completed as function of time and assigned personnel.
- Objective = optimize COST OF REPAIR. Simplified cost function, three terms: (1) parts availability, (2) number of personnel, (3) timing of repair vs probability failure will occur. Maintainer mantra cited: "Give me the parts, and I can fix the problem." Parts cost governed by availability: when unavailable, PREMIUM SHIPPING to point of need.
- Two CONTROLLABLE quantities: number of people assigned (n) and time maintenance is performed (t_f). Time to accomplish repair is fixed BY the 90%-confidence-before-t=10 constraint.
- Cost functional uses constants c1-c4 weighing each term (c2 raised to penalize staffing many people). [OCR? the equation itself appears as two "formula-not-decoded" placeholders at 6112-6114... err at 6312-6314 — actual formula NOT recoverable from text layer; structure known from prose only.]
- TABLE 8.3 arbitrary constant values: c1 = 5; c2 = 1; c3 = 25; c4 = .25. c3 ≫ c4 because c3 × (vanishing tail of TTF PDF) would otherwise be insignificant.
- Fig. 8.9 cost surface over (scheduled maintenance time, number of people). If maintenance impossible → cost = infinity; numerically defined as large value 25. OPTIMAL maintenance time found: t = 5.7, requiring AT LEAST THREE mechanics (task must finish before hard up-time with probability > 90%).
- TABLE 8.4 maintenance cost comparison (time / personnel / cost):
  - schedule ASAP: t = 0, 1 person, cost ≈ 2 (i.e., ≈ +2)
  - optimum: t = 5.7, 3 persons, cost ≈ -11
  - → scheduling as early as possible is significantly higher cost than the optimum (functional is relative; can go negative).
- Solver: simple SIMULATED ANNEALING (Ravi et al., 1997). Better than gradient descent here because the "spots" (≥2) constraint DIVIDED the solution space into two parts; gradient descent from a start outside the part containing the minimum finds only a LOCAL optimum; annealing introduces random effects so the search does not "get stuck" at a local minimum.
- General tooling note: Matlab (MathWorks, www.mathworks.com) and CPLEX (ILOG, www.ilog.com) provide efficient customizable optimization routines applicable to many scheduling problems.

### Boundary notes (verified while reading)
- 8.7 REFERENCES actually starts at line 6348 (not ~6400); 4 refs at 6350-6353 (Helm/Painter/Oakes WSC2002; Moubray RCM 2001; Narayan 2004; Ravi/Murty/Reddy, IEEE Trans. Reliability 46(2):233-239, 1997 — title OCR'd "Nonequillibrium" [OCR? likely "Non-equilibrium"]). SKIPPED per scope.
- Ch8 body ENDS with references; line 6355 begins "## APPENDIX — SOFTWARE FOR DIAGNOSIS" (book-level appendix, not Ch8 prose): Kalman filter MATLAB code, RLS MATLAB code, "TSA in the Frequency Domain" code (generated by Biqing (Becky) Wu, Sept 2005), then "## WEB LINKS — Labs and Organizations" (Georgia Tech ICsl, Impact Technologies LLC, U. Toronto CBM Lab, NCSU ADAC Lab).
- Lines 6397-6454: continuation of WEB LINKS appendix only (labs/orgs table cont.: U. Tennessee MRC, MFPT, MIMOSA, OSACBM, OSD CBM+; Reference Sites: COMADEM, reliabilityweb, DARPA JSF, NASA, Reliability Center Inc., plant-maintenance.com, IPPD; OEM sensor vendors: accelerometers (B&K, Wilcoxon, Sensotec), temperature/thermography, eddy-current probes, MEMS (Analog/Honeywell), fiber-optic (Luna, KEYENCE, Techno-Sciences); Wireless Sensor Networks: Crossbow, MicroStrain X-Link; Software Tools: ANSYS, ABAQUS, CPLEX). Not Ch8 content — no distillation. Last non-blank line before INDEX: 6453 "www.ilog.com/ products / cplex /" (6454 blank; INDEX heading at 6455).

#### 8.6 Coverage Check (source 6270-6355 re-read in one pass, this closing pass)
- The 8.6 section was NOT missing: the "## 8.6 A Simple Example (6272-6346)" block above predates this pass. One-pass source verification found every value in it matches the book; no duplicate section appended, no existing line edited.
- Verified line-by-line vs source: constraints 90% completion-certainty before specified up-time, at least two maintenance "spots", personnel-assignment limit (6280-6282); Fig. 8.4 TTF PDF predicts failure t = 7 to t = 9, estimate set to mean t = 8, hard up-time requirement t = 10, generic time scale caveat (6284); Fig. 8.6 parts availability 70% on demand (no prior notice), 85% with 5 time units lead, rising to 95% at t = 10 (6284); Figs. 8.5/8.7/8.8 personnel, workbenches, task-completion probability vs time and assigned personnel (6284, 6290-6302); three-term cost of repair + maintainer mantra "Give me the parts, and I can fix the problem" + premium-shipping rationale (6306); two controllable quantities n (people) and t_f (time), repair duration fixed by the 90%-confidence-before-t=10 constraint (6308, 6316); cost functional constants c1-c4, c2 raised to penalize staffing (6316); TABLE 8.3 (6320-6327): c1 = 5, c2 = 1, c3 = 25, c4 = .25, with c3 >> c4 because the vanishing TTF-PDF tail times c3 would otherwise be insignificant (6318); cost functional itself = two formula-not-decoded placeholders at 6312-6314, so structure is prose-only — existing [OCR?] tag stands; impossible maintenance = "infinity" cost numerically set to 25 (6329); optimum t = 5.7 requiring at least three mechanics to finish before hard-up-time with probability above 90% (6329); TABLE 8.4 (6339-6344): schedule-ASAP row t = 0 / 1 person / cost ≈ 2 vs optimum row t = 5.7 / 3 persons / cost ≈ -11, early scheduling significantly costlier (6331); solver = simple simulated annealing (Ravi et al., 1997), better than gradient descent because the "spots" constraint divided the solution space into two parts and gradient descent from the wrong part finds only a local optimum, annealing's random effects prevent getting stuck (6333); Matlab (MathWorks) and CPLEX (ILOG) general-tooling note (6346).
- Boundary re-confirmed: 8.6 body = 6272-6346; "## 8.7 REFERENCES" is at 6348 with 4 refs 6350-6353; the tasking's assumed 8.6 range "~6283-6400" was wrong; 6355 begins "## APPENDIX" as already noted.

