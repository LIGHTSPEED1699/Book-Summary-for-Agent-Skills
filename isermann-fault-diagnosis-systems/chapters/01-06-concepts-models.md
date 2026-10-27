# Isermann Ch1-6 — Concepts, Reliability/Safety, Fault & Signal Models

**Fault-Diagnosis Systems — Introduction from Fault Detection to Fault Tolerance** (P.M. Frank, R. Isermann et al., Springer 2006; Isermann-authored chapters). Deep rewrite from the full extraction (~/.knowledge/isermann-fault-diagnosis/pi/full_text.txt, 11,106 lines). OCR caveat: display equations often render as formula-not-decoded; formulas marked [reconstructed] are standard forms pinned to the surrounding prose and printed example numbers, [OCR?] marks garbles. Nothing invented.

## Isermann Ch1-3 — Fault-Diagnosis Systems: An Introduction (Springer 2006) — dense study notes

Scope: Ch1 (source lines 521-643), Ch2 (644-995), Ch3 (996-1432). Ch4 starts line 1433.
Source: /home/hongbin/.knowledge/isermann-fault-diagnosis/pi/full_text.txt (pdf_inspector PP-OCR markdown).
Front matter (abbreviations list) ends ~line 470; '## Introduction' at 517.

### Ch 1 — Introduction / Process automation, contents, history (source lines 517-643)

#### Book-wide motivation (Introduction, 517-519)
- Process automation influence growing "since about 1960"; drivers: demand on process performance / product quality, independence from human operators, relief of operators from monotonic tasks, rising wages.
- Automation pushed forward "drastically since around 1975" when relatively cheap, reliable microcomputers became available; paralleled by progress in sensors, actuators, bus-communication systems, human-machine interfaces, plus better theoretical understanding of processes.

#### 1.1 Process automation and process supervision (521-542)
- Hierarchical scheme (Fig. 1.1, two coupled process parts):
  - LOWER level: sequential control, feedforward and feedback control.
  - MEDIUM level: supervision is assigned here.
  - HIGHER levels: more global acting tasks — coordination, optimization, management.
  - Important process info displayed at the operator's console.
- Digital sequence control + digital (continuous) control made great progress; model-based control (state observers, parameter estimation, nonlinear compensation) improved greatly thanks to modern theory of dynamic systems and signals.
- KEY CAUSAL ARGUMENT: "the better the control functions are performed in the lower levels, the more important become the supervision functions, because operators are removed from the process." An acting human operator both controls AND supervises; with improved lower-level control the supervising functions must improve too.
- Integration of control into the process makes process+control autonomous units → mechatronic systems, drive-by-wire aircraft and vehicles. Reliability and safety then depend on correct functioning of ALL process parts, actuators, sensors, control computers. Faults must be "immediately displayed to the operator (pilot, driver) and redundant or reconfigurable components must be activated by a fault-management system for critical processes."
- Cautions/limitations of classical supervision: "automatic supervision in the past was mostly realized by limit checking (or threshold checking)" of important variables (force, speed, pressure, liquid level, temperatures); alarms raised on limit exceedance, operator or protection system acts. "This is in many cases sufficient to prevent larger failures or damages. However, faults are detected rather lately and a detailed fault diagnosis is mostly not possible with this simple method."
- Modern route: systematic use of mathematical process and signal models, identification/estimation methods, methods of computational intelligence.
- Goals of advanced FDD (verbatim list, 535-542):
  - early detection of small faults with abrupt or incipient behavior;
  - diagnosis of faults in actuators, processes, components and sensors; fault detection in closed loops;
  - supervision of processes in transient states;
  - process condition-based maintenance and repair;
  - deep quality control of assembled products in manufacturing;
  - teleservices like remote fault detection and diagnosis;
  - basis for fault management;
  - basis for fault-tolerant and reconfigurable systems.

#### 1.2 Contents — the book's own chapter map (544-614) [best cross-reference source for the whole book]
- Five parts: I Fundamentals / II Fault-detection methods / III Fault-diagnosis methods / IV Fault-tolerant systems / V Application examples. (OCR: "If Fault-diagnosis methods" = Part III.)
- Terminology is NOT unique across technological areas → book gives explicit definitions (Ch 2) for: faults, failures, malfunctions, reliability, availability, safety, dependability, integrity — with reference to international standards.
- Ch 3: reliability/availability/maintainability basics — failure rate, MTTF, maintainability & availability measures, with numerical examples. Ch 4: safety-related systems — event tree analysis, fault tree analysis, FMEA, hazard analysis, risk classification; terms safety, system integrity, dependability.
- Ch 5-6: continuous- and discrete-time models; mathematical modelling of faults — kinds of fault models, time behavior, influence on process models; examples for actuators, processes, sensors. "Static and dynamic process models... additive (offset) and multiplicative (parametric) faults influence the measurable signals"; plus models of periodic and stochastic signals for signal-analysis-based detection.
- Ch 7 (single-signal, absolute values): limit checking — "most frequently used way for fault detection", applied to measurable absolute values and their trends; then change-detection: real-time estimation of mean and variance of observed stochastic variables; hypothesis testing, t-test, run-sum test, F-test, likelihood ratio test; fuzzy thresholds, adaptive thresholds, plausibility checks.
- Ch 8 (single-signal, signal models): periodic signals — Fourier and correlation analysis incl. FFT and spectral estimation; non-stationary periodic signals via short-time Fourier transform and wavelet transform; identification of stochastic signals. Goal: detect changes of signal behavior caused by process faults (Fig. 1.2).
- Ch 9 (process models, identification): adaptation via cross-correlation or parameter estimation; recursive least squares (RLS) and modifications for LTI and time-variant processes, discrete- and continuous-time; advantage = powerful methods for nonlinear processes (most real processes nonlinear), incl. neural networks for static/dynamic systems implemented as look-up tables. "Fault symptoms then reflect as parameters or output signal deviations."
- Ch 10: parity equations — FIXED process models. Ch 11: state observers / state estimation (OCR "Chapter 1]") — residuals from output error + state variables; enhanced residuals via fault-detection filters or bank of observers; Kalman filters for noisy processes; unknown-input / output observers from transformation to new state variables/outputs so unknown inputs have no influence on residuals; parity-equation and observer methods compared (similarities in computational form of residual equations). Residuals designed with transfer functions → output or equation errors called PRIMARY RESIDUALS; state-space models also; enhanced residuals get special structures or directions; strongly isolating vs weakly isolating residuals distinguished.
- Ch 12: fault detection of CONTROL LOOPS — "as detuned controller parameters, actuator or sensor faults and some disturbances have a similar effect on the control performance, it is rather difficult to detect and diagnose faults in closed loop."
- Ch 13: principal component analysis — under linearity assumption, analyzes fluctuations of input/output variables of large-scale processes, reduces number of variables to those uncorrelated while preserving most information; changes of new variables form residuals.
- Ch 14: comparison of model-based fault detection (assumptions + simulations), suitability per fault type, certain combinations proposed.
- Part III: Ch 15 basic problems; Ch 16 diagnosis by classification (classical pattern recognition → geometric classifiers → neural networks); Ch 17 fault trees + inference for approximate reasoning, FORWARD and BACKWARD chaining; hybrid neuro-fuzzy systems identify fault trees with if-then rules. Symptoms may be analytical or heuristic (linguistic terms observed by humans) and numeric.
- Part IV: Ch 18 fault-tolerant design — static and dynamic redundant structures (voters, hot and cold standby); degradation steps with states of FAIL SAFE, FAIL OPERATIONAL, FAIL SILENT; fault-tolerant sensors with hardware or analytical redundancy; fault-tolerant actuators. Ch 19 fault-tolerant components and fault-tolerant control systems.
- Part V examples: Ch 20 DC motor; Ch 21 AC-motor-driven centrifugal pump (OCR "Chapter 2]"); Ch 22 automotive suspension. More applications in separate book ref [1.25].
- Method-inventory figures: Fig. 1.2 signal models, Fig. 1.3 process models, Fig. 1.4 survey on fault-detection methods (left = single-signal, right = model-based), Fig. 1.5 diagnosis problem, Fig. 1.6 survey on fault-diagnosis methods, Fig. 1.7 basic fault-tolerant structures + degradation steps, Fig. 1.8 static vs dynamic redundancy (hot standby), Fig. 1.9 application to actuators/processes/sensors in open or closed loop.

#### 1.3 Historical notes (616-634)
- Limit checking "probably as old as the instrumentation of machines", dating to end of 19th century.
- ~1935: ink and later point-printing recorders standard for plant supervision.
- ~1960: analog controllers with transistor op-amps + hardwired sequential controllers, still limit checking; spectral analysis realizable with analog bandpass filters + oscilloscopes.
- 1960: on-line operating process computers → improved supervision such as trend analysis.
- 1968: first programmable logic controllers replaced hardwired controllers for electromechanical relays → protection systems easier.
- 1971 microcomputer advent; increasing use in decentralized process automation since 1975 → computationally involved software-based supervision/fault-detection algorithms.
- First model-based fault-detection publications: aerospace systems [1.2],[1.27],[1.37],[1.6] and chemical plants [1.15]. Several early concepts = PARITY RELATION approaches checking consistency of instrument readings or mass/material balances; mass-balance residuals used for pipeline leak detection [1.35]; parity relations further studied by [1.14].
- Observer-based FD: Luenberger observers [1.2],[1.27] or Kalman filters [1.28]; analytic redundancy between measurements for sensor fault detection with a bank of observers [1.6]; unknown-input/output observers for not-measurable inputs [1.36],[1.11]; eigenstructure-assignment observers [1.29].
- Parameter-estimation FD: [1.16],[1.1] jet turbines; [1.19],[1.20],[1.21] general processes with circulation pumps and DC motors; [1.8],[1.7] electrical motors.
- Venue history: IFAC SAFEPROCESS symposia Baden-Baden 1991, Helsinki 1994, Hull 1997, Budapest 2000, Washington 2003, Beijing 2006; IFAC Workshop "On-line fault detection and supervision in the chemical process industries" Kyoto 1986, Newark 1992, Newcastle 1995, Folaize 1998, Cheju 2001.
- [OCR?] Line 620 is Fig. 1.9's caption printed upside-down in the scan (reversed text); lines 570/572 are a figure-float sentence split out of order ("...see Figure 1.4 right").

### Ch 2 — Supervision and fault management of processes: tasks and terminology (source lines 636-995)

#### 2.1 Basic tasks of supervision (644-763)
- Open-loop process (Fig. 2.1a): U(t), Y(t) measurable input/output. Faults F(t) from:
  - EXTERNAL causes: environmental influences — humidity, dust, chemicals, electromagnetic radiation, high temperature → e.g. corrosion, pollution.
  - INTERNAL causes: missing lubrication → higher friction/wear, overheating, leaks, shortcuts.
- Causal chain, verbatim structure: F(t) first affects internal process parameters θ by Δθ(t) (changes of resistances, capacitances, stiffness) and/or internal state variables x(t) by Δx(t) (mass flows, currents, temperatures) — "frequently not measurable" — and via the dynamic process transfer behavior reaches the measurable output as ΔY(t).
- Confounds: natural process disturbances and noise N(t), plus changes of manipulated variable U(t), also influence Y(t).
- OPEN vs CLOSED loop asymmetry (Fig. 2.2, KEY CAUTION):
  - Open loop: a remaining fault f(t) generally gives a PERMANENT offset ΔY(t).
  - Closed loop with integral action (e.g. PI controller): output shows only a short, vanishingly small ΔY(t); instead the manipulated variable keeps a permanent offset ΔU(t) for proportionally acting processes.
  - DANGER: "If only the output Y(t) is supervised, the fault may not be detected because of the small and short deviation, furthermore corrupted by noise." A closed loop compensates not only disturbances M(t) but also parameter changes Δθ(t) and state changes Δx(t) with respect to the controlled variable.
  - Only when the fault grows so that U(t) hits a restriction value (SATURATION) can a permanent ΔY arise.
  - RULE: for closed-loop processes U(t) should be monitored as well as Y(t) — "frequently not realized. Mostly only Y(t) and the control deviation e(t) are supervised."
