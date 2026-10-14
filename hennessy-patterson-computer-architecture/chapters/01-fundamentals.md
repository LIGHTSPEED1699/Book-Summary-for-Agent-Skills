# Ch1 — Fundamentals of Quantitative Design and Analysis (6th ed.)

## The big picture: why specialization
- 1986–2003 "hardware renaissance": 52%/yr performance growth (vs 35%/yr from technology alone). It's over.
- **Dennard scaling ended ~2004** (voltage/current couldn't keep dropping; leakage floor) → industry pivoted from one fast core to many efficient cores (ILP → DLP/TLP).
- **Moore's Law is slowing**: 2022 Apple M2 has 20B transistors vs 106B predicted by the old doubling rate — off by 5×. DRAM: 8Gb 2014 → 16Gb 2019 → 24Gb 2023 (first non-power-of-2); quadrupling now takes 10 years.
- Net: processor performance now doubles ~every 8 years, not 1.5. **Domain-specific architectures are the only remaining path** to big energy-performance-cost gains (Ch7).
- Amdahl caps useful cores: 10% serial → max 10× speedup regardless of core count.

## Five classes of computers (design driver in parens)
- **IoT/embedded**: 1¢–$100, ~30B units/yr; minimum price that meets the need; benchmark data immature (Dhrystone/CoreMark still sadly dominate; Embench is the SPEC-style replacement).
- **PMD (phones/tablets)**: energy+size constraints (battery, fanless, plastic packaging); real-time/soft-real-time media; flash storage; code size matters.
- **Desktop/laptop**: price-performance is the metric; newest and cheapest parts debut here.
- **Servers**: availability (24×7), scalability, **TCO not purchase price** (5–8 yr life; processor ≈ ¼ of TCO), efficient throughput (requests/sec).
- **Clusters/WSC**: tens of thousands of servers as one computer; ~$50M/yr amortized hardware, so 10% price-performance = $5M/yr per warehouse; redundant cheap components + software layer for availability; scalability via LAN, not hardware. Supercomputers differ: FP throughput, batch, low-latency interconnects.

## Parallelism taxonomy
- Application: **DLP** (many data items) and **task-level parallelism**.
- Hardware exploits: **ILP** (compiler+HW, implicit; pipelining/speculation, Ch3), **vector/SIMD/GPU** (one instruction on many data, Ch4), **TLP** (tightly coupled threads, Ch5), **RLP** (loosely coupled requests, Ch6).
- Flynn: SISD (Ch3), SIMD (Ch4), MISD (nobody builds), MIMD (Ch5 tight, Ch6 loose). Real machines are hybrids.

## Architecture = ISA + organization + hardware
- ISA review along 7 dimensions (Appendix A deep): register class (load-store since 1985; x86 is register-memory), byte addressing, alignment (ARM requires, x86/RISC-V don't), addressing modes, operand types (incl. 16-bit FP for AI), operations, control flow (RISC-V branches test registers; x86/ARM test condition codes), encoding (fixed 32-bit ARMv8/RISC-V vs 1–18 byte x86; Thumb-2/RV64IC compact variants).
- **RISC-V is the book's example ISA**: 32 GPR + 32 FP registers, load-store, fixed 32-bit formats (R/I/B/S/U/J), base RV64I + M/F/D extensions; free and open, 200+ member companies, 2B SoCs shipped 2024.
- ARM ships ~30B chips/yr (100× x86). Same ISA, different organization = different machine (EPYC vs Xeon). "Socket" = one CPU whether one die or chiplets.

## Technology trends
- Feature size 10µm (1971) → 7nm/3nm (2022); density scales quadratically with linear shrink, transistor speed only linearly — the architect's opportunity. **Wire delay scales badly** (R·C per length worsens); power now an even bigger obstacle than wires.
- **Bandwidth outpaces latency everywhere**: bandwidth improved 450–80,000× vs latency 5–64× across 40 years; in the last 5 years latency didn't improve at all (disk latency rose with 20TB 7200RPM drives). Design for bandwidth, plan for stuck latency.
- Flash 8–10× cheaper/bit than DRAM; disk 3–5× cheaper than flash, 100–200× cheaper than DRAM; disk density now <5%/yr.

## Power & energy (the central constraint)
- Three numbers: **peak power** (supply sizing), **TDP** (sustained, cooling design; peak ≈ 1.5× TDP), **energy per task** (the right comparison metric: energy = avg power × execution time; a 20% thirstier chip that runs 30% faster wins: 1.2×0.7 = 0.84).
- Dynamic energy per transition = ½CV²; power = energy × frequency. **DVFS example**: 15% voltage cut → energy ×0.72, power ×0.61. Slowing the clock for a fixed task cuts power but NOT energy.
- Static (leakage) power ∝ device count; up to 50% of power in high-end chips (SRAM arrays) → power gating.
- Energy ladder (TSMC 7nm, Jouppi 2021): 8-bit int add = 1000 units; 32-bit FP add = 45,000; 32KB SRAM read = 17,000; 1MB SRAM = 40,000; **DDR4 32-bit read = 187,400,000** — DRAM access ≈ 200,000× an 8-bit add; small SRAM 175× cheaper than DRAM. Caches are everything.
- Dark silicon: too many transistors to power at once. Energy-aware design = narrow ops + local memories → 10–1000× more arithmetic units (the DSA recipe).
- Energy tactics: clock-gating idle units ("do nothing well"), DVFS, design for common case, Turbo (10%→30–80% burst), heterogeneous cores (big.LITTLE), **race-to-halt** (run fast then sleep).
- Carbon: operational CO2e = time × machines × power × CO2e-per-KWh (grid factor varies 5–10× by region: Finland 94% vs Singapore 4% carbon-free); embodied carbon counts manufacturing; higher yield = lower embodied cost per die.

## Cost
- Learning curve (yield doubles → cost halves), volume (≈10% cost cut per doubling), commoditization.
- Chip cost = wafer cost / (dies/wafer × die yield) + test/package. Dies/wafer ≈ πr²/die − πd/diagonal. **Die yield = (1/(1+defects×area))^N** (Bose-Einstein; 2022: defects ≈ 0.012/cm², N=33–35). Cost per die grows ~**square of die area**: 1cm² die ≈ $35, 2.25cm² ≈ $135 on a $16K 5nm wafer. Reticle limit ≈ 8.5cm².
- Masks: $10M (7nm), $20M (5nm) — brutal for <1M volume parts; shuttle runs amortize prototyping.
- **Chiplets** answer both reticle limits and mask economics: AMD EPYC Gen1 = 4×213mm² 14nm → 1.7× cheaper than a monolithic 777mm² die; Rome = 7nm core chiplets + 12nm I/O chiplet (I/O doesn't scale); enables 16–64 core SKUs from one design; 64-core monolithic would exceed reticle. SRAM no longer scales (−20× vs ideal at 3nm) → keep caches off the leading edge where possible.
- WSC economics: TCO = CAPEX + 3–4×OPEX; ~40% of OPEX is power+cooling infrastructure; slowing Moore → stretching IT lifetimes to 6–8 years.

## Dependability
- MTTF (reliability), MTTR (repair), MTBF = MTTF+MTTR; FIT = failures per 10⁹ hours; AFR ≈ 8760/MTBF. Independent exponential failures: **rates add**.
- Disk-subsystem example: 10 disks + controller + PSU + fan + cable → 23,000 FIT → MTTF ≈ 4.7 years.
- Redundant pair: MTTF_pair ≈ MTTF²/(2·MTTF·MTTR) → with 24h repair, a PSU pair is ~4150× more reliable. Redundancy in time or resources.
- **Mercurial cores / silent data corruption** (Google/Meta 2021–22): logic (not memory) produces wrong results undetected, appears late, core-specific, triggered by software changes. Mitigate with result checking, stronger post-manufacturing tests.
- SLA/SLO define "up". Amdahl applies to reliability too: no single-point-of-failure rule.

## Security as an architecture topic
- **Row hammer** (2015): repeated DRAM row writes flip bits in adjacent rows → rewrite page-table protection bits. Hardware security era began.
- **Spectre** (2018) exploits three "innocent" microarchitecture features: instruction speculation (rolls back ISA state but leaves cache breadcrumbs), caches (invisible to ISA, not restored on rollback), hardware multithreading (attacker co-residency). Side channel = cache state. Clouds sell non-shared "dedicated" instances (+5%) as mitigation. Details in Ch2/Ch3.

## Performance measurement
- Response time (execution/wall-clock/CPU time) vs throughput. "X is n× faster" = time ratio; throughput phrasing separate.
- Discredited benchmark styles: kernels, toy programs, synthetics (Dhrystone). Benchmarketing: one compiler+flags for base results; peak allows per-benchmark tuning.
- SPEC CPU2017: 10 int + 17 FP; SPECRatio = ref-time/machine-time; **summarize ratios with the geometric mean** (ratio of GMs = GM of ratios → reference machine irrelevant). SPECrate = throughput (N copies). TPC: transactions/sec with response-time SLO + price mandatory. SPECpower: ssj_ops/watt across 100%→Active Idle (servers rarely run at peak; Google fleet median utilization 10–50%).
- EEMBC failed to kill Dhrystone; CoreMark is another synthetic; Embench (2025) is the open attempt.

## Quantitative principles (the toolkit)
1. **Parallelism** (banks, carry-lookahead, multicores).
2. **Pipelining** (overlap stages).
3. **Prediction** (branches, caches — forgiveness cheaper than permission; also the Spectre door).
4. **Locality** — 90% of time in 10% of code; temporal + spatial.
5. **Redundancy** for dependability.
6. **Focus on the common case** — quantified by Amdahl:
   - Speedup = 1 / ((1 − F_enh) + F_enh / S_enh), F_enh = fraction of ORIGINAL time enhanced (classic pitfall: using post-enhancement fraction).
   - Ceiling = 1/(1−F_enh). Diminishing returns; measure usage before optimizing.
7. **Processor performance equation**: CPU time = IC × CPI × cycle time; each 10% lever worth 10%; CPI = Σ(ICᵢ/IC × CPIᵢ) measured, not from manuals. Interdependencies: cycle time↔technology/organization, CPI↔organization/ISA, IC↔ISA/compiler. DVFS/Turbo muddy measurements — disable for reproducibility.

## Putting it together (6th ed. example)
- Dell R650 (Xeon 8380, 40c/socket) vs R7525 (EPYC 7763, 64c/socket via chiplets): AMD 1.4× price, 1.6× cores; Speed (latency) results within 3–9%, Rate/power (throughput) 1.4–1.6×; **2× ssj_ops/watt** (23,036 vs 11,533). Chiplets + core count win throughput/energy; single-thread parity.

## Fallacies & pitfalls
- All exponential laws slow (Dennard first, then disks, then Moore).
- Node names are marketing: TSMC 7nm metal pitch 40nm vs Intel 10nm 36nm — cross-vendor nm numbers aren't comparable.
- Multiprocessors are not a silver bullet: performance growth is now a **programmer's burden** (make programs parallel).
- Amdahl's heartbreaking law: everyone knows it, everyone forgets to measure first.
- Single point of failure: the fan caps your disk-subsystem reliability no matter how good the PSUs.
- Performance enhancements are NOT energy-neutral: Turbo 1.07× perf cost 1.37× joules (Esmaeilzadeh 2011).
- Benchmarks rot: SPEC89 matrix300 (99% time in one line, 9× compiler win); CINT2006 libquantum 7300× via auto-parallelize+bit-packing; ~70% of old SPEC programs get dropped.
- Disk MTTF marketing: 1.2M-hour MTTF ≠ never fails; real field AFR 2–10%/yr (2–10× worse than rated).
- Peak performance ≠ observed: real codes achieve 5–58% of peak.
- Fault detection without correction lowers availability (Sun L2 parity-only crashed on benign transient errors; scrub + ECC instead).
- Carbon numbers get wildly overstated (Brandolini's law): Netflix 30-min claim 45× too high; "DNN training = 5× car lifetime" was 120,000× too high (actual ≈ 2.6 tonnes for the big paper; tiny for typical models). Four mistakes: ignoring parameter drift, assuming short-term → proportional electricity, long-term projections, extrapolating one slice of IT.
