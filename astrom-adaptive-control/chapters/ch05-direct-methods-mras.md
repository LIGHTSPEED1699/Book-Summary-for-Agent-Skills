# Chapter 5: Direct Methods of Adaptive Control (MRAS)

## Core Idea
MRAS adjusts controller parameters to null the error against a reference model; the MIT rule (gradient of squared model error) works but its gain bound is hidden and its naive use destabilizes — Lyapunov and passivity theory replace guesswork with adaptation laws that are stable by construction.

## Frameworks Introduced
- **MIT rule (5.2)**: minimize J = ½e²(t), e = y − y_m → dθ/dt = −γ e ∂e/∂θ (sensitivity derivative evaluated with θ frozen — slow-variation assumption). Variants: |e| law, **sign-sign algorithm** (dθ/dt = −γ sign(e)sign(∂e/∂θ), used in telecom). Feedforward gain example: θ̇ = −γ(θ − k_c k)k_c k y' — exponential convergence with rate ∝ γk².
- **Adaptation gain determination (5.3)**: average analysis of the linearized error dynamics — for the first-order MRAS the parameter error φ = θ − θ* obeys φ̇ = −γ k² φ (average), but the full system has fast loop dynamics; stability requires γ below a computable bound (e.g. γ < 2ω(1 + ω²T²)/k²-type limits for the first-order example); large γ → unpredictable/oscillatory behavior. Rule: derive the average equation, bound γ from the fast-loop interaction.
- **Lyapunov theory (5.4)**: direct method — V positive definite, V̇ ≤ 0 ⇒ stable; asymptotic via invariance. Used to *design* adaptation laws: pick V = e² + (1/γ)(θ − θ*)², choose θ̇ to make V̇ negative semidefinite.
- **MRAS design by Lyapunov (5.5)**: for first-order plants, error system e = (θ − θ*)G(p)u_c... choose θ̇ = −γ e ε (ε = filtered error/sensitivity signal) via Lyapunov; **Astrom-Wittenmark scheme** generalizes with filter Q(p): adaptation law stable when the transfer W(s) = Q(s)G_m(s) (or ΛG_m) is **positive real** — the design handle: choose Q to make W PR.
- **BIBO / input-output stability (5.6)**: monotone (passivity-type) operators, small-gain for operators; adaptation law as a nonlinear operator from error to parameter; **hyperstability approach**: error system = linear block + nonlinear time-varying block; PR linear block + Passivity Theorem ⇒ bounded signals, e → 0 under conditions.
- **Applications (5.7)**: MRAS for first-order/second-order plants with adjustable feedback/forward gains; the positive real condition W(s) = ρ₀ + ρ₁s + ... chosen via Q.
- **Output feedback MRAS (5.8)**: general scheme with adjustable u = θu_c − θy...; introduce filter Λ(p) = αp + 1 (or Q) so the effective W(s) = Λ⁻¹G_m is PR; guarantees bounded-input bounded-output stability and asymptotic model matching (e → 0) when the plant is minimum phase and relative degree ≤ 2 (with filter, higher).
- **MRAS vs STR (5.9)**: the reparameterization of Ch 3 shows indirect STR ≡ direct MRAS in different coordinates; Lyapunov-designed MRAS ≈ STR with fixed design; comparison table of assumptions.
- **Nonlinear systems (5.10)**: passivity/monotonicity framework covers certain nonlinear plants (the adaptation operator must be monotone); describing-function warnings.

## Key Concepts
- **Sensitivity derivative ∂e/∂θ**: the MIT rule's approximation source; exact only with frozen parameters.
- **Average equation**: fast dynamics averaged → parameter-error dynamics; the tool that bounds γ.
- **Positive real (PR) transfer function**: Re W(jω) ≥ 0 — the frequency-domain certificate that makes the adaptation loop passive.
- **Hyperstability / monotone operators**: Popov-type integral inequality for the adaptation nonlinearity.
- **Model matching**: e → 0 means closed loop behaves like the reference model — the MRAS spec.
- **e-modification / σ-modification**: add −σθ terms for robustness to disturbances (preview Ch 10).

## Mental Models
- "MIT rule = gradient descent on a nonconvex, time-varying landscape" — works for small γ, fails unpredictably past a bound you must derive, not guess.
- "Lyapunov designs adaptation, MIT approximates it": pick V first, read off θ̇; the PR condition is the same fact in frequency-domain clothes.
- "The reference model must be achievable": MRAS can only match models whose relative degree/zeros the plant structure permits.
- "Sign of the high-frequency gain matters": adaptation law sign must match the sign of the unknown gain k (Example 5.1 needs sign k known) — wrong sign = anti-damping (Nussbaum-type tricks come later).

## Anti-patterns
- **Large adaptation gain without average analysis** — the classic MRAS instability; γ beyond the PR-derived bound excites the fast loop.
- **Freezing parameters when deriving ∂e/∂θ and then acting fast** — the approximation's validity condition is violated by your own γ.
- **Nonminimum-phase plant with aggressive model matching** — no filter Q makes an unstable zero-canceling W PR.
- **Believing e → 0 implies θ → θ*** — only with persistent excitation; otherwise parameter error drifts in the null space (Ch 6).

## Reference Tables

### MRAS stability routes
| Method | Certificate | Gives |
|---|---|---|
| Average analysis | φ̇ = −γk²φ + fast terms | γ bound |
| Lyapunov | V̇ ≤ 0 | stable law by construction |
| PR/passivity | Re W(jω) ≥ 0 | BIBO + e→0, filter design |

### Scheme comparison (with Ch 3-4)
| | STR indirect | STR direct | MRAS Lyapunov |
|---|---|---|---|
| Estimates | process params | controller params | controller params |
| Design solve | yes | no | none (law is design) |
| Stability theory | Ch 6 averaging | Ch 6 | Lyapunov/PR built in |
| Needs | excitation | min phase, d₀ | min phase, sign k, PR filter |

## Key Takeaways
1. The MIT rule is a gradient heuristic with a hidden stability bound; average analysis makes the bound explicit.
2. Lyapunov synthesis designs adaptation laws that are stable by construction; the PR condition (choose Q/Λ) is the practical design handle.
3. Passivity/hyperstability gives the operator-level view: a PR linear block + monotone adaptation block = bounded error, asymptotic matching.
4. MRAS and direct STR are the same scheme in different parameterizations — Ch 3's reparameterization is the bridge.
5. Known sign of the high-frequency gain and minimum phase are structural prerequisites, not tuning issues.

## Connects To
- **Ch 3/4**: reparameterization linking MRAS and STR (5.9).
- **Ch 6**: nonlinear dynamics/averaging analysis of these same loops.
- **Ch 9**: robustness modifications (σ-modification, dead zones).
- **Ch 13**: sign-sign algorithms in adaptive signal processing.
