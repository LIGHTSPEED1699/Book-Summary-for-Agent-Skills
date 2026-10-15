# Puig & Simani Vol 2 (Ch1–8) — From Nonlinear FDI to Fault-Tolerant Control

**Diagnosis and Fault-Tolerant Control 2** (ISTE/Wiley 2021). Vol 2 = nonlinear FDI methods, LPV, fuzzy/NN, MPC, nonlinear FTC modeling, virtual sensors/actuators, conclusions, open issues.

## Ch1 — Nonlinear Methods for Fault Diagnosis (Simani & Castaldi)
- Same two-block residual architecture as Vol 1 Ch1 but nonlinear: model-reality mismatch now includes **multiplicative faults** (parameter changes ΔΘ are both "uncertainty" and "fault" — the boundary is a design choice).
- **Nonlinear filtering residuals**: KF innovation is zero-mean white when model+noise assumptions hold; a fault changes innovation mean/variance/whiteness → detect on the innovation. **EKF** bank (one filter per fault hypothesis, Norgaard augmented-state formulation); low SNR on both u and y → EIV/Frisch-flavored identification.
- **NLGA — nonlinear geometric approach** (De Persis & Isidori 2000/2001): find maximal output (C, A)-invariant distribution ΣP∗ inside ker(dh) via recursive algorithm with Lie brackets and involutive closure; compute Ω∗ = o.c.a.((ΣP∗)⊥); if Ω∗ ∩ span{dh} = span{d(Ψ1∘h)} with surjection Ψ1, a diffeomorphism puts the system in coordinates where the **x̄1-subsystem is affected by the single fault f and decoupled from disturbance d** → residual generator designed on that subsystem. Structural disturbance decoupling, exact, geometric.
- **Data-driven FDI**: TS prototypes (affine consequents, weighted average of local ARX models); fuzzy c-means clustering (Bezdek J, Picard iterations, optimal cluster count); TS consequent estimation in **noisy EIV environment** via per-cluster covariance matrices Σ(i); local affine models → extract physical parameters (time constants, static gains, offsets) per operating point and compare vs nominal (Füssel/Isermann online-estimation line).
- **Robustness again**: disturbance decoupling principle (residual insensitive to unknown inputs, sensitive to faults); H∞ filtering formulation; **fuzzy thresholds** δν per operating region (C clusters with multidimensional fuzzy sets ηi) as alternative to geometric tests.

