# Isermann Ch20-23 — Case Studies (DC motor, throttle valve, pump-tank, suspension) + Terminology & Math Appendix

**Fault-Diagnosis Systems** (Springer 2006). The book's application chapters — every seeded-fault isolation result with numbers — plus Ch23's IFAC SAFEPROCESS glossary (the vocabulary sheet for the whole skill) and the math/toolbox appendices. New file added by the deep-rewrite pass.

### Ch20 (intro, lines 8635-8641) — Application examples
- Purpose: test robustness of idealized FDD methods (linearity, precise measurements, small stationary disturbances, constant parameters, open-loop, modeled faults) against real-process violations. Case studies here: two DC motors [20.1, 20.2]; plus circulation pump and automotive wheel suspension in following chapters; many more (actuators, AC motors, pumps, machine tools, robots, heat exchangers, pipelines, combustion engines, passenger cars) in separate book [20.5].

### Ch20.1 Fault detection/diagnosis of a DC motor drive (lines 8643-8871)
#### 20.1.1 Test bench
- Permanently-excited DC motor: rated **P = 550 W at n = 2500 rpm**; two brush pairs (commutation), two pole pairs, analog tachometer; load = **hysteresis brake** (also PWM-controlled). Fig 20.1.
- Measured signals: armature voltage U_A, armature current I_A, speed ω. Servo amplifier with PWM armature voltage, speed + current feedback → **cascaded speed control**. Signal path: analog anti-aliasing filters → DSP (TXP 32 CP, 32-bit, 50 MHz [OCR: "fpt"]) + Intel Pentium host PC.
- Constant-parameter linear model does NOT match over the whole operating range → add **two nonlinearities**: term K_g|ω(t)|I_A(t) compensates brush voltage drop combined with PWM supply; friction = viscous M_Fv·ω + dry M_F0·sign(ω). First-order ODEs (20.1),(20.2) [formulas not decoded by OCR]. Signal flow Fig 20.2.
- Parameters via **least-squares in continuous time**; nominal (Table 20.1): armature resistance R_A = 1.52 Ω; armature inductance L_A = 6.82·10⁻³ Ωs [OCR "6.82-1077" → 10⁻³, plausible flag]; magnetic flux Ψ = 0.33 Vs; voltage-drop factor K_g = 2.21·10⁻? V·s/A [OCR "2.21-10°°" exponent lost]; inertia J = 1.92·10⁻³ kg·m² [OCR "1073"→10⁻³]; viscous friction M_Fv = 0.36·10⁻³ Nms [OCR "10 7" exponent garbled]; dry friction M_F0 = 0.11 Nm. Gain-influencing: R_A, Ψ, K_g, M_Fv, M_F0; time-constant-influencing: L_A, J.
- Measurement: sampling freq **5 kHz**; states filtered by 4th-order Butterworth lowpass, cut-off **250 Hz**.
#### 20.1.2 Parity-equation approach
- Structured parity equations with state-space model (Sec 10.2.1). Nonlinear (20.1)-(20.2) → linearize by redefining inputs: effective voltage input U_A' = U_A + K_g|ω|I_A [reconstructed from OCR "Us = Ky Jo(z)|IA"], load input M_L = M_F0·sign(ω) → linear state-space (20.3/20.4 [formula not decoded]); signal flow = Fig 10.8.
- Observability test: outputs I_A and ω observe each other → full-order (2) parity space possible. W (10.52) chosen for **structured residuals**: r1 ⊥ load M_L, r2 ⊥ voltage input, r3 ⊥ speed ω, r4 ⊥ current I_A [decoupling pairing as printed, OCR risky]. Residuals equal Example 10.3 up to sign (r_i = −r_yi). Additive fault in measured signals or M_L → **all residuals deflect except the decoupled one**.
- Brush-drop compensation does not spoil the residual structure (magnitude small). R_A and M_Fv are **temperature-dependent** → Fig 20.3 (temperature → R_A → residual r1 bias) → use **adaptive parity equations** (Sec 10.5).
- Sensitivity check on r1, r2 (they contain all parameters/signals): residual noise of r1 ~ |..| V [OCR magnitude lost] at I_A = 3 A → a resistance change must exceed **≈ 0.3 Ω** to deflect r1 significantly → track R_A and M_Fv by single-parameter estimation (Sec 10.5), forgetting factor λ = 0.99.
#### 20.1.3 Parameter estimation
- ODEs in regression form (20.7)-(20.9 simplified form, process coefficients; [formulas not decoded]). Method **DSFI** = Discrete Square Root Filtering in Information Form [20.6], forgetting factor λ = 0.99 → θ̂_i, process coefficients via (20.9).
- Idle running (M_L = 0): standard deviations of process coefficients **2% < σ_θ < 6.5%** [20.3].
#### 20.1.4 Fault detection results
- Five fault kinds, artificially injected as **steps at t_f = 0.5 s** [20.2]; residuals normalized by their thresholds → **|r|>1 = detection**. Cases a-d,f excited by **PRBS on armature voltage** U_A (required for dynamic parameter estimation); case e constant input. Fig 20.4 time histories.
  - a) **voltage-sensor gain fault**: deflects r1 (and r3,r4) but NOT r2 (decoupled from U_A); parameter estimates show INCORRECT changes of R_A, L_A, Ψ (sensor gain not modeled).
  - b) **speed-sensor offset**: deflects r1, r2, r4 but NOT the residual independent of ω (the r2/r3 subscripts are OCR-mangled in print); Ψ estimate changes incorrectly [reconstructed].
  - c) **multiplicative R_A change**: estimate R_A tracks correctly; residuals increase variance drastically and (incorrectly) cross thresholds.
  - d) **inertia J change**: estimate J correct; all residuals except one (subscript OCR-lost; Table 20.2 ΔJ-row shows that residual as "0") cross thresholds via variance.
  - e) **same R_A fault with constant input**: R_A estimate does NOT converge; parity residuals r? keep changed mean with large variance → shows excitation requirement.
  - f) **brush fault**: increases R_A AND L_A but not Ψ; residuals increase variance.
