---
name: goralski-illustrated-network
description: Apply Goralski's The Illustrated Network (2nd ed., Sybison 2020) frameworks - the one-topology teaching method for TCP/IP, layer-by-layer protocol analysis with Wireshark ground truth, hierarchical addressing and the two-addresses argument, connectionless-vs-connection-oriented network design, the AS/peering scaling architecture (IGP inside, BGP NLRI-and-attributes between), TCP/UDP and socket multiplexing, MPLS labels and MPLS VPNs, VXLAN/EVPN data-center overlays, DHCP/DNS as the second global database, SNMP/MIB/RMON management plus streaming telemetry, cloud/SDN/NFV economics, NAT/firewall/IPSec (AH/ESP, SAs) layering, and VoIP as the QoS stress test - when designing, teaching, configuring, or troubleshooting enterprise/ISP TCP/IP networks.
---

# The Illustrated Network (Walter Goralski, 2nd ed., Sybison/Pearson 2020)

937-page, 34-chapter TCP/IP course built on one running multi-site enterprise + two ISP ASes ("the Illustrated Network", TIN), with real Cisco/Juniper JUNOS/FreeBSD/RedHat/Windows CLI and Wireshark captures for every protocol.

Use when: building or debugging an enterprise/ISP network, teaching TCP/IP concepts, choosing routing architectures, layering VPN/security, or reasoning about MPLS/VXLAN/SDN evolution.

## Decision index

| Situation | Go to |
|---|---|
| Layer semantics, why two addresses, hop-by-hop vs end-to-end | chapters/01-08-layers-addressing.md Ch1 |
| Ethernet/switching/VLAN/WLAN mechanics | Ch2–4 |
| Subnetting, CIDR, IPv6, ARP/NDP | Ch5–6 |
| Header fields, fragmentation, traceroute/ping mechanics | Ch7–8 |
| Host routing tables, forwarding vs routing | chapters/09-17-routing-transport.md Ch9–10 |
| TCP header/state machine, UDP, sockets/multiplexing | Ch11–13 |
| AS concept, peering, ISP economics | Ch14 |
| RIP vs OSPF vs IS-IS choice | Ch15 |
| BGP: NLRI, attributes, EBGP/IBGP, policy | Ch16–17 |
| Multicast | chapters/18-27-mpls-services.md Ch18 |
| MPLS, traffic engineering, MPLS VPN | Ch19–20 |
| Data center overlays (VXLAN/EVPN) | Ch21 |
| DHCP/DNS operations | Ch22–23 |
| FTP/SMTP/HTTP/SSL application behavior | Ch24–27 |
| SNMP/MIB/RMON + telemetry | chapters/28-34-mgmt-security-media.md Ch28 |
| Cloud/SDN/NFV strategy | Ch29 |
| NAT/firewalls/IPSec composition | Ch30–33 |
| VoIP/QoS | Ch34 |

## The one-paragraph model
The Internet scales by **hierarchy**: hierarchical addresses (area codes) → hierarchical routing (IGP inside an AS, BGP carrying reachability + policy attributes between ASes) → hierarchical naming (DNS). Above a best-effort IP core, each layer adds exactly what it must: TCP adds reliability via sequence numbers and windows; MPLS/VXLAN add circuit-like engineering and isolation; SSL/IPSec/firewalls add security at their own boundaries; SNMP/telemetry and cloud/SDN/NFV add management and elasticity. The book's method: one real topology, every claim verified with CLI output and Wireshark captures.

## Files
- `chapters/01-08-layers-addressing.md` — layers, LANs, addressing, headers, ICMP
- `chapters/09-17-routing-transport.md` — routing, forwarding, TCP/UDP/sockets, AS/BGP
- `chapters/18-27-mpls-services.md` — multicast, MPLS/VPN, VXLAN/EVPN, DHCP/DNS, apps
- `chapters/28-34-mgmt-security-media.md` — SNMP/telemetry, cloud/SDN/NFV, security, VoIP, media
- `glossary.md`, `patterns.md`, `cheatsheet.md`
