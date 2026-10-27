# Puig & Simani (eds.) Vol 2 — Fault-Tolerant Control for Nonlinear Dynamic Systems

**Diagnosis and Fault-Tolerant Control, Volume 2** (ISTE/Wiley 2021). Deep distillation. Verified chapter map: Intro+Ch1 nonlinear FDI methods (Simani), Ch2 LPV descriptor AFTC (Rodrigues et al. — UASB bioreactor), Ch3 fuzzy/NN observers + predictive FTC (Witczak et al. — twin-rotor), Ch4 NN-based robust MPC (Patan — pneumatic servo SSE tables), Ch5 nonlinear modeling for FTC (Simani/Castaldi — NLGA adaptive fault estimators, recursive Frisch self-tuning PI), Ch6 virtual sensors/actuators LMI FTC (Rotondo/Puig — quadruple-tank), Ch7 conclusions, Ch8 open research agenda (sustainable control). [formula-not-decoded]/[OCR?] tags; nothing invented.

## Puig Vol2 Intro + Ch1 — Nonlinear FDI Methods (source lines 1-1079)

### Volume 2 framing (lines 1-167: title/copyright + full TOC)
- Source file is one PDF extraction of "Diagnosis and Fault-tolerant Control 2 — From Fault Diagnosis to Fault-tolerant Control", ISTE/Wiley 2021, coordinated by Vicenç Puig and Silvio Simani; ISBN 978-1-78945-059-0; LCCN 2021941902; ISTE series: Systems and Industrial Engineering (field dir. Jean-Paul Bourrières), subject head "Reliability, Diagnosis, Safety and Maintenance of Systems" (Jean-Marie Flaus); ERC code PE7_1 Control engineering.
- Note: no standalone prose "Introduction" chapter was OCR'd in this file; lines 1-167 are title/copyright pages + the complete volume TOC. The volume roadmap below comes from TOC headings (titles reliable; per-chapter detail is inference from section titles marked [reconstructed]).
- Vol 2 chapter roadmap (what each chapter does):
  - Ch1 (p.1) Nonlinear Methods for Fault Diagnosis — Simani & Castaldi: tutorial survey of model-based + data-driven FDI for nonlinear dynamic systems (detailed below).
  - Ch2 (p.57) Linear Parameter Varying Methods — Rodrigues, Hamdi, Theilliol: LPV framework; classical preliminaries, problem statement, robust observer-based FTC design + stability analysis, application to an anaerobic bioreactor. LPV = quasi-VA (gain-scheduled linear families) route to nonlinear FTC.
  - Ch3 (p.85) Fuzzy and Neural Network Approaches — Witczak, Pazera, Kukurowski, Mrugalski: TS fuzzy systems, TS models via nonlinear embedding, recurrent neural model + uncertainty identification, actuator/sensor fault estimation (NN and fuzzy), FTC overview, robust fault estimation and control, robust invariant set, efficient predictive FTC, illustrative examples.
  - Ch4 (p.121) Model Predictive Control Methods — Patan: MPC idea, MPC robustness, NN-based robust/nonlinear/approximate MPC, robust control of a pneumatic servo (robust nonlinear NN-MPC + robust approximate NN-MPC).
  - Ch5 (p.143) Nonlinear Modeling for Fault-tolerant Control — Simani & Castaldi: joint fault diagnosis and control, nonlinear adaptive fault estimators, fuzzy FTC, recursive adaptive control, sustainable control; fault tolerance and compensation; FTC design.
  - Ch6 (p.193) Virtual Sensors and Actuators — Rotondo & Puig: problem statement, virtual sensors/actuators (reconfiguration block hardware), LMI-based design, application example.
  - Ch7 (p.215) Conclusions and Ch8 (p.241) Open Research Issues — Puig & Simani; Ch8 heavily covers sustainable control design objectives/concepts/ambition/impacts. Back matter: List of Authors p.265, Index p.267, Summary of Volume 1 p.271.
- Overall arc [reconstructed]: Ch1 surveys nonlinear diagnosis (FDI); Ch2-4 give LPV, fuzzy/NN, MPC synthesis for detection/estimation/FTC; Ch5-6 close the loop with joint diagnosis+tolerant control and virtual sensor/actuator reconfiguration hardware-in-the-loop; Ch7-8 wrap up with open/sustainable-control issues. Vol1 material is only summarized at the back (p.271).

### Ch1. Nonlinear Methods for Fault Diagnosis (Simani & Castaldi; lines 169-1071)
#### 1.1 Introduction (175-199)
- Model-based FDI matured over four decades; residuals = changes between process and model; assumption: residual changes "large and long enough" after a fault to be detectable (181).
- Central issue: model-reality discrepancy — model accuracy limits detection; modeling uncertainty arises from incomplete knowledge of the process (191-193).
- Residual generation is "an essential problem": residual generators based on input-output relations, state/output observers, parity relations, parameter estimation are all special cases of one general framework (195-197).

#### 1.2 Fault diagnosis tasks (201-240)
- Model-based FDI defined as detection+isolation+identification via features from measured signals + a priori mathematical model; faults detected with fixed or variable thresholds on residuals = measured minus model-estimated quantities (203).
- Two-stage module (Fig 1.1), structure first suggested by Chow & Willsky (1980), now canonical (207): (1) residual generation module — residual zero/near-zero fault-free, significantly nonzero under fault, ideally independent of process I/O; (2) residual evaluation — threshold test on instantaneous values or moving averages, or statistical tests: GLR (generalized likelihood ratio), SPRT (sequential probability ratio test) (Isermann 1997, Willsky 1976, Basseville 1988, Patton et al. 2000).
- Fig 1.2 closed-loop FDI scheme: plant + actuators + sensors split into **input and output sensors** + controller; u(t), y(t) and controller signal uR(t) assumed completely available for FDI; distinction input-vs-output sensors flagged as necessary relative to Patton et al. 1989 / Gertler 1998 / Patton et al. 2000 (230).
- Important caveat (228-232): if uR (or u) are NOT available, controller design matters for FDI — a robust controller attenuates fault effects and makes diagnosis harder; conversely if actuator is lumped into the digital controller device, controller can be treated as fault-free and the actuator as the fault-prone subsystem, letting controller dynamics be neglected in the diagnosis design.
- Frequency-domain models appropriate when fault vs disturbance effects occupy different spectral regions (Ding & Frank 1990; Massoumnia et al. 1989); state-space descriptions are the general/rigorous tool for deterministic and stochastic residual generation (238).
- Most monitored systems are nonlinear; growing interest in nonlinear observers, EKFs, fuzzy logic, NNs — but supervision vs an operating point makes linear methods often valid (240).

#### 1.2.1 Residual generation task (242-275)
- Residual generator = mapping: auxiliary redundant signal z(t) = Wz(u(·),y(·)), then symptom r(t) = Wy(z(·),y(·)) (Basseville 1988, Fig 1.3); Wy fault-free ≈ 0, nonzero under plant fault; every method reduces to a mapping fed by process I/O (252-260).
- Simplest generator: Wz = identical plant model/simulator → r(t) = z(t) − y(t); extension: output estimator Wz(u(·),y(·)) fed by both I/O; general input-output form Fig 1.4 (Patton & Chen 1991), different parameterizations per Chen & Patton 1999 (256-270).
- Detection = direct comparison of r(t) or J(r(t)) with fixed/functional threshold; geometric tests with fixed thresholds work best near steady state and for large sudden or long-lasting faults; adaptive thresholds as functions of plant operating conditions/inputs (272-274).

#### 1.2.2 Residual evaluation task (276-304)
- Threshold test on instantaneous values or moving averages; noise/disturbances motivate stochastic representation of residuals with nominal mean/variance (Willsky 1976) [formula-not-decoded] (280-284).
- Fixed threshold Δrtol tuned by ϵ: compromise missed faults vs false alarms (292-296); change-detection tests: likelihood-ratio, Bayes decision, run-sum (Isermann 1984; Basseville & Benveniste 1986; Basseville & Nikiforov 1993); fuzzy/adaptive thresholds improve binary decision (298).
- Multivariable: symptom vector Δr in q-dim space, direction fault-dependent; classification by geometrical distance (Carpenter & Grossberg 1987; Tou & Gonzalez 1974) or artificial NNs (Himmelblau et al. 1991; Meneganti et al. 1998) (300-302).

#### 1.3 Model-based fault diagnosis (306-310)
- This chapter focuses on continuous-time dynamic models; parity-space (Gertler & Singer 1990; Patton & Chen 1991) and observer-based (Beard 1971; Frank 1993; Frank & Ding 1997) schemes summarized per Isermann & Ballé 1997, Patton et al. 2000.

#### 1.3.1 Parity space relations (312-344)
- Parity = consistency check on measurements; roots in static/parallel redundancy (Potter & Suman 1977); hardware variants: identical sensors on same variable, or dissimilar sensors with mutually related outputs; focus here = analytical redundancy (314).
- Model GM run in parallel with plant GP → error vector r (Fig 1.5); if GM=GP, input/output faults fu/fy enter residual [1.4] [formula-not-decoded]; parity equations filtered by matrix Gf → rf [1.5] [formula-not-decoded] to shape detection/isolation properties (Patton et al. 2000; Gertler 1991, 1998) (316-330).
- SISO yields a single residual → cannot distinguish faults; more design freedom with intermediate measurements or MIMO; generalization Chow & Willsky 1984, Lou et al. 1986, state-space extension Gertler 1998 (discrete-time) (332-336).
- Equivalence theorem: discrete-time parity relation ≡ dead-beat observer (Massoumnia 1986; Wünnenberg 1990; Patton et al. 1989; Patton & Chen 1994b) → less design flexibility than unrestricted observers (342).
- Delmaire et al. 1999: parity relations on identified NARX/NARMAX models suffer unavoidable parameter redundancy → multiple inconsistent parameter estimates → inconsistent FDI decisions; fix: observers designed from identified canonical state-space forms (344).

#### 1.3.2 Observer-based approaches (346-385)
- Estimate outputs via dynamic observers (deterministic) or stochastic filters; output estimation error (weighted) = residual; state estimation not needed for FDI; observer-gain freedom gives rich FDI scheme variety (Chen & Patton 1999; Frank 1994) (348-350). Plant model [1.6], diagnostic observer [1.7], Fig 1.7 [formula-not-decoded]; input disturbance v(t), output disturbance w(t), additive actuator/process/sensor faults f(t) (352-364).
- Sudden permanent faults → state estimation error ex(t) deviates; both ex(t) and e(t) usable as residuals; limiting conditions = stability + sensitivity to v,w; noise → extended Kalman filter instead of classical observers (Jazwinski 1970) (370-374). Multiplicative faults = parameter changes (model-reality mismatch), residual influence less direct than additive f(t) (378).
- Dedicated-observer taxonomy (382-385): 1) one observer excited by one output → single sensor faults (Clark 1978); 2) bank excited by all outputs, hypothesis test per fault (Willsky 1976); 3) Dedicated Observer Scheme — bank excited by single outputs → multiple sensor faults (Clark 1978); 4) Generalized Observer Scheme — each observer excited by all outputs except one (Wünnenberg & Frank 1987; Frank 1993).

#### 1.3.3 Nonlinear filtering methods (387-451)
- Low SNR on u,y → filtering needed for FDI performance; KF innovation is zero-mean white (Riccati equation) when model+noise assumptions hold; output fault abruptly changes innovation mean/variance/whiteness → detection basis (Basseville 1988) (389-395).
- EKF for FDD via joint state-and-parameter (augmented state) estimation, recursive nonlinear filtering minimizing conditional mean-square error (Norgaard et al. 2000): discrete nonlinear model [1.8] with fi(t) = ith unknown fault input, noises v,w with covariances Q,R; scheme = nonlinear observer with non-stationary gain K(t), innovation e(t) = y(t) − ŷ(t|t−1), prediction/update eqs [1.13]-[1.19] incl. cross-correlation Pxy — all [formula-not-decoded] (397-441).
- EKF practical drawbacks: parameter estimates converge slower than state estimates; only local convergence guaranteed; alternative: multidimensional Stirling interpolation approximation of hi(·) (Zolghadri 1996) (443).
- Q,R tuning is usually ad hoc manual trials; auto-tuning (Simani et al. 2003): minimize RMS of state-estimate error with positivity + diagonal constraints Q=diag(qi), R=diag(ri), weighting Π per error component; solved with Particle Swarm Optimization (445-451).

#### 1.3.4 Nonlinear geometric approach strategy (453-500)
- NLGA for FDI (De Persis & Isidori 2000, 2001; Bonfè et al. 2006 book extension building NLGA filters for active FTC): coordinate change in state+output space to find an observable subsystem affected by fault f but not by disturbance d; gives necessary AND sufficient solvability conditions (455-457).
- Model [1.20] [formula-not-decoded]: x ∈ open X ⊂ ℜn, control c(t), scalar fault f(t), disturbance d(t) (embedding faults to decouple), smooth vector fields n,ℓ,g,p and map h (459-463).
- Algorithm steps (467-474): 1) minimal conditioned invariant distribution ΣP* containing P = span p(x); 2) from (ΣP*)⊥ get largest observability codistribution Ω* contained in P⊥; 3) ℓ(x) ∉ Ω* → proceed, else fault not detectable; 4) find surjection Ψ1, function Φ1 with (local) diffeomorphism (Φ1,Ψ1∘h) — Φ1 = measured state part affected by f not d, Φ3 = unmeasured part affected by f and d.
- ΣP* by recursion [1.22] using Lie brackets + involutive closure, stops when S(k+1)=Sk; Ω* = Q(k*) = o.c.a.((ΣP*)⊥) via algorithm [1.23] with Lie derivatives Lg [formula-not-decoded] (476-488).
- Detectability test: ℓ(x) ∉ (Ω*)⊥ ⇒ d decoupled and f detectable; in new coordinates the x̄1 subsystem (with x̄2 renamed ȳ2 treated as input) is affected by f alone → basis of the residual generator (488-500).

#### 1.4 Data-driven fault diagnosis (502-512)
- Identification from behavior samples is ill-posed (Hadamard 1964; Söderström & Stoica 1987; Ljung 1999): non-unique, discontinuous in data; a priori knowledge (e.g. smoothness) constrains the model space turning it into a minimization (Tikhonov & Arsenin 1977; Morozov 1984) (504-506).
- Kalman (1982a,b, 1984) critique: associating one model to uncertain data injects "prejudices"; the data-driven line here seeks the whole family of models compatible with noisy sequences; chapter's finding: for DYNAMIC systems a single model is generally compatible — the dynamics' sample correlations carry the extra information, no conflict with Kalman (508-510).
- Nonlinear identification performed with parametric affine, neural and fuzzy models (512).

#### 1.4.1 Online identification methods (514-598)
- Premise: faults reflect in physical process parameters → estimate parameters online from u(t),y(t), compare with fault-free reference model parameters; discrepancy ⇒ fault; data-driven adaptive FDI extensible to FTC (Isermann 1997; Patton et al. 2000) (516-518).
- Equation error (EE) method: SISO discrete-time AR model, parameter vector Θ + data vector φ [1.29]-[1.31] [formula-not-decoded]; equation error via Z-transform with process polynomials A(z),B(z) vs estimates Â(z),B̂(z) (Fig 1.8) (520-546); LS estimate + recursive LS (RLS) form (Patton et al. 2000; Isermann 1992) [formula-not-decoded]; filtering improves estimates under noise (552-568).
- Output error (OE) method when faults directly affect output: OE [1.36] vs model output ŷ [formula-not-decoded]; e(t) nonlinear in parameters → no direct LS solution; numerical optimization = much larger computational effort, generally impossible online, but relatively precise estimates (570-580).
- Fault changing parameters by ΔΘ perturbs output linearly for small deviations [1.38]; Θ depend on physical coefficients p (stiffness, damping, resistance) via nonlinear algebraic maps [1.39]-[1.40]; if invertible, changes Δp computable and often directly fault-related (Patton et al. 2000); Δp not needed for mere detection; applies to nonlinear static models too (Isermann 2005) (582-598).

#### 1.4.2 Machine learning approaches to fault diagnosis (600-776)
- Fuzzy/NN fault estimators implemented as open-loop NARX architectures + training algorithms (602).
- Takagi-Sugeno prototypes (Takagi & Sugeno 1985b): rule i = fuzzy antecedents (combined membership λi(x)) ⇒ crisp affine consequent yi = ai·x + b; #rules = #clusters nC; TS inference [1.42] [formula-not-decoded] = weighted average of linear local models, weights = degrees of fulfillment; approximates nonlinear MISO (Fantuzzi & Rovatti 1996; Babuka 2012) (604-614).
- Dynamic TS: consequents = linear ARX of order o; regressor x stacks current/previous u,y samples [1.43]; parameters split a(i) ↔ output samples, δ(i) ↔ inputs [1.44] [formula-not-decoded] (616-624).
- Antecedent design via fuzzy c-means: data matrix Z (n×N), partition matrix U=[μik], prototypes V; Bezdek goal function J with exponent m>1 and squared inner-product distance norm (shape matrix A) [formula-not-decoded]; Picard iterations updating prototypes+partition; choosing optimal nC is critical (clustering assumes nC regardless of data); degrees of fulfillment then by interpolation/curve fitting (626-654).
- Consequent identification (Simani et al. 1999; Fantuzzi et al. 2002): prediction errors of nC local models as independent problems solved by the Frisch scheme for Errors-In-Variables models: both u and y noisy (u = u*+ũ, y = y*+ỹ); data covariance Σ(i) = noise-free + noise part parameterized by unknown variances σ̃u, σ̃y; Frisch constraint [1.53] defines surfaces Γ(i)=0 — if assumptions hold a single common point = true variances; assumptions usually violated in practice → find nearest point; then per-cluster linear parameters via covariance-corrected equations [formula-not-decoded] (656-692).
- NN basics: perceptron = MISO weighted-sum + activation f (Haykin 2009, Fig 1.9); MLP = unidirectional layers; recurrent nets feed outputs back to previous layers = dynamic memory (Medsker & Jain 1999); tapped delay line MLP intermediate; open-loop NARX net ŷ(k) = fnet(delayed u,y; delays du,dy) estimates current output from past I/O (Fig 1.10); input-only case → feed own outputs back = dynamic NN (Fig 1.11) (694-722).
- Training: batch mode preferred over incremental (faster convergence, smaller errors, more memory); minimize performance function E(w) over P input-target pairs, per-pattern error ep, global error ē, Jacobian J of estimation error [formula-not-decoded] (724-757).
- Table 1.1 training update rules (table decoded cleanly; subscripts slightly garbled [OCR?]): gradient descent w(k+1)=w(k)−α·g(k); Newton–Raphson w−H(k)⁻¹g(k); Gauss–Newton w−(JᵀJ)⁻¹J·ē; Levenberg–Marquardt w−(JᵀJ+μI)⁻¹J·ē — α learning rate, μ combination coefficient (763-770).
- Convergence discussion: gradient descent asymptotically convergent for small α; Newton/Gauss-Newton faster but need matrix inverse (may be singular → instability), Hessian expensive; LM approximates H ≈ JᵀJ+μI, μ>0 ensures invertibility → fast AND stable; chosen to train all NN fault estimators in this book; Jacobian via back-propagation (Marquardt 1963; Hagan & Menhaj 1994) (772-776).

