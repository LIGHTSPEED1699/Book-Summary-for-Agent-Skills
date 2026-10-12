# Chapter 9: Subspace Identification (1) - ORT Method

## Core Idea
The full identification problem: input-output data from a system with both a deterministic (exogenous input) and a stochastic (noise-driven) component. Split the output into its deterministic and stochastic parts by projecting data-matrix rows, realize each component with the Part II machinery (deterministic realization for the input part, stochastic realization for the residual), then stitch the joint ARX-type state-space model. ORT (Oblique/Orthogonal projection Realization Technique) does all of this with LQ decomposition + SVD + least squares — no optimization — and the chapter proves the statistical consistency of the estimators as the data length grows.

## Frameworks Introduced
- **Stochastic realization with exogenous inputs (9.2)**: joint model x⁺ = Ax + Bu + w, y = Cx + Du + v; the identification target is the whole (A,B,C,D,K) package, not just the noise model.
- **PE condition for inputs (9.4.2)**: input must be persistently exciting of order ≥ i + (state memory); Appendix B formalized and used here (Assumption 9.3: A1 state excitation, A2 PE of order i+1, A3 no feedback).
- **Splitting deterministic vs stochastic output (9.5, 9.7)**: LQ decomposition of stacked [U_p; Y_p] gives the orthogonal projection of Y_f rows onto the U_p row space → deterministic component; the residual is the stochastic component.
- **ORT for the deterministic subsystem (9.7.1)**: from the LQ blocks, SVD of the projected block L_qb·Y_eᵀ yields 𝒪̂_i (state order from the singular-value gap); then A, C by shift-invariance of 𝒪̂ (Step 2), then B, D by least squares on the linear Toeplitz relation (Step 3).
- **ORT for the stochastic subsystem (9.7.2, Algorithm A)**: whiten the sample covariances of the stochastic component, SVD of the normalized covariance Hankel → observability + reachability factors → A, C, K (Kalman gain) and noise covariances; Algorithm B uses the CCA route of ch8.7.
- **Joint model assembly (9.5.3)**: combine the two subsystem realizations into one state-space model with Kalman gain — the innovations-form model.
- **Consistency (9.6)**: sample covariance/data-matrix estimates converge to their ensemble values; the identified model converges as N → ∞.

## Key Concepts
- Shift invariance: deleting the first ℓ rows of 𝒪_i gives 𝒪_{i−ℓ}; hence A = 𝒪̂^† 𝒪̂_shifted — the standard trick for reading (A,C) off an observability estimate.
- The LQ decomposition simultaneously (a) projects the input effect out (deterministic part) and (b) exposes the state subspace (L_qb block) — one orthogonal transform, two jobs.
- ORT vs PO-MOESP: same data, different projection relations (Remark 9.3) — ORT uses the row-space projection identities (9.50)-(9.51) rather than PO-MOESP's; results coincide asymptotically.
- Order selection = singular-value gap in the projected/covariance Hankel SVD; the gap is the noise floor test.
- Whitening before SVD (Algorithm A Steps 1-2): covariance normalization makes the Hankel's singular values the canonical correlations of ch8.

## Mental Models
- "Split, realize, stitch": every with-input subspace algorithm is deterministic-part ID + stochastic-part ID + joint assembly.
- "One LQ, two paychecks": the triangular factors carry both the input projection and the state subspace.
- "Shift invariance reads the state matrix": once you have any basis of the state space, A is the least-squares map between shifted observability blocks.
- "Consistency is the warranty": the projections make noise vanish as N grows — that's why the assumptions (PE, open loop) are non-negotiable.

## Anti-patterns
- **Skipping the input projection with colored/feedback inputs** — the deterministic/stochastic split silently fails; closed-loop data needs ch11.
- **Reading order from unprojected SVD** — input-driven singular values masquerade as states; project first.
- **Estimating B,D before A,C** — the ORT order matters: B,D come from a linear LS once the state basis is fixed; reversing couples the problems.
- **Forgetting the Kalman gain in the joint model** — a realized (A,B,C,D) without K is not the innovations model the filter needs.

## Reference Tables
### ORT pipeline (deterministic subsystem)
| Step | Operation | Gets |
|---|---|---|
| 0 | LQ of [U_p U_f; Y_p Y_f] | L_qb, projection blocks |
| 1 | SVD of L_qb Y_eᵀ; gap → n | 𝒪̂_i |
| 2 | LS on shifted 𝒪̂ | Â, Ĉ |
| 3 | LS on Toeplitz relation | B̂, D̂ |

### ORT stochastic Algorithm A
| Step | Operation | Gets |
|---|---|---|
| 1 | square roots of sample covariances | whitening |
| 2 | SVD of normalized covariance Hankel; gap → n | state dim |
| 3 | factors | 𝒪̂, R̂ |
| 4 | shifted LS | Â, Ĉ, K̂ |
| 5 | covariance of residual | noise covariances |

## Key Takeaways
ORT = LQ projection + SVD + shift-invariant least squares: the complete optimization-free identification of (A,B,C,D,K) from open-loop PE data.
The deterministic/stochastic split is a projection, not an assumption — it's exact under the model class.
Shift invariance of the observability matrix converts "state subspace found" into "A, C found" in one LS.
Consistency theorems (9.6) certify the method as N → ∞; finite-sample behavior is the noise-gap story.

## Connects To
ch6's data-matrix lemmas and MOESP are the deterministic prototype; ch7-8's stochastic realization supplies Algorithm A/B; ch10 re-derives everything through CCA (the other route promised in ch1's outline); ch11 drops assumption A3 for closed-loop data; Doraiswami ch7 §7.8 gives the practitioner's version of the same pipeline.
