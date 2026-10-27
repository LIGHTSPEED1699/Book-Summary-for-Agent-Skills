# Puig & Simani (eds.) Vol 1 — Diagnosis (FDI) Methods: Structural, Set-Based, Stochastic, Data-Driven, Consistency-Based

**Diagnosis and Fault-Tolerant Control, Volume 1** (ISTE/Wiley 2021). Deep distillation from the full extraction. Verified chapter map: Intro+Ch1 (Puig/Simani survey + Simani FDI tutorial), Ch2 structural analysis (Krysander/Frisk — DM decomposition, MSO, DC-motor example), Ch3 set-membership/zonotopic FDI (Wang/Puig — quadruple-tank), Ch4 stochastic diagnosis as Bayesian inverse problem (Provan), Ch5 data-driven: Frisch/EIV + fuzzy identification (Simani), Ch6 knowledge-based & consistency-based diagnosis (Pulido et al. — Reiter/GDE + possible conflicts, three-tank). [formula-not-decoded]/[OCR?]/[reconstructed] tags throughout; nothing invented.

## Puig Vol1 Intro + Ch1 (Mathematical Modeling & Fault Description) — source lines 199-1781

### Introduction (Puig & Simani; pp. lines 199-~664)

#### IFAC SAFEPROCESS terminology as used by this book (verbatim where stated)
- Historics: 1st IFAC SAFEPROCESS Symp (Fault Detection, Supervision & Safety of Technical Processes) Baden-Baden 1991 (Isermann & Freyermuth 1992); seminal editions Isermann & Ballé 1997, Isermann 1997, Patton 1999; monographs Blanke et al. (2000? OCR merged), Basseville & Nikiforov 1993, Chen & Patton 1999, Gertler 1998, Isermann 1994b; surveys Gertler 1988, Frank 1990, Isermann 1994a. Basic defs also RAM dictionary (Omdahl 1988), IFIP contributions (IFI 1983). IFAC SAFEPROCESS TC tried to fix commonly accepted definitions.
- 1) States and signals: heading present but item lines missing from OCR [OCR?].
- 2) Functions:
  - Monitoring: "a continuous real-time task of determining the conditions of a physical system by recording information, recognizing and indicating anomalies in the behavior."
  - Supervision: "monitoring a physical system and taking appropriate actions to maintain the operation in the case of a fault."
- 3) Models:
  - Quantitative model: static+dynamic relationships among system variables AND parameters, quantitative mathematical terms.
  - Qualitative model: relationships among variables only, qualitative terms (causalities, IF-THEN rules).
  - Diagnostic model: "a set of static or dynamic relationships that link specific input variables, the symptoms, to specific output variables, the faults."
  - Analytical redundancy: "use of more (not necessarily identical) ways to determine a variable, where one way uses a mathematical process model in an analytical form."
- 4) System properties:
  - Reliability: ability to perform a required function under stated conditions, within a given scope, during a given period of time.
  - Safety: ability to operate without causing danger to persons, equipment or the environment.
  - Availability: probability that a system/equipment will operate satisfactorily and effectively at any point of time.
- 5) Time dependency of faults:
  - Abrupt fault: modeled as step-wise function; bias in monitored signal.
  - Incipient fault: modeled by ramp signals; drift of monitored signal.
  - Intermittent fault: combination of impulses with different amplitudes.
- 6) Fault terminology:
  - Additive fault: influences a variable by an addition of the fault itself (e.g., sensor offsets).
  - Multiplicative fault: product of a variable with the fault itself; appears as parameter changes within a process.
- (Detection/diagnosis/accommodation/reconfiguration definitions not yet in this chunk; intro continues.)

#### Data-driven robust FDI framing (intro)
- Robust FDI requirement: both system model AND disturbance distribution matrices must be known; lack of this info obstructed real applications. Book presents research on joint estimation of system and disturbance matrices to solve robust FDI.
- Data-driven parameter estimation split: errors-in-variables methods when all observed variables of a dynamic process are affected by uncertainties; equation error methods when plant variables exactly known (Simani et al.). Note: less attention historically paid to errors-in-variables schemes. Book uses both to build identified plant models under variable uncertainties, and compares data-driven estimates vs parameter estimates.
- Robust residual -> reliable FDI and FTC. Disturbance-decoupling approach's application domain very limited unless those problems addressed [specific unsolved-problem list OCR-dropped].

#### Data-driven diagnosis methods (classification/reasoning)
- Classification methods for symptom vectors: 1) geometrical distance & probabilistic methods; 2) artificial neural networks; 3) fuzzy clustering.
- Diagnostic models as symptom-fault causalities (symptom-fault trees, IF-THEN rules); vague facts -> probabilistic/fuzzy-set unified symptom representation; forward/backward reasoning -> probabilities or possibilities of faults.
- Approximate reasoning methods: 1) probabilistic reasoning; 2) possibilistic reasoning with fuzzy logic; 3) reasoning with ANNs.
- State-of-the-art claims (30 yrs): parameter estimation + observer-based = most frequently applied for fault detection (esp. sensor & process faults); ANN-based/combined growing; detection usually threshold logic or hypothesis testing; isolation often classification (ANNs growing); nonlinear models growing, linearized trend diminishing; analytical redundancy best in mechanical systems (precise models); most nonlinear processes = thermal & fluid-dynamic; chemical processes few but growing; "favorite linear process" = DC motor; trend shifting from safety-related many-sensor processes (nuclear, aerospace) to common processes with few sensors; diagnosis dominated by classification & rule-based reasoning.

#### FDI application report (literature survey 1991-2018, Tables I.1-I.6 as bullets; counts = number of contributions)
- Table I.1 applications: simulation of real processes 105; large-scale pilot 94; small-scale laboratory 68; full-scale industrial 98.
- Table I.2 fault types: sensor faults 129; actuator faults 111; process faults 123; control loop/controller faults 48.
- Table I.3 FDI methods: observer 123; parity space 74; parameter estimation 101; frequency spectral analysis 57; neural networks 79.
- Table I.4 residual evaluation: neural networks 89; fuzzy logic 65; Bayes classification 54; hypothesis testing 48.
- Table I.5 reasoning strategies: rule-based 40; sign directed graph 33; fault symptom tree 32; fuzzy logic 66.
- Table I.6 applications of model-based FD: DC motors 121; power plants/thermal 106; miscellaneous 102; combustion engine/turbines 96; milling & grinding 91; stirred tank reactor 77; navigation system 75; automotive 68; fluid dynamic 67; inverted pendulum 63; nuclear process 50.
- Findings: DC motor most-investigated; observer + parameter estimation ~70% of all applications; >50% of sensor faults detected by observer-based methods; actuator faults mostly observer-based, then parameter estimation and NNs.

#### From FDI to FTC + book roadmap (lines 499-560; OCR heavily merged around the FTC/fault-estimation figure; some sentences fragmentary [OCR?])
- FTC component designed on the basis of fault information from the diagnosis procedure to compensate fault effects; "fault estimation scheme" figure (Simani & Farsoni 2018 lineage).
- Unified framework: FDI/FTC formalized by mathematical description + definitions; methods require a process model in state-space or input-output form. State-space = general, mathematically rigorous tools for residual generator design: deterministic case (generalized observers: UIOs, output dynamic observers — Chen & Patton 1999, Frank 1990, Luenberger 1979, Watanabe & Himmelblau 1982); stochastic case (Kalman filters, unknown-input Kalman filters — Jazwinski 1970, Xie et al. 1994, Xie & Soh 1994). Disturbance-decoupling residual generators via UIO (Chen & Patton 1999; Liu & Patton 1998).
- No physical process knowledge required path: linear models from identification exploiting equation-error (EE) and errors-in-variables (EIV) models; identification per Frisch scheme (Frisch 1934, economics heritage) modified for dynamic systems (Kalman 1982b/1990; Beghelli et al. 1990) -> reliable plant model + input-output noise variances. Nonlinear case: fuzzy models and NNs as identification prototypes; multiple-model approach with several local affine submodels per operating condition.
- Residual definition (book's working definition): "the residual is defined as the output estimation error, obtained by the difference between the measurement of one output and the relative estimate."
- Diagnosis specialization: input-sensor/actuator FDI uses banks of estimators in high SNR, else filters; general principle: design the i-th reconstructor to be insensitive to the i-th system signal. Output-sensor and process-component faults affecting a single residual detected by output observers/filters driven by a single output + all inputs.
- Methodology: output-estimation approach + residual processing = simple threshold detection (deterministic) or statistical analysis (noisy data). Tested on time series from simulated + realistic industrial processes, energy conversion systems, power plants, safety-critical systems; minimum detectable faults "perfectly compatible with the industrial target".
- Volume map (14 chapters total): Vol1 Ch3 = set-based methods; Ch4 = stochastic FDI; Ch5 = data-driven "model-free" schemes; Ch6 = AI approach to diagnosis. Vol2 Ch1 = nonlinear analytical methods; Ch2 = LPV FDI+FTC for descriptor LPV systems with unmeasurable decision variables under actuator faults/perturbations; Ch3 = fuzzy Takagi-Sugeno + NN FDI/FTC; Ch4 = MPC for robustness+nonlinearity; Ch5 = nonlinear FTC methods (FTC component compensates fault effects from diagnosis info); Ch6 = virtual sensors/actuators for sensor+actuator faults, LMI extension to LPV; Ch7 = achievements summary for safety-critical systems; Ch8 = open problems/future directions.
- Note: explicit fault/failure/error and component/system-level definitions were NOT printed in the OCR stream for the intro lists ("States and signals" and part of "Fault terminology" lists OCR-dropped) [OCR?]. Intro closes: provided common terminology + outlined the 14 chapters; extensive bibliography lines 561-664 (Isermann/Frank/Gertler/Patton/Basseville-Nikiforov canon; Frisch 1934; Jones 1973 MIT thesis; Beard 1971 MVT-71-1 self-reorganisation; Willsky 1976 survey A.12(6) 601-611; Isermann survey Automatica 20(4) 387-404).

### Chapter 1. Mathematical Modeling and Fault Description (Silvio Simani; lines 665-1775)

#### 1.1 Introduction / 1.2 Model-based FDI techniques (scope: MISO/MIMO dynamic systems)
- Residual evaluation either threshold/decision logic or statistical methods: generalized likelihood ratio (GLR) testing, sequential probability ratio (SPRT) testing (Isermann 1997; Willsky 1976; Basseville 1988; Patton et al.).
- FDI scheme (Fig 1.2 "closed-loop FDI system", Fig 1.3 rearranged): monitoring via input u(t), output y(t), and controller signals uR(t), supposedly completely available for FDI. Controller behavior inherently taken into account. Caution: if uR(t) or plant inputs u(t) NOT available, controller matters — a robust controller may desensitize fault effects and make diagnosis difficult.
- Observation-problem view: true process signals u*(t), y*(t) usually unavailable; sensors measure u(t), y(t) -> FDI = observation problem on measured u,y (Fig 1.3 rearrangement).
- Fault location topology (Fig 1.4): faults can affect actuators; process/system components; input sensors; output sensors; controllers. Distinction input vs output sensors is explicit novelty vs earlier work (Patton et al. 1989/2000; Gertler 1998).
- Practical simplification (Fig 1.5): controller is treated fault-free (actuator is the fault-prone subsystem; digital control), so controller behavior + control-loop interconnection can be neglected in diagnosis-scheme design once measurements assumed available.

#### 1.2.x / "Mathematical description" — model formalism and fault models (formulas mostly not decoded by OCR [OCR?]; plain-text math captured)
- Process model: discrete-time, time-invariant, LINEAR state-space: x(t) ∈ ℜⁿ state, u*(t) ∈ ℜʳ actuator-driven input, y*(t) ∈ ℜᵐ real output not directly available; A, B, C from modeling or identification. (Equations [1.1]-[1.3] not decoded; standard x(t+1)=Ax(t)+Bu*(t), y*(t)=Cx(t) form implied [reconstructed].)
- Component (process) fault vector fc(t) enters dynamics additively; often a change in system parameters, e.g. entries of A: a change Δa in the i-th row, j-th column of A gives fc(t) = Ii · Δa · xj(t), i.e. Ii (n-vector of zeros with 1 in ith element) times parameter change times state element xj(t) — multiplicative fault rendered as additive vector via the state product [reconstructed from text].
- Sensor faults = additive signals: input-sensor fault vector fu(t) = [fu1(t) … fur(t)]ᵀ, output-sensor fy(t) = [fy1(t) … fym(t)]ᵀ.
  - Stuck sensor: outputs stuck at fixed value ū ⇒ u(t)=ū, fault fu(t) = −u*(t) + ū.
  - Multiplicative sensor fault δ: u(t) = (1+δ)u*(t) ⇒ written additively as fu(t) = δ·u*(t) (multiplicativity converted to additive fault description).
- Fault modes described by step and ramp signals: abrupt (bias) and incipient (drift, hard to detect) faults, matching intro definitions.
- Measurement noise: fault-free signals with additive noise ũ(t), y̅̃(t) = white, zero-mean, uncorrelated Gaussian processes; with faults+noise the fault-free equation [1.4] replaced by [1.5] (not decoded [OCR?]). Actuator block neglected; Fig 1.6 shows structure of the plant sensors.

#### Residual generator theory (1.3.x/1.4 "Residual generation", lines ~795-966)
- EE/EIV identification path repeated: no physical knowledge required; model from system identification based on Equation Error (EE) and Errors-in-Variables (EIV) models.
- Drawback of older FDI class: needs a priori signal characteristics; dependence of signal characteristics on unknown working conditions. Modern model-based contribution: symptom/residual signals that depend on faults and are independent of system operating states; represent inconsistency between actual measurements and model signals.
- General residual generator structure (Basseville 1988, Fig 1.8): auxiliary redundant signal z(t) = W1(u(·), y(·)); residual r(t) = W2(z(·), y(·)). Fault-free case: relations [1.6]-[1.8] hold (not decoded); with a fault r(t) ≠ 0.
- Simplest generator (Fig 1.9): W1 = identical plant model / input-output description from identification (e.g. ARX). As pure simulator (z = W1(u)) no y needed; r(t) = z(t) − y(t); open-loop so simulation may become unstable.
- Output-estimator extension: W1(u(·), y(·)) = M·y(t) estimation of a linear function of output; W2 = W(z(t) − M·y(t)), W = weighting matrix. Key claim: residual generation is nothing but a LINEAR MAPPING of process inputs and outputs, whatever the method.
- Transfer-matrix residual generator (Patton & Chen 1991a; Fig 1.10; eqs [1.11]-[1.15]): r(z) = Hu*(z)u*(z) + Hy(z)y(z), with Hu*(z), Hy(z) discrete transfer matrices designable as stable discrete-time linear systems; design constraints [1.15]: Hu*(z) + Hy(z)G(z) = 0 (fault-free cancellation) [reconstructed — exact form not decoded]; different parameterizations of Hu*, Hy yield the different residual generators (UIO/parity/… unification).
- Threshold decision: compare r(t) or residual function J(r(t)) with fixed threshold ε or adaptive threshold function ε(t); fault flag if J > threshold. Fixed ε works when process ~steady state and fault feature large (large sudden or long-lasting gradual). Adaptive ε(t) may depend on plant operating conditions, e.g. function of plant inputs (Clark 1989; Chen & Patton 1999).
- Focus: discrete-time dynamic linear models (both continuous/discrete exist in literature). Residual-generation scheme taxonomy (Isermann & Ballé 1997; Patton et al. 1989): 1) fault detection via parameter estimation (Isermann 1984, 1993; Isermann & Freyermuth 1992); 2) observer-based approaches (Beard 1971; Frank 1993; Frank & Ding 1997; Patton & Chen 1997; Willsky 1976; Basseville 1988); [3) parity equations — cut at chunk boundary].

#### Actuator faults + general fault model (fills gap lines ~717-794; formulas mostly not decoded [OCR?])
- [1.1]/[1.5]-type models = Errors-In-Variables models (Kalman 1982b, 1990) — recalled later in chapter (EIV/Frisch).
- Purely algebraic actuator (gain 1): u*(t) = uR(t) + fa(t), fa(t) ∈ ℜʳ actuator fault vector.
- If actuation signals u*(t) measurable (neglect sensor noise): process model with fault [1.6]-eq; Fig 1.7 critical case: uR measured only by input sensors — actuator faults cannot be directly related to input measurements u(t), detectable only via outputs y(t).
- General all-fault state-space model [1.10]: x(t+1) = Ax(t) + Bu(t) + L1 f(t) (+ noise), y(t) = Cx(t) + Du(t) + L2 f(t) + L3 f(t-1) [reconstructed structure]; f(t) = [faᵀ fuᵀ fcᵀ fyᵀ]ᵀ ∈ ℜᵏ; fault signals = unknown time functions; L1, L2, L3 = known faulty entry matrices describing how faults enter; u(t), y(t) available/measurable, supposedly known for FDI.
- Input-output transfer-matrix form [1.11]: y(z) = Gyu*(z)u*(z) + Gyf(z)f(z), z = unitary advance operator; Gyu*(z), Gyf(z) defined from state-space via C(zI−A)⁻¹B-type resolvents [reconstructed]. Models [1.10]/[1.11] widely accepted (Patton et al. 1989, 2000; Chen & Patton 1999; Gertler 1998).
- FDI performed on knowledge of measured sequences u(t), y(t) only.
- Frequency-domain descriptions used when faults/disturbances have distinct frequency characteristics (spectra as discrimination criteria) (Ding & Frank 1990; Massoumnia et al. 1989). State-space = rigorous for robust residual generation (deterministic & stochastic). A, B, C in canonical forms from multivariable identification (Guidorzi 1975; Norton 1986; Söderström & Stoica 1987; Ljung 1999). For MIMO, canonical state-space (Guidorzi) vs parity-space methods (Gertler 1995) may avoid unexpected false alarms (Delmaire et al. 1999).
- Novel stance: exploit linear identification procedures in connection with model-based residual generation (EE + EIV). Systems are actually nonlinear but linear models used for tractability; interest growing in nonlinear methods (nonlinear observers, EKFs, fuzzy), yet supervision vs expected operating point keeps linear methods very valid.

#### 1.5 Residual generation techniques — taxonomy + parameter estimation (1.5.1)
- Three process-model-based schemes: 1) parameter estimation; 2) observer-based; 3) parity vector (relation) methods (Chow & Willsky 1984; Gertler & Singer 1990; Patton & Chen 1991a; Gertler & Monajemy 1993; Delmaire et al. 1999).
- 1.5.1 Parameter estimation: parameters unknown/not exact -> estimate online from u(t),y(t) given model structure; assumption: faults reflected in physical system parameters; compare online estimates with reference-model parameters obtained fault-free; discrepancy => fault.
- 1.5.1.1 Equation Error (EE) (Fig 1.11): SISO discrete model order n in vector/regressor form: y(t) + a1y(t-1)+…+an y(t-n) = b1u(t-1)+…+bu(t-n) => y(t) = −θᵀy(t) + θᵀu(t) form with parameter vector and data vector [formulas not decoded]; EE e(t) = y(t) + Â(z)y(t) − B̂(z)u(t) [reconstructed; Z-domain e(z) = ŷ with Ā, B̂ estimates]; LS estimate from minimizing sum of squared EE; recursive LS (RLS) real-time form (Patton et al. 2000; Isermann 1992) with gain/Kalman-like recursion [not decoded]; Kalman filter for parameter estimation when measurements noisy (Jazwinski 1970).
- 1.5.1.2 Output Error (OE) (Fig 1.12): OE e(t) = y(t) − ŷm(t), ŷm model output from simulation with current parameters; direct LS of Θ impossible because e(t) is NONLINEAR in parameters; minimize loss function numerically -> much larger computational effort, online real-time generally impossible, but relatively precise estimates.
- Fault changes parameters by ΔΘ -> output change for small deviations Δy(t) = (∂G/∂Θ)ΔΘ [reconstructed] (eq [1.31] not decoded); estimator indicates ΔΘ.
- Parameters Θ depend on physical process coefficients p (stiffness, damping factor, resistance) via nonlinear algebraic equations Θ = g(p); if inversion p = g⁻¹(Θ) exists, Δp computable — often directly related to faults. Δp facilitates diagnosis (isolation/identification of physical fault) but NOT necessary for fault detection alone. Parameter estimation also applies to nonlinear static process models (Isermann 1993).