#### 1.5 Model-based and data-driven integrated fault diagnosis (778-866)
- Reliability argues for integrating multiple FDI methods (Isermann 1994; Isermann & Ballé 1997): knowledge-based treatment of analytical + heuristic information (780).
- Fuzzy acts at BOTH levels: fuzzy descriptions generate symptoms AND fuzzy logic handles detection/isolation decisions (Dexter & Benouarets 1997; Isermann 1998) (794); noise makes residuals fluctuate nonzero even fault-free — fuzzy handles vague/imprecise facts where complete info unavailable (788-792).
- Single model can't cover all operating conditions of nonlinear systems; when analytic equations impossible/structure unknown, describe process by collection of local affine fuzzy/non-fuzzy models identified from data (Leontaritis & Billings 1985; Takagi & Sugeno 1985a; Babuška 1998) (784-786).
- Integrated architecture: residual generation (analytical knowledge) + feature extraction (heuristic knowledge) → inference mechanism = residual evaluation + symptom observation + pattern recognition; pattern recognition convenient for identifying fault SIZE when model precision limited (Himmelblau 1978; Pau 1981); NNs handle nonlinear/partially-known processes, noise-tolerant, generalize, adapt (796-800).

#### 1.5 cont. (801-865)
- NN trained to classify measurement patterns directly is NOT practical for nonlinear dynamic processes (pattern classification not unique in dynamic situations); better roles: NN as dynamic model identifier, fault→residual connector, function approximator; combine quantitative + qualitative to raise robustness (802-804).
- Neuro-fuzzy (NF) rationale: NN = black box, no interpretable model, unclear behavior off-nominal (Korbicz et al. 1999); fuzzy = linguistic rule model a human can read, handles imprecise/noisy data → NF structures (Patton et al. 1999; Calado et al. 2001). Three NN-fuzzy couplings: 1) fuzzification of NN inputs/outputs; 2) fuzzification of NN interconnections; 3) NN supplies membership functions + rule base inside a fuzzy model (816-819).
- TS-based NF (local linear consequents, interpretable, usable for control+FDI: Füssel et al. 1997; Isermann & Ballé 1997) vs Mamdani-based NF (fuzzy-set consequents, qualitative; B-spline NN with triangular basis functions = simplest Mamdani NF but large rule set, low transparency) (823). ANFIS (Jang 1993; Jang & Sun 1995): fixed grid-partition structure, hybrid learning = LS for consequents + gradient/back-prop for antecedents; fast for low-dimensional inputs but global back-prop risks losing transparency and local accuracy — fix: get antecedents/rules separately by clustering then optimize (827).
- Structure identification: EA, CART (Jang 1994), clustering, Kohonen maps; product space clustering (Babuška 1998) splits X×Y ⊂ ℜ^(p+1) into locally-linear subspaces; LOLIMOT (Nelles & Isermann 1996) identifies fuzzy models with dynamic linear consequents; hierarchical NF decomposes into MISO/SISO levels to fight input dimensionality (Tachibana & Furuhashi 1994); watch sensitivity to uneven data distribution (initialize with many clusters) (829-831).
- Fig 1.12 integration scheme: m residuals ri(t) [1.63] ideally each sensitive to one fault, but noise/disturbance → cross-sensitivity [formula-not-decoded] → NF classifier maps residual vector to fault via rules [1.64] [formula-not-decoded]; alternative to geometric evaluation: fuzzy threshold δν with C regions of different fault sensitivity, multidimensional fuzzy set ηi = fuzzy boundary of region i [1.65] [formula-not-decoded]; heavy dependence on faulty+fault-free data availability; isolation harder for faults appearing in dynamics (833-845).
- Residuals from nonlinear dynamic prototypes: fuzzy-selected local linear/affine models, output weighted by validity μi(x(t)) [1.66]-[1.67] [formula-not-decoded] (product space clustering or LOLIMOT); from ai,k, bi,k, ci extract physical parameters (time constants, static gains, offsets — Füssel et al. 1997) and compare online with per-section-1.4.1 estimates (Fig 1.13); requires accurate model, minimum parallel output error, sufficient excitation at every operating point (851-865).

#### 1.6 Robust fault diagnosis problem (867-913)
- Critical reliability problem = unavoidable modeling uncertainty (process noise, parameter variations, nonlinearities); design goal: residuals robust and reliable (Frank 1994; Frank & Ding 1997) (869-871).
- Disturbance-decoupling principle: summarize all uncertainty as disturbance with estimable distribution matrix, make residual insensitive to it — via generalized observer schemes, optimal robust parity relations, eigenstructure assignment (Chen et al. 1996; Patton & Chen 1994b; Liu & Patton 1998; Duan et al. 2002) (873-879). Complete decoupling may be impossible (lack of freedom) and can also eliminate the fault effect → robust residual generation = multi-objective optimization: maximize fault effect / minimize uncertainty effect; performance index [1.68] [formula-not-decoded] reformulated as inequalities → large-scale optimization solvers (Davis 1991; Boyd et al. 1994 — LMI machinery implied by citation) (881, 893-897).
- H∞ lineage: factorization approach first (Ding & Frank 1990; Ding et al. 2000); ARE-based H∞/μ robust estimator synthesis (Mangoubi et al. 1992 with Appleby et al. 1991 μ synthesis); FDI as standard H∞ filter with ARE solution (Edelmayer et al. 1997); modeling error blocks in H∞ observer design (Niemann & Stoustrup 1996), nonlinearities treated as modeling-error blocks for nonlinear systems (Stoustrup & Niemann 1998; Stoustrup et al. 1997) (885-887).
- Robust residual generation ≠ robust estimation: residual must STAY fault-sensitive; sensitivity via optimal post-filter on primary residual (Sauter et al. 1997); H∞/μ iteration — design low-disturbance observer by ARE, check fault sensitivity, relax robustness bound until max fault/disturbance sensitivity ratio (Sadrnia et al. 1997); Chen & Patton formulation: minimize ||residual − fault|| w.r.t. disturbance+fault → residual replicates fault, indirectly maximizing fault sensitivity; H∞/H− method introduced Hou & Patton 1996/1997 (LMI formulation per their titles) (883, 889-897); unified optimization solution Ding et al. 2000, ~10 yrs after first proposal.
- Active vs passive robustness (Patton & Chen 1994b; Chen et al. 1996): ACTIVE = uncertainty handled at residual-design stage — model approx modeling errors as disturbances with estimated distribution, then decouple; PASSIVE = adaptive threshold ε(t) generated online, depends on u(t)/operating point (threshold selector/adapter: Clark 1989; Emami-Naeini et al. 1988) (899-902). Caveat: disturbance decoupling methods' real effectiveness undemonstrated — most real uncertainty is modeling error, not disturbance (903).
- Concluding remarks inside 1.6 (905-913): residual-generator schemes favored by algorithmic simplicity (cheap verification & validation on real plants); nonlinear NLGA-type design needs state/output coordinate-transform structural decoupling, possibly simplified models; mixed H-/H∞ trade-off now well understood; adaptive-filter nonlinear FDD additionally estimates fault SIZE — key for online control reconfiguration; avoids input/output derivatives → less noise-sensitive; Monte Carlo experiments used to tune FDI/FDD parameters; must bridge design gap between FDD and recovery (FTC) mechanisms.

#### 1.7 Summary (915-925)
- Tutorial chapter: model-based + data-driven FDI in one uniform mathematical framework; residual generation = central issue; diagnosis success depends on residual robustness to modeling uncertainty; integrated knowledge-based FDI combines analytical + heuristic information (917-925).

#### 1.8 References (927-1070)
- ~90-entry bibliography, OCR clean except duplicates/typos: Patton & Chen 1994a ≡ 1994b same paper, Takagi & Sugeno 1985a/1985b duplicates, Duan et al. 2002 page range "7724-7729" implausible [OCR?]. Key anchors: Chen & Patton 1999; Patton/Frank/Clark 1989 + Issues 2000; Isermann 1984/1997/2005; Basseville & Nikiforov 1993; De Persis & Isidori 2001; Ding et al. 2000; Hou & Patton 1996/97 (LMI H-/H∞ FD observers).
- Content audit for this chapter: NO benchmark plant is numerically studied in Ch1 (three-tank system appears only as Ding et al. 1999 reference title); no Volterra series, no Lipschitz/one-sided-Lipschitz conditions, no LPV/quasi-VP terminology in Ch1 — LPV methods begin Ch2 (header at 1072-1078, Rodrigues/Hamdi/Theilliol, Ch2 introduction starts line 1080).

## Puig Vol2 Ch2 — LPV & Fuzzy Consensus Diagnosis (source 1080-1610)

### Ch2 "Linear Parameter Varying Methods" — Rodrigues, Hamdi, Theilliol
- Actual chapter focus (vs. generic "fuzzy consensus" label): robust ACTIVE fault-tolerant control (AFTC) of quasi-LPV DESCRIPTOR (singular) systems with UNMEASULABLE decision/premise variables, under actuator faults + perturbations; LMI-based state+fault estimation feedback. Ch3 starts line 1611.
- Chapter map stated in intro: 2.2 preliminary quasi-LPV results; 2.3 problem statement; 2.4 robust AFTC state feedback + stability; 2.5 numerical example = two-phase flash system.
- Positioning: ~2000-era AFTC split FDI design from reconfiguration law; newer trend = one unified module doing FDI+FTC simultaneously (observer-based). Most LPV-FTC works assume scheduling variables measurable — this chapter drops that assumption (Lopez-Estrada 2014 gap).
- Notation: x∈Rⁿ, u∈Rᵖ, y∈Rᵐ; descriptor matrix E∈Rⁿˣⁿ possibly singular, rank(E)=r<n; X>0 (X≥0) = positive definite (semi-definite).

### 2.2 Preliminaries: quasi-LPV → polytopic transformation
- Start from nonlinear system; define premise/decision variable ξ(t)=[x(t) u(t)]. Nonlinear elements in A(ξ),B(ξ),C(ξ) treated as premise variables z_j(ξ(t)), j=1..h. Multiple equivalent quasi-LPV representations exist (Tanaka & Wang 2001).
- Convex polytopic transformation: for each premise variable, partition F_{j,1}(z_j)+F_{j,2}(z_j)=1 → h premise variables yield N=2ˡ vertex models (text: N = 2h vertex models per OCR; read as 2^h) [formula-not-decoded].
- Scheduling functions ρ_i = products of the F_{j,τ} partition functions; index τ encodes which partition of which premise variable enters submodel i; vertex matrices A_i (B_i, C_i analog) obtained by replacing z_j with its partition bounds [2.4-2.6].
- Convexity: ρ_i(ξ(t)) ∈ [0,1] and Σρ_i = 1 → system [2.2] rewritten as polytopic LPV [2.10] with time-invariant A_i∈Rⁿˣⁿ, B_i∈Rⁿˣᵖ, C∈Rᵐˣⁿ at polytope vertices; measurement equation usually linear time-invariant in practice.
- Classical LPV: ρ(·) depends only on time, exogenous scheduling parameter (Briat 2015). If ρ depends on endogenous ξ(t) → quasi-LPV; scheduling vector measurable (inputs/outputs) or unmeasurable (states only estimated) — the chapter's hard case.

