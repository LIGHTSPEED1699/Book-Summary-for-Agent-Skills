# Chapter 8: Closed Loop Identification

## Core Idea
Most plant data come from loops that are already closed — you cannot stop the process to run open-loop tests. Closed-loop data break the identification assumptions (the input correlates with the noise via feedback), so the chapter builds the two practitioner routes: the two-stage approach (first identify a consistent auxiliary model of the reference-driven response, then identify the plant from the decorrelated signal) and the direct approach (identify the plant model jointly with the loop, using the Kalman-filter-based model as the consistent backbone). The motivating application is a closed-loop sensor network — estimating plant dynamics from data collected under feedback.

## Frameworks Introduced
- **Why feedback breaks identification (8.1-8.2)**: u contains a feedback image of y, hence of noise ⇒ regressor-noise correlation ⇒ LS/PEM bias (the same mechanism as ch7.10, now structurally guaranteed).
- **Kalman filter-based identification model (8.1.1)**: augment the plant with the disturbance/noise model and run the ch6 filter; the filter's innovations provide decorrelated quantities usable for consistent estimation under feedback.
- **Two-stage approach (8.2.1, 8.6)**: Stage I — identify the response driven by the external reference (consistent because the reference is exogenous); Stage II — identify the plant from the Stage-I predicted output vs input (regressors now decorrelated from noise).
- **Direct approach**: parametrize the closed-loop system and identify plant + noise jointly from closed-loop data.
- **Single-input multi-output (SIMO) model (8.3)**: subsystem and overall-system state-space models for networks where one actuator is sensed at many points; transfer-function model of the whole loop.
- **Evaluation on a simulated closed-loop sensor net (8.7)**: performance of the Stage-II scheme under realistic loop conditions.
- **Excitation accounting**: external reference/probe signals are the information source; identifiability requires their richness (mirrors Katayama ch11's condition).

## Key Concepts
- Feedback turns the input into a system output: the exogeneity assumption fails structurally, not accidentally.
- Two-stage logic = manufacture exogeneity: replace the contaminated regressor with a reference-driven prediction that is provably uncorrelated with the noise.
- The Kalman filter's innovation sequence is the decorrelation engine for the direct route.
- Closed-loop data are not "bad data": they concentrate excitation where the loop operates — good models where it matters, if the method respects the loop.
- SIMO structure matters for sensor networks: one input, many correlated outputs, shared identification.

## Mental Models
- "Find an exogenous handle": every closed-loop method is a search for something not contaminated by feedback (reference, probe, innovation) to hang the regression on.
- "Two stages beat one bad regression": a consistent intermediate estimate rescues the final one.
- "The loop is an experiment you didn't design": mine it for its shaped excitation rather than discarding the data.
- "Identify the loop, extract the plant": the Katayama joint input-output view — same theorem, this book's route is the filter-based one.

## Anti-patterns
- **Open-loop identification on closed-loop data** — structurally biased; the chapter's whole point.
- **Two-stage without Stage-I consistency** — garbage in, correlated garbage out.
- **No external excitation anywhere in the loop** — pure regulation with a single noise source is degenerate; identifiability needs richness.
- **Ignoring the controller model in direct approaches** — the loop model includes it; mismatch leaks into the plant estimate.

## Reference Tables
### Closed-loop routes
| Route | Decorrelation device | Needs |
|---|---|---|
| Two-stage | reference-driven prediction | external reference/probe |
| Direct (KF-based) | innovations of augmented filter | noise model + loop model |
| Joint (Katayama) | joint (u,y) process realization | external excitation |

### Bias sources under feedback
| Mechanism | Effect |
|---|---|
| u contains feedback of noise | regressor-noise correlation |
| Controller dynamics | colored loop signals |
| Weak reference | variance explosion |

## Key Takeaways
Feedback structurally violates exogeneity; consistent closed-loop ID manufactures decorrelation (two-stage prediction or filter innovations).
Closed-loop data are valuable — shaped excitation — when the method accounts for the loop.
External excitation richness is the identifiability condition, same as open-loop PE in spirit.

## Connects To
ch6's Kalman filter is the direct route's engine; ch7's bias appendix explains the failure mode; ch12's sensor-network diagnosis runs on these closed-loop models; Katayama ch11 is the theory twin (joint input-output CCA/ORT).
