# Patterns — Goralski, The Illustrated Network

## P1. One-topology verification method (the book's meta-pattern)
**Pattern**: build one realistic multi-site topology; demonstrate every protocol on it with real CLI (Juniper JUNOS, Cisco, FreeBSD, RedHat, Windows) and confirm with Wireshark captures. **Use**: when learning or debugging any protocol, don't trust prose — capture the actual packets on a network you control. **This is the single most transferable habit in the book.**

## P2. Hierarchy is the scaling answer
**Pattern**: flat schemes (physical addressing, every-destination routing, single-level names) always lose to hierarchical ones (IP area-code structure, AS-based routing, DNS tree). **Rule**: when a network table grows unboundedly, introduce a level of hierarchy plus a protocol that aggregates at the boundary (IGP inside, BGP between).

## P3. Two-addresses, two-planes
**Pattern**: keep a locally-significant identifier (MAC, MPLS label, VXLAN VNI) AND a globally-unique one (IP, BGP NLRI). The local one enables fast/engineered forwarding; the global one enables end-to-end reachability. MPLS and VXLAN are the same pattern re-applied.

## P4. Connectionless core, connection-oriented services on top
**Pattern**: the Internet won because the core routes each packet independently (self-healing, simple signaling); circuit-like guarantees (VPN, traffic engineering, QoS) are built as overlays (MPLS LSPs, VXLAN/EVPN, IPSec tunnels) where needed. **Anti-pattern**: rebuilding connection-oriented setup inside the core.

## P5. BGP = policy, IGP = reachability
**Pattern**: inside the AS run OSPF/IS-IS (fast convergence, metrics); at AS boundaries run BGP and think in attributes and policy (what do I accept, from whom, and advertise to whom). **Troubleshooting rule**: cross-AS problems are policy problems; intra-AS problems are topology/metric problems.

## P6. Layered security composition
**Pattern**: SSL/TLS for app sockets, IPSec (AH/ESP + SA, tunnel mode) for site-to-site over shared cores (composed on top of MPLS VPN in the book), firewalls/NAT at edges, physical/media security underneath. Each layer guards a boundary; compose rather than choose one.

## P7. Management designed in
**Pattern**: SNMP agents + MIBs from day one (managers few, agents many), RMON probes for distributed visibility, streaming telemetry for continuous state; virtual/overlay networks need their own management plane. **Anti-pattern**: "go have a look at it" management — the Internet outgrew it in the late 1980s.

## P8. Elasticity economics (cloud/SDN/NFV)
**Pattern**: pooling + metering + rapid elasticity beat fixed allocation (the 4 kHz voice-channel contrast). Separate control from forwarding (SDN) and functions from hardware (NFV) when utilization, not latency, is the binding constraint.

## P9. Voice as acceptance test
**Pattern**: VoIP exercises packetization, jitter buffers, QoS, signaling (SIP/H.323) simultaneously — if voice quality is good, the network's data plane, control plane, and management are all healthy. Use it as the integration test for any converged network.

## P10. Follow the header evolution
**Pattern**: each header encodes its era's priorities — IPv4 (fragmentation, checksum, options) vs IPv6 (fixed base, extension headers, no in-router fragmentation); TCP (window, ECN) vs MPLS label (20-bit simplicity). When designing or debugging, ask what the header fields reveal about the intended service.