- Table 20.2 fault-symptom matrix (PRBS excitation; legend: + positive deflection, ++ strong, 0 none, −/−− negative, special symbol = increased variance [legend OCR shows "+ increased variance", glyph lost]). Table OCR heavily garbled — rows cover faults ΔR_A, brush fault, ΔJ, ΔM_Fv, voltage-sensor gain, speed-sensor offset, current-sensor fault vs symptoms ΔR_A/ΔL_A/ΔΨ/ΔJ/ΔM_Fv + r1..r4; cell-by-cell recovery unreliable, so rely on the a)-f) prose readings above [OCR?].
- Conclusions: 1) **additive faults** (sensor offsets) well caught by parity equations — fast, some need no excitation, but large variance if model mismatch. 2) **multiplicative faults** well caught by parameter estimation, even small; slower but smoothed (regression); REQUIRES input excitation. → **combine both** (Sec 14.3, Fig 14.1): parity equations as always-on watchdog; if unclear, start parameter estimation, inject a few seconds of dynamic test signal if needed. Servo systems already dynamic → continuous parameter estimation with supervision [20.6].
- Big win: continuously estimate armature resistance (single-parameter estimation on parity equation) to track temperature-dependent R_A [20.3],[20.4]; plus **adaptive thresholds** for model uncertainty (Sec 7.5).
#### 20.1.5 Fault diagnosis with SELECT (neuro-fuzzy, [20.1])
- **Symptoms (22 total)**: (i) windowed sums of |U_A|, |I_A|, |ω| (3); (ii) mean + std dev of the four residuals r1..r4 (and output residual σ?; list OCR-truncated) (≈8); (iii) **8 parameter-estimate deviations** from nominal, normalized, e.g. ΔR_A1 = (R_A,nom − R_A,est)/R_A,nom — index = which parity equation the estimate used (ΔR_A1, ΔL_A1?, ΔJ2, ΔJ3, ΔM_F2, ΔM_F3 pattern [subscript list OCR-mangled]); (iv) **2 estimation-quality symptoms**: recursive estimation variances σ_est,Ψ and σ_est,MF — fluctuating estimates ⇒ estimation-equation structure no longer valid ⇒ structural change detected.
- 14 fault situations on the rig; SELECT tree **learned from experimental fault data**: 10–50 test-cycle measurements per fault case, each run = one point in symptom space; **training set total = 140 experiments**; membership functions via **degressive fuzzy-c-means**; prior knowledge used to structure for transparency/interpretability.
- **Structural-knowledge philosophy**: use obvious rules (windowed sums → broken sensor cable); choose symptom subsets for robustness (environmental/wear effects unlearnable from limited data → systems that work only in lab); group similar faults → **hierarchical diagnosis**: first classify meta-classes C_i, then separate within; meta-class hierarchy needs ≥ q = m−1? decisions d_j [OCR "q = m-+r" garbled] with symptom subsets S_i ⊆ S; SELECT yields p parameters, much fewer than a parallel network structure (which converges slower, ill-conditioned optimization). Detailed rule knowledge can be added on top.
- **14 fault situations (classes)**: ΔR_A, ΔL_A (rotor/inductance change); broken rotor wiring F_V?; failure of one of the **four brushes** F_B; increased bearing friction F_F; **offset** on voltage/current/speed sensor (F_O,UA / F_O,IA / F_O,ω); **gain change** of voltage/current/speed sensor (F_G,UA / F_G,IA / F_G,ω); **complete sensor failure** voltage/current/speed (F_Y,UA / F_Y,IA / F_Y,ω) [symbols OCR-approximate].
- Result structure (Fig 20.5): hierarchical tree of shaded blocks = meta-classes, each branch = fuzzy rule learned by SELECT; within meta-class a classification tree picks the individual fault from symptom subset S_i. **98% classification rate in cross-validation**; performs well on new experiments (robustness from simple built-in knowledge); high transparency → transferable to other motors.
- Meta-class design rationale: (C1) three total sensor breakdowns — strong effect on ALL symptoms, separated by the **3 windowed sums** (S1); motor = electrical + mechanical parts → C2 (electrical) and C3 (mechanical) with symptom subsets S2/S3 = residuals + parameter deviations relevant to that domain; **do NOT diagnose electrical faults with mechanical parameter estimates** (S2 excludes ΔJ2, ΔJ3, ΔM_F2, ΔM_F3 — cross-influences misleading/unreliable).
- Example rules (20.14) distinguishing electrical faults [OCR-mangled, gist]: r1 small AND ΔL_A strongly negative → L_A fault; r1 small AND ΔL_A medium → R_A?; r1 small AND ΔL_A large → wiring fault; r2 not small → current-sensor offset; r1 small → current-sensor gain; r1 large AND σ_est,Ψ not small → voltage-sensor offset; else voltage-sensor gain fault. Relevance indices of premises omitted.
  - Insight: **r1 is the workhorse discriminator** (used in most rules). ΔL_A (estimated from 4th parity residual) distinguishes inductance fault by strongly negative value (Fig 20.6); rig only allowed fixed −50% inductance deviation → rules can be manually extended for positive changes (+ adapted membership functions).
  - **σ_est,Ψ distinguishes offset vs gain sensor faults**: offset changes the STRUCTURE of the estimation equation (large σ_est), gain only changes parameters (equation stays valid) — 6th rule logic.
