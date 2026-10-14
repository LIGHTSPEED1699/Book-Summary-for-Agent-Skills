# Ch2 — Memory Hierarchy Design

## Foundations
- Hierarchy works because of **locality** (temporal + spatial) + technology cost/speed ladders: smaller/faster/costlier per byte as you approach the processor. Goal: cost of the cheapest level, speed of the fastest. Inclusion property: lower level is superset of higher (usually).
- AMAT = Hit time + Miss rate × Miss penalty; multilevel: AMAT = HT_L1 + MR_L1 × (HT_L2 + MR_L2 × MP_L2).
- Three C's of misses: **compulsory** (infinite cache still misses), **capacity** (too small), **conflict** (mapping collisions). Conceptual model, not definitive. Multiprocessors add a 4th C: **coherency** misses.
- Miss rate misleads; misses-per-instruction better; AMAT better still; execution time best. Speculation/multithreading shrink *effective* miss penalty.
- i9 12900 demand math: 4 data refs/core/clock × 8 cores × 3GHz ≈ 3840 GiB/s peak demand vs 56 GiB/s DDR5 dual-channel = **2% of demand** — hence 3 cache levels, multiporting, banking.
- Caches can be 25–50% of PMD chip power; 60+ MiB LLC in servers → power matters as much as AMAT.

## Memory technology
- **SRAM** (6T/bit): all cache levels on-chip; L3 access 4–8× L2 but ≥5× faster than DRAM; off-chip DRAM = 50–100× L1 latency, ~100× L1 energy.
- **DRAM**: 1T/bit capacitor; RAS/CAS address multiplexing; row → row buffer (Act/Pre commands); read destroys → rewrite; **refresh** every row within ~64ms (<5% of time budget). Banks inside chips (up to 16 in DDR4) allow overlapped row accesses; row-buffer hits are cheap (column-only access). SDRAM (clocked interface + burst), wider buses, **DDR** (both clock edges). DIMM naming: PC3200 = 200MHz×2×8B. Capacity doublings: 18mo (to 1995) → 26mo → 6yr (2010–16) → next ~2024. DDR4→DDR5: latency flat, bandwidth/power only. LPDDR (mobile), GDDR (graphics, being displaced by HBM).
- **HBM**: DRAM stacks on an interposer in the same package (2.5D): up to 4 stacks × 8 dies, 32+ GiB, ~TB/s-class. 3D stacking today = SRAM L3 on top of die (AMD Genoa: 1GB L3 per 96-core chiplet). Heat/noise limit true 3D DRAM-on-CPU.
- **NAND Flash**: page reads (2–4KiB) ~25µs first byte then 40MiB/s; erase-before-write in blocks (writes ~1500× slower than DRAM, 8–15× faster than disk); nonvolatile, zero standby power; **write endurance** ~100K cycles → **write leveling** in controllers; $0.12–0.20/GiB vs DRAM $5–10, disk $0.02–0.05. Flash replaced disks except bulk archive.
- **PCM/Xpoint** (memristor crosspoint): no erase step, better random writes — shelved commercially (see pitfalls: no clear advantage in both speed AND price).
- **Dependability**: spare rows for fab defects; soft errors (transient) vs hard. Parity (1/8 bits) detects; **ECC** (8/64 bits, SEC-DED) standard in DDR5. **Chipkill/SDDC**: survive whole-chip failure. 10,000-processor × 4GiB server, 3 years: parity → ~90,000 unrecoverable (1/17min); ECC → 3500 (1/7.5h); Chipkill → 1/2months. Chipkill mandatory at WSC scale.

## Ten advanced optimizations (by AMAT lever)
1. **Pipelined L1 + virtual index/physical tag + set associativity**: L1 hit 1→2→4 cycles across Pentium→P4→i9 (higher clock, longer latency, bigger branch penalty). VIPT uses page offset as index → no TLB on critical path; aliasing avoided by associativity ≥ (L1 size/page size) or page coloring. **Way prediction** (>90% accurate 2-way) gets direct-mapped speed with 2–4-way hit rate (R10000, ARM). **Victim cache** (8 entries) helps small direct-mapped L1s; obsolete vs modern associativity+prefetch. CACTI models hit time/energy vs size/associativity (8-way is costly: parallel tag+data reads).
2. **Multiple banks/ports in L1 D-cache**: i7 = 4 banks (2 refs/clock); i9 = 8 banks dual-ported (4 refs/clock). Sequential interleaving (block mod banks). Locality collapses same-block refs; bank-conflict probability math (4 refs, 8 banks, all distinct: no-collision = 8·7·6/8³ ≈ 65%). Dual-port raises access time; banking may not — sometimes dual-ported 2-bank beats quad-ported single bank.
3. **Better replacement**: optimal = Belady MIN (future knowledge). LRU exact too costly; **NRU** (1 bit) ≈ LRU−1%; **2-bit recently-referenced saturating counter** beats LRU by 5% (L2) / 7% (multicore LLC) — distinguishes streaming single-use from reuse. L1: random/NRU; LLC: multibit approximations.
4. **Multibanked L2/L3**: power + latency + refill bandwidth (i9 L2: 8 banks; LLC banks distributed per core).
5. **Nonblocking (lockup-free) caches**: hit-under-miss, miss-under-miss; effective penalty = nonoverlapped stall. ~9% int / 12.5% FP latency reduction for one hit-under-miss; saturates by ~2–64. Needs **MSHRs** (Miss Status Holding Registers: destination, tag, which load/store); misses return out of order (L2 hits vs misses, NUCA). Outstanding-miss sizing: bandwidth × latency (16GiB/s ÷ 64B × 36ns ≈ 9; double for collisions → 18).
6. **Critical word first / early restart**: start processor when the needed word arrives; only pays with large blocks.
7. **Compiler locality optimizations**: **loop interchange** (spatial: walk arrays in storage order), **blocking** (temporal: B×B submatrices; memory words 2N³+N² → 2N³/B+N²; small B also fits registers). Blocking was the SPEC89 matrix300 9× story.
8. **Hardware prefetching**: instruction stream buffers (fetch next consecutive block); data prefetchers — Skylake's four: DCUI, DCUP (L1 stride), L2A (spatial), **L2P streamer = 70% of CPI gain** on memory-heavy SPEC2017; up to 2× on some benchmarks, slightly negative on others; L2 prefetches land in L2 (not L3); bad prefetches evict useful lines + burn bandwidth/power.
9. **Compiler (software) prefetch**: nonfaulting cache prefetch ("semantically invisible"); unroll/software-pipeline to issue ~7+ iterations ahead; worked example: 251 misses → 19 with 400 prefetches, 6.2× faster. Pointer chasing possible (Luk & Mowry: +4–31% on half of pointer-heavy programs).
10. **Multiple memory channels + HBM mixes**: independent channels = bandwidth + fewer stalls; HBM+DDR mix = explicit NUMA (DSL-managed) or **HBM as L4 cache**: tag storage problem → Loh-Hill (tags+data same DRAM row; column access cheap), **alloy cache** (direct-mapped, tag+data burst in one HBM cycle, miss predictor skips tag read on predicted miss) ≈ ideal.

