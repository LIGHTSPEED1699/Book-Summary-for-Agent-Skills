# Ch3 — Pipelining: Advanced ILP, Superscalar, Speculation

## The CPI budget equation
Pipeline CPI = Ideal CPI + structural stalls + data-hazard stalls + control stalls. Every technique attacks one term. Two separable ILP strategies: **dynamic/hardware** (OOO superscalar — dominates everywhere) vs **static/compiler** (VLIW/EPIC — survived only in DSPs and domain-specific code).

## Dependence taxonomy (what limits ILP)
- **RAW** (true dependence): fundamental; can't remove, only hide (forwarding, scheduling, speculation). Loop-carried RAW chains set the floor (pointer-chasing loops are the worst case).
- **WAR/WAW** (name dependences): artifacts of finite register sets; **register renaming eliminates them entirely**.
- **Memory dependences** (load/store through addresses): addresses unknown until AGU runs → **speculative memory disambiguation** (learn which load PCs depend on which store PCs; store sets).
- **Control dependences**: branches; **prediction + speculation** converts them to mispredict penalties.
- **Resource dependences**: structural hazards (ports, functional units) + naming hazards (BTB, predictor aliasing).
- Mapping rule: a program property limits performance only if the hardware doesn't already defeat it (e.g., WAR stalls vanish in renaming machines; don't cite them).

## Superscalar OOO architecture (the modern pipeline)
Three parts, all multi-instruction per cycle:
1. **Front end** (in-order, speculative): fetch/decode N/cycle, branch prediction drives PC, rename, allocate ROB entry + physical registers. Decoupled fetch unit with its own prefetch/buffering is standard.
2. **Execution engine** (OOO, speculative): scheduler (centralized "instruction window" — Intel; distributed reservation stations — AMD hybrid: 4 int + 2 FP schedulers) does wakeup (broadcast match) + dispatch (oldest-ready-first). Wider dispatch than issue/commit absorbs post-miss bursts.
3. **Back end** (in-order): **ROB** commits in program order → precise exceptions + speculation recovery. Mispredict/exception at ROB head → flush younger, restore renaming map (or checkpoint), resume at correct PC.
- Physical register lifecycle: free → used-not-ready → used-ready → architectural; freed at commit of overwriter. Implementations: URF + renaming map + architectural map (fast recovery via bulk copy); or ARF+RRF copy at commit; or rename registers in ROB; or renaming table in ROB (associative search).
- **Issue is the scaling wall**: dependence checks within a bundle grow as O(N²) → issue width stuck at 4–8 for 20 years.
- Recovery speed matters: Golden Cove's **branch order buffer** checkpoints renaming state at branches → recover at detection, not at ROB head; older instructions keep executing.

## Branch prediction (the accuracy gate)
- (m,n) correlating predictors: index by PC ⊕/concat global history; **gshare** = XOR hash baseline.
- **Tournament**: per-branch 2-bit selector between local and global predictors (global chosen ~40% of time for int, <15% for FP).
- Two-level local (history register → pattern counter table) nails low-iteration loops.
- **Tagged hybrid (TAGE)**: multiple history lengths, each table tagged (4–8 bits) to kill aliasing; use longest matching history; P(0) fallback; winners of branch-prediction championships; ~⅓ fewer mispredicts than gshare at equal bits; subsumes loop predictors.
- **BTB** predicts targets (only taken branches stored); branch folding stores target instructions; multilevel BTBs. **RAS** for returns (>15% of branches; stack of 8–16 ≈ perfect). Indirect predictors for jumps.
- Intel evolution: i7-920 (2008) two-level [2-bit + global + loop-exit tournament] → i7-6700 (2016) tagged-hybrid-style; 1.3× fewer mispredicts.
- Misprediction penalty ~15 cycles in deep pipelines; predictor state updates for speculative branches (early update + undo, or dual RASs).

## Memory disambiguation details
- **Load bypassing**: load may pass older stores once all their addresses are computed and differ (store-buffer comparators).
- **Store forwarding**: dependent load takes data from pending store's register (critical for x86 spill/restore patterns; Golden Cove forwards partial overlaps).
- **Speculative disambiguation**: naive speculation is a disaster; **store sets** (SSIT indexed by PC bits → set ID; LFST = last fetched store per set): loads in a tracked set wait for the pending store's address; periodic reset to relearn.
- Value prediction: never panned out commercially.

## Multithreading for single-core throughput
- **Fine-grained** (switch every cycle, round-robin; Sun T-series, GPUs): hides short+long stalls, hurts single-thread latency.
- **Coarse-grained** (switch on costly stalls only): no commercial users.
- **SMT** (fine-grained on an OOO core): rename tables + PCs per thread; issue from one thread/cycle, execution interleaved. Resource policy: static partition (fairness) vs dynamic sharing (utilization); fetch from thread with fewest in-flight instructions balances both.
- Measured (i7 920, Esmaeilzadeh 2011): speedup harmonic mean 1.28 (Java) / 1.31 (PARSEC); energy efficiency 1.0–1.07 — SMT is one of the rare performance gains that also saves energy. Golden Cove SMT: +27% geomean single-core, +16% at 224 threads (memory contention erodes it); biggest wins on underutilizing benchmarks (mcf +46%).

