# Chapter 7 — Pilot Safety Shut-off Valves and Pilot Burners (Clause 7)

## Overview
Clause 7 tiers pilot-train SSOV requirements by input and specifies pilot burner installation, ignition reliability, and turndown. It is the pilot-side mirror of Clause 8's main-burner valve tiers.

## Core Content
### 7.1 SSOV requirements
General properties (7.1.1): certified; open only when energized; manual-reset types open only by manual reset + energizing medium; safety features cannot be bypassed; no bypass except for an approved VPS; multiple valves **wired in parallel** (parallel wiring = loss of either control power closes both).

### Input tiers
| Pilot input | Minimum SSOV arrangement |
|---|---|
| ≤ 20 000 Btu/h (6 kW) | One certified SSOV (Z21.21/6.5 or CGA 3.9), or circuit controlled by combination control (Z21.78/6.20) and/or thermocouple-type control (CAN1-6.4 / Z21.20/C22.2 60730-2-5) |
| > 20k to 400k Btu/h (120 kW) | Two SSOVs in series, wired in parallel (Z21.21/6.5) — or one valve marked **C/I** (or CGA 3.9) |
| > 400k to 3.5 MMBtu/h (1025 kW) | Two certified SSOVs, one marked C/I or CGA 3.9 — or one C/I valve **with proof of closure switch** interlocked into the starting circuit (holding circuit must not defeat the switch) |
| > 3.5 MMBtu/h | Meet full **main valve train** requirements (Clause 8) |

- **7.1.6 VPS**: A VPS used in a pilot train shall be approved (Annex E guidelines).

### 7.2 Pilot burners
- **7.2.1** Installed per manufacturer's instructions, firmly secured, alignment maintained.
- **7.2.2** Designed, installed, adjusted for **safe and reliable ignition** of the main burner.
- **7.2.3** Pilot primary air not restricted; pilot flame must not impinge improperly on main burner orignition hardware.
- **7.2.5 / 11.3.2** Pilot trial-for-ignition timing ties to the flame safeguard (see ch11).
- Pilot location and shielding must ensure reliable main-burner light-off across firing range.

## Decision Table — Choosing the Pilot SSOV Set
| Input | Cheapest compliant arrangement |
|---|---|
| ≤ 20k Btu/h | 1 × SSOV or combination/thermocouple control circuit |
| 20k–400k | 1 × C/I valve |
| 400k–3.5 MMBtu/h | 1 × C/I + proof of closure (start circuit) |
| > 3.5 MMBtu/h | Follow Clause 8 main-train rules |

## Key Takeaways
- Parallel wiring of series SSOVs is deliberate: either valve's control failure de-energizes both.
- "C/I" (close-and-interlock) marking substitutes for a second valve up to 3.5 MMBtu/h; beyond that, proof of closure or full main-train rules apply.
- Proof-of-closure interlock goes in the starting circuit, and the holding circuit must never bypass it.
- Pilot burner hardware discipline (mounting, alignment, air) is code-level, not just workmanship.

## Connects To
- ch05 (pilot supply/regulator), ch06 (pilot manual + test firing valves), ch08 (main SSOV tiers — the >3.5 MMBtu/h destination), ch11 Clause 11 (ignition timing), ch12 Annex E (VPS).