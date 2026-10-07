# Chapter 8 — Main Safety Shut-off Valves, Input Flow Control, and Main Burners (Clause 8)

## Overview
The heart of the valve train. Clause 8 sets SSOV arrangements for main burners by input tier and burner count, then covers flow control (modulating/regulating valves) and main burner installation.

## Core Content
### 8.1 SSOV requirements
General (8.1.1): certified; open only when energized; manual-reset types need manual reset + energy; safety features cannot be bypassed; no bypass except approved VPS; multiple valves wired in parallel (except VPS requirements).
Certification: ≤ 400k Btu/h and inlet ≤ 0.5 psig — Z21.78/6.20 combination control, CGA 3.9, Z21.21/6.5, CAN1-6.4, or Z21.20/C22.2 60730-2-5 controls; > 400k Btu/h or inlet > 0.5 psig — **CGA 3.9 or Z21.21/6.5 only**.

### 8.1.2–8.1.10 input tiers (single and multiple burners)
| Rated input | Minimum arrangement |
|---|---|
| Appliance > 400k Btu/h | Main SSOVs certified to CGA 3.9 or Z21.21/6.5 marked **C/I**; pilot valves per Clause 7.1; downstream valve should be slow-opening |
| Single burner ≤ 400k Btu/h, inlet ≤ 0.5 psig | (a) 2 × SSOV series/parallel-wired; (b) 1 × C/I or CGA 3.9; or (c) combination control (Z21.78/6.20) and/or thermocouple-type control (CAN1-6.4 / Z21.20) |
| Single > 400k to 5 MMBtu/h (1500 kW) | 2 × SSOV series — or 1 × SSOV with **proof of closure** switch in start-up circuit |
| Single > 5 to < 12.5 MMBtu/h | 2 × SSOV series, one with proof of closure |
| Single ≥ 12.5 MMBtu/h (3660 kW) | 2 × SSOV series, **each** with proof of closure |
| Multiple ≤ 5 MMBtu/h total (common flame safeguard) | 2 × SSOV to each burner (header SSOV may count as one) — or 1 × SSOV w/ proof of closure per burner |
| Multiple > 5 to < 12.5 MMBtu/h | 2 × SSOV per burner, one with proof of closure (header valve counts as one of two) |
| Multiple ≥ 12.5 MMBtu/h | 2 × SSOV per burner, each with proof of closure (header valve may count as one) |

- **8.1.3**: A holding circuit used with proof of closure must not defeat the proof of closure switch.
- **8.1.12**: At ≥ 12.5 MMBtu/h, the main SSOVs shall be (a) supervised by an approved VPS, or (b) equipped with an automatic vent valve per 8.1.14/8.1.15. This is a leakage-supervision layer ON TOP of the proof-of-closure arrangements — a VPS does NOT replace the two-SSOV/proof-of-closure valve arrangement. VPS certification: 8.1.16 (CSA E60730-1 or approved); vent valve sizing: 8.1.17 (Tables 8.1/8.2). Annex E.2.1 (informative): VPS is primarily an alternative to a double block and bleed system; E.2.2: VPS shall not be used in lieu of periodic leak testing.

### 8.2 Input flow control systems
- Manual or automatic input controls (butterfly valves, actuators, modulating motors) shall operate within rating, maintain safe fuel-air ratio across range, and not defeat safety functions.
- Modulating controls coordinated with air side (linkage or FARC — Annex D for electronic FARC).

### 8.3 Main burners
- Installed per manufacturer instructions; securely mounted; maintain designed flame geometry.
- Burners shall operate over the declared firing range without flashback, lift-off, or impingement creating hazards.
- Trial-for-ignition timing for main flame per 8.3.11 / 11.2.3 (≤ 10 s typical, see ch11).
- Fuel-air ratio safety across turndown: cross-limiting or certified FARC for electronic systems.

## Decision Table — Fast Selection
| Situation | Pick |
|---|---|
| ≤ 400k, low pressure, smallest cost | Combination control circuit (Z21.78/6.20) |
| 400k–5 MMBtu/h | 2 series SSOVs *or* 1 SSOV + proof of closure |
| ≥ 12.5 MMBtu/h | 2 series SSOVs, both with proof of closure |
| Header + burner valves | Header SSOV counts as one of the two per burner |

## Key Takeaways
- The 400k Btu/h / 0.5 psig line separates "appliance-grade" controls from industrial SSOVs (Z21.21/6.5, CGA 3.9).
- Proof of closure obligations scale with input: none → one valve → both valves at ≥ 12.5 MMBtu/h.
- Multiple-burner trains credit the main header SSOV as one of each burner's two valves.
- Holding circuits must never defeat proof of closure — a recurring audit item.

## Connects To
- ch07 (pilot mirror tiers), ch06 (test firing valve end-switch at 12.5 MMBtu/h), ch11 Clause 11/12 (ignition, flame safeguard), ch12 Annexes E, K, M.