#### 1.5.2 Observer-based approaches (start)
- Estimate outputs from measurements: Luenberger observers (deterministic) / Kalman filters (noisy); output estimation error (or weighted value) = residual. For FDI, output estimation necessary, state estimation usually not needed (Chen & Patton 1999). Advantage: flexibility in gain selection -> rich variety of FDI schemes (Frank 1994b; Frank & Ding 1997; Chen et al. 1996b; Liu & Patton 1998).
- Generalized observer [1.34]: x̂(t+1) = Ax̂(t) + Bu(t) + H[y(t) − ĉ(t)], ĉ(t)=Cx̂(t)+Du(t) [reconstructed; figure 1.13 state & output dynamic observer]. State estimation error ex(t) dynamics: ex(t+1) = (A−HC... no: H output injection) [1.35]-ish; ex(t) and e(t) vanish asymptotically if observer stable via proper design of observer feedback H.
- With disturbances + faults (Fig 1.14, compare [1.10]): e_dynamics driven by L1 f(t), L2 f(t). The vector f(t) enters e(t) and x(t) by summation = additive faults. Sudden permanent faults => state estimation error deviates from zero. ex(t) and e(t) show DIFFERENT dynamic behaviors for L1f(t) vs L2f(t); both can be taken as residuals.
- Observer feedback matrix H design is the key to residuals with special properties (Chen & Patton 1999; Liu & Patton 1998). Noisy signals => Kalman filter instead of classical observers (Jazwinski 1970).
- Faults as parameter changes ΔA, ΔB (multiplicative faults, Isermann 1997; Patton et al.): process x(t+1) = (A+ΔA)x(t) + (B+ΔB)u(t) [reconstructed]; ex/e errors then depend on x(t), u(t) too — residual influence of parameter changes NOT as straightforward as additive f(t).

#### 1.5.2 observer configurations (cont.)
- Fig 1.14 MIMO process with faults and noises: v(t) = non-measurable input-side disturbance, w(t) = non-measurable output-side disturbance; f(t) fault signals at input/output acting through L1, L2 resp.; they can represent actuator, process, input- and output-sensor ADDITIVE faults. With v=w=0: ex dynamics and e(t) [1.39]/[1.40] not decoded; residual e(t) is the basis for output-estimation-based detection methods.
- Observer design limiting conditions: stability + sensitivity against disturbances v(t), w(t) [likely robustness AGAINST them — text as printed "sensitivity against"].
- Configurations taxonomy (Isermann 1997; Willsky 1976; Patton et al.; Chen & Patton 1999):
  1) Dedicated observers for MIMO:
     - one observer excited by one output; other outputs reconstructed and compared -> single output-sensor fault detection (Clark 1978);
     - bank excited by all outputs, several observers for a definite fault signal, hypothesis test (Willsky 1976);
     - bank excited by single outputs -> multiple sensor faults = Dedicated Observer Scheme (DOS) (Clark 1978);
     - bank excited by all outputs EXCEPT one (that one supervised) = Generalized Observer Scheme (GOS) (Wünnenberg & Frank 1987; Frank 1993).
  2) Fault (failure) detection filters: feedback H of state observer chosen so L1f(t) faults change residual in a definite DIRECTION and L2f(t) in a definite PLANE (Beard 1971; Jones 1973; Chen & Speyer 1999). Directional residuals: isolation = pick known fault signature direction nearest residual vector. Class of Luenberger observers with specially designed feedback gain; needs several measurable outputs; exploits internal analytical redundancy of multivariable systems; robustness improved vs parameter changes + unknown v,w (Patton & Chen 1994; Chen et al. 1996b "robust fault detection filter"; Chung & Speyer 1998). Post-filtering of OE [1.42] with special H design.
  3) Output observers / generalized observers incl. Unknown Input Observers (UIO) when state estimate not of primary interest; eigenstructure-assignment design of output observers for robust FDI (Chen et al. 1996b). Linear transformation of observer state -> residual via ṗ = …, r = v + … [formulas not decoded: [1.43]-[1.45]].

#### Coverage note for source gap (approx. lines 880-966 region)
- The read of chunk 967-1116 arrived compressed with a 140-line gap; partial recovery via locator returned lines ~717-966 (actuator faults, general all-fault model [1.10]/[1.11], canonical state-space vs parity, 1.4 residual generation, 1.5 taxonomy). The ONLY content not recovered = tail of 1.5.1.2 OE paragraph into 1.4 heading. Sections "## 1.3.1." (746) and "## 1.3.2. Mathematical description" (772) fully covered above. Any short bridge text between OE and 1.4 is [MISSING from extraction; not invented].

#### 1.5.2 (end) UIO principle + 1.5.3 Parity equations + 1.6 Change detection (lines 1187-1345, recovered full)
- Output-observer/UIO design goal: state estimation error and residuals r(t) designed INDEPENDENT of process states x(t), known input u(t), unknown inputs v(t) and w(t) -> residuals dependent ONLY on fault signals f(t) (Chen & Patton 1999; Patton & Chen 1994; Chen et al. 1996b; Gertler 1998; Patton et al. 2000). Fig 1.15 "process and output observer" (generalized observer).
- 1.5.3 Parity-equation-based FDI:
  - Idea: check parity (consistency) of acquired measurements. Early parity-vector work on static/parallel redundancy: Potter & Suman 1977 (aircraft static redundancy); survey Ray & Luck 1991. Hardware-redundancy relations: (a) identical/similar sensors for same variable; (b) dissimilar sensors for different variables with outputs related to each other (Potter & Suman 1977; Daly et al. 1979) — chapter focuses on ANALYTICAL redundancy.
  - Parallel-model method: model GM(z) = [Â(z) B̂(z)] run in parallel with process GP(z) = [A(z) B(z)] -> error vector r(z) = [Â(z)−A(z) B̂(z)−B(z)]·[u;y] + [fu; fy] type [1.47]-[1.48]; Fig 1.16(a) EE (b) OE. Model parameters/structure must be known a priori (as for observers).
  - Polynomial error [1.49]: r(z) = [1 + Â(z)] y(z) − B̂(z) u(z) [reconstructed] (OE-type parity = output-error parameter estimation eq [1.28]); [1.50] r(z) = [1+Â(z)]y − B̂u variant = equation error [1.21]. Different time responses for additive input vs output faults. Parity equations named per Gertler 1991 under assumptions of fault occurrence + exact process-model agreement; contrast: parameter estimation varies Â, B̂ to minimize residuals, parity keeps them known/constant.
  - Residual filtering: rf(z) = Gf(z) r(z) [1.51] (Gertler 1991; Patton & Chen 1994; Patton et al. 2000) -> design detection+isolation characteristics; [1.49]-[1.51] implement residual generation meeting FDI specs (Gertler 1998).
  - Limitation: SISO => single residual only, hard to distinguish faults; more design freedom if intermediate signals measurable (Fig 1.5) or MIMO.
  - Parity RELATION (Chow & Willsky 1984; Lou et al. 1986; Patton & Chen 1994; state-space extension for discrete models Gertler 1998): given system [1.52] x(t+1)=Ax(t)+Bu(t)+L1f, y=Cx+Du+L2f; substitute output into state eq and delay s times -> stacked V×(n+...) matrix eq [1.53] (V = parity matrix from A^i B blocks [reconstructed]); multiply by parity-space vector W with W·(state-controllability-like block) = 0 to remove non-measurable states -> parity vector/residuals r = W·[u; y] [1.54]-[1.55]; Fig 1.17 parity-EE MIMO; filtered vectors Uf, Yf from delayed signals. Design freedom in W -> structured residuals: pick W elements so one measured variable has NO impact on a specific residual; that residual stays small under additive fault on that variable, others increase (structured-residual / scheme logic per Patton & Chen 1994; Chen & Patton 1999).
  - Equivalence results: parity relation <-> observer correspondence (Massoumnia 1986; Wünnenberg 1990; Patton et al. 1989; re-examined Patton & Chen 1994): parity relation = DEAD-BEAT observer -> less design flexibility than unrestricted observers.
  - Delmaire et al. 1999 comparison (SISO then MIMO, linear discrete models): ARX/ARMAX identified IO forms suffer unavoidable PARAMETER REDUNDANCY -> multiple identifications of same parameters, inconsistent estimates -> inconsistent FDI decisions; fix: observers designed from identified CANONICAL state-space forms (Guidorzi 1975). Re-asserts observer-based FDI capabilities over parity schemes.
- 1.6 Change detection & symptom evaluation:
  - Step 2 = examine symptoms for fault occurrence; simple threshold test on instantaneous values or moving averages of residuals ([1.17]).
  - Statistical route: quantities as stochastic vectors r(t) = {ri(t)}, i=1..q with normal fault-free mean m_r and variance σ²_r [1.56 not decoded]; analytic symptoms = changes Δr(t) = r(t) − r_nominal [1.57]; tf = unknown fault occurrence instant (t > tf).
  - Fixed tolerance threshold Δrtol = ε·σ_r (ε multiplier) [1.58 reconstructed]; ε trades small-fault detection vs false alarms.
  - Change-detection tests: likelihood-ratio test / Bayes decision, run-sum test (Isermann 1984; Basseville & Benveniste 1986; Basseville & Nikiforov 1993); fuzzy or adaptive thresholds improve binary decision (Chen & Patton 1999; Patton et al. 2000).
  - Isolation/classification: symptom vector Δr ∈ q-dim space, direction depends on which fault; evaluation = determine direction + distance of Δr from origin; geometrical distance methods (Carpenter & Grossberg 1987; Tou & Gonzalez 1974) or ANNs (Himmelblau et al. 1991; Meneganti et al. 1998).
  - Generation + evaluation of analytic symptoms completes FAULT DETECTION within model-based FDI framework (Fig 1.8).

#### 1.7 Robust FDI: disturbance decoupling + H∞ (lines 1346-1427; heading text 1.7 = "Robust Fault Detection: Disturbance Decoupling Approach" [title not decoded, reconstructed] [OCR?]; 1.6 heading = "Change detection and symptom evaluation" already covered above)
- Central problem for FDI reliability: unavoidable MODELING UNCERTAINTY — process noise, parameter variations, nonlinearities. Accurate model => simple geometrical residual analysis suffices; real industrial systems always uncertain. Better model = better FDI precision; a method insensitive to modeling uncertainty relaxes need for accurate model. All uncertainties summarized as disturbances with UNKNOWN vector but IDENTIFIABLE distribution matrix -> disturbance decoupling principle applicable.
- Model with uncertainty [1.61] (Patton & Chen 1993): x(t+1)=Ax(t)+Bu(t)+L1f(t)+E1ε(t), y(t)=Cx(t)+Du(t)+L2f(t)+E2ε(t): ε(t) disturbance vector, E1/E2 known disturbance distribution matrices; ΔA, ΔB = parameter errors/variations = modeling errors. Transfer form [1.62]: y = Gu(z)u + Gyu(z)u? — with ΔGu(z) modeling-error term and Gε(z) disturbance term = together modeling uncertainty [details not decoded].
- Residual with uncertainty [1.63]: r(z) = [Hu*(z)+Hy(z)G(z)]u*(z) + Hy(z)Gε(z)ε(z) + Hy(z)ΔGu(z)(...) + Hy(z)Gf(z)f(z): terms Hy Gε and Hy ΔGu cannot be deleted (per [1.14]) -> faults AND modeling uncertainty both affect residual -> discrimination difficult.
- Disturbance decoupling principle [1.64]: Hy(z)Gε(z) = 0 (and Hy ΔGu term decoupled) -> total decoupling r vs ε. Achievers: UIO (Watanabe & Himmelblau 1982; Wünnenberg & Frank 1987; Chen et al. 1996b; Frank et al. 2000); optimal/robust parity relations (Chow & Willsky 1984; Lou et al. 1986; Wünnenberg 1990; Wünnenberg & Frank 1990); eigenstructure assignment (Patton et al. 1986; Patton & Chen 1991b/2000; Liu & Patton 1998; Duan et al. 2002). Patton & Chen vs Chow & Willsky contrast: C&W minimize modeling uncertainty over several operating points; P&C estimate optimum unknown-input distribution matrix over a range of operating points + eigenstructure assignment.
- Exact decoupling caveats: may be impossible (lack of degrees of freedom) and may even eliminate fault effect -> design criterion must include BOTH modeling error and faults: tradeoff fault-sensitivity vs robustness = multi-objective optimization (Chen & Patton 1999 ch.6): maximize fault effects, minimize uncertainty effects (Wünnenberg 1990; Frank et al. 2000). Optimal residuals = set of objectives (frequency-domain expressible); reformulated as inequalities on performance indices -> Genetic Algorithms (Goldberg 1989; Davis 1991) and LMIs (Boyd et al. 1994) search solutions (Chen et al. 1996a, 1997; Hou & Patton 1997; Chen & Patton 1999, 2001). Threshold selector concept (Emami-Naeini et al. 1988) also a robustness device.
- 1.7.1 FDI H∞ approach:
  - Minimize disturbance effect on residual = standard H∞ filtering problem (Chen & Patton 2000; Frank et al. 2000); H∞/H− index approach (Hou & Patton 1996, 1997).
  - History: early H∞ robust FDI via factorization approach (Ding & Frank 1990; Ding et al. 2000); advanced via Algebraic Riccati Equation (ARE) (Zhou et al. 1996); Mangoubi et al. 1992 first ARE solution via H∞/μ robust estimator synthesis (Appleby et al. 1991); direct FDI-as-robust-H∞-filter + ARE: Edelmayer et al. 1997; Niemann & Stoustrup 1996 modeling-error blocks in standard H∞ observer design + weighting factors; nonlinear extension treating nonlinearity as modeling error block (Stoustrup & Niemann 1998; Stoustrup et al. 1997).
  - Key distinction: robust RESIDUAL generation ≠ robust estimation — attenuation alone insufficient, residual must STAY sensitive to faults. Sauter et al. 1997: optimal post-filter on "primary residual" to enhance fault sensitivity. Sadrnia et al. 1997: iterate — design observer with very small disturbance-sensitivity bound via ARE, check fault sensitivity; if too small, relax robustness (increase bound), repeat; goal = maximum ratio fault-sensitivity/disturbance-sensitivity.
  - Chen & Patton 1999/2000: within standard H∞ framework minimize ||residual − fault|| w.r.t. disturbance+fault = replicate fault in residual -> indirectly maximizes fault sensitivity; modeling error handled directly in standard H∞ (or approximated as disturbance vector with estimated distribution matrix).
  - Approximate decoupling when [1.64] infeasible: performance index J = sup ||r|| / ||[ε; u]|| type (Ding & Frank 1991 [1.65]) evaluated via w-transformation (bilinear w = (z−1)/(z+1)) in frequency domain for discrete-data systems (Kuo 1995); [1.66] index min (Frank et al. 2000) widely accepted design objective (Basseville 1997); Ding et al. 2000 unified solution ~10 yrs after first proposal; H∞/H− detailed in Hou & Patton 1996/1997 + Frank et al. 2000; min over specified range in w-plane = approximate decoupling (Ding & Frank 1990; Patton & Hou 1997; Ding et al. 1999); time-domain approximate optimal decoupling (Wünnenberg 1990; Chen et al. 1993).

#### 1.7.2 Active and passive disturbance de-coupling (approx. lines 1429-1471, recovered)
- Modeling errors ΔGu(z) in [1.63] are harder to handle than measured-type disturbances. Two Patton & Chen techniques:
  - ACTIVE robustness (Patton & Chen 1994; Chen et al. 1996b, 1993; Frank 1996): take uncertainty into account AT residual-design stage by approximating modeling errors as disturbances: ΔGu(z)u(z) ≈ Gd(z)d(z), d(z) unknown vector, Gd(z) ESTIMATED transfer function; feed this approximate structure into disturbance-decoupling residual generator design -> robust FDI.
  - PASSIVE robustness: residual evaluator with ADAPTIVE threshold. Fault-free residual r(z) = Hy(z)ΔGu(z)u(z) [not decoded]; modeling errors bounded by δ (norm bound [not decoded]); adaptive threshold ε(t) generated by a linear (state-space) filter driven by u(t) [not decoded]: threshold no longer fixed, depends on input u(t) -> adaptive to operating point; fault if |r| > ε(t) (or J(r) > ε). Threshold adaptor/selector lineage: Clark 1989; Emami-Naeini et al. 1988; Ding & Frank 1991. "Passive" = no effort to design a robust residual.
- Honest limitation stated: disturbance-decoupling methods studied extensively but effectiveness on real problems NOT fully demonstrated — most modeled disturbances account for only a small percentage of real-system uncertainty; decoupling methods don't directly cover modeling errors. Practical way: estimate/approximate modeling errors + other uncertain factors AS disturbance terms with estimated distribution matrix; identification gives the distribution matrix used to design disturbance-decoupled residuals. (Intro/Ch1 roadmap for the book's own EIV-Frisch contribution.)

#### 1.8 Fault diagnosis technique integration + 1.8.1 fuzzy logic + 1.8.2 NNs (lines 1472-1531)
- 1.8: reliable FDI = proper INTEGRATION of several methods exploiting different procedures (Isermann 1994; Isermann & Ballé 1997); comprehensive approach = knowledge-based treatment of all analytical + heuristic information (integrated knowledge-based FDI).
- 1.8.1 Fuzzy logic for residual generation:
  - Two-stage model-based FDI: residual generation (inputs/outputs -> residuals) + decision-making (quantitative residual info -> qualitative faulty/normal statements). Model precision limits detection/isolation accuracy + diagnostic sensibility; most real processes nonlinear, single model can't cover all operating conditions; some nonlinear systems impossible to describe analytically; when structure/parameters imprecise and diagnosis relies on heuristic info, no qualitative model set up -> fuzzy theory natural tool for complicated/uncertain conditions (Babuška 1998).
  - Alternative to complicated nonlinear models: plant as COLLECTION of LOCAL AFFINE fuzzy and non-fuzzy models (Leontaritis & Billings 1985a,b; Takagi & Sugeno 1985) with identified parameters (multiple-model, ties to intro).
  - Noise/uncertainty makes residuals fluctuate ≠ 0 even fault-free -> can hide fault effects; fuzzy logic handles vague/imprecise facts where complete info unavailable; fuzzy expresses expert knowledge as rule-based format; fuzzy improves the yes-no decision stage of residual evaluation (Ulieru & Isermann 1993; Frank 1994a; Meneganti et al. 1998).
  - Rule-based expert systems intensively investigated (Rich & Venkatasubramanian 1987; Kramer 1987; Patton et al. 1989/2000): need rule database, diagnosis accuracy depends on rules; building rich database time-consuming, needs many process experts.
  - Fuzzy approach acts at TWO levels: fuzzy descriptions generate symptoms AND fuzzy logic performs FDI (Dexter & Benouarets 1997; Isermann 1998).
