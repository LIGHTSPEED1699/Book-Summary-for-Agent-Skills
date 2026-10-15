# Goralski Ch9–17 — Routing, Forwarding, Transport, Peering

## Ch9–10 — Routing and forwarding
- Routing vs forwarding: routing = building the table (protocols, policies); forwarding = per-packet table lookup out an interface.
- Host routing tables on FreeBSD/RedHat/Windows shown directly (default gateway, static routes) — hosts are routers-lite.
- Flat vs hierarchical routing; the cost of every-destination tables; why hierarchy (ASes) is unavoidable at Internet scale.
- Forwarding mechanics on the TIN routers: longest-prefix match, next hop, traceroute walks the forwarding path.

## Ch11–13 — UDP, TCP, sockets
- **UDP**: minimal header (ports, length, checksum over pseudo-header), datagram semantics, the voice/streaming choice.
- **TCP header**: ports (ephemeral 1024–4999 on some Unix), **sequence/acknowledgment numbers** with per-connection **ISN** (time-based on Windows, more elaborate on Unix — spoofing note), header length, **ECN bits**, six control bits (URG/ACK/PSH/RST/SYN/FIN), **window size** (flow + congestion control), checksum, urgent pointer.
- TCP state machine and connection management (three-way handshake, teardown) observed via Wireshark/tcpdump across FreeBSD/RedHat/Windows — the book watches segment sequences rather than injecting loss.
- Flow control (advertised window) and congestion control; **multiplexing**: the socket interface — how the OS demultiplexes (protocol, src/dst IP, src/dst port) to the right process; BSD sockets API, well-known ports, /etc/services.

## Ch14 — Routing and peering (the AS concept)
- Connection-oriented vs connectionless networks compared (Table 14.1): circuit identifiers vs global addresses, signaling setup vs independent per-packet routing, frame relay/ATM/PSTN vs IP/Ethernet; the Internet won because connectionless is simpler and self-heals around failures automatically.
- **Autonomous system (AS)**: a routing domain under one administration and one routing policy; the Internet = interconnection of ASes; **peering** arrangements between ISPs (the TIN's Ace/Best ISPs peer); transit vs peering economics in plain language.
- IGP inside the AS, EGP between ASes — the two-protocol architecture that lets the Internet scale.

## Ch15 — IGPs: RIP, OSPF, IS-IS
- **RIP**: distance-vector, hop-count metric, simplicity and limits (split horizon, poison reverse).
- **OSPF**: link-state, areas, Dijkstra SPF, LSAs; configured on TIN routers with real output.
- **IS-IS**: link-state from the OSI world, chosen by many ISPs; TLV flexibility.
- Comparison by design philosophy; the book configures all three on the same topology to show differences concretely.

## Ch16–17 — BGP and expanded BGP
- **BGP is not a routing protocol in the IGP sense**: it carries **reachability information (NLRI)** about routes between ASes, not computed routes; no metrics — **attributes**; path selection is policy-driven.
- **EBGP between ASes, IBGP inside an AS** (why both are needed: transport across the AS without the IGP carrying BGP state).
- BGP runs on border routers (P9, P4 in AS 65531; P7, P2 in AS 65527); IGP still runs inside for internal reachability.
- Routing policy: what BGP is really for — corporate/ISP policy on what routes to accept/advertise; attributes and path selection touched, full policy complexity deliberately out of scope.
- Ch17 expanded uses: BGP scaling, route reflection/multihoming themes, BGP as the Internet's policy distribution system.

## Practitioner takeaways (Ch9–17)
- The Internet's scaling trick: hierarchy (ASes) + two routing planes (IGP inside, BGP between) + policy at the edges.
- BGP troubleshooting is policy reasoning, not metric reasoning — remember NLRI/attributes, not distances.
- TCP behavior differs subtly by OS (ISN generation, window defaults) — the book's cross-platform captures are the debugging habit to copy.
