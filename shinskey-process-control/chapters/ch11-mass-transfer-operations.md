# Chapter 11: Mass-Transfer Operations

## Core Idea
Distillation, evaporation, and drying each demand a different control philosophy. Distillation is a highly interacting multivariable process whose control design must begin with a material-balance model and relative-gain analysis; evaporation yields to rigorous mass- and energy-balance feedforward; drying can measure neither product quality nor flows, so control is inferential, built on a mass-transfer model of the dryer itself. In every case the model decides the configuration — which ratio is manipulated, which disturbance is inherently rejected, and how much the integrated error can be driven down.

## Frameworks Introduced
- **Material-balance + separation-curve model of a column**: the operating point is where the material-balance line crosses the separation curve.
  - When to use: any distillation control design, before touching RGA.
  - How: overall balance F = D + B (11.1); component balance Fz_i = Dy_i + Bx_i (11.2); the ratio D/F sets product split: (z_i − x_i)/(y_i − x_i) = D/F (11.3). Second relationship is the Fenske-based separation factor S = (y_i/x_i)/(y_j/x_j) (11.6). For a binary, y_i = Sx_i/[1 + x_i(S − 1)] (11.8) — a hyperbola; increasing S pulls it toward the origin (purity).
- **Operating curves**: each held-constant ratio (D/F, L/F, V/F, V/B, L/D, L/B) traces a distinct trajectory of y vs x on the y–x impurity plot.
  - When to use: to enumerate the candidate manipulated-variable pairs for composition control.
  - How: increment D/F at each held ratio and recompute compositions (Ex. 11.1 procedure). Constant-S and constant-L/D curves are nearly always closest together; constant reflux ratio (L/D) and constant boilup ratio (V/B) are farthest apart — always — and every other curve falls inside that envelope. The near-vertical V/B curve is the best base for regulating bottom composition.
- **2×2 RGA from curve slopes**: a 5×5 RGA of the column is meaningless because levels/pressure are fast and compositions slow, and any open flow drives levels to limits.
  - When to use: selecting which pair of manipulated variables controls the two compositions.
  - How: λ_y1(m1,m2) = 1 − [(dy/dx)_1/(dy/dx)_2] (11.19), slopes from Table 11.1. D/F (material-balance line) always has slope of opposite sign to the others: pairing a product flow with anything puts all relative gains in the 0–1 range; any other pair keeps the negative sign and gives λ outside 0–1 (the closer the two curves, the higher λ).
- **Disturbance-rejection sensitivity μ = (dm/m)/(dq/q)** (11.20): each candidate manipulated variable inherently rejects some loads.
  - When to use: as the second criterion after RGA, to break ties between λ near 1.0.
  - How: Table 11.3. D and B need zero change for heat-balance upsets but unit response to feed rate; L and V respond −1/+1 to heat; ratios (L/D, V/B) have zero sensitivity to feed rate — which is why flow ratios beat flow rates when feedforward would otherwise be needed.
- **Relative integrated error RIE = (μ1 + |μ2|)·λ_y1** (11.21) compares configurations on one number; for λ < 1 configurations add the detuning correction (0.22 + 0.78√λ)² in the denominator (11.22, 11.23).
- **Inferential control** (drying): when the controlled variable cannot be measured, compute its set point from a model of the process using the variables that CAN be measured — T*_0 = r + R·T_i (11.41).

## Key Concepts
- **Separation factor S** — function of relative volatility α, stages n, efficiency E, and energy input; constant S ⇔ constant L/D ⇔ constant D/V ⇔ constant L/V (11.15–11.18: V = Q_i/H_D, V = L + D).
- **Ryskamp system** (Fig. 11.4): accumulator level manipulates total condensed flow L + D; top composition manipulates the ratio D/(L + D); a subtractor (decoupler, K = range D / range L) converts a change in D into the opposite change in L. Preferred for the majority of columns (L/D > 1).
- **Van Kampen decoupler lead**: set K > D/L and the accumulator becomes a dominant lead instead of a lag — composition-loop period on a propylene-propane splitter fell from 5 h to 30 min.
- **Inverse response in the column base**: heat-input manipulation of base level can inverse-respond (typical of sieve trays at low load, valve trays at all loads — Buckley observed 11 min, forcing base level onto reflux). Liquid feed needs dynamic compensation (dead time + lag of feed-to-bottom trays) on any feed-ratio boilup so boilup starts rising only as base level begins to rise.
- **Logarithmic composition compensation**: process gain varies directly with the controlled impurity (Kp = k·c), so use e = ln c − ln r (11.24); controller gain then varies inversely with c. Fixes the slow-downscale/fast-overshoot asymmetry of high-purity loops (verified on a simulated methanol-ethanol column). Caveat: IE of equal-and-opposite upsets is no longer zero — tank-averaged composition drifts above set point.
- **Floating pressure saves energy**: relative volatility improves as pressure falls — nearly 1% energy per °F of coolant temperature reduction. Combine a tight PI pressure loop with an integral-only valve-position controller slowly driving the pressure set point to the condenser's extreme (I ≈ 1 h), and feed pressure forward to the separation control per Q = F·m(p_o + p) (11.25); temperature composition measurement needs pressure compensation T_b = T + [(p_b − p)/(dP/dT)]_x (11.26–11.27).
- **Constraint control**: maximum recovery runs at a constraint (condenser on a hot day, reboiler with heavy feed, column loading). Column differential pressure across trays is the flooding index — downcomer flooding shows as a sharp steady ΔP rise, and emptying the column takes as long as filling it, so act on first indication; ΔP override on heat input prevents it outright.
- **Multiple-effect evaporator economy**: vaporization per unit steam = nE with E ≈ 0.94 (Table 11.6: n=1→0.94, 2→1.84, 3→2.74, 4→3.64). Material-balance control: V_0 = W_0(1 − x_0/x_n)/nE (11.34); with feed density ρ, (1 − x_0/x_n) = 1 − m(ρ − 1) is linear (11.35), giving F* = V_0·nE/500 ÷ [1 − m(ρ − 1)] (11.36–11.37, 500 = gpm water → lb/h steam). Slope m is the feedforward set point, adjusted by the composition feedback controller.
- **Inferential dryer model**: rate in the falling-rate zone ∝ x/x_c; fluid-bed integration gives x ∝ (x_c·GC/H_v·A)·ln[(T_i − T_w)/(T_0 − T_w)] (11.38–11.40). Holding T_0 constant while load varies moves T_w and changes product moisture — the set point must move with T_i per (11.41). The T* generation is a positive-feedback loop: R sets steady-state stability, and a lag longer than the T_0 controller's integral time is required for dynamic stability.

