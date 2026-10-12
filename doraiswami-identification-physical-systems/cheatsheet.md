# Cheatsheet — Identification of Physical Systems (Doraiswami et al.)

## Signal characterization
| Tool | Formula | Use |
|---|---|---|
| Autocorrelation | r_xx(m) = Σ x(k)x(k−m) | periodicity, model order |
| Cross-correlation | r_xy(m) = Σ x(k)y(k−m) | delay (peak), detection |
| PSD | S_xx = FFT{r_xx} | signature |
| Coherence | γ² = \|S_xy\|²/(S_xxS_yy) | estimate trust |
| Non-parametric H | Ĥ = S_yx/S_xx | quick plant estimate |

## Estimation
| Method | Estimator | When |
|---|---|---|
| ML | argmax p(data;θ) | known noise model |
| MMSE | E[θ\|data] | prior on θ |
| LS | (HᵀH)⁻¹Hᵀz | Gaussian, uncorrelated noise |
| RLS | K-gain recursion | online |
| PEM | min Σ ε²(θ), iterative | general noise |
| Subspace | LQ+SVD+LS | state-space, open-loop PE |

## Kalman filter
| Step | Equation |
|---|---|
| Predict | x̂⁻ = Ax̂ + Bu |
| Residual | e = y − Cx̂ − Du |
| Correct | x̂⁺ = x̂⁻ + Ke |
| Gain | K = P̄Cᵀ(CP̄Cᵀ+R)⁻¹ |
| Covariance | P⁺ = P̄ − K(CP̄Cᵀ+R)Kᵀ |

## Closed-loop identification
| Route | Handle | Needs |
|---|---|---|
| Two-stage | reference-driven prediction | external reference |
| Direct (KF) | innovations | noise+loop model |
| Joint (Katayama) | joint (u,y) process | external excitation |

## Fault diagnosis pipeline
| Stage | Object | Tool |
|---|---|---|
| Residual | e(k) | Kalman filter |
| Detection | GLT / Bayes test | residual whiteness |
| Isolation | influence vectors | max-correlation classification |
| Magnitude | f̂ | ML estimation |
| Network | KF bank + topology | path intersection |

## Five-step scheme (ch11)
1. Select diagnostic parameters (sensitive to fault classes)
2. Identify fault-free nominal model (high-order LS + reduce)
3. Design Kalman filter (tune K to white, minimal-variance residual)
4. Estimate influence vectors offline (perturb emulators γ one at a time, LS fit)
5. Diagnose by Bayes multiple-hypothesis test (max residual correlation)

## Soft sensor stack (ch13)
| Layer | Object |
|---|---|
| Virtual sensor | identified model |
| Real-time estimate | Kalman filter |
| Robust controller | mixed-sensitivity H∞ on augmented model |
| Status monitor | residual + Bayes test |

## Quick diagnostics
| Symptom | Likely cause |
|---|---|
| Biased ARX fit | regressor-noise correlation (output-error/closed-loop) |
| Residual colored | unmodeled dynamics or fault |
| Poor coherence | noise/artifact in band |
| Identified order < physical | low SNR / weak excitation |
| Fault hidden under control | feedback masks residual signature |
| Soft-sensor drift | model mismatch (check residual) |

## Model-order & validation
- Order: high-order LS then reduce (Hankel/frequency-weighted); or subspace singular-value gap.
- Validate: residual whiteness, flat residual spectrum, small parameter covariance, moderate cond(H).
- Always: coherence with spectra; residual analysis with every fit.
