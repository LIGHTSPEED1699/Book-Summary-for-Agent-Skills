# Ch5 — Parallel Processors: Multicores, Coherence, Consistency

## Scope & economics
- TLP via MIMD: multicores (8–1024 cores, shared address space) up to DSM/NUMA boxes; clusters/WSC (Ch6) are loosely coupled by contrast.
- Two hurdles, both Amdahl-shaped: (1) limited parallelism — 80× on 100 cores needs 99.75% parallel; (2) communication latency — 0.2% remote refs at 200ns turns CPI 0.5 → 2.6 (**5.2× slower**). Attack #1 in software/algorithms; #2 with caching, placement, multithreading, prefetch.
- UMA (bus, dead beyond a few cores) → shared sliced LLC + on-chip network (NUCA even when UMA); NUMA/DSM across chips.

## Coherence (what values reads see)
- 3 properties: uniprocessor read coherency; multiprocessor read coherency; **write serialization** (all processors see writes to the same location in the same order).
- **Coherence ≠ consistency**: coherence = same-location behavior; consistency = ordering across different locations.
- **Write-invalidate** dominates (write-broadcast burns bandwidth). Coherent caches give migration + replication = the performance win.
- Snooping (broadcast; every cache watches every transaction) vs directory (state tracked at home node; point-to-point messages). Modern = **hybrid**: snooping within a chip/LLC domain, directory across chips.
- Protocols: MSI → **MESI** (Exclusive clean state; CXL uses it) → MESIF (Intel: F picks the responder) → **MOESI** (Owned: dirty but shared without writeback; AMD).
- Implementation requires **atomicity + serializability** of coherence events: bus arbitration gave it free; on networks, add **transient states** (restart interrupted transactions) and acknowledgments (know when invalidates complete before write proceeds).
- Snoop bandwidth math: 16 cores, 15-cycle L2, CPI 0.5, 40% ld/st → coherence traffic ≤50% of L2 bandwidth needs **CMR ≤ 0.26%** — real apps exceed 1% → scale via duplicated tags, banked inclusive LLC snooping (Power), or directories.
- Directory: per-block state (Uncached/Shared/Modified) + Sharers bit vector at home node; messages: read/write miss → home; fetch/fetch-invalidate → owner; data reply/writeback; **acks** for invalidates. Optimizations: direct owner→requester forwarding. Inclusive LLC = free directory (bit vector in LLC tags; i7); noninclusive needs separate directory (Xeon) or duplicated L2 tags (EPYC).

## Miss taxonomy at scale
- Uniprocessor 3 C's + **coherence misses**: true sharing (real communication) vs **false sharing** (invalidated because a neighbor word in the block was written).
- OLTP case (Alpha 21164): growing L3 kills capacity/conflict misses but **true sharing is cache-size-insensitive** → gains stop at 2MiB/proc; growing cores raises true sharing; growing block size halves true sharing, cuts compulsory, barely touches conflict (poor spatial locality in DB code), doubles false sharing; 64–128B blocks pay off with fast DRAM.
- Web-search workload (Xeon E7): request-level parallel, little sharing → **capacity misses dominate**; block-size tuning: L1I and L3 benefit most, L1D sweet spot ~64B; traffic growth must be weighed.

## Synchronization
- Hardware primitives: atomic exchange / test-and-set / fetch-and-increment; **RISC-V load-reserved/store-conditional** (reservation register; sc fails on any write to the line or after exceptions/context switch; keep the LR/SC window tiny and memory-free).
- Spin locks: naive swap-spin floods the interconnect with write misses; **test-and-test-and-set** (read-spin locally, then race with swap) exploits coherence; LR/SC's separate load makes spinning free of bus traffic. Lock locality: last unlocker often relocks (cache-resident lock).

## Memory consistency models
- Sequential consistency = program order per processor + interleaving. Cost: write miss stalls until all invalidates ack (60+40+80 = 180 cycles vs 60 to ownership).
- **Data-race-free (synchronized) programs** are the contract: if every cross-processor access pair is ordered by synchronization, relaxed hardware still behaves SC.
- Ladder: SC → **TSO/processor consistency** (relax W/R only; x86) → PSO (relax W/R + W/W) → **release consistency** (RISC-V, ARMv8, C/C++ standards: only acquire/release boundaries impose order; FENCE for explicit ordering).
- **Speculation can hide SC latency** (Hill's argument): reorder freely, detect invalidations to uncommitted loads, rollback — only truly racy programs trigger restarts (R10000 did SC this way).

## Cross-cutting
- Consistency model also gates **compiler** reordering of shared accesses.
- **Inclusion**: inclusive LLC simplifies directories/snooping filters; different block sizes break inclusion silently (worked example); modern trend: Intel/AMD dropped L3 inclusion (L2 and L3 hold different data → effective capacity up; coherence bookkeeping up).
- SMT on multicores: Power8's 8 threads beat Xeon E7's 2 on the search workload (1.5× vs 1.2×); wide-issue + many FUs is what makes big SMT pay.

## Putting it together (2020–23 servers)
- **IBM Power10**: 15 cores/chip, 8MiB L3 slice per core (16 rings), up to 16 memory channels; 2-chip modules, up to 16 chips (240 cores) fully connected in ≤2 hops. Best SPECintRate scaling: **97% efficiency at 220 cores**; 210-core Power10 ≈ 1.3× throughput of 240-core Xeon (70–80% from cores, 20–30% from scaling).
- **Intel Xeon Platinum**: up to 40–56 cores, dual rings, 60MiB distributed L3, 8 channels, UPI links for 8-socket (448-core) meshes; ~70% scaling efficiency at 240 cores; SPEComp (OpenMP, real sharing): linear to 72 cores → ~50% efficiency at 220.
- **AMD EPYC Milan**: 8 cores/chiplet, 32-core CCX ring + 8-bank L3, Infinity Fabric full-connect across chiplets/sockets; 66% efficiency at 128 cores.
- SPECpower on Xeon: throughput scales ~perfectly 28→224 cores (workload scales with machine — beware); energy efficiency best at high load (≤30% load = <65% of full-load efficiency).

## Fallacies & pitfalls
- **Speedup curves lie**: compare best-algorithm-on-each ("true speedup"), not identical code; superlinear usually = aggregate cache effect; weak scaling (grow data with cores) ≠ strong scaling; never conclude relative machine performance from relative speedup plots.
- "Amdahl broken by 1000 processors": that was scaled speedup with constant serial time — law intact.
- "Linear speedup needed for cost-effectiveness": memory/I/O/box costs don't scale linearly with cores → sublinear speedup can still improve perf/$ (IBM p5: 8–32 cores beat 4-core perf/$ on SPEC despite sublinear speedup).
- **Uniprocessor-era software serializes multiprocessors**: SGI single page-table lock killed parallel init even for non-sharing processes; OS data structures need partitioned locks. Parallel software lags hardware — the recurring theme.
- Multicore ≠ power salvation: 96-core machine where only ~55 cores average usable (Amdahl mix) < 2× over 24 cores; clock gains matched 4× core gains. Power caps clock (40-core Xeon 2.3GHz/270W vs 8-core 3.2GHz/140W).
- **The answer is heterogeneity**: Apple M1 (4P+4E cores + 8-core GPU + 16-core neural engine 10–15× inference + media/encryption engines); Intel P/E cores (P 1.5–2× faster, 1.3–1.7× power); turbo via core shutdown; accelerators carry the domain load.