- 1.8.2 Neural networks:
  - Quantitative model-based diagnosis gives symptoms from analytical knowledge — usually insufficient to indicate fault LOCATION and MODE. Integrated system: analytical knowledge -> residual generation; heuristic knowledge -> feature extraction; then inference mechanism = residual evaluation + symptom observation + pattern recognition. Pattern recognition convenient for fault identification (determine SIZE of fault) when model only partly precise (Himmelblau 1978; Pau 1981).
  - NN assets: handle nonlinear behavior + partially known processes via training data; noise-tolerant; generalize; adapt during use (Hoskins & Himmelblau 1988; Dietz et al. 1989; Venkatasubramanian & Chan 1989; McDuff & Simpson 1990; Chen et al. 1990).
  - Caveat: NN trained to identify fault from measurement patterns — classification of individual measurement pattern NOT always unique in dynamic situations -> straightforward NN-on-raw-patterns impractical for dynamic plants; instead NN finds (a) dynamic model of monitored system (then residuals = model outputs) or (b) connections from faults to residuals (pattern classifier / nonlinear function approximator). Book uses fuzzy + non-fuzzy model identification + NN as function approximators.
  - Quantitative vs qualitative approaches: complementary; combine to increase robustness of quantitative techniques; main research aim = proper combination for highly reliable diagnostic information.

#### 1.8.3 Neuro-fuzzy (NF) approaches to FDI (lines 1532-1560)
- Multivariable process identification = approximation of input-output mapping; traditional models sensitive to modeling errors, parameter variation, noise, disturbance. NN: universal approximator (nonlinear, even dynamic) with suitable weights/architecture; online training adapts FDI to process/controller changes; generalizes to unseen inputs, intelligent with noisy/corrupted data; multivariable-ready; highly parallel -> higher fault tolerance; works on qualitative AND quantitative data; useful when NO mathematical model available. Dynamic elements (filters, delays) combinable.
- NN weaknesses: "black box" — no qualitative/quantitative info about the represented model; engineers/operators want to see rules; ambiguous performance in unexpected situations (Korbicz et al. 1999). Fuzzy strengths: mimic human operator sensing/generalizing/processing/operating/learning; linguistic model via rules; inherent handling of imprecise/noisy data.
- Fuzzy neuron = artificial neuron with some/all components & parameters described by fuzzy logic; fuzzy NN = built on fuzzy neurons or standard neurons with fuzzy data; connectionist model for implementation + inference of fuzzy rules (Chiang et al. 2001; Nelles 2001).
- Three common NN-fuzzy combination methods: 1) fuzzification of NN inputs/outputs; 2) fuzzification of interconnections of conventional NNs; 3) NNs inside fuzzy models providing membership functions + rule base.
- B-spline NF networks: identify process with NN architecture while extracting qualitative knowledge; include operator heuristic knowledge; simple easy-to-build framework (Uppal & Patton 2000). NF applications successful from industrial processes to financial systems (Wu & Harris 1996; Ayoubi 1995) — but implementation depends heavily on prior knowledge + training data.
- NF for FDI (Uppal & Patton 2000 scheme): once NF structure/params identified -> residual generation + decision making (classification). Fault classes known a priori with data available: M fault classes -> network output vector dimension M+1 (M fault models + healthy/nominal model). Training: decompose into (M+1) MIMO sub-models, optimal weighting coefficients per sub-model. Test point {u(t),y(t)}: nominal condition -> all outputs zero EXCEPT the last (nominal model); specific fault i -> output i deviates from zero and output i+1 (nominal) becomes zero => system no longer healthy. This is multiple-model NF residual+classification architecture.

#### 1.8.4 Fault detectability and isolability + NF model taxonomy (recovered)
- Detectability: successful detection needs residual with MAXIMAL sensitivity to the fault; detectability conditions per Chen & Patton (1999). Isolation follows: distinguish a particular fault from others; ONE residual suffices for detection but a residual VECTOR is required for isolation; faults isolable iff each residual is sensitive to a SUBSET of faults and insensitive to the rest -> structured residual set design.
- NF structures: combine numerical + symbolic knowledge in one framework; automatic linguistic rule extraction useful with little/no prior knowledge (Brown & Harris 1994; Jang & Sur 1995); NF model of nonlinear dynamical system from empirical data -> insight into nonlinearity/dynamics.
- Two fuzzy-model families under NF: TSK (Takagi & Sugeno 1985; Sugeno & Kang 1988) local LINEAR consequents -> interpretable, usable for control + FDI (Füssel et al. 1997; Isermann & Ballé 1997); Mamdani (1976; Mamdani & Assilian 1995) fuzzy-set/rule consequents -> more qualitative. B-spline NN with triangular basis functions = simplest Mamdani NF structure but large consequent rule set -> low transparency.
- NF limits: limited number of inputs; identification often low transparency (transparency = meaningful description: fewer rules with appropriate MFs). ANFIS (Jang 1993; Jang & Sur 1995): fixed structure, grid partition, hybrid learning (LS for consequent params + gradient/backprop); fast/easy for low-dimensional inputs but loses transparency + local accuracy (backprop = global optimization, not locally nonlinear); fix: find antecedents/rules separately via clustering, constrain antecedents, then optimize. Hierarchical NF: decompose into series of MISO/SISO subsystems; local rules use input subsets, activated by higher-level rules (Tachibana & Furuhashi 1994).
- Design criteria depend on NF role in FDI scheme: pre-processing, identification, residual generation, or classification. Identification stage wants high approximation + disturbance rejection (accurate residuals); classification stage wants transparency.
#### 1.8.5 NF model structure identification
- Complexity reduction/transparency: find input partitions, rules, MFs. Methods: Evolutionary Algorithms, CART (Jang 1994), clustering, unsupervised NN (Kohonen feature maps); then consequent params by least squares.
- Product space clustering (Babuška 1998) for TSK + Mamdani structure ID: MISO nonlinear dynamic system with p inputs -> product space X×Y ⊂ ℜ^(p+1) divided into subspaces where LINEAR models approximate the system. LOLIMOT (locally linear model tree, Nelles & Isermann 1996): identifies TSK fuzzy model with dynamic linear models as consequents. Caveat: structure-ID sensitive to uneven data distribution (more clusters where more data); mitigation: initialize with many clusters.
- Transparency enhancement by structure simplification/optimization: tune rules + MFs (Babuška 1998); optimal rule count via cluster validity measures + Compatible Cluster Merging (CCM, Krishnapuram & Freg 1992); simplify by merging similar fuzzy sets, removing sets similar to universal set; supervised fuzzy clustering + orthogonal techniques + tuning (Setnes & Kaymak 1998).
#### 1.8.6 NF residual generation for FDI
- Scheme A (Fig 1.18): several NF models identify faulty + fault-free behavior; residual vector r_i(t) from bank of NF models [1.72 not decoded]; ideally each r_i sensitive to one fault, in practice noise/disturbances couple several. Mamdani (linguistic style) NF classifier processes residuals -> fault indication via rule set [1.73 not decoded]. Fuzzy threshold evaluation [1.74]: C = total number of input regions with different fault sensitivity; multidimensional fuzzy set η_i defines fuzzy boundary of region i. Depends heavily on faulty+fault-free data availability; harder to isolate faults appearing in the dynamics.
- Scheme B (Fig 1.19, TSK NF-based): residuals from nonlinear dynamic plant model approximated by LOCAL LINEAR models (product-space clustering or LOLIMOT); each local model = linear approximation in an input subspace, selection fuzzy; output y(t) = Σ αi(us)·fi(u) [1.75/1.76 not decoded], αi = validity degree of local model i at operating point us; local model params ai,k, bi,k, ci -> extract PHYSICAL parameters per operating point (time constants, static gains, offsets; Füssel et al. 1997) and compare with ONLINE-estimated parameters (= parameter-estimation diagnosis on a local-model network). Requirements: accurate nonlinear dynamic model; output error minimal when run in parallel; sufficient excitation at EVERY operating point for online parameter estimation.
#### 1.9 Conclusion (key takeaways as stated)
- Tutorial treatment of basic principles of model-based FDI; FDI formalized in uniform framework (mathematical description + definitions); residual generation = CENTRAL issue; residual generator summarized in multiple structures; residual design for isolation discussed; success of diagnosis depends on QUALITY of residuals; successful diagnosis requires residuals robust wrt modeling uncertainty; robust FDI problem discussed, robust residual-generator implementation deferred to following chapters; fuzzy logic, qualitative modeling, NN briefly covered; integrated knowledge-based fault diagnosis (analytical + heuristic information) presented.
- 1.10 Bibliography ~lines 1637-1775 (sampled, not fully read): Isermann/Blanke/Frank/Patton/Ding canon + Korbicz et al. 1999 "Fault Diagnosis in Systems" Springer + Zhou/Doyle/Glover "Robust and Optimal Control" (Prentice Hall) + Wünnenberg & Frank robot FDI. Chapter ends at 1775; "## 2 Structural Analysis" (Krysander & Frisk, Linköping Univ.) heading at 1776-1781 = Chapter 2 boundary.

## Puig Vol1 Ch2-3 — Structural Analysis & Set-Based FDI (source lines 1776-2759)

### Ch2. Structural Analysis — Krysander & Frisk (Linköping) [lines 1776-2177]
- Purpose: analyze diagnosability PROPERTIES of a model (what detectable/isolable, where to put sensors), not just design algorithms. Structural analysis uses only coarse (qualitative) model info → scales to large nonlinear DAE models without numerical difficulty; cost: results are GENERIC/BEST-CASE only.
- Tooling: faultdiagnosistoolbox (Frisk et al. 2017), MATLAB + pip-installable Python; examples in chapter run with it.
- 2.2.1 Structural model: model = constraints E + variables V as bipartite graph G=(E∪V,A); edge iff variable appears in equation. Bi-adjacency matrix ("structural matrix"): rows=equations, cols=variables, entry=dot if vj ∈ ei. V = X (unknown) ∪ Z (known: inputs+measurements) ∪ F (faults). Reduced structure graph = constraints + unknown variables only (the part that matters for analysis).
- Dynamics handled as differential constraints e8/e9 of form x′ = ẋ, marked D (needs differentiation to solve for x′) and I (needs integration to solve for x) in the structural matrix.
- Running example (running throughout): series-wound DC electric motor. 9 equations: e1 Kirchhoff voltage (includes fR, input V), e2 motor torque eq (Tm=Kf·i — text names constant Kf, parameter list says Ka [OCR?]), e3 Newton 2nd law (J, b), e4 torque balance (load torque Tl, fload), e5-e7 sensor eqs (yi,yω,yT with sensor faults fi,fω,fT), e8-e9 differential constraints for i′, ω′.
  - X={i,i′,ω,ω′,T,Tm,Tl}; Z={yi,yω,yT,V}; F={fR,fi,fω,fT,fload}; params {R,L,Ka,b,J}. Faults modeled as additive vars, zero fault-free, non-zero otherwise → generic fault model valid for any size/dynamics.
- 2.2.2 Dulmage-Mendelsohn (DM) decomposition (Dulmage & Mendelsohn 1958; for diagnosis: Blanke et al. 2006, Krysander et al. 2008): reorder bi-adjacency matrix of reduced graph to block-triangular: G- underdetermined / G0 exactly determined (finer "Hall components" Gi) / G+ overdetermined (= contains redundancy, usable for diagnosis). Components unique; triangular arrangement may vary. (·)+ = overdetermined-part operator.
- Def 2.1 Matching Γ⊂A: edges w/o common vertices; maximal = largest; perfect = every vertex matched. Structural rank = size of maximal matching (Murota 2009). Interpretation: ei matched to xj ⇒ ei is the mechanism to solve for xj (causal/computational order). Overdetermined systems have multiple complete matchings.
- Motor DM result (Fig 2.4a): no underdetermined part; exactly-determined part {e2,e4} (solves Tl,Tm); all redundancy in overdetermined block; unmatched eqs e5,e6 = redundant relations. Def 2.2 Redundant Relation: eq in E+ not in a maximal matching; every RR → an ARR once unknowns eliminated via knowns.
- 2.2.3 DM for DAE simulation: semi-explicit form ẋ1=f(x1,x2,u), 0=g(x1,x2,u); take X={ẋ1,x2} unknown, Z={u,x1} known; DM decomposition gives sequential computation scheme (start at bottom, solve for matched variable). Diagonal blocks >1 require simultaneous solve. Motor with inputs (V,Tl) is just-determined → pure sequential scheme (Fig 2.4b).
- 2.3.1 Detectability: fault f modeled as new var; WLOG each fault violates exactly ONE equation (else split via new var xf and eq f=xf). ef = violated eq. Motor: efR=e1, efload=e4, efi=e5, efω=e6, efT=e7.
  - Def 2.3 (semantic): f detectable if Of \ ONF ≠ ∅ (O_f = observations consistent with fault mode f).
  - Def 2.4 (structural): f detectable iff ef ∈ M+. Motor: M+ = M\{e2,e4} ⇒ fR,fi,fω,fT structurally detectable; fload NOT (e4 ∈ just-determined part).
  - Residuals have computational form (known vars only) + internal form (fault sensitivity); used to verify detection correspondence.
- 2.3.2 Isolability: Def 2.5 fi isolable from fj iff Ofi \ Ofj ≠ ∅. Detection = isolation from no-fault mode.
  - Def 2.6 (structural): fi isolable from fj iff efi ∈ (M \ {efj})+ [formula-not-decoded in OCR, but the working example confirms this exact condition].
  - Computation: one DM decomposition per fault: faults in (M\{efj})+ are exactly those isolable from fj.
  - Fault isolability matrix (Fig 2.5b): rows fi, cols fj; dot = NOT isolable; unique isolation of all faults = identity; block for detectable faults is symmetric. Motor: fload undetectable→isolable from nothing; {fR,fi} not isolable from each other but from all else; fω,fT uniquely isolable. From fi, only fT,fω isolable ((M\{e5})+ = {e3,e6,e7,e9}).