- **Relation to fault trees (d)**: reverse the decision hierarchy → fuzzy **fault tree per fault** (Fig 20.7, e.g. increased friction); intermediate nodes ("Mechanical Fault") become fault-tree events; redundant but intuitive representation for understanding/visualizing.
- **Computational demands (e)**: most time-critical = continuous-time residuals needing state-variable filters (hard in fixed-point arithmetic; discrete-time residual variant exists [20.9]). Diagnosis only runs when detection thresholds violated → not time-critical, can be a background job in the motor controller; floating-point ops (SELECT neuron exp) doable on fixed-point via lookup tables. Diagnosis time ≪ human response time → computation not a real issue; safety-critical actions taken at threshold violation BEFORE diagnosis completes.
- Sec 20.1 summary: 14 faults detectable from **only 3 measured signals** by combining parity equations + parameter estimation; SELECT diagnoses all with **98% correct classification**.

### Ch20.2 Electrical throttle valve actuator (lines 8872-8997)
#### Context + 20.2.1 setup
- Automotive actuator (SI engines): controls air mass flow through intake manifold; embedded in engine/traction/velocity control; must survive wide temperature range, vibrations, signal/power disturbances; friction + temperature-varying parameters make fast precise positioning + reliability hard.
- Hardware (Fig 20.8): PMDC motor + gear turns throttle valve against **closing torque of helical spring**; PWM armature voltage U_A, measured armature current I_A; angular position φ_x **redundantly measured by two potentiometers** in range 0..90° (cf. 19.2 doubled slider).
- Model (Fig 20.9): gear = proportional factor with reduction ratio i [20.8],[20.9]; **inductance neglected** (electrical time const ≈ 1 ms ≪ mechanical); parameters: R_A, flux Ψ, inertia J, viscous friction M_Fv, spring constant c_F; disturbance torque M_r = spring pretension + external load torques. Mechanical subsystem hard to model precisely (several nonlinear effects); model above the **limp-home position φ_0** given by (formula not decoded). Symptom generation = parameter estimation + parity equations combination.
#### 20.2.2 Parameter estimation
- **Two recursive estimators**: one electrical subsystem, one mechanical (Fig 20.10); data/parameter vectors per subsystem [formulas not decoded]; extra constant **G_sim in the regression models additive (sensor) faults**; all physical process coefficients recoverable uniquely; derivatives ẋ, ẍ via state variable filter. Method: **RLS with UD-factorization** (Sec 9.2.3).
- Estimation **switched off at low speed** |ω_x| < ω_min to avoid strongly nonlinear friction at slow motion. Sampling time **T_0 = 6 ms**.
- PRBS excitation at position-controller setpoint: electrical parameters converge very fast; injecting an **R_A increase**: estimate R_A rises while Ψ and G_sim stay constant as expected (Fig 20.11). Mechanical estimates J, M_F1, M_F2 converge fast; **spring constant c_F needs ~3 s and has larger variance** (Fig 20.12).
- **Table 20.3** process-parameter deviations per fault (legend: 0 no significant change, + large increase, − large decrease; cells OCR-garbled, patterns below are indicative [OCR?]): F1 incr. spring pretension, F2 decr. spring pretension, F3 commutator shortcut, F4 armature winding shortcut, F5 armature winding break, F6 added series resistance, F7 added parallel resistance, F8 increased gear friction, F9-F11 offset faults U_A/I_A/φ_x, F12-F14 scale (gain) faults U_A/I_A/φ_x — vs estimates ΔR_A, ΔΨ, ΔG_sim, ΔJ, Δc_F, ΔM_F1/ΔM_F2, ΔM_r. Text verdict: **all faults except F1, F2, F11 show distinct symptom patterns**; parametric faults F3-F8 isolate better than sensor offset faults (F11 offset φ_x vs F14 scale φ_x collide: both −/+, not isolable by parameter symptoms alone).
#### 20.2.3 Parity equations
- Unlike the DC motor, the throttle's mechanical load (gear + high-pretension helical spring + friction at bearings/gear/spring adjustment) could **not be modeled well enough** for parity equations → residuals with too large variance [20.9]. Final design: parity approach limited to the **electrical subsystem only**, one residual r1(t) [formula not decoded], using φ_x from potentiometer 1; ẏ_x from state-variable filter, which also low-pass filters U_A, I_A.
- Residual r1 deflects for **offset faults of sensors U_A, I_A, y_x** and **parameter changes of R_A, Ψ**; residuals normalized to threshold; faults injected at t = 1 s → threshold crossed after **≈ 200 ms**; angle-sensor offset only briefly overshoots threshold (bad for detection); parameter changes → increased variance. Fig 20.13 cases: a fault-free, b R_A +20%, c 20% offset on throttle angle, d 20% gain change of throttle angle, PRBS excitation.
- Temperature/load drift after **30 min continuous operation: R_A +50%, Ψ −10%** → adaptive parity equations (Sec 10.5) track R_A and via it Ψ → smaller residual variance at small extra computational effort [20.9].
- Additional residual **r2 = difference between the two position sensors** feeds a sensor fault-tolerant scheme [20.5] (ties back to Fig 19.1b duplex w/ self-detection).
#### 20.2.4 Diagnostic equipment for quality control
- End-of-assembling-line test rig (Fig 20.14): power electronics + online-coupled DSP + host PC [20.10]; throttle disconnected from engine, special test cycle possible.
- Test cycle (Fig 20.15): **5 phases, total 9.4 s**. Phase 1ff: open-loop feedforward → basic faults (open armature circuit, short circuits, sensor offsets). From **phase 4**: closed-loop → operating range + some mechanical parameters. **Phase 5**: dynamic PRBS on position setpoint → estimate ALL electrical + mechanical parameters. **Fuzzy rule-based diagnosis: 38 different faults detected from 30 generated symptoms**.
#### Ch20.2 summary
- Three measured signals need combination of **limit checking + parameter estimation + one parity equation**; parameter estimation gives deep diagnosis; parity equations viable only for the electrical part (mech subsystem unmodellable) — the regression's inherent error-reduction made comprehensive diagnosis possible.

