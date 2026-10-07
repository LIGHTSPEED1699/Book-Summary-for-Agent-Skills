# Chapter 6 — Manual Shut-off Valves, Manual Isolation Valves, and Test Firing Valves (Clause 6)

## Overview
Clause 6 specifies the hand-operated valves that make a valve train serviceable and testable: manual shut-off, dual-fuel isolation, and test firing valves with their interlock for large inputs.

## Core Content
- **6.1 Dual/multiple fuel isolation**: With two or more fuels (dual/combination burner) and pilot takeoff from the main train, a manual isolation valve goes **upstream of the main SSOVs and downstream of the pilot connection** — pilot can run on shared fuel while the main train is isolated.
- **6.2 Requirements for manual, isolation, and test firing valves**:
  - Quarter-turn type, certified to CSA 3.11, CSA 3.16, or CSA/ANSI Z21.15/CSA 9.1 (or approved for gas);
  - Operate within rated temperature/pressure;
  - Clear open indication (handle parallel to flow is acceptable);
  - ON/OFF operable without removing the handle;
  - Stops in both open and closed positions;
  - Attached handle, loose key, or extended wrench; gear-operated handwheel allowed **> NPS 4**.
- **6.3 Pilot manual shut-off valve**: Independently controls the pilot, located **upstream of all other pilot-train components**.
- **6.4 Pilot test firing valves**: Each burner gets a test firing valve **except pilots ≤ 20 000 Btu/h (6 kW)**.
- **6.5 Location**: Downstream of all SSOVs, as close as practicable to the burner.
- **6.6 Large inputs (> 12.5 MMBtu/h / 3660 kW)**: The test firing valve needs an **electric or pneumatic end switch** wired into the safety limit control circuit, interlocked so the valve stays closed until **prepurge completes and pilot flame is proven**.
- **6.7 Exemption**: 6.6 does not apply where safety limit controls are **manual-reset type** or wired into the non-recycling circuit of the combustion safety control (or a combination).

## Decision Table
| Item | Rule |
|---|---|
| Valve type | Quarter-turn, certified (3.11/3.16/Z21.15-9.1) |
| Open indication | Handle parallel to flow or equivalent |
| > NPS 4 | Gear-operated handwheel permitted |
| Pilot test firing valve | Not required ≤ 20 000 Btu/h pilot |
| Test firing valve position | Downstream of SSOVs, near burner |
| > 12.5 MMBtu/h test valve | End-switch interlock to prepurge + pilot proven |
| Interlock exemption | Manual-reset or non-recycling safety limits |

## Key Takeaways
- Three distinct hand valves: pilot manual shut-off (first in pilot train), test firing valve (last before burner), dual-fuel isolation (between pilot tap and main SSOVs).
- Test firing valves let technicians attempt main ignition under controlled leak-test conditions — hence the 12.5 MMBtu/h end-switch requirement.
- The 6.7 exemption recognizes that manual-reset/non-recycling safety circuits already prevent unsafe resets.

## Connects To
- ch05 (pilot supply), ch07–ch08 (SSOVs upstream of test valve), ch11 Clause 12 (safety limit control circuits), ch12 Annex A (start-up dry-run procedure).