- Limit/threshold checking definition: check whether quantities lie in tolerance zone Y_min < Y(t) < Y_max; alarm on exceedance. Typical variables: pressures, forces, liquid levels, temperatures, speeds, oscillations.
- TASK TAXONOMY (this is the spine of the chapter; Tasks 1-2 = classical, 3-4 = advanced):
  1. MONITORING: measurable variables checked with regard to tolerances, alarms generated for the operator; after an alarm the OPERATOR takes the counteractions.
  2. AUTOMATIC PROTECTION: if a threshold exceedance means a dangerous process state, monitoring automatically initiates the counteraction; process usually commanded to a FAIL-SAFE state, frequently an emergency shut-down (Table 2.1).
  3. SUPERVISION WITH FAULT DIAGNOSIS, subtasks (a)-(e):
     (a) FEATURE GENERATION — special signal processing, state estimation, identification and parameter estimation, or parity relations;
     (b) FAULT DETECTION and generation of symptoms;
     (c) FAULT DIAGNOSIS using analytical and heuristic symptoms and their relations to faults — classification methods or reasoning via fault-symptom trees; goal = determine KIND, SIZE and LOCATION of the fault;
     (d) FAULT EVALUATION — classify faults into different HAZARD CLASSES;
     (e) DECISION ON ACTIONS dependent on hazard class and possible degree of danger, automatically or by operator (Table 2.2).
  4. SUPERVISION ACTIONS AND FAULT MANAGEMENT (per hazard class):
     (a) safe operation, e.g. shut-down if immanent danger for process/environment;
     (b) reliable operation, e.g. hindering further fault expansion by changing operating state — operation with lower load, speed, pressure, temperature;
     (c) reconfiguration — use other sensors, actuators or redundant (standby) components to keep process in operation and under control with a "reconfigured" structure;
     (d) inspection — detailed diagnosis by additional measures;
     (e) maintenance — instantaneous or next possibility, tune process parameters or exchange worn parts;
     (f) repair — instantaneous or at next possibility (overhaul or revision).
  - Fault management may incorporate several intermediate actions for redundant systems in a dangerous state: aircraft, power plants, chemical plants, automatic guided vehicles.
- Table 2.1 automatic protection examples (Process | Fault | Counteraction (safe state) | Protection device):
  - electric cable | short cut | interruption of current | electrical fuse
  - electrical motor | overheating | interruption of current | temperature protector
  - steam turbine | overspeed | fast valve closes | overspeed protector
  - heating boiler | overheating (boiling) | interruption of fuel supply | safety temperature switch
  - aircraft combustion engine | break of flexible linkage | full throttle (max. power) | throttle spring
  - automotive engine | break of flexible linkage | idle gas (min. power) | throttle spring
  [Note the safe state is application-specific opposite directions: aircraft goes to full throttle, automotive to idle.]
- LIMITATIONS of classical monitoring/protection (cautions, verbatim substance):
  - Setting tolerances requires COMPROMISE between detection size for abnormal deviations and unmeasurable/wrong (false) alarms from normal fluctuations.
  - Fixed thresholds work well only if process stays in steady state or the monitored variable does not depend on operating point. Involved when variable changes dynamically with operating point: forces in rolling mills or machine tools; pressures and temperatures in chemical batch processes.
  - Advantage = simplicity and reliability for steady-state situations; but can only react after a relatively LARGE change of a process feature (large sudden fault or long-lasting gradually increasing fault).
  - In-depth fault diagnosis usually NOT possible from threshold violation of one or a few variables.
  - Adding more sensors/cables/transmitters/plugs raises costs AND deteriorates overall reliability, "because the probability of faults increases with more elements". Direct software implementation of operator know-how is hard and "does not lead much further without physically-based process models."
  - LARGE-SCALE PROCESS PROBLEM: after a severe fault several alarms trigger in short time sequence = "ALARM-SHOWER"; operators overloaded both in immediate reaction and in finding causes.
- Requirements for advanced supervision (i)-(iv): (i) early detection of small faults with abrupt or incipient time behavior; (ii) diagnosis of faults in processes/process parts and their manipulating devices (actuators) and measurement equipment (sensors); (iii) detection of faults in closed loops; (iv) supervision of processes in transient states. Goal of early FDD = enough time for counteractions: other operations, reconfiguration, planned maintenance or repair.
- Model-based information gain (Fig. 2.4): use ALL available measurements and relate them via mathematical process models; measuring U(t), accessible state variables x(t), maybe disturbance signals lets changes of static/dynamic behavior serve as information source; changes of ΔY(t) caused by inputs ΔU or measurable disturbances are automatically accounted for → comparison variables become more sensitive to faults; effects of normal disturbances vs faults are automatically separated. (This is analytical redundancy, cf. Ch 1.)
- Table 2.2 hazard classes (class | safety | reliability | action during operation | after operation | example):
  - 1 | high | high | emergency safe (e.g. stop) | fail- repair | bearing without lubrication
  - 2 | medium | medium | other operation state | maintenance | bearing with too low oil pressure
  - 3 | medium | high | reconfiguration | repair | one pump of a duplex pump system overheated
  - 4 | no | high** | transfer to reliable state | repair | unbalanced wheels
  - 5 | no | small | no | maintenance | leaking seals
- Further developments listed: maintenance on request (process condition); tele-diagnosis with modern communication; 100% quality control of products.
- ECONOMICS number: "maintenance costs resemble in most cases a high percentage (e.g. < 20%) of overall operating costs" [OCR? the sign reads "< 20%", probably meant "≈/> 20%" — quote as printed] → advanced supervision/diagnosis can reduce maintenance effort and cost and improve lifetime.
- IMPORTANT SYSTEMIC POINT: the whole chain faults→signals→features→symptoms→decisions→actions is a feedback system = SUPERVISORY LOOP or FAULT MANAGEMENT LOOP. Unlike feedback control, not all signals/states act continuously: signal evaluation, feature generation, symptom generation may run continuously, but fault diagnosis, decision making and actions act as DISCRETE EVENTS on fault appearance → "the supervisory loop is a hybrid continuous and discrete event system."
- Literature map by process type: machines [2.39],[2.10],[2.2],[2.9],[2.21]; electrical motors [2.6],[2.7]; pumps [2.7],[2.25],[2.42],[2.4],[2.11]; steam turbines [2.34]; manufacturing [2.33]; bearings/machinery [2.5],[2.43],[2.40],[2.21]; aircraft [2.27],[2.24],[2.23]; automotive [2.31],[2.20],[2.18]; chemical processes [2.12],[2.32]. Model-based FD books [2.28],[2.29],[2.16],[2.8],[2.3],[2.35],[2.1]; fault-tolerant systems [2.22],[2.37].

#### 2.2 Faults, failures, malfunctions (765-816) — VERBATIM DEFINITIONS
- Terminology is not unique; standardization efforts: the RAM (reliability, availability, maintainability) dictionary [2.26], contributions [2.14], German standards DIN and VDI/VDE-Richtlinien (guidelines), and the IFAC-Technical Committee SAFEPROCESS definitions [2.19] (see also Chapter 23.1; survey of standardization literature in bibliography of Ch 23.1).
- FAULT (verbatim): "A fault is an unpermitted deviation of at least one characteristic property (feature) of the system from the acceptable, usual, standard condition."
  Remarks: a fault is a STATE within the system; the unpermitted deviation = difference between the fault value and the violated threshold of a tolerance zone for its usual value; also "an abnormal condition that may cause a reduction in, or loss of, the capability of a functional unit to perform a required function" [2.13]; many types — design fault, manufacturing fault, assembling fault, normal-operation fault (e.g. wear), wrong-operation fault (e.g. overload), maintenance-fault, hardware-fault, software-fault, operator's fault (some of these are also called ERRORS, especially if directly caused by humans); a fault is independent of whether the system is in operation or not; a fault may NOT affect correct functioning (like a small rent in an axle); a fault MAY initiate a failure or a malfunction; faults are frequently difficult to detect, especially if small or hidden; faults may develop ABRUPTLY (stepwise) or INCIPIENTLY (driftwise).
- FAILURE (verbatim): "A failure is a permanent interruption of a system's ability to perform a required function under specified operating conditions."
  Remarks: failure = "termination of the ability of a functional unit to perform a required function" [2.13]; a failure is an EVENT; a failure results from one or more faults; types of failures:
  - number of failures: single, multiple;
  - predictability: RANDOM failure (unpredictable, e.g. statistically independent from operation time or other failures); DETERMINISTIC failure (predictable for certain conditions); SYSTEMATIC or CAUSAL failure (dependent on known conditions);
  - usually a failure arises after begin of operation or by increasingly stressing the system.
- MALFUNCTION (verbatim): "A malfunction is an intermittent irregularity in the fulfillment of a system's desired function."
  Remarks: a malfunction is a TEMPORARY interruption of a system's function; a malfunction is an EVENT; results from one or more faults; usually arises after begin of operation or by increasingly stressing the system.
- RELATION CHAIN (Fig. 2.5): fault (state) → develops abruptly (step-function) or incipiently (drift-like); the corresponding FEATURE is assumed PROPORTIONAL to the fault development; after exceeding the tolerance of normal values the feature INDICATES A FAULT; dependent on its size, a FAILURE or MALFUNCTION follows at time t_f. So: fault = state, failure = permanent interruption (event), malfunction = intermittent/temporary irregularity (event). Fault precedes; failure/malfunction are consequences.
- Table 2.3 fault→feature→failure/malfunction examples (Process | Fault | Feature | Failure | Malfunction):
  - electrical illumination | switch with corroded contacts | occasionally no electrical conductivity | – | interrupted light
  - electrical illumination | broken wire in cable | no electrical conductivity | no light | –
  - electrical DC motor | worn brushes | armature resistance high | – | occasionally interrupted torque and changing speed
  - electrical DC motor | broken wire in excitation coil | no electrical flux | no torque, no speed | –
  - machine tool belt drive | belt with too low pretension | no continuous torque transfer | – | sluggish dynamics, piecewise motion
  - machine tool belt drive | broken belt threads | no torque transfer | standstill of feed drive | –
  - pneumatic valve | leak in supply air pressure | slow motion, limited position range | – | closed loop does not follow setpoint for some time
  - pneumatic valve | corroded shaft | mechanical friction too high | deviation, no motion, permanent control deviation | –
  Pattern: gradual/partial faults (corrosion, wear, low pretension, leak) → MALFUNCTION; complete faults (broken wire, broken threads) → FAILURE.

