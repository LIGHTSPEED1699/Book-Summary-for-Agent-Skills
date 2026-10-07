# Chapter 12 — Annexes A–N (Informative Guidance)

## Overview
The annexes are informative but written in mandatory language so AHJs can adopt them directly. They contain the operational "how": start-up procedures, control-system guidelines, oxygen/liquid/solid fuel rules, risk-based programs, food trucks, turbines, hazardous locations, manuals, and hydrogen.

## Core Content
### Annex A — Initial start-up > 400k Btu/h
Dry run with all manual gas valves closed; minimum **4 control cycles**; installer present; room cleared.
- **Cycle 1**: damper ≥ 80% airflow in purge; verify 4 air changes; low-fire return at end of purge.
- **Cycle 2**: simulate airflow failure (motor, damper, belt, tubing removal) — no spark may occur.
- **Cycle 3**: meter the scanner signal — must read zero before ignition (no false signal from spark).
- **Cycle 4**: simulated flame before ignition → no start; low-fire position at spark; pilot trial ≤ 10 s; main valve opens after pilot proof; flame-loss closes main valve.
- **Cycle 5 — Pilot turndown test**: find lowest pilot heat release that reliably lights the main burner (pre-firing: reduce pilot to trip, record; light-off: re-purge, re-light, attempt main light; 3 successful attempts = pass). Fail → reposition pilot or add low pilot gas pressure safety.
- Performed separately for each burner on multi-burner units.

### Annex B — Valve diagrams; Annex C — Abbreviations
Reference diagrams of typical valve train arrangements and the Code's abbreviation list.

### Annex D — FARC (electronic fuel-air ratio control)
- Certified FARC → **ISO 23552-1**. Non-certified → monitored by a microprocessor-based system per Clause 12.7 that trips the burner on unsafe fuel-air ratio.
- Engineered non-certified FARC: closed-loop evaluation; continuous position feedback; fault detection preventing overshoot; declared operating curve commissioned and programmed; **fuel/air cross-limiting**; revert to safe state on fault; direct shaft position sensing preferred; external open/close indication.

### Annex E — VPS (valve proving systems)
- Definitions: detecting device, leak detection limit, leakage testing time, trip pressure, VPS sequence.
- VPS proves effective closure of SSOVs by detecting leakage (flow or pressure methods). Code hook: at ≥ 12.5 MMBtu/h the main SSOVs shall be VPS-supervised or equipped with an automatic vent valve (8.1.12); VPS in a pilot train shall be approved (7.1.6). VPS is NOT a substitute for proof-of-closure or two-valve arrangements (Annex E.2.1 frames it as an alternative to double block and bleed). Complex appliances must document testing time, minimum detection setting, and sequence (Annex M).

### Annex F — Oxygen in combustion systems
- Two SSOVs in series in oxygen line; filter/strainer upstream of first; high oxygen flow/pressure limit downstream of final regulator; low limit upstream of first SSOV; auto-close on interlock; approved VPS; **no vent valves** on oxygen piping; no SSOV as modulating valve; tightness-check means; position indication > 150k Btu/h (no indirect indication).
- Materials: Z21.21/6.5 valves declared for oxygen; oxygen-cleaned components verified under UV; N2 pressure test and purge; velocity limits per material (CGA G-4.1 cleaning).
- Oxygen-enriched burners: oxygen only when airflow proven continuously; auto-revert to safe ratio on oxygen loss; low coolant flow switch for liquid-cooled burners.

### Annex G — Liquid fuels; Annex H — Solid fuels
- Liquid: design per CSA B140 series + NFPA 86 Ch.8/NFPA 85; install per **CSA B139**; standard documentation package.
- Solid: design per **CSA B366.1**, install per **CSA B365** (+ NFPA 85); documentation incl. fuel switch-over procedure; functional test per B365 Clause 10.

### Annex I — Risk-based program (complex facilities)
- Applies where legislation permits audit of inspection/maintenance; appliances ≥ 4 burners with radiant tubes (flue gas outside tube) or load-combustion appliances; excludes direct-contact and radiant-tube appliances.
- **ALARP** principle (Figure I.1): unacceptable / tolerable / acceptable risk contours.
- Program elements: documented **QMS** (I.3, preapproval possible); competent **team** (I.4, engineer + facility operator); **hazard scenario identification** across all phases of operation (I.5.1); consequence → likelihood → risk estimation; documented risk criteria (I.5.5); risk reduction (I.5.6); component certification lists (I.5.7, e.g., CAN1-6.4 components); on-going **inspection, testing, maintenance, training** programs (I.6, incl. third-party training); documented **list of requirements** (I.7).
- Good-practice references: API 534/538/556/565, NFPA 85/69/86 overlays for refineries/petrochemical.

