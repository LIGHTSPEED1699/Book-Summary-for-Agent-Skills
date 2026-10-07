# Chapter 5: Stochastic Optimal Control

## Core Idea
Optimize the *expected* cost: with perfect measurements the disturbance simply inflates the cost (same Riccati, extra trace term); with imperfect measurements the general problem is intractably coupled (dual control), but for the linear-quadratic-Gaussian case estimation and control **separate exactly** — certainty equivalence — and the cost decomposes additively into a control part and an estimation part.

## Frameworks Introduced
- **5.1 Perfect measurements**: stochastic principle of optimality — minimize E[J] with the information set = current state; for LQ problems with random w: the optimal control law is the *same* deterministic Riccati law; randomness adds a fixed expected-cost increment ∝ trace(Q_c·P) (disturbance cost) — control design and disturbance statistics decouple.
- **5.2 Imperfect measurements**: information set I = measurement + control history; **derived information set** = conditional mean X̂ and covariance P (Markov + white measurement error ⇒ present estimates summarize the past); stochastic HJB conditioned on the information set is generally unsolvable because the value function depends on the *entire* conditional density — the hyperstate problem.
  - **Dual control**: control actions affect future information (probing); **probing has value only when the system is nonlinear or parameters unknown** — "neutral" systems (known linear plant + linear feedback) gain nothing from probing; this bounds the practical relevance of dual control.
  - **Neighboring-optimal stochastic control**: linearize around the nominal trajectory → filter + Riccati feedback + feedforward terms; the estimator "hedges" the control by not responding to deviations likely due to measurement error.
- **5.3 Certainty equivalence (LQG)**: for linear dynamics, Gaussian noise, quadratic cost: u°(t) = −C(t)x̂(t) where x̂ is the Kalman-Bucy estimate and C the deterministic LQ gain — **separation principle**; expected cost = deterministic-optimal cost + estimation-error penalty (trace terms), each computable independently; discrete-time version identical; additional CE cases enumerated (e.g., certain observation structures).
- **5.4 LTI steady-state machinery**: asymptotic stability of the LQR (Riccati solution gives A(s) = det(sI − F + GC) robustness — developed fully in Ch 6.5); asymptotic stability of the Kalman-Bucy filter (detectability ⇒ convergence of P); the **stochastic regulator** = filter + gain: closed-loop eigenvalues = {regulator modes} ∪ {estimator modes}; steady-state performance decomposition: E[xᵀQx] = (control-design term) + (estimation-design term) — trade disturbance rejection vs sensor noise via Q_c, R separately.

## Key Concepts
- **Information set / derived information set**: what the controller knows vs the sufficient statistics (x̂, P) it should use.
- **Hedging**: the estimator's smoothing prevents the controller from chasing measurement noise.
- **Dual effect / probing**: control that buys information; valuable only under nonlinearity/parameter uncertainty.
- **Separation (certainty equivalence)**: LQG optimum = LQ gain × Kalman estimate; design the two halves independently.
- **Cost decomposition**: E[J] = J_control + J_estimation — the design budget split.
- **Eigenvalue union**: stochastic regulator modes = regulator modes + estimator modes (no interaction in the LTI perfect-model case).

## Mental Models
- "Noise costs, but doesn't redesign": for LQ with perfect state info, randomness only adds a trace-term bill — the law is unchanged.
- "The estimator is a hedge, not a lag": it deliberately ignores the part of the signal likely to be noise — that's why CE control doesn't thrash.
- "Probing pays only where the map is wrong": known-linear = neutral = no dual value; unknown parameters or strong nonlinearity = probing earns.
- "Two design budgets, one bill": tune Q/R for the estimator and Q/R for the regulator separately; the expected cost adds their prices.

## Anti-patterns
- **Assuming separation holds generally**: with unknown parameters or nonlinear dynamics, estimation and control couple (hyperstate); CE is an LQG privilege.
- **Probing in neutral systems**: dither that can't change knowledge is pure cost.
- **Feeding raw measurements to the LQ gain**: without the estimator's hedge, measurement noise propagates into control energy (the CE architecture exists to prevent exactly this).
- **Forgetting the estimator's own dynamics when assessing robustness**: the union of modes includes the filter's — Ch 6.6 shows the compensator's margins can be worse than either half alone.

## Reference Tables

### Stochastic problem hierarchy
| Setting | Solution | Coupling |
|---|---|---|
| LQ, perfect measurements | deterministic Riccati law + trace cost | none |
| General nonlinear, imperfect | hyperstate HJB (intractable) | full dual coupling |
| LQ, Gaussian, imperfect | CE: −Cx̂ (separation) | none (cost adds) |
| Nonlinear/unknown params, imperfect | approximate: EKF + Riccati + (rarely) probing | partial |

## Key Takeaways
1. Stochastic LQ with perfect state info changes only the cost, not the control law.
2. With imperfect info the general problem is the hyperstate; probing/dual control matters only for nonlinear or parameter-uncertain systems.
3. LQG's certainty equivalence is the load-bearing theorem of this book: Kalman estimate + LQ gain, designed separately, cost added.
4. The stochastic regulator's dynamics are the union of regulator and estimator modes — and its robustness must be checked on the combined loop (Ch 6.6).
5. Estimation quality is a priced design variable: tighten sensor/model statistics and the control-side bill drops.

## Connects To
- **Ch 3**: deterministic extremals and neighboring-optimal gains.
- **Ch 4**: the filters supplying x̂ and P.
- **Ch 6**: LTI specialization — Riccati equations algebraic, margins, multivariable robustness.
- **Ch 6.7**: the adaptive-control footnote where probing returns.
