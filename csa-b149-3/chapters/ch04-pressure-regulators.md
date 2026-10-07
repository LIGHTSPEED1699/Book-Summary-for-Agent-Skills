# Chapter 4 — Pressure Regulators (Clause 4)

## Overview
Every burner needs regulated fuel. Clause 4 mandates one regulator for the main supply, a separate one for pilots, sets tolerance and type, and controls venting of pilot regulators.

## Core Content
- **4.1 Main regulation**: Fuel supply to the burner (or burner group) shall be regulated by a pressure regulator.
- **4.2 Independent pilot regulation**: Pilot supply shall have its own regulator, independent of the main burner regulator — main regulator failure must not over-pressure the pilot.
- **4.3 Regulator type**: Spring-loaded or pressure-balanced type only.
- **4.4 Operating tolerance**: Outlet pressure within **±10%** of set pressure across the full firing range (min to max input).
- **4.5 No bypassing**: A regulator shall not be bypassed.
- **4.6 Lock-up requirement**: Inlet pressure > 0.5 psig (3.5 kPa) → regulator must be **lock-up (positive shut-off)** type, or integral to a multifunctional control.
- **4.7 Pilot regulator bleed vents**:
  - Lighter-than-air gas: bleed vent outdoors (per B149.1) or into combustion chamber adjacent to a continuous pilot — **unless** inlet ≤ 2 psig AND leak-limiting design restricts escape to ≤ 2.5 ft³/h (SG 0.6 gas, ≤ 7 mg H2S/m³).
  - Heavier-than-air gas: vent outdoors (per B149.2) — unless inlet ≤ 2 psig AND leak-limiting ≤ 1 ft³/h (SG 1.53).
  - Vent-limiting regulators must be in ventilated spaces only.
- **4.8 Regulator venting**: Regulators needing atmosphere access shall vent to a safe location; vent-limiting designs (per 4.7 and 10.6.8) need no external vent line. Exception: zero governors on gas/air proportioning systems still need venting.
- **4.9 Certification**: Regulator certified to **CSA/ANSI Z21.18/CSA 6.3**, *or* protected by low and high gas pressure safety devices monitoring outlet pressure (high set per 12.5.1, low per 12.5.2).

## Decision Table — Regulator Selection
| Condition | Requirement |
|---|---|
| Any main burner supply | One regulator, ±10% tolerance |
| Pilot supply | Separate independent regulator |
| Inlet > 0.5 psig | Lock-up type or multifunctional control |
| Pilot regulator, light gas, inlet ≤ 2 psig, leak-limited ≤ 2.5 ft³/h | Indoor bleed OK |
| Pilot regulator, heavy gas, inlet ≤ 2 psig, leak-limited ≤ 1 ft³/h | Outdoor vent required otherwise |
| No Z21.18/6.3 certification | Add high + low pressure safety devices (12.5.1/12.5.2) |

## Key Takeaways
- Pilot regulators are always separate from main regulators — never share.
- ±10% outlet tolerance across full turndown is the pass criterion.
- 0.5 psig inlet is the lock-up threshold.
- Without a certified regulator, the alternative is high/low pressure safety switches on the outlet.

## Connects To
- ch02 (Z21.18/6.3), ch05 (pilot supply takeoff), ch11 Clause 12.5 (pressure safety device settings), ch12 Annex M (documenting regulator settings).