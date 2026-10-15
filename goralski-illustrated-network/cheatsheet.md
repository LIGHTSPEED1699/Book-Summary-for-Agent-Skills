# Cheatsheet — Goralski, The Illustrated Network

## Protocol → chapter locator
Layers 1 · Ethernet 2 · Switching 3 · WLAN 4 · Addressing 5 · ARP/NDP 6 · Headers 7 · ICMP 8 · Routing 9 · Forwarding 10 · UDP 11 · TCP 12 · Sockets 13 · Peering/AS 14 · IGPs 15 · BGP 16 · BGP expanded 17 · Multicast 18 · MPLS 19 · MPLS VPN 20 · EVPN/VXLAN 21 · DHCP 22 · DNS 23 · FTP 24 · SMTP 25 · HTTP 26 · SSL 27 · SNMP 28 · Cloud/SDN/NFV 29 · Security 30 · NAT 31 · Firewalls 32 · IPSec 33 · VoIP 34 · Media Part VIII.

## Quick header facts
- IPv4: 20-byte base + options; ID/flags/fragment offset; TTL; header checksum.
- IPv6: fixed 40-byte base; no checksum; extension headers; hop limit; fragmentation at sender.
- TCP: ports, ISN-based seq/ack, 4-byte header length, ECN, SYN/ACK/PSH/RST/FIN/URG, window, pseudo-header checksum.
- UDP: src/dst port, length, checksum (pseudo-header).
- MPLS label: 20 bits + EXP + S + TTL — deliberately tiny.

## Debugging drills (the TIN method)
1. Reproduce on a known topology; capture with Wireshark/tcpdump at both ends.
2. Intra-AS reachability: check IGP adjacency, then routing table (FreeBSD `netstat -rn`, RedHat `ip route`, Windows `route print`), then forwarding (traceroute).
3. Cross-AS: check BGP neighbor state, accepted/advertised routes, policy — not metrics.
4. Application: socket-level (ports, /etc/services), then session trace (handshake, window updates, resets).
5. Performance: window size, RTT from captures, jitter for voice.

## Design checklists
- Addressing: hierarchical, CIDR-aggregatable, private space planned, IPv6 dual-stack ready.
- Routing: IGP choice (OSPF/IS-IS for scale, RIP only tiny); BGP policy documented per peering/transit.
- VPN/overlay: MPLS VPN for WAN isolation, VXLAN/EVPN for data-center scale.
- Services: DHCP scopes + relays; DNS redundancy; NTP implied.
- Security: SSL for apps, IPSec tunnel mode site-to-site, firewall rules at edges, NAT consciously (not as fake security).
- Management: SNMP v3 + MIBs, telemetry streams, RMON probes.
- Acceptance: VoIP call quality test across the whole path.

## Comparison tables worth memorizing
- Switched vs connectionless (Ch14 Table 14.1): circuit IDs vs global addresses; signaling setup vs per-packet routing; frame relay/ATM/PSTN vs IP/Ethernet.
- TCP vs UDP: reliable ordered connection vs unreliable datagram; choose UDP for voice/streaming, TCP for completeness.
- IGPs: RIP hop-count simplicity; OSPF areas/SPF; IS-IS TLV ISP flexibility.
- NAT vs firewall vs IPSec: address reuse/hiding vs policy filtering vs cryptographic protection.

## Common pitfalls
- Treating BGP like an IGP (looking for metrics) — it's NLRI + attributes + policy.
- Forgetting frames are rewritten every hop; debugging L2 when the problem is L3 (and vice versa).
- NAT as a security plan; IPSec SA mismatches (one direction works, the other doesn't).
- Polling-only management at cloud scale — add telemetry.
- Ignoring the media layer: cabling/optics/FEC failures masquerade as "random" protocol flapping.
