# Goralski Ch18–27 — Multicast, MPLS, VPNs, Data Center, Core Services

## Ch18 — Multicast
- One-to-many delivery: IGMP for group membership, multicast routing vs flooding; multicast addressing (IPv4 class D, IPv6 multicast + MLD); the efficiency argument for group traffic.

## Ch19–20 — MPLS, IP switching, MPLS VPNs
- Convergence frame: telephone/TV/data networks merging onto one packet infrastructure — the motivation for traffic-engineered IP.
- **MPLS**: label swapping at the core edge (label push/swap/pop), LSPs (label switched paths), the marriage of connection-oriented forwarding speed with connectionless flexibility; configured across the merged ISP AS on the TIN routers.
- **MPLS-based VPNs**: per-customer label forwarding tables (VRF-style separation) so one ISP core carries many isolated customer networks; the enterprise site-to-site service built on the TIN.

## Ch21 — EVPN and VXLAN
- Data center overlay era: **VXLAN** encapsulation (MAC-over-UDP overlays, VNI segmentation, breaking VLAN scale limits), **EVPN** as the control plane for MAC learning/multi-homing; the modern replacement for classic VLAN-only designs.

## Ch22–23 — DHCP and DNS
- **DHCP**: four-step lease (discover/offer/request/ack), options, relays across routers.
- **DNS**: hierarchical domain tree, resolvers/authoritative servers, zone files, records (A/AAAA/MX/CNAME), the Internet's other global database besides routing.

## Ch24–27 — Application protocols
- **FTP**: control vs data connections, active/passive modes, GUI vs CLI clients on the TIN.
- **SMTP and email**: mail flow (MUA→MTA→MX), POP/IMAP retrieval, spam themes.
- **HTTP**: request/response, methods, status codes, Apache servers on TIN hosts, Web browsing traces in Wireshark.
- **SSL/TLS ("Securing Sockets with SSL")**: layering security between transport and application, certificates, HTTPS on the Apache sites — the same socket API, encrypted.

## Practitioner takeaways (Ch18–27)
- Two global databases make the Internet usable: routing tables (where) and DNS (names); both hierarchical.
- MPLS/VXLAN are the same idea at different layers: precomputed paths/overlays to give packet networks circuit-like properties (traffic engineering, isolation, scale).
- Every application protocol chapter follows the same drill: semantics → real session on the TIN → Wireshark dissection.