## Isermann Ch21-23 — Case Studies (pump-tank, suspension) + Terminology

### Ch21 Fault detection and diagnosis of a centrifugal pump-pipe-system (9000-9183)

**Testbed (21.1)**
- Centrifugal pump + pipe + tank over wide operating range; pump driven by inverter-fed speed-variable squirrel-cage induction motor, field-oriented speed control.
- Hardware: AC motor Siemens 1LA 5090-2AA, 1.5 kW, 2900 rpm; frequency converter Lust MC 7404; centrifugal pump Hilge, Hmax = 130 m, Vmax = 14 m3/h, Pmax = 5.5 kW. [OCR: caption says "circular pump", "Vinax"; read as centrifugal/Vmax]
- Sensors: stator current vector is = (isd, isq) transformed to rotor-flux frame; torque M = kT*isq with kT from nameplate; p1 inlet, p2 outlet, Dp = p2-p1, pump speed w, volume flow V. Pump head H = Dp/(rho*g).
- [21.4],[21.2] motor-current/torque reconstruction; modern frequency converter can reconstruct motor torque without additional sensors.

**Models (21.2)**
- Theoretically derived centrifugal-pump equations ([21.3]) adapted to plant; simplified since V ~ proportional to w and viscous friction neglected, with Dp = rho*g*H: static pump model (21.8), inverse pump model (21.9), dynamic pipe model (21.10) with ag = l/(g*A) (l pipe length, A cross section). [all formulas not-decoded by OCR; structure from prose]
- Models agree with [21.1] for a larger pump-pipe system. Signal flow diagram Fig 21.3.