- 2.3.3 Canonical isolability decomposition of M+: if M=M+, partition equations into sets Mi such that fi,fj isolable iff in DIFFERENT Mi (Fig 2.6: n blocks (Mi,Xi) plus m−n+1 singleton equation-only sets). Mi computed per-equation as complement of (M\{ef})+ [eq 2.5, formula-not-decoded]. Motor: blocks {e1,e5,e8}↔{fR,fi}, {e3,e7,e9}↔{fT}, {e6}↔{fω}; fR,fi co-blocked because too few eqs relate i,i′. Same partition as equivalence classes in MSO algorithm. Dynamics (D/I marks) ignored in plain structural isolability; integral-causality extensions (Frisk et al. 2012, 2017) can reduce isolability under observer-style integration-only causality (motor unaffected).
- 2.4 Testable submodels (residual generation from structure; pioneered by Staroswiecki, Blanke et al. 2006):
  - Def 2.7 PSO (proper structurally overdetermined): M = M+. Def 2.8 MSO: PSO with no proper PSO subset. Def 2.9 structural redundancy degree φ(M) (= #eqs − structural rank, [formula-not-decoded]).
  - Motor: φ(M)=2; MSO sets (redundancy 1 each): M1={e3,e6,e7,e9}, M2={e1,e5,e6,e8}, M3={e1,e3,e5,e7,e8,e9}. Each testable submodel has a corresponding MSO.
  - Def 2.10 test support (TS): fault set ζ = F(M) for some PSO M (Krysander et al. 2010); Def 2.11 TES (equation set: F(M)≠∅, PSO, no PSO superset with ⊇-fewer faults); Def 2.12 MTS, Def 2.13 MTES. In the motor all MSOs are MTES, not true in general.
  - 2.4.2 FindMSO algorithm (Krysander et al. 2008/2010), top-down recursion: if φ(M)=1 → {M} is MSO; else for each e∈M recurse on (M\{e})+. Walkthrough on motor finds M1,M2,M3, some discovered multiple times → equivalence relation (e′,e)∈R iff (M\{e})+ = (M\{e′})+; partition M into equivalence classes, lump into reduced structure to return each MSO once.
  - 2.4.3 Residual generation via matching: Def 2.14 ARR r(O)=0 holds for all observations consistent with model. Recipe: complete matching of unknowns inside an MSO → compute all unknowns from knowns → residual = the redundant (unmatched) constraint. If all constraints invertible, ANY MSO constraint can be the residual equation (performance differs!). Causality: choosing e5 vs e1 vs e3 as residual eq in M3 gives integral / mixed / differential causality computational graphs (Fig 2.7); D marks: integral = flow ẋ→x, differential = x→x′. Non-invertible constraints: nonlinear, conditional functions, differential constraints. Def 2.15 residual generator: r(t)→0 asymptotically for all o consistent with M.
- 2.5 Sensor placement (Krysander & Frisk 2008): specification = Fdet ⊆ F (detectability) + ordered-pair set I (isolability; assume isolated faults also detectable).
  - Worked toy plant #2: 5th-order linear model (states x1..x5, input u, faults f1..f4, no sensors → no redundancy, nothing detectable). Max-isolability minimal sensor sets: {x1,x3},{x1,x4},{x2,x3},{x2,x4},{x3,x4}. If new sensors may themselves fail: 9 minimal sensor MULTISETS (e.g. {x1,x1,x3}). Def 2.16 minimal sensor set (multiset on measurable-variable set S).
  - Method, 3 steps: (1) sensors for detectability, (2) rewrite isolability as detectability, (3) combine. Assumes no underdetermined part; one equation per fault and single-variable sensors WLOG (introduce xnew=h(x) otherwise).
  - Detectability: DM-triangularize → strong components bi with partial order (Hasse diagram, Fig 2.8b). Thm 2.1: measuring a variable in block bj above block bi makes (Mi∪eq) overdetermined [statement formula-not-decoded]. Detectability set D(fi) = variables in blocks ordered ≥ block containing ef_i; e.g. f3 hits b4 → D(f3)={x1,x2,x4}. All-faults detectability = minimal HITTING SET over {D(fi)} (Reiter 1987; de Kleer & Williams 1987) → {x1},{x2},{x3,x4} for the toy model.
  - Isolability (all faults already detectable): split into |F| sub-problems — for each fj, work in M′ = M\{efj}; fi isolable from fj ⇔ fi detectable in M′∪MS (Def 2.6 + Def 2.4 combo). Faults outside M′ never isolable from fj (same equation); faults already in (M′)+ free; faults in just-determined part M0 of M′ need sensors per D() construction. Thm 2.2: max isolability from fj iff S hits every nonempty D in family for F0 in M0. Example (Fig 2.9, sensors on x3,x4 + sensor faults f5,f6): D(f5)={x1,x2,x3}; minimal additional: {x1},{x2},{x3,x4}.
  - Both (nothing detectable yet): enumerate each minimal detectability set, then solve isolability sub-problems within M∪{sensors}; union → same 5 sets for the toy model.
  - Complexity: everything polynomial except minimal hitting set (NP-hard); the driver of complexity is |P| (specified measurable candidates), not #equations/#faults; approximate hitting-set algorithms (de Kleer 2011) for tractability; physical models' structure helps.
- 2.6 Summary points: test selection is the missing next step — #testable sets exponential in redundancy; select by fault-affected equation (Krysander et al. 2010), by differential index (Frisk et al. 2017), or ML from data (Frisk & Krysander 2018; Jung & Frisk 2018, handles noise/uncertainty via data).
- Chapter-2 ARR coverage: yes — Def 2.14 + RR→ARR pipeline; residual generators generated sequentially from MSO matchings (not just zero-structure parity). No explicit "zero-structure" term used [checked].
#### Ch2 extra detail (from same lines)
- 2.1 motivation: diagnosability analysis should precede diagnosis-system design; for LTI models fairly exhaustive results exist (Nyberg & Frisk 2006); nonlinear/large models need techniques that structural methods replace cheaply.
- Example 2.1 specifics: M+ = {e1,e3,e5,e6,e7,e8,e9} (i.e. M minus {e2,e4}); M+ itself is NOT an MSO since proper PSO subsets exist; each MSO has structural redundancy degree exactly 1; every testable submodel contains an MSO.
- Isolability matrix reading rule: dots in row fi = the set of faults that would be diagnosed (candidates) when fi is the injected fault; unique isolation of all faults ⇔ identity matrix; fR/fi form a 2×2 non-isolable diagonal block.
- Hall-component fine structure inside G0 shown in Fig 2.3; over/under/just-determined + Hall blocks; components unique but block-triangular arrangement can vary when Hall components are independent.
- Hasse diagram detail (Fig 2.8b): blocks connected via nonzeros in the triangular structure give edges; edge bj→bi means bj ≤ bi; partial order — e.g. b3 and b4 unordered; each block bi maps to equation set Mi from the DM decomposition.
- D(f3) worked example: f3 violates eq in block b4; measuring any var in b1, b2 or b4 (blocks ≥ b4 in the order) achieves detectability → D(f3)={x1,x2,x4}; detectability sets for all faults listed at [2.11] (formula-not-decoded); min hitting sets {x1},{x2},{x3,x4}.
- Isolability sub-problem fault trichotomy (Fig 2.9 example, model M={e1..e7} with sensors x3,x4 + sensor faults f5,f6, isolate-from-f1 case, M′=M\{e3}): (M′)+={e4,e5,e7}; just-determined part {e1,e2,e6}; f2 ∉ M′ (violates same eq as f1 → never isolable from f1), f3/f4/f6 already in (M′)+ (free), f5 in just-determined part (needs one more sensor: D(f5)={x1,x2,x3} over vars {x1,x2,x3}).
- Sensor-placement multiset result detail: max isolability with sensor-fault coverage = nine minimal multisets, e.g. S={x1,x1,x3} (two sensors on x1, one on x3).
- Residual-generator output condition in Def 2.15 rendered as "lim_{t→inf} r = 0" [OCR of lim notation garbled]; input o ⊂ O subset of observations, scalar r output.
- MSO algorithm pseudocode (verbatim logic): `FindMSO(M): if φ(M)=1 → MMSO={M} else for each e∈M: M'=(M\{e})+; MMSO ∪= FindMSO(M')`. Motor trace: remove e1 → {e3,e6,e7,e9} (φ=1, save M1); remove e3 → {e1,e5,e6,e8} (M2); remove e5 → duplicate of M1; remove e6 → M3={e1,e3,e5,e7,e8,e9}; these are the only three.
- Detectability example residuals [2.3] not OCR-decoded (formula placeholders) but chapter confirms they detect {fR,fi,fT,fω} and fload is not detectable analytically as well as structurally.

### Ch3. Set-based Fault Detection and Isolation — Ye Wang (Melbourne) & Vicenç Puig (ERII-UPC) [lines ~2179-2751; title page at 2189]
- 3.1 framing: robust FDI two families — ACTIVE: residuals insensitive to uncertainty but sensitive to faults (UIO, robust parity equations, H∞; Chen & Patton 1999 survey). PASSIVE: propagate model uncertainty INTO residuals, adaptive thresholds at decision stage (seminal: Horak 1988 time-domain, Emami-Naeini et al. 1988 frequency-domain threshold selector; Puig et al. 2006 interval observers DAMADICS, Puig et al. 2008 interval models, Rambeaux et al. 2000 optimal thresholding, Adrot & Flaus 2008, Ploix & Adrot 2006 parity relations for uncertain systems).
- Interval models = nominal model + every parameter uncertainty bounded by intervals; deterministic unknown-but-bounded (no statistics). Same idea under 3 names: worst-case/tolerance analysis (circuits, Kolev 1993), set-membership / error-bounded approach (estimation: Milanese et al. 1996; control: Bhattacharyya et al. 1995, Ackermann 2002), semi-quantitative (qualitative reasoning; modal interval analysis, Sainz et al. 2002 three-tank FDI — three-tank appears ONLY in references, chapter benchmark is four-tank).
- 3.2 sets: Zonotope Def 3.1: Z = <c,H> = {c + Hp : p ∈ [-1,1]^r}, c=center, H=segment matrix; equivalently Z = c ⊕ H·B_r (Minkowski sum w/ hypercube). Key linear properties [3.2, formula-not-decoded]: linear map L<c,H>=<Lc,LH>; Minkowski sum <c1,H1>⊕<c2,H2>=<c1+c2,[H1 H2]> (standard forms; OCR formulas not decoded). Size measures: Def 3.2 P-radius (Le et al. 2013, Combastel 2015) and Def 3.3 weighted F-radius via weighted Frobenius norm (formulas not decoded). Zonotope reduction operator ↓q,W(H), inclusion <c,H> ⊆ <c,↓q,W(H)>, q≥n caps #generators; denoted H̄ (Combastel 2015).
- 3.3.1 plant class: discrete-time LTI [3.5] x+ = Ax + Bu + Dw·w; y = Cx + Dv·v (+ feedthrough matrices; exact eqs formula-not-decoded). Assumption 3.1: w(k) ∈ <0,I_mw>, v(k) ∈ <0,I_mv> (unitary zonotopes). Assumption 3.2: x(0) ∈ X(0)=<c(0),H(0)>. Faulty system [3.7]: + F_u f_u (actuator) and F_y f_y (sensor) fault distribution matrices.
- 3.3.2 two estimation methods, both zonotopic:
  - (1) Set-membership state estimation (Puig et al. 2001; Alamo et al. 2005; Wang et al. 2018): Algorithm 3.1 = predict X^p(k) from dynamics, then intersect with output-consistent set X^y(k): X^e(k) = X^p(k) ∩ X^y(k) (Fig 3.1). Alternatives intervals/ellipsoids/polytopes; zonotopes chosen for low complexity + symmetry.
  - (2) Set-based (interval) observer (Raïssi et al. 2012 nonlinear interval observers; Combastel 2015): Luenberger observer structure, propagate enclosing zonotope under UBB disturbance/noise; Algorithm 3.2 computes estimated-state sets X^e(k) AND estimated-output sets Y^e(k) (Fig 3.2 "interval observer"). Simulation-based propagation (no intersection step) vs set-membership intersection scheme.
- 3.4.1 Prop 3.1 state-bounding zonotopes for set-membership: any correction matrix Λ ∈ R^{nx×ny}; recursion ĉ(k)=Ac(k-1)+Bu(k-1), R(k)=[A H(k-1), Dw]; corrected c(k),H(k) via Λ(y(k) − Cĉ(k) − ...) [3.8-3.9 not decoded]. Proof = standard generator-parameterization x=c+Hθ, ‖θ‖∞≤1, stack θ,ϖ,σ (w=Dwϖ, v=Dvσ).
- 3.4.2 Prop 3.2 prediction-type zonotopic observer: gain G(k), observer eq [3.14]; recursion c(k+1),H(k+1) [3.15] uses reduction H̄ (keeps generator count bounded); inclusion x(k+1) ∈ <c(k+1),H(k+1)> [3.16].
- 3.4.3 equivalence (Wang et al. 2018, descriptor systems): set-membership corrects x(k) with y(k) (current estimate); prediction observer produces x(k+1). Prop 3.3: set-membership ⟺ CURRENT-estimation-type zonotopic observer [3.17-3.19, time-varying gain G̃(k)] — same recursion at step k+1.
- 3.5.1 robustness (shrink uncertainty propagation):
  - Prop 3.4 robust correction matrix: given 0<γc<1, ε>0 find P≻0, Y, diagonal Γ⪰0 (mw), Υ⪰0 (mv) s.t. LMI [3.20]; guarantees V(X(k+1)) ≤ γc·V(X(k)) + ε (V = P-radius) → asymptotic bound V(X(∞)) ≤ ε/(1−γc); Λ = P⁻¹Y. Proof: contraction of P-radius, diagonal multipliers bound max over ‖θ‖∞≤1, Schur complement, coordinate transform T.
  - Prop 3.5 Zonotopic Kalman gain (Combastel 2015): G*(k) = argmin_G ‖H(k+1)‖²_F,W; closed-form via Schur complement [not decoded]; J convex in G, ∂J/∂G=0. Remark 3.1: G* does NOT actually depend on W (W=I fine) — key Combastel result (gain optimal under UBB despite Kalman-like form).
  - Cor 3.1 robust zonotopic observer gain: same LMI pattern with (γo, εo); G = P⁻¹Y; Ψ=[A−GC, Dw, GDv]ᵀP[A−GC, Dw, GDv].
- 3.5.2 fault sensitivity: Cor 3.2 residual zonotope R(k)=<cr(k),Hr(k)> = linear projection M of state zonotope (M ∈ R^{ny×ny} residual gain; residual = M(y − Cx̂) style [3.30-3.31 not decoded]). Prop 3.6 sensor-fault "H-" sensitivity condition [OCR: likely H−/H∞-type]: LMI [3.32] in P,Y,N, scalars αs,βs>0 ⇒ L2 gain from f to residual center crf bounded below/above (condition "H-" = ‖crf‖² ≥ α‖f‖² − β style, not decoded); G=P⁻¹Y, M=(N^{1/2}) [rendered "M = N 1 2" OCR]; proof: w=v=0, error dynamics ef(k)=x(k)−c(k), residual zonotope collapses to its center crf; criterion J_s over horizon T + Lyapunov Qs=αs P; N=MᵀM.
- 3.6 FD decision tests (validity = empty intersection):
  - Set-membership [3.41]: fault detected at first k with X^e_k = X^p_k ∩ X^c_k = ∅ (Algorithm 3.3; consistent-set intersection emptiness = validity test). Recovery after detection: reset X^e_k to a larger set guaranteed to capture true post-fault state.
  - Zonotopic/interval observer [3.42]: measurement interval [y_k]; fault if y_k ∉ Y^e_k (equivalently [y_k] ∩ Y^e_k = ∅); Algorithm 3.4 loops output-data acquisition + predicted-output set via Algorithm 3.2.
  - Consistent answer semantics (3.8): inconsistency ⇒ fault; consistent ⇒ NO statement possible (no false-alarm-free proof of health).
- 3.6.2 fault ISOLATION: bank of observers approach (standard, Blanke et al. 2016) — each observer sensitive to all faults EXCEPT one; NOT set-inversion-based localization (parameter set-inversion FDI line (Ploix/Adrot, Fagarasan) only cited, not developed). Actuator-fault decoupling via UIO: existence condition rank(C F_u) = rank(F_u) [3.43 standard, not decoded]; then O = (C F_u)⁺ pseudoinverse, premultiply state eq [3.44] and substitute → system decoupled w.r.t. f_u [3.7-transformed, formulas not decoded] (Chen & Patton 1999 UIO; Keller & Darouach 1999 two-stage transformation alternative).
- 3.7 benchmark: QUADRUPLE-TANK system (Fig 3.3), discrete model from Pourasghar, Combastel, Puig, Ocampo-Martinez 2019 (FD-ZKF paper — zonotopic Kalman filter optimizing fault detection not estimation); matrices [3.5-form] formula-not-decoded. Setup numbers (verbatim): two normalized sensor faults f=[f1,f2]ᵀ, Fs = 10·I, f1,f2 ∈ [−1,+1], fault active during 200 ≤ k ≤ 600, simulation horizon 1000 steps, closed-loop data collected (Fig 3.4).
- Results (Figs 3.5-3.8, qualitative — plots not OCR'd):
  - Robustness-only set-membership (optimal correction Λ, Fig 3.5): detects only fault ON/OFF edges (k≈200, k≈600); most sensor-fault magnitudes NOT detected.
  - Robustness-only zonotopic Kalman observer (Fig 3.6): same — uncertainty effect minimized, only edges detectable.
  - Zonotopic observer w/ Cor 3.1 robustness LMI only (Fig 3.7): similar, most faults undetected.
  - Zonotopic observer w/ BOTH robustness (Cor 3.1) + fault sensitivity (Prop 3.6) (Fig 3.8): improved detection (chapter presents as successful; figure content not in text layer).
- 3.8 conclusions: set-membership = deterministic UBB alternative to statistical methods; enclose exact possible-behavior set with approximating sets (parameter or state space); consistency check observed vs predicted; same principle used to estimate interval models for FD and to develop fault-tolerance EVALUATION methods [forward reference to Vol.1 Ch.10-ish content].
- Chapter roadmap quirk [OCR/text]: 3.1 roadmap lists sections 3.2, 3.3, 3.6, 3.7, 3.8 and skips 3.4-3.5 (present in body).
- Density-check answers for this chapter: set representations = boxes/intervals + zonotopes (ellipsoids/polytopes mentioned as alternatives, not used); validity test = empty intersection (X^e_k=∅ or y_k∉Y^e_k); residual evaluation = residual zonotope center+radius vs zero (interval residual bands); simulation-based (set-membership predict-correct + interval observer propagate) both covered; set inversion NOT used for localization (observer bank + UIO decoupling instead); benchmark = four-tank, with numbers above (three-tank only in refs).

## Puig Vol1 Ch4 — Stochastic Diagnosis (source 2760-3142)

### 4.1–4.2 Stochastic diagnosis as inverse problem
- Motivation: uncertainty is the core FDD challenge (model imprecision + noisy measurements). Fault probabilities matter: point estimates inaccurate; omitting probability = assume all faults equiprobable → bad multiple-fault diagnosis (Provan; cites Venkatasubramanian et al. 2003).
- Counter-framing to "standard" two-step residual/ARR diagnosis (Gertler 1991): adopt first-principles **model inversion** framework (Stuart 2010).
- Setup: faults/modes φ ∈ Φ (faulty + nominal), observations y ∈ Y, forward model **y = ξ(φ, η)**; ξ = forward operator, η = noise + modeling error. Diagnosis = reconstruct unobservable φ from noisy y (statistical inverse problem).
- Two canonical difficulties: (1) inversion is **ill-posed** — forward map many-to-one, inverse one-to-many, φ non-unique (Vogel 2002); (2) computational cost — statistical inversion needs thousands–millions of forward-model evaluations (MCMC-class sampling), prohibitive at scale (Du et al. 2017: model-driven needs many samples; data-driven needs much data, calibration sensitive to amount/distribution).
- Three-approach taxonomy (Figure 4.1, hierarchy of methods):
  - model-driven: first-principles inverse φ = ξ⁻¹(y) given uncertainty η;
  - data-driven: learned pseudo-inverse classifier φ = ξ⁻¹_Θ(y), params Θ fit from data D;
  - hybrid: uses D **and** ξ to invert more efficiently than pure model-driven.
- Notation (Table 4.1 as bullets): x1:k states, y1:k observations, φ1:k modes, u1:k controls over time; v = process noise, w = measurement noise.
- Formal model: Φ Banach/Hilbert space of functions on Ω ⊂ R^d, Y on data manifold M; ξ decomposes into state equations (x evolves under φ, u) + output equations. Def 4.1 nonlinear continuous-time stochastic system [formulas not decoded]; linearized form x˙ = Ax + Bu + γ + v, y = Cx + w, A,B ∈ R^{N×N} state-independent, C ∈ R^{q×N}, γ captures direct param contributions/forcing, no direct param→output term (wlog).
- Uncertainty representation, two methods: (1) additive noise y = ξ(φ) + δy; (2) intrinsic uncertainty y = P(y|φ) — standard is probabilistic: likelihood π(y|φ) = probability of measurements given φ, folds forward model + noise into π. (Sharifian et al. 2019 survey for chemical process PE.)
- Bayesian formulation: φ as random variable with prior π_pr(φ); posterior **π_post(φ) ∝ π(y|φ)·π_pr(φ)** [4.6 formula-not-decoded] — solution of inverse problem IS a PDF over φ. Data finite-dim y = (y(t1)..y(t_nt)), M = n_t·q; nonlinear case posterior represented by **samples**; moments/marginals from samples.

### 4.3 Inference tasks vs other tasks
- Diagnosis at time t from anomalous y_t computes fault state φ_τ, τ ≤ t: inversion φ = ξ⁻¹(y). Three solution routes restated (model-based inversion / data-driven classifier / hybrid).
- Distinction bullets: state estimation computes P(x_k|Y_k) for full state x_k, usually assumes fault-free; diagnosis wants only P(φ_k|Y_k). State forecast computes P(x_{k+1}|Y_k, x_k).
- Ch plan: 4.4 model-driven, 4.5 data-driven, 4.6 hybrid, 4.7 comparison, 4.8 conclusion.

### 4.4 Model-based approach (traditional FDD + Bayesian inversion)
- Abstract view: minimize misfit to data, loss L(ξ(φ,y)) ≈ maximize log-likelihood (ML solution).
- Traditional FDD = residual reasoning, two steps: (i) residual generation r from model prediction ŷ vs measured y; (ii) fault isolation = statistical evaluation of r. Fault detection defines r via norm of y − ŷ [formula-not-decoded]; deterministic residual ideal: zero iff fault-free.
- Stochastic residuals are density-based: "zero residual" ⇔ residual density statistically equivalent to measurement-noise density; tests: LLR, GLR, SPRT, CUSUM. Nonlinear systems need advanced tests (Alrowaie et al. 2012). Residual generation: observer for deterministic models (Patton & Chen 1997) or filter for stochastic processes (Alrowaie et al. 2012); additive-noise model assumed. Isolation = identify specific mean value φ̄ᵢ of the fault modes {φ̄ᵢ}, i=1..m.
- ARR/structural methods (Gertler 1991; Staroswiecki & Declerck 1990; Cordier et al. 2004): transform dynamics ξ → ξ′ exposing the **diagnosable subset**: variables with ≥ as many equations as unknowns (over/fully determined); rest = underdetermined, not diagnosable. ARR = model constraint involving **only measured variables** → residual eval from any observation; satisfaction ⇔ zero residual. Computed by elimination via structural analysis / **Dulmage–Mendelsohn** canonical decomposition of the equation–variable bipartite graph (complete matching on unknowns) → unique decomposition into under/just/over-determined sets; just-determined + redundant relations = ARR basis; overdetermined sets drive isolation (logical combination of measured deviations vs implicated fault params).
- Observer-based: parallel process model + feedback of output estimation error r_t = y_t − ŷ_t, gain K (Figure 4.2); matrix inverse transform of [4.4]/[4.5]. Single fault only → **bank of observers**, one per candidate fault, for simultaneous multiple faults. Few results for stochastic FDE (Chen & Patton 1996 early formulation).
- Bayesian filtering: Def 4.2 discrete-time stochastic system: state-transition prob P(φ_k|φ_{k−1},u) + stochastic measurement model [4.9]/[4.10, formulas not decoded]; goal = health state **P(φ_k | y_1:k)** via Bayes. Def 4.3 statistical inversion: joint posterior P(φ_1:k|y_1:k) ∝ P(φ_1:k)·P(y_1:k|φ_1:k); prior from dynamic model, likelihood from measurements, normalizer P(y_1:k) = integral [formula-not-decoded]. Intractable: posterior is a function, recomputed per new measurement, dimensionality grows each step → need restrictive approximations/assumptions.
- Inference families (Blei et al. 2017):
  - Exact: graphical model G(Z), Z = φ ∪ y, join-tree decomposition/propagation (Koller et al. 2009); form-specific algorithms: HMM (Smyth 1994), Kalman filter (Kalman 1960), particle filter (Doucet & Johansen 2009), dynamic Bayes nets; Provan 2019 overview of PGM diagnostic inference. MAP estimator = point maximizing posterior PDF.
  - Robust/bounded-error inversion (El Amri et al. 2020): compute set of y with sup_{φ∈Φ} ξ(y,φ) ≤ c.
  - Sampling: MCMC 3 steps — (1) ergodic Markov chain on φ with stationary dist = posterior, (2) sample chain, (3) empirical posterior from samples (Berg & Billoire 2007); drawback: many samples needed for many variables.
  - Variational: pick π* ∈ family F minimizing **KL divergence** to exact posterior [formula-not-decoded]; decouples degrees of freedom, fits variational parameters; faster & scales better than MCMC but less well understood theoretically/empirically.

### 4.5 Data-driven approaches
- Fit when physics unknown/too complex. Success hinges on data amount + **quality** (distribution of nominal vs faulty); sparse faulty data → hard to train fault classifiers → fallback: binary normal/abnormal classifier needing only normal historical data (easy, quick).
- ML triad: supervised (all data fault-labeled; needs nominal + failure mode data), semi-supervised (some labels; often only healthy data), unsupervised (no labels; limited to clustering, e.g. vibration signatures). Chapter focuses on supervised. Reviews: Khan & Yairi 2018; Zhao et al. 2019; Ademujimi 2017; Lo 2019; Rezaeianjouybari 2020; Nor et al. 2020 (chemical process FDD).
- ML as nonlinear pseudo-inverse: find ξ⁻¹_Θ : Y→Φ with pseudo-inverse property [formula-not-decoded]; Θ ∈ parameter space Z; learning = optimize Θ against a **loss functional** chosen per supervised/unsupervised training data. Methods used: ANN, neuro-fuzzy, SVM, Gaussian mixture, KNN, Bayesian networks.
- Scaling wall (numbers/scope): most stochastic-diagnosis ML limited to **single-component** systems (condition monitoring of motors/drives); few system-level applications — insufficient system-level data incl. fault conditions; black-box ML has no clear state-variable notion → cannot compose component models into system-level models (unlike component models in model-based approaches).
- Statistical (multivariate) methods: PCA, PLS/partial least squares, ICA, Fisher discriminant analysis; extract correlations, reduce dimensionality (Chiang et al. 2000). Handle hundreds of variables, noise-insensitive, handle missing data well. Two-step: (1) project data to low-dim latent space where normal/abnormal regions defined; (2) statistical tests on new data — T² score plot, squared prediction error (SPE) plot; isolation via **contribution plots** (each variable's contribution to deviation from in-control PCA/PLS model): powerful for simple sensor/actuator faults, weak for complex faults.
- Shared drawback (ML + statistical): **no explainability / no causal description** of the process — unlike parity-equation approaches, no causal basis for isolation; same single-component composition limitation.

### 4.6 Hybrid / surrogate (gray-box) methods
- Hybrid = model- + data-driven (Bohlin 2006; Mattis & Wohlmuth 2018; Xiong & Jutan 2002). Surrogates attack the **extreme computational cost** of stochastic inversion: replace part of model ξ with data-driven ξ_s; combination stays physically interpretable. Overviews: McBride & Sundmacher 2019 (chemical process), Bhosekar & Ierapetritou 2018 (model design optimization).
- Two construction routes: (1) sampling → simpler model ξ_s; (2) data D + simplified model → data-augmented ξ_{s,θ} better than simplified alone.
- Sampling route problem stmt (Garud et al. 2017; Mattis & Wohlmuth 2018): given y = ξ(φ) and a form for ξ_s, compute sampling set S giving prescribed approximation accuracy over φ ∈ Φ.
- Data route problem stmt: given y = ξ(φ), low-fidelity ensemble Ξ̃ = {ξ̃₁(φ),…,ξ̃_q(φ)}, data D, and a form for ξ_s, compute aggregator ζ such that ζ(ξ̃₁(φ),…,ξ̃_q(φ)) ≈ ξ(φ) to prescribed accuracy.
- Two data-driven surrogate diagnostics variants:
  - **tuning**: data D improves a simplified model/ensemble — Provan (2017): polynomial regression tuning an ensemble of low-fidelity ODE diagnosis models to hit embedded-processing limits.
  - **augmentation**: learn part of the model from D — Yang & Perdikaris (2019): conditional deep surrogate models, multi-fidelity stochastic processes from variable-fidelity info sources; Yan & Zhou (2019): deep-NN adaptive surrogate for large-scale Bayesian inversion.

### 4.7 Comparative analysis (one inversion lens: all methods output a posterior over φ)
- Model-driven: use dynamical equations y = ξ(φ,η) directly. FDD: pseudo-inverse of ξ + statistical test for isolation. Bayesian filtering: no statistical test needed — posterior fault distribution computed directly.
- Data-driven: induce pseudo-inverse ξ⁻¹_Θ from data, no manual model. FDD-style = pseudo-inverse + statistical test; ML-style = classifier gives diagnosis directly via φ = ξ⁻¹_Θ(y).
- Hybrid: computationally simpler model than model-driven, with data tuning the process.
- Trade-off bullets:
  - model-driven: interpretable, good extensibility for isolation, model libraries → compose large systems from component models; BUT laborious manual model construction, expensive inference.
  - data-driven: no manual modeling, inference typically cheap; BUT needs large well-distributed nominal+fault data, not interpretable, poor isolation extensibility, no composition from component models.
  - hybrid: potentially best of both (simpler compute + less manual modeling); BUT immature — significant research needed for real-world diagnostics.

### 4.8 Conclusions + future prospects
- Chapter unifies heterogeneous stochastic-diagnosis algorithms in one consistent model-inversion framework for comparison; introduces hybrid family as the emerging third leg.
- Future: deep learning helps diagnostics only at **component level** today (e.g. bearings/motors); scaling to large systems unclear; expected remedy = hybrid methods blending model structure for large systems with local fault classifiers.

### 4.9 References anchors (key citations for the framework)
- Inverse-problem framing: Stuart 2010 (Bayesian perspective), Vogel 2002 (ill-posedness).
- FDD surveys/context: Venkatasubramanian et al. 2003 (Part I quantitative model-based), Gertler 1991 (ARR survey), Chiang/Russell/Braatz 2000 (industrial FDD), Cordier et al. 2004 (ARRs vs conflicts AI-vs-control view), Staroswiecki & Declerck 1990 (structural ARR).
- Stochastic inference: Blei et al. 2017 (variational review), Doucet & Johansen 2009 (nonlinear filtering), Smyth 1994 (HMM fault detection), Kalman 1960, Koller et al. 2009 (PGMs), Alrowaie et al. 2012 (particle-filter FDI in stochastic nonlinear state-space), Chen & Patton 1996 (robust FDI stochastic w/ unknown disturbances), El Amri et al. 2020 (data-driven stochastic inversion via functional quantization).
- Surrogates: Garud et al. 2017 (smart sampling), McBride & Sundmacher 2019, Bhosekar & Ierapetritou 2018, Provan 2017 (embeddable reduced-order diagnostics), Yang & Perdikaris 2019, Yan & Zhou 2019.
- Uncertainty survey: Sharifian et al. 2019 (chemical process systems).
- Chapter author: Gregory Provan (UVa/Cork; cf. Provan 2019 PGM diagnosis chapter in Escobet et al., Springer). Ch4 ends; Ch5 "Data-Driven Methods for Fault Diagnosis" (Simani) starts at 3135.

## Puig Vol1 Ch5 pt.1 — Data-Driven Diagnosis, first half (source 3135-3790)

### 5.1. Introduction (3143)
- ID from behavior samples is ill-posed (Hadamard): non-unique, discontinuous in data (Söderström & Stoica 1987, Kalman 1990, Ljung 1999); a priori knowledge constrains the model space (regularity → smoothness → minimization; Tikhonov & Arsenin 1977).
- Chapter's key framing: Frisch scheme (Frisch 1934) extended from algebraic to dynamic systems — aim: determine the WHOLE FAMILY of models compatible with noisy sequences, not one prejudiced pick (Kalman 1982a/b/1984 critique: a unique model from uncertain data requires extra information, i.e. "prejudices").
- Punchline result that surprised the authors: in the DYNAMIC case a single model is generally compatible with the data — not in contrast with Kalman, because dynamic sample correlations carry the extra information (Fantuzzi et al. 2002).
- Frequency-domain EIV approach (Kalman 1990; Beghelli et al. 1994a,b, 1997) still in development. Chapter scope: linear + nonlinear (affine, piecewise-affine, fuzzy) dynamic ID for FDI — parameters, order AND structure via Frisch-scheme extension.

### 5.2. Models for linear system fault diagnosis (3167)
- Monitored system at steady state: linear discrete-time LTI state-space x(t)∈ℜⁿ, y*(t)∈ℜᵐ, u*(t)∈ℜʳ, matrices A,B,C [formulas not decoded].
- Sensor measurements corrupted by additive noise ũ(t), ỹ(t): white, zero-mean, uncorrelated Gaussian. Only u(t), y(t) available → this is the Errors-In-Variables (EIV) model class.
- Two regimes by SNR:
  - high SNR (ũ≈0, ỹ≈0): Equation Error (EE) identification; pick ARX/ARMAX within an assumed family.
  - low SNR: Frisch scheme identifies the generating discrete linear system AND the noise variances σ̃u², σ̃y²; noises assumed zero-mean white, mutually uncorrelated, uncorrelated with every component of u*, y*.
- I/O behavior as m ARX MISO models with order n, params αi,j, βi,j,k; εi(t) = modeling error (process noise, parameter variations). [formula-not-decoded]
- Downstream: EE models → state-space for Luenberger observers; Frisch models → state-space for Kalman filters. Canonical-form realization matrices Ai,Bi,Ci,Bωi,Dωi given (Ci = [1 0 … 0]) [formulas not decoded].

### 5.3. Parameter estimation methods for fault diagnosis (3219)
- Model classes used: discrete-time, parametric, deterministic+stochastic, I/O MISO dynamic models.
- Disturbances modeled as noises on input/state/output; global effect often = white-noise-driven filter output added to deterministic part. High SNR → identify deterministic part only (5.3.1); low SNR → both parts (5.3.2+).

#### 5.3.1. Data-driven method in ideal conditions (3225)
- SISO ARX order n over [1,L]; N = L−n prediction steps; cost J(θ) = mean-square prediction error [formulas not decoded].
- Hankel matrices Hu, Hy build Hn; optimal θ̂ = (Hn⁺) thing — pseudo-inverse solution; θ̂ converges asymptotically to true params.
- Order estimation: sequence of matrices Sk = Hk*ᵀ Hk* tested for singularity; first singular Sk ⇒ k=n. Fails in practice because ε(t)≠0 makes every Sk non-singular.
- Workaround for large N: estimate σε from Jn(θ̂) (Ljung 1999); define σεk. Behavior: σεh > σεk for h<k; σεk > σε for k<n; σεk ≈ σε for k≥n → decreasing then stabilizing sequence marks the order. σ²εk = Jk(θ).
- PPCRE criterion (Guidorzi et al. 1982): σεk as % of measured-output std; PPCRE(k) gives prediction error of order-k ARX WITHOUT computing parameters/predictions. Select minimal order whose increase no longer significantly improves.
- Worked example (Figures 5.1, 5.2, images not OCR-decoded): simulated 2nd-order model n=2; slope change visible at k=2 for both PPCRE(k) and Jk(θ) curves.
- Same relation [5.17] underlies FPE, AIC, MDL order criteria (Söderström & Stoica 1987).

#### 5.3.2. Data-driven methods in real scenarios (3293)
- One-line bridge section: identification from noisy data → algebraic (5.3.3) and dynamic (5.3.4) cases separately.

#### 5.3.3. Algebraic Frisch scheme (3301)
- Setup: n variables x1..xn observed at N>n times; linear relations aᵀx=0; X data matrix, relations = columns A with XᵀX A = 0 i.e. ΣA = 0, Σ = XᵀX zero-mean sample covariance.
- With noise, rank[Σ]=n → no relations unless data modified → need EIV. Frisch assumptions: (1) all variables symmetric, each with unknown additive noise; (2) each noise independent of all other noises and of true variables; xi = xi* + x̃i.
- Core problem: given Σ ≻ 0 (n×n), find all diagonal Σ̃ ⪰ 0 with Σ* = Σ − Σ̃ ≥ 0. Solution NOT unique: rank(Σ*) changes with Σ̃, so the same data can support different numbers of linear relations.
- Key theorem: rank(Σ*) = n−1 for all admissible Σ̃ iff Σ⁻¹ can be made strictly positive by LΣ⁻¹L, L = diag[±1].
- Solution set in parameter space = convex simplex whose n VERTICES are the least-squares solutions (each = assume one variable noisy, all others noise-free); max noise variance on variable i alone: σ̃imax = 1/(Σ⁻¹)ii [formula not decoded; Σi minor form] (Beghelli et al. 1990).
- Geometry: allowable (σ̃1,…,σ̃n) form a convex hypersurface in the first orthant of noise space ℝⁿ₊; plane sections parallel to coordinate planes are hyperbola segments. Hypersurface splits the orthant: above → Σ* non-definite, below → Σ* positive-definite. Lower-rank solutions lie on the hypersurface; parameter-space solution set can be a collection of convex polyhedral sets.

#### 5.3.4. Dynamic Frisch scheme (3348)
- Dynamic relations: linear MISO discrete systems order n, params αi, βij [5.23]. Noiseless problem first: determine n and params from u*1..u*r, y*.
- Build covariance matrices Σ*k from Hankel-type vectors; realization problem: test increasing-dimension Σ*k for singularity; first singular Σ*k ⇒ n = k−1; the dependence coefficients of the (n+1)-th vector = system parameters.
- Sample requirement: N ≥ (r+1)n + 1 to avoid spurious dependence; less data → only partial realization.
- Noisy case: Σ*k always non-singular → noiseless procedure useless. Frisch: Σk = Σ*k + Σ̃k with Σ̃k block-Toeplitz diagonal from white-noise variances σ̃y, σ̃uj, no cross-time noise correlation.
- Problem: for each k, find all diagonal Σ̃k ⪰ 0 such that Σ*k = Σk − Σ̃k ≥ 0 (singular at true order). Noise space stays ℝ⁽ʳ⁺¹⁾₊; parameter space is ℝ⁽ʳ⁺¹⁾ᵏ⁻ʳ (note: differs from algebraic case).
- Solution set per k = hypersurface in first orthant of (σ̃y, σ̃u1…σ̃ur) hyperplane, concavity facing the origin. The (r+1) boundary points where exactly one variance is zero = dynamic extension of least-squares solutions (output-only-noisy / input-j-noisy).
- THEOREM (Beghelli et al. 1990): solution-set curves for different k are NON-CROSSING; for k>n all hypersurfaces share at least one common point = TRUE noise variances (σ̃y*, σ̃u1*…σ̃ur*) — identification search starts there.
- Spectral properties of Σ*k: k≤n positive-definite; k>n null-space dim (and least-eigenvalue multiplicity) = k−n; at k=n+1 the dependence coefficients among the (r+1)k−r vectors ARE αi, βij; k>n+1 all dependence relations share the same (r+1)n coefficients.
- Example Figure 5.3 (image): noise space and singularity surfaces for a SISO n=2 system; circled point = true input/output noise variances.
- Caveat: real processes violate linearity/finite-dimension/LTI/white-additive assumptions → hypersurfaces have NO common point for k>n → model-selection criterion needed (Beghelli et al. 1994a).

#### 5.3.5. MIMO case Frisch scheme (3451)
- MIMO via Guidorzi (1981) canonical models: m interconnected observable canonical subsystems of orders νi; indices νij−1 satisfy constraints [formula not decoded]; νi = Kronecker observability invariants, fully define structure.
- Identification = determine structure {ν1..νm} AND params αijk, βijk. Solvable per Guidorzi (1981), generalizes to multistructural (overlapping) models.
- FDI payoff of canonical models: minimal parameterization (Delmaire et al. 1999), reduced storage/compute, high algorithm efficiency.
- MISO properties carry over: single common noise-space point across increasing-k hypersurfaces ⇒ true I/O noise variances ⇒ problem collapses to realization → canonical model. BUT search in (m+r)-dim space is time-expensive, and coincident hypersurfaces (non-unique solution) are not excluded. Bottom line: no conceptual difference Frisch SISO vs MIMO.

### 5.4. Nonlinear dynamic system identification (3475)
- Black-box parametric nonlinear models for real processes; choice of parametric structure is the hard step (Juditsky et al. 1995; Billings & Voon 1983b).
- Multi-regime plants: one model per operating condition + switching function = piecewise/hybrid models (Bemporad & Morari 1999 linear; Pettit & Wellstead 1995, Sontag 1981, Banks & Kathur 1989 affine). Priestly (1988) state-dependent model precedent.
- Headline theorem: hybrid models with affine submodels approximate any nonlinear target to arbitrary precision in Sobolev norm (function AND first derivative).
- Distinctive twist vs cited bibliography: PWA identification under EIV structure with Frisch/Kalman noise assumptions → generalizes Beghelli et al. (1990) single-model results to structure+parameter ID with measurement-noise rejection.
- NOTE: the parent-facing brief expected LS/total-LS/RLS/PEM here; in 3135-3790 that ladder does NOT appear. What exists: ordinary LS via Hankel pseudo-inverse (5.3.1), total-LS-like EIV/Frisch machinery, and eigenvalue-based order selection. No RLS/PEM/max-likelihood in this half.

#### 5.4.1. Piecewise affine model (3495) + 5.4.2. Hybrid model structure (3509)
- SISO nonlinear time-invariant regression y(t+n) = F(y(t..t+n-1), u(t..t+n-1)), F continuous on Dn = Uⁿ×Yⁿ (Leontaritis & Billings 1985a,b). ID = approximate F by a parametric structure with arbitrary-accuracy interpolation.
- Structure: M affine submodels; regressor xn(t) = [y(t),…,y(t+n-1), u(t),…,u(t+n-1)]ᵀ (2n-dim); switching function χi(xn) = indicator of region R(i)n; {R(1)n..R(M)n} partitions Dn; params per region a(i) = [α(i)0..α(i)n-1, β(i)0..β(i)n-1, b(i)]ᵀ — affine (constant term b(i)), not homogeneous.

#### 5.4.3. Nonlinear system approximation (3527)
- Metrics: Lebesgue norm ‖·‖w then stricter Sobolev norm including first ∂F/∂xj (avoids jittery approximations).
- Density result: PWA f dense in C¹ under ‖·‖w ∀w>0: ∀ε>0 ∀F∈C¹ ∃ PWA f with both ‖F−f‖w<ε and ‖∂(F−f)/∂xj‖w<ε [formulas not decoded].
- Proof vehicle: Ritz piecewise polynomial theorem (Strang & Fix 1973, Thm 3.1): if regions between nodes are convex, non-degenerate, diameter < d̂, and f reproduces first-order polynomials exactly per region → pointwise |F−f|<ε and |∂F−∂f|<ε.
- Bounded Hessian ∇∇F gives d̂ ~ ε linearly via constants C0, C1 (d̂ ≤ C·ε form) [formulas not decoded]. Compactness of Dn upgrades to norm density.
- Practical read: knowing a Hessian bound would bound region diameter → number of regions; rarely known, so just refine partition and improvement is guaranteed eventually. Derivatives may jump at boundaries yet converge to target derivative pointwise as surrounding regions shrink — consistency even along boundaries.

#### 5.4.4. Model continuity and domain partitioning (3595)
- Target F continuous ⇒ f forced continuous: a(i′)ᵀ[x̄n,1] = a(i″)ᵀ[x̄n,1] at every shared accumulation point [5.53] — infinitely many constraints naively.
- Convex-boundary result: if R(i′,i″)n convex and [5.53] holds at p points, it holds on their convex hull (δ-combination proof). ⇒ convex polyhedra regions: continuity just at polyhedron vertices → FINITE matrix constraint Cn·a = 0 (block-difference of adjacent a-vectors) [formulas not decoded].
- Triangulate Dn into 2n-dim simplexes; admissible triangulation: simplexes disjoint or share a whole k-face (k=0..2n-1); affine model pinned by values at ≤2n+1 affinely-independent vertices per simplex.
- Recursive triangulation of hyper-rectangle Uⁿ×Yⁿ (order n grows, reuse work): base n=1 split each rectangle by a diagonal (Figure 5.4: D1 = U×Y into 2 triangles R(1)1, R(2)1; image); step: prism p = s × IY_i triangulated into 2n+1 equal-volume simplexes = convex hulls of ξ0..ξi, ξ′i..ξ′2n; alternate Y- then U-steps. Same end result as non-recursive Rovatti et al. (1998); asymptotically efficient simplex count (Mara 1976; Cottle 1982; Sallee 1982/84; Haiman 1991) but keeps fast simplex search. Figure 5.5: prism triangulation in 3-D (image).

#### 5.4.5. Local affine model estimation (3669)
- Per-region Frisch-style ID (Fantuzzi et al. 2002), affine version of 5.3.4. Region-i data matrix Xi stacks [y(t), y(t+1), u(t), u(t+1)]ᵀ rows, t=0..Ni-1; need k+Ni-1 ≤ Li, Ni large enough to avoid spurious dependence.
- Noiseless: increasing ((2k+2)×(2k+2)) covariances Σ(i)k; first singular ⇒ n = k; parameters a(i) = dependence coefficients of FIRST vector of Σ(i)n on the rest (note: shift convention vs 5.3.4's n=k−1; affine constant folds in).
- Regressor vectors xn(·) must actually lie in R(i)n of the chosen partition.
- EIV: u = u*+ũ, y = y*+ỹ, region-independent, zero-mean white, mutually independent; variances σ̄̃u, σ̄̃y. Σ(i)k = Σ*(i)k + Σ̄̃k (block diagonal repeated variances).
- Noisy problem: det[Σ(i)k − Σ̃k] = 0 with Σ̃k = diag[σ̃yI(k+1), σ̃uI(k), 0] over (σ̃u, σ̃y). Infinite solution set = curve Γ(i)k(σ̃y,σ̃u)=0 in first orthant of noise PLANE, concavity toward origin; constructive numerics in Beghelli et al. 1990. Non-crossing curves across k; for k≥n all curves share ≥1 point = true variances (σ̄̃u, σ̄̃y) — search starts there. Figure 5.6: singularity curve (image).
- Eigen properties (mirror of 5.3.4 with n=k convention): k<n → PD; k>n null-space dim = k−n+1; k=n dependence coefficients = a(i); k≥n+1 all (k−n+1) relations share same 2n+2 coefficients.
- Example: text cites Figure 5.3 (likely typo for 5.7 region) for n=3: curves k=3,4 share circled common point (σ̄̃u, σ̄̃y). [OCR? figure cross-ref inconsistent]

#### 5.4.6. Multiple-model estimation (3748, extends past 3790 — second half of 5.4.6 continues in agent-2 range)
- If noise physics are region-independent (same σ̄̃u, σ̄̃y for all regions), all regions share one common noise matrix Σ̄̃n satisfying det[Σ(i)n − Σ̄̃n] = 0 ∀i [5.66]; RHS degenerates to single point in noise plane → unique noise estimate + complete rejection.
- Uniqueness test: Σ(i)j = minor deleting row/col j; if across regions pairs i′,i″ exist matching minors with M > m (more regions than needed), the common set collapses to a single point [formulas not decoded].
- Figures 5.7 & 5.8: singularity surfaces for two regions, n=3, sharing the true-variance point (images).
- After n fixed: solve per-region regression Σ*(i)n-family relation for a(i), i=1..M [formula not decoded].
- Real data violate Frisch assumptions → NO common point across Γ(i)n=0 surfaces → per-region best-approximation noisy point via selection criterion.
- Order detection in real case: Γ(i)n+1=0 meets Γ(i)n=0 at a point where Σ*(i)n+1 is DOUBLE-singular; find (σ̃u,σ̃y) on Γ(i)n+1=0 minimizing second-smallest eigenvalue (min eigen=0, second ≈0). Sweep k: order n = k minimizing second eigenvalue of Σ*(i)k+1 — consistent (returns the common point when assumptions hold).
- Region-independent n for whole PWA model [5.44]: pick k with λ(i)k < ϵ, λ(i)k = smallest nonzero eigenvalue of Σ*(i)k+1 [inequality formula not decoded]; Fantuzzi et al. 2002 order-selection algorithm begins at 3800 (OUTSIDE my range — agent 2).

### Boundary/section placement (peek 3791-3800)
- 5.4.6 content runs through my 3790 cut and continues (order-selection algorithm statement at 3800); agent 2 (3791-4452) inherits mid-5.4.6.
- Next headers: 5.5 Fuzzy models 3867, 5.5.1-5.5.7 (3883-4085, incl. Gustafson-Kessel @~4051, optimal clusters @~4085), 5.6 Fuzzy model identification 4092, 5.7 4332, 5.8 4344, Ch6 ~4453.
- Figures 5.1-5.8 all present as `<!-- image -->` placeholders, no decoded numeric data; no numeric worked examples anywhere in 3135-3790.

## Puig Vol1 Ch5 pt.2 — Data-Driven Diagnosis, second half (source 3791-4452)

### 5.4.6 (continuation; section starts at 3748 — first-half agent's boundary at 3790)
- Piecewise-Frisch model order selection: since n unknown, increase hypothesized order k; the k whose **second eigenvalue of Σ*⁽ⁱ⁾_{k+1}** is minimal corresponds to order n. Criterion consistent: leads to the common point of the surfaces when Frisch assumptions hold.
- Order n of piecewise model [5.44] is region-independent; determined by choosing k fulfilling an inequality [formula-not-decoded] with ε arbitrary positive constant, λ⁽ⁱ⁾_k = minimal nonzero eigenvalue of Σ*⁽ⁱ⁾_{k+1}.
- Order-selection algorithm (Fantuzzi et al. 2002): 1) fix ε, k, M_k (initial order hypothesis); 2) construct partitions {A⁽¹⁾_k…A^(M_k)_k}; 3) cluster data into partitions; 4) compute Σ*⁽ⁱ⁾_{k+1} from clustered data in region A⁽ⁱ⁾_k; 5) test eq [5.69] — success ⇒ n=k exit, else k:=k+1 goto 2.
- After n chosen, params a⁽ⁱ⁾ cannot come from eq [5.68]: the surfaces Γ⁽ⁱ⁾_n=0 do NOT share the common point (σ̄̃_u, σ̄̃_y). Must consider **region-dependent noise variances** (σ̄̃⁽ⁱ⁾_u, σ̄̃⁽ⁱ⁾_y); relation [5.65] rewritten [formula-not-decoded] with Σ̃⁽ⁱ⁾_n = diag[σ̄̃⁽ⁱ⁾_u I_{n+1}, σ̄̃⁽ⁱ⁾_y I_n, 0].
- Per-region variances found by an optimization minimizing distances between (σ̄̃⁽ⁱ⁾, σ̄̃⁽ʲ⁾) pairs plus continuity constraints of eq [5.56] [formula-not-decoded]; H positive-definite weighting matrix; distance d [formula-not-decoded]; s⁽ⁱ⁾: q_i∈[0,1] ↦ (σ̃⁽ⁱ⁾_u, σ̃⁽ⁱ⁾_y) parameterizes curve Γ⁽ⁱ⁾_n=0. Cost = distance measure among noise-plane points + fulfillment-of-continuity term.
- Matrix A_n collects params a⁽ⁱ⁾ depending on the region variances. In real data item two (null eigenvalue multiplicity) only approximately holds: for k>n, null eigenvalue has algebraic multiplicity one, second-min eigenvalue near zero.
- Minimization of [5.71] is hard (2M independent variables) ⇒ **common polar-coordinate parameterization** of all surfaces Γ⁽ⁱ⁾_n: [formula-not-decoded] with ρ⁽ⁱ⁾ chosen so Γ⁽ⁱ⁾_n(ρ⁽ⁱ⁾cos(π/2 q), ρ⁽ⁱ⁾sin(π/2 q))=0, q∈[0,1]. Cost function [formula-not-decoded].
- Solution algorithm: 1) set ε>0, h>0, k=0, H; 2) k:=k+1; 3) solve [5.71] optimization for (σ̄̃⁽ⁱ⁾_u, σ̄̃⁽ⁱ⁾_y) and A_k; 4) compute λ⁽ⁱ⁾_min = second-min eigenvalue of Σ*⁽ⁱ⁾_k for all i… [formula-not-decoded] (test cut off in OCR).
- Parameterization is consistent: if data come from a continuous PWA dynamic system satisfying Frisch assumptions with region-independent noise, surfaces share a noise-plane common point, cost J(q)=0, variances identified exactly.
- After q* minimizing [5.74], construct Σ̃⁽ⁱ⁾_n and get a⁽ⁱ⁾ via relation [formula-not-decoded] — completes the multiple-model identification procedure; compatible with the ideal common-point case.
- Use: identification of models for real nonlinear processes via piecewise-affine prototypes, then exploited for **generation of residual diagnostic signals** (Fantuzzi et al. 2002).

