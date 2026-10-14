# Ch7 — Domain-Specific Architectures (DSAs)

## The argument
- Post-Dennard + slowing Moore: energy budget is flat, so higher ops/s requires lower **energy per operation**. Instruction fetch + cache access cost more energy than the arithmetic itself (90nm: 125–150pJ overhead vs ALU op).
- Fix: raise **arithmetic operations per instruction** from 1 to hundreds → DSAs. The 8 pillars:
  1. **Interconnect** (data movement dominates energy; shorten wires, dedicated memories).
  2. **Memory hierarchy** (software-controlled scratchpads, not caches).
  3. **Arithmetic units** (10–1000× more, narrower).
  4. **Programming model** (DNN frameworks/DAGs, not ISA-level).
  5. **Flexible data types** (narrow: int8/bf16/fp8/fp4; accumulate wider).
  6. **Parallelism** (the simplest kind that matches the domain).
  7. **Compiler** (does everything: ILP, DLP, memory-level, TLP scheduling).
  8. **Cost** (amortize across a big enough market; WSC-scale deployment).
- Five design guidelines (used to audit every DSA below):
  1. Dedicated memories to minimize data movement distance.
  2. Invest the transistors saved from dropping OOO/speculation/prefetch into ALUs or memories.
  3. Use the simplest parallelism that matches the domain.
  4. Reduce data size/type to the simplest the domain needs.
  5. Use a domain-specific programming language/framework to port code.

## The domain: deep neural networks
- DNN = layers of matrix multiplies + nonlinear activations; training = forward + backward (gradient) passes; inference = forward only.
- Workloads: MLP → CNN → RNN/LSTM → **Transformer** (2017) → **LLM** (2022+); model mix shifts ~quarter-of-workload in 2 years; footprint/compute grow ~1.5×/yr → specialization must stay flexible.
- Key operation: matrix multiply-accumulate; arithmetic intensity high; precision tolerant (int8 fine for inference; bf16/fp16 for training).

## Google TPU v4 / v4 lite (the flagship example)
- **Systolic matrix unit (MXU)**: 4 × 128×128 per TensorCore; 128 inputs pipelined in, partial sums flow right, 1024 MACs/clock each; **compiler must feed it on time** (systolic latency is a programming concern).
- Memory: VMEM 16MiB per TC + **CMEM 128MiB common** (28% of die) — 160MiB software-managed SRAM, ~20× more energy-efficient than HBM; HBM 32GiB (v4) / 8GiB (v4 lite).
- **VLIW ~400-bit bundles**; **compiler-compatible, not binary-compatible** (Itanium lesson; XLA is the single compiler; HLO machine-independent vs LLO machine-dependent layers).
- XLA explicitly schedules ILP (software pipelining), DLP (2D register/memory layouts feeding the systolic array), **memory-level parallelism (no caches — compiler-scheduled tensor DMAs; 4D DMA unifies local/chip-to-chip/host)**, and TLP (4→4096 chips).
- v4 = 2 TensorCores, 275 TFLOP/s bf16, 6 ICI links → 3D torus **pods of 4096 chips >1 EFLOP/s**, deployed by the dozens.
- Guideline audit: dedicated memories ✓; 131,072 ALUs (10× a server CPU) ✓; 2D SIMD + VLIW + multichip ✓; bf16 compute/fp32 accumulate + int8 ✓; JAX/PyTorch/TF ✓.

