# Goralski Ch28–34 + Media — Management, Cloud/SDN, Security, Voice, Media

## Ch28 — Network management: SNMP, RMON, MIB
- **SNMP**: manager (few) ↔ agent (many) model; the Internet outgrew "go have a look at it" management in the late 1980s; SMI tree and **MIBs** designate management information; GET/SET/TRAP semantics; private MIBs; **RMON** remote monitoring MIB for distributed probes.
- **Network management and telemetry** (2nd ed additions): streaming telemetry beyond polling; management of virtual networks (the management implications of overlays/SDN).

## Ch29 — Cloud, SDN, NFV
- **Cloud** NIST-style definition: on-demand self-service, broad network access, resource pooling (multi-tenant), rapid elasticity, measured service; the economics — utilization and the shift from centralized data to network-shuttled analytics.
- **SDN**: control plane separated from forwarding (controller decides, routers/switches forward); OpenFlow-style flow tables; the controller as the new routing brain.
- **NFV**: network functions (firewalls, NAT, VPN gateways) as software on general-purpose hardware, instantiated elastically — the operational mirror of cloud economics.
- The through-line: statistics-driven networks — bandwidth/switching once allocated in fixed units (4 kHz voice channels) are now metered, pooled, elastic.

## Ch30–33 — Security
- **NAT** (Ch31): address translation at the edge (CE0 doing NAT for LAN1 hosts); private→public mapping tables; the accidental firewall debate.
- **Firewalls** (Ch32): packet filtering on site routers, host/client protection, hardware vs software firewalls; rules as routing-policy cousins.
- **IPSec** (Ch33): "a piece of IPv6 pressed into service for IPv4 out of desperation"; **AH** (authentication) and **ESP** (encryption) core protocols — not standalone protocols; **security associations (SAs)** and SAD/SPD; modes (transport vs tunnel); **IKE** for key exchange; deployed on top of the MPLS VPN between site routers — layered security on layered connectivity.
- (Ch27 SSL sits with the apps; Ch30 in this edition covers network security themes bridging into NAT/firewall/IPSec.)

## Ch34 — VoIP
- Voice vs audio distinction (comprehension of speech vs full-fidelity sound); why voice quality over IP was long controversial; codec basics, packetization delay, jitter and the need for buffering; H.323 vs **SIP** signaling; an Avaya IP Softphone "borrowed" onto the TIN for demonstration; QoS reality: best-effort IP vs voice expectations.

## Media part (Part VIII)
- Structured cabling and physical media generations: twisted pair categories, fiber types, the "packet optical" layer, forward error correction; the reminder that every abstraction above still rides photons and electrons.

## Practitioner takeaways (Ch28–34)
- Management is a protocol like any other: SNMP/MIB/RMON plus modern streaming telemetry; design it in, not bolt on.
- Cloud/SDN/NFV = the same economic logic (pooling, elasticity, metering) applied to compute, control, and network functions.
- Security stacks: SSL at app, IPSec at network (AH/ESP + SA), firewalls/NAT at edges — each layer protects a different boundary; the TIN shows them composed on one topology.
- VoIP is the strictest QoS test of any IP network: if voice works, the data plane, signaling, and management all work.