### 5.5. Fuzzy data-driven approach to fault diagnosis
- Fuzzy set theory since 1965; modeling/control of dynamic systems a major application area; useful when no precise formal knowledge, strong nonlinearity, high uncertainty, time-varying characteristics (Babuška 1998).
- Fuzzy models = logical IF-THEN rule models; fuzzy sets as smooth interface between qualitative rules and numerical I/O data; rule-based nature allows natural-language info, transparent to interpretation. Computationally: flexible structures like neural nets approximating large classes of nonlinear systems.
- Neuro-fuzzy "marriage" improves approximation accuracy via optimization but transparency suffers ⇒ most neuro-fuzzy models are **gray-box** with little process insight.
- This section's approach: identify **transparent rule-based fuzzy models** (accurate prediction + insight). Focus on TS (Takagi-Sugeno 1985) internal rule structure; fuzzy model = composition of local affine submodels with smooth fuzzy transitions.
- Methodology: fuzzy clustering partitions data into subsets with linear behavior; links to linear regression combine fuzzy logic with system-ID tools; then model-based fault detection → residual generator from fuzzy model of a nonlinear dynamic process. Orientation: practically useful methodologies, academic + industry readership.

### 5.5.1. Fuzzy model identification
- "Fuzzy identification" = constructing fuzzy models from data. Two integration approaches (Babuška 1998):
  1) verbal expert knowledge → IF-THEN rules → structure, then fine-tune params (MFs, rule weights) with I/O data via layered-network learning = **neuro-fuzzy modeling**.
  2) **no prior knowledge**; model built from numerical data only; rules/MFs get a-posteriori interpretation; expert confronts with own knowledge, modifies rules, designs more informative experiments.