### 2.3 Problem statement: descriptor quasi-LPV + actuator faults + disturbances
- Plant [2.11-2.12]: polytopic LPV **descriptor** system E ẋ = Σρ_i(ξ) A_i x + Σρ_i B_i u_f + H d(t); d(t)∈R^q bounded unknown disturbance input; u_f = faulty control input; H_i added vertex matrices.
- Actuator fault model: u_f(t) = (I_p − γ(t)) u(t) rewritten as additive external signal f(t) = −γ(t)u(t). γ_k(t) = loss of effectiveness of actuator k — concrete example in text: 50% effectiveness loss ⇒ γ₁(t)=0.50. (Literature note: faults can also be modeled multiplicatively — Rodrigues et al. 2014, Chen et al.)
- AFTC goal: control law u(t) = −Σρ_i(x̂) K_i [x̂(t); f̂(t)]-style state feedback using ESTIMATED state x̂ and ESTIMATED fault f̂ (K_i to find); scheduling uses unmeasurable ξ̂ = [x̂ u]. Core problem: joint state + fault magnitude estimation with online scheduling ρ_i(x̂) when decision variable is not measured.
- Assumptions A1–A5: A1 rank(CB_i)=rank(B_i)=p (input-effectiveness/controllability, classic for observer design; full-column-rank B_i needed for LMI development). A2 (E,A_i,C) R-observable (reconstructs dynamic-part state), A3 impulse-observable (estimates algebraic-part state of descriptor system), each at vertices only — LMI feasibility is the SUFFICIENT condition guaranteeing observability along all scheduling trajectories [2.9]. A4 ‖f‖≤α₁, ‖ḟ‖≤α₂ finite (general, standard). A5 partial actuator faults only: γ_k(t) ∈ [0,1[ (no total outage).
- Key gap callout: quasi-LPV premise variables ρ_i(x(t),u(t)) depend on state → not available when state not fully measured; Rodrigues et al. 2014/2015 did NOT address this.
- Trick: rewrite state eqn [2.17] with extra term w(t) = difference between [2.12] and [2.17] — a bounded VANISHING perturbation: bounded via A4 + bounded d(t) + convex weights, and w(t)→0 iff x̂(t)→x(t). [formula-not-decoded]

### 2.4.1 Robust polytopic observer (RPO) with joint state+fault estimation
- Observer [2.19]: z(t) observer state vector, f̂(t) fault estimate, ŷ=Cx̂; Γ symmetric positive-definite LEARNING-RATE matrix for the fault-estimation dynamics; unknown design matrices N_i, G_i, R_i, U_i, T2 to determine (parameter-dependent, one set per vertex i). [formula-not-decoded]
- Error coordinates: x̂ = z + T2Cy → state estimation error e_x dynamics [2.23-2.28]; fault estimation error e_f [2.22]. Requires rank[E C]=n to build nonsingular T1∈Rⁿˣⁿ, T2∈Rⁿˣᵐ with [E C] structure [2.21]; solution [T1 T2] exists iff condition [2.30] (Hamdi et al. 2012); particular solution via generalized inverse (·)⁺ [2.31].
- After matching conditions [2.25-2.26] (incl. M_i=(T1−I_n)B_i, T̄_i=T1[H_i I_n], w̄=[dᵀ wᵀ]ᵀ), observer error dynamics collapse with L_i = N_iT2 − R_i [2.27-2.28].
- Closed loop with feedback [2.14]: augmented dynamics of x, e_x, e_f; vertex closed-loop matrix Φ_ij=(A_i−B_iK_j) [2.29].
- Differences vs prior work: time-VARYING faults (ḟ≠0, unlike Hamdi et al. 2012) AND perturbations d(t) (unlike Rodrigues et al. 2014).

### 2.4.2 Stability: LMI with equality constraint (Theorem 2.1)
- Lemma 2.1 (scalar μ>0, P1>0; Zhang et al. 2008 bounding inequality) and Lemma 2.2 (scalar α, Υ1>0, Ψ1≤0 bounding) used to handle cross terms [formula-not-decoded].
- THEOREM 2.1: under A1–A5, given scalars σ,μ,β>0, if ∃ symmetric PD matrices Q, X=P1⁻¹, P2, Q4 and matrices W_i, S_i s.t. LMIs hold ∀i,j∈[1..h] subject to EQUALITY constraint [2.40], then x(t), e_x(t), e_f(t) bounded; gains recovered as L_i=Q⁻¹S_i, K_i=W_iX⁻¹. (Change of variables W_i=K_iX, S_i=QL_i.) [formula-not-decoded]
- Proof sketch: quadratic Lyapunov V in (x,e_x,e_f) with P1=X⁻¹,Q,Γ; V̇<0 ensured via lemmas + A1/A4; δ = max over i,j of perturbation bound; result V̇<0 when ε‖x̃‖²>δ (x̃=[x;e_x;e_f]) ⇒ ULC-style convergence to a small ball, not asymptotic to 0 [2.61-2.68].
- REMARK (design knob): with time-varying bounded-rate faults, e_x,e_f converge to a BALL centered at origin sized by δ and ε; radius minimized by choosing learning-rate Γ to minimize δ while ε stays independent of Γ → improves estimation accuracy. Input-to-state convergence [2.68] satisfied after solving LMI.
- Proof mechanics: parameterization Z_ξ, Z_ξξ; block-diagonal X; QPQᵀ PD preservation; Lemma 2.2 replaces X1Λ_ξξX1 with slack scalar β; Schur complement + modified Schur lemma; P1⁻¹Π̃_ξξP1⁻¹ → XΠ_ξξX + XQ4X. Ends with equality constraint [2.40] retained.
- Conservatism reduction options (stated, not proven): parameter-dependent Lyapunov functions (Rodrigues et al. 2013) beat common Lyapunov; Pólya's theorem route (Sala & Arino 2007) trades more LMIs for less conservatism; equality constraint hard to satisfy jointly ⇒ Theorem 2.1 reformulated as an OPTIMIZATION problem (next: min γ or similar, cut at 1469). [OCR?] hard equality [2.40] feasibility flagged as practical difficulty.

### 2.5 Benchmark: UASB anaerobic bioreactor (descriptor quasi-LPV, unmeasurable scheduling)
- NOTE: intro promised "two-phase flash system" but the actual case study is an ANAEROBIC BIOREACTOR (UASB up-flow anaerobic sludge blanket), descriptor model validated in Lopez-Estrada (2014) — internal inconsistency in the chapter itself. [OCR?] not needed; text explicit.
- States: x1=xo anaerobic biomass concentration; x2=s1 organic matter as COD; x3=QCH4 methane biogas outlet flow; x4=μ specific growth rate. Inputs: u1 dilution rate, u2 COD concentration of affluent. Outputs: y1=xo, y2=s1, y3=QCH4. Model modified to MINIMIZE number of varying parameters (nearly-constant ones frozen over operating range).
- Physical parameters: kml mass specific growth rate, kd dilution/death, ks1 semi-saturation, Y1 COD degradation yield, IpH pH inhibition with limits pHLL/pHUL.
- Table 2.1 constant parameters (as bullets):
  - kml = 5.1 gCOD/gCOD·d
  - kd = 0.02 l/d
  - ks1 = 0.5 gCOD/l
  - Y1 = 0.1 gCOD/gCOD
  - YCH4 = 0.35 lCH4/gCOD
  - α = 0.5
  - IpH = 0.9068
- LPV embedding: 2 scheduling variables θ(t) with bounds θj ≤ θ(t) ≤ θ̄j (j=1,2 non-constant elements) → polytope vertices at extrema; weighting functions ρi(θ), i=1..4 = combinations of θj (Hamdi et al. 2012). Quasi-LPV descriptor model augmented with disturbance d(t) + additive actuator fault f(t).
- Disturbance injection numbers: H = [0 0 0.2 0.8]ᵀ constant distribution matrix; d(t) = pseudorandom noise, magnitude 1, frequency 0.02. w(t) perturbation vanishes as x→x̂.
- Design numbers: solved optimization form of Theorem 2.1 with YALMIP; β=0.4, σ=0.1, μ=0.2; observer + controller gain matrices obtained [formula-not-decoded — matrices not rendered].
- Simulation outcome (Figures 2.3-2.4): AFTC (red dashed) corrects outputs y1,y2 under fault and converges to nominal; without AFTC outputs fail to converge. Measurement noise injected: random, max magnitude 0.01 on outputs.
- Fault estimation (Figures 2.5-2.6): real vs estimated f̂1, f̂2 — method estimates AND compensates both constant and TIME-VARYING actuator faults online; chapter calls observer "APO" (adaptive polytopic observer) here vs "RPO" earlier — naming inconsistency [OCR?].
- Verdict claimed: "whatever the fault is — constant or time-varying — the AFTC algorithm... can compensate these faults efficiently and robustly."

### Takeaways / hooks to other chapters
- Chapter novelty vs Vol1 LPV material: scheduling functions computed from ESTIMATED state ξ̂=[x̂ u] (separation-principle-style workaround for unmeasurable premise variables) rather than assuming measured scheduling.
- Technique anchors: polytopic N=2^h vertex embedding (TS-fuzzy-identical machinery, Tanaka & Wang 2001); descriptor-system observability split R- vs impulse-; LMI with equality constraint + generalized-inverse particular solution; Γ learning-rate as accuracy tuning knob shrinking the error ball.
- Reference ladder worth tracking: Hamdi et al. 2012 (PI observer FDI in LPV descriptor), Rodrigues et al. 2014/2015 (observer FTC / adaptive polytopic fault estimation), Lopez-Estrada 2014/2015 (unmeasurable scheduling h-/h∞ FDI), Rotondo/Nejjari/Puig 2013/2016 (quasi-LPV modeling + virtual actuators + set-membership FE — Vol1 links), Wan et al. 2020 (probabilistic set-membership parity — Vol1 Ch set-membership).
- Ch3 starts at line 1611: "Fuzzy and Neural Network Approaches" by Witczak/Pazera/Kukurowski/Mrugalski (Zielona Góra) — that is the actual TS-fuzzy chapter, not this one. Task-label "fuzzy consensus" maps to Ch3, not Ch2; Ch2 has no consensus/fusion of multiple residuals content.

## Puig Vol2 Ch3 — Fuzzy & Neural-Network Approaches (source 1611-2426)

### 3.1. Introduction (1611-1628)
- Chapter setting: actuator fault estimation is the crucial problem for FTC (state estimation used inside the control loop); effective actuator estimation lets redundant actuators compensate a faulty one. Sensor FDI methods are abundant in literature.
- Terminology per this chapter: a **fault** = deviation of at least one system property from its nominal value; a **failure** = complete inability to perform the scheduled mission.
- Classical FDI = three-stage process: fault detection → fault isolation → fault identification (Blanke et al. 2006).
- **Integrated FTC** (Witczak & Puig 2013): the classical FDI process is eliminated and replaced with fault *estimation* only; all fault estimation errors are incorporated into the control design. Cannot fully compensate estimation errors for complex nonlinear systems.
- Observer-based FTC needs an analytical model; when too complex/unavailable, use ANN-based approaches — ANNs imitate behavior without reflecting structure (good for FDI, hard for FTC due to complex math description + no uncertainty description). Solution proposed in the chapter: design a neural model for fault estimation **with its uncertainty description**, converted (without linearization) into **LPV form**.
- Alternative: **Takagi–Sugeno (TS) fuzzy model** = nonlinear system as local linear models blended by fuzzy membership functions; TS-based FTC applied where LPV works: missiles, aircraft, energy production, active vehicle suspension, engines, FTC (Ichalal et al. 2012).
- Sensor FDI via a **bank of observers**, each sensitive to only one fault (Witczak 2007). UIOs decouple the effect of given inputs (e.g., faults) on the state estimation error → estimator insensitive to a chosen set of actuator faults.

### 3.2. Fuzzy model design (1629-1720)
#### 3.2.1. Takagi–Sugeno systems
- Nonlinear system [3.1]–[3.2] with x∈R^n, u∈R^r, y∈R^m, exogenous disturbances w∈R^{nw}. [formula-not-decoded]
- TS fuzzy IF-THEN rule: rule i combines local linear model with matrices A_i (state) and input matrices (OCR rendered "Ai, i" — A_i, B_i) [formula-not-decoded]; **premise variables** s1,k…sp,k may be functions of external disturbances, state variables, and time.
- Blended TS system: x_{k+1} = Σ_i w_i(s_k) A_i x_k + Σ_i w_i(s_k) B_i u_k style [formula-not-decoded]; premise vector s_k = [s1,k,…,sp,k].
- Membership grades: w_i(s_k) built from M_ij(s_j,k) membership grades; normalized weights ρ_i(s_k) = w_i / Σ_j w_j [formula-not-decoded].

#### 3.2.2. Generation of TS models via nonlinear embedding (Kwiatkowski et al. 2006 automated LPV/TS generation; polytopization per Sun & Postlethwaite 1998)
Five-step automated procedure, all formulas [formula-not-decoded]:
- Step 1: write state equation in standard form, each row extended into summands f_ij (T_i summands); each summand decomposed into numerator α_ij, denominator β_ij, constant κ_ij; numerator factored into non-factorisable terms h_ij times inputs u^r and integer state powers x^q.
- Step 2: classify summands into two classes: **K0** = constant / non-factorisable numerator (no positive power of input or state as numerator factor); **KP** = arbitrary positive power of factor where numerator contains positive integer powers of input u_i or state x_i.
- Step 3: select components s_ai,j,k and s_bi,j,k linking summand to entries of state matrix A and input matrix B. If f_ij ∈ K0: nx possible assignments in A, nu in B. If f_ij ∈ K_P and some μ_ijk ≠ 0 or ν_ijk ≠ 0: assign directly to A/B element.
- Step 4: build premise variables from s_a/s_b by **direct assignment** (premise = the component itself) or **superposition** (premise = sum of all summand contributions into the same A/B element); renumber premises to be consistent with [3.3].
- Step 5: **bounding box** method → polytopic LPV/TS: compute upper/lower bounds of each premise s_i over admissible x, u, w; express s_i = μ̄ s̄ + μ_underline s_underline with convex weights as membership functions; subsystems = every available combination of premise memberships in the IF parts.

### 3.3. Neural model design (1721-1820)
#### 3.3.1. Recurrent neural network (RNN)
- Aim: parametric description of a neural model enabling its conversion into **LPV form** (LPV/gain-scheduling popular for usability + linear algebra; Rotondo 2016, Hoffmann & Werner 2015).
- Discrete-time nonlinear system x_{k+1} = f(x_k, u_k), f unknown continuous [formula-not-decoded]. MLP with enough hidden neurons p suffices for static maps but not dynamics → use RNN (modified structure per Lachhab et al. 2008).
- RNN structure: hidden layer activation σ(·); weight matrices **A, B, A11, E1, E2**; state x_k; input u_k ∈ R^q; **actuator fault f_a,k ∈ R^q enters the model as an input** (the fault is a modeled input signal). Training requires measurable state; output matrix C is not part of the ANN (C = I_n during training). [formula-not-decoded]
- RNN → discrete-time LPV form with scheduling parameter α [formula-not-decoded]; advantage: LPV neural model combines with standard state-estimation methods, simplifying training.
- Transformation (based on Abbas & Werner 2008): α = s(ρ) depends on measurable **scheduling signals** ρ ∈ R^s via continuous s: R^s → R^p; scheduling parameter varies in convex polytope Θ = conv hull of vertices v_1..v_q; row-wise varying parameters α_i defined from matrix rows; diagonal Θ = diag(α_1..α_p) collects them; neural state-space [3.22]–[3.23] rewritten into LPV-like then traditional LPV form (A(α), B(α) style). All steps [formula-not-decoded].

#### 3.3.2. Identification of the neural model uncertainty
- Robust control needs a **mathematical uncertainty description** of the identified neural model.
- Final RNN structure (Fig. 3.1, two paths): linear path matrices A ∈ R^{n×n}, B ∈ R^{n×r}; **nonlinear path** matrices A1 ∈ R^{n×va}, B1 ∈ R^{n×vb} with weight matrices E1, E2; D ∈ R^{n×q} diagonal, C output; v_a/v_b = number of nonlinear units in the nonlinear paths; σ_h nonlinear/continuous/differentiable/bounded, σ_o linear. d_k = difference between measured x_d,k and modeled x_k (modeling error as unknown input). [formula-not-decoded]
- Extend RNN with exogenous disturbance w_k via distribution matrices W1, W2; w_k = [w1,k; w2,k] = **process and measurement uncertainties** respectively.
- Key stance: whatever the training method, residual modeling errors are captured as unknown input d_k with distribution matrix D → the neural model always carries a set-membership-style uncertainty wrapper, which is what makes observer-based FTC on neural models possible.

### 3.4. Fault estimation and diagnosis (1821-2050)
#### 3.4.1. Actuator fault estimation using neural networks (1823-1925)
- Simultaneous **state + actuator fault estimation** on the LPV-converted neural model, while attenuating exogenous disturbances and decoupling an unknown input. Luenberger-style observer with E-correction [3.43]–[3.45] [formula-not-decoded]; T = I + EC.
- Assumptions (all [formula-not-decoded]):
  - A3.1: exogenous disturbances bounded (energy-bounded, ‖w‖ ≤ bound) — physical law: disturbances limited.
  - A3.2: actuator fault bounded (must not grow endlessly).
  - A3.3: rank condition enabling **unknown-input decoupling** (cf. Gillijns & De Moor 2007; Chadli & Karimi 2013); requires **TD = 0**.
- Super-vector stacking of state-estimation error + fault-estimation error into compact error dynamics [3.53]-style [formula-not-decoded]. Full methodology: Witczak et al. 2017.
- **Theorem 3.1** (proof = Witczak et al. 2017): for prescribed attenuation level μ > 0, H∞ observer design for [3.22]–[3.23] + observer [3.43]–[3.45] solvable iff matrices P, U, N satisfy LMI constraints [formula-not-decoded]. Design = convex optimization (minimize μ subject to LMIs [3.59]).
- Design recipe (numbered steps):
  - Step 0: identify A_i, B_i from the neural LPV conversion [3.33]–[3.34].
  - Step 1: E = −D[(C D)^T (C D)]^{-1} (C D)^T.
  - Step 2: G from T B − G = 0.
  - Step 3: solve optimization [3.59]; Step 4: solve K̄ from [3.58]; (Step 5 line OCR'd as formula gap); Step 6: N = TA − NEC − LC = TA − K̃C, K̃ = NE + L → get L; Step 7: implement E, F, G, N, L into observer.

#### 3.4.2. Sensor and actuator fault estimation using fuzzy logic (1927-2050)
- TS fuzzy system [3.60]-[3.61] with activations h_i(v_k) ≥ 0, Σ h_i = 1, premise vector v_k = [v1k…vpk]^T built from **measurable** variables (known inputs, outputs); unmeasurable premises handled per Ichalal et al. 2018. Shorthand X(v_k) = Σ h_i(v_k) X_i.
- **Simultaneous estimation of state + actuator faults f_a,k ∈ F_a ⊂ R^{na} + sensor faults f_s,k ∈ F_s ⊂ R^{ns}**; distribution matrices: B_f(v_k) (rank n_a), C_f (rank n_s); feasibility constraint **n_a + n_s ≤ m** (cannot estimate more faults than measured outputs). W1/W2 distribute process/measurement disturbances w1,k, w2,k.
- Trick: actuator fault re-expressed through chosen full-rank matrix f̄ (rank n_a), e.g. f̄ = (1/M)Σ f_i; original fault via **pseudo-inverse** f† [formula-not-decoded]; comparison of [3.60] vs [3.62] absorbs f_a into a modified state equation.
- **Descriptor/state super-vector** x̄_k stacks state + actuator + sensor faults → system recast in singular (descriptor) form [3.66]-[3.67] [formula-not-decoded]; observer [3.68]-[3.69] with internal state z_k ∈ R^{n+na+ns} estimating x̄_k.
- Notable claim: the method **abolishes the typical bounded-rate-of-fault-change assumption** common in the literature (Pazera & Witczak 2019).
- Design conditions via T1, T2 matrices [3.70]; estimation error dynamics [3.73] with w̃_k = [w̄_k^T, w̄_{k+1}^T]^T; full derivation Pazera et al. 2020b.
- **Theorem (quadratic boundedness)**: error system [3.73] strictly quadratically bounded for all w̃_k ∈ E_w iff ∃ P ≻ 0, U, N̄ and α ∈ (0,1) s.t. LMI [3.74] holds. Proof in Pazera et al. 2020b.
- Offline procedure: Step 0 T1,T2 from [3.70]; Step 1 pick α∈(0,1), set N̄_i with U via [3.74]; Step 2 solve for L_i/observer gains (four formula steps [formula-not-decoded]). Online procedure: init z0, iterate z_{k+1}, x̂ from [3.68]-[3.69].
- α tunes convergence rate (Pazera & Witczak 2019); **ellipsoidal bound** on estimation error set by P [formula-not-decoded] → per-variable **uncertainty intervals** for states/faults using columns c_i of identity [formula-not-decoded] → these intervals feed robust FTC downstream.

### 3.5. Fault-tolerant control (2051-2264)
#### 3.5.1. An overview of the fault-tolerant scheme (2053-2106)
- TS form sources: local linearization at operating points, identification from real data, or **nonlinear sector approach** (Tanaka & Wang 2001); details Rotondo et al. 2015. Unmeasurable premises possible (Chadli & Karimi 2013; Ichalal 2012) but out of scope here.
- Normalized TS model output inferred from (s_k, u_k); h_i(s_k) normalized firing strengths via t-norm T (e.g. product) of memberships μ_{F^i_j}(s_jk) [formula-not-decoded].
- Assumptions:
  - A1: rank(B_i) = r for all i = 1..M.
  - A2: actuator fault bound [formula-not-decoded] (actuator fault vector fa,k with distribution B_f, bounded).
  - A3: control constraint set U: |u_i,k| ≤ ū_i, symmetric around zero (asymmetry easy via scaling).
  - A4: col(B(h_k)) ⊆ col(B_f(h_k))-type containment of the disturbance distribution matrix W(h_k) in the control column space; simplest choice **W(h_k) = B(h_k)** (matched-disturbance condition).
- Goal: drive the system to the origin **regardless of actuator fault f_a,k**. Control strategy [3.88]: u predicted over horizon n_c as
  - u_{k+j} = −K(h_k) x_{k+j} + f̂_a,k−1 + c_j (schematic; [formula-not-decoded] for exact form):
  - K(h_k) = Σ h_i(s_k) K_i = **H∞ parallel distributed compensation (PDC)** controller (robust to w_k);
  - f̂_a,k−1 = fault estimate used for **direct fault compensation (virtual actuator-style feedforward)**;
  - c_j = extra design freedom, used only when fault compensation is insufficient due to **actuator saturation**; c_j = 0 outside the prediction horizon n_c → pure H∞ feasibility.

#### 3.5.2. Robust fault estimation and control (2108-2180+)
- Both estimator and robust PDC designed for the **unconstrained** case first; c_j = 0. Constrained handling follows **Kouvaritakis & Cannon (2016)**: constraints imposed by building a set of states where the robust-PDC + fault-compensation law stays feasible, and by computing c_k that enlarges the feasible state set.
- Fault estimate via **direct algebraic inversion** (Gillijns & De Moor 2007): build H(h_k) [formula-not-decoded], multiply system eq. [3.81] by H and extract f̂_a,k [formula-not-decoded]; error ε_f,k [formula-not-decoded].
- **Subtlety/caveat (honest limitation in text)**: f̂ requires H(h_k) to exist, i.e. every convex combination of B_i full rank — and H(h_k) is generally NOT the convex combination of (B_i)^+; no standard check in control literature.
- **Theorem 3.2** (proof Witczak et al. 2015b): equivalence — (a) all convex combinations of B_1..B_M full rank ⇔ (b) B_M full row rank AND a big ((M−1)Mn)-square block matrix [formula-not-decoded] is a **block P-matrix** (Kolodziejczak & Szulc 1999) w.r.t. a given partition. Gives the verifiable rank test.
- Causality: f̂_a,k needs x_{f,k+1} (future state) → the controller actually uses **f̂_a,k−1**; lumped uncertainty v_k ∈ l2 contains both w_k and ε_f,k with bounds [formula-not-decoded].
- **Theorem 3.3**: for attenuation level μ > 0 on x_{f,k}, H∞ PDC design solvable iff ∃ U, N_i, P_i ≻ 0 with LMI [3.99] [formula-not-decoded], N_j = K_j U (change-of-variables). Proof Witczak et al. 2015b.
- **Lemma 3.1**: relaxes [3.99] into tractable effective-LMI form (two sufficient conditions [formula-not-decoded]).
- PDC synthesis ends: solve relaxed LMIs [3.101]–[3.102] for U, N_j, P_i, then K_j = N_j U^{-1} [formula-not-decoded].

#### 3.5.3. Derivation of a robust invariant set (2185-2195)
- Need a **robust invariant set** to keep desired behavior under faults+disturbance (Kouvaritakis & Cannon 2016).
- Boundedness ladder: **quadratic boundedness (QB)** (Pazera & Witczak 2019) → **extended non-quadratic boundedness (EQNB)** (Zou & Li 2011). QB results force P(h_k) = P common quadratic matrix; EQNB drops that constraint (affine P(h_k) = Σ h_i P_i). Derivations: Witczak et al. 2015b.
- Robust invariant set described by **ellipsoidal bounding** [formula-not-decoded] = inner approximation of the exact maximal invariant set (Gilbert & Tan 1991); conservative (smaller) but computationally tractable online.

#### 3.5.4. Efficient predictive FTC (2197-2264)
- Gap in 3.5.3 scheme: fault compensation via changing faulty-actuator control does **not account for saturation of all actuators**. Strategy: when the faulty actuator saturates, change the **remaining actuators'** strategy to *enlarge* the robust invariant set and restore feasibility.
- Uses **Kouvaritakis–Cannon efficient predictive control**, extended to external disturbances (robust version). Prediction variables [3.105]: z_k = [x_f,k^T, ω̄_k^T]^T, ω̄_k = {ω_k, ω̄_k} free-motion sequence parameterized over horizon [formula-not-decoded].
- Existence: invariant set E_z exists if E_{x_f} exists for [3.105]; invariant set definition [formula-not-decoded]. Stability: A(h_k)−B(h_k)K(h_k) stable ⇒ nominal (w̄_k = 0) stable; w̄_k ≠ 0 stability via LMI condition [3.106] with α > 0, P_i ≻ 0.
- Input constraints handled by **rescaling ω_k** (replace ω_k by c_k-scaled version [formula-not-decoded]); constraint LMIs built [formula-not-decoded].
- **Set maximization**: minimize Σ tr(P_i) subject to [3.106] (maximizes E_{x_f} size) [3.110].
- **c_k computation** (Kouvaritakis & Cannon algorithm): minimization [3.111]→[3.113] using block partitions P1,1, P1,2, P2,2 of P(h_k) conformal to z_k split [formula-not-decoded].
- Scheme summary (algorithm box):
  - Offline: 1) for μ > 0 design K(h_k) via [3.100]; 2) compute invariant set via [3.110] under [3.106] LMIs.
  - Online for each k: 1) f̂_a,k−1 from [3.90]; 2) solve optimization [3.113]; 3) apply first element of ω_k, i.e. c_k.