**Residual generation (21.3a: measure i, w, Dp, V)**
- 4 nonlinear (dynamic) parity residuals: r1,r2,r3 = output residuals comparing measured Dp(k), V(k) with model outputs (static pump / dynamic pipe / pipe-pump models); r4 = input residual: measured motor torque vs inverse-pump-model load torque. r2,r3 include first-order flow-sensor dynamics. Sampling Ts = 10 ms.
- Parameters wj from physical data or least-squares on isd,w,Dp,V; strongly speed-dependent at low speed -> multi-model: LOLIMOT local linear model network, wj(w) i=1..10, 3 local models, identified with APRBS (amplitude-modulated PRBS) excitation over whole operating range; excellent reconstruction (Fig 21.5).
- Parity residuals run in normal operation without excitation; adaptive thresholds = constant + term driven by high-pass-filtered speed w (raises threshold on speed transients) [21.5].

**Faults seeded (7 kinds)**
- Sensor offsets: w, V, p1, p2; increased flow resistance (closing valve downstream of pump); cavitation (closing valve upstream of pump); increased bearing friction (removing grease, adding iron deposits); defect impeller (one channel between vanes closed with silicon); sealing-gap losses (opening bypass valve); leakage between pump and flow measurement.

**Results**
- Parity-only: all faults detectable; strongly isolable: sensor offsets, sealing-gap losses, increased bearing friction. Weakly/not isolable: flow resistance increase, cavitation, impeller defect.
- Parameter estimation (RLS on (21.8)-(21.10)) with APRBS excitation: changes of physically defined parameters -> ALL faults become isolable/diagnosable (Table 21.1; table itself badly rotated-OCR garbled [OCR?]).
- Reduced setup (21.3b, no Dp/V sensors): r4 from w + motor current isg detects sensor fault in w and some pump faults; extra parameter estimation of J, M_m0, M2 (21.8) isolates some more.
- Larger plant [21.1]: P = 3.3 kW, V = 150 m3/h, circulation loop with two heat exchangers, two flow meters -> 6 residuals + 4 parameter estimates + 2 residual variances = 13 symptoms -> diagnose 11 different faults (sensor/pump/pipe). Symptoms trained 20 fuzzy rules via SELECT (Sec 17.3.5) -> 100% classification accuracy.

**Sensor-configuration ladder (Table 21.2: detectability/diagnosability vs sensor set)**
- Minimal (torque M from converter + speed w): detects few faults, none diagnosable. Adding p1,p2 (or Dp): many more detectable AND diagnosable. Adding flow sensor V: little effect on detectable count, but considerably increases diagnosable faults.
- Faults listed: total breakdown, defective bladed wheel, increased shaft/motor friction, sensor faults w/V/p1,p2, decreased/increased flow resistance, cavitation via pressure reduction, insufficient de-ventilation of sensors p1,p2 / V. Parenthesized = difficult but not impossible (setup-dependent). Faults at converter itself and other motor electrical faults omitted. [cell marks X/(x)/garbled; direction legible from prose + column headers]
- Bottom line: model-based detection feasible with 3-4 sensors; diagnosis improves considerably with one more (flow). Nonlinear parity eqs cover some additive faults; parameter estimation gives much deeper insight, esp. for parametric (multiplicative) faults; best coverage = combine both.

### Ch22 Fault detection and diagnosis of an automotive suspension and the tire pressures (9184-9362)

**Model & measurement concept (22.1)**
- Goal: diagnosis either at a service station / technical inspection or during driving; use only easy-measurable, on-board-available variables and little a priori car-type knowledge: vertical body accel zB_dd, wheel accel zW_dd, suspension deflection zw - zB. Wheel damping small, usually neglected.
- Quarter-car model, force-balance eqs (22.1),(22.2) [formulas not decoded]. Symbols: cP body spring stiffness, cw tire stiffness, mB body mass, dG body/damper damping coeff, r road displacement, Fp damper force, Fs spring+damper force, Fw wheel force, Fc Coulomb friction, f0 resonance freq.
- Test rig: quarter-car rig of IAT, TU Darmstadt with continuously adjustable damper (magnetic valve opens/closes a bypass); built for semi-active parameter-adaptive suspension control [22.2].

**Parameter estimation on rig (22.2)**
- Damper force-velocity curve nonlinear, degressive, piston-direction dependent, + Coulomb friction; piecewise-linearize into m sections of piston velocity (7-section eq 22.3; figures use 4 sections, 2 per direction): estimates dg_i per section + Fc_i Coulomb forces.
- Inputs: body accel zB_dd + suspension deflection (velocity by numerical differentiation); either mB or cP must be known a priori. Tire stiffness cw estimable via (22.4) but needs road-wheel distance r - zw -> only feasible on test stand, too costly on-board.
- Rising valve current opens bypass -> damping sinks; estimated damping curves distinguishable across currents -> worn damper = changed curve = detectable.
- Table 22.1 (influence of faults on parameter estimates; + inc / - dec / 0 none): process faults (friction, damping, spring stiffness), sensor faults (offset zB_dd, offset zw-zB, gain zB_dd, gain zw-zB). Each fault has a distinct estimate pattern -> ALL parametric faults strongly isolable EXCEPT sensor offset faults (no clean pattern). [table cells badly OCR-garbled; rows/names legible, signs partially reconstructed from caption + prose]