- Section focuses on approach 2 (automated acquisition from data) — obviates the knowledge-acquisition bottleneck (McGraw and Harbisson-Briggs 1989); expert takes active role in analysis/validation → emergent knowledge acquisition.
- Literature mostly aims at accuracy-only fits (Takagi-Sugeno 1985; Sugeno-Kang 1988; Johansen 1996; Wang 1995); alternatives for gray-box modeling: nonlinear regression (Seber & Wild), splines, neural nets. Requirement here: model predicts AND gives insight, easier to adapt to changed design/operating conditions.
- Fuzzy models = local modeling class: decompose complex problem into simpler subproblems; fuzzy sets represent uncertainty of the decomposition, smooth transitions, knowledge integration.
- TS model = local linear/affine submodels each approximating behavior around one working point; submodel scheduling via smooth fuzzy function of state (Klir & Yuan 1995).
- Structure matches **multiple-model** definition (Leontaritis & Billings 1985a,b) — same as section 5.4.1: local models + smooth (fuzzy) fusion of local outputs.
- Common two-step procedure in fuzzy modeling/ID algorithms (Babuška & Verbruggen 1995; Babuška et al. 1997): step 1 determine operating regions via heuristics or data clustering; step 2 identify each submodel's params by least-squares **or Frisch scheme**.
- Fuzzy ID = search for a decomposition balancing model complexity vs accuracy (system complexity non-uniform); automated decomposition generation from data via fuzzy clustering algorithms.

### 5.5.2. Takagi-Sugeno prototypes
- TS fuzzy model (Takagi & Sugeno 1985; Figure 5.9 — image): rule consequents are crisp functions of inputs [formula-not-decoded]; x(t)∈ℜ^p antecedent var, y_i∈ℜ consequent; R_i = i-th rule, K rules; A_i antecedent fuzzy set with multivariate MF [formula-not-decoded].
- Antecedent 'x(t) is A_i' usually a logical combination of univariate propositions, conjunctive form [formula-not-decoded].
- Consequents f_i = instances of one parameterized structure, only params vary. Affine linear form [formula-not-decoded]: a_i param vector, b_i scalar offset ⇒ **affine TS model**; consequents = hyperplanes in ℜ^{p+1}; antecedent = fuzzy validity region for the affine consequent; global model = smoothed piecewise approximation of a nonlinear surface (approximation properties: Rovatti 1996).
- Special case b_i=0 ⇒ **homogeneous TS model** [formula-not-decoded]; weaker approximation than affine (Fantuzzi & Rovatti 1996).
- a_i=0 ⇒ constant consequents ⇒ **singleton model** [formula-not-decoded].
- Degree of fulfillment β_i(x): multivariate antecedent ⇒ β_i = μ_Ai(x); with logical connectives ⇒ combination of membership degrees via fuzzy logic operators (Jager 1995; Babuška 1998).
- TS inference reduces to fuzzy-mean defuzzification [formula-not-decoded]; normalized degree of fulfillment [formula-not-decoded] ⇒ affine TS model = **pseudo-linear model with input-dependent parameters** [formula-not-decoded]; a(x), b(x) convex linear combinations of a_i, b_i [formula-not-decoded].
- TS model = mapping from antecedent space to a convex region (polytope) in parameter space of the quasi-linear system [5.84].
- Example: TS rules whose consequents are **linear ARX models** (n_u, n_y integers related to system order) [formula-not-decoded].

### 5.5.3. Data-driven Fuzzy modeling
- Effective nonlinear-ID approach: partition data into subsets, approximate each by a simple model (Babuška & Verbruggen 1995); fuzzy clustering gives partitions with **gradual rather than abrupt** transitions. Intro-level treatment (Babuška 1998).
- Deeper references: Duda & Hart 1973, Bezdek 1981, Jain & Dubes 1988, Bezdek & Pal 1992, Backer 1995. Notation follows Bezdek (1981).

### 5.5.4. Clustering methods
- Cluster analysis: classify objects by similarity, organize data into groups; unsupervised (no prior class identifiers); few distributional assumptions → useful with little prior knowledge; reveals underlying structure → classification, pattern recognition, and **complexity reduction in modeling/optimization**.
- Data: observation z_k=[z_1k…z_nk]^T ∈ ℜ^n of n measured variables; N observations Z={z_k} as n×N matrix [formula-not-decoded]. Columns = patterns/objects, rows = features/attributes, Z = pattern/data matrix.
- For dynamic-system modeling/ID in fault diagnosis: columns = time-signal samples, rows = physical variables of the diagnosed system; **past values included in Z to represent dynamics**.
- Cluster = group more similar internally than across clusters (Bezdek 1981; Jain & Dubes 1988); in metric spaces similarity via distance norm; distance to data vectors or to cluster **prototypes** (found by the algorithm simultaneously with the partition); prototypes may be vectors or geometrical objects (linear/nonlinear subspaces, functions); clusters differ in shape/size/density.
- Clustering as objective-function (c-means) class vs hard/fuzzy: hard = classical sets (belong or not); fuzzy = simultaneous membership with degrees; boundary objects get partial memberships in [0,1] (OCR shows "O and 1" — [OCR?] should be 0 and 1).
- Objective-function methods → nonlinear optimization for local extrema → least-squares optimization ⇒ close relationship to statistical regression & system identification; the presented algorithm optimizes the basic c-means objective = **fuzzy c-means (FCM) algorithm** (Dunn 1974).

### 5.5.5. Fuzzy c-means clustering algorithms
- FCM minimizes fuzzy functional (Bezdek 1981) [formula-not-decoded]: U = fuzzy partition matrix [formula-not-decoded]; V = cluster prototypes/centers to be determined [formula-not-decoded]; D²_ik = squared distance norm [formula-not-decoded]; m = weighting exponent controlling fuzziness [formula-not-decoded].
- Cost = squared distance of each z_k to prototype v_i weighted by membership power (μ_ik)^m; J measures total variance of z_k about v_i.
- Solve via first-order stationary conditions: adjoin fuzzy-partition constraint [formula-not-decoded] with Lagrange multipliers [formula-not-decoded], set gradients of J̄ wrt U, V, λ to zero. For D²_ikA>0 ∀i,k and m>1, minimizer must satisfy [formula-not-decoded] (prototype update) and [formula-not-decoded] (membership update); these satisfy partition constraints [5.97]/[5.98] [formula-not-decoded ×2].
- v_i = weighted mean of data belonging to the cluster (weights = membership degrees) ⇒ name "c-means".
- Alternating optimization: loop U^(l), V^(l); terminate when max_ik |μ^(l)_ik − μ^(l−1)_ik| < ε; convergence proven by Bezdek (1980).
- **Number of clusters c is the most important parameter** (others secondary on U); choice of c deferred to 5.5.7.

### 5.5.6. Gustafson-Kessel clustering algorithm
- Family of FCM-derived algorithms; key one = **Gustafson-Kessel (GK)** (Gustafson & Kessel 1979): extends FCM with an **adaptive distance norm** to detect clusters of different geometrical shapes in one data set.
- Each cluster has its own norm-inducing matrix A_i: norm D²_ikA_i [formula-not-decoded]. A_i are optimization variables in the c-means functional ⇒ each cluster adapts the distance norm to local topological structure. A = c-tuple (A_1…A_c); GK objective functional [formula-not-decoded] with U∈M_fc, V∈ℜ^{n×c}, m>1.
- Stationary-point solutions [formula-not-decoded] where PD^n = space of n×n positive-definite matrices; for fixed A, FCM conditions [5.95]/[5.96] apply directly.
- Problem: [5.100] is **linear in A_i** — J can be made arbitrarily small by making A_i less positive-definite ⇒ constraint needed: **fix det(A_i)** [formula-not-decoded] = optimize cluster shape at constant cluster volume.
- Lagrange multiplier ⇒ A_i expression [formula-not-decoded] with F_i = **fuzzy covariance matrix** of cluster i [formula-not-decoded].
- Without prior knowledge cluster volumes ρ_i fixed at 1; **drawback: GK finds only clusters of approximately equal volumes** (constraint [5.102]).
- Eigenstructure of F_i = cluster shape/orientation: hyperellipsoid axis-length ratios = ratios of sqrt eigenvalues of F_i; axis directions = eigenvectors (Babuška 1998). **Flat hyperellipsoids ≈ hyperplanes represent linear subspaces**; eigenvector of smallest eigenvalue = hyperplane normal → computes optimal local linear models from the covariance matrix (Babuška 1998). ← this is the link from GK clustering to local linear submodels.

### 5.5.7. Optimal number of clusters
- Real data without a-priori structure: c must be assumed; the algorithm finds c clusters whether present or not. Two approaches (Babuška 1998):
  1) cluster for different c values and assess partitions with **scalar validity measures** (several proposed in literature);
  2) start with sufficiently large c, **successively merge** similar/compatible clusters per predefined criteria.

