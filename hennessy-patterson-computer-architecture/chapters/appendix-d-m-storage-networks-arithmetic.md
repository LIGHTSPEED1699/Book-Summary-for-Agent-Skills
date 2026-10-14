# Appendices D–M — Storage, Embedded, Networks, Vector Depth, Parallel SW, Arithmetic, ISA Survey

## Appendix D — Storage Systems and I/O
- Disk areal density history: 29%/yr → 60% → 100% (1997–2003) → ~30%/yr; every "disk is doomed" challenge failed because challengers arrive after DRAM/disk already improved (the recurring memory-technology fallacy).
- Disk performance: seek + rotational latency + transfer; **disk scheduling** (SCAN elevator), multiple platters/zones (ZBR), prefetch, disk arrays.
- **RAID levels**: 0 (striping, bandwidth only), 1 (mirroring), 2 (Hamming — dead), 4 (dedicated parity), **5 (distributed parity: small-write cost 2 reads + 2 writes = 4× I/O; rebuild from any surviving disks)**, 6 (double parity for big drives), 0+1 vs 1+0 (mirrored pairs striped: better MTTF under double failure). Small-write penalty math and rebuild-time exposure (MTTF of array during rebuild = the reason for hot spares + scrubbing) are the core quantitative results.
- I/O measures: bandwidth, IOPS, response time; **SPEC SFS / file-server benchmarks**; OS bypass (raw I/O, DMA, async I/O).
- **Queuing theory (the must-know toolkit)**: utilization U = arrival rate × service time; response time R = S/(1−U) (M/M/1) → **response explodes as U→1** (10× at U=0.9); arrival rate law; utilization law (device U = throughput × service demand); response time law R = U × S/(1−U). Design rule: keep I/O device utilization well below 1 or buy another device; the same curve explains WSC power/latency cliffs.
- Case study: Internet Archive cluster — balance disk bandwidth vs capacity vs network; the OS decides what hardware features get used (OS is the "compiler" of storage).

## Appendix E — Embedded Systems
- Embedded = 99% of processors by volume; design axis = **cost + power + real-time**, not peak performance; software is burned-in ROM, optimized for size (code size = money).
- Benchmarks: EEMBC kernels/CoreMark (see Ch1 fallacy); power measurement per task.
- Multiprocessors in embedded: heterogeneous cores (control + DSP + media); **Sony PS2 Emotion Engine** (superscalar + 2 VLIW vector units + 128-bit SIMD), **digital camera DSP pipeline**, **cell phone baseband + application SoC** — early previews of the heterogeneous SoC era (Ch7).

## Appendix F — Interconnection Networks
- Metrics: **latency (hop count × per-hop), bandwidth (link + bisection), jitter**; switch types: crossbar (O(N²) crosspoints), multistage MIN (Omega: N log N, blocking risk), shared media (bus: cheap, scales poorly).
- Topologies: star/tree, **2D/3D mesh** (simple, scalable, diameter grows; torus folds edges), **hypercube** (log N hops, wiring explodes), **fat tree / Clos** (bisection = full at cost; the WSC answer, Ch6), dragonfly/torus variants.
- Routing: **deterministic order routing (DOR)** = deadlock-free by dimension order; adaptive routing needs turn restrictions (west-first/north-last: break cycles but keep connectivity); wormhole flow control (stalls block whole paths → deadlock risk) vs store-and-forward vs cut-through; virtual channels break resource cycles.
- Switch microarchitecture: input-queued (head-of-line blocking ~29.3% throughput loss at 100% load — the classic result), output-queued (perfect but needs speedup), **combined input-output with VOQ + iSLIP-style scheduling**; crossbar scheduling = bipartite matching.
- SAN (memory-side, cache-coherent, µs) vs LAN/WAN (message-passing, ms); internetworking (routers, fragmentation, QoS).

## Appendix G — Vector Processors in More Depth
- Chaining details: start-up + n/lanes model; **convoy analysis** of loops (which instructions chain); conditional code via mask registers (compress/expand); stride and index vector memory systems (conflict math as in Ch4).
- Sparse matrix handling: gather/scatter + programmer assertions of distinct indices.
- Historical machines: Illiac-IV, CDC Star, TI ASC (memory-to-memory vectors); **Cray X1** as the modern hybrid (CMOS vector + conventional cores).

## Appendix I — Parallel Programming & Scientific Applications
- **Interprocessor communication is the critical performance issue**: communication time per step vs computation; **isoefficiency** — problem size must grow with processor count to hide communication (weak vs strong scaling, foreshadows Ch5 fallacies).
- Scientific app characteristics: regular meshes, nearest-neighbor communication, synchronous phases (bulk-synchronous flavor); synchronization scaling (barriers cost log P with tree/hierarchical barriers; contention).
- Coherence implementation costs at scale; **Blue Gene/L custom-cluster philosophy**: slow clocks + massive concurrency + hardware support for collective communication (the energy-efficiency argument a decade early).

## Appendix J — Arithmetic (integers and IEEE 754)
- Integer: add (carry ripple → carry lookahead), overflow detection (xor of carry-in/carry-out at MSB), multiply (shift-add, Wallace tree/Booth), divide (restoring/nonrestoring, SRT), **shift-left-1 = multiply, shift-right = divide** with sign caveats.
- **IEEE 754**: sign/exponent/biased, hidden leading 1; formats half/binary32/binary64/binary128; **special values**: ±0, ±∞, quiet/signaling NaN; **denormals** fill the gap below min normal (gradual underflow); **round-to-nearest-even default** + 3 directed modes; exceptions set flags and continue by default (no trap culture).
- FP add: align exponents (right-shift smaller), add, normalize, round — **guard/round/sticky bits** decide correctness (Pentium FDIV & the classic 0.1+0.2 story); FP mul: multiply significands, add exponents, normalize/round; **fused FMA** = one rounding instead of two (accuracy + speed).
- Division/remainder: Newton-Raphson + SRT digit recurrence; IEEE remainder (round-to-nearest quotient) via remainder-step instructions.
- Speeding up integer: carry-save, carry-lookahead, carry-select; multiply via Wallace/Dadda trees; the "hardware is only as accurate as its adder pipeline" theme.

## Appendix K — Instruction Set Architecture Survey
- Ten ISAs surveyed against RISC-V: **ARM** (Thumb-2 16/32-bit mixed, condition codes legacy, dominant PMD/embedded), **MIPS** (microMIPS), **Power/PowerPC** (AltiVec SIMD, server lineage), **SPARC** (register windows — why they failed: window overflow traps), **HP PA**, **Intel 80x86** (register-memory, variable 1–15 byte instructions, segmentation legacy, x87 stack of 8 FP registers, internal RISC translation), **VAX** (the CISC apex: 16 addressing modes, orthogonal but slow — why RISC killed it), **IBM 360/370** (the compatibility contract: GPR pairs, byte-addressing, EBCDIC legacy, still alive in mainframes).
- Lesson: compatibility contracts are the strongest force in ISA evolution; clean ISAs win only when the ecosystem can move (RISC-V's opening).

## Appendix M — Historical Perspectives
- Per-chapter history + references: M.2 early computers (Ch1), M.3 caches/VM (Ch2), M.4 ISAs (A/J/K), M.5 pipelining/ILP (Ch3/C/H), M.6 vector/SIMD/GPU (Ch4), M.7 multiprocessors (Ch5/F/G/I), M.8 clusters (Ch6), M.9 I/O (D). Use when tracing an idea's origin or hunting primary sources.
