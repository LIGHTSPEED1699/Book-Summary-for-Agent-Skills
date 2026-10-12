# Chapter 11: Fault Diagnosis of Physical Systems

## Core Idea
The ch9 pipeline deployed on real rigs, with the practical machinery made explicit: a five-step scheme — (1) choose diagnostic parameters that see every subsystem, (2) identify a fault-free nominal model, (3) design the Kalman filter (gain tuned online because Q, R are unknown) so the residual is white with minimal variance, (4) estimate influence vectors offline by perturbing diagnostic parameters one at a time (or via fault emulators when the true parameters are inaccessible), (5) decide fault/no-fault and isolate by Bayes multiple-hypothesis testing on residual correlations. The two-tank and position-control case studies expose the real-world wrinkles: feedback masks faults, and identified order ≠ physical order.

## Frameworks Introduced
- **Five-step diagnosis scheme (11.1)**: diagnostic parameters → identification → Kalman filter → influence vectors → Bayes decision; each step independently maintainable.
- **Fault emulators (11.2.1)**: cascade gain blocks (γ_l leakage, γ_a actuator, γ_s sensor) inject reproducible faults and enable offline influence-vector experiments on parameters you cannot otherwise perturb.
- **Influence vectors by LS fit (11.1)**: perturb one diagnostic parameter at a time; influence vector = least-squares fit of residual vs parameter variation — ch5's LS again.
- **Online Kalman gain tuning (11.1)**: with unknown Q, R, tune K until the residual is zero-mean white with minimal variance — whiteness as the tuning objective.
- **Bayes multiple-hypothesis diagnosis (11.1)**: detection + isolation as one Bayes framework with fault priors and decision costs; isolation = maximum correlation between measured residual and hypothesized residual signatures.
- **Diagnosability vs control performance tradeoff (11.2.2)**: aggressive closed-loop control restores tracking under faults — and simultaneously suppresses the residual signature, "compromising the performance of the fault diagnosis scheme."
- **Model-order discrepancy (11.2.2)**: physical 4th-order two-tank model identifies as 2nd-order + delay under low SNR — identification sees what the data can support, not what physics says.

## Key Concepts
- Diagnostic parameters must be *selectable for sensitivity*: they should move the residual measurably for the faults you care about.
- Fault emulators convert "untestable fault" into "offline experiment" — influence vectors need fault replay, not real failures.
- Residual whiteness is both the filter's tuning target and the no-fault null hypothesis — one statistic, two jobs.
- Feedback is a double agent: it generates useful data (ch8) and hides faults (this chapter); diagnosability analysis must account for the loop.
- Identified order is an SNR/excitation statement; don't force physical order onto weak data.

## Mental Models
- "Diagnosis is a designed experiment you run offline and read online": influence vectors offline, Bayes test online.
- "Whiteness is the null hypothesis": tune to it, test against it, alarm when it breaks.
- "Emulate before you diagnose": a fault you can replay is a fault you can isolate.
- "The controller is in the diagnosis loop": assess diagnosability under the actual control law.

## Anti-patterns
- **Judging diagnosis by tracking performance** — good tracking under fault is exactly what feedback guarantees; look at residuals.
- **Influence vectors from a single operating point** — sensitivity varies with operating condition; sweep it.
- **Forcing physical model order on identification** — low-SNR data can't support it; the 4→2 order collapse is information, not error.
- **Fixed Q, R guesses for the filter** — tune them (or K) to residual whiteness instead.

## Key Takeaways
The five-step scheme is the book's diagnosis product: parameters, model, filter, influence dictionary, Bayes decision.
Fault emulators + offline perturbation experiments build the influence dictionary on real hardware.
Closed-loop operation both enables data collection and suppresses fault signatures — diagnosability must be engineered.
Residual whiteness is the universal health statistic: tune to it, test with it.

## Connects To
ch9 supplies the theory (influence vectors, GLT/Bayes); ch6 the filter; ch7 the identification (high-order LS + reduction used here); ch10 the rigs; ch12 extends to sensor networks; ch13 adds fault-tolerant control on top.