#### 2.3 Reliability, availability, safety, dependability, integrity (818-904)
- RELIABILITY (verbatim): "Ability of a system to perform a required function under stated conditions, within a given scope, during a given period of time." Short version: ability to perform a required function for a certain period of time. "Reliability is quality for some time." Reliability can be affected by malfunctions and failures.
  - MEASURE: Mean Time To Failure MTTF = 1/λ, where λ = rate of failures per time unit [text says "see Chapter 5" — Ch 3 in this book's numbering has the reliability math; treat as forward reference; cross-check Ch 3].
- SAFETY (verbatim): "Ability of a system not to cause danger to persons or equipment or the environment." Short version: ability not to cause danger. Safety is concerned with the DANGEROUS EFFECTS of faults, failures, malfunctions. "The safety can usually be seen as a status, where the risk is not larger than a specified risk limit (risk threshold)."
  - CAUTION / KEY TENSION: measures for reliability aim at AVOIDING faults/failures/malfunctions; measures for safety aim at avoiding their DANGEROUS EFFECT. Improving reliability generally improves safety. BUT "an improvement of safety can result in a deterioration of the reliability if, e.g. the number of components increase" (more safety hardware = more failure sources; echoes the sensor-count argument in 2.1).
  - SAFETY vs SECURITY: similar meanings; SAFETY deals with life, equipment, environment; SECURITY deals with privacy, property, community, state.
- AVAILABILITY (verbatim): "Probability that a system or equipment will operate satisfactorily and effectively at any period of time." Of major importance for the USER; takes into account that failures/malfunctions happen and need repair time.
  - MEASURE (OCR garbled, best faithful reading of the standard formula): A = MTTF / (MTTF + MTTR), where MTTR = Mean Time To Repair (printed "A = TT FGuT TR"; see Ch 3 for the worked numbers).
  - To reach high availability, MTTF must be LARGE vs MTTR:
    - large MTTF → PERFECTION: highly reliable components; → TOLERANCE: tolerable faults through redundant structure;
    - small MTTR → fast and reliable FAULT DIAGNOSIS; fast and reliable removal of faults (maintenance/repair).
  - THE BOOK'S OWN VALUE PROPOSITION: "fault detection and fault diagnosis can improve the availability by early fault detection in combination with maintenance on demand (larger MTTF) and by fast and reliable diagnosis (smaller MTTR)."
- DEPENDABILITY — explicitly "seems not to be clearly defined", two cited meanings:
  (i) "A form of availability that has the property of always being available when required (and not at any time). It is the degree to which a system is operable and capable of performing its required function at any randomly chosen time during its specific operating time, provided that the system is available at the start of the period" — this definition excludes non-operation-related influences [2.26];
  (ii) "Dependability is a property of a system that justifies placing one's reliance on it. It covers reliability, availability, safety, maintainability and other issues of importance in critical systems" [2.37].
  - Standard [2.13] on safety-related systems does NOT define dependability, only safety integrity.
- INTEGRITY: earlier definition [2.37]: "The integrity of a system is the ability to detect faults in its own operation and to inform a human operator." Meaning broadened over years, associated with critical systems; frequently used as synonym for dependability. Per [2.13]: "Safety integrity is the probability of a safety-related system satisfactorily performing the required safety functions under all the stated conditions within a period of time."
- accident, hazard, risk are defined in Ch 4.

#### 2.4 Fault tolerance and redundancy (906-918)
- Even after reliability/safety analysis for design improvement + testing + quality control during manufacturing, "the appearance of certain faults and failures cannot be avoided totally" → unavoidable faults must be TOLERATED by additional design effort. Hence high-integrity systems must have the ability of fault tolerance: "faults are compensated in such a way that they do not lead to system failures."
- After improving PERFECTION of components, the remaining obvious way = REDUNDANCY: one or more back-up modules in addition to the considered module, usually in a PARALLEL configuration (Fig. 2.6).
- Function modules can be HARDWARE components or SOFTWARE parts, either IDENTICAL or DIVERSE. Arrangements: static or dynamic redundancy, cold or hot standby. Modules e.g. actuators, sensors, computers, motors, pumps.
- General scheme: function modules supervised with fault-detection capability, followed by a RECONFIGURATION MECHANISM to switch off failed modules and switch on spare modules (dynamic redundancy). For electronic hardware, simpler schemes with n > 3 modules and MAJORITY VOTERS, e.g. 2-out-of-3 systems (static redundancy). Details in Part IV (Ch 18-19).

#### 2.5 Knowledge-based fault detection and diagnosis (920-944+)
- FDD rests on measured variables (instrumental) + observed variables/states (human operators). Automatic processing of measured variables requires ANALYTICAL process knowledge; evaluation of observed variables requires human expert knowledge = HEURISTIC knowledge → knowledge-based approach [2.30],[2.38]; overall scheme Fig. 2.7 [2.15],[2.17].
- 2.5.1 ANALYTIC symptom generation — three routes to characteristic values:
  1. LIMIT VALUE CHECKING of direct measurable signals → characteristic values are the VIOLATED SIGNAL TOLERANCES;
  2. SIGNAL ANALYSIS of directly measurable signals using SIGNAL MODELS: correlation functions, frequency spectra, autoregressive moving average (ARMA) → characteristic values = variances, amplitudes, frequencies, model parameters;
  3. PROCESS ANALYSIS using mathematical PROCESS MODELS with parameter estimation, state estimation, parity equation methods → characteristic values = PARAMETERS, STATE VARIABLES, RESIDUALS.
  - Then special FEATURES may be extracted: physically defined process coefficients, or special filtered/transformed residuals; compared with normal features of the non-faulty process using change-detection and classification methods. Resulting changes (discrepancies) in measured signals, signal models, or process models = ANALYTIC SYMPTOMS.
- 2.5.2 HEURISTIC symptom generation — qualitative info from human operators: observation/inspection gives heuristic characteristic values = special noises, colors, smells, vibration, wear and tear. Further source: PROCESS HISTORY (maintenance performed, repairs, former faults, life-time and load measures). Plus statistical data from experience with same/similar processes (e.g. MTBF, fault probabilities). Heuristic symptoms represented as LINGUISTIC VARIABLES (small, medium, large) or VAGUE NUMBERS (e.g. around a certain value).

#### 2.5.3 Fault diagnosis (944-952)
- TASK DEFINITION (verbatim): "The task of fault diagnosis consists in determining the type, size and location of the most possible fault, as well as its time of detection."
- Diagnosis procedures use analytic AND heuristic symptoms, so symptoms should be presented in a UNIFIED form: confidence numbers, membership functions of fuzzy sets, or probability density functions after statistical evaluation over some time.
- Two method families: CLASSIFICATION methods if a learned pattern-based procedure is preferred (faults from symptom patterns or clusters); REASONING methods with FORWARD and BACKWARD CHAINING if more information on fault-symptom relations is known (logic fault-symptom trees, if-then rules).
- Terminology per [2.19] (IFAC TC SAFEPROCESS), see Ch 23.1. Methods detailed in Parts II and III.

#### 2.6 Implementation issues (954-977) — the "V"-model for FDD systems
- Development of FDD-systems and fault-tolerant systems represented as a "V"-diagram, probably originating from [2.36], especially used for mechatronic design [2.41] (Fig. 2.8, caption printed upside-down at line 960). Steps are in logical order but some run in parallel/iteratively. Each phase has an outcome called a "DELIVERABLE".
- Sequence of phases:
  1. REQUIREMENTS: summarize expected functions — the FAULTS TO BE DETECTED AND DIAGNOSED (a FAULT LIST), the SMALLEST REPLACEABLE UNITS replaceable when they contain a fault, the allowable cost for development and final product. A reliability and safety analysis AT THIS STAGE is useful to find weak points and risks. Requirements are the basis of top-level design → great care, continuously UPDATED during design if basic changes happen.
  2. SPECIFICATIONS: how requirements are fulfilled — partitioning of functions/parts, available sensors and actuators, available computing power, use of further knowledge, definition of MILESTONES.
  3. MODELLING: mathematical modelling of the process, its signals and EXPECTED FAULTS, incl. SIMULATION of behavior without and with faults.
  4. METHOD DESIGN: design of FDD methods and, if required, of fault tolerance.
  5. SOFTWARE-IN-THE-LOOP (SiL) simulations: common software systems simulate process, faults, and FDD functions.
  6. PROTOTYPING: powerful real-time prototype computer + real process. Then FDD-system is mature for final software on the series-product microcomputer.
  7. TESTING/TUNING of FDD microcomputer hardware+software. First tests by HARDWARE-IN-THE-LOOP (HiL): microcomputer with other real parts (actuators) + real-time process simulation on another powerful computer; requires a special SENSOR-SIMULATION-INTERFACE. HiL is used when expensive real-system tests can be saved OR when fault experiments are made that are NOT ALLOWED on the real process; otherwise test on the real process directly.
  8. SYSTEM INTEGRATION (when FDD is implemented together with other functions, e.g. automatic control): consider functional dependencies of ALL control levels, from lower-level control to top-level process management, incl. documentation of FDD results.
  9. SYSTEM TESTS incl. VERIFICATION and VALIDATION:
     - VERIFICATION = does the system meet its SPECIFICATIONS (fulfills specified functions correctly)?
     - VALIDATION = does the system as a whole satisfy the REQUIREMENTS, i.e. is it appropriate for its intended purpose? → includes checking the CORRECTNESS OF THE SPECIFICATION itself.
     - For CRITICAL SYSTEMS: external regulating authorities must be convinced to achieve CERTIFICATION; stated standards/guidelines checked; tests must show e.g. the FAULT COVERAGE for given operating conditions.
  10. FIELD TESTS: under many different operating conditions, production tolerances, hard environmental conditions, before series production.

#### 2.7 Problems (978-990) — study questions worth self-testing
- basic supervision tasks; supervision vs monitoring difference; more automatic-protection examples; advanced vs classical supervision tasks; the following-up task chain; fault vs failure vs malfunction with one example each; tabulate reliability/safety/availability definitions; example of a fault-tolerant system; analytic vs heuristic symptoms with examples; describe/differentiate fault detection vs fault diagnosis tasks.

### Ch 3 — Reliability, availability and maintainability (source lines 993-1432)
Chapter intro (994): reliability/availability/maintainability are very important properties of modern products; described via CHARACTERISTIC QUANTITIES. History: reliability studies first applied to electrical/electronic components and quality control in manufacturing around the 1940s, then extended to military equipment, aerospace vehicles, nuclear power systems, automobiles [3.4],[3.22]. Standards used: [3.10], [3.6].
IMPORTANT OCR CAVEAT for this chapter: nearly all display equations came through as `<!-- formula-not-decoded -->`. Where a formula is missing, only its NAME or its verbal description (or numbers from the printed tables) are recoverable — noted below. Do not treat reconstructed forms as verbatim.

#### 3.1 Reliability — Definition (996-1002)
- VERBATIM (repeated, slightly fuller than Ch 2): "Reliability is the ability of a component, process or a system to perform a required function correctly under stated condition within a given scope, during a given period of time."
- "The reliability is affected by faults and failures. Therefore the reliability analysis depends on the kind of faults and failures."

#### 3.1.1 Type of faults (1004-1024)
- Faults are distinguished by three axes (Table 3.1): FORM = systematic or random; TIME BEHAVIOR = permanent, transient, intermittent, noise or drift (cf. Figure 5.3 — forward ref to Ch 5); EXTENT = local or global, incl. size.
- Table 3.1 "Main characteristics (/) of primary faults for different components" — columns: mechanical components | electrical components | electronic hardware | software. Checks are OCR-destroyed; faithful reading of the stated prose:
  - Electronic HARDWARE shows SYSTEMATIC faults if they originate in specification or design mistakes; once in operation, hardware-component faults are mostly RANDOM with all kinds of time behavior.
  - SOFTWARE faults (bugs) are usually SYSTEMATIC: wrong specification, coding, logics, calculation overflows etc.; "in general not random like faults in hardware."
- MECHANICAL failure MECHANISMS classification (verbatim list): DISTORTION (buckling, deformation); FATIGUE and FRACTURE (cycle fatigue, thermal fatigue); WEAR (abrasive, adhesive, cavitation); CORROSION (galvanic, chemical, biological) [3.19]. They appear as drift-like changes (wear, corrosion) or abruptly (distortion, fracture) at any time or after stress.
- ELECTRICAL systems: large number of components with various failure modes — short cuts, loose or broken connection, parameter changes, contact problems, contamination, EMC problems. "Generally, electrical faults appear more randomly than mechanical faults."
- Extent depends on importance of components; can be global in all cases even if faults appear primarily locally.
- KEY MODELLING ASSUMPTION: "Reliability analysis is usually based on the assumption of RANDOM faults." Holds especially for electronic/electrical components and for large systems with many components and systematic faults that SEEM random because of their large number (large mechanical systems, software systems) [3.22].

#### 3.1.2 Reliability estimation (1026-1162)
- RELIABILITY FUNCTION R(t): for a large number N of identical elements at begin of operation — defined as the ratio of the number n(t) of correctly functioning elements to N; "describes the probability that the elements function correctly until time t." [formula not decoded; R(t) = n(t)/N is the stated relation]
- UNRELIABILITY FUNCTION Q(t) = 1 - R(t) [formula not decoded; relation given by text "with number of failed elements n_f"].
- FAILURE RATE λ(t): "the instantaneous rate of failing elements dn/dt related to still functioning elements n(t)" [formula not decoded: λ(t) = -(dn/dt)/n(t), equivalently λ = -dR/dt / R].
- BATHTUB CURVE (Fig. 3.1): electronic components and electro-mechanical systems show (1) a large DECREASING failure rate after commissioning = INFANT MORTALITY, (2) a CONSTANT value in normal operation life = USEFUL LIFE, (3) an INCREASING value in the ageing period = WEAR OUT.
- During normal operation-life a constant λ is assumed → EXPONENTIAL FAILURE LAW, R(t) = e^(-λt) (form given in Fig. 3.2 caption, OCR'd "R(t) = e*!").
- EXAMPLE 3.1 Reliability function (verbatim numbers, 1062-1064): N = 1000 units, λ = 4·10⁻⁵ [1/h] (printed "4- 107°", OCR-ambiguous), operating time t = 20000 h → R = 0.449, Q = 0.551 → n = 1000·0.449 = 449 units still functioning (survived), n_f = 1000·0.551 = 551 units failed. "The reliability function can also be called SURVIVAL PROBABILITY." (Consistency check by me, not in text: R = 0.449 at t = 20000 h requires λt = 0.8, i.e. λ = 4·10⁻⁵ /h; the λ exponent in the OCR is unreliable.)
- Initial tangent of R(t) cuts the time axis at t = 1/λ (stated explicitly, 1072).
- Remarks: (a) R(t) gives the number of survived elements n relative to initial N, a function of time; (b) λ relates failures per time interval to the number of SURVIVED elements — so for constant λ the failures per interval DECREASE with time, hence R(t) decays.
- MTTF (OCR "MTTE"): average failure-free (correct) operation time t_f until a failure; can also be calculated by dividing the number of functioning elements n(t) by the number of failures per time interval. Comparison with the exponential law shows MTTF is the RECIPROCAL of the failure rate: MTTF = 1/λ (verbal statement).
- MTTF = average operating time of a large number of NON-REPAIRABLE elements before failure, for constant λ. Probability of functioning at t = MTTF = 1/λ is e⁻¹: "after an operating time of MTTF only 37% probability of correct operation results" → MTTF is an AVERAGE life time of many components, not a guarantee for one.
- MTBF (Mean Time Between Failure): similar to MTTF, defined per [3.19],[3.17] for REPAIRABLE systems where all failed units are repaired periodically → Section 3.3.
- FAILURE DENSITY (measure for unreliability): d(t) = -dR/dt [formula not decoded]; for λ = const. it has the same time history as R(t) — large for small t, small for large t. "The probability of failed units during time period Δt becomes" [formula not decoded — the density-times-Δt relation].
- EXAMPLE 3.2 Failed units (1132-1140): λ = 10⁻⁵ [1/h] (OCR "107°"), N = 10⁶ units; initial probability of failed units in the FIRST YEAR = [formula not decoded, numeric result lost]; in the FIFTH YEAR (after t = 35040 h) the failed units = [formula not decoded]. t = 35040 h = 4·8760 h, i.e. the elapsed time at the start of year 5.
- WEIBULL DISTRIBUTION (1144-1150) — three parameters, verbatim: t₀ = failure-free period (LOCATION parameter); t_T = characteristic life time (63% of distribution, SCALE parameter); B = SHAPE parameter. Can be adjusted to a wide variety of distributions [3.19]. B = 1 and t₀ = 0 → reduces to EXPONENTIAL distribution; B ≈ 3.55 → approximates the NORMAL distribution.
- STRESS DEPENDENCE: failure rate depends on external and internal temperature, voltage, current, power, vibration, dust, humidity. Per [3.27]: MTTF of ICs is INVERSE PROPORTIONAL TO THE SQUARE OF CURRENT DENSITY and depends EXPONENTIALLY on temperature.
- Per [3.14] influences enter as multiplicative FACTORS for quality, learning, temperature, power, environment → "the failure rate may vary by 2...3 DECADES". For STANDSTILL, 10% of λ₀ (basic λ) is taken. Temperature increase from 40 °C to 70 °C enlarges failure rates by FACTORS 2 to 15.
- Mechanical element reliability influenced much by distortion, fatigue, fracture, wear, corrosion [3.4],[3.14],[3.21],[3.20],[3.13].
- AUTOMOTIVE DESIGN BASIS [3.9] (numbers to remember): time in service 10 years; operation time 3000 h; average speed 50 km/h; drive distance 150000 km; number of rides 50000. Required component life time = [number of rides in 10 years × demands per ride]: airbag 50 h; ABS 5·10⁵ h; window heating 10⁴ h; door locking 5·10⁴ h; wipers, lighting 2.5·10⁵ h. [OCR? exponents/units garbled — magnitudes should be re-checked against the printed page; the ABS/door-locking numbers cannot both be "hours" in the usual sense]
- Table 3.2 typical failure rates of MECHANICAL / ELECTROMECANICAL elements [3.19] (λ [1/h]; label column OCR-merged into one string "ball bearing sleeve bearing belt coupling gear pump seal valve, hydraulic", so pairing is uncertain):
  - mechanical λ values as printed: 1.64·10⁻⁷, 2.38·10⁻⁸, 19.72·10⁻⁶, 5.54·10⁻⁶, 4.69·10⁻⁶, 43.65·10⁻⁶, 5.47·10⁻⁶, 8.83·10⁻⁶ [OCR? 8 values vs 7 labels]
  - electromechanical: actuator, general 26·10⁻⁶; brush, general 9·10⁻⁶; cable, general 1·10⁻⁶; electric motor, general 9·10⁻⁶; generator, general 7.3·10⁻⁶; regulator, general 1.3·10⁻⁶.
- Table 3.3 failure rates of ELECTRONIC/ELECTRICAL elements [3.14], conditions stated in caption: STATIONARY, 40 °C, 60% POWER; plus column "mobile application m_E" = multiplication factor for mobile application. Mobile factors visible: 18 (discrete elements group), 4.2 (passives/analog IC group), 4.2 (digital IC group); flight computer (80286) ref [3.18]. Row values are heavily OCR-mangled (ranges such as 36-360·10⁻⁶ for thyristors and 0.05-0.2·10⁻⁶ / 2-5·10⁻⁶ for digital IC/logic elements are the least-bad reading) [OCR?] — treat the λ magnitudes in this table as unreliable, the CONDITIONS and the mobile multipliers as reliable.
- Figure 3.2: (a) exponential reliability function R(t)=e^(-λt) for constant λ (caption value λ = 4·10⁻⁷ [1/h], OCR'd "4-107" — different from Example 3.1's λ, and exponent unreliable [OCR?]); (b) time history of an element that functions correctly (f = 1) for t < t_f and fails at t = t_f (f = 0).

#### 3.1.3 Connected elements (1164-1222) — series/parallel reliability networks
- Reliability analysis generally requires evaluating CONNECTED ELEMENTS via RELIABILITY NETWORKS representing the kind of connection = COMBINATIONAL MODELLING.
- SERIES connection (Fig. 3.3a), elements failing statistically independently, constant failure rates λᵢ: overall reliability requires ALL elements to operate correctly → PRODUCT LAW OF RELIABILITY [formula not decoded: R_tot = ΠRᵢ; for exponential R_tot = exp(-Σλᵢ·t)].
- Total failure rate and total MTTF for series [formulas not decoded]: λ_tot = Σλᵢ and MTTF_tot = 1/λ_tot. CONFIRMED by Table 3.4 numbers (m identical λ=10⁻⁵ elements in series: λ_tot = 1,2,3,4,…,10 ×10⁻⁵ and MTTF_tot = 10⁵, 0.5·10⁵, 0.33·10⁵, 0.25·10⁵, 0.2·10⁵ → 1/(mλ)).
- CAUTION (design rule, verbatim): "In order to reach a small overall failure rate, all elements should be of similar small failure rate λᵢ. Otherwise the largest λᵢ will dominate and determine λ_tot."
- PARALLEL connection (Fig. 3.3b) = REDUNDANT; unreliability Qᵢ(t) = 1 - Rᵢ(t) is the probability that one element fails; ALL m parallel elements have failed with probability Q_tot = ΠQᵢ → PRODUCT LAW OF UNRELIABILITY. Reliability of the parallel connection: R_tot = 1 - Π(1 - Rᵢ) [formulas not decoded, but the caption of Fig. 3.3 states the function fᵢ is either correct (1) or fail (0); Table 3.4 numbers confirm identical-λ form R_tot = 1 - (1 - e^(-λt))^m].
- Parallel λ and MTTF for EQUAL λ (assumed λᵢ = λ, using the exponential law) [formulas not decoded; the printed numeric sequence confirms the harmonic-sum form MTTF_par = (1/λ)(1 + 1/2 + ... + 1/m)]:
  - "For m = 3 it holds" … "Generalizing leads to" … "and therefore with (3.20)" … (all formula placeholders lost).
  - EXPLICIT PRINTED RESULT (verbatim, 1218): "MTTF increases for two parallel elements by factor 1.5, for three by 1.833, for 4 by 2.083."
- Table 3.4 (identical connected elements, λᵢ = 10⁻⁵ [h⁻¹], operating time t = 10⁴ [h]) — m = 1, 2, 3, 4, 5, 10:
  - SERIES: R_tot = 0.905, 0.818, 0.741, 0.670, 0.606, 0.368 (= e^(-m·0.1)); λ_tot = 10⁻⁵, 2·10⁻⁵, 3·10⁻⁵, 4·10⁻⁵, 5·10⁻⁵, 10·10⁻⁵; MTTF_tot = 10⁵, 0.5·10⁵, 0.33·10⁵, 0.25·10⁵, 0.2·10⁵, 0.1·10⁵ h [last values partly OCR-mangled].
  - PARALLEL: R_tot = 0.905, 0.9910, 0.99914, 0.99992, 0.99999, 0.99999; λ_tot = 10⁻⁵, 0.667·10⁻⁵, 0.545·10⁻⁵, 0.480·10⁻⁵, 0.438·10⁻⁵, 0.341·10⁻⁵; MTTF_tot = 10⁵, 1.5·10⁵, 1.83·10⁵, 2.08·10⁵, ~2.26·10⁵, 2.929·10⁵ h.
- INTERPRETATION (verbatim substance): overall reliability decreases CONSIDERABLY with increasing number of elements; MTTF is only HALF for two serially connected elements, ONE THIRD for three, etc. Redundancy by parallel elements improves MTTF by 50% for two, 83% for three, etc. — "the improvement is initially considerable, but the INCREMENTAL ADVANTAGE BECOMES SMALLER with each parallel component" (diminishing returns of redundancy; harmonic series growth 1.5 / 1.833 / 2.083).
- SERIES-PARALLEL connections: divide the system into series and parallel arrangements so the product laws of reliability and unreliability can be applied CONSECTIVELY [3.22],[3.2].
- Figure 3.4: MTTF for m connected elements with equal failure rate λ = 10⁻⁵ [h⁻¹]: (a) series; (b) parallel.

#### 3.2 Maintainability (1224-1262)
- MAINTENANCE (verbatim definition): "Maintenance is understood as an action taken to retain a system in, or return a system to its designed operating condition. It extends the useful life of systems, ensures the optimum availability of installed equipments or equipment for emergency use."
- "Maintenance is quite often very expensive and may extend the investment cost with time."
- Maintenance may be performed WHILE IN OPERATION (e.g. ship engines, electric transmission lines) or by temporary shut-down; usually the system must be taken OUT of service → DOWN TIMES.
- MAINTAINABILITY = quality of several features enabling maintenance: proper design, required tools, standardized components, group subsystems (MODULARITY), aids for trouble-shooting, spare parts and logistics.
- DOWN TIME = interval where the system is not in acceptable operation; decomposed into: DIAGNOSTIC TIME, ACTIVE REPAIR TIME, LOGISTIC TIME, ADMINISTRATIVE TIME. (Diagnostic time being first is why fast FDD pays.)
- MEASURE: probability that a failed system is repaired within time period T_r; expected repair time = MTTR (Mean Time To Repair) [formula not decoded; cf. Fig. 3.6 time history of f(t) for repairable elements: t_pi time to failure, t_rei repair time].
- Kinds of maintenance (Fig. 3.5 [3.2]): usually PLANNED. PREVENTIVE or SCHEDULED maintenance begins with INSPECTION and includes e.g. cleaning, adjustment, lubrication at PREDETERMINED INTERVALS; also replacement of minor components subject to wear BEFORE they fail, depending on inspection. CORRECTIVE maintenance includes minor repairs and planned regular OVERHAULS, i.e. complete replacement of wearing components. UNPLANNED maintenance is performed in an EMERGENCY situation to avoid immediately drastic failures, shut-downs or losses, or for safety reasons.

#### 3.3 Availability (1264-1276)
- VERBATIM: "The availability is the probability that a considered system will be functioning correctly at any give[n] time t. It is a time dependent function like reliability, however, for systems which are repairable."
- DISTINCTION: reliability = probability operation is failure-free UP TO time t; availability = probability of failure-free operation AT time t, INCLUDING possible down times for repair.
- Measure A [formula not decoded; standard form A = MTTF/(MTTF+MTTR) — same statement given verbally in Ch 2 §2.3 and here: "A large availability is obtained by large MTTF and small MTTR"].
- For a REPAIRABLE system, MTBF [formula not decoded; standard form MTBF = MTTF + MTTR].

#### 3.4 Fault management for total life cycles (1278-1282)
- Reliability/availability/maintainability must be seen in the context of the OVERALL LIFE CYCLE (Fig. 3.7): planning and design → realization/manufacturing → installation/commissioning → operation → decommissioning → waste treatment. If recycling, reconditioning and reuse are possible, a LOOP FLOW for some parts arises.
- The ACTIVE/FUNCTIONAL phases (realization, installation, especially operation) are supported by maintenance, repair or FAULT MANAGEMENT → increases quality, performance and life time. Supervision, fault detection and diagnosis help especially these functional product phases.
- FAULT MANAGEMENT (verbatim): "describes the actions after the (sudden) appearance of faults to maintain the operations. It includes, for example, emergency maintenance or repair, use of spare parts, or reconfiguration in the case of static or dynamic redundancy, see Chapter 19." [cross-ref Ch 18-19]

#### 3.5 Some failure statistics (1284-1286) — CAUTION on data quality
- Purpose: quantitative info on reliability and understanding of appearance/kind of faults. "The basis of the statistical numbers given is, of course, RATHER DIFFERENT." Numbers from technical organizations, service associations, insurances etc. Divided into COMPONENTS (3.5.1) and SYSTEMS (3.5.2).

#### 3.5.1 Statistics of components (1292-1341)
- Table 3.5 AC motors (11...50 kW ... 1 MW) [3.24], percentage of all failures: bearings 51.1 | stator 15.8 | (stator windings/external equipment) 15.6 | (squirrel) cage 4.7 | (axle/clutch) 2.4 | not defined 10.4. [column labels OCR-merged]
- AC-motor FAILURE RATES (printed p.a. percentages let the exponents be pinned down): low power (< 100 kW): 5% p.a. → λ = 5.8·10⁻⁶ [h⁻¹]; high power (> 100 kW): 10% p.a. → λ = 1.16·10⁻⁵ [h⁻¹]. (0.05/8760 = 5.7·10⁻⁶ and 0.10/8760 = 1.14·10⁻⁵ confirm the printed "5.8-10⁻⁶ / 1.16-10⁻⁵"; the OCR exponent glyphs are unreliable.) Refs [3.24],[3.8],[3.15].
- Physical causes named: BEARINGS = material fatigue with rent generation and pitting, wear, corrosion, plastic deformation, faults during assembling, lack of cooling. STATOR WINDINGS = overheating, loss of isolation, loose iron plates. SQUIRREL-CAGE ROTOR = broken rotor bars, unsymmetries, excentricities, resonance frequencies, vibrations. EXTERNAL EQUIPMENT = e.g. power electronics with frequency converters [3.26].
- Table 3.6 circular pumps [3.25], % of all failures: sliding ring seal 31 | ball bearings 22 | leakage 10 | motor 10 | drive 9 | oil bearings 8 | clutches 4 | split tubes 3 | casing 3.
  - Basis: inquiry among chemical industry, water and wastewater treatment companies. Operation kinds: PERMANENT 59%, DAILY 19%, SHORT 22%. Inspection happens ALL THREE MONTHS; unplanned defects with repair ALL NINE MONTHS.
  - Causes of operational MALFUNCTIONS: cavitation, gases in liquids, blockage through closed valves, dry operation through missing fluid, wear through erosion (particles), corrosion, ball bearings, split flow, deposits and oscillations [3.26].
  - CUSTOMER PRIORITIES (ordered): 1 reliability, 2 energy consumption, 3 no leakages, 4 price, 5 noise, 6 control range. Refs [3.25],[3.16],[3.11].
- Table 3.7 hydraulic actuators (aircraft components): spool valve | cylinder | mechanics | power components (pumps) | others ≈ 32 | 19 | 16 | 16/3 | 14 [OCR; the prose below says the largest share is 51% in the spool valve, so the table's 32 and the prose's 51 disagree — flag [OCR?]]. The spool valve manipulates the oil flow to the cylinder.
  - SPOOL VALVE failures: erosion at the edges 65%, dirt 20%, external leakage 10%.
  - VALVE failures: internal leakage 10%, insufficient function 35%, external leakage 15%.
  - CYLINDER failures: external leakage at the rod seals 58%, internal leakage 14%, broken or cracked rod.
- Table 3.8 LIFETIME COSTS of sensors and actuators, 15 years of operation, 388 plants, 41 EUR/h labor cost [3.7] — the single most important economic argument in Ch 3. Reconstructed (leading "1" digits in the OCR are table-border artifacts; every figure verified against the printed % of total):
  - IT PRESSURE SENSOR: acquisition 816 (31.5%) | planning, assembling 490 (18.9%) | maintenance 460 (17.7%) | repair 745 (28.7%) | others 82 (3.2%) | TOTAL 2593 EUR. (816+490+460+745+82 = 2593 ✓)
  - TEMPERATURE SENSOR: acquisition 230 (27.1%) | planning/assembling 388 (45.8%) | maintenance 153 (18.1%) | repair 0 | others 77 (9.0%) | TOTAL 848 EUR ✓
  - FLOW SENSOR: acquisition 1990 (28.7%) | planning/assembling 1173 (16.9%) | maintenance 918 (13.2%) | repair 2704 (39.0%) | others 153 (2.2%) | TOTAL 6938 EUR ✓
  - VALVE: acquisition 832 | planning/assembling 735 | maintenance 153 | repair 534 | others 82 | TOTAL 2336 EUR ✓ (the printed % column for the valve does not reconcile: [OCR?])
  - Ratios printed: maintenance+repair ÷ acquisition ≈ 1.5 (pressure), 0.7 (temperature), 1.8 (flow), 1.3 (valve [OCR? 0.8 from the EUR numbers]); overall cost ÷ acquisition = 3.5 (flow), 3.3 (valve; from EUR ratio 2.81, [OCR?]).
- FINDINGS from Table 3.8 (verbatim substance): total costs of FLOW sensors highest, then PRESSURE sensors and VALVES; TEMPERATURE sensors cheapest. Maintenance+repair costs over 15 years especially high for flow and pressure sensors and valves. "The overall costs are about 3.5 [times] larger than the acquisition costs." → "these numbers underline the great significance of EARLY FAULT DETECTION to reduce at least part of costs for maintenance and repair." NOTE the planning+assembling share (45.8% for temperature sensors) exceeds maintenance — installation dominates for cheap devices.

#### 3.5.2 Statistics of systems (1343-1390)
- ADAC (German automobile club) statistics, Table 3.9 Pannenstatistik 1999 [3.1]: basis ≈ 20000-100000 breakdowns and service helps per year. Most frequent (and INCREASING within the last 5 years) are failures of the ELECTRICS: battery, generator, V-belt, starter, blockage, loosened cables, burned fuses. Ignition-system defects caused by the IMMOBILIZER (theft protection), ECU's, sparks, or MARTEN BITES. Engine problems: broken toothed belts or chains of the camshaft, oil pump defects, too little oil, overheating.
- Table 3.9 percentages (with prior-year value in parentheses): general electr. 31.3 (35.1) | ignition 14.1 (14.1) | motor 12.2 (10.5) | cooling system 8.4 (7.2) | fuel system 6.6 (6.0) | (fuel) injection 6.2 (5.7) | tires 6.8 (6.9) | clutch 5.8 (5.0) | chassis 4.2 (4.8) | exhaust system 2.2 | brake system 1.4 | suspension 0.6 | steering system 0.3. [column labels merged by OCR]
- BRAKE SAFETY NUMBERS: hydraulic brakes of passenger cars in Germany (1999) responsible for about 900 accidents with injuries out of about 36000 → 2.5% of all accidents and 18% of all accidents due to TECHNICAL faults (accidents during rain, snow and ice are about 48.5%) [3.23],[3.5]. Reasons for brake failure: LEAKAGE or GAS ENCLOSURES. 60% due to LACKING MAINTENANCE (porous flexible brake tubes, corroded brake lines, cut seals at cylinder pistons), 10% due to wrong assembling and repair. → i.e. 2/3 of brake failures are maintenance-preventable, exactly the FDD/maintenance-on-demand target.
- Table 3.10 water cooling system of passenger cars, ADAC 1999 [3.1], % of all failures: V-belt 29 | flexible pipes (heating/cooling) 20 | cylinder head seals 16 | pump 10 | water/coolant liquid 6 | (stator?) 6 | cooler/expansion vessel 6.
  - Cooling system = about 8% of all vehicle breakdowns. KEY DETECTABILITY NUMBER (verbatim): "By leak detection almost 48% of all failures can be detected, e.g. by measuring the coolant liquid level."
- Table 3.11 damage statistics of components in the CHEMICAL INDUSTRY during ASSEMBLING AND COMMISSIONING [3.3],[3.12], % of all failures: pipes 10 | columns, cooling towers 9 | tanks, containers, reactors 18 | vessels, filters, mufflers 9 | heat exchangers 14 | ovens 14. [percentages do not sum to 100 — table is an extract]
- Table 3.12 damage statistics of components in the PROCESS INDUSTRIES (refineries, petrochemical, gas production, terminals, general process industries), based on 2023 FAILURES [3.12], % of all failures given as ranges: pipes 5-22 | tanks 5-21 | containers 5-20 | reactors 3-20 | heat exchangers 4-5 | ovens, vessels, heaters 4-7. [OCR? the em-dash ranges may be mis-split]
- Relative frequency of accidents especially high in: paper, cellulose, alkali-chlorine, fertilizer, chemical (US industries, 1994-1999) — up to 200 accidents per year, e.g. in the paper industry.
- PIPES AND PIPELINES = most frequent cause for damages (up to 33% or even 46% according to other sources), followed by TANKS, CONTAINERS, REACTORS.
  - Pipe damage reasons: material weakening through erosion/corrosion or chemical corrosion, ESPECIALLY AT ELBOWS, and unsuitable material. Further: overpressure 20%, corrosion 16%, human operating errors 31%.
  - ALL HUMAN ERRORS = 41%, split into wrong MAINTENANCE 39%, DESIGN 27%, OPERATION 14%.
  - Valve damages are counted inside pipes, about 4% to 11% of pipe damages.
  - Tanks and containers cause the next frequent damages, especially in the chemical industry by OVERFILLING or FAILING OF WELDING SEAMS. Pipes + tanks + containers = the reason of about 30-50% of all events.
  - PUNCHLINE (verbatim): "This means that especially the MORE SIMPLE COMPONENTS and not the more complicated ones increase the overall damages."
- COSTS PER EVENT, average for material/property and break of operations (based on 2700 damages since 1984) [3.12]: petrochemical industry 20 / 28 Mill US$; refineries 15 / 17 Mill US$; chemical processes 11 / 15 Mill US$; machines, electronics 5 / 7 Mill US$. [first number = material/property, second = break of operation, per the heading order]

#### 3.6 Problems (1391-1404) — worked-exercise inputs, all solvable with the Ch 3 formulas
- 1) 10000 devices, 10 failures observed each year → determine failure rate and MTTF.
- 2) Mortality rate of a 30-year-old man λ = 10⁻³ [1/year] (printed "1077", exponent unreliable [OCR?]) → estimated lifetime as MTTF if health condition stays the same.
- 3) Estimate the infant phase, normal phase and ageing phase of a HUMAN and an AUTOMOBILE; determine the reasons for failures in all three life phases (bathtub-curve mapping exercise).
- 4) Manufacturing unit λᵢ = 1 failure per year → overall failure rate and MTTF for 2, 3, 5, 10 identical units in SERIES; then the same numbers for PARALLEL connection.
- 5) Passenger cars ≈ 300 h/year operation time; λ = 10⁻⁵ [1/h] (printed "107?") → how many fail in a population of 10⁶ cars in the 1st and the 5th year? (Compare Example 3.2.)
- 6) Hydraulic brake system of passenger cars has REDUNDANT paths in parallel configuration; failure rate of one path λ = 10⁻⁶ [1/h] → determine MTTF of the whole brake system.
- 7) Availability of a machine tool for MTTF = 1 year and MTTR = 1 day.
- 8) Determine λ and MTTF for an electric motor WITH GEAR as a series connection of switch, cable, motor, gear using failure rates of Tables 3.2 and 3.3 (applies the "largest λᵢ dominates" rule).
- 9) Truck type A: MTTF = 8 months, repair 2 days; type B: MTTF = 5 months, repair 1 day → compare availability.
- 10) Switching solenoid relays in automobiles: about 5 ppm faulty ones; 50 relays per car → how many cars are affected? What is the failure rate if these faulty relays show up in 1 year or 5 years?