- Figure 3.2: robust predictive FTC scheme block diagram [image not decoded].

### 3.6. Illustrative examples (2266-2346) — benchmark: twin-rotor system (TRS)
#### 3.6.1. Sensor and actuator fault estimation example (2268-2322)
- Plant: **twin-rotor system (TRS)** (Pazera & Witczak 2019; Pazera et al. 2020b), nonlinear model converted to TS form via Rotondo et al. (2015) automated method.
- States: ω_v, ω_h = rotational velocities, Ω_v, Ω_h = angular velocities of main/tail rotors; beam pitch θ_v and yaw θ_h; inputs u_v, u_h = main/tail DC motor voltages, range **(−1, 1)**. [formula-not-decoded for full state/input vectors]
- Simultaneous constant-bias fault scenario (exact values from text, [formula-not-decoded] equations):
  - actuator fault f_a,1,k: **decreases first actuator performance by 10%**; f_a,2,k: **increases second actuator performance by 10%** (full actuator-fault distribution B_f);
  - sensor faults: f_s,1,k = **negative bias −2.5** on tail-rotor angular velocity Ω_h measurement; f_s,2,k = **positive bias +1.6** on main-rotor Ω_v measurement; sensor distribution C_f = extracted rows of C.
- Validation results (Figs 3.3–3.7, qualitative): TS-scheme estimates track nonlinear-model reference with good state+fault precision; estimates track real faults despite measurement uncertainties; ellipsoidal **uncertainty intervals shown as black dashed bands**; states reconstructed properly under simultaneous actuator malfunctions + wrong-signed sensor readings. [images not decoded; no numeric error metrics given]
#### 3.6.2. Fault-tolerant control example (2324-2346)
- Same TRS, TS form via de Oca et al. (2012) (LPV FTC for 2-DOF helicopter method); actuator-fault scenario for f_a,1,k / f_a,2,k of main/tail rotors [formula-not-decoded].
- Results (Figs 3.8–3.9, qualitative): with FTC (blue) vs without FTC (red) on main/tail rotor angular positions; fault estimates track real faults despite exogenous disturbances + high nonlinearity-induced modeling errors; **non-FTC scheme cannot control rotor positions under these actuator malfunctions; FTC succeeds with minor overshoots**. Control signals u1, u2 in Fig 3.9. No numeric metrics reported.

### 3.7. Conclusion (2348-2350)
- Chapter's through-line: neural + TS fuzzy models combined with classical observer design for sensor/actuator FDI + estimation; robustness via **H∞ + quadratic boundedness**; results feed a **predictive FTC** method; demonstrated on TRS.

### 3.8. Acknowledgment (2352-2354)
- National Science Centre, Poland, Grant UMO-2017/27/B/ST7/00620.

### 3.9. References (2356-2417) — load-bearing sources
- Core method lineage: Witczak et al. 2017 (Neurocomputing, NN state+actuator FE w/ unknown-input decoupling → Thm 3.1); Pazera et al. 2020b (Sensors, TS simultaneous actuator+sensor FE on TRS → descriptor observer + Thm QB-boundedness); Pazera & Witczak 2019 (IEEE Access, nonlinear QB simultaneous FE baseline); Witczak et al. 2015b (Witczak P. et al., robust predictive FTC for TS, block P-matrix test + predictive scheme); Witczak & Puig 2013 (Int. J. Control, integrated FTC on TRS); Abbas & Werner 2008 (neural → polytopic quasi-LPV); Kwiatkowski et al. 2006 (automated affine LPV generation); Rotondo et al. 2015 (automated TS vs quasi-LPV generation comparison); Kouvaritakis & Cannon 2016 (MPC book: efficient predictive MPC, invariant sets, c_k); Gillijns & De Moor 2007 (UIO minimum-variance input/state estimation); Zou & Li 2011 (EQNB); Gilbert & Tan 1991 (maximal output admissible sets); Kolodziejczak & Szulc 1999 (convex combinations of matrices full-rank characterization); de Oca et al. 2012 (LPV FTC 2-DOF helicopter); Ichalal et al. 2012/2018 (TS FTC + unmeasurable premises); Chadli & Karimi 2013 (UIO for TS); Tanaka & Wang 2001 (LMI fuzzy control); Takagi & Sugeno 1985; Zou/Li; Witczak 2007/2014 monographs.
- NOTE on this chapter's benchmark: TRS only (no LoLiMobots/robotic platform in Ch3; that material belongs elsewhere — Ch4 "Model Predictive Control Methods" by Patan starts at line 2419/2427).
- Chapter author attribution: Witczak/Pazera/Kukurowski/Mrugalski (per parent map; author block lines OCR-dropped — [OCR?]).

## Puig Vol2 Ch4 — Model Predictive Control Methods (source 2427-2824)

Chapter heading (line 2421): **Model Predictive Control Methods**; author Krzysztof Patan (Univ. Zielona Góra). Chapter title itself sits just before the 2427 range start; 2427 opens §4.1. CAUTION: essentially every equation in this chapter is [formula-not-decoded] — only formula numbers cited by the prose are recorded; nothing reconstructed.

### 4.1. Introduction (2427-2440)
- Four MPC generations: (1) LQR (early 1960s) — rejected by process industry (nonlinear plants, no constraints, weak optimal-control knowledge); (2) late 1970s-80s: MAC (Richalet 1978, impulse-response model), DMC (Cutler–Ramaker 1980, step-response), QDMC (Garcia–Morshedi 1986, QP under constraints); adaptive branch: MVC (Åström 1970, horizon=1), GVM for non-minimum-phase, PBSTC (Peterka 1984), GPC (Clarke 1987, discrete differential-equation model) — GPC lineage still dominant; (3) constraint priorities + multi-objective, SMOC (Marquis–Broustail 1988, state-space); (4) nonlinear MPC (Bemporad–Morari 1999) — stability/robustness become crucial, far harder than linear
- Robust-control lineage (all linear): Zames 1963, Kalman 1964; LQG margins (Doyle 1978), IQC (Safonov–Athans 1977), singular-value robustness (Safonov 2012), μ-synthesis (Doyle 2016), H∞ (Zames 1981; Doyle 1989); nonlinear robustness still open
- Chapter scope: two ANN-based robust MPC schemes — robust **nonlinear** MPC (optimization as NLP) and robust **approximate** MPC (optimization as QP); both tested on a pneumatic servomechanism

### 4.2. Idea of MPC (2441-2483)
- MPC = finite-horizon open-loop optimal control re-solved every sample; three common elements: (1) prediction model, (2) cost function, (3) deriving control sequence
- Receding-horizon mechanics (Fig 4.1): predict over N2 from outputs up to k + past inputs + future moves; optimize Nu-length move sequence; **apply only first move**, reject the rest; re-plan at k+1
- GPC criterion [4.10] [formula-not-decoded]: penalize (ŷ(k+i) − y_r(k+i)) over i=N1..N2 plus ρ·Δu(k+i−1); N1 min prediction horizon, N2 prediction horizon, Nu control horizon, ρ move penalty; state-space variant penalizes x_r vs x̂
- Constraint taxonomy [4.3]-[4.5] all [formula-not-decoded]: (a) control moves; (b) process variable v over horizon Nv with limits v_l ≤ v ≤ v_u; (c) terminal constraint on tracking error e = y_r − ŷ (state-space: x_r − x̂) over horizon Nc
- Constraints complicate the optimization; linear MPC mature (Bemporad–Morari, Mayne surveys); open nonlinear problems: modeling, state estimation, robustness, fault-tolerant control

### 4.3. Robustness of MPC (2484-2519)
- Uncertainty sources (Skogestad–Postlethwaite): (1) parametric = structured (structure known, parameters uncertain; design often boils down to H∞), (2) neglected/unmodeled dynamics (represented in frequency domain as multiplicative uncertainty), (3) lumped = unstructured (fusion of both into one perturbation of chosen structure)
- These descriptions insufficient for nonlinear processes; three nonlinear-appropriate routes:
- LPV/polytopic embedding: nonlinear system [4.5] as LTV set with [A(k) B(k)] ∈ Ω = convex hull of r extreme models [4.6]; r ≈ number of operating points; finite r → polytope ("polytopic uncertainty") — quite conservative for nonlinear systems (Bemporad–Morari)
- Global uncertainty [4.8] [formula-not-decoded]: output = f(nominal) + w(k), w(k) ∈ W compact with known bounds; w(k) may be a function of past inputs/outputs; key fact: bounded process variables ⇒ bounded global uncertainty (Camacho–Bordons; Limon 2005)
- Set invariance (Blanchini 1999): Ω robust invariant iff a feedback u = h(x(k)) makes Ω robust positively invariant for the system [4.9]; trajectory in (or entering) Ω stays in Ω; constraint satisfaction guaranteed for all time and all disturbances if initial state in a robust control invariant set — foundational for constrained MPC design

### 4.4. Neural-Network-Based Robust MPC (2520-2539)
- Criterion [4.10] = GPC cost (increments Δu, penalty ρ, horizons N1/N2/Nu); minimized each sample → future move sequence u(k..k+Nu−1) [4.11], constraints [4.12]
- Assumes Nu < N2; only first Nu moves free, control constant afterward; practical advice: keep Nu small (1 or 2)
- ŷ = minimum-variance i-step-ahead prediction; predictor built two ways: (i) successive recursion of one-step nonlinear model → **NMPC** (iterative minimization, NLP); (ii) instantaneous linearization → **AMPC** (Nørgaard 1996; unique direct solution; drawback: linearized model only locally valid in some operating regimes)

#### 4.4.1. Neural Network Models (2541-2590)
- Process [4.13]: y(k) = f(y(k−1)…y(k−na), u(k−1)…u(k−nb)), f unknown nonlinear; 1-step NN predictor [4.14] with f̂; i-step by recursion [4.15]; past *measurements* available only up to k, so predicted outputs substituted beyond that [4.16]
- Workhorse: multilayer perceptron **with external dynamics** (Fig 4.2) = tapped delay lines + feedforward net; universal approximation (Hornik 1989); trained with serial-parallel identification model (Narendra–Parthasarathy 1990) so standard FFN training applies (backprop Rumelhart 1986; LM Hagan–Menhaj 1994)
- For i > na the model feeds its own predicted outputs back as inputs (eq [4.17]) → structure "something between feedforward and recurrent" — crucial for MPC i-step prediction
- **Model error modeling** (Reinelt 2002) for robust identification: identify error model from prediction residuals — [4.18] estimates w(k) given nominal model [4.14] + measurements; training data {u(i), w(i)} gathered e.g. by evaluating a predictive controller that uses the nominal model; enrich data by simulating uncertainty sources (e.g. parametric)
- Error model structure [4.19]: ŵ(k) = g(ŵ past nc lags, u past nd lags), g unknown nonlinear; **robust model [4.20]** = nominal + error model combined
- If error model not falsified by data → statistical confidence bounds: wu(k), wl(k) around ŵ ± t_α·σ [formula-not-decoded], t_α = N(0,1) tabulated value at 1−α, σ = error-model std dev; uncertainty-region center ŷ(k)+ŵ(k) ≈ y(k)

#### 4.4.2. Nonlinear MPC (2591-2606)
- NN predictor ⇒ outputs nonlinear in controls ⇒ constrained NLP; iteration [4.23]: u(i+1) = u(i) + η(i)h(i) (step size × search direction)
- Algorithm requirements: fast convergence, real-time, numerical robustness; gradient methods too slow, metaheuristics too complex → **second-order methods** chosen; h(i) from Hessian H(i) + gradient g(i) [4.24]-[4.25]; λ(i)I added to H to force positive definiteness

#### 4.4.3. Approximate MPC (2607-2632)
- **Instantaneous linearization** (Nørgaard 1996): at each sampling time k=τ Taylor-expand neural model around current operating point φ(τ), drop nonlinear terms → linear model [4.26]-[4.28]; φ(k) = [y(k−1)…y(k−na), u(k−1)…u(k−nb)]
- Interpretation: ARX model + disturbance that depends on the operating point; then MPC works exactly like GPC (Diophantine equations)
- Prediction [4.29]: y_l = G·Δu + f, G = step-response matrix, f = free response; y_l and Δu stacked vectors over N2/Nu
- QP; unconstrained solution [4.30]: Δu = H⁻¹g with H = GᵀG + λI, g = (y_r − f)ᵀG; applied control = first move [4.31]-[4.32]

#### 4.4.4. Robust Nonlinear MPC (2633-2649)
- Robustness route: keep **nominal cost [4.10]** but inflate the **output constraints** by the uncertainty bounds [4.21]-[4.22] → two-sided tightened output constraints [4.32]/[4.33] for i ∈ [N1,N2] (Patan–Witczak 2014)
- Constraints handled by **penalty-cost** reformulation: penalty term [4.34] with switch S(x)=1 if x>0 else 0 (activates only violated/active constraints at current iterate) → unconstrained problem [4.35]
- Algorithm details: Patan & Witczak 2014; Patan 2019

#### 4.4.5. Robust Approximate MPC (2651-2696)
- Error model [4.19] also linearized each sample → linear error model [4.36]/[4.37]: c_i feedback, d_j feedforward parameters; ε(k) integrated white noise
- Error-model prediction [4.38] with step-response matrix G_w and free response f_w; **superposition** (per robust model [4.20]): nominal prediction [4.29] + error prediction [4.38] → robust prediction ȳ_l [4.39]
- Cost [4.10] modified: use ȳ_l in place of ŷ → [4.40]; problem stays QP [4.30]-style with H = G̃ᵀG̃ + ρI, g = (y_r − f̃)ᵀG̃
- Constraint stack: actuator limits u_l/u_u; robust-model output bounds y_l/y_u; plus robust (tightened) constraints — all collapsed to augmented matrix inequality [formula-not-decoded], S = lower-triangular unit matrix (cumulative-sum operator on Δu), 1 ∈ R^Nu; final RAMPC form includes extra moves Δu_c over remaining prediction horizon; details Patan 2018/2019

