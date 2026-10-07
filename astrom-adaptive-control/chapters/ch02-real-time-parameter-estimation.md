# Chapter 2: Real-Time Parameter Estimation

## Core Idea
Least squares is the engine of adaptive control's estimation loop: write any model *linear in the parameters* as a regression y = φᵀθ, then run the recursive version (covariance form, projection form, stochastic-approximation form) — but the experimental conditions and noise structure decide whether the estimates are unbiased, and no algorithm fixes a badly chosen model set.

## Frameworks Introduced
- **Regression model form**: y(i) + a₁y(i−1) + ... = b₁u(i−1) + ... → y(t) = φᵀ(t)θ + e(t) with parameter vector θ and regression vector φ (delayed outputs + inputs = autoregressive/ARX form). Batch least squares θ̂ = (ΦᵀΦ)⁻¹ΦᵀY (Theorem 2.1); statistical view: θ̂ ~ N(θ, σ²(ΦᵀΦ)⁻¹) (Theorem 2.2).
- **Model-set hierarchy**: FIR (transversal filter; many params if h short vs slowest time constant) → ARX/transfer-function A(q), B(q) → output-error (OE) and Box-Jenkins structures → continuous-time via **filtering instead of differentiation**: rewrite A(p)y = B(p)u as y = filtered signals φᵀθ with stable filters Hᵢ(p) of pole excess ≥ n — never differentiate measured data.
- **Equation error vs output error methods**: LS on A(q)y = B(q)u + e (equation error) is unbiased only if noise enters the equation's right side as white e; for output white noise the equation-error estimate is **biased** (regressor contains noise) — use output-error/prediction-error criterion V = Σ(y − ŷ)² instead (nonlinear in θ; iterative or recursive gradient methods).
- **Recursive algorithms** (Theorem 2.5 family, all one-step-ahead prediction ε(t) = y(t) − φᵀ(t)θ̂(t−1)):
  - **Recursive least squares (RLS, covariance form)**: θ̂(t) = θ̂(t−1) + R(t)φ(t)ε(t); R update with forgetting factor λ ∈ (0,1] (P(t) = (1/λ)[P(t−1) − PφφᵀP/(λ + φᵀPφ)]); λ trades memory vs tracking; covariance trace bounded ⇒ finite "effective memory".
  - **Projection algorithm**: gradient-type with normalization; R fixed or gain-scheduled.
  - **Stochastic approximation (LMS-like)**: θ̂(t) = θ̂(t−1) + γ(t)φ(t)ε(t) with γ(t) ↓ 0 (e.g. 1/t) — converges under conditions, cheap, slow.
- **Persistent excitation**: ΦᵀΦ nonsingular / average of φφᵀ positive definite — without it parameters are not identifiable and covariance winds up or freezes; excitation must come from reference steps or deliberate probing (Ch 11).
- **Prior information handling**: parameter constraints, initial covariance as prior, freezing converged parameters (dead zones, conditional updating — preview Ch 11).
- **Model quality assessment**: residual analysis (whiteness tests), prediction correlation, model validation on held-out data; complexity choice via trade-off (2.3 model set section: smallest set capturing the control-relevant dynamics).

## Key Concepts
- **Regression vector φ(t)**: delayed inputs/outputs assembling the linear-in-parameters form.
- **Forgetting factor λ**: exponential weighting; λ = 1 covariance saturates (bounded memory), λ < 1 tracks drift but adds noise sensitivity.
- **Covariance wind-up**: with no excitation, P grows (λ < 1) then a sudden spike of φ causes parameter jumps — the classic STR failure mode.
- **Bias due to noise-regressor correlation**: equation-error LS biased under output noise; remedies: whitening (estimate noise model C(q) and prefilter), instrumental variables, output-error methods.
- **Prediction error method (PEM)**: minimize filtered output prediction error — the general unbiased route.
- **Identifiability**: unique θ for given excitation; ties to model set order selection.

## Mental Models
- "Linear in the parameters is the magic property" — nonlinear-in-inputs is fine (Example: y with u², u·y regressors); nonlinear-in-θ forces gradient/iterative methods.
- "Filter, never differentiate" for continuous-time identification.
- "The algorithm is a detail; the noise model decides bias" — pick equation-error vs output-error from where the noise enters, not convenience.
- "Excitation is a design input": no persistent excitation ⇒ no convergence, regardless of algorithm elegance.
- "λ is a low-pass on belief": smaller λ = faster forgetting, noisier estimates.

## Anti-patterns
- **Equation-error LS under output noise** → biased parameters → wrong controller (STR bias; Ch 9 robustness).
- **Adapting with a frozen regression** (constant closed-loop signal): covariance wind-up then parameter explosion on the next transient.
- **Over-parameterizing**: FIR with h ≪ slowest time constant; more parameters ≠ better control — the underlying design problem only needs the control-relevant dynamics.
- **Differentiating measurements** for continuous-time estimation — use state-variable filters Hᵢ(p).

## Reference Tables

### Estimator comparison
| Algorithm | Update | Gain | Pros/Cons |
|---|---|---|---|
| Batch LS | (ΦᵀΦ)⁻¹ΦᵀY | — | exact, O(t) storage |
| RLS covariance | +Rφε | R = P (λ-faded) | fast convergence; O(n²); wind-up risk |
| Projection | +Rφε | R fixed/scheduled | stable, slower |
| Stochastic approx | +γ(t)φε | γ(t)→0 | cheapest; slow, tuning-sensitive |

### Noise structure → correct method
| Noise model | Unbiased method |
|---|---|
| A(q)y = B(q)u + e (e white) | equation-error LS (ARX) |
| y = G(q)u + v (v white) | output-error / PEM |
| colored noise | ARMAX / BJ + whitening filter |

## Key Takeaways
1. Everything adaptive estimates is a regression y = φᵀθ; least squares + matrix inversion lemma gives the recursive workhorse.
2. Bias comes from noise-regressor correlation, not from the recursion — match the method to the noise entry point.
3. Persistent excitation is a property of the experiment (or the reference), and it is necessary; design for it.
4. Forgetting factor λ sets the memory/time-variance trade-off; covariance wind-up without excitation is the #1 practical estimator failure.
5. Continuous-time identification = filtered-signal regression; never differentiate data.

## Connects To
- **Ch 3-4**: RLS is the estimator half of STR.
- **Ch 6**: convergence of these algorithms analyzed via averaging.
- **Ch 7**: stochastic convergence, martingale tools.
- **Ch 11**: implementation — square-root algorithms, dead zones, conditional updating.
