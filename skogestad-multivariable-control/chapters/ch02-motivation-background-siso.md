# Chapter 2: Motivation and Background (SISO classical design)

## Core Idea
All of feedback design is frequency-by-frequency shaping of two complementary functions — S (keep small where disturbances/references live) and T = I − S (keep small where noise and unmodeled dynamics live) — and every classical margin, peak, and bandwidth rule is a proxy for that shaping; the MIMO machinery later is this same idea with singular values replacing magnitudes.

## Frameworks Introduced
- **S/T decomposition of the loop**: e = S(G_d d − r) + T n; y = T r + S G_d d + T n; u = K S(r − G_d d) = T G⁻¹(r − G_d d).
  - When to use: any loop analysis; write every signal in terms of S, T, L = GK first.
  - How: S = (I+L)⁻¹, T = L(I+L)⁻¹, S + T = I. With measurement dynamics G_m: L = GKG_m.
- **Why feedback (3 reasons)**: unknown disturbances, model uncertainty, unstable plants. Model uncertainty ≠ fictitious disturbance: LQG treats E u as noise, but noise can't destabilize while E inside the loop can — must treat model uncertainty explicitly.
- **Loop-shaping design**: specify jL(jω)j shape, then K = L/G.
  - How: (1) crossover ω_c set by required speed (ω_c ≥ signal frequencies to track/reject); (2) slope N = −1 through crossover (guarantees PM ≥ 45° if no extra lag), roll-off ≥ 2 beyond; (3) system type: one integrator in L per integrator in r (step → 1 integrator, ramp → 2) for offset-free tracking.
- **Bandwidth definitions**: ω_B = first crossing of |S| = 0.707 from below (preferred — S magnitude alone indicates performance); ω_BT (|T| crossing) can mislead badly with RHP zeros (T ≈ 1 in magnitude but wrong phase); ω_c (|L| = 1) lies between them for PM < 90°.
- **Peak criteria M_S, M_T**: M_S = max|S|, M_T = max|T|. Design rule: M_S ≤ ~2 (6 dB), M_T ≤ ~1.25-1.4. M_S < 2 guarantees GM ≥ 2 and PM ≥ 29° — peaks subsume margins. Distance from L to −1 point is M_S⁻¹.
- **Weighted sensitivity (H∞) design**: performance spec |S| ≤ 1/|w_P| ⇔ ‖w_P S‖∞ < 1 with w_P(s) = (s/M + ω_B*)/(s/M + ω_B*·A): A ≤ 1 steady-state error bound, M ≥ 1 peak bound (≈2), ω_B* bandwidth. Mixed sensitivity: stack N = [w_P S; w_u KS] (or w_T T), minimize ‖N‖∞ = max σ̄(N); H∞ optimal controllers give flat σ̄(N(jω)) = γ_opt; stacking costs at most √n factor per spec.
- **Weight selection shortcut**: let w_P look like |G_d| where |G_d| > 1 (disturbance rejection needs |S G_d| < 1); or take S from an initial loop-shaped design and back out the weight.
- **Inverse-based design**: for minimum-phase G, K = G⁻¹ × filter to set ω_c; plant zeros/poles cancel into L; RHP zeros/delays must stay in L (never invert them).

## Key Concepts
- **Frequency response**: G(jω) = steady-state sinusoidal gain/phase at ω; phasor notation y(ω) = G(jω)u(ω) used throughout, valid for MIMO with complex vectors/matrices.
- **Minimum phase**: stable + no delays/RHP zeros → Bode gain-phase relation; phase ≈ (π/2)·local log-slope N(ω). RHP zero at z adds phase −2arctan(ω/z) at unity gain; delay θ adds −ωθ.
- **Ultimate gain K_u / period P_u**: P-controller gain/period at instability onset (Ziegler-Nichols basis); book warns ZN PI/PID tunings are aggressive (example: M_S = 3.92, PM = 19° — unacceptable).
- **ω_180**: phase crossover (∠L = −180°); Bode stability condition: stable iff |L(ω_180)| < 1 (for single-crossing stable plants).
- **Time-domain measures**: rise time t_r, settling t_s, overshoot ≤ 1.2, decay ratio ≤ 0.3, excess variation; TV = ‖impulse response of T‖₁ ≈ M_T (bounds: TV ≤ M_T ≤ n·TV for order n).
- **Delay margin from PM**: tolerable extra delay θ_max = PM/ω_c (radians!) — lowering ω_c buys delay robustness.

