# Chapter 9: Gain Scheduling

## Core Idea
When you know how dynamics move with operating conditions, preprogram the controller parameters as functions of a measured scheduling variable — the foremost industrial method for parameter variation, with no estimation loop and no feedback correction of the schedule, so its quality is exactly the quality of your offline design and interpolation.

## Frameworks Introduced
- **The principle (9.2)**: linear controller whose parameters are feedforward functions of an auxiliary variable w correlating with dynamics (Mach/altitude in flight control; production rate in process control since τ, L ∝ 1/throughput); design = tune at grid of operating points → table/function → validate transitions by simulation. No closed-loop feedback to the schedule.
- **Scheduling variable selection**: physics-driven; must reflect operating point; ideally simple parameter↔w relations.
- **Design toolbox (9.3)**:
  - **Actuator linearization**: insert approximate inverse f⁻¹ of static nonlinearity (valve u² example, two-line approximation) between controller and actuator — static compensation, not gain scheduling proper (no operating-point measurement).
  - **Auxiliary-variable scheduling**: e.g., tank with height-dependent cross-section A(h): linearized gain/T depend on h → PI parameters K ∝ √h-type functions of measured h.
  - **Time scaling by production rate**: schedule on throughput to normalize time scales.
  - **Interpolation**: linear interpolation between design points; more entries where parameter sensitivity is high.
  - **Implicit gain scheduling**: reparameterize the controller in the form used by direct STR (Ch 3.5) and schedule *those* coefficients on w — avoids solving design equations on-line.
- **Nonlinear transformations (9.4)**: change variables so the transformed system is operating-point independent — feedforward/feedback linearization: tank with square-root outflow (h² transform), ball-and-beam (x² transform), robot manipulators (computed torque); controller = transformation ∘ linear controller ∘ inverse transformation; transformations may need estimated states.
- **Applications (9.5)**: flight control (the standard technique), process control nonlinearities, split-range control as a special case.
- **Limitations**: open-loop compensation — a wrong schedule is not corrected; stability/performance only as good as quasi-LPV assumption (w slowly varying); design effort grows with grid size — mitigated by transformation-based designs.

## Key Concepts
- **Scheduling variable**: measured auxiliary signal correlated with dynamics changes.
- **Explicit vs implicit gain scheduling**: schedule raw gains vs schedule the reparameterized (STR-form) coefficients.
- **Feedback/feedforward linearization**: nonlinear coordinate + input transform making the loop linear — gain scheduling's analytic limit case.
- **Split-range control**: gain schedule on output range — degenerate case.
- **Quasi-LPV validity**: frozen-w analysis per point + slow-w assumption; fast w variation is outside the theory.

## Mental Models
- "Gain scheduling = the offline version of STR": same design at every operating point, computed once and tabulated instead of every sample.
- "Prefer transformation to table": if a change of variables linearizes the plant, one linear controller replaces the whole schedule.
- "The schedule is open-loop faith": no estimator checks it — sensor failure on w or unmodeled dynamics leaves the wrong controller silently engaged.
- "Adaptation complements scheduling": schedule to get in the right region fast, adapt to fine-tune (Ch 1 preview).

## Anti-patterns
- **Scheduling on a variable that doesn't dominate the dynamics** — table effort with no benefit; find the physics driver first.
- **Ignoring transitions between schedule points**: validation must cover moves across the grid, not just points.
- **Treating gain scheduling as guaranteed-stable**: no general stability theory for fast-varying w; simulate the nonlinear system.
- **Inverse-compensating a hysteresis/stiction actuator with a static inverse** — static inverses fix static nonlinearities only.

## Reference Tables

### Gain scheduling vs alternatives
| Situation | Best tool |
|---|---|
| Known dynamics vs measurable w | gain scheduling (table or implicit) |
| Known nonlinearity, invertible | transformation / inverse compensation |
| Unknown drift, no w | STR/MRAS |
| Both | schedule coarse + adapt fine |

## Key Takeaways
1. Gain scheduling is preprogrammed parameter adjustment on a measured operating variable — the dominant industrial technique for known parameter variation (flight control's standard).
2. Implicit gain scheduling (schedule STR-form coefficients) avoids on-line design solves.
3. Nonlinear transformations can eliminate the schedule entirely when the nonlinearity is invertible in the state coordinates.
4. Its weakness is structural: open-loop schedule, no self-correction — validate transitions and keep adaptation as backup.
5. Static actuator inverse compensation is a cheap first move but is not gain scheduling and doesn't fix dynamic nonlinearities.

## Connects To
- **Ch 1**: gain scheduling as the simplest adaptive scheme; scheduling + adaptation combo.
- **Ch 3/5**: reparameterization enabling implicit scheduling.
- **Ch 8**: auto-tuning builds the schedules experimentally.
- **Ch 12**: flight-control and process applications.
