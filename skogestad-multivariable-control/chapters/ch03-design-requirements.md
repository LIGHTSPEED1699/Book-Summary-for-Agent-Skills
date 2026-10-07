# Chapter 3: Control System Design Requirements (MIMO foundations)

## Core Idea
MIMO systems add *directions* to gains: at each frequency a plant amplifies different input directions differently (SVD), and this directionality — not poles/zeros alone — is what makes multivariable control hard; every SISO magnitude rule generalizes via maximum singular value σ̄, but SISO margins do NOT generalize, and NP + RS does not imply RP.

## Frameworks Introduced
- **MIMO block diagram rules**: cascade (order reverses: G = G₂G₁), feedback ((I∓L)⁻¹), push-through (G(I+KG)⁻¹ = (I+GK)⁻¹G), and the MIMO rule: walk backwards from output against signal flow, most direct path, insert (I−L)⁻¹ when exiting a loop. Non-commutativity matters: GK ≠ KG.
- **S/T at both loop breaks**: output side L = GK, S = (I+L)⁻¹, T = L(I+L)⁻¹; input side L_I = KG, S_I, T_I. Identities: S + T = I, GS = SG, KS = S_I K, T = I − S (use it to avoid state explosion in numerics).
- **SVD as the directionality tool**: G(jω) = U Σ Vᴴ; input direction v_i → output direction u_i with gain σ_i. σ̄ = max gain (strongest direction v̄,ū), σ̲ = min gain (weakest v_,u). For l×m with l > m, u_{m+1} is the uncontrollable output direction.
- **Condition number**: γ(G) = σ̄(G)/σ̲(G) — measures ill-conditioning (gain spread across directions). Large γ ⇒ control hard *when input uncertainty lets signals leak between directions* (shopping cart: push sideways, uncertainty leaks force into the strong forward direction).
- **σ̲(G) as controllability/resiliency measure**: with scaled variables, an input of norm ≤ 1 can produce output ≥ σ̲(G) in ANY direction; need σ̲(G) ≳ 1 at frequencies where control is required (Morari resiliency index).
- **MIMO performance spec**: σ̄(S) ≤ 1/|w_P| ⇔ ‖w_P S‖∞ < 1 (worst-case error ratio over all reference directions); MIMO bandwidth ω_B = where σ̄(S) crosses 0.707 from below (worst direction); bandwidth *region* between σ̄(S) and σ̲(S) crossings.
- **Generalized plant P / N-Δ framework (Doyle)**: w = exogenous (r, d, n), z = weighted errors to minimize, v = controller measurements, u = manipulated; P contains plant + weights, not K; almost any linear control problem (feedback, feedforward, estimation) fits z = N(K)w, minimize ‖N‖∞; weights normalize signals to magnitude ~1 so ‖N‖ < 1 = specs met.
- **Two robustness warnings that motivate μ**:
  - *Spinning satellite*: infinite GM and 90° PM in each loop checked one-at-a-time, yet simultaneous 1/(1+a)-level input gain errors destabilize. Large σ̄(S), σ̄(T) (≈10) flagged it.
  - *Distillation column*: inverse-based decoupler gives perfect NP, σ̄(S) = σ̄(T) < 1 everywhere (no peaks!), infinite GM / 90° PM per channel, RS to 100% input gain errors — yet 20% simultaneous input gain error (ε₁ = −ε₂) wrecks performance (RP fails), and adding output gain uncertainty destabilizes at ε > 1/λ₁₁ ≈ 12% (λ₁₁ = 35.1 from the RGA).

## Key Concepts
- **Interaction vs ill-conditioning**: interaction = every input affects every output; ill-conditioning = gain spread across directions (γ ≫ 1). A plant can be interactive but well-conditioned, or triangular (non-interactive) yet ill-conditioned.
- **Diagonal input uncertainty**: u' = (I + ε)u, ε = diag(ε_i) — always present (actuator gain errors, ~20% typical in process control); sits between controller and plant; the classic MIMO killer.
- **RS condition preview (Ch 8)**: diagonal input uncertainty |ε_i| < 1/σ̄(T) guarantees robust stability.
- **RGA preview**: large RGA elements (|λ| ≫ 1) predict inverse-based controller fragility; instability bound with simultaneous I/O gain errors: ε < 1/λ₁₁ (2×2 special case G(s) = g(s)G₀).
- **Eigenvalues are a poor gain measure**: spectral radius ρ(G) can be 0 while σ̄(G) = 100 (nilpotent matrix); eigenvalues only measure gain in eigenvector directions (input = output direction); use σ̄ for performance, ρ only for stability.
- **Matrix norms used**: σ̄ (induced 2-norm, kGk₂), Frobenius, max row/column sum; only induced norms support gain bounds.
- **SVD (decoupling) controller**: K = W₁ K_s W₂ with W₁ = V, W₂ = Uᵀ rotates into principal directions, design diagonal K_s per direction — robust when done in the *right* directions (exercise: SVD control of the column IS robust where inverse-based fails).