### 4.5. Robust Control of a Pneumatic Servo (2697-2706)
- Benchmark: pneumatic position servo (Nørgaard et al. 2000) — double-acting cylinder lifting inertial mass m, compressed air via four adjustable flow-control valves; S1+S4 open ⇒ u ≥ 0 (piston right), S2+S3 open ⇒ u < 0 (left); SISO: valve signal → piston position (Fig 4.3)
- Nonlinearities: nonlinear friction, deadband from stiction, dead time from air compressibility; data sheet in Nørgaard 1996 / Patan 2018

#### 4.5.1. Robust Nonlinear NN-based MPC — RNMPC case (2707-2751)
- Servo poorly damped + integrator action ⇒ open-loop data collection impractical → training data recorded in **closed loop with P controller, gain 10**; random-step references; Gaussian noise added to output
- Fundamental (nominal) model: na = nb = 4, one hidden layer 8 tanh units + linear output neuron; Levenberg–Marquardt training; Fig 4.4 shows close offline fit
- Error model via model error modeling: NN again; data logged while predictive controller (N2=10, Nu=2, ρ=0.003) runs the servo, with extra simulated **parametric gain uncertainty**; best error model: 1 hidden layer, 10 tanh neurons, nc = 2, nd = 10
- Key observation: offline-accurate fundamental model breaks down under real-world conditions (large process-vs-model gap, Fig 4.5 black vs blue); trained error model closes most of it (red dotted = robust model)
- RNMPC deployment settings: N1 = 1, N2 = 10, Nu = 2, ρ = 0.003; control bounds u_l = −4, u_u = 4
- Evaluation protocol: 3 reference profiles (random steps, ramp, harmonic) × 3 conditions (nominal / parametric gain uncertainty / white output noise); metric = sum of squared errors
- **Table 4.1 (SSE; NMPC vs RNMPC — RNMPC wins every cell):**
  - Random steps: nominal 2.4019 vs 2.2545; param var 2.2632 vs 2.1151; noise 2.3848 vs 2.2612
  - Ramp signal: nominal 0.1977 vs 0.1599; param var 0.2751 vs 0.2364; noise 0.2277 vs 0.1908
  - Harmonic signals: nominal 0.128 vs 0.0856; param var 0.1463 vs 0.0997; noise 0.1398 vs 0.097
- vs classical P controller (Figs 4.6-4.8, normal conditions): RNMPC cuts control time and — crucially — kills steady-state tracking error, which P cannot

#### 4.5.2. Robust Approximate NN-based MPC — RAMPC case (2752-2759)
- Training data in closed loop with **PI controller**; reference = harmonic mix in [0.1, 0.5] Hz + ramps + random unit steps, levels covering piston positions (−0.245, 0.245); 5000 samples
- Fundamental model: 1 hidden layer, 5 tanh neurons + linear output; na = 4, nb = 2; LM off-line, 200 steps; validation on random steps: SSE = 0.0057, mean error/sample = 1.43e-6
- Error model data from running **AMPC** (N2=10, Nu=2, ρ=0.001; u bounds ±4; output bounds ±0.245) with input **and** output multiplicative uncertainty (Patan 2018); best error model: 9 tanh hidden units, nc = 2, nd = 5
- RAMPC uses same parameters/constraints as error-model training; Table 4.2 SSE, PI vs RAMPC (RAMPC wins all):
  - Normal operation: 0.6403 vs 0.1616
  - Input uncertainty: 0.6139 vs 0.1822
  - Output uncertainty: 0.6166 vs 0.4053
  - Uncertainty in viscous coefficient: 0.6329 vs 0.2838
  - Uncertainty in load mass: 0.6174 vs 0.2208
  - Uncertainty in cylinder volume: 0.6208 vs 0.20

### 4.6. Conclusion (2760-2774)
- Core idea: NN nominal model + NN **error model** to estimate prediction-model uncertainty; nonlinearity handled by both networks
- RNMPC (NLP): high-quality nonlinear robust predictions, but optimization hard to solve
- RAMPC (QP): per-sample linearization simplifies optimization, but predictions less accurate
- Pneumatic servo results: NN-based robust MPC deemed a very efficient technique
- §4.7 References (2775-2820): Patan solo monographs anchor the method — Patan 2008 (Springer, neural modeling/fault diagnosis), Patan 2018 (ISA Trans 72:56-65, two-stage NN modeling for robust MPC), Patan 2019 (Springer-Nature, Robust and Fault-Tolerant Control: Neural-Network-Based Solutions), Patan–Witczak 2014 (ISIC, robust NN-MPC)

## Puig Vol2 Ch5 — Nonlinear Modeling for Fault-tolerant Control (source 2825-3696)
Authors: Silvio SIMANI & Carlo CASTALDI (Univ. of Udine) (per task assignment; corroborated by self-citation cluster Beghelli-Castaldi-Simani in refs). Chapter goal: move from fault diagnosis to fault tolerance; FTC applied to dynamic processes via signal-correction principle (baseline controller NOT modified; its inputs/outputs compensated by estimated faults). Passive vs active FTC compared; reconfiguration for stability.

### 5.1 Introduction (2825-2878)
- Model/data-driven FDI = 40+ yrs open research; robustness via disturbance/model-error minimization on residuals, but those techniques assume ideal systems or special uncertainty structure.
- Frequency-domain robustness lineage: Patton et al. 1986 first frequency-domain FDI design (freq-domain optimal observer → transfer-matrix factorization); Ding & Frank 1990 extensions; Gertler 1998 factorization-based H∞; advanced H∞ via Algebraic Riccati Equations; H∞/μ robust estimator synthesis (Chen & Patton 1999), extended to time-variant/nonlinear.
- H∞ residual generation objective [5.1]: max‖Q(s)Gf(s)‖∞ / min‖Q(s)Gd(s)‖∞ over frequency band (Q=pre-filter, Gf residual←fault, Gd residual←disturbance); design = compromise disturbance robustness vs fault sensitivity. [formula-not-decoded]
- Caveat: ‖QGf‖∞ can be SMALLER than ‖QGd‖∞ in some bands even when ratio maximized; Gd(s) defined only for disturbances → robustness vs MODEL ERRORS unsolved; only remedy = compute residual bound + adaptive threshold. μ-synthesis+H∞ vs model errors still early stage = future research.
- Data-driven freq-domain alternative: EIV (errors-in-variables) identification + dynamic Frisch scheme (Beghelli et al. 1994a, 1997) → accurate estimates of Q(s), Gf(s), Gd(s) from I/O data with white uncorrelated/correlated noise; uniquely determines noise characteristics AND process transfer matrices; time- vs freq-domain comparison Beghelli et al. 1994b.
- Adaptive observers (Fig 5.1): estimate & compensate parameter variations; valid for linear systems with parametric variations if stability/convergence conditions hold (Patton et al. 1989); drawback = complexity. Alternative (Chen & Patton 1999): estimate BIAS term in residual due to modeling errors and compensate adaptively — avoids estimating modeling errors themselves.
- Online parameter estimates Â(t), B̂(t) (methods of Söderström & Stoica 1987, Ljung 1999) + x̂(t) generate adaptive residuals; observer parameter relations [5.2] [formula-not-decoded]; adaptive residual generation = hybrid of observer-based + identification-based FDI (complementary advantages).
- KEY ADAPTIVITY LIMIT: adaptation compensates fault effects AND modeling errors/parameter variations → incipient faults almost impossible to detect (abrupt acceptable). Workaround: treat fault as slow-varying parameter estimated alongside; if parameters & faults vary at different rates use TWO filters with different gains.

### 5.1.1 Joint fault diagnosis and control (2879-2908)
- Conventional FTC = separate modules (modeling/identification, controller design, FDI, reconfiguration); FDI↔controller linked only via reconfiguration module → interactions among identification/control/FDI neglected = fundamental weakness; need joint study of interactions.
- Fault IDENTIFICATION is the top diagnosis task: once fault magnitude estimated, detection+isolation easy; but under-researched. Parameter-identification/parity/observer methods cannot directly identify sensor & actuator faults.
- Kalman filter for statistical testing & fault ID (Patton et al. 1989) — high computational demand. Fault ID via system inversion problem (Simani et al. 1998, 1999c; Chen & Patton 1999).
- Fig 5.2 FTC scheme: fault identification = estimate nonlinear map residual→fault magnitude (robust residuals contain only fault info); approximated by neural networks OR inversion of residual-fault transfer matrix.
- Linearization around operating point fails for high nonlinearity + wide dynamic range; many linearized models → many FDI schemes = impractical; study direct nonlinear residual generation: nonlinear observers (Frank et al. 2000; De Persis & Isidori 2001; Chen & Patton 1999), nonlinear UIO incl. adaptive & sliding-mode observers; bilinear-system observers if nonlinearity class restricted.
- When explicit math models impossible → universal approximate models: NN (functional approximation power, Schilling et al. 2001; early use = classifiers for steady-state, later residual generators/modeling for FDI); fuzzy models as residual classifiers (Sneider & Frank 1996) and parametric models (Ying 1994) → fuzzy observers with fuzzy fusion of local observer outputs/residuals; global-observer stability issue, LMI/Lyapunov solution (Chen & Patton 1999) quite conservative.
- Hybrid models: composition of local affine (PWA) models selected by operating conditions (Antsaklis 1998); identification + optimal selection of local affine models from noisy measurement sequences (Rovatti et al. 1998; Simani et al. 1999a, 1999b; Fantuzzi et al. 2002); application to model-based FDI an open area.

### 5.1.2 Nonlinear adaptive fault estimators (2909-~3193, first part)
- NLGA (De Persis & Isidori 2001) achieved structural decoupling of CRITICAL disturbances/modeling errors; this section improves robustness vs NON-CRITICAL (undecoupled) disturbances/model errors while maximizing fault effect on residual.
- Restrict to scalar components of x̄1-subsystem: decompose x̄1, ȳ1 into (x̄11 ∈ ℝ scalar, ȳ11 ∈ ℝ) + complement [5.3]-[5.4]; conditions [5.5]: h11(·) smooth map, h1c(·) invertible smooth map — satisfied for the considered dynamic processes → use scalar x̄11-subsystem [5.6] in place of x̄1. [formula-not-decoded]
- Gain tuning in [5.6] framework inadequate (non-critical disturbances not represented) → embed non-critical disturbance description into x̄11-subsystem [5.7]: x̄11 assumed directly measured (wlog); ν ∈ ℝ measurement noise on x̄11; ζ ∈ ℝ + scalar field e(·) = non-critical effects not in NLGA process model.
- Filter form [5.8] = generic scalar residual generator rf; designed residual generators are particular cases; gain kf tuned to min effects of ζ, ν while max effect of fault f on rf.
- Estimation error defined [5.9] → equivalent residual model [5.10] (state-error + residual dynamics) [formula-not-decoded].
- Mixed H−/H∞ approach applies for tuning kf (Chen & Patton 1999; Hou & Patton 1996): linearize [5.10] near steady-state working condition; cf. H∞ optimization of nonlinear UIO in aerospace in Amato et al. 2006.
#### 5.1.2 continued — H−/H∞ mixed optimization (2955-3074)
- Benchmark has SMALL excursions about trim values x̄10, x̄30, c0, ȳ10, ȳ20 → nonlinear residual generator robustness achieved; linearize [5.10] about steady state → [5.11] (matrices A1,C1 etc. [formula-not-decoded]).
- Observer formulation [5.14] preferred over filter form [5.8]; introduce estimation error x̃o → error dynamics [5.15]-[5.16]; linearized [5.16]; both filter [5.11] and observer [5.17] linearized models collapse to general form [5.18] with E1=[e11, 0]; Table 5.1 maps observer↔filter parameter relations [formula + image, not extracted].
- Scalar NLGA residual generators → mixed H−/H∞ yields simple closed-form analytical solution for gain kf = a highlighted contribution vs general MIMO H∞ machinery.
- Norms [5.19]: ‖G‖∞ = sup_ω σ̄(G(jω)), ‖G‖− = inf_ω σ(G(jω)) (max/min singular values; Zhou et al. 1996, Zhou & Doyle 1998).
- Trade-off statement [5.20]: for β>0, γ>0 define set K of gains k such that ‖G_rε‖∞ (disturbance→residual error) small < γ-type constraint AND ‖G_rf‖− (fault→residual) > β lower bound.
- Scalar SISO result: Grf(s) = m/(s − a + k); wlog m>0 ⇒ ‖Grf‖− = m/(k−a); ‖Grf‖− > β ⇒ k < a + m/β [5.22]-[5.28].
- If γ > 1: max feasible β respecting ‖Grε‖∞ < γ is βmax(γ) [5.34]-[5.35]; feasible gain set K = open interval for γ>1, β∈]0, βmax(γ)[ [5.36, formula-not-decoded].
- Performance-index maximization [5.37] (ratio β/γ) worked next [continues].
#### 5.1.2 cont. — optimal k + NLGA-AF adaptive fault estimator (3075-3193)
- Optimal-gain conditions [formula-not-decoded throughout]: from [5.23]; performance index J [5.40] maximized at max J [5.41] for k > (a + √(e²₁₁+a²)) region per [5.39]; scheme guarantees max J AND both constraints ‖Grε‖∞<γ, ‖Grf‖−>β when β ≥ m/√(e²₁₁+a²), which forces k < (a + √(e²₁₁+a²)); for γ>1 a suitable β always exists [5.33].
- Residual-gain design procedure (4 steps, based on [5.36]): 1) choose γ>1 → desired disturbance attenuation; 2) compute βmax(γ), choose β∈]0,βmax(γ)[ → desired fault sensitivity; 3) compute k [formula-not-decoded]; 4) apply fixed k to kf (filter form [5.8]) or ko (observer form [5.14]).
- Optimized NLGA generator is named NLGA Adaptive Filter (NLGA-AF); used for fault magnitude estimation on the dynamic processes.
- Motivation: basic NLGA residual scheme (De Persis & Isidori 2001) gives NO fault size estimation; reconstruction via successive derivatives of input/output (Kaboré et al. 2000; Kaboré & Wang 2001) is noise-sensitive → NLGA-AF = NLGA coordinate transformation + adaptive filtering to reconstruct fault magnitude.
- NLGA-AF solvability conditions = De Persis-Isidori fault detectability + 3 new constraints: (1) x̄1-subsystem independent of x̄3 states; (2) fault = STEP function of time → f constant to estimate; (3) ∃ scalar component x̄1s of x̄1 with matching output component ȳ1s = x̄1s and relation [5.43] with M1(t) ≠ 0 ∀t≥0; M1(t), M2(t) computable each instant from input/output measurements (form [5.44] = general diagnosed-system relation, presumably ȳ1s-dynamics = M1(t)f + M2(t)) [formula-not-decoded].
- Adaptive filter = least-squares with forgetting factor (Ioannou & Sun 1996): adaptation law [5.45]; output estimate + normalized estimation error ϵ(t) [5.46]; all variables scalar; λ>0 filter bandwidth parameter; β≥0 forgetting factor; N² = 1 + M̘1² normalization.
- Uses LOW-PASS filtered signals M̘1, M̘2, ȳ̘1s [5.47] (avoids raw derivative noise). Asymptotic link ϵ(t) ↔ (f − f̂(t)) [5.48].
- Stability proof (two Lyapunov steps, words): (a) auxiliary system y′ [5.49] with solution [5.50]; V = (y′−ȳ1s)²-type [5.51] pos-def radially unbounded, V̇ < 0 ∀y′≠ȳ1s ⇒ y′(t) → ȳ1s(t) globally asymptotically; via [5.50]→[5.53]→[5.54] ϵ(t) asymptotics. (b) W = (f̂−f)-type [5.55] pos-def radially unbounded; smoothness lets [5.48] asymptotic approximation enter Ẇ [5.56]: ∃t⋆>0 s.t. sign(Ẇ) settled ∀t≥t⋆; Ẇ negative definite ∀f̂≠f since M̘1 (low-pass of smooth non-null M1) ≠0 and N²=1+M̘1²>0 ⇒ W Lyapunov, f̂(t) → f GLOBALLY asymptotically.
### 5.1.3 Fuzzy fault-tolerant control (3194-3251)
- Goal: fuzzy description of the FTC + controller-model estimation via TS fuzzy models (Babuška 1998); fuzzy clustering partitions data into subsets with linear behavior → fuzzy logic × system identification blend; FMID toolbox (Fuzzy Modeling and IDentification) available in MATLAB (Babuška 2000). Submodel switching/scheduling = smooth state function via fuzzy sets.
- Two-step algorithm: (1) operating regions from data clustering = Gustafson-Kessel (GK) fuzzy clustering; (2) consequent-parameter estimation via identification algorithms generalizing least squares (Babuška 1998).
- TS model form [5.59]: rule i: yi = ai·x + bi; x(k) = regressor of delayed u,y samples; antecedent fuzzy sets μi from fuzzy partition matrix; consequents ai, bi estimated from data; integrated in FMID; when TS model used as PREDICTOR, consequents computed via Frisch scheme for EIV descriptions (Jens et al. 2012).
- Inverse-model control principle (Babuška 1998): for stable fuzzy systems with stable inverted dynamics, controller = fuzzy model inverse; ideal case → perfect tracking, zero steady-state error; practical modeling errors/disturbances handled by DIRECTLY identifying the inverse-model controller (fuzzy model predicts any behavior).
- Optimal-control variant: cost = desired-vs-controller output difference + stability penalty, stability constraints in the optimization → non-convex problem per sample = impractical; workaround = parameterized search at a higher level (Babuška 1998).
- Fuzzy inverse controller accounts for process nonlinearities incl. inherent saturation (level) constraints on control inputs & process variables; controls entire operating range.
- Process model discrete-time [5.60]-[5.61]: inputs x(k) = [y(k),…,y(k−n+1), u(k−1),…,u(k−n+1)]ᵀ + current u(k); output = prediction y(k+1); superscript (m) for process model (μ(m)ᵢ, x(m), a(m)ᵢ, b(m)ᵢ).
- Control objective: choose u(k) so y(k+1) = r(k+1) = reference; u(k) = f⁻¹(xc(k), r(k)); analytical f⁻¹ rarely available → identify inverse mapping u(k+1)=f⁻¹(x(c)(k), r(k)) as another TS prototype [5.63] (valid if controlled system stable); controller-model inputs x(c)(k) = [x(m)(k), r(k−1),…,r(k−n+1)]ᵀ + r(k); superscript (c) for μ(c)ᵢ, a(c)ᵢ, b(c)ᵢ.
- Fig 5.3 fuzzy controller principle: series connection controller ∘ inverse model ≈ identity [5.64] when ∃u(k) with r(k+1)=f(x(m)(k),u(k)); model errors/noise/disturbances → |r(k+1) − f(x(m)(k),u(k))| made arbitrarily small by tuning μ(c)ᵢ, number of clusters M, regressand a(c)ᵢ,b(c)ᵢ.
- Process fuzzy model runs recursive state prediction x(m)(k); controller state updated from x(m)(k) + r(k); apart from membership degrees, everything = matrix ops + linear interpolation → real-time feasible.
- Model-reality mismatch → reference-vs-output error; compensate by ONLINE adaptation of both process [5.61] and controller [5.63] models. Classical adaptive = consequents only (antecedents fixed); poor initial model → adapt membership params via nonlinear optimization (Babuška 1998); clustering can be repeated offline/online but short industrial sampling times forbid heavy computation → motivates §5.1.4 linear-model adaptive strategy.

