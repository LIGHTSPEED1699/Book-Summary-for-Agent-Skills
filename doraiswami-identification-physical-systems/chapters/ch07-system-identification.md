# Chapter 7: System Identification

## Core Idea
The practitioner's identification chapter: estimate the integrated ARX/ARMAX model of ch1 from input-output data. Plain least squares on the ARX regressor is simple and unbiased only when the noise is white and uncorrelated with the regressors; with output-error noise it is biased — hence the ladder: recursive LS for online, high-order LS followed by principled order reduction, and the prediction error method (PEM) as the general (iterative, ML-flavored) answer. The chapter closes by presenting the subspace method (Katayama's world) as the optimization-free alternative for state-space models, and arms the reader with residual analysis and frequency-weighted reduction as the quality controls.

## Frameworks Introduced
- **System model (7.2)**: state-space and frequency-domain models with explicit assumptions; the integrated ARX/ARMAX difference-equation model as the identification target.
- **LS identification (7.4)**: regressor data matrix H(k) of past inputs/outputs; θ̂ = (HᵀH)⁻¹Hᵀz; unbiasedness and covariance formulas; variance of the LS residual = (1 − M/N)σ²; SVD computation and the condition number of HᵀH.
- **RLS identification (7.4.6)**: recursive estimator with Kalman-gain/Riccati recursion — streaming LS.
- **High-order LS method (7.5)**: deliberately over-model (n_h ≫ n), justify via projection error decay, then derive a reduced-order model; model order selection criteria (7.5.4).
- **Prediction error method (7.6)**: residual model ε = (1 − C(q)⁻¹...) structure; objective = mean squared prediction error; iterative prediction algorithm; the family of PEM algorithms (ARX/ARMAX/OE/Box-Jenkins variants).
- **High-order LS vs PEM (7.7)**: when they agree (whitened noise) and where PEM wins (general noise models, bias removal).
- **Subspace identification method (7.8)**: the Hankel/LQ/SVD pipeline in practitioner dress — no parametrization, no iteration; the bridge to Katayama.
- **LS performance appendix (7.10)**: correlated vs uncorrelated error analysis; correlation of error with the data matrix — the exact bias mechanism; residual analysis as model validation.
- **Frequency-weighted model order reduction (7.11)**: reduce where it matters spectrally; choice of weighting frequencies.

## Key Concepts
- LS bias mechanism: regressors correlated with noise (output-error models) ⇒ E[Hᵀe] ≠ 0; the appendix computes the bias exactly.
- Consistency conditions: θ̂ → θ as N → ∞ with cov(θ̂) = σ²(HᵀH)⁻¹ — information again (ch3).
- High-order-then-reduce trades parametrization worry for a reduction step with its own criteria (Hankel singular values / frequency weighting).
- PEM = minimize prediction error over a parametrized model class — ML in disguise (ch3), iterative because the residual depends on θ.
- Subspace methods dodge both problems: no θ parametrization, no iteration — at the cost of the open-loop/PE assumptions.
- Residual whiteness + residual-spectrum flatness = the validation certificate.

## Mental Models
- "Know your noise, pick your method": white noise → LS fine; colored/output-error → PEM or subspace.
- "Over-model then cut": if order is unknown, go high and reduce with a criterion rather than search orders blindly.
- "Bias is a correlation story": check E[Hᵀe]; if nonzero, the estimator lies.
- "Residuals are the jury": every method's output must survive residual analysis before use.

## Anti-patterns
- **ARX-LS on output-error data** — biased; the chapter's 7.10 appendix quantifies exactly how bad.
- **Order selection by fit score alone** — overfitting; use the reduction criteria/weighting (7.5.4, 7.11).
- **PEM without initialization/iteration care** — nonlinear objective, local minima; start from LS or subspace.
- **Skipping residual analysis** — colored residuals mean unmodeled dynamics or noise misfit.
- **Condition-number blindness** — ill-conditioned H (poor excitation) makes θ̂ variance explode; excite properly (PE again).

## Reference Tables
### Method ladder
| Method | Noise class | Iterative? | Output |
|---|---|---|---|
| ARX LS | white, uncorrelated | no | biased for OE noise |
| RLS | same, online | recursive | streaming θ̂ |
| High-order LS + reduce | white | no | reduced ARMAX |
| PEM (ARMAX/OE/Bj) | general | yes | consistent ML-type |
| Subspace | general, open-loop PE | no | state-space (A,B,C,D,K) |

### Validation checks
| Check | Pass when |
|---|---|
| Residual whiteness | autocorrelation ≈ δ |
| Residual spectrum | flat in band of interest |
| Parameter covariance | small (well-excited data) |
| Condition number of H | moderate |

## Key Takeaways
LS is exact only under uncorrelated noise; the bias mechanism is regressor-noise correlation, computable and often material.
The method ladder (LS → RLS → high-order+reduction → PEM → subspace) trades simplicity for generality; subspace methods skip parametrization entirely.
Residual analysis is the universal validation gate.
Frequency-weighted reduction keeps the model right where it will be used.

## Connects To
ch1's integrated model is the target; ch3's ML theory underwrites PEM; ch5's LS/SVD is the engine; ch6's Kalman filter consumes the identified model; ch8 extends to closed-loop data; ch9-13 use the identified models for diagnosis and soft sensing. Katayama ch6/9/10 is the full treatment of §7.8.
