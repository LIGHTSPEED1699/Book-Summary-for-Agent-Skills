# Ch4 — Vector Architectures, Multimedia SIMD, and GPUs

## Why SIMD/DLP
- DLP lives in scientific linear algebra + media + ML — all linear algebra. One instruction launches many data ops → energy-efficient vs MIMD; programmer still thinks sequential.
- Three flavors: **vector** (Cray→RV64V; general, easy to compile, needs bandwidth), **multimedia SIMD** (MMX→SSE→AVX/AMX; narrow, no gather-scatter originally), **GPU** (SIMT; graphics ecosystem, its own memory, heterogeneous).

## Vector architecture (RV64V = the model)
- Vector instructions operate on whole variable-length vectors from memory via vector registers; **strip mining** (vsetvl sets VL per tail) handles any length; **masking** (vm bit + mask register) handles conditionals without branches.
- **Convoys**: instructions that can chain together (independent pipelines) execute in one pass; **chime** = start-up + convoy time. Chaining lets load→add→store overlap.
- Performance model: cycles ≈ start-up overhead + n/lanes per convoy. More lanes = more speed but memory must keep up.
- **Memory banks**: conflict if stride s is a multiple of bank count when bank-busy-time ≤ latency; classic example: 8 banks, stride 32 → 5× slowdown. Interleave/bank-aware layout matters.
- **Gather/scatter** (vloxe/vsoxe) for sparse matrices: slow but general; compiler needs programmer assurance of distinct indices.
- Vector >> multimedia SIMD because: variable length, masking, gather-scatter, stride addressing.

## Multimedia SIMD (x86 SSE/AVX)
- Fixed-width registers (128/256/512-bit), same instruction on packed elements; horizontal ops and shuffles awkward; historically **no gather/scatter** (AVX2/AVX-512 added them late) → scattered data gets little benefit.
- Peak requires using them at all: highest FLOPs on x86 come from fused multiply-add in AVX; AMX adds matrix tiles (Golden Cove).

## Roofline model (the evaluation tool)
- Attainable FLOPs/s = min(peak compute, bandwidth × arithmetic intensity). **Ridge point** = peak/bandwidth; kernels left of it are memory-bound — no amount of compute helps.
- Arithmetic intensity counted against **DRAM traffic** (cache blocking raises it).
- GPU vs CPU rooflines: GPU has higher compute roof AND higher bandwidth roof AND lower ridge point → easier to saturate.

## GPU architecture (NVIDIA Pascal as the worked example)
- Programming model: **Thread Block** = body of a vectorized loop (up to 1024 threads); **Grid** = array of blocks; threads get coordinates → each computes its element.
- Hardware mapping: Thread Block Scheduler assigns blocks to **multithreaded SIMD Processors** (SM); each runs **threads of SIMD instructions** (warp = 32-wide SIMD thread); **SIMD Lanes** (16 physical lanes for 32-wide warp → 2-cycle SIMD instruction; "wide but shallow" — vector analogy: 16 lanes, VL 32, chime 2).
- Two scheduler levels: block→processor; SIMD-thread→lanes (scoreboard over up to 64 threads; switch threads to hide variable memory latency — **massive TLP hides latency instead of OOO**).
- Registers: 32K–64K 32-bit regs per SIMD Processor (1024/lane); ≤256 per thread.
- Memory hierarchy: **local (shared) memory** per SIMD Processor (fast, scratchpad, NOT shared across processors despite NVIDIA's name), private memory, L2, graphics DRAM; **Address Coalescing Unit** merges accesses to the same DRAM line; memory controller queues per-bank traffic, opens rows in batches (bandwidth up, latency up — needs many threads).
- **Divergence**: threads in a SIMD thread that branch differently serialize (predication helps short branches).
- Jargon map: SM = multithreaded SIMD Processor; CUDA core = SIMD Lane; shared memory = local memory; SIMT ≈ SIMD with per-thread control.
- PTX intermediate ISA = the reason GPUs can radically change hardware (memory-oriented → register-oriented, 32→64-bit) without breaking software; coprocessor distance = freedom to experiment.

## Loop-level parallelism (compiler side)
- A loop is parallel iff its dependence graph (across iterations) has **no cycle**. Loop-carried dependence ≠ fatal: non-circular ones can be peeled/interchanged (peel first/last iteration, swap statements).
- Dependence analysis: affine indices a·i+b; GCD test (sufficient for absence: GCD(a,c) ∤ (d−b) ⇒ no dependence); general case NP-complete; hierarchy of exact cheap tests in practice. Pointers/nonaffine/cross-procedural = hard (why Fortran persists; why explicit OpenMP/CUDA).
- **Reductions** (dot product): scalar expansion → parallel map + reduce; hardware reduce trees; requires associativity → not IEEE-exact, needs -ffast-math-style opt-in. MapReduce is the same idea at WSC scale (Ch6).
- Induction variables eliminated by unrolling; name dependences removed by renaming.

## Cross-cutting
- **Slow & wide beats fast & narrow for energy**: halve clock + double lanes = same peak, lower V → less energy (why GPUs clock lower). DLP hardware skips OOO/speculation control logic; vector instructions declare their resources → easy clock-gating.
- HBM (stacked DRAM, 4096–5120 wires, same package) is the bandwidth answer.
- Strided accesses can thrash TLBs (one TLB miss per element possible).

## Putting it together
- **Intel Iris Xe** (client): 96 Execution Units (7-way multithreaded SIMD processors, 8-wide FP/int SIMD), 12MB L3, 128B/clock to DRAM.
- **NVIDIA H100** (server): 132 SIMD Processors, 2.0GHz, **HBM3 5120-bit → 3330 GB/s**, 80B transistors, 814mm² 4nm, ~700W.
- **Lee et al. 2010 CPU-vs-GPU kernel study** (the canonical analysis): GTX 280 vs Core i7 — GPU wins where roofline slope/roof explains it (memory-bound kernels 5×; SP compute-bound 3–6×; transcendentals 5.7×; gather-scatter GJK 15.2× via ACU+vector-style addressing); CPU wins where **cache blocking** rescues it (RC, Search, Sort 0.8×) or where **synchronization/atomics + memory consistency** matter (Hist, Solv 0.5×). "100× GPU" is a myth; 2–5× typical.
- Update: Xeon 8180 vs P100 — new GPU 2–5× new CPU; SGEMM 3.9× + CUDA openness → AlexNet 2012 → DNN explosion → NVIDIA market cap 30× Intel by 2024 (not a master plan — an enabler's payoff).

## Fallacies & pitfalls
- "GPUs are just coprocessors (bad)": distance enabled PTX and architectural experimentation.
- Ignoring **vector start-up overhead** (STAR-100/CYBER 205: break-even vector length >100).
- Boosting vector peak while scalar stays slow → harmonic-mean loss (Stardent-1500 vs MIPS M/120-5 on Livermore kernels: 2.5× max-rate win, worse overall). Same trap today: more lanes, unchanged scalar.
- "Vector performance without memory bandwidth": DAXPY is 1.5 refs/FLOP; Cray-1 Linpack doubled via blocking (fewer DRAM refs).
- "Just add more threads on GPUs": only works if threads' accesses are coalesced/local; scattered accesses eventually defeat any thread count.
- SIMD extensions without gather-scatter mislead peak-FLOP marketing (6/14 kernels needed it).
