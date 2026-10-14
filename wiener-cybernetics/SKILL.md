---
name: wiener-cybernetics
description: Apply Norbert Wiener's Cybernetics (1948 text + 1961 supplementary chapters) frameworks - feedback as the definition of purpose, information as negative entropy, the causal-operator stability criterion for servomechanisms, message-vs-noise filtering and prediction, binary/digital cost reasoning, redundancy and majority voting, brain-as-single-machine-run for habit and vicious circles, organizational communication and homeostasis, learning as second-order programming, coupled-oscillator self-organization - when designing or debugging control systems, agents, automation, organizational feedback loops, prediction/filtering, human-machine systems, or reasoning about machine purpose, learning, and risk.
---

# Cybernetics (Wiener) — Skill

Cybernetics = "the entire theory of control, communication, and statistical organization of the system." The whole book in one sentence: **purposeful behavior is feedback-regulated behavior, and its quantitative study is the study of messages, noise, and operators on the past.**

## The five load-bearing ideas
1. **Purpose = feedback.** A system acts purposively when its effector performance is monitored back and corrected against a criterion — "regulated by some measure of the amount by which it has not yet been accomplished." No animism, no introspection needed; ataxia and servos prove it.
2. **Information = negative entropy.** I = −Σ p log₂ p; a message is a member of a statistical ensemble; noise is an independent ensemble; the Maxwell demon pays for its information. Communication engineering = moving information through noise with causal operators.
3. **Causality constrains everything.** Physical operators act on the past only: ∫₀^∞ a(τ)f(t−τ)dτ. Stability of a feedback loop is decided by whether −1/λ lies inside the image curve A(iy) (Wiener's criterion, equivalent to Nyquist). Three cascaded lags defeat any single loop.
4. **The machine and the brain are the same relay logic** (all-or-none, binary, Boolean, memory, redundancy: "what I tell you three times is true") — but the brain is a machine that **never clears between runs**, so its pathology and its habit are traffic phenomena in an ever-accumulating memory.
5. **Learning = non-linear second-order feedback**: the fast loop acts with fixed valuations; the slow loop refits the valuations from recorded experience. Program it to what you actually want — machines are literal-minded (Monkey's Paw rule).

## Decision index
| Problem | Load |
|---|---|
| Is determinism/prediction even possible here? Probability foundations, Maxwell's demon | `chapters/01-newtonian-program.md` |
| Purpose, behaviorism, agent design, what "goal-directed" means operationally | `chapters/02-revisionism.md` |
| Information measure, entropy, noise, filtering, prediction, Wiener–Khinchin | `chapters/03-transmission-information.md` |
| Servo stability, oscillation, compensators, dither probing, homeostasis | `chapters/04-feedback-oscillation.md` |
| Digital vs analog, binary cost, redundancy, memory design, brain≈computer | `chapters/05-computing-nervous-system.md` |
| Pattern recognition, group invariance, sensory substitution; mental illness as traffic jam; media/org homeostasis, limits of social science, first chess-program sketch | `chapters/06-08-gestalt-psychopathology-society.md` |
| Learning machines, game AI, AI risk fables, self-reproducing transducers, brain waves, coupled oscillators | `chapters/09-10-supplementary-1961.md` |
| Terms and formulas | `glossary.md` · `cheatsheet.md` |
| Recurring moves across chapters | `patterns.md` |

## How to apply
Any control/agent/organization question: (1) draw the loop — sensor, criterion, effector, delay; (2) write the open-loop operator and count lags (≥3 → inner loops needed); (3) ask what ensemble the signal belongs to (prediction floor = noise spectrum); (4) check redundancy and the p^(1/n) compounding cliff across stages; (5) ask who owns the monitoring channel (org version of the triple constriction); (6) for learning systems, separate first-order action from second-order valuation fitting, and audit the valuations against what you actually want.

## Fallacy tripwires
- Laplace's demon (perfect knowledge → perfect prediction) — false in principle.
- Behavior without an inner loop: S→R chains that ignore the system's own outputs.
- "The market/self-correcting org is a thermostat" — demand the actual feedback loop.
- Bigger community = smarter community — the State is stupider than most of its components.
- "We can always turn it off" — stopping requires knowing when, at the machine's speed.
- Single-stage reliability thinking — multi-stage systems fail suddenly at the compounding cliff.
- Social science with tight observer-observed coupling — "never good to more than a very few decimal places."
