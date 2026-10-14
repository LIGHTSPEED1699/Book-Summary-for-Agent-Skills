# Ch6 — Warehouse-Scale Computers (WSCs) & Cloud

## The WSC as a computer
- 50–100K servers co-designed end-to-end (HW, SW, network, power, cooling); the modern descendant of the supercomputer (Cray as godfather). Metrics: cost-performance, energy efficiency, "four nines" availability, scalability.
- Utilization reality: user-facing clusters average 10–50%; batch clusters 50–85%. Servers rarely peak → energy proportionality matters more than peak perf.

## Virtualization (the cloud's substrate)
- Popek-Goldberg: virtualizable iff sensitive instructions ⊆ privileged. x86 violated it (17 sensitive-but-unprivileged instructions) → VMware's dynamic binary translation vs Xen's paravirtualization (~1% of Linux x86 code changed; Dom0 back-end drivers; driver domains for isolation).
- **VT-x**: root/nonroot modes (no ring compression), VMCS state container, vmlaunch/vmresume/vmexit/vmcall. RISC-V H extension (orthogonal HS mode); ARM EL2 (plus EL3 TrustZone).
- **Memory virtualization**: HPM/GPM/GVM三层. Shadow page tables (pre-2006, hardest part of a hypervisor) → **EPT/NPT hardware 2D page walks**: TLB miss costs 24 memory accesses instead of 4 (**6× walk cost**) → huge pressure for TLB coverage, large pages, page-walk caches. Worked AMAT math: 0.2% L2-TLB miss × 4×50cyc = +0.4 cycles; virtualized needs miss rate ≤0.033% or walk ≤33cyc/access to break even.
- **I/O virtualization**: hypervisor interposition (enables live migration + device emulation + policy) vs direct assignment: **SR-IOV** (PF + VFs) + **IOMMU** (DMA remapping with its own TLB — must keep up with 400M pkt/s; interrupt remapping + **posted interrupts** = exitless delivery).
- **Confidential computing**: SGX-style enclaves (encrypted-at-rest code+data, decrypt only on-die, attestation hash, state scrubbed on exit); AMD/Intel memory encryption. Motivated by untrusted operators + co-resident attackers.

