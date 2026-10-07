# Chapter 8: Auto-Tuning

## Core Idea
General-purpose adaptation failed at "push-button" tuning because it lacked a priori time-scale knowledge — the fix is deliberate closed-loop experiments (relay feedback) that generate exactly the frequency information a PID needs, making auto-tuning a robust ballpark experiment rather than an adaptive scheme.

## Frameworks Introduced
- **Realistic PID implementation (8.2)**: u = f(K_c e + ∫(K_c/T_i)e dt + dI/dt) with: derivative on measurement only (no setpoint kick), derivative filter (N ≈ 10), anti-windup via tracking term (T_r resets integral on saturation), bumpless manual/auto switching. Tunables: K_c, T_i, T_d.
- **Open-loop transient methods (8.4)**: step response → first-order-plus-delay K, L, T (tangent or area methods: A_0 = KL; A_1 up to T+L gives T); **Ziegler-Nichols step method**: P: K_c = T/(aL); PI: 0.9T/(aL), T_i = 3.3L; PID: 1.2T/(aL), T_i = 2L, T_d = 0.5L (a = response slope); applicability test 0.1 < L/T < 0.6; ZN damping too low — modify constants.
- **Closed-loop relay feedback (8.5, the Åström-Hägglund relay auto-tuner)**: relay of amplitude d in feedback → limit cycle of amplitude a, period T_u; **harmonic balance**: relay describing function N(a) = 4d/(πa); oscillation condition G(jω_u)N(a) = −1 ⇒ **K_u = 4d/(πa)** (ultimate gain), ω_u = 2π/T_u — the experiment auto-generates a signal concentrated at ω_u, keeps integrating processes bounded, and is disturbance-robust.
- **ZN closed-loop method**: P: 0.5K_u; PI: 0.45K_u, T_i = 0.83T_u; PID: 0.6K_u, T_i = 0.5T_u, T_d = 0.125T_u — pairs naturally with relay measurement (relay auto-tuner: switch to relay, wait for stable limit cycle, compute, switch back).
- **Describing function method (8.6)**: N(a) for relay/hysteresis/other nonlinearities; limit cycles ⇔ G(jω) and −1/N(a) intersect in Nyquist plane; gives amplitude/frequency of self-oscillation — the analysis tool for both tuning and Ch 10's self-oscillating adaptive systems.
- **Frequency-based tuning (8.5 cont.)**: from (K_u, T_u) shape the loop: frequency response design with specified phase/magnitude margins (M_s ≈ 2) rather than ZN's aggressive constants.
- **Expert/pattern-recognition tuning**: observe normal-operation transients, estimate damping/period/static gain, rule-based adjustment (Foxboro/Fenwal) — tuning during operation without experiments.

## Key Concepts
- **Ultimate gain/period (K_u, T_u)**: the stability-boundary pair measured by relay experiment.
- **Describing function / harmonic balance**: fundamental-only analysis of nonlinear loops; relay N = 4d/(πa).
- **Push-button tuning**: relay auto-tuner as product feature (SattControl, Fisher-Rosemount).
- **Pre-tuning for adaptive systems**: auto-tuners supply the a priori time scales MRAS/STR need.
- **L/T applicability ratio**: decides ZN validity / dead-time compensation need.

## Mental Models
- "Tune where you'll operate": the relay forces the plant to speak at ω_u — the one frequency that matters for PID design.
- "Closed-loop experiments beat open-loop for tuning": bounded outputs, integrator-safe, disturbance-robust.
- "ZN constants are a starting point, not a spec": quarter-decay ZN loops are too oscillatory for most modern specs; back off via M_s-based rules.
- "Auto-tuning ≠ adaptation": one-shot experiment + fixed controller is simpler, verifiable, and covers most industrial loops; adaptivity is for drift you can't schedule.

## Anti-patterns
- **Deploying MRAS/STR without pre-tuning**: the historical failure — unknown time scales ⇒ wrong sampling/filtering ⇒ adaptation does more harm than none.
- **Open-loop step tests on integrating processes**: output runs away; use closed-loop relay.
- **Blind ZN PID constants**: quarter-amplitude decay spec = poorly damped by modern standards (M_s ≈ 2.7); check the closed-loop peak.
- **Relay tuning on systems with multiple unstable modes or strong asymmetry**: no unique limit cycle — harmonic balance assumptions fail.

## Reference Tables

### ZN tuning constants
| Method | P | PI | PID |
|---|---|---|---|
| Open-loop (K,L,T; a = L·slope/K) | T/(aL) | 0.9T/(aL), T_i=3.3L | 1.2T/(aL), T_i=2L, T_d=0.5L |
| Closed-loop (K_u,T_u) | 0.5K_u | 0.45K_u, T_i=0.83T_u | 0.6K_u, T_i=0.5T_u, T_d=0.125T_u |

### Relay auto-tuner facts
| Quantity | Formula |
|---|---|
| Relay describing function | N(a) = 4d/(πa) |
| Ultimate gain | K_u = 4d/(πa) |
| Oscillation condition | ∠G(jω_u) = −180°, \|G(jω_u)\| = 1/N(a) |

## Key Takeaways
1. Auto-tuning succeeded where general adaptation failed: a deliberate closed-loop experiment (relay) delivers the two numbers (K_u, T_u) that fix PID scales.
2. The relay experiment is self-designing: it generates energy exactly at the critical frequency and keeps the loop bounded.
3. ZN rules (both flavors) are the classic map from experiment to parameters — but their damping is aggressive; margin-based tuning is the modern upgrade.
4. Real PID implementations (derivative filter, anti-windup, bumpless transfer) are part of the tuning problem, not footnotes.
5. Auto-tuners double as pre-tuners: they supply the a priori time scales that MRAS/STR need to be safe.

## Connects To
- **Ch 2**: open-loop identification is a small special case of estimation theory.
- **Ch 9**: gain scheduling + auto-tuning = table built experimentally.
- **Ch 10**: describing functions reused for self-oscillating adaptive systems.
- **Ch 12**: auto-tuning products (SattControl, Yokogawa, Honeywell).
