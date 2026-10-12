# Chapter 13: Soft Sensor

## Core Idea
The capstone pipeline: when the variable you must control is hard or slow to measure (composition, quality), build a *soft sensor* — identify a model relating it to easy measurements, run a Kalman filter to estimate it in real time, and close the loop with a robust (mixed-sensitivity H∞) controller designed on the augmented model with an explicit uncertainty model. Then make it fault-tolerant: the same residual machinery monitors model mismatch/status, and the Bayes decision strategy triggers accommodation. Identification, filtering, robust control, and diagnosis become one integrated system, demonstrated on simulation and a physical velocity control system.

## Frameworks Introduced
- **Soft sensor concept (13.1-13.4)**: estimate an unmeasured/important variable from identified models of the accessible channels + Kalman filtering; offline identification (high-order LS + reduction), online estimation.
- **Augmented model for control (13.5.2)**: plant + soft sensor + disturbance/noise models in one state-space form — the controller designs on the integrated object from ch1.
- **Uncertainty model (13.5.4)**: identification error/variation bounds the plant uncertainty — the bridge from identification quality to robust-control margins.
- **Mixed-sensitivity optimization (13.5.5-13.5.6)**: H∞ weighting on sensitivity/complementary sensitivity/control effort; state-space realization of the robust control system; performance vs robustness dial.
- **Closed-loop performance and stability under mismatch (13.5.3, 13.6.1)**: residual and model-mismatch analysis (ch6.7) quantifies what the identified model's error does to the loop.
- **Fault-tolerant layer (13.6.2-13.6.4)**: Bayes decision strategy on residuals for status monitoring; high-performance control continues, fault-tolerant control accommodates.
- **Evaluations (13.7-13.8)**: simulated soft-sensor system (offline ID → mixed-sensitivity design → performance/robustness → status monitoring) and the physical velocity control system.

## Key Concepts
- Soft sensing = estimation where sensors are absent: the identified model is the virtual sensor; the Kalman filter is its readout.
- Identification error is not an academic number — it becomes the uncertainty weight in the H∞ design; model quality sets achievable robustness.
- Mixed-sensitivity shaping: weights encode the spec (tracking, noise, effort); the identified model sits at the nominal point.
- Status monitoring rides on the same residual as diagnosis: one signal serves control (innovation), diagnosis (fault signature), and soft-sensor validity (model mismatch).
- Fault tolerance is layered, not woven in: monitor → decide (Bayes) → accommodate.
- The physical velocity-control demo closes the book's loop: model → identify → filter → control → monitor, all on real hardware.

## Mental Models
- "The best sensor is a model": where hardware fails (slow, expensive, hostile), estimate with an identified model + filter.
- "Uncertainty is inherited, not invented": robust-control weights should reflect what identification actually achieved.
- "One residual, three jobs": innovation for the filter, signature for diagnosis, validity flag for the soft sensor.
- "Integrate the models, then design once": the augmented model is the single source of truth for control and diagnosis.

## Anti-patterns
- **Soft sensor without validity monitoring** — model drift silently corrupts the estimate; the residual is the validity alarm.
- **Robust design with generic uncertainty** — ignore the identification-derived bound and the margins are fiction.
- **Soft-sensor model from open-loop tests only** — the loop changes excitation (ch8); identify where it runs.
- **Fault accommodation without decision costs** — Bayes framing sets when to switch modes; ad-hoc thresholds thrash.

## Reference Tables
### Soft sensor stack
| Layer | Object | Chapter |
|---|---|---|
| Virtual sensor | identified model | ch7-8 |
| Real-time estimate | Kalman filter | ch6 |
| Robust controller | mixed-sensitivity H∞ on augmented model | 13.5 |
| Status monitor | residual + Bayes test | ch9, 13.6 |

### Mixed-sensitivity knobs
| Weight | Controls |
|---|---|
| S (sensitivity) | tracking/disturbance |
| T (complementary) | noise, robustness |
| KS | control effort |

## Key Takeaways
Soft sensing turns identification + filtering into a virtual instrument; its validity is guarded by the same residual used for diagnosis.
Identification quality feeds robust-control uncertainty directly — the pipeline is only as strong as its model.
Fault-tolerant operation = continuous performance layer + Bayes-decision monitor + accommodation.
The book's whole toolkit composes: ch1 models → ch7-8 identification → ch6 filtering → ch9-12 diagnosis → ch13 integrated control.

## Connects To
Every prior chapter is a component here: ch1's augmented model, ch6's filter and mismatch theory, ch7-8's identification, ch9's Bayes decision, ch10-11's physical-rig practice. This is the book's integration chapter.
