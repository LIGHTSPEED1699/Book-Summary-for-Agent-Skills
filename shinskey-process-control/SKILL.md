---
name: shinskey-process-control
description: Reference distill of Shinskey's "Process Control Systems: Application, Design, and Adjustment" — one file per chapter (ch01–ch12, ~8–28k chars each) with the book's core ideas, frameworks, key concepts, mental models, anti-patterns, reference tables of exact numeric results, and worked examples. Use when authoring or auditing process-control teaching material, when you need Shinskey's specific reasoning about loop dynamics (dead time, capacity, self-regulation), controller selection and tuning (P/PI/PID, IAE-first), the five common loops (flow, pressure, level, temperature, composition), nonlinear elements, cascade/selective/adaptive structures, feedforward and dynamic compensation, interaction and decoupling (RGA), energy transfer and conversion (heat transfer, boilers, machines), chemical reactor stability, or pH and endpoint control; or when a claim about feedback control needs a citation to the book's own equations, tables and worked numbers.
---

# Shinskey, Process Control Systems

A chapter-by-chapter distill of Shinskey's *Process Control Systems: Application, Design, and Adjustment*. Each chapter file follows the same shape: **Core Idea**, **Frameworks Introduced** (when to use / how), **Key Concepts** (definitions and formulas), **Mental Models**, **Anti-patterns**, **Reference Tables** (the book's numeric results), and a **Worked Example** using the book's own numbers.

## How to use it

- **Authoring teaching material** (slides, quizzes, classroom outlines): ground claims in the chapter files, not in general control lore. Shinskey's positions are specific and often contrary to textbook consensus — decay ratio is rejected in favour of minimum IAE, "quarter-amplitude decay belongs to the past", and stability is treated as a *design* property (heat-transfer area, feed rate) before it is a tuning problem.
- **Auditing**: check a claim against the chapter's Reference Tables and Worked Example. Numbers in those sections are quoted from the book, so a mismatch is a real finding.
- **Citations**: equation numbers (e.g. "Eq. 10.20", "Table 10.1") are the book's own and are stable across editions; page-level positions are edition-specific.

## Chapters

| File | Chapter | Load it for |
|---|---|---|
| `chapters/ch01-dynamic-elements-in-the-control-loop.md` | 1 Dynamic Elements in the Control Loop | Dead time, capacity (self-regulating vs integrating), dynamic gain/phase, IAE as the objective, tuning rules |
| `chapters/ch02-characteristics-of-real-processes.md` | 2 Characteristics of Real Processes | Process gain and time-constant placement, noise, valve characteristics, rms error addition |
| `chapters/ch03-analysis-of-some-common-loops.md` | 3 Analysis of Some Common Loops | Flow, pressure, level and temperature loops; hydraulic resonance; loop periods; Table 3.3 properties |
| `chapters/ch04-linear-controllers.md` | 4 Linear Controllers | Mode selection and optimum settings, performance criteria, robustness, adjustment procedures, model-based control, sampling/digital control |
| `chapters/ch05-nonlinear-control-elements.md` | 5 Nonlinear Control Elements | Describing functions, limit cycles, dead band, velocity limiting, negative resistance, on-off and dual-mode control, error-squared PIDs |
| `chapters/ch06-improved-control-through-multiple-loops.md` | 6 Improved Control through Multiple Loops | Cascade, multiple outputs, valve-position control, selective control, windup protection, adaptive control (including EXACT) |
| `chapters/ch07-feedforward-control.md` | 7 Feedforward Control | Why feedback fails, steady-state and dynamic compensation, averaging level control, ratio and blending, adding feedback, economics |
| `chapters/ch08-interaction-and-decoupling.md` | 8 Interaction and Decoupling | Relative gain array, pairing, decoupler design and error tolerance, relative disturbance gain, partial decoupling |
| `chapters/ch09-energy-transfer-and-conversion.md` | 9 Energy Transfer and Conversion | Heat transfer and exchangers, phase change, combustion and safety-selective air/fuel, fired heaters, steam plant, drum level (inverse response, shrink/swell), pumps and centrifugal compressor surge |
| `chapters/ch10-controlling-chemical-reactions.md` | 10 Controlling Chemical Reactions | Equilibrium and kinetics, exothermic reactor stability (thermal gain, negative resistance), continuous vs recycle reactors, severity control, pH and endpoint control |
| `chapters/ch11-mass-transfer-operations.md` | 11 Mass-Transfer Operations | Distillation composition control, pressure and level schemes, evaporators, drying |
| `chapters/ch12-batch-process-control.md` | 12 Batch Process Control | Batch sequencing, heat-up/cool-down control, recipe-driven operation, end-point detection |

## Companion files

- `glossary.md` — notation decoded (P/I/D conventions, λ, Kt/τt, γ, ti, α, S, installed characteristic…) plus the book's recurring maxims.
- `patterns.md` — 16 cross-chapter design patterns + 8 diagnosis playbooks (limit-cycle triage by period and waveform, windup signature, inverse response…).
- `cheatsheet.md` — the tuning tables and formulas worth pulling fast (Table 4.4, batch rules, reactor stability squeeze, feedforward compensator settings, RGA rules).

## Provenance and caveats

- Chapter files were distilled from the **3rd-edition** text layer (`Calibre Library/Shinskey, F. Greg/Process-control systems _ application, design, and adjustment (16474)/`, 548 pp), which is also the OpenMAIC grounding source. The plan of record notes the 4th edition as the citation target; chapter structure is identical and equation numbering agrees, but where an audit turns on an edition difference, defer to whichever edition the reader holds open and spot-check the 4th-ed scan.
- **4th-edition scan now extracted** (2026-10-10, PP-OCRv6 via pdf-inspector): `~/.knowledge/shinskey/pi/shinskey4e-pi.md` (229-page two-up scan of the McGraw-Hill 4th ed; raw PDF + sha256 in `~/.knowledge/shinskey/raw/`). Key constants spot-verified against it: I = 1.6Kpτd and P = 250Kp (Ch. 1), τn = 3.94ti (Ch. 9), Eqs. 10.22–10.23 (reactor stability), Eq. 11.19 (column RGA from curve slopes). The damaged `Gn1` passage (Ch. 3, Eq. 3.24 context) is still unrecoverable in this scan.
- **One damaged formula**: in Ch. 3 (level loops, resonant-gain estimate), the first approximation for resonant gain `Gn1` is unrecoverable in both text layers; the second approximation `Gn = Gn1/[1 − 1/(2Gn1)²]` (3.24) and the qualitative rule are intact. Do not quote a value for `Gn1` without the printed page.
- Formula and table values marked in the chapter files are transcribed from the book; treat them as source data, not as independently verified results.