## NVIDIA A100 / T4 (GPUs as DSAs)
- SMs scaled by generation (56 Pascal → 132 Hopper); redundant SMs = yield.
- **Tensor Cores**: Volta 2 TC/subcore doing 4×4×4 matmul/clock (64 FLOP) from register fragments per thread (warp-mapped); A100 4 TC/SM at 4096 bits/clock. NOT systolic (small tiles, combinational).
- Data-type ladder across generations: fp16/bf16/int8 → **tf32** (fp32 exponent + fp16 mantissa) → **fp8** (two flavors: E4M3 forward, E3M2 backward) → **fp4** (Blackwell); Hopper's **Transformer Engine** auto-picks fp8/fp16 per layer by monitoring output statistics.
- **2:4 structured sparsity** (A100): any 2-of-4 zeros → 2× peak on sparse matmul (real gain 1.10–1.18×).
- A100: 7nm, 826mm², 54B transistors, 300W, HBM2E 40GiB @1555GB/s, 12 NVLink → DGX-8 → 4096-chip clusters. T4: 12nm, 70W passive, GDDR6 16GiB @320GB/s, 8 chips max — inference SKU.
- **ECC gotcha**: GDDR6 = in-band ECC (steals bandwidth; optional) vs HBM side-band (free). Google requires ECC → T4 loses 19–26% vs MLPerf claims; also thermal throttling (idle 35°C → 75°C in 30s, clock 1.6→0.9–1.3GHz). TPU v4i unaffected (provisioned cooling + extra ECC memory).
- vs TPU v4 lite in Google DCs: TPU 1.3× (server) / 1.6× (offline) faster than T4.

## Graphcore IPU Bow (the memory bet)
- 1472 cores × 64 fp16 MACs, 6 threads/core, own scalar ISA, **Bulk Synchronous Parallel** (compute → communicate → barrier steps); Exchange unit + 3 links/chip (benchmarked to 256).
- Radical: **897MiB on-chip SRAM** (624KiB/core; 6× TPU v4's SRAM, 22× A100 L2) and **no DRAM at all** — overflow goes to host DDR4. Bet: DNNs fit on-chip.
- Training MLPerf: slower than A100/TPU v4 at scale (256-chip ceiling).

## Samsung NPU (the smartphone class)
- 3 cores (v1) / 2 (v2), each with 1MiB TCM scratchpad (51% of core area), 4×16×16 MAC tensor units, int8 focus (v2 adds fp16/int4, 4096 MACs/engine), **sparsity unit skips zeros** (+1.4× avg), vector unit for activations.
- 5.4mm² die, 0.33–0.79W — two orders of magnitude below datacenter DSAs.
- Beats Core i7 + Iris Xe by 1.2–3.4× on MLPerf Mobile despite 5–25× smaller power/clock budget. v2 modes: always-on (89% power save), low-power, low-latency (cross-core gather unit).

## Cross-cutting
- **SoC integration via IP blocks**: accelerators over PCIe pay the Amdahl data-shipping tax; IP blocks (portable design blocks in Verilog) integrate on-die — Apple SoC: CPU+GPU only ⅓ of area, IP blocks the rest, tripled in 4 years. SOC design = city planning; new IP must offer a small-resource version to get adopted.
- **RISC-V for DSAs**: free/open ISA with 4 reserved custom opcodes × 10-bit function space → thousands of custom instructions without a vendor contract; and DSAs programmed at DAG level care less about ISA compatibility. Third-biggest ISA after ARM/x86.
- **ML energy/carbon — the 4 Ms** (Patterson 2022, up to 100× energy / 1000× emissions): **Model** (NAS finds 4.2× faster equal-quality architectures — cost amortized across reuse), **Machine** (TPU v4 14× vs P100), **Mechanization** (PUE 1.1 vs 1.6), **Map** (clean grid: 6–9× lower CO2e/kWh).

## Fallacies & pitfalls
- **DNNs move fast**: BERT 0→25% of workload in 2 years; LLMs likewise — a DSA must survive its domain's evolution (TPU's compiler-compat + flexible data types are the hedge).
- **IPS is a meaningless summary metric** (TPU v1: 360K IPS on MLP1 vs 4.7K on CNN1 — 75× spread); use MLPerf, no excuses.
- **DSA compilers take years to mature**: most post-2017 ML-chip startups never posted an MLPerf score — the software stack, not the silicon, killed them.
- **Batch size ≠ 1 for low latency**: TPU v4 lite meets 99th-percentile ms latency SLOs with batches in the hundreds.
- **Multitenancy must be designed in** (sharing an accelerator across models/users without interference).
- Benchmark-vs-datacenter gap: ECC + cooling + sustained runs cut vendor MLPerf numbers 20%+ — measure in the real environment.
