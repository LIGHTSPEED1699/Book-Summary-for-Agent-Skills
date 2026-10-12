# Chapter 11: Identification of Closed-loop System

## Core Idea
Subspace methods' standing assumption A3 (no feedback from states to inputs) fails exactly when the data are most valuable: normal closed-loop operation. The fix is the joint input-output approach: treat (u, y) as one joint stochastic process, identify the closed-loop system's model from it, and extract the plant — provided some external excitation (reference or probe) keeps the joint process sufficiently rich. Both ch10 CCA and ch9 ORT adapt: the input projection is replaced by an orthogonal decomposition of the joint process, and the state realization runs on the closed-loop Markov parameters.

## Frameworks Introduced
- **Why closed loop breaks the open-loop machinery (11.1-11.2)**: with feedback, U_p and the state sequence become correlated — Assumption 9.3 A3 fails; naive MOESP/ORT/CCA estimates are biased.
- **Joint input-output approach (11.2.2)**: the pair (u,y) under feedback is itself a jointly stationary process driven by (r, disturbances); identify a model of the joint process first (its "Youla-form" / pseudo-linear parametrization), then recover the plant from it.
- **Excitation requirement**: an external signal (reference r or probe) with sufficient rank/spectrum must enter the loop; pure regulation with only colored noise needs care (identifiability via known noise spectra).
- **Closed-loop CCA method (11.3)**: realize the joint input-output process by CCA of its past/future (11.3.1), then map the joint realization to the plant via the closed-loop Markov-parameter relations (11.3.2) — the "Closed-loop Identification - CCA Method" recipe.
- **Closed-loop ORT method (11.4)**: orthogonal decomposition of the joint process separates the exogenous excitation from the loop signals (11.4.1); realization of the closed-loop system then follows the ORT pattern (11.4.2).
- **Consistency and examples**: estimators remain consistent under the joint approach when the excitation condition holds.

## Key Concepts
- Feedback makes inputs "part of the system": the plant+controller closed loop is the object whose Markov parameters are directly identifiable from (u,y) data.
- Plant recovery: from the joint/closed-loop model, the plant follows by algebra (Youla/Koopman parametrization) once the controller is known, or jointly when unknown.
- The external-excitation condition replaces PE of the input: rank of the excitation spectrum must cover the needed order.
- Both CCA and ORT survive closed-loop with the same projection/SVD machinery — only the decomposition target changes (joint process, not input-vs-residual).
- Closed-loop data can be *better* than open-loop for the frequency region where the loop operates (excitation shaped by sensitivity functions).

## Mental Models
- "Identify what the data actually generate": closed-loop data generate the closed-loop process; identify that, then algebra out the plant.
- "Feedback is not noise, it's structure": the correlation between U_p and X_p is the thing to model, not project away.
- "Excitation is the new PE": without external richness, no method rescues identifiability — check the reference/probe spectrum first.
- "Two doors, one room": closed-loop CCA and closed-loop ORT are the same theorem with different projections, exactly as in ch9/ch10.

## Anti-patterns
- **Running open-loop subspace ID on closed-loop data** — biased; the A3 violation is not a technicality.
- **Identifying the plant without external excitation** — in pure regulation, plant and noise model trade off; identifiability needs known spectra or injected signals.
- **Forgetting controller knowledge in the plant-recovery step** — the algebraic extraction assumes the controller (or estimates it jointly); mismatch corrupts the plant.
- **Assuming closed-loop bias immunity** — the joint approach is consistent under its conditions, not magic; noise on the actuator/reference changes the bookkeeping.

## Reference Tables
### Open-loop vs closed-loop subspace ID
| Aspect | Open loop (ch9-10) | Closed loop (ch11) |
|---|---|---|
| Standing assumption | A3: no state→input feedback | joint process model |
| Input role | exogenous, PE | loop signal + external excitation |
| Object identified | plant directly | joint/closed-loop model → plant |
| Failure if ignored | none | bias |

### Closed-loop routes
| Method | Decomposition | Realization |
|---|---|---|
| CCA (11.3) | canonical variates of joint (u,y) past/future | joint model → plant map |
| ORT (11.4) | orthogonal split of exogenous vs loop | ORT on closed-loop Markov params |

## Key Takeaways
Closed-loop identification = identify the joint (u,y) process, then extract the plant algebraically; both CCA and ORT adapt cleanly.
External excitation (or known noise spectra) is the load-bearing identifiability condition.
The same projections/SVD/LS machinery serves everywhere — Part III's three chapters are one algorithm wearing three assumptions.

## Connects To
Closes Part III: ch9 (ORT), ch10 (CCA), ch11 (closed-loop versions of both); relies on ch4-8 stochastic realization throughout; Doraiswami ch8 covers closed-loop identification (two-stage/direct) from the practitioner's angle with the same motivation.