#### Ch 3 boundary note
- Ch 3 body + problems end at line 1404 (Problem 10). Line 1405 is blank/junk; the next chapter's TITLE "Safety, Dependability and System Integrity" and its UNNUMBERED introduction occupy lines 1406-1432 (the harness's Ch3 block runs to 1432); the first numbered section of Ch 4, "## 4.1 Reliability analysis", is at line 1433. So: Ch 3 = 993-1404; Ch 4 heading/intro = 1406-1432; Ch 4 sections start 1433.

#### Bonus: Ch 4 unnumbered intro block (1406-1432) — captured because it sits inside the Ch3 line range
- For safety-related systems, all aspects of RELIABILITY, AVAILABILITY, MAINTAINABILITY and SAFETY = **RAMS** must be considered, because they are relevant for the RESPONSIBILITY of the manufacturers and the ACCEPTABILITY of customers. Special procedures exist in railway, aircraft, space, military and nuclear systems; covered by the terms SYSTEM INTEGRITY or SYSTEM DEPENDABILITY.
- Different safety requirements → different LEVELS OF INTEGRITY of safety-related systems, from lowest to highest requirements.
- SAFETY INTEGRITY (verbatim, [4.2] — identical wording to the Ch 2 §2.3 definition): "Safety integrity is the probability of a safety-related system satisfactorily performing the required safety functions under all the stated conditions within a stated period of time."
- Safety and reliability are generally achieved by a combination of FIVE MEANS (verbatim list): FAULT AVOIDANCE; FAULT REMOVAL; FAULT TOLERANCE; FAULT DETECTION AND DIAGNOSIS; AUTOMATIC SUPERVISION AND PROTECTION.
  - Fault AVOIDANCE and REMOVAL are mainly accomplished during DESIGN and TESTING phase.
