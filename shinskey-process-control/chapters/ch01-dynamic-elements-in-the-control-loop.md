# Chapter 1: Dynamic Elements in the Control Loop

## Core Idea
Every control loop can be decomposed into elementary dynamic blocks — dead time, capacity (integrating and self-regulating), and the controller modes — and the loop's behavior (period, damping, error) is fully predictable from those elements. Controller tuning is the search for the best settings against a measurable objective function, and Shinskey's chosen function is **integrated error / integrated absolute error (IAE)**, not decay ratio.

## Frameworks Introduced
- **Negative feedback loop**: controller manipulates m to counteract load q and restore deviation e to zero. Process and controller each have a steady-state gain (Kp, Kc) and a **dynamic gain** vector (gp, gc) with scalar magnitude G and phase angle φ.
  - When to use: always the starting analysis for any loop.
  - How: loop gain product KcGcKpGp; phase sum φp + φc.
- **Conditions for uniform oscillation**: a loop oscillates steadily (1) at the period where total dynamic phase lag = −180° (plus the 180° of negative feedback), and (2) when the loop gain product at that period = 1.0. These two conditions are the foundation of all tuning rules in the book.
- **Natural period (τn)**: the period of oscillation when the controller contributes no phase shift. It is a property peculiar to each loop; a damped loop has a **phase margin** (unaccounted phase lag at the observed period).
- **Dynamic gain of each element** (exact Shinskey formulations):
  - Dead time: gain 1.0, phase −360°·Td/τ0. "Dead time is the most difficult dynamic element naturally occurring in physical systems."
  - Integrator / integrating (non-self-regulating) process: gain τ0/(2πI) or τ0/(2πτ), phase −90° at every period.
  - First-order lag (self-regulating capacity): G₁ = cos φ₁, φ₁ = −tan⁻¹(2πτ₁/τ0); phase never exceeds −90°, so single-capacity processes can be controlled at zero proportional band — the easiest to control.
- **Quarter-amplitude decay**: loop gain product 0.5 (each full cycle decays to ¼). Acceptable classic rule; **(4th ed) "belongs to the past"** — high-performance controllers produce optimum curves without oscillation or measurable decay.
- **Integrated error criteria (4th ed, front and center)**:
  - **IE = ∫e dt = I·Δm** for any controller with integral action — units of %·min; multiplied by ingredient cost, it is dollars given away. IE is the economic measure of controller performance.
  - **IAE = ∫|e| dt** — the single criterion that ensures both offset elimination and damping; tuning in the book minimizes IAE.
  - **ISE rejected**: no general economic function varies as the square of deviation.
  - **Overshoot** = ratio of first two peaks of the load-response curve; a low but measurable overshoot is a feature of minimum-IAE curves (and often ≈ the decay ratio).
  - **Performance = IE_best/IE_actual**, compared only at equivalent stability (minimum-IAE) conditions.
- **Best possible load response**: no feedback controller can act before the controlled variable responds, so the deviation must be sustained one dead time; **IE_b = |Kp·Δq|·Td** (dead-time process). This is the yardstick every controller is measured against.

## Key Concepts
- **Process gain Kp** = dc/dm; split into steady-state Kp and dynamic gain gp (vector).
- **Proportional band P**: Kc = 100/P; proportional-only control leaves **offset** = P(m−b)/100.
- **Integral (reset) time I**: output rate dm/dt = e/I; drives deviation to zero but adds 90° phase lag.
- **Undamped proportional band Pu / undamped integral time Iu**: settings giving loop gain exactly 1.0; damping is achieved by moving away from them (P > Pu or I > Iu).
- **Non-self-regulating (integrating) process**: no natural equilibrium (e.g., level with metered outflow); cannot be left unattended.
- **Self-regulation**: outflow depends on the controlled variable — natural negative feedback inside the process. The parameter **k** (index of self-regulation) is nearly always ≪ 1 and drops out of the gain product: time constant and steady-state gain vary, but their product is constant.
- **τd/τ₁ ratio**: the master index of process difficulty. For τd/τ₁ ≤ 0.5 a self-regulating capacity behaves like an integrator.

