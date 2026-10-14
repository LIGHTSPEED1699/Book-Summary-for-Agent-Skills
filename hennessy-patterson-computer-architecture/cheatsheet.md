# Cheatsheet — formulas, numbers, tables (CAQA 6th ed.)

## Formulas
- Amdahl: S = 1/((1−F) + F/k); max = 1/(1−F). F = fraction of ORIGINAL time.
- CPU time = IC × CPI × cycle time; Pipeline CPI = ideal + structural + data + control stalls.
- AMAT = HT + MR×MP; multilevel: AMAT = HT₁ + MR₁(HT₂ + MR₂·MP₂).
- Vector time ≈ start-up + n/lanes per convoy; chime model.
- Die yield = (1/(1+D·A))^N (D≈0.012/cm², N≈33–35, 2022); dies/wafer ≈ πr²/A − πd/√A.
- Energy: E = ½CV² per transition; power = E×f; DVFS 15% V → 0.72×E, 0.61×P.
- Coherence-miss bandwidth: coherence traffic ≤ fraction of cache bandwidth → CMR ≤ (cycles available)/(refs×penalty) (worked: 16 cores → CMR ≤ 0.26%).
- Outstanding misses ≈ bandwidth × latency (16GiB/s × 36ns ÷ 64B ≈ 9; double → 18).
- Queuing: U = λS; R = S/(1−U); R = D + W; utilization law X_i = U_i/S_i.
- Roofline: Perf = min(π, β×I); ridge = π/β.
- TCO ≈ CAPEX + 3–4×OPEX; ~$2/W-year; WSC build $7–10/W; server ~$0.10–0.11/hr.
- PUE = total facility power / IT power (Google fleet 1.10).
- CO2e = kWh × grid factor (varies 5–10× by region).
- Redundant pair MTTF ≈ MTTF²/(2·MTTR).
- Blocking: memory words 2N³+N² → 2N³/B+N² (B = block size).
- HoL blocking throughput limit ≈ 2−√2 ≈ 58.6% (input-queued switch).

## Energy ladder (TSMC 7nm, relative units)
8-bit add 1000 · 32-bit add 3000 · 16-bit mul 3000 · 32-bit mul 18,000 · 32KB SRAM read 17,000 · 1MB SRAM 40,000 · **DDR4 32-bit read 187,400,000**.

## Memory latencies (i9-12900 class)
L1 4–5c · L2 15c · L3 50c · DRAM ~200c total. TLB: L1 1c, L2 TLB 8c, page walk 24 accesses (virtualized).

## Coherence protocol quick table
| Protocol | States | Notable |
|---|---|---|
| MSI | M,S,I | minimal |
| MESI | +E | clean-exclusive; CXL |
| MESIF | +F | one responder (Intel) |
| MOESI | +O | dirty-shared, no writeback (AMD) |

## Consistency ladder
SC → TSO (x86: W/R relaxed) → PSO (W/W too) → release/acquire (ARM/RISC-V/C++). DRF contract = relaxed HW behaves SC.

## Parallelism map
ILP (Ch3, pipelining/speculation) · DLP (Ch4, vector/SIMD/GPU) · TLP (Ch5, coherence/consistency) · RLP (Ch6, WSC) · DSA (Ch7, all levels compiler-managed).

## DSA five guidelines (audit checklist)
1. Dedicated memories, minimize movement. 2. Reinvest dropped OOO/speculation transistors in ALUs/memory. 3. Simplest parallelism matching the domain. 4. Smallest data types (int8/bf16/fp8/fp4; wider accumulate). 5. Domain programming model (JAX/PyTorch/CUDA).

## Key machines (6th ed. reference points)
- Cortex-A53: 2-wide in-order, 32KiB L1s, 1MiB L2, PMD class.
- Golden Cove: 6-wide rename, ROB 512, 8-wide retire, 48KiB L1D, AMX.
- i9-12900: 8P+8E, 30MiB noninclusive L3, DDR5 77GB/s.
- H100: 132 SMs, HBM3 3330GB/s, fp8, 700W. T4: 70W passive, GDDR6 (in-band ECC tax).
- TPU v4: 2 TCs, 4×128×128 MXU, 160MiB SRAM, 275 TFLOP bf16, 4096-chip 3D torus.
- IPU Bow: 1472 cores, 897MiB SRAM, no DRAM, BSP, ≤256 chips.
- Graviton3: 64 OOO Arm cores, DDR5, always-on encryption.
- Power10: 15 cores, 16 rings, 97% scaling to 220 cores.

## Benchmark sanity rules
- Geometric mean of ratios (reference machine cancels).
- base = one flag set; peak = per-benchmark tuning; rates = throughput, speed = latency.
- MLPerf: fixed/benchmark/open; demand field conditions (ECC, cooling, sustained).
- Never compare miss rates across speculative vs in-order; use MPKI.

## Fallacy tripwires (one-liners)
Every exponential slows · nm is marketing · speedup plots lie · peak ≠ observed · benchmarks rot · MTTF ≠ never · 100× GPU is a myth · cloud is profitable · wimpy nodes cost latency · PUE is gamed · DNN carbon 100× overstated · multicore isn't a power savior · batch≠1 for inference SLOs · no compiler = no DSA.