### 5.6. Fuzzy model identification
- Decompose nonlinear identification into locally linear models via **product space fuzzy clustering**; procedure outline + structure selection + regressor choice; product-space clustering principle emphasized.
- Figure 5.10 "Fuzzy clustering phases" (image): iterative identification procedure, steps repeatable for different parameter choices. Steps:
  1) **Data collection** — determines information content; excite system over entire variable range in amplitude & frequency; sampling period, anti-aliasing filters, experiment duration (Norton 1986; Ljung 1999).
  2) **Structure selection** — pick relevant I/O variables + model dynamics structure/order; translates dynamic-system ID into a regression problem solvable quasi-statically; can be automated by comparing candidate structures on performance measures, or user-chosen.
  3) **Data clustering** — nonlinear static regression approximated by local linear submodels; location+params found by clustering data; each cluster = fuzzy region with local affine submodel; number of clusters chosen (may repeat step 3).
  4) **TS model** — params identified from fuzzy partition matrix + cluster prototypes; membership functions and model params extracted automatically.
  5) **Validation** — accept/reject; on rejection repeat loop with different settings (Norton 1986; Ljung 1999); beyond numerical simulation validation, **interpretation matters**: analyze rule coverage of input space; fill incomplete rule base with prior knowledge, local linearization, or first-principle models.
- Structure estimation subproblems:
  1) **I/O variable selection** — often unclear for multivariable/closed-loop systems; based on modeling aim; partially automatable by comparing candidate models w.r.t. performance measures (Guidorzi 1975, 1981).
  2) **System's order representation** — transform dynamic ID to static regression (Billings & Voon 1983a; Leontaritis & Billings; Chen & Billings 1989; Sjöberg et al. 1995); choice from a-priori knowledge + intuition + physical laws; mapping from time-signal domain to state-determining **regressors**; output (regressand) = static map of regressor space; regressor choice crucial — wrong choice ⇒ useless models.
  3) **Fuzzy model complexity** — number of rules; literature calls this "structure identification" (Sugeno & Kang 1988); with fuzzy clustering, **number of clusters is the primary parameter**; complexity also depends on model type (different function-approximation means ⇒ different complexity for same accuracy); practical accuracy-vs-complexity trade-off.

