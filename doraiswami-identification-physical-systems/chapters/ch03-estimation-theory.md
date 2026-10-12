# Chapter 3: Estimation Theory

## Core Idea
Parameter estimation from noisy data is a statistical problem with a standard toolkit: model the measurement as a map from unknown parameters plus a probabilistic error model, form the likelihood, and choose an estimator. The quality yardsticks — bias, variance, MSE, consistency — trade off against a hard floor: the Cramér-Rao lower bound set by Fisher information. Maximum likelihood is the workhorse: maximize the likelihood (equivalently minimize negative log-likelihood), and for Gaussian errors ML *is* least squares. ML is asymptotically efficient — it hits the Cramér-Rao bound — which is why the identification chapters lean on it.

## Frameworks Introduced
- **Estimation setup (3.2)**: mathematical model (map from parameter θ to measurement), probabilistic model (error density), likelihood function p(data; θ) viewed as a function of θ.
- **Estimator properties (3.3)**: estimator = random variable; bias, variance, MSE decomposition; unbiasedness; median vs mean estimators; small-sample vs large-sample (consistency) properties.
- **Fisher information & Cramér-Rao (3.4)**: I(θ) = E[(∂ log p/∂θ)²); any unbiased estimator satisfies var(θ̂) ≥ 1/I(θ) — the information budget of the problem.
- **Maximum likelihood estimation (3.5)**: θ̂_ML = argmax p(data;θ); log-likelihood form; Gaussian errors ⇒ least-squares criterion; ML invariance under reparametrization.
- **ML properties (3.6)**: consistency, asymptotic normality, asymptotic efficiency (attains Cramér-Rao); conditions (regularity, identifiable model).
- **Scalar and vector cases (3.7)**: explicit scalar formulas; vector θ with Fisher information matrix and covariance bound I⁻¹.

## Key Concepts
- The likelihood is the data's opinion about θ; estimators are functions of data, so they have their own distribution (hence bias/variance).
- MSE = variance + bias² — the bias-variance tradeoff is the first design decision.
- Consistency ≠ unbiasedness: an estimator can be biased at finite N yet converge (ML often is).
- Fisher information is what the experiment is worth: more informative inputs/data ⇒ lower achievable variance (ties to persistent excitation).
- Gaussian ⇒ LS: the ubiquitous least-squares methods are ML under a Gaussian assumption, not free-standing magic.
- Efficiency: ML reaches the Cramér-Rao bound asymptotically — the justification for PEM/ML identification in ch7.

## Mental Models
- "Estimators have distributions": never report θ̂ without its variance story.
- "Bound first, then build": compute (or estimate) the Cramér-Rao floor before judging an estimator — the gap tells you if there's anything left to gain.
- "Likelihood is the objective, criterion is its alias": every loss function in the book is a negative log-likelihood of some noise model.
- "Information is experimental design": Fisher information quantifies how much the chosen input/record buys — design for information.

## Anti-patterns
- **Unbiasedness fetish** — a slightly biased, much lower-variance estimator often wins on MSE.
- **ML without identifiability** — flat likelihood directions mean no estimator can succeed (connects to Katayama's identifiability warnings).
- **Ignoring the noise model when choosing the criterion** — LS is only ML for Gaussian; heavy-tailed noise wants a different likelihood.
- **Reading finite-N variance from asymptotic formulas** — ML efficiency is an N → ∞ statement.

## Reference Tables
### Estimator quality
| Property | Definition | Regime |
|---|---|---|
| Bias | E[θ̂] − θ | finite N |
| Variance | E[(θ̂−E[θ̂])²] | finite N |
| MSE | var + bias² | finite N |
| Consistency | θ̂ → θ in prob | N → ∞ |
| Efficiency | var → CRLB | N → ∞ |

### Cramér-Rao
| Object | Formula |
|---|---|
| Score | ∂ log p / ∂θ |
| Fisher info | I(θ) = E[score²] = −E[∂² log p/∂θ²] |
| Bound (scalar) | var(θ̂) ≥ 1/I(θ) |
| Bound (vector) | Cov(θ̂) ⪰ I(θ)⁻¹ |

## Key Takeaways
Estimation quality is bounded by Fisher information; good estimators approach the bound, and ML does so asymptotically.
Least squares = ML under Gaussian errors — know the noise model behind every criterion.
Bias/variance/MSE and consistency are separate claims; check each explicitly.
Identifiability and information come before algorithms: no method beats the bound or rescues a flat likelihood.

## Connects To
ch4 extends to random parameters (Bayesian/MMSE vs this chapter's frequentist/ML); ch5's LS is the Gaussian-ML special case used for identification; ch7's PEM is ML identification; ch9's GLT fault tests are likelihood-ratio machinery. Katayama ch1's PEM discussion is the same story from the control side.