Summary rule: each technique targets one lever (hit time / bandwidth / miss penalty / miss rate) and usually hurts another or adds complexity (0–3 scale in Fig 2.17).

## Virtual memory & protection
- VM = physical memory as cache of secondary storage + **protection**: user/supervisor modes, unwritable mode bit + protection state, system call/return transitions, page-table PTEs (read/write/execute per page; only OS updates).
- **TLB** caches PTEs (tag = virtual bits; data = physical page + protection + valid/used/dirty). Two-level TLBs standard; hardware page-table walkers for misses (i9: 4 parallel walks); huge-page TLBs separate; VMs add shadow page tables → costlier walks (Appendix L).
- **Side-channel attacks on caches** (prime → let victim run → probe): leak branch paths/secrets via shared cache state even with correct VM isolation. Easier across cores sharing LLC; multithreading raises bandwidth ~100×. Mitigations: page randomization, timing obfuscation, cache flush on context switch (costly), **LLC partitioning** (server chips support it). Speculation + multithreading make hardware/software fixes mandatory (→ Ch3 Spectre).

## Cross-cutting
- Autonomous instruction fetch units fetch whole blocks (miss rates no longer per-instruction comparable); translation caches (micro-ops) cut fetch bandwidth + mispredict penalties.
- Speculation generates phantom accesses: exceptions must be deferred; miss rates inflated but total penalty often lower; never compare miss rates across speculative vs in-order machines.
- I/O coherence: prefer DMA to main memory; write-through L1 keeps memory fresh; I/O register pages marked **non-merging write-through** (side-effect registers can't take merged multiword writes); input buffers noncacheable or flushed/invalidated.

## Putting it together (6th ed.)
- **Cortex-A53** (PMD IP core, 2-wide, ≤1.3GHz): 32KiB VIPT L1s (2-way I, 4-way D), 1MiB 16-way L2, 2-level TLB + page map cache; aliasing detected on miss; critical-word-first; SPECint2006 L1D miss 0.5–37.3% (median 2.4%), global L2 0.05–9% (median 0.3%); L2 penalty 9.5× L1 → L2 misses dominate memory-stress benchmarks. IP cores: hard (fixed, faster/smaller) vs soft (retargetable).
- **Core i9 12900** (Alder Lake big.LITTLE: 8 P + 8 E cores; P-core focus): 48b virtual/36b physical; TLBs: L1I 256×4KiB (8-way, 1 cycle), L1D 96 (split load/store), L2 TLB 2048 (16-way, 8 cycles), 4-way hardware walker; caches: 32KiB 8-way L1I (4c), 48KiB 12-way L1D (5c), **1.25MiB 20-way L2 per core (15c)**, 30MiB 15-way hashed-bank shared **noninclusive** L3 (50c); DDR5 dual channel 77GB/s; total L3-miss-to-DRAM ≈ 200 cycles. L1 write miss → write buffer, no allocate. Noninclusive L3 (L2 grew 2–4×) → effective cache = L2+L3 sum; complicates coherence (Ch5). MPKI (not miss rate) is the metric for speculative prefetching machines; mcf = cache buster.
- i9 vs A53 lesson: same hierarchy concepts, opposite budgets (energy vs bandwidth).

## Fallacies & pitfalls
- **Don't extrapolate cache behavior across programs**: same-size cache, data misses 2–90 MPKI; instruction misses 0.0004–55 MPKI (gcc vs lucas).
- **Simulate enough instructions**: locality phases drift; perl's first 1.9B instructions mislead (2.5 → 4.7 → up to 7.9 MPKI across inputs).
- **Caches don't guarantee memory bandwidth** — streamers still need HBM behind the cache.
- **New memory tech must beat both neighbors**: PCM/Xpoint, bubble, CCD, optical all failed; Flash succeeded (nonvolatile + much faster than disk + cost/bit closing).
- Memory wall is back: DRAM latency flat (DDR4→DDR5), SRAM scaling stalled, LLC diminishing returns, streaming/DNN workloads with weak locality → different memory organizations (scratchpads, HBM, near-memory) in GPUs/DSAs.