**Parity equations on rig (22.3)**
- No permanent excitation, less computation, but shallower insight -> strategy: supervise online with parity eqs, run parameter estimation only after detection (Sec 14.3, [22.10]).
- z-domain transfer of (22.1) -> residual (22.7); params a_i, b_i via z-transform or discrete-time estimation on fault-free process.
- Experiments: 0.1 V offset (~3% of max) added to body accel sensor at t=5 s -> residual/threshold violates immediately, BUT cannot tell which sensor (deflection vs accel) is at fault. 20% gain fault -> only the VARIANCE of residual changes (slow detection via variance only). Same for wheel accel + deflection channels. These sensors are in series production of semi-active shock absorbers.
- Conclusion: sensor-fault detection possible (process params constant), diagnosis needs combination with parameter estimation patterns (Table 22.1).

**Driving vehicle (22.4)**
- Opel Omega (medium class), instrumented: body + wheel vertical accels, suspension deflections; rear-axle dampers switchable in 3 steps; drive over 2 cm boards at ~30 km/h.
- Estimated damping coefficients converge after ~2.5 s; within ~10% of directly measured values; 3 settings separable; compression vs rebound asymmetry visible (weaker than direct measurement).

**Highway fault detection (22.5), real measurements [22.1]**
- Damper setting switched at t = 30/60/90/120 s (0-30 s soft; 30-60 & 90-120 s medium = normal; 60-90 & 120-150 s hard). Deflection derivative from state variable filter.
- RLS with exponential forgetting: very good; adapts to new damping setting in ~10 s.
- PCA (Ch13) alternative: reference data matrix X trained in normal (medium) windows; X = deflection + body accel at 4 corners + roll/pitch/yaw rates + longitudinal/lateral/vertical accel + LAGGED deflections/accels (k-1, k-2, all 4 suspensions) = 30 variables; 24 principal components sufficient.
- T^2 statistic over whole run: during abnormal windows (soft/hard) exceeds threshold only occasionally -> detected, and no false alarms during normal windows. Overall RLS better than PCA. Semi-active/active suspension survey in [22.3].

**Tire pressure supervision via spectral analysis (22.6)**
- Only wheel vertical accel needed (body vibration band well below wheel band -> simplified model Fig 22.11); tire stiffness cw drops with pressure loss -> wheel resonance frequency f1 drops.
- f1 estimated by AR-parameter-based frequency estimation (Sec 8.1.6). Test rig Table 22.2: f1 = 12.23/12.39/12.56/12.7/12.85/12.91 Hz increasing with pressure [pressure row OCR-garbled; freq row legible]. Wideband excitation needed for good results.
- Autobahn: accelerometer 200 Hz sampling; pressure set 2.0 bar then reduced to 1.5 bar; f1 wanders ~0.5 Hz but low-pressure values always below normal. Front-minus-rear f1 difference reduces road-excitation variation and increases margin, but detects only RELATIVE changes (equal loss on both tires undetectable) -> combine both methods.
- Detection limit ~0.4 bar loss -> slow punctures detectable at little computational cost; body-accel variant in [22.8],[22.5]; combine with wheel-speed difference (lower pressure -> higher wheel speed), no direct TPMS sensors; direct/indirect TPM survey [22.4].

**Ch22 summary**: parameter estimation best suited (unique estimate patterns isolate several faults); parity eqs detect (e.g., sensor offsets) but cannot diagnose; combination recommended; tire pressure supervision via wheel-accel vibration analysis, best combined with wheel-speed differences.

### Ch23 Appendix (9363-~9867) — terminology + math/toolbox appendices

**23.1 Terminology in fault detection and diagnosis (9367-9443)** — the book's own vocabulary sheet; definitions from the IFAC TC SAFEPROCESS coordinated action, published in [23.8]; also DIN / VDI/VDE Richtlinien (see refs list 9431-9443).
- 1) States and signals:
  - Fault: unpermitted deviation of at least one characteristic property of the system.
  - Failure: permanent interruption of a system's ability to perform a required function under specified operating conditions.
  - Malfunction: intermittent irregularity in fulfilment of a system's desired function.
  - Error: deviation between a computed value (of an output variable) and the true, specified or theoretically correct value.
  - Disturbance: unknown (and uncontrolled) input acting on a system.
  - Perturbation: input acting on a system causing a temporary departure from steady state.
  - Residual: fault indicator based on deviations between measurements and model-equation-based calculations.
  - Symptom: change of an observable quantity from normal behavior.
