# Goralski Ch1–8 — Protocols, Layers, LANs, Addressing, Headers

**The Illustrated Network: How Networks and Technology Are Changing the Way We Talk and Work** (Walter Goralski, 2nd ed., Sybison/Pearson 2020). A whole-Internet-in-one-network teaching approach: one running topology ("the Illustrated Network", TIN) carries every protocol, with real CLI output (Cisco/Juniper JUNOS routers, FreeBSD/RedHat/Windows hosts) and Wireshark captures.

## The Illustrated Network (the book's spine)
- Multi-site enterprise: main site + research site + remote offices, connected through **two ISP ASes** (Ace ISP AS 65531, Best ISP AS 65527, later merged) with peering; routers named CE* (customer edge), P* (provider), R* (site); hosts bsdclient/lnxclient/wincl1 etc.
- Conventions: ssh/FTP to routers (JUNOS 15.1, Unix-like shell), CLI on Unix hosts, GUI on Windows, **Wireshark packet captures** as the ground truth for every protocol discussion.
- Router roles: LAN switches (Layer 2 frames), routers (Layer 3 packets), firewalls on site routers, MPLS across the ISP core.

## Ch1 — Protocols and layers
- TCP/IP stack: **data link** (framing, physical addressing, error detection, access control, flow control; frames have header + trailer), **network** (packet delivery source→destination across many links; logical hierarchical addresses; routing tables; hop-by-hop forwarding — frames change at every hop, the packet endures), **transport** (process-to-process: TCP connection-oriented reliable ordered vs UDP connectionless datagram), application layer.
- Why two addresses: physical addresses are numerous, unsystematic, locally significant; network addresses are hierarchical (telephone-area-code analogy) and globally unique. **Address resolution** maps between them.
- Routers = Layer 3 intermediate systems (two+ physical/data-link instances, forwarding decision at Layer 3); switches = Layer 2. IP = "best effort/unreliable"; transport adds reliability.

## Ch2–4 — Ethernet, switching, WLAN
- Ethernet: frame formats (DIX Ethernet II + 802.3/802.2), MAC addressing, CSMA/CD heritage, switched full-duplex Ethernet; structured cabling generations.
- Switching: bridging/learning, spanning tree, VLANs, layer-3 switching; switches vs routers division of labor.
- Wireless LANs: 802.11 families, association/authentication, the same TCP/IP above a very different Layer 2.

## Ch5–6 — Addressing and resolution
- **IPv4**: classful heritage → CIDR, subnetting, private addresses, hierarchical allocation; **IPv6**: 128-bit, unicast/multicast/anycast, autoconfiguration, why v6 finally arrived.
- **ARP** (IPv4) and **NDP** (IPv6, over ICMPv6): the address-resolution family; ARP tables, proxy ARP, duplicate address detection.

## Ch7–8 — Headers and ICMP
- **IPv4 header**: version/IHL, TOS/DSCP, total length, identification/flags/fragment offset, TTL, protocol, checksum, options; fragmentation and MTU interaction.
- **IPv6 header**: simplified fixed 40-byte base (no checksum, no fragmentation in routers) + **extension headers** chain; the design reset.
- **ICMP**: error reports (destination unreachable, time exceeded, parameter problem) and query messages (echo, router discovery); **traceroute** = TTL exhaustion + ICMP time-exceeded; ping; ICMPv6 carries NDP and multicast listener discovery.

## Practitioner takeaways (Ch1–8)
- Follow the packet, not the frame: end-to-end IP survives; L2 headers are rewritten hop by hop.
- Hierarchy in addresses is what makes routing tables scale — the telephone-area-code argument is the book's core scaling intuition.
- Wireshark on a real topology beats any diagram: every chapter's claims are capture-verifiable.
