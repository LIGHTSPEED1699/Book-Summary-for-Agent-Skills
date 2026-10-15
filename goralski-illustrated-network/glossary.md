# Glossary — Goralski, The Illustrated Network (2nd ed.)

## The running example
- **Illustrated Network (TIN)** — the book's single multi-site enterprise + ISP topology used for every protocol demonstration.
- **CE0…CE10** — customer-edge routers; **P2/P4/P7/P9** — provider (ISP) routers; **R*** — site routers; hosts: bsdclient/bsdserver (FreeBSD), lnxclient/lnxserver (RedHat/Ubuntu), wincli/winsvr (Windows).
- **Ace ISP AS 65531 / Best ISP AS 65527** — the two provider autonomous systems (later merged) with a peering arrangement.

## Layers and addressing
- **Hop-by-hop delivery** — frames forwarded router-to-router; frames technically differ on each link; the IP packet endures.
- **Physical (MAC) address** — locally significant, unsystematic; **network (IP) address** — logical, hierarchical, globally unique (telephone area-code analogy).
- **Address resolution** — mapping network→physical addresses: **ARP** (IPv4), **NDP** (IPv6 over ICMPv6).
- **CIDR** — classless inter-domain routing, the hierarchical allocation scheme; **subnetting**; private addresses.
- **Fragmentation** — packet too big for an outgoing frame/MTU; IPv4 fragments in routers, IPv6 relies on the sender (extension headers).

## Routing
- **Routing vs forwarding** — building tables vs per-packet lookup; **longest-prefix match**.
- **Autonomous system (AS)** — one routing domain, one administration, one routing policy.
- **IGP** — interior gateway protocol inside an AS: **RIP** (distance-vector, hop count), **OSPF** (link-state, areas, SPF), **IS-IS** (link-state, TLVs, ISP favorite).
- **BGP** — the exterior gateway protocol: carries **NLRI** (network layer reachability information) with **attributes**, not metrics; **EBGP** between ASes, **IBGP** across an AS; policy-driven path selection; "not really a routing protocol."
- **Peering / transit** — ISP interconnection arrangements; **routing policy** — what routes to accept/advertise at AS boundaries.
- **Connection-oriented (switched) networks** — circuit identifiers, signaling setup (frame relay, ATM, ISDN, PSTN); **connectionless (router-based)** — globally unique addresses, per-packet independent routing (IP, Ethernet).

## Transport
- **TCP** — connection-oriented reliable ordered delivery: **ISN** initial sequence number, sequence/ack numbers, **window size** (flow + congestion control), control bits SYN/ACK/FIN/RST/PSH/URG, **ECN** bits, pseudo-header checksum.
- **UDP** — connectionless datagram service; ports + length + checksum only.
- **Multiplexing / demultiplexing** — delivering to the right process via (protocol, src/dst IP, src/dst port); **sockets** API; **ephemeral ports** (1024–4999 on some Unix).

## Core and data center
- **MPLS** — label swapping: push/swap/pop; **LSP** label switched path; traffic-engineered convergence of voice/video/data.
- **MPLS VPN** — per-customer forwarding tables in a shared ISP core.
- **VXLAN** — MAC-over-UDP overlay with VNI segmentation (data-center scale beyond VLANs); **EVPN** — its control plane (MAC learning, multi-homing).
- **Multicast** — group delivery: IGMP/MLD membership, class D addresses.

## Services and management
- **DHCP** — discover/offer/request/ack lease with options and relays; **DNS** — hierarchical name database (resolvers, authoritative servers, zone files, records).
- **SNMP** — manager/agent network management; **MIB/SMI** — the management information tree; **RMON** — remote-monitoring MIB; **streaming telemetry** — push-based management beyond polling.
- **Cloud** — on-demand self-service, broad network access, resource pooling (multi-tenant), rapid elasticity, measured service; **SDN** — control plane separated from forwarding; **NFV** — network functions as elastic software.

## Security and voice
- **NAT** — edge address translation with mapping tables; **firewall** — packet filtering (hardware or software) at edges/hosts.
- **IPSec** — network-layer security: **AH** (authentication) and **ESP** (encryption) core protocols, **security association (SA)**, SAD/SPD, transport vs tunnel modes, **IKE** key exchange; "a piece of IPv6 pressed into service for IPv4."
- **SSL/TLS** — socket-level security between transport and application (HTTPS).
- **VoIP** — voice (comprehension) vs audio (fidelity); codecs, packetization/jitter, **H.323** vs **SIP** signaling.