### Annex J — Mobile outdoor food service (food trucks)
- Enclosed units (4 walls + roof + floor), self-propelled or towed; open carts → ANSI Z83.11/CSA 1.8.
- Tanks per **CSA B51**; relief valves spring-loaded internal type, no shut-off between relief and tank; excess-flow valve integral to cylinder valve; QCC1 quick-coupling certified to UL/ULC 1337; vapour-withdrawal only; valve protection from road debris; no welding on pressure shell (field welding only on saddle plates/lugs/brackets); "readily accessible" shut-off (no tools/climbing); warning labels ("WARNING/AVERTISSEMENT" ≥ 6.4 mm letters).

### Annex K — SSOVs/vent valves for large gas turbines
- > 12.5 MMBtu/h AND inlet > 150 psig: no bypass or external closure prevention; no fuel-gas-powered closure; fast closing (**≤ 5 s**); Z21.21/6.5 compliance incl. leakage at declared cycles (recommended 20 000 cycles); UV protection outdoors; gas-resistant elastomers.

### Annex L — Hazardous locations
- B149.3 equipment is for **ordinary locations** by default; hazardous-location suitability is the electrical authority's jurisdiction (CEC 18-004).
- Classification by qualified persons, documented and authenticated; gas Zones 0/1/2, dust Zones 20/21/22; gas Groups IIA (propane, natural gas…), IIB, IIC (acetylene, hydrogen); dust Groups IIIA/IIIB/IIIC; equipment per Zone + Group; adequate ventilation means a valve train typically does not create a hazardous location.

### Annex M — IOM manual contents
- Installation (M.2.1): contacts, fuel, rating, elevation, classification, emergency procedures (power loss, external fire, flood, fuel release), BOM, schematics, wiring diagrams, anchoring, venting, LOTO, warning label locations.
- Complex adds (M.2.2): P&ID with safety controls, component data sheets, operating ranges per burner, area classification, supply/overpressure settings, **PLC control narrative** (firing method, purge duration/rate, ignition source, pilot mode, trial-for-ignition times, flame-failure response), VPS design/testing spec, explosion-relief drawings.
- Operation (M.3) and maintenance (M.4) similarly tiered; manufacturer's instructions = minimum maintenance interval where AHJ sets none.

### Annex N — Hydrogen and H2/natural gas blends
- Scope: utilization equipment; dry natural gas only as hydrocarbon base; excludes production, storage, dispensing, vehicle fuel.
- H2 flammability: **LFL 4.0%**, **UFL 75.0%** in air.
- Components > 66 psi (455 kPa): hydrogen-suitable materials, embrittlement assessed. **≤ 66 psi: no embrittlement considerations required.**
- Embrittlement classes (ISO/TR 15916): negligible — aluminum 1100/6061-T6/7075-T73, Be-Cu 25, copper/brass/bronze, A286; slight — 1020/1042 normalized, 310/316 SS, titanium (evaluation per ISO 11114-4); severe — Inconel/Monel, 4140, Ni steels, 304/410/440C SS, Ti-6Al-4V; extreme — maraging 18Ni-250, 17-7PH, **Inconel 718**.
- Leakage detection: blends > 25% H2 and > 66 psi → combustible gas detection for both gases; alarm at **20% LFL**; de-energize at **40% LFL** (with ventilation) or **20% LFL** (without).
- Valve train ≥ "no normal release, limited abnormal release"; threaded connections ≤ 2 in; tape ≤ 1.5 in.
- Flame detection > 25% H2: **UV or UV/IR scanners** (H2 flames have weak IR signature); flame rods acceptable if proven.
- Vent lines for double-block-and-bleed above 25% H2 may use flame arresters per **ISO 16852** (IIC/Group B).
- Area classification: blends > 25% H2 at > 66 psi → Area Classification study or **≥ 6 volume changes per hour** ventilation (NFPA 85 dilution basis).

## Key Takeaways
- Annex A's 4-cycle dry run + pilot turndown test is the de-facto start-up script for > 400k Btu/h equipment.
- Oxygen service: double SSOVs, no vent valves, oxygen-cleaned hardware, airflow-proven enrichment.
- Annex I lets audited complex facilities replace prescriptive parts of the Code with an engineered risk program (ALARP).
- Food trucks: B51 tanks, vapour withdrawal, QCC1, road-debris protection, accessible shut-offs.
- Hydrogen rules hinge on 66 psi (embrittlement) and 25% blend (detection, scanners, ventilation) thresholds.

## Connects To
- ch10 (Annex M documentation tiers), ch11 Clauses 15/18/19 (start-up, flare pilots, risk program), ch02 (all annex-referenced standards).