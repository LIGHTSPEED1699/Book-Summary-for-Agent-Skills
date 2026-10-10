# Cheatsheet — Shinskey, Process Control Systems (4th ed.)

Quick reference: formulas, tuning tables, and the numbers worth memorizing. Equation numbers are the book's.

## The five numbers to internalize
- **IE_b = |Kp·Δq|·Td** — dead-time floor on integrated error. No tuning beats it.
- **e_b = Δq·τd/τ1** (integrating) — best possible peak error; tuned PI lands at 1.48·e_b, PID at 1.13·e_b.
- **τn = 4τd** — undamped period of an integrating process + dead time; Pu = 63.7·Kp·τd/τ1.
- **Peak γ 2–3** — acceptable cyclic load sensitivity; keep load periods away from ~6τd.
- **τd/τt < −0.5** — exothermic reactor uncontrollable by tuning; redesign (F↓, x0↓, UA↑).

## Process identification (Ch. 4)
- Open loop: step m, draw max-slope line; τd at baseline intercept; τ1/Kp from traverse time. (The intercept actually measures τd + τ2 — fine for D, overestimates P if τ2 > 0.2τd.)
- Closed loop: narrow P until undamped cycle → τn, Pu directly. Prefer this: I/τn and D/τn are more robust to τd/τ1 error than I/τd (Table 4.6).
- PI optimum damped period ≈ 1.35·τn regardless of τd/τ1; interacting PID ≈ 3τd.

## Tuning tables

### Pure dead-time process, minimum IAE (Ch. 1)
| Mode | Setting | IAE/IAE_b |
|---|---|---|
| I only | I = 1.6·Kp·Td | 2.04 |
| PI | P ≈ 250·Kp, I ≈ Td/2 | 1.30 |

### PID step load, minimum IAE (Table 4.4; P in units of τd/τ1)
| τd/τ1 | Interacting I/τd, D/τd, P, IAE/IAE_b | Noninteracting |
|---|---|---|
| 2.0 | 0.77, 0.35, 72, 1.25 | 0.92, 0.32, 55, 1.13 |
| 1.0 | 1.03, 0.40, 88, 1.58 | 1.17, 0.37, 67, 1.44 |
| 0.5 | 1.17, 0.48, 105, 1.70 | 1.43, 0.41, 74, 1.61 |
| 0.2 | 1.43, 0.52, 105, 1.86 | 1.77, 0.41, 76, 1.79 |
| 0 (integrating) | 1.57, 0.58, 108, 1.99 | 1.90, 0.48, 78, 1.94 |

PID vs PI on an integrating process: IAE/IAE_b falls 4.58 → 1.99. Noninteraction buys < 3%.

### Set-point steps (Ch. 4)
- Dead-time process, PI: P = 266Kp, I = 0.47τd → 1.39·IAE_b (IAE_b = |Δr|τd).
- Integrating process: use PD, both on deviation: P = 140τd/τ1, D = 0.42τd → 1.24·IAE_b (IAE_b = |Δr|(τd + 0.5·tr)).
- Ramp following without overshoot: PD P = 120τd/τ1, D = 0.45τd (~1.2τd late); if integral required, D > I: P = 360τd/τ1, I = 0.55τd, D = 1.9τd.

### Batch / zero load (Ch. 12)
- Base rules: **P = 120τd/τ1, D = τ2 + 0.5τd**, derivative on the controlled variable.
- Table 12.1 (IAE/IAE_b): batch one-stage PID (P 173τd/τ1, I 1.57τd, D 0.57τd, preload q−4%) = 1.99; batch two-stage (P 110, I 2.0τd, D 0.57τd, preload q−10%) = 2.48; delayed-I variant = 2.47; continuous two-stage PID = 2.63.

### Unstable exothermic reactors (Ch. 10, interacting PID, P as multiple of −Kt)
| τd/τt | I/τd | D/τd | P | −P/Kt |
|---|---|---|---|---|
| −0.2 | 1.90 | 0.60 | 100·Kt·τd/τt | 20 |
| −0.5 | 2.00 | 0.80 | 112·Kt·τd/τt | 56 |
| −0.80 | 2.40 | 1.00 | 120·Kt·τd/τt | 96 |
| −1.0 | no stability margin | | | |

Steady-state stability: P < −100Kt (10.22). Dynamic: P > 100Kt·τd/τt (10.23).

## Feedforward (Ch. 7)
- Integrals of flow: **m = r + (Kq/Km)q** (7.2). Properties: **m = r·q·(gq/gm)/Kp** (7.7).
- Heat exchanger: Ws = Wp·K(T* − Ti); calibrate one coefficient K; trim via set point.
- Dead-time imbalance: dc(t) = dr(t−τdm) + (dq·r/q)(τdq − τdm) (7.18). Compensate delay τdq − τdm; impossible if τdm > τdq.
- Compensator settings by class (Table 7.1): class I τ1 = τm, τ2 = τq; class II add τd = τdq − τdm; class IIIb τ1 = ½(τdm − τdq), τ2 = τ1/10; class IIIc τ1 = 0.8τm + 0.4(τdm − τdq), τ2 = τq + 0.2τm + 0.6(τdm − τdq). Always τ2 ≥ τ1/10; ratio ≤ 10.
- Tune order: dead-time comp → IE = 0 (sets τ1 − τ2) → ratio τ1/τ2 for min IAE.
- Results: feedforward + lead-lag cuts IAE ≥ 10× vs feedback; class III still 3–5×.
- Drum boiler: WF = Ws + (mL − 0.5)·scale; back-calculate fL = 0.5 + (WF − Ws)/K for windup protection.