## Mental Models
- **Think of the loop as a pendulum**: it resonates at its own natural period; disturbances excite that component and the loop rejects the rest. Measure the period → infer the process.
- **Phase budget**: −180° is shared among dead time, lags, and the controller. Every control mode you add spends phase; the period tells you where the budget went.
- **Dead time sets the floor on error**: IE_best = Kp·Δq·Td — you cannot tune your way below it; you can only design dead time out of the process.
- **Tune against IAE, diagnose with symmetry/overshoot (4th ed)**: a minimum-IAE curve has low measurable overshoot and near-symmetric excursion; PI phase lag at minimum IAE is always < 45° — if calculated phase lag exceeds 45°, the controller is definitely mistuned (classic symptom: PI on level with a huge proportional band producing a slow, light cycle).

## Anti-patterns
- **Tuning to quarter-amplitude decay as the goal (4th ed)**: it belongs to the past; it does not correspond to minimum error and misleads with high-performance controllers.
- **Minimizing IE alone**: the lowest achievable I is Iu (the stability limit) — IE minimization without damping is unsatisfactory; use IAE.
- **Using ISE**: accumulates in oscillating loops with no economic justification.
- **Independent (non-ISA) PI form**: proportional gain changes the controller's phase angle, so damping adjustments can destabilize; the standard ISA algorithm's phase depends only on period and I.
- **Assuming a proportional loop can oscillate with only one lag**: single-capacity and integrating processes under P control never reach −180° — no oscillation, and P can be set very tight.

## Reference Tables
Exact results for a pure dead-time process (Td), process gain Kp:

| Control | Undamped setting | Natural/loop period | Minimum-IAE setting | IAE/IAE_best |
|---|---|---|---|---|
| P only | Pu = 100Kp | τn = 2Td (exact) | — | ∞ (offset) |
| I only | Iu = 0.64KpTd | τ0 = 4Td | I = 1.6KpTd | 2.04 |
| PI | — | — | I ≈ 0.5Td, P ≈ 235Kp (3ed Table 1.1); (4th ed) P = 250Kp, I = Td/2 | 1.30 (IE-based performance 80%) |

Dead time + capacity, PI tuned for minimum IAE (3ed Table 1.2): as τd/τ₁ falls from ∞ to 0, optimum I rises from 0.5Td to ~4Td and P from 235Kp to ~105Kp·Td/τ₁; absolute controllability improves (index IAE/|KpΔq|Td falls).

## Worked Example
**Conveyor weigh feed (dead time only)**: belt 12 ft/min, weigh cell 4 ft from valve → Td = 4/12 = 0.333 min; valve 10% → 14% weight change → Kp = 1.4.
- Integral control, minimum IAE: I = 1.6KpTd = 1.6 × 1.4 × 0.333 ≈ **0.75 min**; damped cycle period ≈ 4Td ≈ 1.3 min (extended by damping).
- PI control, minimum IAE (3ed Table 1.1): I ≈ 0.5Td ≈ 0.17 min, P ≈ 235Kp ≈ 330%; period ≈ 2.8Td ≈ 0.9 min; IAE only 30% above best possible.
- Best possible IE = Kp·Δq·Td; e.g., a 10% load step gives IE_best = 1.4 × 10 × 0.333 ≈ 4.7 %·min.

**(4th ed) PI response forensics**: with P = 250Kp and I = Td/2 on a 30% step deviation, the proportional action steps output 8% immediately, and the integral "repeats" that 8% step every I — twice during the dead time — so the manipulated trajectory is visible in the deviation one dead time later. Observed period 2.87Td, overshoot 0.14, decay ratio 0.24, controller phase lag ≈ 41° (< 45° ⇒ properly tuned). IE = I·Δm formula gives IE = 1.25Kp·Δq → performance 80% of best possible.

## Key Takeaways
1. Two conditions define the stability limit: phase sum −180° and loop gain 1.0; all tuning rules derive from them.
2. τn = 2Td (P control of dead time) is exact, not an approximation — measure the period, get the dead time.
3. Tune for minimum IAE; express performance as IE_best/IE at equal stability.
4. Quarter-amplitude decay is a legacy criterion (3ed uses it as fallback; 4ed explicitly retires it).
5. Dead time is the enemy: it sets the irreducible error floor; design it out where possible.
6. Self-regulation parameter k almost always drops out — the gain product KpG₁ is what matters.
7. PI phase lag at optimum is always < 45°; a bigger calculated lag means mistuning.

## Connects To
- **Ch 2**: combining these elements into real (second-order, multicapacity) processes.
- **Ch 4**: full tuning rules and error criteria (IE functions, robustness) built on this chapter's element analysis.
- **Ch 7**: feedforward exists to beat the dead-time error floor of feedback.
- External: classic PID literature; ISA standard PI algorithm; IMC/MPC (Ch 4's PID₂).