- Analysis methods for investigating the effect of faults on reliability/safety during design AND for TYPE CERTIFICATION (verbatim list): reliability analysis; EVENT TREE ANALYSIS (ETA); FAULT TREE ANALYSIS (FTA); FAILURE MODE AND EFFECT ANALYSIS (FMEA); HAZARD ANALYSIS (HA); RISK CLASSIFICATION. Methods developed in special fields are more or less accepted in other fields. Refs [4.13], [4.2].
- Ch 4.1 (1435-1437, first lines only, outside scope but boundary-relevant): random faults occur at random time subject to DEGRADATION MECHANISMS (esp. electronic hardware; depend on component quality, manufacturing tolerances, operational stress); SYSTEMATIC faults/failures are related DETERMINISTICALLY to a certain cause (human errors, manufacturing processes, operational procedures). "Random hardware failures can be predicted with reasonable accuracy, based on the experience with large numbers of pieces. However, SYSTEMATIC failures cannot be accurately predicted based on statistics." Cross-refs back to §3.1 and Table 3.1; measures R(t), λ [h⁻¹] (e.g. failures per 10⁶ hours), MTTF [h]; series connections DETERIORATE and parallel (redundant) connections IMPROVE reliability.

### Cross-chapter map as actually stated in Ch 1-3
- Ch 2 → Ch 3 (RAM measures, worked numbers) → Ch 4 (safety integrity, ETA/FTA/FMEA/HA/risk classification) → Ch 23.1 (terminology/standardization bibliography).
- Ch 2 fault tolerance/redundancy → Part IV, Ch 18-19; Ch 3 §3.4 fault management also points at Ch 19.
- Ch 2 §2.5 analytic symptoms (limit checking / signal models / process models) = the three routes that become Ch 7 (single-signal + thresholds + statistical change detection), Ch 8 (signal models: Fourier, correlation, FFT, STFT, wavelet), Ch 9-11 (parameter estimation, parity equations, observers), Ch 13 (PCA), Ch 14 (comparison); heuristic symptoms + unified symptom representation → Ch 16-17 (classification, fuzzy, neuro-fuzzy, fault-symptom trees, forward/backward chaining).
- Ch 3 §3.1.1 fault time behavior (permanent/transient/intermittent/noise/drift) → Figure 5.3 in Ch 5 (fault models); additive/multiplicative fault models also Ch 5-6.
- Recurring book thesis, stated three ways: (a) limit checking detects too late and cannot diagnose (Ch 1, Ch 2); (b) closed loops hide faults in Y(t), so monitor U(t) too (Ch 2); (c) FDD raises AVAILABILITY by increasing MTTF (maintenance on demand) and decreasing MTTR (fast diagnosis) (Ch 2 §2.3, Ch 3 §3.2-3.3) — and the economics justify it: lifetime costs ≈ 3.5× acquisition costs (Table 3.8), 41% of process-industry damage events involve human error with 39% of those being wrong maintenance, and simple components (pipes/tanks/containers) cause 30-50% of events.

