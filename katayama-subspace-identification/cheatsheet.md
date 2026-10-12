# Cheatsheet — Subspace Methods for System Identification (Katayama)

## The master equation
W_p = 𝒪_i X_p + 𝒯_{i,s} U_p  (past); W_f = 𝒪_i X_f + 𝒯 U_f (future)
- 𝒪_i = [C; CA; …; CA^{i−1}] extended observability
- X_p = [x(0) x(1) … x(i−1)] state sequence (the hidden factor)
- 𝒯 = block Toeplitz of Markov parameters

## Standing assumptions (check before any run)
| Code | Condition | Fails when |
|---|---|---|
| A1 | rank X_p = n (state excited) | poor initial conditions |
| A2 | input PE of order ≥ i+1 (rank of stacked U) | constant/short input |
| A3 | no feedback (U_p ⟂ X_p dependence) | closed-loop data |

## Order selection
- Noise-free: rank of projected data/covariance Hankel.
- Noisy: singular-value gap in SVD of projected block; n = #large σ.

## Algorithm pipelines
### MOESP (ch6.5)
1. LQ of [U_p; Y_p] → input projection
2. oblique projection of Y_f along U_p
3. SVD → 𝒪̂_i, n
4. LS: A,C (shift invariance), then B,D

### ORT deterministic (ch9.7.1)
1. LQ of data → L_qb, projection blocks
2. SVD of L_qb Y_eᵀ → 𝒪̂_i
3. LS shifted 𝒪̂ → Â, Ĉ
4. LS Toeplitz → B̂, D̂

### ORT stochastic Algorithm A (ch9.7.2)
1. whiten sample covariances
2. SVD of normalized covariance Hankel → n
3. factors → 𝒪̂, R̂
4. shifted LS → Â, Ĉ, K̂
5. residual covariance → noise covariances

### CCA (ch10.6)
1. project input out of past & future
2. whiten both blocks
3. SVD of whitened cross-covariance → ρᵢ, variates
4. Algorithm A: factor realization; Algorithm B: state X̂ then one joint LS for (A,B,C,D,K)

### Closed-loop (ch11)
1. treat (u,y) as joint process (needs external excitation)
2. CCA/ORT on the joint process → closed-loop model
3. algebraic plant recovery (Youla/joint approach)

## Key identities
- Projection ⟺ idempotent: Π² = Π; rank(Π) = trace(Π); orthogonal ⟺ Π = Πᵀ.
- Orthogonal projection: Π = A(AᵀA)⁻¹Aᵀ.
- Shift invariance: Â = 𝒪̂_{i−1}† · shift-down(𝒪̂_i).
- Kalman gain (stationary): K = AΣCᵀ(CΣCᵀ+R)⁻¹, Σ from DARE.
- CCA: Â = Σ_xx^{-1/2} Σ_xy Σ_yy^{-1/2}; ρᵢ = σ(Â).
- PR test: Φ(e^{jω}) + Φᵀ(e^{jω}) ≥ 0 ∀ω (scalar: Re Φ(e^{jω}) ≥ 0).
- Gaussian conditioning: E[x|y] = μ_x + P_xy P_yy⁻¹(y−μ_y).

## Deterministic ↔ stochastic dictionary
| Deterministic | Stochastic |
|---|---|
| impulse response / Markov params | covariance sequence |
| Hankel rank = order | covariance Hankel rank = order |
| minimal realization (up to similarity) | Markov model family (LMI on Σ) |
| balanced Gramians | CCA canonical correlations |
| solvability: finite rank | solvability: positive realness |

## Quick diagnostics
| Symptom | Likely violated |
|---|---|
| garbage order | A2 (PE) or noise gap absent |
| biased with feedback | A3 → use ch11 |
| no model exists | spectrum not PR |
| unstable realization | non-stabilizing ARE solution |
| rank collapse | A1 (state excitation) |