- 2) Functions (pipeline: detection -> isolation -> identification, all inside diagnosis):
  - Fault detection: determination of faults present in a system and time of detection.
  - Fault isolation: determination of kind, location, time of detection of a fault by evaluating symptoms; follows detection.
  - Fault identification: determination of size and time-variant behavior of a fault; follows isolation.
  - Fault diagnosis: determination of kind, size, location, time by evaluating symptoms; follows detection; includes detection + isolation + identification.
  - Monitoring: continuous real-time task of determining possible conditions of a physical system, recognizing and indicating anomalies of behavior.
  - Supervision: monitoring + taking appropriate actions to maintain operation in case of faults.
  - Protection: means by which potentially dangerous system behavior is suppressed if possible, or consequences of dangerous behavior avoided.
- 3) Models:
  - Quantitative model: static/dynamic relations among system variables and parameters in quantitative mathematical terms.
  - Qualitative model: same relations in qualitative terms such as causalities or if-then rules.
  - Diagnostic model: set of static/dynamic relations linking specific input variables - the symptoms - to specific output variables - the faults.
  - Analytical redundancy: use of two, not necessarily identical, ways to determine a quantity where one way uses a mathematical process model in analytical form [definition truncated mid-sentence in OCR; intended completion "the other (usually) a measurement" — flag as not verbatim].
