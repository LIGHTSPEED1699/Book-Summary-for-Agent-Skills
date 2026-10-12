# Chapter 12: Fault Diagnosis of a Sensor Network

## Core Idea
Scale diagnosis from one loop to a network: a sensor net of interconnected dynamic subsystems (cascade, parallel, feedback) gets a *bank of Kalman filters*, each driven by a pair of signals — two consecutive sensor measurements, or a reference and a measurement. Each filter's residual is a reliable indicator of faults in exactly the path between its input pair; intersecting the verdicts of all filters detects, isolates, and *locates* the faulty subsystem or sensor. The model-based scheme is benchmarked against model-free alternatives (limit/visual/plausibility checking, ANN, fuzzy, ANFIS) on simulation and the two-tank rig.

## Frameworks Introduced
- **Sensor-network model (12.2)**: nodes = dynamic subsystem G_i (with disturbance w_i) + sensor as static gain k_si with delay z^{-τ_i} and noise v_i; closed-loop networks of cascade-connected G_i.
- **Bank of Kalman filters (12.3)**: one KF per signal pair; each filter models the transfer between its two inputs; residual ≠ white ⇒ fault in the intervening path.
- **Path analysis for isolation (12.1, 12.3)**: each filter votes on its path; the intersection of positive/negative votes pinpoints the faulty node — topology does the isolating, not just statistics.
- **Model-free alternatives (12.1)**: LVP checks, ANN, fuzzy logic, ANFIS (transparent if-then rules from labeled faulty/fault-free data); strengths (no model needed, fast) and costs (opacity, training data, rule engineering).
- **Distributed diagnosis requirements**: high correct-diagnosis probability, low false alarms, timely decisions, geographically distributed devices — the industrial spec sheet.
- **Head-to-head evaluation**: model-based KF bank vs ANN/ANFIS on the same data, including the physical two-tank system with sensor, actuator, and leakage faults.

## Key Concepts
- Residual-to-path mapping: the filter's input pair defines its jurisdiction; faults outside the path leave its residual white.
- Topology-aware isolation: the network's interconnection structure converts a set of binary residual tests into a unique fault location (when paths separate the candidates).
- Sensor = gain + delay + noise: the practical sensor model that makes path accounting work.
- Model-free methods detect fast but localize poorly (and need labeled fault data); model-based methods are transparent and precise but inherit model quality.
- ANFIS as the hybrid: universal approximation with readable rules — the book's honest middle ground.
- False-alarm control across many filters needs per-test thresholds (ch9's Bayes framing) — a bank multiplies the multiple-comparisons problem.

## Mental Models
- "One filter, one jurisdiction": each KF answers exactly one question — is anything wrong between my two inputs?
- "Let the topology convict": isolation is a set-cover/intersection argument over path verdicts.
- "Bank beats bank-shot": many cheap pairwise tests beat one monolithic observer for localization.
- "Model-free is not free": it trades model-building cost for data-labeling and opacity costs.

## Anti-patterns
- **Isolating by single-residual magnitude** — magnitude says "somewhere"; only the pattern across the bank says "where".
- **Ignoring path overlap degeneracies** — two faults can produce identical vote patterns; check isolability of the topology.
- **Deploying ANN diagnosis without fault-labeled data coverage** — unseen operating scenarios = silent misses.
- **Neglecting sensor delay in the path model** — k_si z^{-τ_i}: unmodeled delay colors residuals and fakes faults.

## Reference Tables
### Diagnosis classes
| Class | Tools | Strength | Cost |
|---|---|---|---|
| Model-based | KF bank + identification | transparent, precise localization | model building |
| Model-free | LVP, ANN, fuzzy, ANFIS | no model, fast detection | data labels, opacity |

### KF bank design
| Filter | Inputs | Jurisdiction |
|---|---|---|
| KF_i | y_i, y_{i+1} | path G_{i+1} + sensor |
| KF_r | r, y_1 | forward first block |

## Key Takeaways
A bank of pairwise Kalman filters + topology analysis gives detection, isolation, and location across an interconnected sensor network.
Residual-path jurisdiction is the design principle; isolability is a property of the network topology.
Model-based and model-free methods are complements: benchmark both on your data.

## Connects To
ch6's filter and ch9's residual statistics at every node; ch8's closed-loop sensor-net identification supplies the G_i models; ch11's influence-vector machinery is the single-loop ancestor; ch13 uses the network's identified models for soft sensing.