## Isermann Ch4-6 — Safety-Related System Design, Process/Fault Modelling, Fault Detection Methods
Source: ~/.knowledge/isermann-fault-diagnosis/pi/full_text.txt (pdf_inspector OCR markdown). Ch4 ends ~line 1631, Ch5 at 1632-2162, Ch6 at 2163-2434; Ch7 ("Fault detection with limit checking", 7.1 "Limit checking of absolute values") starts ~2426-2435.

### Ch 4 — Development of Safety-Related Systems (source lines ~1428-1631)
Chapter purpose (1431): methods developed in special fields are "more or less accepted in other fields", reviewed "to find an appropriate procedure for developing safety-related systems".

#### 4.1 Reliability analysis (1433)
- RELIABILITY (verbatim): "the probability of a component or system to function correctly over a certain period of time and for certain operating conditions." Unreliability arises if faults develop/appear which lead to failure.
- Faults and failures are RANDOM or SYSTEMATIC (Table 3.1): random faults occur at random times driven by degradation mechanisms, especially electronic hardware; degradation depends on component quality, manufacturing tolerances, operational stress. Systematic faults/failures are "related in a deterministic way to a certain cause" (human errors, manufacturing processes, operational procedures).
- Predictability: random hardware failures "can be predicted with reasonable accuracy, based on the experience with large numbers of pieces"; systematic failures "cannot be accurately predicted based on statistics".
- Quantification measures: reliability function R(t), failure rate λ [1/h] (e.g. failure per 10^6 hours) [OCR: "A{h7'"] , Mean Time To Failures MTTF [h]. Series connections deteriorate reliability; parallel (redundant) connections improve it.
- Failure physics by component class: mechanical — distortion, fatigue, fracture, wear, corrosion; improved a lot by oversizing, protection (corrosion), wear reduction, "generally need no redundancy". Hydraulic — more subject to wear and faults through the fluid and sealing; redundancy significant e.g. for aircraft. Electrical — "can be improved by almost all measures". Electronic hardware — depends greatly on manufacturing process, environmental conditions, internal load; failures sudden and more random; improve especially by redundancy and protection. Software (systematic faults) — "usually only redundancy with diversity helps and maintenance to reduce bugs."
- Table 4.1 (potential: ++ very large, + large, 0 small, x not usable; cells heavily OCR-garbled): oversizing: mech ++, hydraulic +, software 0; maintenance: mech ++, hydraulic +, hw 0, software +; protection: electrical +, software 0; wear reduction: mech +?, hyd +, elec +, hw 0, sw 0; redundancy: software +; static redundancy: hydraulic +, hw 0; dynamic redundancy: hw ++, software +; redundancy w/ diversity: hw ++, software ++ (several cells [OCR?]). "This influences the design of safety-related systems considerably."

#### 4.2 Event tree analysis (ETA) and fault tree analysis (FTA) (1443)
- ETA (verbatim spirit): "begins with the event of a component (a basic fault) and progresses this through all the components in normal or fail operational mode and determines the consequence of the system's function, i.e. either active or inactive." Must consider normal AND failed conditions of all connected components incl. logic AND/OR. Each event branches: N events → 2^N branches → very large trees. Only binary states.
- Fig 4.1 caption: ETA for three components in series — "inductive analysis from special cause to general system effects".
- FTA: "proceeds in the reverse direction of ETA. It begins with the failure of the system (as top event) and determines the possible causes in the components respective basic components failures including logic operations." Only failed events considered → smaller tree than ETA. Binary states only.
- Fig 4.2 caption: FTA for six components, parallel for 1,2 and 5,6, serial for 3,5 — "deductive analysis from special effects to causes".

#### 4.3 Failure mode and effects analysis (FMEA) (1462)
- FMEA (verbatim): "a formalized method to consider all components, their functions, failure modes and causal system failures." Developed 1960s, used by NASA for Apollo, later aerospace + nuclear power; now standard in automotive industry.
- Procedure: list all components + operating modes + failure modes → for each failure mode: possible causes, effects on the unit and on the complete system, counter actions. "Usually only single failures are considered." Worksheet = Table 4.2 (Component | Failure mode | Failure causes | Failure effect on unit | Failure effect on system | Counter action). Use: detect weak spots of the design in early and later development stages.
- Result: tree-like network with binary states, like an event tree but without normal operating modes and without logic interconnection → "does not blow up like ETA". Strength: completeness. Weakness: "very time-consuming".
- FMEA + FTA complement each other: FMEA yields possible system failures = inputs of FTA.
- FMECA = FMEA extension: importance of each component failure via its probability of occurrence and effects on system, "i.e. by expressing the risk of operation".
- Failure Risk Priority Number (FRPN) states criticality; formula not decoded by OCR [OCR: standard FMEA product A·B·E form]. Ranking numbers 1..10 for A, B, E ("Tables 4.3 and 4.4"; detection-rate E ranking table not visible in OCR run [OCR?]).
- Table 4.3 (Ranking A = possibility of failure occurrence, passenger cars; failure rate assumes 300 operating hours/year): rank 10 very high (500,000 failures/yr), 9 high (50,000; 10,000), medium 5,000/2,000/1,000, low 100/50, very low 1 failure/yr; λ column badly garbled — readable fragments: 1.67·10⁻³, 0.67·10⁻³, 0.33·10⁻³, 0.33·10⁻⁴, 1.67·10⁻⁵, 0.33·10⁻⁶ (row mapping uncertain [OCR?]).
- Table 4.4 (Ranking B = effects of failures, vehicles): 10,9 catastrophic | system damage | death | destruction, fire; 8,7 major | system shut-down | serious injury | serious damage; 6,5 severe | subsystem down | injury | failure; 4,3 minor | partly down | slight injury | minor failure; 2,1 no effect.

#### 4.4 Hazard-analysis (HA) (1519)
- HAZARD (verbatim): "undesirable system conditions with the potential to cause or to contribute to a damage or accident." HA = basic procedure to provide awareness/information of safety-critical components and states.
- Method: from FMEA extract all safety-critical failures → identify hazards ("potential sources of harm, i.e. physical injury or damage"), effects, and ways to minimize or avoid; FMEA-like worksheet; binary state results; example: electromechanical brake [4.4]. Once hazards identified, causes analyzed by FTA with the hazard as top event.
- HAZOP (Hazard and Operability Studies, 1960s chemical industry): systematic investigation of deviations from normal operating conditions; considers parametric changes and out-of-range values that could result in a hazard, and safety features that compensate hazards. Starts from interconnection of components, follows flow of materials/signals, defines attributes via guide words "no, more, less, reverse, early, late". Considers ranges of values (stepwise classification), not just binary. Causes+consequences → hazards; results stated in a fault tree.
- Practice note: these reliability/safety procedures are compiled by a team of engineers in consecutive sessions covering the whole system; must be repeated several times during project development.

