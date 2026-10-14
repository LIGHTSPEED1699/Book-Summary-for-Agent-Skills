---
name: hennessy-patterson-computer-architecture
description: Apply Hennessy & Patterson's Computer Architecture A Quantitative Approach (6th ed., Kozyrakis et al.) frameworks - quantitative design analysis, Amdahl's law, the memory hierarchy AMAT toolkit, ILP vs TLP vs DLP vs DSA, cache coherence and consistency models, WSC economics (TCO/PUE/tail latency), the DSA eight pillars and five guidelines, roofline analysis - when designing, evaluating, or debugging processors, memory systems, multicore, GPUs, accelerators, or datacenter infrastructure, or when making perf/$/perf/W tradeoff decisions.
---

# Computer Architecture: A Quantitative Approach (6th ed.) — Skill

The quantitative method: measure, use the common case, apply Amdahl's law, exploit parallelism, account for the whole system (perf, price, power, carbon, dependability). Every design decision is a number.

## The five laws this book lives by
1. **Amdahl's law**: Speedup = 1/((1−F)+F/S); ceiling 1/(1−F). Applies to performance, reliability (no single point of failure), and core scaling (99.75% parallel for 80× on 100 cores). Measure F before spending on S.
2. **The performance equation**: CPU time = Instruction Count × CPI × Cycle Time. Every lever (ISA, organization, technology) hits one factor; improvements interact.
3. **Locality + the 90/10 rule**: 90% of time in 10% of code/data; caches work because of it; streaming/DNN workloads break it → different memory organizations.
4. **Energy = power × time; race to idle**: energy per task is the right metric; DVFS, narrow data types, dedicated memories; DRAM access ≈ 200,000× an 8-bit add (TSMC 7nm ladder).
5. **Post-Dennard, post-Moore-slowdown**: no free lunch from transistors — performance now comes from parallelism (ILP→TLP→DLP) and above all **domain-specific architectures** (10–1000× ops per instruction).

## Decision index — which chapter file to load
| Problem | Load |
|---|---|
| Is my optimization worth it? Benchmarks, GM, speedup claims, perf/$ | `chapters/01-fundamentals.md` |
| Cache/TLB/DRAM/flash design, miss rates, prefetch, ECC, memory wall | `chapters/02-memory-hierarchy.md` |
| Superscalar/OOO, branch prediction, speculation, Spectre-class attacks, why ILP died | `chapters/03-pipelining-ilp.md` |
| Vector/SIMD/GPU, roofline, bank conflicts, GPU programming model, CPU-vs-GPU 2–5× | `chapters/04-vector-simd-gpu.md` |
| Multicore: MESI/MOESI, directories, false sharing, locks, TSO/release consistency, SMT | `chapters/05-multiprocessors.md` |
| Datacenter: virtualization/EPT, Clos/oversub, RAID, TCO $/W, PUE, tail latency, Graviton/Nitro | `chapters/06-warehouse-scale.md` |
| Accelerators: TPU/A100/IPU/NPU, systolic arrays, bf16/fp8/fp4, MLPerf, DNN energy 4 Ms | `chapters/07-domain-specific.md` |
| ISA design/review (RISC-V), basic cache levers, 5-stage pipeline/Tomasulo | `chapters/appendix-a-c-isa-memory-pipeline.md` |
| Disks/RAID/queuing theory, embedded SoC, network topology/routing/deadlock, IEEE 754, ISA surveys | `chapters/appendix-d-m-storage-networks-arithmetic.md` |
| Terms, formulas, units (FIT, AMAT, PUE, MPKI, ridge point…) | `glossary.md` |
| Recurring frameworks & anti-patterns across chapters | `patterns.md` |
| Quick reference: formulas, numbers, protocol tables | `cheatsheet.md` |

## The core mental models (use constantly)
- **AMAT = Hit + MissRate × Penalty** — every memory technique attacks exactly one term; check what it worsens (Fig 2.17 discipline).
- **Roofline**: performance = min(peak compute, bandwidth × arithmetic intensity). Know which side of the ridge point you're on before optimizing compute.
- **Dependence taxonomy**: RAW (fundamental) / name (rename away) / memory (disambiguate) / control (predict) / resource (provision). A program property only hurts if the hardware doesn't already defeat it.
- **Coherence ≠ consistency**: coherence = same-location values; consistency = cross-location ordering (SC → TSO → release). Data-race-free is the contract that lets hardware relax.
- **Latency vs bandwidth vs occupancy**: hide latency (multithreading, OOO, prefetch), buy bandwidth (banks, channels, HBM), or shorten the path (locality, placement). GPUs = massive TLP for latency; CPUs = speculation; DSAs = compiler-scheduled movement.
- **Perf/W/$ at scale**: $2/W-year budget; TCO = CAPEX + 3–4×OPEX; 99th-percentile latency is the product; oversubscribe power 40%, network 3:1; utilization 10–50% is normal.
- **DSA audit**: eight pillars (interconnect, memory, ALUs, programming model, data types, parallelism, compiler, cost) + five guidelines (dedicated memories; reinvest saved control logic in ALUs/memory; simplest parallelism; smallest data types; domain language).
- **Fallacy reflex**: every exponential slows; node names are marketing; speedup plots lie; peak ≠ observed; benchmarks rot; MTTF ≠ never; "100× GPU" is a myth; cloud is profitable; wimpy nodes cost latency; PUE is gamed; DNN carbon claims run 100× high.

## How to apply
When evaluating any architecture question: (1) write the equation (AMAT/Amdahl/perf-equation/roofline/TCO), (2) get real numbers (MLPerf/SPEC/field data, never vendor peak), (3) identify which term dominates, (4) attack that term with the chapter's toolkit, (5) check the chapter's fallacies for the trap you're about to step in, (6) price it ($/W-year, TCO) and carbon it (grid factor).
