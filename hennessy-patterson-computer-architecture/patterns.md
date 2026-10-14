# Cross-chapter patterns & anti-patterns (CAQA 6th ed.)

## Recurring frameworks
1. **The equation-first method**: never argue qualitatively — write AMAT, Amdahl, CPU-time, roofline, TCO, or the queuing response law, plug measured numbers, find the dominant term.
2. **One lever, one cost**: every technique improves exactly one term of one equation and worsens another (Fig 2.17). Bigger blocks ↓miss rate ↑traffic; associativity ↓conflict misses ↑hit time/energy; speculation ↑ILP ↑energy ↑security risk.
3. **Locality is the free lunch; when it breaks, redesign**: caches exploit it for 25 years (memory wall held at bay); streaming/DNN workloads break it → scratchpads, HBM, systolic dataflow, co-design.
4. **Hide, overlap, or shorten**: latency strategies — hide (threads, OOO, prefetch), overlap (pipelines, banks, channels), shorten the path (placement, on-die memory). GPUs pick hide-with-threads; DSAs pick shorten+compiler-overlap; CPUs pick hide-with-speculation.
5. **Prediction beats perfection, forgiveness beats prevention** — branch predictors, memory disambiguation, speculative execution — but every prediction is a security surface (Spectre) and an energy tax (~30% wasted int instructions).
6. **Redundancy buys availability, and it's cheap at scale** — ECC/chipkill, RAID, replicated state, hedged requests, power oversubscription; the failure-rate math (FITs add; MTTF²/2MTTR) is the pricing tool.
7. **Scale changes the physics of the argument** — at 50K servers: 1% = $5M/yr; DRAM FITs 15–25× vendor claims; µs tails dominate UX; power peaks decorrelate; the network is a co-designed organ, not a product you buy.
8. **Compatibility is the strongest force in computing** — x86's contract forced translation; VLIW died on binary compatibility; TPUs chose compiler-compatibility; RISC-V wins by having no contract. Choose your compatibility axis deliberately.
9. **The interface moves the work**: compiler (ILP era) → OS (storage) → framework/DAG (DSA era). Whoever owns the interface owns the optimization.
10. **Measure in the field, not at the booth** — MLPerf vs datacenter (ECC/thermal: −20%), MTTF vs AFR, peak vs sustained, PUE at the right meter.

## Anti-pattern catalog (the fallacies, cross-referenced)
- Exponential thinking: "disk density will save us", "Moore will rescue perf" — every exponential has already slowed (Ch1/2).
- Marketing numbers: nm node names across vendors (Ch1), IPS for DNNs (Ch7), peak FLOPs without roofline (Ch4), MTTF without AFR (Ch1), PUE at the wrong meter (Ch6).
- Benchmark sins: synthetics (Dhrystone/CoreMark), per-benchmark flags, stale suites (libquantum 7300×), speedup-curve comparisons without best-algorithm (Ch5), ignoring 99th percentile (Ch6).
- Amdahl amnesia: optimizing the 20%, claiming "Amdahl broken", wimpy-node fleets, serial fractions in requests (Ch1/5/6).
- Energy illusions: perf gains are never energy-neutral (Turbo 1.37× J), sleep modes useless, turning off idle servers saves ≤7%, carbon claims 100× high without the 4 Ms (Ch1/6/7).
- Memory illusions: cache behavior doesn't transfer across programs; short simulations lie; new memory tech must beat both neighbors (PCM/Xpoint died); bandwidth without locality still fails on GPUs.
- Parallel illusions: linear speedup expected, OS locks serialize (SGI page table), multicore ≠ power savior, communication is the bottleneck (isoefficiency), "just add threads" fails on scattered access (Ch4/5, App I).
- Security illusions: ISA-level isolation isn't enough (Spectre/Meltdown), correct implementations can leak via timing; multitenancy must be designed into accelerators (Ch3/6/7).
- DSA illusions: silicon without a mature compiler is a paperweight (startup graveyard); domains drift (BERT→LLM) — build flexibility into data types and the compiler path (Ch7).

## Design recipes that repeat
- **Sizing outstanding requests**: bandwidth × latency (MSHRs, prefetch depth, TCP windows — same math).
- **Banking/interleaving conflict check**: stride vs bank count, before buying hardware.
- **Two-level anything**: caches/TLBs/predictors/locks/switches — small fast + big slow with a learned selector between them.
- **Learned prediction with periodic reset**: tournament selectors, store sets, hybrid TAGE — adaptivity needs forgetting.
- **Amortize fixed costs over volume**: masks ($20M), WSC buildings, custom silicon ($50–100M dev), NAS model search — the volume threshold decides general-purpose vs custom.