#### 4.5 Risk classification (1531)
- ACCIDENT (verbatim): "an unintended event causing injury, death, environmental or material damage." RISK (verbatim): "determined by the combination of the probability (frequency) and its severity (consequence) of a hazard." Qualitative or quantitative classification.
- Eq. (4.2)/(4.3): formula not decoded by OCR; variables (verbatim): F_h = "the frequency (probability) of the hazard" [OCR "Fy,"], C = "the consequence (severity)" [OCR "C'"]. Risk reduction accomplished by reducing both risk parameters (probability and severity). Assignment of risk measures is domain-specific (nuclear, aircraft, heating/ventilating) → industry-specific standards.
- Table 4.5 accident frequency classes (military): frequent = continually experienced; probable = often; occasional = several times; remote = some time; improbable = unlikely but may exceptionally occur; incredible = extremely unlikely at all.
- Table 4.6 (aircraft hazard probabilities, garbled): critical / loss of aircraft / catastrophic / extremely improbable [~10⁻⁹ per flight-hour class, OCR?]; essential / large safety reduction / hazardous / improbable + extremely remote [OCR]; essential / significant safety reduction / major / improbable+remote [~10⁻⁷..10⁻⁵, OCR]; non-essential / minor / probable+reasonably probable [~10⁻⁴..10⁻³, OCR]; non-essential / normal or nuisance / probable+frequent [~10⁻²..10⁻¹, OCR]. Columns: occurrence per flight-hour; flight hours / flight years per occurrence.
- Table 4.7 risk classes: I intolerable; II undesirable, tolerable only if risk reduction impractical or costs greatly disproportional to improvement; III tolerable if cost of reduction would exceed improvement gained; IV negligible.
- Table 4.8 frequency × consequence matrix (rows frequent…incredible × cols catastrophic/critical/marginal/negligible) → classes I..IV; cells partially garbled [OCR: e.g. improbable row ll/Ul/IV/IV; incredible row all IV].
- SIL (safety integrity levels): "Based on the probability of dangerous failures ... the JEC has proposed four safety integrity levels (SIL) for electronic programmable systems." SIL = "a measure of the likelihood of the safety system correctly performing its tasks." Table 49 (cells badly garbled; exponential mapping reconstructed from hours/years columns [OCR]):
  - SIL 4: failure prob 10⁻⁸…10⁻⁹ /h | 10⁸…10⁹ operating h per failure | 10⁴…10⁵ years
  - SIL 3: 10⁻⁷…10⁻⁸ /h | 10⁷…10⁸ h | 10³…10⁴ years
  - SIL 2: 10⁻⁶…10⁻⁷ /h | 10⁶…10⁷ h | 10²…10³ years
  - SIL 1: 10⁻⁵…10⁻⁶ /h | 10⁵…10⁶ h | 10…100 years
- Operational-state weighting: if the effect of a safety-critical failure depends on operational state, risk number can be modified by the frequency of the operational state F_op — e.g. vehicles: acceleration; cruising high/low speed; braking with engine or brake; cornering with/without acceleration or deceleration.

#### 4.6 Integrated reliability and safety design (1603, Fig 4.3 at ~1624)
- Chain: FMEA identifies all components/failures/causes/effects → single failures go to FTA (causes + logic interconnection at component level) → failure causes feed the overall reliability design → remaining unavoidable failures are classified and determine the maintenance procedure.
- Parallel safety chain: FMEA → hazard analysis extracts safety-critical failures → (reduced) fault tree gives causes with logic interconnections, i.e. dangerous faults leading to hazards → design safety system at lower levels → remaining dangerous failures undergo risk classification → determines supervision and safety methods at higher levels to reduce risk to acceptable measure.
- Fault tolerance implemented at component and unit level improves both reliability and safety. Fig 4.3 shows integrated procedure across design and testing phases.
- Operation phase: unavoidable failures covered by maintenance + online supervision and safety methods, "including fault tolerance, protection and supervision with fault detection and diagnosis and appropriate safety actions" — these are the following chapters' topics.

#### 4.7 Problems (1613) — numeric problem data worth capturing
- Prob 8: hazard risk number R_0h per (4.3) [OCR "Ro,"]: passenger aircraft F_h = 10⁻⁸ [1/h] [OCR "1078"], C = 200 people, F_op = 5000 h/year; passenger car F_h = 10⁻⁶ [1/h] [OCR "10°"], C = 4 people, F_op = 300 h/year; assume total breakdown of control system = major effect. Find recommended SIL if injured people = 1 in 100 years or 1000 years [OCR?].
- Prob 9: repeat with total fleets, fleet sizes N_aircraft = 10³, N_cars = 10⁶ [OCR "Ngircraft = 1073 tears = 10°"].

## Isermann Ch5-6 — Process/Fault Models, Signals

### Ch5 Process Models and Fault Modelling (lines 1632-2162)
- Model-based fault detection: extract features (parameters θ, states x, residuals r) from process-model relations between measured U, Y; compare with nominal via change-detection → **analytical symptoms s** → basis for diagnosis.
- Process configs (Fig 5.2): (a) SISO, (b) SISO w/ intermediate measurements, (c) SIMO, (d) MIMO; distinguishability improves a→b→c with more measurements.
- Model classification: continuous vs discrete-event models, each in continuous or discrete time. Continuous = equation-based (linear/nonlinear/time-variant); discrete-event = finite-state machines, functional diagrams, Petri nets.

#### 5.1 Fault models (1656)
- Fault modelling needs understanding physics of real process + **fault-symptom-tree analysis**. Fault causes: 1) wrong design/assembling; 2) wrong operation, missing maintenance; 3) ageing, corrosion, wear.
- Operation phase: present at start or sudden; small/large, step, or gradual drift = **deterministic faults**; intermittent faults = stochastic, especially disadvantageous.
- **5.1.1 Basic fault models**: fault = unpermitted deviation of ≥1 characteristic property ("feature") from usual condition (Ch.2 def). Feature enters physical law Y(t)=g[U(t),x(t),θ] as input uᵢ(t), output yᵢ(t), state xᵢ(t) (time functions) or parameter θᵢ (usually constant) → faults appear as **signal or parameter changes**.
- Time-dependency classes (Fig 5.3): **abrupt (stepwise), incipient (drift-like), intermittent (with interrupts)**.
- Signal changes = **additive faults**: Y(t) = Y₀(t) + f(t) [formula OCR-undecoded; form implied by text]. Detectable change ΔY(t) independent of other signals; additive detectable for any Y₀(t).
- Parameter changes = **multiplicative faults**: another variable multiplied by f(t), e.g. Y(t) = [1+f(t)]·U(t) [formula OCR-undecoded; implied]. Detectable output change ΔY(t) **depends on input**: only detectable if U(t)≠0; size of ΔY scales with size of U. (Fig 5.4: additive on output; multiplicative.)

#### 5.1.2 Examples for fault models (1702)
- **Example 5.1 Sensor faults**: sensor = dynamic transfer element, only output Y(t) accessible, true input Y₀ unknown w/o calibration. Static: linear Y=K₀Y₀ [formulas OCR-undecoded] or nonlinear w/ gain. Dynamic: linear transfer fn, simple case first-order lag (K_s/(1+T_s p)). Disturbances (Fig 5.5, ref [5.19]): **external** (environment): superimposed signal f_a(t) e.g. electromagnetic induction → additive fault, size independent of true value Y₀ (Fig 5.6a); environmental changes f_e(t) (temperature, flow velocity, contamination) deform transfer behavior by changing **gain & time constant** → static+dynamic deviation → **parametric faults**. **Internal** (sensor itself): power supply, R/C/L changes, backlash, friction → static+dynamic changes.
- Three static sensor faults (Fig 5.6): (a) constant offset ΔY (zero offset); (b) gain change ΔK → value-dependent offset ΔY(Y₀); (c) direction-dependent offset (hysteresis) ΔY(sign Ẏ₀). a,b = additive; c = direction-dependent additive.
- Some faults change stochastic character: **mean value and variance of output are also fault models** (ẏ, σ²). Sensor dynamic change (time-constant change ΔT) must be modeled with process → **multiplicative fault**.

- **Example 5.2 Actuator faults** (electromagnetic proportional flow valve, Fig 5.7): chain i=f₁(U), z=f₂(i), A_F=f₃(z), ṁ=f₄(Δp); overall ṁ=f(U), approximated by polynomial (p_i const). **Additive** = parallel shift of characteristic lumped in constant c₀: physical = offset in U, spring counter-position/pretension change, flow-area change at zero position A(z=0). Dry Coulomb friction = direction-dependent offset of input; backlash similar [5.11]. **Multiplicative** = contained in coefficients c₁,c₂: change of flux in coils (coil-wire resistance), air gap in electromagnet, friction at shaft/magnet, power-electronics gain, valve piston geometry, pressure difference Δp change. Shaft/magnet friction & backlash also as direction-dependent parameter. ⇒ many faults are multiplicative class.
- **Example 5.3 Electrical cable connection** (Fig 5.8): cable resistance R₁+R₂ feeding load R₄; short-circuit fault resistance R₃=fr between them, shortcut current i₃(t)=f_f(t); model as R₃∈(0,∞).
  - a) Measure i₁,i₄: as changing resistance R₄→ parametric fault, "gain" g₁(f_f) changes (Kirchhoff node+mesh). Using only current balance (mesh law), shortcut appears **additive** — but offset i₁(t) depends on input current → violates additive definition; additive OK only at constant operating point I₁.
  - b) Measure U₁,i₄: shortcut appears as **multiplicative fault**; parameter estimation yields R₃[o]2 [OCR?], fault size f_f computable if R₁,R₂,R₄ known (f_f→∞ = no shortcut).
- **Example 5.4 Pipeline leak** (Fig 5.9; measure in/out flows ṁ₁,ṁ₄, pressures p₁,p₄; leak flow ṁ₃(t)=f_leak(t); orifice outflow: leak flow ∝ leak area A_L·√p₃ [OCR?]; analogy to Fig 5.8):
  - a) Measure ṁ₁,ṁ₄: mass balance → leak = **additive fault** at constant operating point ṁ₁=const. With laminar-flow linear resistance law ṁ=G·Δp [reconstructed; OCR undecoded] and leak conductance cr₃=f_fr: **multiplicative fault** over arbitrary operating points ṁ.
  - b) Measure p₁,ṁ₄: leak = **multiplicative** (analog to electrical). Additive only via balance eq. at fixed op point. **Clogging**: conductance cr₁ (→resistance) grows → also multiplicative.
- **Key lesson (line 1880)**: additive vs multiplicative depends on **model choice + physical nature**. Sensors mostly additive; actuators more multiplicative than additive; processes additive if only balance equations, but multiplicative when constitutive/phenomenological laws used in detail. Fault modelling must consider underlying physics.

#### 5.2 Process models
- **5.2.1 Theoretical vs experimental modelling**: theoretical = first principles from laws of nature, start from process elements, simplify with assumptions. Five basic-equation types: (1) balance equations (stored masses/energies/impulses); (2) constitutive equations (physical-chemical state eqs of elements); (3) phenomenological equations for irreversible/equalizing processes (heat conduction, diffusion, chemical reaction); (4) entropy balance equations (multiple irreversible processes); (5) connection equations (element interconnection).
- Distributed-parameter systems → PDEs in space+time; negligible space dependence → lumped parameters → ODEs. Simplifications: linearization, model-order reduction, lumped approx of distributed systems. Balance equations always linear; phenomenological often linear in wide ranges; **constitutive equations introduce nonlinearity**.
- Experimental modelling = **identification**: from measurements + a-priori knowledge; natural operating or artificial test signals; parametric/nonparametric → experimental model [refs 5.3, 5.13, 5.16]. Comparing theory vs experiment reveals which modelling steps to correct; they mutually complete: white-box = theoretical (functional relation physical data↔parameters, good for design/simulation), black-box = experimental (numeric parameters, physics unknown; often more accurate/cheaper → good for controller tuning, signal prediction, fault detection). Intermediate: **light-grey** (laws known, parameters measured), **dark-grey** (only physical if-then rules known, parameters experimental), Fig 5.10.
- **5.2.2 Static process models**: steady-state behavior via characteristic curves (measured or computed); often polynomial approx y=β₀+β₁u+...+β_q u^q [reconstructed; OCR undecoded]. **Δβ₀ = additive fault; Δβᵢ (i=1..q) = multiplicative faults**. Input fault f_U and output fault f_Y additive (f_Y=Δβ₀). βᵢ depend on physical process parameters pⱼ (see 5.2.3; flow-valve/ circulation-pump examples Ch.21). Fig 5.11: static model with parametric faults Δf and additive f_U, f_Y.