## Mental Models
- **The column is its curves**: every control configuration is a trajectory on the y–x plot. Read the design off the picture — curve pairs close together interact badly (high λ), far apart interact well.
- **RGA picks the fight, sensitivity picks the loser**: λ near 1.0 on both sides (0.919 vs 2.11) is not decidable by algebra; the load you actually get (feed composition vs heat balance) decides, via RIE.
- **A ratio needs no feedforward**: manipulating L/D or V/B absorbs feed-rate changes through the level controllers — all four flows (B, V, L, D) move with feed automatically, no dynamic compensator.
- **Unmeasurable ≠ uncontrollable**: drying is controlled through a model (T* = r + RT_i) because the wet-bulb temperature and product moisture are not instrumentable; calibrate r and R in the field — raising either dries the product more.

## Anti-patterns
- **Building a 5×5 RGA of the column** — levels and pressure are fast, compositions slow; the honest object is several 2×2 arrays with levels/pressure assumed closed.
- **Manipulating D and B together for compositions** — they lie on one operating curve (single material balance); they cannot act independently.
- **Holding T_0 constant in a dryer** — that is the conventional scheme, and it silently raises product moisture as load rises because T_w rises with it.
- **Sharing one chromatograph between sample points on a slow interval** — analyzer dead time already limits the loop; sampling interval adds directly to it.
- **Trim heaters without feedforward thinking** — the trim loop must keep nE constant (fixed share of heat load) or the feedforward model is wrong; with feedforward, the trim heater is not really needed.

## Reference Tables
Table 11.2 — Relative gains λ_y1 (ethylene fractionator, 100 trays, α = 1.40, L/D = 4.0, E = 81.6%):

| x controlled by | y by D | y by L | y by S |
|---|---|---|---|
| B | — | 0.893 | 0.919 |
| V | 0.113 | 15.2 | 3.13 |
| V/B | 0.141 | 3.61 | 2.11 |

Table 11.4 — Relative integrated errors (same column): feed-composition upsets: B–L 3.83, B–S 4.77, V–L 4.38, V–S 3.89, V/B–S 4.51 (D–V 42.1, D–L 37.9, D–S 4.26). Heat-balance upsets: B–L 1.06, B–S 1.04, V–S 6.26, V/B–S 4.22 (V–L 30.4, V/B–L 7.22). L–B is best for disturbance rejection here.

Table 11.5 — Ethylene fractionator with side stream (121 trays, reflux/side-stream 4.6): λ for x_m: P 0.584–0.590 with V, V/B; side-stream P controlling w_h preferred (0.416/0.417 set).

Table 11.6 — Evaporator thermal economy: nE = 0.94, 1.84, 2.74, 3.64 for n = 1–4.

## Worked Example
**Ethylene fractionator, Ex. 11.1**: feed 47.0% ethylene (l), 51.1% ethane (h); distillate 99.7% / 0.2%; bottoms 2.0% / 94.6%. D/F = (0.47 − 0.02)/(0.997 − 0.02) = 0.461; S = (0.997/0.002)/(0.02/0.946) = 23,579. Increase D/F by 0.01 to 0.471: solve the quadratic (11.10) with a = 11,105, b = −10.81, c = −0.510(1 − 0.0005/0.471) → y_h = 0.00728, x_h = 0.9590, y_l = 0.9917, x_l = 0.00554. A 0.01 step in D/F moves ethylene purity 99.7 → 99.17% — the gain of the quality loops is enormous, which is why configuration (not just tuning) decides performance.