- 4) System properties:
  - Reliability: ability to perform a required function under stated conditions, within a given scope, during a given period; measure MTTF = mean time to failure, MTTF = 1/Lambda (Lambda = failure rate, e.g. failures/h).
  - Safety: ability of a system not to cause danger for persons, equipment, or environment.
  - Availability: probability that a system/equipment operates satisfactorily and effectively at any point in time; A = MTTF/(MTTF+MTTR); MTTR = mean time to repair = 1/mu (mu = rate of repair). [formula OCR'd as heading 'A= <MTTF MTTF+MTTR'; reconstructed fraction]
- References on terminology (9431-9443): DIN 25424 (fault tree analysis), DIN 40041/40042 (reliability EE/devices), DIN 31051 (maintenance), DIN 55350 (quality/statistics terms), IFIP WG 10.4 (Como 1983), Laprie 1983 (dependability: faults/errors/failures), VDI 3541/3691, ASQC RAM dictionary, Robinson 1982.

**23.2 State variable filtering to obtain signal derivatives (9445-9455)**
- Need y_dot(t), y_ddot(t)... from noisy y(t) (parameter estimation for continuous models, residual eqs). Numerical differentiation + interpolation (splines, Newton) only for very small noise.
- State variable filter (SVF) [23.21]: low-pass that outputs all derivatives while filtering disturbance; filter parameters fi nearly free to choose; Butterworth design recommended [23.16]. Alternative: FIR filters convolving derivatives of a low-pass impulse response with the signal [23.14],[23.11],[23.9].

**23.3 Fuzzy logic - short introduction (9457-9543)** (compiled by D. Fussel [23.3]; Zadeh-style multi-valued logic simulating human reasoning)
- Fuzzy sets: gradual set membership vs classical 0/1; linguistic terms ("low/medium/high") are highly application-specific; example 90 C: membership "low" > 0 and "medium" > 0, "high" = 0 (exact values in OCR-missing formula [OCR?]).
- Membership function mu_i in [0,1], shape arbitrary: trapezoidal/triangular typical; Gaussian/sigmoid/B-splines popular (continuously differentiable -> good for nonlinear optimization); usually designed to sum to 1 over input domain (interpretation as probabilities). Support = range where mu > 0. Union of fuzzy sets over a range = fuzzy variable; individual sets = attributes/terms/labels.
- Singleton membership: represents crisp data (mu = 1 at exact value, else 0).
- Inference with if-then rules: inputs = symptoms si, outputs = fault measures fi; linguistic rules R with premises combining linguistic statements via connectives (e.g. "symptom s_i increased").
- Pipeline: fuzzification (evaluate membership of each premise term) -> inference = premise evaluation + activation + accumulation -> (defuzzification).
- Premise evaluation operators: must match Boolean at crisp 0/1; options min/max, bounded difference/sum, algebraic product/sum; operator choice usually not vital: AND = min, OR = max, NOT = 1 - mu suffices (23.6).
- Activation: apply rule fulfillment to consequence (limiting or scaling/product; optional weight 0..1). Accumulation: max (or sum) over activated output membership functions per output variable.
- Defuzzification methods: maximum, center of gravity, mean of maximum; with singleton outputs simplifies to weighted sum of singletons.
- 23.3.2 Simplification for fault diagnosis: output is a FAULT MEASURE 0..1 (degree of possibility), not a continuous variable -> consequences reduce to singleton scaled by rule fulfillment; no output membership functions, no defuzzification (Fig 23.4). Fault measure ~ likelihood but NOT probability (no statistical evaluation of events).

**23.4 Estimation of physical parameters for dynamic processes (9545-9721)** (treatment per [23.5])
- Two-layer parameter view: input-output model parameters theta vs physical process coefficients p (the laws governing process dynamics). theta -> sufficient for control design; p required for: (a) non-measurable coefficients in natural sciences, (b) checking performance data, (c) online supervision & fault diagnosis, (d) quality control in manufacturing.
- Recipe: first estimate theta from u(t),y(t) (mature after 30 yrs; good convergence if structure fits, excitation sufficient, SISO parameter count ~4-6 max), then invert p = g^-1(theta) via known theoretical model relations.
- Three open questions: (a) identifiability of p; (b) which signals must be measured; (c) influence of a priori known p_i on variances of theta and p. [23.17] identifiability of biological compartment models via computer algebra; [23.1] two-step estimation with known physical parameters as boundary conditions (gradient method); [23.12]: model parameters = sums of products of process coefficients.
- 23.4.2 lumped-parameter model structure: balance + constitutive + phenomenological laws in unified form [23.7]; linear process, M measurable signals eta_j, N non-measurable xi_i, L elements; Laplace element equations -> matrix form (G,H); H triangularized to eliminate non-measurable signals -> input/output ODE -> continuous-time regression form; divide by u0 (all params times 1/u0, parameter count reduces by one).
- Elements of G,H contain process coefficients separately; after triangularization model parameters theta_r = algebraic functions of p; auxiliary zeta_k = abbreviations for existing products/singles of p1..pP (zeta-matrix form 23.20/23.22).
- Known-parameter split theta = (theta', theta''): LS estimate uses only unknown-parameter block with known-part signal derivatives moved to output side; 2nd-order simulation: convergence improves strongly if (i) the known parameter is the largest-variance one (alpha2 or b0), (ii) if several known, alpha2 or b0 must be among them, others must be known very precisely.
- 23.4.3 calculation of p: theta nonlinear algebraic in p -> no general inverse; 1st/2nd order models usually direct solution; higher order: successive resolution or computer algebra [23.20],[23.18]. Identifiability condition independent of method (implicit function theorem [23.15]): functional determinant |d theta / d p| != 0 near solution, requires l (number of process coefficients) = r (number of model parameters); example determinant evaluates to nonzero product form [formula not decoded].
- 23.4.4 example: second-order electrical circuit (R-L-C type network, Fig 23.6) [equations not decoded]; robot-axis example in [23.5].

**23.5 From parallel to hierarchical rule structures (9723-9829)** (compiled by D. Fussel [23.3])
- Goal: tree-structured sequential rule assembly for binary classification (classes C1/C2, crisp, no fuzzy transition here — fuzzy vocabulary reused as notation only) — more understandable and smaller than parallel rule bases.
- 23.5.1 parallel: grid partition of symptom space (s1,s2), attributes A11,A12,...; one Mamdani-prototype rule per shaded region (class C1; else C2 by complement, e.g. C1 = fault, C2 = fault-free). Multi-region class -> multiple rules; accumulation = union = OR (max operator; crisp case = boolean OR). Insight: accumulation of separate rules == OR merged into premises; AND shrinks selected region, OR unions regions covering class C.
- 23.5.2 hierarchical: decomposable region (axis-orthogonal pieces, some subregion depends on only one symptom) -> diagnosis meaning: some symptoms irrelevant for certain faults in certain symptom-space regions; problem intrinsically lower complexity than input dimensionality suggests.
- 6 parallel rules (23.32) collapse to 2 hierarchical rules (23.33): "IF s2 is A23 THEN C1; ELSEIF s1 is A12 THEN C1" — same picture. ELSE hides the complement of all rules above (parallel notation would need it spelled out); incomplete premises (input omitted) combine rule sets (R1..R4 -> R1*, R5,R6 -> R2*).
- Tree view (Fig 23.11): premises at nodes, conclusions at leaves; traverse root -> leaves, accumulate leaf fulfillments with OR. Complexity reduction not guaranteed: worst case chessboard-alternating class regions — trees no better than parallel base.
- SELECT method (Sec 17.3.5) = neuro-fuzzy system implementing hierarchical structures with upgrades: fuzzy transitions between class regions, continuous fuzzy-AND neuron for AND, boundaries not strictly axis-orthogonal, continuous rule fulfillments 0..1 -> whole structure always evaluated (no pruning).
- Concluding remarks (9831-9837): book covers signal-based + model-based FDD methods + fault-tolerant structures; method selection must match process properties (static/dynamic, excitation, model precision, computational expense, sampling time, diagnosis depth, costs); a certain fault coverage usually requires properly combining different methods. Applications volume "Fault diagnosis of technical processes - Applications -" (Springer, ~2006): A components (electrical drives/actuators, fluidic actuators), B machines & plants (pumps, pipeline leak detection, industrial robots, machine tools, heat exchangers, medical devices), C automotive (combustion engines, automobiles), D fault-tolerant (systems, fly-/drive-by-wire).

