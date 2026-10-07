# Chapter 7: Stochastic Adaptive Control (Dual Control)

## Core Idea
The fully correct adaptive controller is a stochastic-control problem: parameters are states with a stochastic model, the optimal solution is the Bellman equation on the hyperstate (conditional distribution of everything), and it deliberately probes; certainty equivalence is the delta-function approximation of that solution — usually good, provably suboptimal when estimate uncertainty is large.

## Frameworks Introduced
- **Multistep decision structure (7.2, two-armed bandit)**: open-loop → open-loop optimal feedback (OLOF = receding horizon without learning value) → dynamic-programming optimal; Example 7.1: p = 0.6 known vs q ~ U[0,1] unknown — open-loop gain 0.6/play, full knowledge 0.68 (+13%), optimal strategy probes machine II early (N=6 state diagram: try, then switch after losses); many plays needed to approach optimum (N=1000 → 0.6773). **Value of knowledge is front-loaded: early probing pays over the horizon.**
- **Stochastic adaptive problem (7.3)**: ARX plant with parameters θ(t) following a Gauss-Markov process θ(t) = Θθ(t−1) + v(t) (Θ = I for constant parameters); Gaussian quadratic N-stage criterion E[Σ(y−u_c)²]; admissible strategies = functions of output history; the plant becomes a **nonlinear** system in (states, parameters) — y is not Gaussian even with Gaussian ingredients.
- **Bellman equation / hyperstate (7.4)**: value function I(Z(t)) on the sufficient statistic Z (conditional mean + covariance of state and parameters, or full conditional distribution = hyperstate); optimal u = argmin E[I(Z(t+1))]; existence unproven in general, closed-form only in toy cases; structure = nonlinear estimator + nonlinear feedback map.
- **Dual property**: optimal control balances direct action (drive y to reference) with **probing** (inject perturbations when parameter covariance is large to improve future control); myopic (N=1) controller ignores the probing term entirely.
- **Certainty equivalence as approximation (7.5)**: STR = replace the true conditional distribution by a point mass at its mean (delta approximation) — the probing term vanishes; other approximations: one-step lookahead with variance penalty, "variance control" adding a term ∝ parameter covariance × sensitivity, limited-memory hyperstates.
- **Known-parameter separation benchmark**: linear-quadratic-Gaussian with known parameters separates (Kalman filter + LQ gain); with unknown parameters separation fails — the estimator's covariance enters the optimal gain.
- **Examples (7.6)**: first-order system with one unknown parameter solved numerically by dynamic programming — dual effects matter at startup/large uncertainty, negligible in steady regulation; bandit-style experiments quantifying probing gains.

## Key Concepts
- **Hyperstate**: conditional probability distribution of states + parameters given data — the state of the optimal adaptive controller.
- **Probing / dual action**: deliberate excitation for information; automatic in the Bellman solution, engineered (or suppressed) elsewhere.
- **Myopic controller**: N = 1 criterion — no probing value assigned to information.
- **OLOF**: receding-horizon open-loop optimal feedback — uses feedback but undervalues information.
- **Value of information**: the gap between certainty-equivalent and dual-optimal performance; largest when uncertainty is large and horizon long.
- **Gauss-Markov parameter model**: θ(t) = Θθ(t−1) + v(t) — the stochastic description that makes parameters ordinary states.

## Mental Models
- "STR = dual control with amnesia about uncertainty"; when estimate covariance is small (steady regulation, constant parameters) the amnesia is harmless — at startup or fast drift it isn't.
- "Information is a control input": the Bellman solution prices it; if your algorithm doesn't, inject excitation explicitly (Ch 11 startup procedures).
- "Two-armed bandit intuition generalizes": always try the unknown option early when the horizon is long — probing is an option, and options decay with remaining horizon.
- "Θ = I is the generic hard case": constant unknown parameters still make the problem nonlinear — time-varying parameters only add tractability (forgetting) not difficulty.

## Anti-patterns
- **Expecting STR to self-excite**: certainty equivalence never probes; a quiet loop can freeze estimates (covariance wind-up follows — Ch 2/6).
- **Using myopic dual control as if dual**: N=1 "dual" controllers ignore the information term — the whole point is the lookahead.
- **Full dual control in practice**: hyperstate dimension explodes; no general solution exists — use STR + engineered excitation instead.
- **Assuming Gaussian priors stay Gaussian**: the product structure (parameters × states) breaks Gaussianity of y; approximations must be checked.

## Reference Tables

### Controller hierarchy
| Controller | Uses estimate covariance? | Probes? | Computable? |
|---|---|---|---|
| Open-loop | no | no | yes |
| OLOF / receding horizon | no | no | yes |
| Myopic (N=1) | partially | negligibly | simple cases |
| Certainty equivalence (STR) | no | no | yes — practice |
| Dual optimal (Bellman) | yes | yes | toy cases only |

## Key Takeaways
1. The exact adaptive problem is a nonlinear stochastic control problem on the hyperstate; the Bellman solution exists formally and probes optimally.
2. Certainty equivalence = delta-approximation of the hyperstate — the book's unifying explanation of every STR/MRAS in earlier chapters.
3. Probing value is largest at startup/fast drift/long horizon; negligible in steady regulation of constant-parameter plants.
4. Two-armed bandit numbers (+13% value of knowledge, slow convergence to it) set realistic expectations for dual gains.
5. Practice: STR + engineered excitation (startup sequences, periodic re-tuning) captures most dual benefit at STR cost.

## Connects To
- **Ch 1**: hyperstate/dual control preview.
- **Ch 2/6**: estimator covariance behavior (wind-up, PE) that dual control would manage.
- **Ch 11**: practical startup/excitation procedures.
- **Ch 13**: bandit/experiment design connections in adaptive signal processing.