### 5.1.4 Recursive adaptive control (3252-~3429, first part)
- Recursive implementation of the batch FRISCH scheme for dynamic EIV identification + recursive bias-compensating update; exponential FORGETTING factor added → compensates systematic errors of original method (Jens et al. 2012) → handles LINEAR TIME-VARYING (LTV) systems; feeds adaptive control design.
- Process G(z) = B(z⁻¹)/A(z⁻¹) [5.65]; unknown params ai, bi; orders na, nb fixed a priori (adaptive-control orientation); parameter vector θ [5.65], extended θ̄ with noise variances; difference eq. form [5.66] with extended regressor ψ̃(k) [formula-not-decoded].
- Frisch scheme estimates σu², σy² (input/output measurement error variances) + θ for LTI; batch form [5.70]: (Σψ − Σψ̃)·θ̄ = 0 with noise covariance Σψ̃ = diag(σy², σu²) and sample covariance Σψ over N samples.
- Core condition: find σu, σy s.t. (Σψ − Σψ̃) is singular positive semidefinite (RANK-ONE DEFICIENT) and overdetermined [5.70] solvable; θ̄ = solution.
- Residuals ε(k) [5.71]; sample auto-covariance rε(h,k) over N samples [5.72-5.74] (h = time shift).
- Recursivization: covariance-matrix update straightforward [5.75]; but auto-covariance rε(h,k) NOT recursively computable when 1 ≤ l ≤ k → approximation [5.76] introduced [continues].
#### 5.1.4 cont. — recursive Frisch + self-tuning PI (3314-3429)
- Recursive approximation [5.76]: at step k compute only residual ε(k, θ̄(k)) from stored ψ(k)+current θ̄(k) → auto-covariance recurses needing only ε(k+h, θ̄(k)) [5.77]; θ(0), Σψ̃(0), rε(0,h) initialized by batch Frisch (Jens et al. 2012).
- Forgetting-factor motivation: [5.75]/[5.77] numerically problematic for large k; forgetting = down-weight old data → avoids storing k AND reduces [5.76] approximation error; exponential-forgetting covariance/auto-covariance [5.78] with scaling ω(δ) (= k when no adaptation); recursion [5.79], 0<δ<1.
- Adaptive Frisch scheme 3 steps: 1) init [formula-not-decoded]; 2) each recursion compute σu, σy from rε(h,k); 3) each recursion determine θ̄(k) by solving [5.70] via [5.79] → θ(k) estimates at step k; implemented in MATLAB/Simulink (Bobál et al. 2005 Simulink toolbox).
- Self-tuning PI design (NOT fuzzy-based): second-order online model na=nb=n=2 [5.80] with params â1,â2,b̂1,b̂2 [5.81]; justification: literature linearizations of the benchmark (Odgaard et al. 2009; Sloth et al. 2011; Odgaard & Stoustrup 2012 — wind-turbine references) = 4th-order for 2 inputs/2 outputs; per output ≈ 2-in/1-out 2nd-order → one PI adaptive loop per output.
- PI law, forward Euler discretization (Franklin et al. 1998) [5.82]: e(k)=r(k)−y(k), Ts sampling; Kp & TI time-varying, recomputed from θ(k).
- Ziegler–Nichols-type tuning numbers: Kp = 0.6·KPu, TI = 0.5·Tu (Bobál et al. 2005); KPu = critical gain, Tu = critical period, both computed each k from â2,â1,b̂2,b̂1 via relations [5.83]/[5.84] involving auxiliary d (formulas not decoded; critical values depend on choice of d).
- Alternative: discrete pole placement; closed-loop GR = QP; characteristic polynomial D = A·P + B·Q depends on Kp,TI; D choices: 2nd-order response specs / dead-beat / quadratic optimal; for the process (limited overshoot required): D form (Bobál et al. 1995) with real pole z1=α (0≤α<1) + conjugates z2,3=α±jω (α²+ω²<1); Kp,TI solved from LINEAR equation system in b1,b2,a1,a2 + desired poles.
- Identified-model stability caveat: identification assumes stable data-generating system; finite-data estimates NOT guaranteed stable even if true system stable → stability constraints can be included in identification (Chui & Maciejowski 1996).
- Unstable identified model: include gain/phase margin specs (Ho & Xu 1998), w-plane design; [5.80]→[5.86] equivalent FOPDT: gain k, unstable/dominant lag τo, effective delay L (Skogestad 2003 "all-approximation" neglecting fast stable modes); tuning [5.87] yields margins (Am, φm); achieved margins typically within 5% max error of specified [NUMBER].
- Non-minimum phase / delay: [5.83]-[5.84] self-tuning performs poorly; Skogestad (2003) approximations: inverse-response constant Tᵒᵢⁿᵛ (negative numerator zero) ≈ extra delay [5.88]; small lag τs ≈ extra delay [5.89]; effective L = Tᵒᵢⁿᵛ + τs (+ Ts/2 D/A-converter contribution in digital) → stable FOPDT k·e^(−sL)/(τo s+1) [formulas not decoded]; PI tuning for FOPDT: single knob τc (desired closed-loop 1st-order response time): small τc fast, large τc robust; rule of thumb τc = L (Skogestad 2003).
- Sampling-time remark: design rules look Ts-dependent (small Ts → aggressive action) but identification/retuning rate may be SLOWER than data sampling — model-reality mismatch dynamics slower than measurement-error disturbances → control Ts can be larger than data Ts.
- PI not P: pure proportional adaptive control → no asymptotic tracking/disturbance rejection at t→∞; PI + actuator saturation → integral windup (overshoot/oscillation) → anti-windup via conditional integration (Visioli 2003; built into Simulink PI block).
- Bumpless transfer at controller switching: exact plant unknown at switching → use slow-co-decomposition method (Cheong & Safonov 2008; Jun & Safonov 1999): re-initialize PI mode states at switching instants → continuous controller output, no fast transient bumps.
### 5.1.5 Sustainable control (3430-3443)
- Motivation: MW-scale power plants expensive → availability/reliability maximize energy production; offshore O&M = key energy-cost factor; capital+installation = energy "fixed cost"; O&M = "variable cost" raising energy cost up to ~30% [NUMBER].
- Industrial systems more complex/expensive, less tolerance for degradation/productivity loss/safety hazards → FDD/FDI + fault tolerance to minimize degradation and avoid danger; computerized control/networks enable real-time monitoring but add challenges.
- FTC classification (Mahmoud et al. 2003): PFTC = FIXED controller robust against a class of presumed faults; AFTC = reacts actively by RECONFIGURING control actions to keep stability + acceptable performance; PFTC vs AFTC compared on safety-critical benchmark in Odgaard et al. 2013 (= simple wind turbine benchmark; dynamics nonlinear/unsteady, complicated actuator inputs) → "sustainable" control challenging (Odgaard & Stoustrup 2013).
- Faults that change ACTUATOR DYNAMICS cannot be accommodated by signal correction alone → must be in controller design; component-change fault = most likely, destabilizes reference controller; lost output measurement → controller falls back to noisier controlled output → reconfiguration needed.
### 5.2 Fault-tolerant control strategies (3444-3512)
- Comparison protocol: AFTC vs PFTC controllers must be derived by the SAME procedure fault-free, so performance/complexity differences attribute only to the fault-tolerance approach; controllers must handle parameter-varying behavior along nominal trajectory (nonlinearities) → LPV or fuzzy design (Bianchi et al. 2007; Galdi et al. 2008).
- Structure difference (Figs 5.4 AFTC / 5.5 PFTC): ONLY AFTC carries an FDD module feeding fault info f to the controller; FDD estimates unknown input (fault) → enables reconfiguration; FDD ALSO improves fault-free performance (compensates modeling errors/uncertainty/disturbance).
- PFTC: no FDD; optimized fault-free + graceful degradation specs in faulty cases; vs plain robust control: guarantees same performance with NO risk of false FDI or reconfiguration.
- Design requirements: output feedback (partial state), noise-aware, nonlinear or LPV-suitable; modern = LPV/fuzzy/neural with fault-tolerance added (guaranteed stability/performance vs parameter variation).
- AFTC scheduling: FDD-estimated LPV/fuzzy structure parameters schedule the controllers (Sloth et al. 2010; Sami & Patton 2012). PFTC: modify LPV/fuzzy designs for parametric uncertainty (Puig 2010; Rodrigues et al. 2007) or nominal-performance-preserving approach (Niemann & Stoustrup 2005); optimization = max disturbance attenuation s.t. constraints, formulated as LMIs (Chen et al. 1997).
### 5.2.1 Fault tolerance and compensation (3470-3512)
- Restates: fault estimation = most important diagnosis phase (detection+isolation easy once estimated); under-researched; parameter-ID/parity/observer methods can't directly identify sensor/actuator faults; KF statistical testing (Patton et al. 1989) costly; system-inversion fault ID applied to POWER SYSTEMS (Simani & Patton 2002; Simani & Fantuzzi 2002).
- Fig 5.6 fault estimation strategy: identify nonlinear map residual→fault magnitude (robust residuals contain only fault info, independent of the system); nonlinear function approx via data-driven or model-based approaches.
- NLGA-based purely nonlinear FDD (De Persis & Isidori 2001) does detection+isolation+size estimation via disturbance-decoupled adaptive nonlinear filters (NLGA-AF); original NLGA residual scheme cannot estimate fault size; results: enhanced control requirements, ASYMPTOTIC fault accommodation, control objective recovery (fault-free + faulty).
- Fig 5.7 integrated AFTC logic scheme signals: ur reference set-point; u actuated inputs; u* unmeasurable inputs; uc controlled inputs; un control signals; y controlled outputs; y* unmeasurable outputs; f generic equivalent faults; f̂ estimated faults.
- Operation: FDD fed by (uc,y) → estimates f̂ of actuator fault f → INJECTED into control loop for compensation → controller exactly tracks ur (itself possibly from compensation block); f̂ feedback improves f identification (reduces estimation error/model-mismatch bias).
- Caveat: asymptotic accommodation + objective recovery verified in SIMULATION in this book; real plants need further study. Advantage: existing (logic-based switching) controller structure unmodified; reconfiguration = extra loop on online fault estimate; applied to several dynamic processes with faults+disturbance+noise+modeling errors.
### 5.3 Fault diagnosis and tolerant control (3513-3577)
- Fault model [5.92] (discrete time, Fig 5.8): u*(k), y*(k) actual unmeasurable variables; sensor acquisitions u(k), y(k) = u*+fu+noise? additive equivalents: u = u* + fu (+noise), y = y* + fy (+noise); fu(k), fy(k) nonzero ONLY under fault; single additive representation covers actuator, system AND sensor faults.
- Residual generation (Fig 5.9): data-driven or model-based filters on u(k), y(k) directly OUTPUT fault estimates: r(k) = f̂(k) = the equivalent faults fu, fy of [5.92] (residuals ARE fault reconstructions).
- Detection logic: evaluation function F(·) on residual (identity, or moving average / statistical ops) → threshold test [5.95]: fault i detected when |rei| outside ± thresholds; rei = random variable, fault-free mean r̄ei & variance σ²ri estimated from N fault-free samples [5.96].
- TOLERANCE PARAMETER δ ≥ 2 [NUMBER]: tunes fault-free vs faulty separation; δ trades false alarm rate vs detection probability; common choice = three-sigma rule, else optimize by simulation.
- Isolation = bank of r+m MISO (multi-input single-output) fault estimators, one per fault (r inputs + m outputs); i-th estimator reconstructs f̂i(k)=ri(k) driven only by the u,y channels SENSITIVE to fault fi (selector blocks); multiple simultaneous faults NOT isolable with this configuration.
- FMEA (Stamatis 2003) must run BEFORE estimator design: for each fault mode identify most sensitive measurements → defines estimator IO configuration & dynamic fault↔IO relations.
- Table 5.2 fault signature/sensitivity matrix as bullets [1=residual sensitive to fault, 0=not]:
  - rows r1..r(r+m) × cols u1..ur, y1..yr: r1 → (u1:0, u2:1, …, ur:0 | y's 0)
  - r2 → (u1:1, u2:0 | y's 0)
  - ri → (u's 0 except ur:1 | y1:1, y2:0… pattern) ; r(r+m) → (u's 0 | yr:1, others 0)
- Fig 5.11: summary of complete design flow (image).
### 5.3.1 Fault-tolerant control design (3578-3613)
- FTC architecture (Fig 5.12, Fig 5.11 design steps): FDI module provides ONLINE fault estimates; estimated faults compensate faulty input-output measurement signals BEFORE they reach the controller → pre-existent controller NEVER modified; same FDI module can alternatively drive controller RECONFIGURATION.
- Compensation signals: û (from [5.92]) corrects actuator signal from controller; ŷ corrects acquired output measurement → controller tracks nominal POWER reference signals; controller can be designed purely for fault-free condition thanks to estimation feedback (wind-turbine "power reference" wording confirms benchmark = wind turbine).
- Stability logic in words: model variables remain in a BOUNDED SET → control performance assured even with faults; additive faults do NOT modify system structure → GLOBAL stability guaranteed; fault effect eliminated in STEADY STATE; during TRANSIENT the compensation is not properly handled → stability must be watched.
- Concluding remarks: linear+nonlinear I/O descriptions with disturbance decoupling; fault-sensitivity/dynamic-response optimization procedures.
- Linear residual generators: algorithmic SIMPLICITY = key virtue for verification & validation cost on real systems (complexity ↑ → V&V cost ↑).
- Nonlinear methods: structural decoupling via state/output coordinate transformations (simplified models may be needed); mixed H−/H∞ trade-off fault-sensitivity vs disturbance vs model error = well understood theoretically, promising for energy conversion systems.
- Adaptive-filter FDI advantage: provides fault SIZE estimation (unusual for FDI) → useful for online automatic reconfiguration; applies to more general nonlinear classes; LESS noise-sensitive because NO input-output signal derivatives used.
- Stochastic side: filtering algorithms for systems with NON-GAUSSIAN noise/disturbance; noise-process knowledge exploited in diagnosis+accommodation design.
- Main advantage vs alternatives: nonlinearity and reality-model mismatch handled directly; compensation applicable to HIGH-FIDELITY power-plant (wind) simulators with disturbances+measurement errors; effectiveness via simulations + comparison with data-driven and model-based decoupling schemes; ROBUSTNESS to model uncertainty/disturbance/noise to be analyzed with Monte Carlo tuning of FDI/compensation parameters.
- Closing thesis: bridge the design gap between fault diagnosis and recovery = sustainable control; diagnosis + FTC designs combine coherently.
### 5.4 Summary (3614-3623)
- Fault estimators designed for FTC; by-products = FD + FI tasks; fault-tolerant controller implementations = key issue in sustainable control of safety-critical systems.
- Most effective FTC = online ESTIMATION + COMPENSATION of faults modeled as equivalent input and output sensor faults → effectively describes ANY fault condition of the considered dynamic systems.
### 5.5 References (3624-3690, ~55 entries)
- Anchor lineages: Frisch/EIV = Beghelli-Castaldi-Guidorzi-Soverini (1994a, 1994b, 1997), Jens/Linden/Larkowski/Burnham (2012); NLGA = De Persis & Isidori (2001) IEEE TAC 45(6):853-865; H−/H∞ FD observers = Hou & Patton (1996); Chen & Patton (1999) monograph; fuzzy/TS = Babuška (1998, 2000 FMID toolbox), Kaboré & Wang (2001); PI/self-tuning = Bobál et al. (1995, 2005), Franklin et al. (1998), Skogestad (2003) JPC 13(4):291-309, Ho & Xu (1998), Visioli (2003); bumpless = Cheong & Safonov (2008), Jun & Safonov (1999); wind benchmark cluster = Odgaard/Stoustrup/(Damgaard, Nielsen)/(Kinnaert) 2009-2013 (IEEE TCST 21(4):1168-1182 benchmark model), Sloth et al. 2010/2011, Bianchi et al. 2007, Galdi et al. 2008, Sami & Patton 2012, Gong & Qiao 2013, Freire et al. 2013; PFTC=AFTC book = Mahmoud/Jiang/Zhang (2003); LPV FTC = Rodrigues et al. (2007), Puig (2010), Niemann & Stoustrup (2005); FMEA = Stamatis (2003); NN fault diagnosis = Simani/Fantuzzi/Spina (1998), Simani & Patton (2002), Schilling et al. (2001); PWA = Rovatti/Fantuzzi/Simani/Beghelli (1998), Fantuzzi et al. (2002), Simani et al. (1999a,b,c).
- Benchmark plant PARAMETER TABLE NOT in this chapter: Ch5 is the modeling framework chapter; the only numbers = O&M ≤ ~30% energy cost, Kp=0.6·KPu, TI=0.5·Tu, margins within 5% max error, δ≥2 (three-sigma), τc=L rule; wind-turbine plant values appear in later application chapters. Table 5.2 signature matrix rows as OCR-fragmented pattern above [OCR?].

## Puig Vol2 Ch6 — Virtual Sensors and Actuators (source 3697-4127)

Authors of chapter: Damiano Rotondo (Univ. of Stavanger) & Vicenç Puig (IRI, UPC Barcelona).

### 6.1 Introduction (3697-3711)
- Two FTC families: (a) redesign control law after fault; (b) hide fault from controller via a **fault masking block** so the controller is never redesigned.
- Why masking: plug-and-play deployment (no re-tuning) + the nominal controller embeds valuable implicit plant/performance knowledge acquired in its design cycle.
- Virtual sensors/actuators belong to the fault-masking family. Formalization in Blanke et al. (2016); originally introduced by **Lunze and Steffen (2006)**.
- Extension lineage: first LTI, then LPV (Rotondo et al. 2014), Hammerstein (Richter & Lunze 2010), Lure (Pedersen et al. 2016), Takagi-Sugeno (Rotondo et al. 2016), piecewise-linear (Richter et al. 2011).
- Virtual sensor = observer estimates the faulty sensor's output (a.k.a. **soft sensor**). Virtual actuator obtained by **duality**: replaces faulty actuator by redistributing control action to the remaining healthy actuators; design equations mirror virtual sensor ones (like controller/observer transposition).
- Requirement: enough redundant sensors/actuators to compensate faulty components.
- Chapter arc: eigenvalue-assignment design → LMI formulation as bridge to nonlinear systems via LPV polytopic representation → four-tank case study → conclusions/outlook.

### 6.2 Problem statement (3713-3793)
- Nominal setup: LTI plant (state x ∈ R^n) interconnected with a state observer (state x̂ ∈ R^n); estimate-feedback control law updates u ∈ R^p; plant→observer feedback flow is the innovation C·e(t) = C(x−x̂) ∈ R^m. A,B,C known; K (controller), L (observer) designed for asymptotic stability. [formulas 6.1 not decoded]
- Augmented state z_xe = [x^T, e^T]^T makes the closed loop **block-triangular** → separation principle: design K, L separately s.t. A−BK and A−LC asymptotically stable. [formula-not-decoded]
- **Sensor fault case**: output equation becomes y = C_f x + f_y, with C_f faulty output matrix (multiplicative faults) and f_y ∈ R^m additive sensor faults. C_f built from C by scaling column i by effectiveness γ_i ∈ [0,1): γ_i=1 healthy, γ_i=0 total failure. [formulas-not-decoded]
- Consequences (augmented system no longer block-triangular):
  - separation principle no longer holds; state matrix may acquire non-negative eigenvalues from C_f → closed loop unstable despite asymptotically stable nominal design;
  - even if stability survives the C_f/C mismatch, the augmented system is non-autonomous due to f_y(t) → error does not converge to zero.
- Assuming estimates Ĉ_f, f̂_y available, Problem 1 (**virtual sensor structure choice**): choose virtual sensor dynamics (state x_vs, output y_vs, gain M — structure [6.6], [formula-not-decoded]) fed instead of y(t) into the observer, so the overall augmented interconnection (faulty plant + observer + virtual sensor) tends to an autonomous system resembling block-triangular diag(A−BK, A−LC) as Ĉ_f→C_f and f̂_y→f_y.
- **Actuator fault case** (dual): state equation xdot = B_f u + f_u with B_f faulty input matrix, f_u ∈ R^p additive actuator faults, effectiveness factors φ_i ∈ [0,1) scaling B's columns same way as γ_i. [formulas-not-decoded]
- Problem 2 (**virtual actuator structure choice**, structure [6.10] with gain N, outputs u_va, y_va — [formula-not-decoded]): feed faulty plant with u_va instead of u and observer with y_va instead of y; same "recover block-triangular autonomous" objective as B̂_f→B_f, f̂_u→f_u.
- Key stability logic: solving Problems 1-2 keeps nominal K, L enforcing asymptotic stability under fault **provided the extra diagonal block introduced by the virtual sensor/actuator is itself asymptotically stable**; each masking block adds only one extra block, independent of K and L.

### 6.3 Virtual sensors and virtual actuators (3795-3892)
- Sensor side, two cases decided by a **rank condition** [6.6.2 per OCR numbering; formula-not-decoded]:
  - condition holds → information lost through Ĉ_f can be reconstructed **perfectly from available measurements alone** (no dynamic model needed) → virtual sensor is a **static block** g_vs not depending on x_vs [6.15];
  - condition fails → must exploit the system's dynamic model → virtual sensor is a **dynamic block** [6.16] with state x_vs and **virtual sensor gain M ∈ R^{n×m}**; Ĉ* defined by [formula-not-decoded].
- Static case [6.15] is a special case of dynamic [6.16]: when the rank condition holds, Ĉ* → C so (C − Ĉ*)x_vs → 0.
- Interconnection (faulty plant + observer + dynamic VS) is excited only by the additive fault **estimation error** f_y(t) − f̂_y(t) [6.18]; with [6.17] it simplifies to an autonomous system as Ĉ_f→C_f, f̂_y→f_y [6.19]. A change of variables [6.20] yields [6.21], proving structure [6.16] solves Problem 1.
- **Extended separation principle** (main theoretical payoff): virtual sensor can be designed **independently of controller and observer**. [6.21] gives the augmented eigenvalue set Λ_vs = nominal closed-loop spectra ∪ one extra masking-block spectrum ([formula-not-decoded]; text note: "eig(M) denotes eigenvalues of matrix M" [OCR? notation ambiguous]).
- Design recipe (sensor): given asymptotically stable nominal loop, fault tolerance = insert VS designed so **A − MĈ* is Hurwitz**.
- Actuator side, exact dual, two cases by rank condition **[6.23]**:
  - holds → lost actuation from B_f compensated perfectly by **redistributing over remaining actuators**, no need for state-matrix A dynamics → **static virtual actuator** [6.24];
  - fails → must exploit A → **dynamic virtual actuator** [6.25] with state x_va and **gain N ∈ R^{p×n}**; B̂* defined [6.26, formula-not-decoded].
- Consistency: when [6.23] holds, B̂* → B so (B − B̂*_f)u(t) → 0 and x_va(t)=0 ∀t (if x_va(0)=0) → static is special case of dynamic.
- Interconnection excited by actuator estimation error f_u − f̂_u [6.27]; autonomous as B̂_f→B_f, f̂_u→f_u; change of variables gives eigenvalue set Λ_va = nominal spectra ∪ extra block [formula-not-decoded].
- Design recipe (actuator): insert VA designed so **A − B̂*N is Hurwitz**.

### 6.4 LMI-based design (3893-3980)
- M and N could be placed with standard LTI tools (e.g. **Ackermann formula**, Ackermann 1972), but the LMI route is presented because it extends easily to nonlinear systems with **convex representations** (López-Estrada et al. 2019), notably **LPV** (Rotondo et al. 2014).
- Foundation: **quadratic stability** — ∃ symmetric P ≻ 0 with PA + AᵀP ≺ 0 (≻/≺ = positive/negative definiteness: all eigenvalues of P positive, all of PA+AᵀP negative) [Definition; formula-not-decoded].
- **Problem 3**: given A,B,C,Ĉ*,K,L choose M s.t. autonomous VS augmented system [6.21] quadratically stable. **Problem 4**: given A,B,B̂*,C,K,L choose N s.t. [6.30] quadratically stable.
- **Lemma 1 (QS of block-triangular systems)**: if diagonal subsystems ẋ₁=A₁₁x₁ and ẋ₂=A₂₂x₂ are QS, the whole block-triangular system [6.34] is QS.
  - Proof sketch: P₁,P₂ from each subsystem; candidate P = [P₁ 0; 0 P₂] + ε off-diagonal [6.37]; plug into [6.33]; **Schur complements** (Duan & Yu 2013) with γ=1/ε; conclusion rests on: for Z≻0 (min singular value σ_Z>0) and any W (max singular value σ_W), ∃γ>0 with γZ−W≻0 since vᵀ(γZ−W)v ≥ (γσ_Z−σ_W)‖v‖² > 0 when γσ_Z > σ_W.
- Consequence: once the two nominal diagonal subsystems are QS, Problems 3-4 reduce to making the single extra block (A − MĈ* resp. A − B̂*N, [6.45]) quadratically stable.
- Sensor gain LMI: condition PA−…M is a **BMI** [6.46] (product P·M); change of variable **W = PM** linearizes to LMI **[6.47]**, then **M = P⁻¹W** a posteriori.
- Actuator gain LMI: BMI converted by **congruence** pre/post-multiplication with **Q = P⁻¹** (signature preserved — Sylvester's law of inertia) to LMI **[6.49]** with **H = NQ**, recovered as **N = HQ⁻¹**.
- These LMIs are the ones solved in the quadruple-tank application (6.6): [6.47] → virtual sensor matrix, [6.49] → virtual actuator matrix.

### 6.5 Additional considerations (3981-4039)
- **Joint formulation** (Rotondo et al. 2014): handle sensor AND actuator faults together by modifying the virtual sensor [6.16]→[6.50] and feeding it with a combined signal [6.51] instead of y(t).
- Under Ĉ_f→C_f, B̂_f→B_f, f̂_u→f_u, f̂_y→f_y, the full interconnection (faulty plant [6.3]+[6.12], observer [6.7], VA [6.25], modified VS [6.50]) is autonomous [6.52]; a change of variables [6.53] makes it **similar to a block-triangular matrix [6.54]** → justifies **separate** design of M and N.
- **Pole hierarchy caution**: as with observer-based control (relative position of A−LC poles vs A−BK), the masking poles of A−MĈ* and A−B̂*N **should be faster than those of A−BK** to minimize performance degradation. With reduced redundancy under fault this is unrealistic; the relaxed requirement [6.55] compares Re(dominant eigenvalue) of the blocks [formula-not-decoded]. **D-stability** pole-region LMI extension: Chilali & Gahinet (1996).
- **LPV extension**: A,B,C functions of θ(t) ∈ compact Θ (measured or estimated online); assumed expressible as convex combination of constant vertex matrices [6.56]-[6.58] (Rotondo et al. 2019a). VS/VA gains become θ-dependent; LMIs [6.47]/[6.49] replaced by parameter-varying versions [6.59]-[6.60], converted to a **finite set of vertex LMIs** via the convex-hull assumption (Sala & Arino 2007).
- Special case B,C constant (only A(θ) varies): LMIs reduce [formulas-not-decoded]; vertex gains recovered as **M_i = P⁻¹W_i**, **N_i = H_iQ⁻¹**.

### 6.6 Application example (4041-4068)
- Benchmark: **quadruple-tank system** of **Johansson (2000)**, modified with an extra pump + valve feeding tanks 3 and 4 to add **actuator redundancy** for demonstrating the virtual actuator (Figure 6.1).
- Linearized model around operating point **u0 = [3 3]ᵀ, x0 = [12.4 12.7 1.8 1.4]ᵀ** [matrix formula-not-decoded]. Parameters (Table 6.1):
  - A1 = A3 = 28 cm²; A2 = A4 = 32 cm² (tank cross sections)
  - T1 = 62.7034 s; T2 = 90.3353 s; T3 = 23.8900 s; T4 = 29.9930 s (time constants)
  - k1 = 3.33; k2 = 3.35; k3 = 3.34 cm³/(V·s) (static gains)
  - γ1 = 0.7; γ2 = 0.6; γ3 = 0.65 (valve opening degrees); kc = 0.5 V/cm (sensor gains)
- Control: state feedback (all levels measured), designed with LMIs around the linearization point; gain [6.64] [formula-not-decoded].

#### 6.6.1 Virtual actuator (4070-4080)
- Fault on the **third actuator** (the added pump); 2 remaining pumps healthy → still controllable, but rank condition [6.23] **fails** → static VA insufficient, need **dynamic VA [6.25]**.
- Solve LMI [6.49] → VA gain [6.65] [formula-not-decoded — number not recoverable from OCR].
- Scenario: fault appears at **t = 10 s**, VA activated at **t = 15 s**; closed loop recovers nominal behavior; without VA it does not (Figure 6.2 compares nominal / faulty w/o VA / faulty w/ VA).

#### 6.6.2 Virtual sensor (4082-4092)
- Fault on the **sensor measuring tank-2 level**; 3 remaining sensors healthy; text says "still controllable" [OCR? presumably observable] but rank condition **fails** → need **dynamic VS [6.16]**.
- Solve LMI [6.47] → VS gain [6.66] [formula-not-decoded].
- Same timing: fault at 10 s, VS activated at 15 s; recovers nominal vs faulty-without-VS (Figure 6.3).

### 6.7 Conclusion (4094-4100)
- Recap: fault-masking FTC = hide fault from controller via masking block (VS for sensors, VA for actuators); **plug-and-play** — the block joins the loop, controller never redesigned; easy nonlinear extension via LPV + LMI.
- Active trend: **reconfiguration blocks (RB)** generalize VS/VA to handle either sensor or actuator faults generically (Bessa et al. 2020, TS-fuzzy RB).
- **DoS-attack extension** (Rotondo et al. 2019b): attacker assumed energy-limited (pulse-width-modulated DoS on actuators); VA design incorporates attacker-energy constraints → **milder conditions on A − B*N: it may even be unstable** during an attack if the attack-free asymptotically stable loop compensates the instability between attacks.

### 6.8 References (4102-4121) — load-bearing anchors
- Origin: **Lunze & Steffen (2006)** IEEE TAC 51(10) (disturbance-decoupling reconfiguration); formalized in **Blanke/Kinnaert/Lunze/Staroswiecki (2016)** 3rd ed.
- LPV VS/VA: Rotondo, Nejjari, Puig (2014) JPC 24(3); TS-VA to fuel cell: Rotondo et al. (2016); LPV LMI design survey: Rotondo et al. (2019a); convex-approaches review: López-Estrada et al. (2019); vertex-LMI finiteness: **Sala & Arino (2007)** (Pólya's theorem); pole-placement LMI: **Chilali & Gahinet (1996)**; Schur/LMI compendium: Duan & Yu (2013); Ackermann (1972); benchmark: **Johansson (2000)** quadruple-tank; other system classes: Richter & Lunze (2010) Hammerstein, Richter/Heemels/van de Wouw/Lunze (2011) PWA, Pedersen et al. (2016) Lure/power-system; DoS: Rotondo et al. (2019b) Neurocomputing 365.

Chapter ends at 4121; Ch7 "Conclusions" (Puig & Simani) starts 4122.

## Puig Vol2 Ch7 — Conclusions (source 4128-4391)

### 7.1. Introduction (4128-4179) — book retrospective
- Ch7 = Conclusions; Vol2 Ch7 recaps achievements, Vol2 Ch8 holds open problems/futures (4176-4178)
- Framing: diagnose & compensate faults early to improve performance, cut maintenance cost, raise availability/safety (Zhang & Jiang 2008; Isermann 2005b; Mahmoud 2003; Blanke 2003)
- Data-driven vs model-based verdict (4138): data-driven exploits plant's existing measurements, avoids expensive auxiliary monitoring modules; model-based needs accurate analytical descriptions but gives more efficient regulation + quicker reaction/recovery
- Application examples modeled uncertainty as Gaussian stochastic disturbance; experiments via high-fidelity simulators / hardware-in-the-loop (4144)
- Vol1 Introduction = state-of-the-art literature survey 2015-2020 (4150)
- Vol1 recap bullets (4150-4162):
  - Ch1: mathematical modeling + descriptions of most-used fault classes, matched to diagnosis/FTC design strategy
  - Ch2: structural analysis; standard tools identify submodels for model-based & data-driven diagnostic modules; operates on equation sets obtainable model-free too
  - Ch3: set-membership + interval observers for robustness with preserved fault sensitivity; isolation extension via unknown-input observers
  - Ch4: stochastic FDI methods, model- and data-based
  - Ch5: "model-free"/data-driven FDI for nonlinear dynamics with non-smooth nonlinearities; system parameters may be unknown
  - Ch6: AI methods; logic-reasoning model-based diagnosis as AI-community predominant approach, plus its evolution
- Vol2 recap bullets (4164-4178):
  - Ch1: nonlinear model-based FD/FTC review; extensions of linear schemes to nonlinear; robustness under uncertainty
  - Ch2: LPV FDI/FTC of descriptor LPV systems with non-measurable scheduling variables (actuator faults + perturbations)
  - Ch3: fuzzy + neural-network FDI/FTC for uncertain models (uncertainty + nonlinearity)
  - Ch4: MPC under uncertainty/nonlinearity at several approximation and computational-complexity levels
  - Ch5: nonlinear FTC methodology: detect, isolate, accommodate; controller compensates faults using FD info
  - Ch6: virtual sensors/actuators for sensor+actuator faults; LPV extension via LMI framework

### 7.2. Closing remarks (4180-4239) — economic/technical synthesis
- Key economic number: O&M expenses can increase production cost by up to ~30%, esp. offshore energy conversion (stated twice: 4182, 4212; cites Blesa 2014, Shi & Patton 2015a)
- Industry default = conservative: shut down and wait for maintenance; book's case: diagnosis + FTC prevents critical failures, avoids unplanned replacement of functional parts, cuts O&M (4184)
- Redundancy paradox (4188): extra sensors/actuators (wind turbines: extra sensors vital; power plants: independent actuation per redundant actuator, 1-2 failures still safe) improve safety but add cost/downtime; enhanced safety can REDUCE availability (Kimmich 2005)
- Wind-turbine hardware taxonomy (4190-4194): pitch actuator in hub; mechanical/electrical/hydraulic brakes; epicycloidal or parallel-axis gearboxes; generators:
  - asynchronous/squirrel-cage: slip small at nominal, "constant speed" machine
  - doubly-fed: rotor-to-grid power converter enables variable speed
  - synchronous: voltage frequency proportional to rotational speed
  - full-converter: converter between generator and grid, variable speed
  - tower height sets hub height; power up because wind speed grows with distance from surface
- Closed loop decomposed: process + actuators + controller + input sensors + output sensors, each carries its fault class (4198)
- Hardware redundancy = multiple components + voting; effective but equipment+maintenance cost conflicts with sustainability (4198)
- Analytical redundancy: model-estimated variable, residual ~0 healthy / clearly nonzero faulty; software only, no extra equipment; risk: model inaccuracy + disturbances/noise -> false alarms/missed faults (4200)
- Residual pipeline (4202): generation = measured minus estimated (ideally independent of I/O fault-free) then evaluation: fixed threshold ("geometrical methods") or pre-processing (moving average, statistical methods) before thresholding (Basseville refs)
- Signal-based subclass: output-only; vibration analysis of rotating machinery via band-pass filters / spectral analysis (4204)
- Canonical model-based FDI trio: output observer, parity equations, parameter estimation (4206); nonlinearity + time-varying params + unknown noise create fault-free model-plant discrepancy that can hide faults; counters: unknown-input observer, eigenstructure assignment, parity relation
- Data-driven rationale (4208): fuzzy = collection of local affine models with transitions via identified fuzzy parameters; NN learns functioning from training data
- FTC taxonomy (4210-4218):
  - PFTC: no diagnosis, no reconfiguration; fixed parameters, robust to a fault set; optimized fault-free with degradation constraints; limited tolerance but zero false-FDI/reconfiguration risk
  - AFTC: reconfigures control via FDD block giving real-time fault (unknown-input) estimates; extra loop for fault accommodation; nominal-only design; FDD also boosts fault-free performance by compensating model errors/disturbances
- Design constraints (4220): output feedback + measurement noise + nonlinear/LPV; LPV & fuzzy descriptions as bases; AFTC schedules controller on FDD-estimated LPV/fuzzy parameters; PFTC modified for parametric uncertainty or via optimization maximizing disturbance attenuation
- Digital twin (4222-4226): lineage handmade drafting -> CAD -> model-based systems engineering; twin = real-time sensor-updated copy (shape, position, gesture, status, motion); used for monitoring/diagnostics/prognostics, turbine/jet-engine/locomotive maintenance, autonomous-vehicle AI training/validation
- Performance maximization (4228-4230): extremum seeking (no detailed model, but slow convergence, struggles with global max on non-convex surface) vs optimal set-point determination + regulator (needs accurate model); generic framework = upper optimal set-point stage + lower tracking loop, both under physical constraints (variable-speed turbine: optimal rotational speed via torque/blade-pitch control)
- Control = constrained optimization; classic quadratic tracking-error objective is a special case (4232); methods developed since late 1970s (4234)
- Adaptive control (4238): system-ID black-box models have no structural relation to physics; data-driven + controller computation = adaptive schemes; linear-model adaptive schemes track nonlinearity-induced variation, but nonlinear systems best served by dedicated fixed-parameter nonlinear controllers; stability/convergence care across all regimes

### 7.3. References (4240-4385) — 133 alphabetical entries, no prose
- 133 bullet entries spanning Anderson(1985)-Zogg(2006); heavily SAFEPROCESS-school: 24 entries mention Patton, 11 Frank, 8 Isermann
- Benchmark anchor: Bartys et al. 2006, DAMADICS actuator FDI benchmark study, Control Engineering Practice 14(6), 577-596 (special issue)
- Book-length anchors: Blanke et al. 2003/2006 DFTC (Springer); Isermann 2005a Fault-Diagnosis Systems; Ding 2008; Chen & Patton H-infinity filter line (2000)
- Wind-turbine FTC cluster underpinning the 30% O&M claim: Blesa et al. 2014 (CEP 24, 138-155, interval observer + virtual sensors/actuators), Shi & Patton 2015a (Renewable Energy 75, 788-798, offshore), Shaker & Patton 2014 (T-S sensor FTC)
- LPV/descriptor anchors: Shi & Patton 2015b (IJRNC 25(5), 689-706), Hassanabadi et al. 2016, Rodrigues et al. 2007 (polytopic LPV)
- Set-membership anchor: Puig 2010 (IAMCS 20(4), 619-635); survey anchors: Zhang & Jiang 2008 (Annual Reviews in Control 32, 229-252), Frank 1990 (Automatica 26(3)), Basseville 1988 survey
- [OCR?] editorial dup: Svard & Nyberg 2010a and 2010b (4359-4360) are byte-identical citations of the same paper (IEEE Trans SMC-A 40(6), 1310-1328)
- Boundary: source lines 4386-4391 hold '## 8 Open Research Issues' + Ch8 author block (Ch7 content ends at 4385)

## Puig Vol2 Ch8 — "Open Research Issues" (source 4392-4774; actual chapter title at line 4391: "## 8 Open Research Issues", Puig & Simani)
### 8.1 Further works and open problems (4392-4404)
- Goal: advanced control + condition monitoring + innovative strategies that maximize performance while cutting installation (mechanical structure), operation and maintenance costs; energy conversion processes are the flagship case (Bossanyi et al. 2009); ambition = **lighter mechanical structures with improved performance** via mitigation of vibrations and fatigue damage from rotating machines → cost-effectiveness + reliability.
- Control strategies must be designed so process working-condition spectra do NOT match the mechanical structure's natural frequencies (fatigue/peak-load reduction) — extremely important for wind turbines (Bianchi et al. 2007; Fischer et al. 2012).
- Advanced control needs reliable states, disturbance distribution among control/driving inputs, uncertainty forecasting → more sensor info than normally available (effective driving inputs, structural modes) → **measurement reliability is a key issue**; if control relies on faulty sensors with no accommodation → HIGHER loads / lower availability (lost production or de-rating) instead of lower.
- Method: test advanced control + sensing concepts first on high-fidelity simulators of simplified models; extension to complex systems treats the whole design as a **global optimization problem**.
- Exploit knowledge of typical sensor/actuator faults to build tolerance into the control (the volume's FTC thesis); exemplars van Engelen 2011, Odgaard 2013, Shi & Patton 2015 = the "sustainable control" concept; synergy of vibration condition monitoring + predictive/proactive maintenance + load identification extends wind turbine lifetime; coupling of power-optimization control ↔ fatigue/extreme loads ↔ lifetime control must be handled.
### 8.1.1 Sustainable control design objectives (4406-4443)
- Control optimization of the ENTIRE power plant via integrated sensing design; European industry cost split = direct (fabrication) + indirect (installation) (Fischer et al. 2012; Willecke & Fischer 2013); better disturbance/uncertainty mitigation → lighter structures at same power → lower energy cost + reduced O&M.
- Three industry-set objectives: (i) reduce **lost production factor** (actual vs possible production, plant-caused only), (ii) decrease **production cost** (all put-up/keep-up/take-down expenses ÷ producing lifetime), (iii) reduce **maintenance costs** of main components (Bossanyi et al. 2009; Odgaard 2012). Fig 8.1 "Key points of sustainable approach" + Fig 8.2 "objectives-goals-impacts link" [figure not decoded].
- Methodology task list (4424-4429): plant specs/models incl. disturbance, uncertainty, model-reality mismatch; sensor/actuator models + their faults; sensing systems = sensors + condition monitoring + FDI + fault tolerance; disturbance-reducing control incorporating new sensing outputs into sensor/actuator FTC; verification on high-fidelity simulators/benchmarks — disturbance mitigation evaluated per **IEC 61400** + plant lifetime; lost production factor + cost-reduction contribution.
- Safety note: with no special actions, a wind turbine must simply **shut down** on sensor faults. EU agenda: advanced control of large-scale turbines AND wind farms (efficiency, lower cost of energy, value via response to grid disturbances/market); treat the whole wind plant as one control optimization problem (Hossain 2018; Niemann 2018; Leite 2018; Bossanyi 2003).
- Deliberate stance: NO future untested sensors — exploit existing proven sensor technology with faults studied from past experience; control may replace heavier structures only once confidence/reliability is demonstrated; business/normative/health+safety from a lifecycle perspective; define KPIs early in design.
### 8.1.2 Sustainable control concepts and approaches (4445-4461)
- Core: raise the knowledge level of states around each process module → exploited for condition monitoring + advanced control → same working conditions with lighter/simpler structures, big production-cost cut.
- Lifetime loading: disturbances + extreme load/torque peaks from rotating machines (key issue offshore); structures must withstand intense vibrations AND small continuous vibrations (fatigue); lighter-structure dynamics handled only with reliability tools of the FTC framework (Blanke et al. 2006; Isermann 2005; Odgaard et al. 2013).
- Pure structural shape/material choice at design stage is "limited"; step forward = structure sensing feeding a **"semi-active" control system** minimizing overall dynamic response under extreme conditions (Bottasso et al. 2013).
- Faults reframed as **loads/structural stress** on the load-carrying structure; diagnosis + prognosis + root-cause analysis let faults be predicted and eliminated in advance → efficient O&M planning.
- Sensor inventory (state-of-the-art industrial only): ultrasonic wind, **LiDAR**, mechanical wind, pitch position, blade load, rotor azimuth, rotor speed, tower-top + structure accelerometers (Lio et al. 2015; Towers & Jones 2014); LiDAR models kept for comparison — test whether industry-sensor sensing matches remote sensing (Valencia-Palomo 2014); validation mandate: high-fidelity simulation codes + test benches.
### 8.1.3 Sustainable control approaches and working methods (4463-4510)
- Iterative design: hardware sensors + **software sensors (observers)** estimating all states; estimates cross-checked against extra sensors + thresholds on unmeasured variables; the added physical sensors validate observers and give redundancy for congruity tests; redundancy diagnoses actuator health and abnormal-stress development; fault/disturbance estimation compensates in feedback via robust state estimates (Plumley et al. 2014).
- 7 design tasks (4481-4493; iterations = cross-couplings in Fig 8.3 [figure not decoded]): 1) problem description + control-requirement characterization; 2) subsystem/plant dynamics + sensor/actuator modeling; 3) new sensing systems (sensors + observers + condition/health monitoring + FDI + fault tolerance); 4) advanced control incorporating new sensing, integrated disturbance/uncertainty mitigation with sensor/actuator fault tolerance; 5) test/verification of disturbance, uncertainty, lifetime, lost production factor, cost decrease on high-fidelity simulators + test benches per **IEC 61400** extreme scenarios incl. faults; 6) cost evaluation + risk/safety analysis; 7) final result analysis.
- Sensing details: optimal state estimation given sensor status; sensor faults and external misreadings diagnosed by **unknown-input observers with adaptive thresholds** + robust control; fault accommodation via estimator reconfiguration and/or fault estimation-compensation (geometric, fuzzy); **sensor placement optimization**.
- Controller: robust FTC + multivariable design vs sensor/actuator faults; safety during emergency stop/start-up/shut-down; optimize conflicting performance-vs-max-admissible-disturbance objectives in near-normal operation; challenge = use the process itself as a **"high-level" sensor**; disturbance behavior approaching structural filtering/control of high-performance aircraft (Castaldi et al. 2014); Fig 8.4 "Sustainable design strategy tasks and targets" [figure not decoded]; lifecycle: models → design → verification → experimentation.
### 8.1.4 Sustainable control design ambition (4511-4547)
- Spelled-out tension: load-mitigating add-ons **individual pitch** (Bossanyi 2003; Bottasso 2013; Lio 2015) + **LiDAR wind-speed preview** make turbines *more expensive and more fault-sensitive* and can LOWER availability if faults are not accommodated (Odgaard 2012) — worst at very large rotors offshore in harsh environments (Bossanyi & Hassan 2000).
- The gap: disturbance-limiting control needs MORE state measurements → the innovation is *how existing sensors are used*: state observers tolerant of sensor faults and external misreadings (Odgaard & Stoustrup 2013; Johnson & Fleming 2011).
- Unaccommodated sensor faults → performance/availability lost → undesired shutdown → higher lost production factor; shutdowns themselves cause extreme disturbances → avoid by control-input modulation during emergency stops or controllers that mitigate extreme disturbances; offshore site inaccessibility (weather) → FTC + FDI recognized as THE sustainability solution (availability + power generation).
- Ambition: develop software sensing, CM, advanced control, FDI and DEMONSTRATE effectiveness on high-fidelity simulators per IEC 61400; the most ambitious item = **automatic fault prediction + fault/failure root-cause analysis during operation**; self-calibration schemes and optimal sensor placement included; fault info is a free by-product of the FDI/FTC modules that also protect the sensing system itself.
- Pitch actuators = the particularly relevant actuator class; emergency shutdown must never violate prescribed plant limits.
- Honest self-critique (4531): "One of the most important problems of the fault-tolerant control issues is that they have never been related to real problems." FTC scope widened beyond sensor/actuator faults to **unwanted dynamic behavior (disturbance) created by the improved operating conditions themselves**.
- 4 best-industrial-practice objectives (4539-4545): improved performance while keeping original structure + lifetime; reduced lost production factor (advanced sensing + FTC); reduced maintenance cost of main components; decreased production cost of future plants; requires a multi-disciplinary framework (mechanical engineering, metrology, fluid mechanics, condition/vibration monitoring, fault diagnosis, automatic control, signal processing, computer simulation).
### 8.1.5 Sustainable control innovation potentials (4549-4559)
- Main novelty = radically new control + condition-monitoring tools that control **structural disturbances** using an advanced software-sensing system providing states, key measurements, disturbance/uncertainty effects and unknown inputs; disturbance compensation improves working conditions WITHOUT modifying process design or production efficacy.
- Both controller and sensing made fault-tolerant → availability up → production cost down ("very important and novel outcome"); next outcome = strategies covering disturbance/uncertainty/**damage distribution** under complex working conditions, simulations + practical testing with global optimization.
- Hard control-theoretic difficulty named: for powerful machines **required control bandwidths can be close to disturbance frequencies** (no clean spectral separation) → estimation + compensation mandatory; robustness/reliability of the CM/FDI/FTC modules themselves is load-bearing for the whole strategy.
### 8.1.6 Sustainable control expected impacts (4561-4581)
- Benchmark numbers (IEA/EC via World Energy Council 2018): **EU electricity demand could double by 2030**; **~10,000 billion euros** global investment needed incl. replacing aging infrastructure.
- Wind = most advanced "new" renewable technology; innovation = control/shaping of induced disturbances → lower building/installation/maintenance costs, esp. harsh environments; scientific impact = sensing/diagnosis/control tools integrated with structural design tools + new high-fidelity simulators and observer/estimation/control schemes.
- Industrial impact: higher technology levels, demonstrators + high-fidelity simulators as verification; long-term: climate/energy challenges via lower cost + higher availability, new markets, competitiveness.
### 8.2 Summary (4583-4591)
- Concrete further-research leads named by the authors: (1) **optimize residual generators, esp. NN schemes** — compare architectures and training algorithms; (2) **upgrade the main controller inside active FTC** — the volume used only a "simple pre-existent controller"; (3) validate the tools on **real industrial plants**.
- Critique of practice: currently adopted industrial control strategies are "often too conservative" — they shut the faulty plant down and wait for maintenance service.
- Closing position: sustainable control application is "still in its infancy", industrial use at "prototype phase"; renewable energy conversion is the flagship target; the systems & control community has many fundamental/applied problems to work on.
### 8.3 References (4593-4628)
- ~30 refs anchored on: Bianchi et al. 2007 (WT control), Blanke/Kinnaert/Lunze/Staroswiecki 2006 (FTC text), Bossanyi 2003 / Bossanyi & Hassan 2000 / Bossanyi et al. 2009 (load-reduction control), Bottasso et al. 2007/2013 (multi-layer load control), Burton et al. 2011 (Wind Energy Handbook 2e), Castaldi/Mimmo/Simani 2014 (diff-geometry AFTC aircraft), van Engelen et al. 2011 (sustainable-control FTC), Fischer et al. 2012 (integrated offshore design+controls), Odgaard 2012 / Odgaard & Stoustrup 2013 & 2015 / Odgaard-Stoustrup-Kinnaert 2013 (the wind-turbine FDI/FTC benchmark family), Lio et al. 2015 (IPC), Towers & Jones 2014 (LiDAR wind-field state estimation), Shi & Patton 2015 (offshore FTC), WEC 2018 (Cost of Energy).
- No original benchmark numbers in the chapter — only the WEC figures; figures 8.1-8.4 are concept diagrams [figure not decoded].
### Back matter in range (4630-4774) — low value, once
- 4630-4660 List of Authors (+pre-stubs): Castaldi (Bologna), Hamdi (Kairouan), Kukurowski/Mrugalski/Patan/Pazera/Witczak (Zielona Góra), Puig (UPC Barcelona), Rodrigues (Lyon), Rotondo (Stavanger), Theilliol (Lorraine), Simani (Ferrara).
- 4662-4767 Index [OCR? heavy two-column fragmentation, verify before quoting]: page numbers map the volume — pp.1-46 residual generation (parity equations, observer-based, fuzzy/geometric thresholds); pp.144-157 H∞ & H-/H∞ filter residual generation + NLGA fault estimation; pp.161-171 EIV/Frisch scheme, TS-fuzzy, Gustafson-Kessel clustering, LOLIMOT/ANFIS, Ziegler-Nichols; pp.174-183 AFTC/PFTC, LPV, bumpless transfer, online fault estimation; pp.219-254 wind/sustainable control (LiDAR 249, semi-active control 248, load mitigation 246/254, predictive+proactive maintenance 243, complex systems 241, global optimization 242).
- 4769-4774: "Summary of Volume 1" → "Introduction" → Puig & Simani byline = start of the back-printed Vol-1 summary; body content lies beyond 4774 (bookmark-dump zone, not touched per task constraint).

