# Patterns — Subspace Methods for System Identification (Katayama)

Recurring reasoning moves across the book.

## 1. Rank is order
The system's McMillan degree is a matrix rank: Hankel rank (ch2-3), data-matrix rank after projection (Lemma 6.3, ch6), singular-value gap under noise (ch9-10). **Use when:** choosing model order — count, don't search.

## 2. Project, then realize
Annihilate the known/nuisance term with a projection (orthogonal or oblique), leaving a matrix whose column space is the state/observability space; then realize by least squares. **Use when:** any identification step — MOESP, ORT, CCA are all this.

## 3. The state lives in the data
W_p = 𝒪X_p + 𝒯U_p: the state sequence is a factor of the data matrix. Estimate the state subspace directly instead of parametrizing it. **Use when:** tempted to write down a parameter vector and optimize — don't.

## 4. Shift invariance reads the model
Any basis of the state space gives A via the least-squares map between shifted observability blocks. **Use when:** you have 𝒪̂ or X̂ and need (A,B,C,D,K).

## 5. Split deterministic / stochastic, realize each, stitch
Project the input effect out (deterministic part), take the residual (stochastic part), realize each with the right theory, assemble the joint innovations model. **Use when:** identification with exogenous inputs (ch9-11).

## 6. Covariances are impulse responses
Stochastic realization runs the deterministic Hankel machinery on covariance data; positive realness is the existence certificate; the LMI/Riccati family replaces the unique minimal realization. **Use when:** modeling a stationary process or auditing whether a spectrum admits a Markov model.

## 7. CCA is the state
Canonical variates between (input-projected) past and future are balanced states; canonical correlations are Hankel singular values. **Use when:** balancing, reducing, or extracting the state from stochastic data (ch8, ch10).

## 8. Orthogonal transforms over normal equations
QR/LQ/SVD everywhere; never square the condition number. **Use when:** implementing — the book's algorithms are numerically serious by construction.

## 9. Assumptions are rank tests
A1 state excitation, A2 PE input, A3 no feedback — each is a rank/dependence condition checkable from data. **Use when:** diagnosing a failed identification — find the violated assumption.

## 10. Identify what the data generate
Closed-loop data generate the closed-loop process; identify the joint (u,y) model, then algebra out the plant. **Use when:** feedback is present — never run open-loop methods on closed-loop data.

## 11. Consistency is the warranty
Projections make noise vanish as N → ∞; sample covariances → ensemble covariances by ergodicity. **Use when:** trusting a finite-data result — know the asymptotic claim you're leaning on.

## 12. Run the tape backwards
Forward and backward Markov models / Kalman filters bracket the state from both time directions; subspace methods exploit the symmetry. **Use when:** past/future Hankel geometry appears.

## Anti-patterns (cross-chapter)
- Normal equations in production code (ch2).
- Order from unprojected SVD (ch9-10).
- Open-loop ID on closed-loop data (ch11).
- Non-PR spectrum realization (ch7).
- Skipping the PE check (Appendix B).
- Truncating in unbalanced coordinates (ch3, ch8).
