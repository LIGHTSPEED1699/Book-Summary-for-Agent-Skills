# CSA C22.1:24 Patterns — Recurring Installation Templates

Synthesis of the recurring design/inspection patterns across the Code. Rule numbers verified against the source; each pattern is a shortcut to the governing sections.

## 1. Supply chain hierarchy (always identify which segment you're in)

**Supply service → Consumer's service → Service box/equipment → Feeder → Branch-circuit OCPD → Outlet**

- Consumer's service: service box (or equivalent) up to the supply service (Section 6 sizing rules, 6-300s).
- Feeder: service box to branch-circuit overcurrent devices (S8 load calc; Table 14 W/m² demand; 8-200 series).
- Branch circuit: final OCPD to outlets (8-202 series).
- Load calc chain: connected load → demand factors (8-104/8-106) → ampacity/size (Table 13 OCPD; Tables 1-4 conductors) → voltage drop check (8-102).

## 2. Ampacity decision chain (rule 4-004)

1. Pick base table: Table 1 (Cu free air), 2 (Cu raceway/cable), 3 (Al raceway/cable), 4 (Al free air).
2. Apply Table 5A if ambient >30 °C (e.g., 40 °C: ×0.88 at 75 °C rating, ×0.91 at 90 °C).
3. Apply Table 5C if >3 conductors in raceway/cable (4-6 → ×0.80; 7-24 → ×0.70).
4. Check termination temperature limits (rule 4-006: 60 °C/75 °C defaults; No. 1 AWG ≤100 A boundary).
5. Confirm against the protecting OCPD (Table 13 standard sizes).
6. Flexible cords/equipment wire: Table 12 instead (11A/11B conditions of use).

## 3. Grounding vs bonding (Section 10) — never mix the paths

- **System grounding**: source-side grounding of the system (neutral) via grounding electrode — rules 10-1xx/10-2xx/10-3xx; electrode conductors per Table 43/51.
- **Bonding**: non-current-carrying metal parts to the system — bonding conductors sized by OCPD rating via **Table 16**; service raceway bonding jumper per Table 41.
- No soldered connections in bonding paths (10-6xx); equipotential bonding for special occupancies (10-700s, e.g., pools 68-xxx, EVSE 86-xxx).
- Impedance-grounded systems: alarm/de-energization conditions per Table 17 (10-302).

## 4. Wiring method selection (Section 12)

- Interior dry residential: NMD90 (12-900s). Wet/outdoor: NMWU or raceway methods.
- Raceway fill: Table 8 (53%/31%/40%), conductor dimensions Tables 6A-6K, trade-size internals 9A-9H.
- Vertical runs: support per Table 21. Bends: Table 7 radius (12-924).
- Parallel conductors: 12-108 (and bonding in parallel per 10-602).
- Buried cable/raceway cover: Table 53. Cable tray: Table 12E ampacities + 5D spacing factors.

## 5. Receptacle & GFCI placement (Section 26 + occupancy sections)

- General: 26-700; bonding 26-702; GFCI Class A 26-704 (incl. within 1.5 m of wash basins/bathtubs/shower stalls); tamper-resistant 26-706; weather-exposed 26-708.
- Residential spacing: 26-720s (wall spacing, hallway 26-722, outdoor/garage counts 26-724); dedicated appliance receptacles 26-740s (dryer 14-30R, range 14-50R).
- Outdoor/wet occupancies stack more GFCI/bonding: pools/spas (68), marinas (78), EVSE (86).

## 6. Motor circuit template (Section 28)

- Conductors: ≥125% motor FLC (Table 37 insulation; sizes via Tables 27/28; motors per Table 44/45).
- Overload protection in the controller (starter includes it by definition); short-circuit/ground-fault OCP per Table 29.
- Disconnecting means within sight of and ≤9 m from motor + controller, or lockable open (28-600s).
- Welders: conductor multipliers Tables 42A/B/C by welder type; crane/hoist special ampacity Table 58.

## 7. Voltage drop verification (8-102)

- ≤3% feeder or branch; ≤5% supply-side-to-utilization total; basis = connected load, else 80% of OCPD rating.
- Dwelling 120 V/20 A general-use branches: Table 68 max-length method (90 °C Cu, 120 V 2-wire).

## 8. Hazardous locations workflow (Section 18 + Appendix J/L)

1. Classify: gas Zones 0/1/2 or dust Zones 20/21/22 (Section 18 rules + Appendix L factor checklist L4).
2. Map to legacy Division system if needed: Table 18A (Zone↔Division equivalence).
3. Select equipment per Table 18 (explosive-atmosphere suitability; App A product standards).
4. Install seals + bonding per Section 18 rules; verify with App H (gas detection) where applicable.

## 9. Special occupancies cross-reference pattern

Pools/spas (68) → GFCI + equipotential bonding grid; patient care (24) → isolated/essential systems; emergency power (46) → life-safety continuity; EVSE (86) → GFCI + bonding + 8-500 EVEMS load mgmt; renewables/ESS (64) → source interconnection + rapid shutdown-type requirements; temporary installations (76) → reduced durations with equivalent protection.

## 10. When rules seem ambiguous

- Check **Appendix B** Notes on Rules for the rationale (chapter map in ch13).
- Provincial amendments may modify effective text (ESA Ontario bulletins etc.) — confirm with the local AHJ.
- "Special permission" = written authority of the inspection department (Section 0 definition).