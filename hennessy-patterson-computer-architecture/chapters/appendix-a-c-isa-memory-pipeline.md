# Appendices A–C — ISA, Memory Optimization, Basic Pipelining

## Appendix A — Instruction Set Architectures
- Review ISA along 7 dimensions: (1) number/length/class of registers (data vs address; RISC = load-store), (2) memory addressing (byte-addressed; alignment rules), (3) addressing modes (immediate, register, displacement, register indirect, indexed, base+offset — the compiler-friendliness axis), (4) operand types (int/FP/decimal/character; width flexibility), (5) operations (data xfer, computation incl. multiply/divide/shift, system control), (6) control flow (branches vs jumps, condition codes vs direct register comparison, procedure call linkage), (7) encoding (fixed vs variable length; opcode size; R-type/I-type/J-type fields).
- **RISC-V as reference**: RV32E (16 regs, embedded) / RV32I / RV64I; extensions M (mul/div), A (atomics LR/SC), F/D (FP + fused FMA), C (compressed 16-bit), V (vector); fixed 32-bit base formats R/I/S/B/U/J; big immediate encodings spread bits across fields to keep decode simple.
- Fallacies: "RISC vs CISC" is dead (x86 is internal RISC + speculation; ARM gained complex instructions); "more addressing modes = faster" — measured wrong (load-store + simple modes + compiler wins); "large register sets help only via spills avoided" — also renaming.

## Appendix B — Memory Hierarchy Optimization (the six basic levers)
1. **Increase hit rate**: bigger blocks (spatial locality, until false sharing/traffic), bigger caches, higher associativity (2–8 way captures most of full-associativity benefit).
2. **Reduce hit penalty**: small fast L1 (separate I/D), pipelined access, way prediction, PIPT vs VIPT tradeoffs.
3. **Increase bandwidth to memory**: multibanking, L2/L3 caches, wider buses, multiple channels, instruction+data parallelism in the memory system.
4. **Use smaller caches** (for the same miss rate): subblock placement (load only the touched subblock), **sector caches** (tag per sector; L1 tags replicated in L2 → L2 hit without L1 miss), nonallocating caches for streaming.
5. **Reduce miss penalty**: read/write buffers (write-back absorbs writes), **critical-word-first + early restart**, nonblocking (overlapped) misses, prefetching.
6. **Reduce frequency of VM misses**: **TLBs** (fully associative, small; multi-level; huge pages), inverted page tables for sparse spaces, OS page-size choice.
- Cache performance math: AMAT chains; three C's decomposition (Appendix B's classic: compulsory/capacity/conflict via trace-driven simulation of infinite + direct-mapped + k-way caches).
- Virtual memory: page tables (multilevel), TLB miss handling (hardware walk vs software trap), protection bits per page, thrashing when working set > physical memory.

## Appendix C — Pipelining Basics (the 5-stage MIPS model)
- Ideal 5 stages: IF, ID/regs, EX, MEM, WB. CPI = 1 + stalls.
- **Structural hazards**: resource conflicts (unified memory → split I/D caches; register file needs 2R+1W ports).
- **Data hazards (RAW)**: load-use needs a bubble without forwarding; **forwarding paths** (EX/MEM→ALU, MEM/WB→ALU, FPU variants) fix all but load-use; **stall vs interlock** detection.
- **Control hazards**: branch penalty; static not-taken; **branch prediction** (predict-taken, 2-bit saturating counters beat 1-bit by avoiding flip-flop pathology); delayed branches (MIPS — compiler fills slots; faded with deep pipelines + good predictors).
- **Exceptions**: precise exceptions require pipeline flush + register-file write ordering discipline (WB before commit of older instructions).
- **Static scheduling** (compiler reorders to fill stalls; loop unrolling + software pipelining) vs **dynamic scheduling**: scoreboard (Tomasulo-era CDC 6600: wait until FU free + no CDB conflict) → **Tomasulo's algorithm** (reservation stations + register renaming + CDB broadcast: eliminates WAR/WAW, allows OOO execution; the conceptual ancestor of every modern OOO core).
- R4000 (MIPS) as the worked in-order 8-stage example.