## WSC hardware
- Compute: 1RU 2-socket workhorse; multi-node (Meta Yosemite: 1-socket blades sharing NIC/BMC/power); **heterogeneous fleet** matched to workloads (Meta's 7 server types); DSA servers (8×H100 DGX: NVLink 900GB/s intra, 400Gbps IB per GPU, 10kW) as the new big unit.
- Arm in the cloud is real and uses **big OOO cores** (Graviton), not wimpy cores (see fallacies).
- Memory trend: DDR pin limits (3.2–8.4Gb/s) vs logic transceivers (64–100Gb/s) → **CXL**: memory controllers move to buffer chips; DRAM sharing/disaggregation across servers; HBM in CPU packages.
- Storage: local NVMe for hot/enterprise; **JBOD/JBOF** (dumb disk/flash arrays, 72 HDDs or 30 SSDs) + head nodes running distributed storage software; reliability by software (replication 3× = 200% overhead vs Reed-Solomon RS(9,6) = 50% overhead + rebuild reads) unified across disk/enclosure/rack/network failures.
- Networking: **Clos** (TOR→leaf→spine) built from identical commodity chips; Jupiter: 1.3 Pbit/s bisection; **oversubscription** 3:1 typical (worked sizing: 98K servers at 3:1 vs 33K at 1:1); copper to TOR, optics above; **optical circuit switches (OCS)** replace spines at Google — rate-agnostic MEMS mirrors → incremental upgrades + **topology engineering** (reconfigure connectivity daily to match demand matrix). Centralized control plane; RDMA (IB/RoCE) for µs remote memory.
- Programmer's-view memory hierarchy: local DRAM 100ns/409GB/s; rack DRAM +100µs; row DRAM +200µs, 2.5GB/s at 20Gbps oversub; local flash 100µs; remote flash barely slower than local (device latency dominates); **remote disk ≈ remote DRAM for big transfers** (network is the bottleneck; parallelism wins). AMAT example: 90/9/1% local/rack/row → 100× slowdown vs all-local → locality within server is vital.

## I/O device architecture
- NIC path: SQ/CQ ring buffers + doorbell + DMA + interrupts. Optimizations: stateless offloads (checksums), LSO/USO (1MB = 1 protocol pass not 112), **interrupt moderation + steering + RSS** (per-connection core affinity; 200M int/s otherwise), DDIO (packets into LLC), header splitting, zero-copy. SmartNICs = programmable cores offloading VPC overlay/encryption/storage protocols (Firestone/DPU). RDMA NICs (IB/RoCE) = full transport in hardware + GPU zero-copy.
- **NVMe FTL**: LBA→page map, block info table (erase counts), write pointer; log-structured writes + garbage collection → **write amplification**; wear leveling; supercapacitor flush on power loss. NVMe: 50–100µs, 1–2M IOPS vs disk 5–10ms, 100–200 IOPS.

## Power & cooling
- PUE = facility/IT power: 2.5 (2007 industry) → 1.57 (2021 avg) → **1.10 Google fleet average**. Levers: rack-level battery UPS (99% vs 94–97% double-conversion central UPS), DC distribution, hot/cold aisle containment, 27°C cold aisles, server fans + room fans co-designed, air/water economizers (free cooling), liquid/immersion cooling for 400W CPUs / 800W GPUs.
- Power delivery chain: 115kV → 10–50kV → 400–500V + UPS/gensets → PDUs (6kW breakers) → server PSUs → VRMs; ~11% losses classic, ~10% more inside the server (sPUE).
- **Power provisioning**: measured peak ≈ 60% below nameplate; **oversubscribe power 40%** across servers (peaks uncorrelate); mitigate spikes with DVFS, rack batteries, descheduling, task migration.

## Economics (the numbers to remember)
- ~$9–13/W build (2010) → $7–10/W (2018); TCO dominated by servers (60–65%) + facility (10%); power+PUE only 5–8%.
- Amortize: facility 10–20yr, network 4yr, **servers 3yr** → decade server capex ≈ 3× facility capex (the "facility costs more" fallacy).
- **$2 per watt-year** fully burdened (amortized infra + electricity) = the budget for any power-saving design decision.
- ~$0.10–0.11/server-hour all-in; electricity swings it only $0.10–0.13 across $0.03–0.15/kWh.
- Turning off idle machines saves ≤7% of OPEX (infra amortization > power bill) → better: run batch/spot work instead; energy-proportional servers; active low-power modes (µs wake) over sleep modes (DRAM/disk can't be touched).

## Efficiency levers
- Utilization: right-sizing, autoscaling, interference-aware scheduling, harvesting/spot instances, cache/MBM partitioning for isolation (Paragon/QoS).
- **Tail latency is the product**: Bing 200ms delay → +0.6% revenue loss and lingering search abandonment; SLOs are percentile targets (99%/99.9%); **tail tolerance** (fine-grained load balancing, hedged requests) beats trying to eliminate variability.
- Latency cliff gap: hardware hides ns (caches) and ms (OS), but **µs-scale events (flash, fast NICs) lack programming support** — a standing open problem.

## Custom silicon: AWS as the case study
- Why: vertical innovation, specialization, HW/SW co-scheduling, security, and skipping the 20–100% commodity margin at volume (custom ASIC dev cost $50–100M amortizes).
- **Nitro**: hypervisor offloaded to cards (ENA VPC data plane, EFA/SRD RDMA, EBS remote-storage NVMe, instance storage with FTL + key-destroy-on-terminate, Nitro Controller); minimal KVM hypervisor only allocates resources; **VM ≈ bare metal within 1%**; 70 → 600+ instance types; secure boot chain with TPM + formally verified boot code; no AWS employee data path (encryption everywhere).
- **Graviton**: 3 generations, OOO Arm cores (G3: 64 cores, 7 chiplets, DDR5-4800, 2TB/s mesh, small LLC justified by bandwidth+prefetch, no SMT for isolation, single-socket only, always-on memory encryption, PAC+TRNG); energy-proportional by design (~50% TDP at 50% load); fleet-aware CPU selection at 50/90/99th-percentile load.
- SPECrate across 6 instances: no single winner — Ice Lake best single-thread int, Milan best FP + best all-core int (192 vCPUs), Graviton3 wins individual benchmarks (fotonik3d) → **instance diversity is a feature**.

## Fallacies & pitfalls
- "Cloud is unprofitable" — AWS = ~¾ of Amazon's operating profit.
- **Wimpy-node fallacy**: Atom-class servers 3× query latency, worse QoS under load, even 1–2% worse search answers at low load → revenue loss dwarfs energy savings; use low-end of *server*-class, and remember Amdahl inside requests.
- "Many tiny servers are always better": scheduling overhead + finer partitioning inefficiency.
- PUE is gamed: measure point (before substation vs after), season, design-goal vs 12-month running average.
- Facility capex > server capex: false after amortization (3× servers).
- Sleep modes: inactive low-power modes useless (wake cost + monitoring needs liveness); prefer active low-power + energy proportionality.
- "ECC optional at scale": Google measured DRAM FITs 15–25× vendor claims (25–70K FIT/Mb); ⅓ of servers see ≥1 uncorrectable/yr; without Chipkill, SECDED-only would leave 4–10× more silent; parity-only would burn ~6% of fleet capacity in reboots. (Google's 2000 stuck-at-zero index corruption = the origin story.)
- Flash-only-for-warm-data: cold photo storage on spinning disks costs 5W/disk to meet latency SLOs; flash idles free → sometimes cheaper for cold data.