## Ch2 — LPV Methods for FDI + FTC (Rodrigues, Hamdi, Theilliol)
- **Polytopic/quasi-LPV models**: scheduling functions ρi(ξ(t)) convex (Σρi=1, ρi≥0); vertex systems Ai,Bi,C,Hi. Classical LPV treats ρ as exogenous measurable — this chapter's twist: **unmeasurable decision variable ξ = x̂** (quasi-LPV) plus actuator faults plus disturbances, on **descriptor (E, A, C) systems**.
- **Actuator fault model**: f(t) = −γ(t)u(t), γk(t) ∈ [0,1[ = loss of effectiveness (0.50 = 50% loss). Partial faults only (Assumption A5).
- Assumptions: rank(CBi)=rank(Bi)=p; (E,Ai,C) R-observable and impulse-observable at each vertex; f and ḟ norm-bounded.
- **Robust polytopic observer (RPO)** with algebraic trick: rank[EC]=n gives T1,T2 decomposition; z(t) + T2Cy(t) reconstructs x̂; **joint state + fault estimation** with symmetric positive-definite learning matrix Γ; scheduling mismatch w(t) = difference between plant and observer scheduling terms treated as bounded vanishing perturbation; LMI conditions for error dynamics.
- **Active FTC**: state feedback u = Σρi(ξ̂)Ki x̂ with estimated states AND estimated faults fed back → online compensation of time-varying faults. Case study: **anaerobic bioreactor** (COD parameters ks, Y, YCH4) — output with vs without FTC compared.
- Recipe: polytopic LPV = the workhorse that lets linear robust tools (LMIs, observers, gain scheduling) cover nonlinear plants with unmeasurable scheduling via x̂.

## Ch3 — Fuzzy and Neural Network Approaches (Witczak, Pazera, Kukurowski, Mrugalski)
- **Observer-based FTC needs a model**; when the analytical model is too complex/unavailable, use **neural state-space models** (with uncertainty description, Mrugalski) or **TS fuzzy models**.
- **TS generation by nonlinear embedding** (Kwiatkowski et al. 2006 automated procedure): write each row of the nonlinear state equation as sum of summands fij = αij/βij + κij; classify summands (constant/non-factorizable vs containing inputs/state powers); assign each to A or B matrix entries via μijk, νijk; premise variables from superposition or direct assignment. → exact TS/LPV embedding of a known nonlinear model.
- **RNN → LPV**: recurrent net x_{k+1}=f(x_k,u_k) transformed to discrete LPV form via diagonal Θ of sector-bounded activation slopes — neural model becomes polytopic for LMI tools.
- **H∞ unknown-input observer for TS systems**: TD=0 decoupling of exogenous disturbance; Theorem 3.1 LMI conditions (P,U,N) for prescribed attenuation μ; 7-step design recipe (E = −D[(CD)ᵀ(CD)]⁻¹(CD)ᵀ, optimization, K̄, N=TA−NEC−LC, K=NE+L).
- **Simultaneous actuator + sensor fault estimation** (Gillijns–De Moor dead-beat style): fault estimate from output differences; feasibility requires **all convex combinations of Bi full rank** — checkable via **block P-matrix test** (Theorem 3.2, Kolodziejczak–Szulc). Twin-rotor system (TRS) example: constant positive/negative biases on both actuators and sensors estimated simultaneously; TS vs nonlinear-estimation comparison.
- **H∞ PDC FTC**: u_k = K(h_k)x̂_k + fault compensation from f̂a,k−1; Theorem 3.3 LMI + Lemma 3.1 relaxation for tractability; **robust invariant set** via ellipsoidal bounding (inner approximation of Gilbert–Tan exact set) to keep behavior admissible under faults.

## Ch4 — Model Predictive Control Methods (Patan)
- MPC pillars: prediction model, rolling horizon objective J = Σ‖y_ref−ŷ‖² + ΣλΔu² with N1≤i≤N2, control horizon Nu<N2, constraints on u and Δu.
- **Uncertainty taxonomy** (Skogestad–Postlethwaite): parametric; neglected/unmodeled dynamics; lumped. Multiple models over operating points; **global uncertainty** description ŷ = f(·) + w(k), w∈W compact known bounds; **set invariance theory** (Blanchini): robust positively invariant sets for constraint satisfaction under disturbance.
- **Neural MPC**: NARX difference equation model; i-step prediction by successive recursion (nonlinear model, iterative optimization) or instantaneous linearization; **MLP with external dynamics** (delays on inputs/outputs) as one-step predictor.
- **Robust NMPC via error models**: identify nominal NN model AND an **error model** ĝ trained on data {u(i), w(i)} generated while running the nominal controller; composite model = nominal + error; uncertainty measures feed the prediction. RNMPC vs NMPC benchmark tables (random/steps/ramp/harmonic references: RNMPC wins consistently); **RAMPC** (robust approximate NN MPC) on a pneumatic/hydraulic cylinder: PI quality 0.61–0.64 vs RAMPC 0.16–0.41 across input/output/parameter uncertainties (viscous coefficient, load mass, cylinder volume).
- FTC link: MPC reconfigures by switching/re-identifying the prediction model after fault diagnosis; constraints + invariance handle actuator saturation after fault.

## Ch5 — Nonlinear Modeling for FTC (Simani & Castaldi)
- **Fault identification is the crown**: if the fault magnitude is estimated, detection and isolation follow. Most FDI techniques (parameter estimation, parity, observers) don't directly identify sensor/actuator faults — need residual→fault-magnitude mapping: **neural approximation of the inverse transfer matrix between residuals and faults**.
- **NLGA + adaptive tuning**: on the x̄11 scalar subsystem (conditions [5.5] on smooth h11, invertible h1c), put residual generator in **filter form** ṙf = −kf rf + h(f, ζ, ν); tune kf by **mixed H−/H∞** (minimize disturbance gain, maximize fault gain); observer formulation preferred over filter form in practice.
- **Additive input/output fault representation**: u(k)=u*(k)+fu(k)+noise, y(k)=y*(k)+fy(k)+noise — equivalent additive faults describe actuator and sensor faults for the whole design.
- **Detection**: residual mean/variance estimated fault-free; threshold |re_i| > δ·σ_ri with δ≥2 tuned for false-alarm/detection trade-off.
- **Isolation via bank of MISO generalized estimators** (Willsky line): each fault estimator driven by input-output subset selected by a **fault sensitivity tool**; **fault signature matrix** (residual × input/output 0/1 table); **FMEA performed before estimator design** to choose I/O configurations.
- **AFTC architecture**: FDD module integrated with existing control loop (Figure 5.7); estimated f̂(k) compensates; digital-twin validation before real deployment.

## Ch6 — Virtual Sensors and Virtual Actuators (Rotondo & Puig)
- The **block-reconfiguration** FTC philosophy: instead of redesigning the controller, insert a **virtual sensor** (replaces faulty measurement channel) or **virtual actuator** (reconfigures faulty actuator channel) between plant and the *unchanged* nominal controller+observer.
- Fault model: sensor effectiveness γi ∈ [0,1) (1 healthy, 0 total failure) in Ĉf; actuator effectiveness φi in B̂f.
- **Virtual sensor**: if rank condition holds (lost sensor info reconstructible from remaining measurements) → **static** block; else **dynamic** block ẋvs = (A−MC_f̂)xvs + Bu + MĈ*y with gain M; makes augmented system autonomous and similar to nominal block-triangular form → **extended separation principle**: nominal K, L stay; fault tolerance added by choosing M with eig(M) stable. Same story for **virtual actuator** with gain N (static redistribution vs dynamic reconfiguration using A).
- **LMI design**: quadratic stability LMIs for M, N; pole-location hierarchy specs (dominant eigenvalue ordering between A−LC and A−BK blocks); **joint virtual sensor+actuator formulation** shows separate design is justified by block-triangularity.
- **LPV extension**: gains M(θ), N(θ) as convex combinations of vertex gains; parameter-varying LMIs → finite vertex LMI set (Sala–Arinò); Mi=P⁻¹Wi, Ni=HiQ⁻¹.
- Case study: Johansson quadruple-tank with sensor/actuator faults; virtual blocks recover nominal closed-loop behavior.
- This is the **passive→active bridge**: virtual blocks tolerate faults without online diagnosis of the controller itself, but rely on fault estimates Ĉf, B̂f from the diagnosis module.

## Ch7 — Conclusions (Puig & Simani)
- Book's map: Vol1 Ch1 model-based FDI, Ch2 structural, Ch3 set-based, Ch4 stochastic, Ch5 data-driven, Ch6 AI; Vol2 Ch1 nonlinear FDI, Ch2 LPV FDI+FTC, Ch3 fuzzy/NN, Ch4 MPC, Ch5 nonlinear FTC modeling, Ch6 virtual sensors/actuators.
- Residual = error between measured and model-estimated output; signal-based techniques when only outputs available (vibrations etc.).
- **AFTC vs PFTC**: active FTC relies on a diagnosis system providing fault info to reconfigure; passive FTC is robust design that tolerates a fault class without diagnosis. Both derivable from the same fault-free design procedure.
- FTC designs must use **output feedback** (partial state measurement) and be validated on **high-fidelity simulation / digital twins** before real plants (turbines, jet engines, locomotives: sensory + historical data for monitoring, diagnostics, prognostics).

## Ch8 — Open Research Issues / Sustainable Control (Puig & Simani)
- **Sustainable control design**: iterative task chain — problem/requirements → subsystem+sensing/actuation modeling → new sensing systems (hardware sensors + software sensors/observers + condition & health monitoring + FDI + tolerance) → integrated advanced control mitigating disturbance/uncertainty with tolerance → test/verify on high-fidelity sims and test benches (lost production factor, production cost) → cost/risk/safety analysis → final analysis.
- Wind-turbine case framing: redundant sensing (hardware + software sensors) enables condition monitoring, actuator health diagnosis, fault/disturbance estimation compensated in feedback.
- The gap to fill: lower production cost while keeping availability/reliability — more state knowledge around working conditions, better sensor/actuator combinations guaranteeing prescribed fault tolerance, and proving lost-production reduction in practice.
- Open directions implied: digital-twin-based validation, prognostics+PHM integration, software-sensor reliability, integrated sensing-control design rather than bolt-on FDI.

## Practitioner takeaways
- FTC decision tree: fault class known and small → **passive** (robust/H∞ design, invariant sets); need to keep operating after real faults → **active**: diagnose (Vol 1 tools) → estimate magnitude (Ch5 bank of estimators / Ch2 RPO / Ch3 TS observers) → reconfigure (**virtual sensor/actuator blocks** Ch6, or MPC model switch Ch4, or scheduled gains Ch2).
- **Virtual sensor/actuator is the cheapest active FTC**: nominal controller/observer untouched; only add M/N gains via LMIs; extended separation principle makes it modular.
- TS/LPV embedding (nonlinear embedding, RNN→LPV) is the gateway that lets every LMI tool in the book apply to nonlinear plants.
- Always validate on a digital twin before the plant; run FMEA before designing fault estimators; δ≥2 residual thresholds with σ estimated fault-free.