## Mental Models
- "S small where signals are, T small where uncertainty/noise are" — the whole design problem in one sentence.
- "|S| is a performance meter, |T| is a robustness meter" — and M_S is the single best scalar health check of a loop.
- "Speed is capped by non-minimum-phase physics": ω_c < 1/θ (delay) and ω_c < z/2 (RHP zero) keep their phase penalty under ~55°.
- "Margins are proxies; peaks are the truth": M_S < 2 ⇒ GM > 2, PM > 30°; the converse doesn't hold.

## Anti-patterns
- **Ziegler-Nichols as final design**: aggressive; yields M_S ≈ 4, oscillatory responses; use as starting point only.
- **Using ω_BT (|T| bandwidth) as speed indicator**: with RHP zeros it overstates achievable speed ~10× (book example: ω_BT = 1.0 vs actual rise time ≈ 1/ω_B).
- **Inverting RHP zeros/delays**: they must appear in L; canceling them destabilizes or wastes margin.
- **Treating model error as disturbance noise** (LQG habit): ignores that uncertainty closes the loop and can destabilize.

## Reference Tables

### Design objectives → loop gain direction
| Objective | Needs |
|---|---|
| Disturbance rejection, tracking, stabilize unstable plant | L large |
| Noise rejection, small inputs, proper controller, NS/RS (stable plant w/ delays, RHP zeros, unmodeled dynamics) | L small |
Resolution: large L below ω_c, small L above.

### Typical design targets
| Quantity | Rule of thumb |
|---|---|
| M_S | ≤ 2 (guarantees GM ≥ 2, PM ≥ 29°) |
| M_T | ≤ 1.25-1.4 |
| GM | > 2 |
| PM | > 30° |
| ω_c vs delay | ω_c < 1/θ |
| ω_c vs RHP zero | ω_c < z/2 |
| Slope of L at crossover | ≈ −1 (N = −1.5 max for PM 45°) |
| Overshoot / decay ratio | ≤ 1.2 / ≤ 0.3 |

### Performance weight w_P(s) = (s/M + ω_B*)/(s/M + ω_B* A)
| Knob | Meaning |
|---|---|
| A ≤ 1 | max steady-state tracking error (A→0 forces integrator) |
| M ≥ 1 | max S peak (use ~2) |
| ω_B* | required bandwidth (≈ ω_c) |
Steeper low-freq demand (slope −2 for L) → use w_P2 = (s²/M + ω_B*²)/(s²/M + ω_B*²A).

## Key Takeaways
1. Write every closed-loop signal in S/T form before analyzing anything.
2. Shape L: integrators for type, slope −1 at crossover, ω_c set by signal content, roll-off ≥ 2, keep RHP zeros/delays' phase penalty < 55° at ω_c.
3. Check M_S ≤ 2 as the primary loop health metric; margins follow automatically.
4. ω_B (from |S| = 0.707) is the honest bandwidth; ω_BT lies with RHP zeros.
5. H∞ weighted sensitivity = loop shaping made formal: weights are specs, γ_opt < 1 means specs met, H∞ solution is flat.
6. Tracking and disturbance rejection can demand opposite low-frequency shapes — resolve with 2-DOF (prefilter F_r on r, separate from K).
7. TV ≈ M_T links frequency peaks to time-domain ringing.

## Connects To
- **Ch 3**: turns M_S/ω_B rules into formal requirements incl. robustness.
- **Ch 7-8**: SISO RS/RP with uncertainty → MIMO singular-value versions of exactly these weights.
- **Ch 8-9**: μ analysis and H∞/loop-shaping synthesis generalize mixed sensitivity.
- **Ch 5**: RHP-zero/delay bandwidth limits quantified as controllability.