### 5.6.1. Nonlinear model identification
- Fuzzy systems = general function approximators → general nonlinear regression (Wang 1992; Kosko 1994; Zeng & Singh 1996). Nonlinear regression: static dependence of regressand y∈Y⊂ℜ on regression vector x=[x_1…x_p]^T over domain X⊂ℜ^p; elements = regressors, X = regressor space; data generator: y ≈ f(x) [formula-not-decoded]; f deterministic, ≈ because y not an exact function of x.
- Dynamics example: **EE model** (Kalman 1982b, 1990) [formula-not-decoded], ε = error term.
- Regression aim: construct F(x) approximating f(x) over whole X, not just data; "reasonable" depends on purpose; for prediction, accuracy is key; integral error I over X [formula-not-decoded] usually uncomputable (f known only at data points) ⇒ average prediction error J over available data [formula-not-decoded], N samples.
- Minimizing true I ⇒ best model for selected structure; minimizing J only guarantees least-squares fit to available data ⇒ **separate validation step** needed over the full region of interest X.
- Other goal: model to analyze/understand the generating system; fuzzy strength = simple local submodels as rules, combinable with analytical models (TS local linear models from 5.5.2).
- **NARX** (Nonlinear AutoRegressive with eXogenous input) model widely used with neural nets (Hunt et al. 1992a), RBF (Chen et al. 1991), CMAC (Brown & Harris 1994), fuzzy (Lee et al. 1994), neuro-fuzzy: relation y(k+1)=F(y(k),…,y(k−n_y+1),u(k),…,u(k−n_u+1)) [formula-not-decoded]; k discrete time; n_u,n_y integers related to system order; F = fuzzy model; regression vector x(k)=[y(k),…,y(k−n_y+1),u(k),…,u(k−n_u+1)]^T; regressand = ŷ(k+1); static nonlinear regression approximates F.
- Structure ID = choose model type + n_y, n_u: a-priori knowledge gives first guess of parameter range, then minimize a criterion within it; most direct = mean-square prediction error [formula-not-decoded] **evaluated on a different data set** to avoid fitting noise.
- Start with a **linear** model for structure (simpler, numerically more robust): singular value & coherence tests (Verhaegen & Dewilde 1992), information-theoretic criteria (Akaike 1974; Rissanen 1978); best linear structure = starting point for nonlinear modeling; cluster validity measures guide order + number of clusters within the structure.
- y scalar ⇒ MISO assumed; MIMO via input-output models in two ways: vector-valued F (typical of neural nets) vs **decomposition into coupled MISO systems** (fuzzy modeling's preferred way) — more flexible: each output may have a different nonlinearity type (one complex, another linear in the same region); decomposition reduces number of MFs and rules.

### 5.6.2. Product space clustering identification
- Principle: approximate a nonlinear regression problem by decomposing into several **local linear subproblems**. Advantages over global nonlinear models (e.g. neural nets): structure easy to understand/interpret qualitatively & quantitatively; integrates empirical knowledge + measured data + mathematical models; computational advantages; straightforward adaptive/learning algorithms (Murray-Smith & Johansen 1997).
- Fuzzy clustering applied in **product space of regressors and regressand X×Y**. X = matrix in ℜ^{N×p} with regression vectors x_k^T in rows; y = column in ℜ^N of regressands y_k [formula-not-decoded]; N samples, p regressor dimension; for I/O dynamic models X contains shifted input/output data.
- Geometric view: unknown nonlinear y=f(x) = **regression surface/hypersurface** in (X×Y)⊂ℜ^{p+1}; data = sample points from it; clustering finds local linear models approximating the surface optimally.
- Clustered data set Z = concatenation of regressor matrix X and regressand y [formula-not-decoded]; subset of Cartesian product space defined by the nonlinear relation [5.105] [formula-not-decoded].
- Z partitioned into fuzzy subsets by clustering algorithms **capable of detecting linear substructures** (per 5.5.3). Cluster covariance = variance of data in cluster.
- Clustering algorithm C as a mapping C: (Z × N) → (M_fc × ℜ^{n×c} × PD^n) [formula-not-decoded]: c clusters, U_o initial partition matrix, m and ε algorithm parameters; U = membership degrees with prototypes V.
- Cluster covariance F_i holds shape/orientation info: j-th eigenvalue λ_ij and unit eigenvector φ_ij (Babuška 1998); eigenvalues ordered [formula-not-decoded] with matching eigenvector labels.
- **Eigenvectors φ_i1…φ_i(n−1) span the cluster's linear subspace; φ_in (smallest eigenvalue λ_in) = normal to it = "smallest eigenvector"**.
- Structure diagnostic via eigenvalues: intrinsic dimension p ⇒ λ_in orders of magnitude smaller than the rest (n-dim data locally = linear combination of n−1 variables). If all eigenvalues same order ⇒ **no functional relation detected between regressors and regressand — structure not rich enough**; several relatively small eigenvalues ⇒ local dimension lower than assumed OR data not rich enough (Babuška 1998).

### 5.6.3. Fuzzy clustering model identification
- Fuzzy clustering approximates data by local linear models, each = a fuzzy subset of the identification data set; to get a prediction model, extra step needed to make a model **independent of the identification data** — representable as rule base or fuzzy relation (Babuška 1998). Section reviews constructing TS fuzzy models from product-space fuzzy partitions: antecedent MF generation + consequent parameter estimation.
- Each cluster = local linear approximation of the regression hypersurface; global model = set of affine TS rules [formula-not-decoded].
- Antecedent fuzzy sets A_i: computed analytically in the antecedent product space OR extracted from the fuzzy partition matrix. Consequent params a_i, b_i: estimated from data by section 5.3 methods (**Frisch scheme procedure**) OR extracted from the eigenstructure of the cluster covariance matrices.

### 5.6.4. Antecedent membership function estimation
- Two routes: project the fuzzy partition onto antecedent variables, or compute membership degrees directly in the antecedent product space; **the second is used** for TS identification per Babuška (1998, 2000).
- **By projection**: project multi-dimensional fuzzy sets (pointwise, rows of U) onto individual antecedent variables; orthogonal projection on original regression variables, or **eigenvector projection using the p largest eigenvectors** of cluster covariance matrices for new transformed antecedent variables — useful for clusters **opaque to the axes** of regression space (axis-orthogonal projection insufficient).
- Projecting row μ_i of U onto variable x_j gives pointwise fuzzy set A_ij; for prediction, MFs must handle inputs not in Z ⇒ approximate pointwise MF by a parametric function.
- **Piecewise-exponential MFs** fit the envelope of projected data by numerical parameter optimization; advantages: projected MFs always approximable as **convex** fuzzy sets; **asymmetric** MFs can reflect actual partition of the nonlinear regression problem.
- **Multi-dimensional MFs**: analytic via inverse distance from cluster prototype; membership computed for the whole input vector (no decomposition); TS antecedents = simple propositions with multi-dim fuzzy sets [5.116], β_i(x)=μ_Ai(x).
- F_x=[f_ij], 1≤i,j≤p = cluster covariance minus its last column; norm-inducing matrix [formula-not-decoded]; v_x_i = projection of cluster center onto X; norm [formula-not-decoded] measures antecedent-vector-to-center distance.
- Distance→membership transform, two options:
  - clustering-algorithm formula [formula-not-decoded]: rule degree relative to other rules; memberships of all rules sum to one ⇒ classified **probabilistic**.
  - independent-of-other-rules transform [formula-not-decoded].
- Both centered at cluster centre ⇒ same position in antecedent space, but shapes may differ significantly (Babuška 1998).

### 5.6.5. Estimating consequent parameters (part 1 of 2 — continues past 4310)
- Several methods. (a) Geometric: consequent params computed directly from cluster prototypical points + **smallest eigenvectors** of cluster covariance matrices; assumes errors in **both regressors and regressand** = **total least squares (TLS)** solution of local linearization around cluster centre (Van Huffel & Vandewalle 1991).
- (b) Optimal-w.r.t.-model-output params from data by ordinary least squares or the section-5.3.4 approach: minimize total prediction error via TS defuzzification formula [5.82], or per-local-model errors as **c independent weighted least-squares problems**.
- TLS example preferred when TS model serves as a **predictor** (Babuška 1998).
- Geometry: c clusters ≈ p-dimensional linear subspaces of regression space; φ_in (smallest eigenvalue λ_in) = normal to the hyperplane spanned by remaining eigenvectors; denote φ_i = φ_in. With z^T=[x^T, y], prototype v_i: implicit normal form φ_i^T(z − v_i)=0 [formula-not-decoded].
- Partition v_i^T=[(v_x_i)^T, v_y_i] and φ_i^T=[(φ_x_i)^T, φ_y_i]; [5.121] rewritten [formula-not-decoded]; inner product [formula-not-decoded]; explicit hyperplane [formula-not-decoded]; compare with affine TS consequent [5.116] ⇒ a_i = [formula-not-decoded] (essentially −φ_x_i/φ_y_i), b_i = [formula-not-decoded].
- a_i from [5.125] = solution of a **weighted TLS problem** locally around v_i, weights = membership degrees in row i of U; v_i = local operating point; b_i from a_i + cluster centre.
- Alternative: after clustering, run the **Frisch scheme identification** per data subset (Frisch 1934; Beghelli et al. 1990) to estimate TS params of each affine submodel, per section 5.4.5 rules (Simani et al. 1998, 1999; Fantuzzi et al. 1998; Rovatti et al. 2000; Simani 2000); the noisy-measurement ID of section 5.3.2 adapted to affine models.
- TS SISO model [5.82] structure ID in cluster i (i=1..c): matrices defined [formula-not-decoded], and [formula-not-decoded].
- Frisch assumptions (Frisch 1934; Kalman 1982b; Beghelli et al. 1990): noises ũ(t), ỹ(t) **additive** on I/O data u*(t), y*(t) and **region independent** (here: per-cluster).
- Positive-definite Σ⁽ⁱ⁾_k for cluster-i sequences: Σ⁽ⁱ⁾_k = Σ*⁽ⁱ⁾_k + σ̄̃Σ_k [formula-not-decoded]; unknown noise variances σ̄̃_u, σ̄̃_y found by solving [formula-not-decoded] in σ̃_u, σ̃_y with Σ̃_k = diag[σ̃_y I_{k+1}, σ̃_u I_k, 0].

### 5.6.5. Estimating consequent parameters (part 2 of 2)
- Surfaces of type [5.130] have **at least one common point** (σ̄̃_u, σ̄̃_y) = the true variances of noise on input and output data ⇒ if noise characteristics are common to all clusters AND Frisch assumptions hold (independence between I/O sequences, additive noise, noise whiteness), the identification search starts by determining this point in noise space.
- Real case: assumptions relaxed ⇒ **no common point among surfaces Γ⁽ⁱ⁾_n=0** in the noise plane ⇒ unique solution impossible.
- Workaround for local fuzzy model ID: find (σ̃_u, σ̃_y) ∈ Γ⁽ⁱ⁾_{n+1}=0 making Σ*⁽ⁱ⁾_{n+1} **closest to the double-singular condition** — recovers the common point that would exist if Frisch assumptions held.
- Per-cluster noises (σ̄̃⁽ⁱ⁾_u, σ̄̃⁽ⁱ⁾_y): relation rewritten [formula-not-decoded] with Σ̃⁽ⁱ⁾_n = diag[σ̄̃⁽ⁱ⁾_u I_{n+1}, σ̄̃⁽ⁱ⁾_y I_n, 0].
- Build Σ̃⁽ⁱ⁾_n, get model parameters in each cluster via relation [formula-not-decoded] for c clusters ⇒ **completes the multiple-model identification procedure in the fuzzy environment**.

### 5.7. Conclusion
- Chapter covered off-line identification of linear + nonlinear static/dynamic systems from noisy data; models usable for fault diagnosis: linear, piecewise-affine (linear), fuzzy.
- PWA & fuzzy = multiple-model: several local affine submodels, one per operating condition; params/orders estimated with the **Frisch Scheme** for linear systems. Nonlinear case: continuity constraints between local linear dynamic models forced to get a continuous PWA prototype; for non-fuzzy models solved by an optimization technique; Frisch properties enhance constraint fulfillment.
- Nonlinear process ID also via neural nets / fuzzy / neuro-fuzzy; **product space fuzzy clustering** partitions data into fuzzy subsets locally described by linear submodels; select regression structure first (to represent dynamics), then cluster in regressor×regressand space; each cluster = local linear model ⇒ clustering must detect clusters lying in linear subspaces.
- Two final tasks for TS construction: **antecedent MF generation** + **consequent parameter estimation**; consequents from cluster centers & covariances, or least squares, or local Frisch scheme per submodel.
- Fuzzy ID algorithms for both fuzzy partitions and TS structures come from proper fuzzy clustering + identification procedures.

### 5.8. References
- ~65 entries, no prose. Reference clusters anchoring the chapter: Frisch scheme (Frisch 1934; Beghelli-Guidorzi-Soverini 1990; Beghelli-Castaldi-Soverini 1994a/b; Beghelli et al. 1997; Beghelli & Soverini 1992); Kalman noisy-data ID (1982a/b, 1984, 1990); fuzzy modeling/cluster core (Babuška 1998 Fuzzy Modeling for Control + Babuška 2000 Fuzzy Modeling & Identification Toolbox 3.1 Delft; Babuška & Verbruggen 1995; Babuška-Keizer-Verhaegen 1997; Bezdek 1980/1981; Gustafson & Kessel 1979; Dunn 1974; Hathaway & Bezdek 1983 switching regression + fuzzy clustering); TS lineage (Takagi & Sugeno 1985; Sugeno & Kang 1988; Rovatti 1996; Fantuzzi & Rovatti 1996; Wang 1992/1995; Kosko 1994; Zeng & Singh 1996); PWA-in-noise research line (Fantuzzi-Rovatti-Simani-Beghelli 1998; Fantuzzi-Simani-Beghelli-Rovatti 2002 IJC; Simani-Fantuzzi-Rovatti-Beghelli 1998/1999; Rovatti-Fantuzzi-Simani 2000 DSP implementation; Simani 2000 SAFEPROCESS sugar cane crushing multi-model FDI); NARX/NARMAX (Chen & Billings 1989; Leontaritis & Billings 1985a/b; Billings & Voon 1983a/b; Billings & Voon 1986 correlation validity tests; Johansen & Foss 1993); TLS (Van Huffel & Vandewalle 1991); multiple models (Murray-Smith & Johansen 1997; Skeppstedt et al. 1992); ill-posed regularization (Tikhonov & Arsenin 1977; Morozov 1984); n-cube triangulation (Cottle 1982; Haiman 1991; Mara 1976; Sallee 1982/1984 — behind the PWA partitions); classical ID texts (Ljung 1999; Norton 1986; Söderström & Stoica 1987; Åström absent here).

## Puig Vol1 Ch6 — AI Approaches to Diagnosis (source 4453-5060)

### 6.1 Introduction
- AI has always targeted diagnosis as a high-level cognitive task; historically framed as classification linking symptoms to causes (MYCIN lineage, Shortliffe 1976).
- Console 2000 definition: diagnosis = given a system + observations from a faulty situation, determine what is wrong (and what to repair to restore normal state).
- AI systems design isolates three modules (Balakrishnan & Honavar 1998): knowledge source (root causes + symptoms), process (generate symptoms from observations), reasoning process (link symptoms to causes). Contrasts with the control-theory framing (Venkatasubramanian 2003, Gertler 1998).
- Four major AI diagnosis categories (as bullets, per the chapter's classification):
  - Knowledge-based systems (KBS): domain/expertise knowledge, no explicit math models; causal symptom↔cause relations explored by forward/backward chaining; domain-specific, no learning; examples: MYCIN (medical), SOPHIE (electronics troubleshooting), oil extraction, financial.
  - Case-based reasoning (CBR): case collection, no inference model; four-R cycle Retrieve/Reuse/Revise/Retain; lazy learning; needs many cases.
  - Machine learning: induced symptom→diagnosis relations from examples; lacks self-explanation; needs many samples.
  - Model-based: analytic physics-based models; predicted fault-free behavior vs observation; deviations = symptoms; estimated components = fault candidates; model reusability is the advantage, model complexity the drawback.
- Chapter scope: KBS + model-based diagnosis (CBD). CBR ~ lazy learning; data-driven models were Ch 5. Model-based is theoretically soundest but tools are domain-narrow.

### 6.2 Case studies
- Static case: binary full adder (Reiter 1987) — 2 AND (A1,A2), 2 XOR (X1,X2), 1 OR (O1), all five can be faulty; inputs a,b,cin; outputs s,cout; unobserved x,y,z; nominal gate equations [formula-not-decoded].
- Dynamic case: three-tank system (Ding 2014; adapted Escobet et al. 2019) — tanks T1,T2,T3 same height/area A; single input qi into T1; pipes q12, q23 between tanks; outflow q30 from T3; sensors LT1 (level T1), LT2 (level T3), FT1 (flow q23).
- Six faults: 3 pipe blockages + 3 tank leakages, modeled via parameters Stuckqjk and LeakageTj set to 0/1 → covers both multiplicative and additive faults in one model.
- Model: mass balances ḣTj, flows q12/q23/q30/qf1..qf3 from Torricelli-type laws [formula-not-decoded]; measured hT1, hT3, q23; qi known; initial levels zero unless configured.

### 6.3 Knowledge-based diagnosis systems
- KBS = explicit symbolic knowledge + coherence with it; minimum two parts: knowledge base (declarative) + inference engine; typically also working memory and user interface (Fig 6.3).
- Production rules: If <antecedent> Then <consequent>; semantics: antecedent true in working memory ⇒ conclude consequent, added as fact.
- MYCIN (meningitis diagnosis/therapy): paradigm rule-based ES; introduced Certainty Factors for uncertainty (e.g. 0.7 on consequent); Fig 6.4 natural-language rule: concludes "identity of organism is streptococcus" iff all antecedent premises in working memory.
- Two search directions: forward chaining (facts→solution) vs backward chaining (goal-directed, works backwards consequent→antecedent); backward chaining wins in diagnosis KBS because it implicitly schedules new-data acquisition around the current goal.
- 6.3.1 Diagnosis task = generate/test/discriminate hypotheses explaining faulty behavior to select repairs; KBS use explicit mostly-qualitative models, almost all classification models (incl. causal networks): failures = classes characterized by symptom abstractions; solution = classes compatible with observations.
- Classification ES examples: MYCIN, INTERNIST, CENTAUR (medicine, where quantitative models are lacking); MORE (hydrocarbon extraction), MUD (drilling fluids), SOPHIE (electronic circuit faults). Formal models: Reggia 1983, Peng & Reggia 1990; survey Stefik 2014.
- 6.3.1.1 Clancey heuristic classification (1985): abstract-data ↔ abstract-solution matching, three steps: abstraction (semantically richer data from raw), matching (select abstract solutions), refinement (specialize with more data); knowledge acquired from experts; failure families in a hierarchy; Fig 6.6 MYCIN fragment; Fig 6.7 shows the actual rule hides model + strategic/context knowledge in premises.
- 6.3.2 Physical devices: classification works if there is contrasted diagnostic experience; KB systems are built for one (usually stationary, control-maintained) operating point — nonlinear systems change symptom nature at other points → one model per operating point needed.
- Qualitative abstraction of raw signals: usually 3 abstract values {0,+,-} (normal/high/low), sometimes 5, rarely 7+; same symbols for first derivatives.
- Three-tank worked rules (assumes no sensor fault + single fault):
  - If FT1 = − Then upstream leak or blockage (first abstract solution).
  - If upstream leak/blockage AND LT2 = 0 Then leak at T2 (refinement via other sensors).
- 6.3.3 Limits of KBS: mature tech; ontologies SAREF (Daniele 2018) and ifcOWL help knowledge modeling; suitable when experience exists and no other knowledge form fits; NOT adequate for new/reconfigurable devices.
- Core weaknesses: costly knowledge acquisition dependent on experts; device dependence (similar components show different failure patterns); classification limits — multiple faults hard, unforeseen failures out of scope → brittleness; large-KB consistency maintenance is lifecycle-critical.

### 6.4 Model-based diagnosis
- Shift came when KBS limits (domain specificity, large-KB maintenance) bit; AI turned to physical laws as models: "reasoning from structure and behavior" (Davis 1982); survey Hamscher et al. 1992, Poole 1991.
- Consistency-based diagnosis (CBD) = most popular; first-order-logic roots (Reiter 1987); began with component-oriented combinatorial/static time-invariant systems; extended to dynamic/hybrid/distributed without a formal FOL theory, following four Reiter ideas:
  - system = composition of component models (compositional modeling);
  - only structure (components + interconnections) + component behavior models used for reasoning;
  - only correct (fault-free) behavior models required;
  - discrepancies between expected and observed behaviors incriminate components — NO exoneration (a component is not assumed correct merely because there is no evidence against it).
- GDE (General Diagnostic Engine, de Kleer & Williams 1987): first domain-independent framework for multiple-fault diagnosis using only correct-behavior models.
- 6.4.1.1 Theoretical framework rests on the no-function-in-structure principle: each component's local model assumes nothing about its environment (other components, operating point); only terminal I/O relations + internal parameters → deviations trace to correctness assumptions ¬AB(c); enables model libraries/reuse; component models are acausal constraints among variables [component model pattern formula-not-decoded; AND-gate example: XORgate(c) ∧ ¬AB(c) ⇒ Output = ...].
- Any use of a component model records correctness assumption ¬AB(c); discrepancy → trace dependencies to fault candidates ⇒ theorem prover must couple with a dependency-recording engine (DRE).

#### Reiter's formalization (definitions as bullets)
- Def 6.1 System = triplet (SD, COMPS, OBS): SD finite set of FOL sentences (structure = correct-behavior models ¬AB(x) of components), COMPS finite set of constants, OBS finite FOL sentences; no diagnosis without observations.
- Def 6.2 D(Cp,Cn) = [∧c∈Cp AB(c)] ∧ [∧c∈Cn ¬AB(c)] — declares Cp faulty, Cn healthy.
- Def 6.3 Diagnosis: Δ ⊆ COMPS; D(Δ, COMPS−Δ) is a diagnosis iff SD ∪ OBS ∪ {D(Δ,COMPS−Δ)} is satisfiable (removing Δ restores logical consistency).
- Def 6.4 Minimal diagnosis: no proper subset Δ′ ⊂ Δ is a diagnosis; CBD only seeks minimal candidates (parsimonious solution space).
- Hypothesis 6.1 Minimal diagnosis hypothesis: if D(Δ,COMPS−Δ) minimal diagnosis, every superset Δ′ ⊇ Δ is also a diagnosis; holds only with correct-behavior models + no exoneration (breaks if faulty-behavior models or exoneration used).
- Def 6.5 AB-literal: AB(c) or ¬AB(c). Def 6.6 AB-clause: disjunction of AB-literals with no complementary pair.
- Def 6.7 Conflict: AB-clause entailed by SD ∪ OBS; positive conflict = only positive AB-literals. Intuition: at least one component in the conflict set is faulty; also = set of correctness assumptions supporting an inconsistent symptom (GDE interpretation).
- Def 6.8 Minimal conflict: no proper subset is a conflict. Def 6.9 Hitting set: H ⊆ ⋃S∈C S hitting every S ∈ C; minimal if no proper subset hits.
- THEOREM 6.1 (Reiter): D(Δ,COMPS−Δ) is a minimal diagnosis ⟺ Δ is a minimal hitting set of the collection of minimal conflicts.
- Minimal hitting-set computation is expensive for large collections; incremental computation fits diagnosis because conflicts arrive sequentially.

#### Full-adder worked example (numbers/structure)
- COMPS = {X1,X2,A1,A2,O1}; SD = gate axioms XOR/AND/OR ∧ ¬AB(c) ⇒ boolean relation + wiring equations; OBS = terminal values.
- Scenario 1 inputs {1,1,1 carry-in chain}: expected outputs {Output(X2)=1, Output(O1)=1} (=11 binary); empty diagnosis is minimal (satisfiable).
- Scenario 2 observed Output(X2)=0, Output(O1)=1: propagate ¬AB(X1) ⇒ Output(X1)=0; ¬AB(X2) ⇒ predicted Output(X2)=1 ≠ observed 0 ⇒ conflict {X1,X2}, minimal; minimal diagnoses from hitting set: {X1} and {X2}.
- Non-causal reasoning bonus: theorem prover can infer Input2(X1)=0 backwards from Output(X2)=0 — same conflict {X1,X2}.
- Scenario 3 with also Output(O1)=0: second chain infers Output(O1)=1 ≠ 0 ⇒ second conflict {X1,A2,A1,O1}; its solo candidates {X1},{A2},{A1},{O1}; hitting set over both conflicts ⇒ minimal diagnoses {X1}, {X2,A2}, {X2,A1}, {X2,O1} — one singleton + three double-fault candidates.

#### 6.4.1.2 GDE computational framework
- Reiter gives diagnosis-from-conflicts but no way to compute conflicts; a naive theorem prover infeasible for hundreds of formulas ⇒ GDE (de Kleer & Williams 1987), first automated multiple-fault diagnoser.
- GDE scope: only component-malfunction faults (not FDI-style parameter faults); sensors must be modeled as components to be diagnosable; evidence only rejects inconsistent modes — no exoneration.
- Incremental loop: (1) generate every possible prediction from available observations; (2) detect every symptom (prediction-vs-observation or prediction-vs-prediction discrepancy); (3) identify minimal conflicts per discrepancy; (4) incrementally generate minimal diagnosis candidates.
- Inference propagates in every direction (not only causal) through all constraints.
- DRE = ATMS (Assumption-based Truth Maintenance System, de Kleer 1986a/b/c): builds an implicit graph online; node types: facts (true, e.g. observations), assumed nodes (¬AB(c) ⇒ label {c}), derived nodes; justification = node set used in an inference; environment = assumption set for a justification chain; ATMS label = set of minimal environments where datum true.
- Discrepancy ⇒ ATMS collects labels used ⇒ falsity node with NOGOOD environment ⇒ minimal conflict automatically.
- Traced ATMS labels for scenario OBS={1,1,1,Output(X2)=0,Output(O1)=0}: step labels {{X1}} → {{X1,X2}} NOGOOD (conflict 1) → {{X1,A2}}, {{A1}}, {{X1,A2,A1,O1}} NOGOOD (conflict 2); incremental hitting set ⇒ {{X1}, {X2,A2}, {X2,A1}, {X2,O1}} — same as Reiter; redundant backwards nogoods skipped (efficiency).
- GDE also selects new observations by maximizing information gain (information theory); usually little room for extra measurements in real systems — details in de Kleer & Williams 1987 / Escobet et al. 2019 ch. 5.

#### 6.4.1.3 Computational alternatives to GDE
- Two problems vs real complex dynamic systems: (1) ATMS stores every inference → memory blowup, computational overload for real-valued domains, worse for dynamic models (correctness/time dependencies of state variables to previous steps); (2) no extension of Reiter's theory to dynamic systems.
- Two response families:
  - Extend GDE: multiple contexts (Guckenbiehl & Schäfer-Richter 1990), time steps in predictions (Dague 1994; Loiez & Taillibert 1997), avoid qualitative-model simulation (Dressler 1996 = state-based diagnosis, Struss 1997) — all qualitative/discrete, not traditional engineering analytical models.
  - Avoid on-line dependency recording → topological methods: graphical models (temporal causal graphs, bond graphs, bipartite graphs, hypergraphs) where equations = edges between variable nodes; conflicts = paths from observed inputs to a discrepant observed output; at least one edge (equation) and its parameters (faults) must be wrong.
- Online-search references: Ca-En (Travé-Massuyès 2006), TRANSCEND (Mosterman & Biswas 1999); offline-search references (Pulido & Alonso-González 2004; Krysander et al. 2008; Armengol et al. 2009; Bregon et al. 2014b) tie directly to Ch 2 structural analysis.

### 6.5 CBD for dynamic systems
- Dynamic diagnosis was central from the DX start: Hamscher & Davis 1984 extended constraint suspension to dynamic models and stressed that state variables must be observable for deterministic results.
- No single formal theory of temporal modeling in AI (vs FDI): Brusoni et al. 1998 categorized the field along three dimensions:
  - temporal phenomena: time-varying contexts, temporal behavior (discrete/continuous state change), time-varying behavior (component modes switch normal↔faulty — intermittent faults or not);
  - ontologies for time: metric/quantitative time, qualitative ordering (Allen 1983 interval algebra), ad-hoc;
  - diagnosis notion: consistency-based (consistent with observations) vs abductive (must explain all observations).
- Chapter's chosen framework (comparable to FDI ODE models): time-varying behavior; continuous state/parameter changes; no intermittent faults; quantitative metric time; consistency-based diagnosis.
- Core modeling issue: representing state variables and influence of previous states; Chantler et al. 1996 discrete-time relation [formula-not-decoded] = differential constraint (vs instantaneous algebraic constraints).
- If dx(t−1)/dt computable ⇒ integrate to get x(t); if states observed ⇒ compute dx/dt and estimate x(t+1) = x(t) + Δt·dx/dt.

#### 6.5.1 Approaches
- Two alternatives to the ATMS problem for dynamics: extend GDE with temporal inferences (Guckenbiehl 1990; Dague 1990; Loiez & Taillibert 1997; Dressler 1996) — persistent drawbacks: (1) pruning dependencies outside a recent temporal window to save memory; (2) revised probabilistic tests for probe-point selection; (3) no direct extension of Reiter's theory to support results logically.
- Struss 1997: split intra-state (same time step) from inter-state (across steps) inferences; state-based diagnosis looks only at intra-state conflicts — qualitative models only.
- Mainstream: topological approaches = couple a simulation/quantitative model with a parallel graphical model for conflicts; online vs offline dependency recording.
- Ca-En (Bousson 1994; Milne & Travé-Massuyès 1997 — TIGER gas-turbine monitor): local model = causal graph (influences as links), global model = quantitative/interval relations checked for residual generation; on residual, check local model consistency; influences on path to inconsistency = conflict.
- TRANSCEND (Mosterman & Biswas 1999; Manders 2000): starts from bond graph (Broenink 1999; effort/flow variables, domain-independent, auto-derivable causal graphs/equations); uses real-valued state-space model + Extended Kalman Filter to track observed variables and generate residuals; residuals + derivatives quantized to qualitative pairs, e.g. {+,0} = above expected and stationary; temporal causal graph propagates qualitative values backward to find inconsistencies → parameters on traversed edges = hypothetical faults; forward traversal generates qualitative signatures per fault, inconsistent ones rejected; survivors identified by numerical optimization.
- CBD with Possible Conflicts (PCs; Pulido et al. 2001; Pulido & Alonso-González 2004; Bregon 2012): offline DX decomposition to find minimal conflicts; PCs implementable via DAE simulation, EKF, Neural Networks, or Dynamic Bayesian Networks [only NN mention in the chapter].
- PC machinery: abstract ODE/DAE model to a hypergraph (Murota 2012): nodes = variables, hyperarcs = relations, e.g. e1: ({ḣT1, qi, q12, qf1}), only qi observed.
- Depth-first exhaustive search from each variable for subsystems with minimal analytical redundancy ⇒ Minimal Evaluable Chain (MEC) ≡ minimal ARR; stop when #equations = #non-observed variables + 1.
- MEC solvability: build directed and-or graph, one edge per causal assignment; differential constraints get 2 assignments (e.g. e121 integrates ḣT3→hT3, e1212 differentiates); a valid global causal assignment = Minimal Evaluable Model (MEM); e.g. MEC {e3,e8,e9,e12} has MEM {e31,e81,e91,e121}.
- All offline, no model evaluated; then each MEC → executable monitor: simulation (Pulido 2001), state observer (EKF, Bregon 2014a), or DBN (Alonso-Gonzalez 2010).
- Equivalence results: PCs ≡ minimal conflicts (Pulido & Alonso-González 2004) ≡ minimal ARRs ≡ MSOs (Armengol 2009; Krysander 2008) — bridges DX and Ch 2 structural analysis. Residual fired ⇒ MEC equations act as the minimal conflict ⇒ standard CBD cycle.

### 6.5.2 PCs for the three-tank system
- Add state/derivative constraints e10-e12 (ḣTj relations) [formula-not-decoded]; observed vars starred: {q*i, q*23, h*T1, h*T3}; unknowns {q12, q30, qf1..qf3, ḣT1..ḣT3, hT2}; hypergraph H3Ts = {V3Ts (13 vars), R3Ts = {e1..e12}} [hyperarc set formula-not-decoded].
- Algorithms of Pulido & Alonso-González (2004) derive MECs m=1..5 (Table 6.1); one causal assignment per constraint e1-e9; integral causality only for e10-e12.
- Table 6.1 as bullets (MECm: RMECm | observed outputs Ym ∪ non-observed Xm ∪ observed inputs Sm):
  - MEC1: {e3,e8,e9,e12} | {h*T3} ∪ {ḣT3,q30,qf3} ∪ {q*23}
  - MEC2: {e2,e4,e6,e7,e11} | {q*23} ∪ {hT2,ḣT2,q12,qf2} ∪ {h*T3,h*T1}
  - MEC3: {e1,e2,e4,e5,e6,e7,e10,e11} | {h*T1} ∪ {ḣT1,q12,hT2,ḣT2,qf1,qf2} ∪ {q*i,q*23}
  - MEC4: {e1,e4,e5,e6,e10} | {} ∪ {hT2,ḣT1,q12,q23,qf1} ∪ {q*i,h*T1,h*T3}
  - MEC5: {e1,e2,e5,e6,e7,e10,e11} | {} ∪ {ḣT1,ḣT2,q12,hT2,qf1,qf2} ∪ {h*T1,q*23,h*T3}
- Result: exactly one MEM each for MEC1-3 → Possible Conflicts PC1,PC2,PC3 estimating {h*T3, q*23, h*T1}; MEC4/5 have no valid global causal assignment → not PCs.
- MEM traversal leaves→root (root = ŷm) defines the executable monitor model; hard to build for complex nonlinear systems; tool DBCwithPCs: https://www.infor.uva.es/~belar/SoftwareCPCs/ [URL as OCR'd [OCR?]].

### 6.6 Conclusion
- Four AI routes (KBS, CBR, ML, model-based); chapter reviewed KBS + model-based.
- KBS: no longer hot research but widely deployed; drawbacks: device dependence, KB maintenance/coherence, multiple & unforeseen faults.
- Model-based: domain-independent, automatic multiple-fault diagnosis with correct-behavior models only; CBD rejects rather than confirms; no-function-in-structure ⇒ model libraries.
- Reiter + GDE gave parsimonious minimal-candidate space from minimal conflicts; dependency recording (esp. with time annotations) spawned online vs offline research; temporal info made it critical.
- De facto dynamic alternatives: Ca-En, TRANSCEND (online/topological), Possible Conflicts (offline compilation); graphical model searched for conflicts; ~25 years of GDE-idea extensions.
- Three persistent AI-vs-FDI differences: AI emphasizes isolation/identification with qualitative/symbolic info (FDI: robust detection + residual analysis); AI works at component level via compositional modeling (FDI: whole system models); CBD forbids exoneration. Hybrid AI+FDI solutions are the future direction.

### 6.7 References (key anchors only)
- Core theory: Reiter 1987 (AITP 32:57-95, theory from first principles); de Kleer & Williams 1987 (AITP 32:97-130, diagnosing multiple faults/GDE); de Kleer 1986a/b/c (ATMS trilogy); Hamscher/Console/de Kleer 1992 (Readings in MBD).
- Temporal diagnosis: Hamscher & Davis 1984; Allen 1983; Brusoni et al. 1998 (AI 102:39-79); Chantler et al. 1996; Struss 1997; Dague 1994/1990; Loiez & Taillibert 1997; Dressler 1996.
- Topological/PC line: Ca-En — Bousson 1994, Milne & Travé-Massuyès 1997 (TIGER), Travé-Massuyès 2006; TRANSCEND — Mosterman & Biswas 1999, Manders 2000, Bregon 2012, Broenink 1999 (bond graphs); PCs — Pulido & Alonso-González 2004, Pulido et al. 2001/2010, Bregon et al. 2014a/b, Krysander 2008, Armengol 2009, Murota 2012; book companion Escobet et al. 2019 (Fault Diagnosis of Dynamic Systems, Springer).
- KBS/classification: Shortliffe 1976 (MYCIN), Buchanan & Shortliffe 1984, Clancey 1985 (AI 27:289-350), Reggia 1983, Peng & Reggia 1990, Stefik 2014, Jackson 1998, Brown 1982 (SOPHIE), Kahn & McDermott 1986 (MUD), Matsatsinis 1997.
- Framing: Balakrishnan & Honavar 1998; Venkatasubramanian 2003; Gertler 1998; Davis 1982; Console 2000; Kolodner 2014; Watson 1998; Mitchell 2006; Witten 2016; Ding 2014 (three-tank case study); SAREF Daniele 2018 / ifcOWL Pauwels & Terkaj (ontologies).

NOTE (source audit): the parent's topic brief (fuzzy-logic diagnosis, static/recurrent NN residual generation, neuro-fuzzy hybrids, decision fusion, benchmark tables with numbers) does NOT match this line range. Ch6 at 4453-5017 is KBS + Reiter/GDE consistency-based diagnosis with full-adder + three-tank worked examples; the only NN mention is one line (PC implementations via NN/DBN, 4871). No fuzzy logic, no decision fusion anywhere in range. Those topics likely live in the data-driven chapter (Ch5) or Vol 2's nonlinear methods. Line 5018+ is book back matter (List of Authors/Index), correctly excluded.