## Speculation's costs
- ~30% of integer instructions executed are mispeculated (vs small for FP) → speculation is often energy-negative for integer code post-Dennard.
- Only speculate through cheap events (cache miss); defer expensive ones (TLB miss) until non-speculative.
- Speculative loads to invalid addresses are safe functionally (exceptions deferred) but **are the security hole** (below).

## VLIW/EPIC (the failed rival)
- Fixed packets, compiler-scheduled; unrolling + local scheduling gets great rates on structured FP (7 results/9 cycles vs 1.29 vs superscalar's ~2), but: code bloat, lockstep stalls, **binary incompatibility across implementations** (fatal logistically). IA-64/EPIC dead (canceled 2020); VLIW lives in DSPs and inside DSAs (Ch7).
- Five-way taxonomy: static superscalar (A53, 2-issue in-order), dynamic superscalar no-speculation (none), dynamic+speculative superscalar (Xeon/EPYC/Apple M/big ARM), VLIW (TI C6x), EPIC (Itanium).

## Limits of ILP (why multicore happened)
1. Complexity ∝ issue-width²; power hungry.
2. Branch prediction accuracy gates everything.
3. Long cache misses block the ROB head (Karkhanis-Smith: it's ROB blockage, not the dependent-instruction window, that hurts).
4. **Wall's ILP ceiling**: even a perfect 64-issue machine with perfect disambiguation and 1-cycle latencies extracts only modest ILP from conventional integer code. ILP is exhausted; TLP/DLP/DSA took over.

## Microarchitecture side-channel (transient execution) attacks — 6th ed. centerpiece
- Attack template = prime → **exploit speculation to run secret-reading code that never commits** → probe. Meltdown pseudocode: flush user array; trigger exception; speculatively load kernel byte; index user_array[bit×256]; probe which line is cached → bit leaks.
- Spectre variant: make the *victim's own code* speculate on attacker-chosen inputs (bounds-check bypass via branch misprediction).
- **SMT makes it worse**: co-residency + shared L1/BTB = high-bandwidth channels, fast probing.
- Defenses: compiler fences / speculative load hardening; SMT off; cache partitioning; pipeline changes to undo speculative cache effects. No complete defense exists. ISA specs are timing-abstract → correct implementations can still be vulnerable; formal timing-security models are an open research area.

## Putting it together
- **Cortex-A53**: dual-issue **in-order static** superscalar, 8-stage integer pipeline; 4-level fetch prediction (1-entry target cache → 3072-entry hybrid → 256-entry indirect → 8-deep RAS); 8-cycle mispredict penalty; scoreboard issue; ~1/200 the power of an i7 quad. Stalls: functional/data/control + cache/TLB misses; cache misses dominate worst programs.
- **Intel Golden Cove** (2021 p-core): 32B fetch → 6 decoders → 144-µop queue; **4K-µop cache** (8 µops/cycle) + loop stream detector; rename 6/cycle; **ROB 512**; 97-entry ALU scheduler (5 int + 3 FP/vector ports); 70-entry load sched (3 AGUs, 3×32B loads or 2×64B/cycle), 38-entry store sched (2 stores); load buffer 192, store buffer 114; retire 8/cycle; 128-entry branch order buffer with renaming checkpoints; AVX-512 + **AMX matrix engine** (8 2D registers, 2K Int8 ops/cycle); 48KiB 12-way L1D 5c, 1.25–2MiB L2 15c, 48 outstanding L2 misses; 2-way SMT; up to 5.5GHz.
- Skylake→Sunny Cove→Golden Cove: ROB 256→352→512, issue 4→5→6, retire 4→4→8 — the steady evolutionary grind.
- SPECint2017 CPI 0.32–0.89; mcf/leela (pointer chasing, data-dependent branches) are the mispredict/cache-miss disasters; gcc L3 MPKI 2.8 → 20.2 at 224 threads (multicore memory contention).

## Fallacies & pitfalls
- Same ISA + same technology ≠ predictable performance/energy: i7-920 vs Atom-230 (both 45nm x86): i7 4–10× faster but **Atom 1.5–2× more energy-efficient**. Aggressive OOO buys speed with energy.
- Lower CPI ≠ faster; higher clock ≠ faster — product matters (Pentium 4's 20+ stage pipeline failed both ways).
- **Bigger and dumber is better**: P4's ILP ambition lost to i7's 8–9MiB L3 — hiding misses with caches beat hiding them with more ILP.
- **Smarter is better than bigger and dumber**: TAGE beats gshare at equal bits despite spending bits on tags.
- Believing "more techniques will find more ILP": Wall 1993 upper bound — conventional programs just don't have it.
- ILP techniques are invisible to programmers; multicore made performance a programmer's problem — that pivot defines the modern era.