## Interaction (Ch. 8, 11)
- λ = 1 no interaction; λ < 0 never pair; 0 < λ < 1 costs period; λ > 1 stiff set point.
- Single-loop gain product at stability limit (Table 8.1): λ = 0.5 → 0.707∠−135°; λ = 2 → −0.586; λ → ∞ → −0.5.
- Decoupler error to destabilize (Table 8.2): λ = 1.5 → 73%; λ = 2 → 41%; λ = 8 → 6.9%; λ = 16 → 3.3%.
- Column pairing: λ_y1 = 1 − [(dy/dx)1/(dy/dx)2] (11.19); D/F curves always opposite slope to the rest. RIE = (μ1 + |μ2|)·λ (11.21). Ethylene fractionator: L–B best for heat-balance upsets (RIE ≈ 1.0).

## Loop properties (Table 3.3)
| | Flow/pressure | Level | Composition | Temperature |
|---|---|---|---|---|
| Dead time | no | no | constant | variable |
| Noise | always (flow) | always (level) | often | none |
| Typical P | 50–500% | 0–5% | 5–50% | 100–1000% |
| Integral | essential (flow) / unnecessary (press.) | seldom | essential | yes |
| Derivative | no | no | if possible | **essential** |
| Valve | linear / equal-% | linear | linear | equal-% |

- Level under P control: τm = τ1·P/100 (3.28); level amplitude ∝ 1/P but flow amplitude ∝ 1/P²; keep P > 200τf/τ1 with a filter (3.33).
- Mixing model: τd = (V/F)(1−α)/2, τ1 = (V/F)(1+α)/2 (3.46–3.47).
- Orifice rangeability: at 10% flow a 1% element + 0.25% transmitter gives 1.25% flow error; at 5%, 2.5% (Table 3.1).

## Energy systems (Ch. 9)
- Drum level inverse response: τn = 3.94·ti from inversion time ti (9.26–9.28); shrink/swell = lag with negative lead, φi = −2tan⁻¹(2πτi/τ0) at unity gain (9.25).
- Combustion air targets: gas 5% excess air (0.9% O2), oil 6% (1.1%), coal 10% (1.9%).
- Fired heater / exchanger PID: P = 140τi/τI, I = 2τi, D = 1.1τi → 25% lower IAE than PI (P = 150τi/τI, I = 9τi).
- Pumps: Δp/ρ = k1N² − k2F² (9.31); hhp = F·Δp/1714 (gpm, psi); speed control at constant load cuts power ~3× vs throttling; cube law only with zero static head.
- DC variable-speed drives: stall < 5%, restart at 10% → sawtooth limit cycle at low load; VFDs exempt.

## Reactors (Ch. 10)
- Plug flow: y = 1 − e^(−kV/F); back-mixed: y = (kV/F)/(1 + kV/F), τx = V/(F + Vk) (10.9). Max slope at kV/F = 1.
- Dynamic gain exceeds steady-state: back-mixed dy/dT = (E/RT²)·y (10.15).
- Kt = −UA/[UA + FρC − HrFx0(dy/dT)x] (10.20); τt = KtVρC/UA (10.21).
- Unstable reactor: −180° at steady state (negative resistance); two resonant peaks ~3τd and ~9τd.
- Recycle without composition loop → non-self-regulating (x1 = (X−Y)/V·∫dt, 10.24) → no integral on composition.
- pH: sensitivity ≈ 10⁶ pH/N strong/strong; weak acid at pH = pKa ≈ 100× easier; carbonates buffer at 6.35 and 10.25. Rangeability: sequence two 50:1 equal-% valves ≈ 2500:1; only one open at a time.

## Distillation (Ch. 11)
- Fenske separation factor S; binary y = Sx/[1 + x(S − 1)] (11.8).
- Ryskamp: accumulator level → L + D; composition → D/(L + D); subtractor decoupler K = range D/range L. Van Kampen: set K > D/L to turn the accumulator into a lead (splitter period 5 h → 30 min).
- Floating pressure: ~1% energy per °F of coolant reduction; VPC on pressure I ≈ 1 h.
- Log composition control: e = ln c − ln r (11.24) when Kp ∝ c.
- Evaporators: V0 = W0(1 − x0/xn)/nE (11.34); nE ≈ 0.94n.
- Flooding: column ΔP is the index; act on first rise (emptying takes as long as filling).

## Nonlinear elements (Ch. 5)
- Describing-function rule of thumb: gain falling with amplitude → stable everywhere (dead band + P, Table 5.1); gain rising with amplitude → limit cycle (dead band + PI, Table 5.2 onset at A/a ≈ 3.3).
- Derivative gain limit 10–20: negligible effect for τ0 > D; at τ0/D = 5 phase lead drops only 7° (Table 4.3).
- Interacting PID: D_eff ≤ I_eff/4; with integral feedback from output and D in output path, Kc = (100/P)(1 + D/I)/(1 − D/I) → negative beyond D = I (4.33).

## Robustness warnings
- Widening P on an integrating process: sensitivity peak moves from ~3 to ~10τd and grows — loose tuning is not safer, it's slower and often worse.
- Self-tuning controllers don't suit batch (one shot per batch).
- Feedforward pH: a change in influent pH can drive the reagent valve the wrong way; feedback + fast delivery wins.