## Mental Models
- "Check margins one-loop-at-a-time and you will be fooled" — MIMO failure lives in *simultaneous* perturbations; that's what μ exists to compute.
- "σ̄(S) is the worst-case error amplifier" — bound it and you've bounded performance in every direction.
- "Large RGA elements ⇒ never invert the plant" — inverse-based control of γ ≫ 1 plants turns small input errors into large output errors.
- "NP + RS ⇏ RP in MIMO" — the distillation column is stable-but-useless under 20% gain error; test RP explicitly.

## Anti-patterns
- **Inverse-based/decoupling control on large-RGA plants**: perfect nominal response, catastrophic under input uncertainty (distillation example).
- **Judging robustness by per-channel GM/PM or by absence of S/T peaks**: both passed in the distillation example while RP failed.
- **Using eigenvalues of G(jω) as MIMO gains**.
- **Forgetting non-commutativity** when manipulating block diagrams (G(I+KG)⁻¹ ≠ (I+GK)⁻¹G is false — they're equal by push-through; but G(I+GK)⁻¹ doesn't exist).

## Reference Tables

### SISO → MIMO generalization map
| SISO tool | MIMO replacement | Caveat |
|---|---|---|
| \|G(jω)\| | σ̄(G(jω)) (and σ̲ for best/worst) | direction-dependent |
| \|S\| ≤ bound | σ̄(S) ≤ bound | worst direction |
| ω_B from \|S\| | ω_B from σ̄(S) = 0.707 | bandwidth becomes a region |
| GM/PM | σ̄(T), σ̄(S) peaks; μ | per-channel margins misleading |
| Bode stability condition | no direct generalization | MIMO phase ill-defined |
| NP + RS ⇒ RP | false | must check RP (μ) |

### Distillation column physics (canonical ill-conditioned example)
| Direction | Input pattern | Gain | Meaning |
|---|---|---|---|
| Strong (σ̄ = 197) | u₁ − u₂ = L − V (external flow imbalance) | huge | high-purity columns hypersensitive to D = V − L imbalance |
| Weak (σ̲ = 1.39) | u₁ + u₂ = L + V (internal flow) | ~1 | making both products purer needs large actions |
| RGA | λ₁₁ = 35.1 | | inverse-based control fragile; I/O gain errors destabilize at ε > 1/λ₁₁ |

### Generalized plant recipe
1. Identify w (r, d, n), z (errors to minimize), v (measurements), u.
2. Break loops around K; P = transfer [w;u] → [z;v], weights folded into P.
3. Normalize weights so |w|, |z| ~ 1 ⇒ spec = ‖N(K)‖∞ < 1.
4. Solve min_K ‖N(K)‖∞ (H∞) or mixed S/KS/T stacks.

## Key Takeaways
1. Directions are the essence of MIMO: use SVD at the bandwidth frequencies that matter, not just at DC.
2. γ(G) = σ̄/σ̲ large + input uncertainty = the fundamental MIMO difficulty; σ̲(G) ≳ 1 is the input-authority requirement.
3. Per-channel margins and S/T peaks are necessary-ish but NOT sufficient robustness indicators; simultaneous structured uncertainty needs μ (Ch 8-9).
4. σ̄(S) ≤ 1/|w_P| is the MIMO performance spec; ω_B from σ̄(S).
5. Formulate everything as P (weights inside) and minimize ‖N‖∞ — the book's design engine from here on.
6. Never invert an ill-conditioned plant; decouple in principal directions (SVD controller) or accept diagonal structure.

## Connects To
- **Ch 2**: all these are the MIMO shadows of S/T loop shaping.
- **Ch 5-6**: σ̲(G), γ(G), RGA become the controllability toolkit.
- **Ch 7-8**: uncertainty representation + RS/RP conditions (σ̄(T) bounds, μ) formalize the two motivating examples.
- **Ch 10**: variable selection uses σ̲ and QR to avoid the shopping-cart trap.