- **5.2.3 Linear dynamic process models**: dynamics adds info vs static — time-varying inputs excite mass/energy/momentum storages → internal parameters + state variables reveal fault changes [5.8].
- **Example 5.5 Spring-mass-damper**: serial spring-mass-damper (or parallel spring+damper): m·z̈ + d·ż + c·z = ΔF_a (excitation force on mass, z = deviation from steady state) [equation OCR-undecoded, standard form]. TF: G(p)=K/(1+a₁p+a₂p²) with **K=1/c, a₁=d/c, a₂=m/c** (i.e. ω₀=√(c/m), damping ratio D=d/(2√(mc)) [reconstructed]). Static reduces to z = ΔF_a/c → only spring constant c observable statically; dynamic excitation reveals 3 params (m, d → ω₀, D) = extra process-condition info.
- a) Continuous-time models: lumped-parameter dynamic processes → generally nonlinear ODEs; linearize around operating point (Y₀|U₀) → linear ODE b₀y + b₁ẏ + ... + b_q y⁽⁾ = a₀u + ... [OCR undecoded; standard n-th order form]. Transfer function via Laplace (ratio of polynomial coeffs aᵢ/bⱼ).
- Fig 5.12: input fault f_U and output fault f_Y **additive**; parameter faults Δaᵢ, Δbᵢ **multiplicative**. Additive f_U/f_Y change output even with constant input U → detectable deviations (Fig 5.13: 1st-order step responses).
- **Example 5.6 Time-varying params of first-order process**: a₁ẏ(t)+y(t)=b₀u(t)+b₁u̇(t); steady state y=b₀u. Deviations: a₁Δẏ+Δy = b₀Δu + b₁Δu̇. Consequences of parameter steps at **constant input (u=0 deviation, steady state)**: **Δa₁ step → no output change** in steady state; **Δb₀ changes gain → lasting Δy**; **Δb₁** (lead/differential term) → no output change if u̇=0. If input change u(t)=ΔU(t) happens simultaneously: **passing (transient) deviations** for Δa₁, Δb₁ (Figs 5.14-5.15). **Lesson: gain changes detectable in steady state; other parameters (a₁, b₁) require input excitation to observe.**
- Slowly changing params (slow relative to process dynamics): terms with derivatives of parameter changes (∂Δf/∂t etc.) small → simplified approximations usable [formulas OCR-undecoded].
- Vector form ẏ = A₀y + B₀u; small parameter changes Δθᵢ → extra terms; slow changes simplify. State-space from ODE: ẋ(t)=Ax(t)+Bu(t), y=Cx (Fig 5.16): additive faults as input/state faults fₓ or output faults f_m; parametric faults Δbᵢ, Δaᵢ, Δcᵢ = multiplicative. Similar for nonlinear, MIMO, discrete time.

- b) Discrete-time models: sample with T₀, k = t/T₀ = 0,1,2,...; small T₀ → discretize ODEs; larger T₀ → amplitude-modulated δ-functions → both give **difference equations**; z-transform (z=e^{pT₀}) → z-transfer function G_D(z) (may include holding element). Relation G(z)↔G(s) simple only for order n=1,2; complicated for higher orders [5.7],[5.1].
- **Remarks on fault modelling**: most faults are **multiplicative**, additive only in special cases; constant additive faults on measurable signals do NOT cover most real faults. Sensor faults come as constant / value-dependent / direction-dependent offsets — constant f_Y covers only one type. Actuator faults mostly multiplicative → output deviations scale with input size. Figs 5.11/5.12/5.16 additive & multiplicative injections are **idealized assumptions**.
- c) **Model params ↔ physical params**: model params θᵢ depend on physical process coefficients p (stiffness, damping, resistance, capacitance) via **nonlinear algebraic relations** θ=f(p). If inversion p=g(θ) exists, Δp computable from θ̂/Δθ̂ → better fault **localization** (faults affect specific pᵢ) → eases diagnosis. Unique inversion requires **identifiability condition** (implicit function theorem): functional determinant (Jacobian ∂θ/∂p) must satisfy rank/nonzero condition [OCR-undecoded; see Ch 23.4].
- **5.2.4 Nonlinear process models**: nonlinear static+dynamic esp. over wide operating ranges; structure follows from first-principles modelling (balance/constitutive/phenomenological laws); check if directly usable with linear-system FDI methods. Typical approximators (given as discrete-time):
  - a) Classical nonlinear dynamic models: polynomial approximators — general: **Volterra series, Kolmogorov-Gabor polynomials**; structured: **Hammerstein, Wiener, nonlinear difference equation (NDE)** models. **Bilinear systems**: input U(k) multiplied by state x(k); example: externally excited DC motor (excitation current multiplies speed ω and armature current I_A) [5.6,5.17,5.23].
  - b) Artificial neural networks: general-purpose, no structure knowledge needed (Ch. 9 [OCR shows "Chapter 0"]).
- **5.3 Problems** (sample): time-behavior fault types; typical temperature/pressure/flow sensor faults; additive vs multiplicative (sensor example); thermocouple contamination fault type; pneumatic diaphragm actuator faults; oil-pipeline leak via mass balance vs resistance laws; RLC circuit param faults detectable static vs dynamic; 2nd-order mechanical system (Ex 5.5) signal sketches for additive step faults & param faults Δc,Δd with/without input excitation; RC-circuit which of R,C estimable from U_in,U_out or I; continuous vs discrete-time model pros/cons.

### Ch6 Signal models (lines 2157-2434)
- Ch6 intro: many processes oscillatory/cyclic (rotating machines, AC) → periodic signals or periodic parts; random processes (acoustic noise, road surfaces, turbulent flow, on-off switching of consumers in electrical/water networks) → **stochastic signals**. Both usable for fault detection if faults change their models.

#### 6.1 Harmonic oscillations
- **6.1.1 Single oscillations**: harmonic steady-state: y(t)=y₀·sin(ω₀t+φ) [reconstructed] with amplitude y₀, frequency f₀=1/T_p, ω₀=2πf₀, phase φ. **Damped** harmonic: y(t)=y₀·e^{-δt}·sin(ω₀t+φ) [reconstructed], damping constant δ. (Section heading for undamped periodic: valid for cycle duration T_p.) Formation examples in mechanical systems in [6.6].
- **6.1.2 Superposition**: addition of oscillations y=y₁+y₂; two undamped oscillations ω₁,ω₂ → amplitude spectrum = two spectral lines (Fig 6.1).
- **6.1.3 Amplitude modulation**: carrier ω₁ (amplitude y₀₁) altered by modulating oscillation ω₂ (amplitude y₀₂): **multiplicative** operation y = y₀₁(1+m·sin ω₂t)·sin ω₁t [reconstructed]; trig identity sinα·sinβ = ½[cos(α−β)−cos(α+β)] → **two components of equal amplitude at difference (ω₁−ω₂) and sum (ω₁+ω₂) frequencies** (Fig 6.2 spectrum).
- **6.1.5 Beating (Libration)** [heading order scrambled in OCR: printed before 6.1.4]: superposition of two same-amplitude oscillations with small Δω=ω₂−ω₁; identity sin α + sin β = 2 sin[(α+β)/2]·cos[(α−β)/2] [reconstructed] → carrier at mean freq modulated by envelope cos(Δω t/2) — beating.

- **6.1.4 Frequency & phase modulation**: carrier modulated in frequency, or phase angle modulated [formulas OCR-undecoded]. Used in communication engineering — information in frequency/phase of carrier; amplitude disturbances practically don't affect demodulation/reconstruction.
- **Example 6.1** (Fig 6.3 time courses of AM/FM/PM of a signal of two undamped partial oscillations; caption OCR-garbled): (a) AM: v(t)=sin(2π·10Hz·t)·sin(2π·1Hz·t + 2/3) [OCR? phase likely 2π/3]; (b) FM: v(t)=2sin[(2π·10Hz)t − 0.5·sin(2π·1Hz·t + 2π/3)] [OCR?]; (c) PM: v(t)=0.5sin(2π·1Hz·t + 2·sin(2π·10Hz·t) + π/3) [OCR?, indices garbled]. Carrier ≈ 10 Hz, modulating ≈ 1 Hz.
- Beating detail (belongs with 6.1.5): result = sinusoid with **averaged frequency (ω₁+ω₂)/2** and amplitude y₀(t) varying cosinusoidally with **half-difference frequency Δω/2**. Superposition of adjacent-frequency oscillations = amplitude-modulated signal: carrier (ω₁+ω₂)/2, modulation (ω₂−ω₁)/2.
- **Example 6.2**: superposition of two oscillations [formulas OCR-undecoded] → beating with frequency **Δf/2 = 0.005 Hz** (so Δf = 0.01 Hz) [Fig 6.4].
- **6.1.6 Superposition and nonlinear characteristics**: signal v(t)=sin ω₁t + sin ω₂t [reconstructed] fed to nonlinear characteristic y = f(v) (squared: a₂v²) → squared sinusoids at each fundamental + amplitude-modulated sinusoid; via trig identity sin²α = ½(1−cos2α) [reconstructed] → output angular frequencies {2ω₁, 2ω₂, ω₁+ω₂, |ω₁−ω₂|} [reconstructed list; OCR "the angular frequencies become..."] **plus a DC offset** (Fig 6.5: squared characteristic on two-line spectrum). **Lesson: nonlinear transfer elements generate new frequencies at the output** (harmonics + intermodulation) — basis for spectral fault signatures.

#### 6.2 Stochastic signals
- **6.2.1 Continuous time**: time history random, not exactly describable; describe properties via statistics/probability/averaging. Measurable stochastic signals not fully random — internal relations → math signal models. One signal source → family/ensemble of random functions xᵢ(t) = **stochastic process**; one member = **sample function**. Stationary = PDFs independent of time; **ergodic hypothesis**: ensemble averaging ≡ time-averaging of one sample function over infinite interval.
- Characteristic values (formulas OCR-undecoded; standard forms reconstructed):
  - average value m = lim_{T→∞} (1/T)∫x(t)dt
  - quadratic average / variance ψ² = lim (1/T)∫x²(t)dt [variance about mean flagged [OCR?]]
  - **auto-correlation function (ACF)** rₓₓ(τ) = lim (1/T)∫x(t)x(t+τ)dt — internal similarity of the random signal
  - **auto-covariance function** Cₓₓ(τ) = rₓₓ(τ) − m² [reconstructed]
  - **cross-correlation function (CCF)** rₓ_z(τ) = lim (1/T)∫x(t)z(t+τ)dt — relation between two different stochastic signals
  - **power density** (spectral density) Sₓ(ω) = Fourier transform of the auto-covariance function [Wiener-Khinchin]
- **White noise**: totally statistically independent → covariance Cₓₓ(τ)=S₀·δ(τ) [reconstructed]; constant power density S₀=const at all frequencies; **not realizable; infinite variance**.
- ACF of periodic signals is also periodic → correlation functions separate periodic vs stochastic signal components well [6.5]. Fig 6.6 signal models: white noise; high-frequent noise; low-frequent noise; harmonic oscillation; harmonic + stochastic noise; DC signal.
- **6.2.2 Discrete time**: from sampling continuous signals with T₀, k = t/T₀ = 0,1,2,...; model values follow by replacing integrals with sums: average, variance, ACF r(kT₀)... [formulas OCR-undecoded; discrete analogs: (1/N)Σ over N samples].

- Discrete-time white noise: covariance ∝ **Kronecker delta δ(z)** [C_xx(k)=S₀δ(k), reconstructed]; **contrast: discrete white noise IS realizable with finite variance** (vs continuous: not realizable, infinite variance).
- **ARMA model of stochastic signals**: stochastic difference equation = filtered discrete white noise v(k): a₀y(k)+a₁y(k−1)+...+a_n y(k−n) = b₀v(k)+...+b_m v(k−m) [reconstructed structure]; y(k) = output of fictitious filter with z-transfer G(v→y) driven by white noise with **zero mean, variance σ²=1** [OCR? "o7=1"]. Specializations: **AR process** (only y-lags; MA numerator = 1) and **MA process** (only v-terms) ⇒ general case (6.32) = **ARMA process** [6.3,6.1,6.5].
- **6.3 Problems** (with numbers): (1) 1000 Hz acoustic harmonic AM by 50 Hz → sidebands 950/1050 Hz (derived via 6.1.3). (2) harmonic f₁=100 Hz, amp y₀₁=1 [OCR?], modulated by f₂=20 Hz amp y₀₂=0.5 → sidebands 80/120 Hz + carrier (derived; sketch amplitude spectrum). (3) aircraft two engines at 2500 & 2510 rpm, six-cylinder four-stroke, noise at ignition frequency → which frequencies heard? (ignition freq = rpm·3/60 → 125 vs 125.5 Hz, beating 0.5 Hz [derived]). (4) solenoid armature force ∝ square of magnetomotive force/current → AC 50 or 60 Hz → force pulsation at double frequency 100/120 Hz (derived, cf. 6.1.6 squaring). (5) difference ACF vs auto-covariance. (6) draw white-noise autocorrelation, continuous vs discrete. (7) knocking detection on gasoline-engine crankshaft-casing walls, oscillations 20–30 kHz: which sensors + detection methods + equations.

