# Patterns — Puig & Simani, Diagnosis and Fault-tolerant Control

## P1. Residual generation triad
**Problem**: need a fault indicator. **Pattern**: pick among (a) observers/estimators (fixed parametric model), (b) parity equations (fixed parametric/non-parametric), (c) identification/parameter estimation (adaptive models). Residual = measured − model-estimated quantity. **Rule**: only output estimation is needed, not full state reconstruction. **Anti-pattern**: chasing full-state accuracy when a scalar residual suffices.

## P2. Bank of estimators for isolation
**Problem**: which fault? **Pattern**: one estimator per fault hypothesis (Willsky hypothesis test); variants: excited by one output / all outputs / all-but-one (generalized observer supervising the excluded sensor). Isolation = which estimator's output deviates, or nearest directional signature. **Vol 2 upgrade**: bank of MISO **fault estimators** driven by I/O subsets chosen by a fault-sensitivity/FMEA study → direct magnitude estimates f̂, not just flags.

## P3. Robustness ladder (thresholds)
**Problem**: model uncertainty makes residuals nonzero without faults. **Pattern**, increasing formality: (1) fixed threshold Δr = ε·σfault-free; (2) **passive**: adaptive threshold ε(t) driven by u(t) tracking operating point; (3) **active**: represent modeling error as disturbance, decouple at design (UIO, H∞ filtering, mixed H−/H∞ gain tuning); (4) **set-based**: zonotopic residual envelope with LMI-guaranteed contraction — alarm only when measurement exits the predicted set. **Rule**: disturbances and faults are indistinguishable unless the disturbance structure is known or bounded.

## P4. Structural analysis before design
**Problem**: don't know what's detectable/isolable. **Pattern**: build structure graph → DM decomposition → M+ gives detectable faults; per-fault DM gives isolability matrix; MSO sets give minimal residual candidates; sensor placement changes the ceiling. **Payoff**: cheap combinatorial analysis that bounds any later design; also yields the test set to select from (exponentially many — selection needed).

## P5. Conflicts ≡ ARRs ≡ MSO ≡ Possible Conflicts
**Problem**: unifying symbolic (AI) and analytic (FDI) diagnosis. **Pattern**: Reiter CBD: minimal diagnoses = minimal hitting sets of minimal conflicts. For DAE dynamic models: compute MECs, causal-assign → MEM → Possible Conflict = executable monitor; PC detected ⇔ conflict asserted. **Use**: component-level, compositional, multiple-fault isolation; no exoneration (only rejection of inconsistent modes).

## P6. Set-membership robust FDI
**Problem**: unknown-but-bounded noise, want guarantees without statistics. **Pattern**: zonotopes throughout; design observer gain by LMI for P-radius contraction (robustness) and add fault-sensitivity LMI (H−) so residual center responds to sensor faults; alarm on interval violation. Quadruple-tank demo: robustness-only vs robustness+sensitivity designs.

## P7. Stochastic diagnosis as inverse problem
**Problem**: inherently uncertain plant, probabilistic answer wanted. **Pattern**: forward model y=ξ(φ,η); three routes — model-driven inversion (Bayes/MCMC/particle filters), data-driven pseudo-inverse classifier, hybrid surrogate (tune low-fidelity models with data, or augment equations with learned terms). **Rule**: model-driven interpretable + extensible; data-driven needs fault-distributed data; hybrid is the practical middle.

## P8. TS/LPV embedding as the LMI gateway
**Problem**: nonlinear plant but want linear robust/LMI machinery. **Pattern**: (a) TS via nonlinear embedding (factor summands, premise variables); (b) RNN → LPV via sector-bounded activation slopes; (c) quasi-LPV with scheduling on x̂ when the true decision variable is unmeasurable. Then: H∞ observers, PDC controllers, polytopic virtual sensors/actuators all apply. **Check**: convex combinations of Bi full rank (block P-matrix test) before dead-beat fault estimation.

## P9. Joint state + fault estimation observer
**Problem**: need f̂(t) online for compensation. **Pattern**: augment/learn: RPO for descriptor LPV (T1/T2 decomposition, learning matrix Γ, bounded ḟ); TS H∞ unknown-input observer (TD=0 decoupling); Gillijns–De Moor dead-beat for simultaneous actuator+sensor faults. **Anti-pattern**: assuming scheduling functions measurable when they depend on the state you're estimating.

## P10. Virtual sensor / virtual actuator reconfiguration
**Problem**: keep certified nominal controller+observer, survive sensor/actuator faults. **Pattern**: insert virtual block: sensor → static redistribution if rank condition holds, else dynamic gain M; actuator → redistribution over healthy actuators or dynamic gain N. Augmented system becomes block-triangular → **extended separation principle**: nominal loops untouched, add stable virtual dynamics. Design M, N by LMIs with pole-hierarchy specs; LPV version = vertex gains. **This is the book's flagship FTC architecture.**

## P11. Robust MPC with error models
**Problem**: constrained nonlinear control that must tolerate uncertainty/faults. **Pattern**: NN one-step predictor (MLP with external dynamics) + separately identified **error model** trained on the nominal model's realized errors; composite prediction; invariant-set machinery for constraint satisfaction; reconfigure by switching/re-identifying the prediction model after diagnosis.

## P12. Validate on a digital twin first
**Problem**: FTC on real plants is expensive/dangerous. **Pattern**: FMEA before designing fault estimators; high-fidelity simulation (digital twin) with sensory+historical data before deployment; sustainable-control task chain (sensing → control → test → cost/risk). **Rule**: any new control strategy is tested in detailed simulation models before the process.
