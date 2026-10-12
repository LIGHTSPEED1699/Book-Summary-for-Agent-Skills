# Chapter 10: Modeling and Identification of Physical Systems

## Core Idea
Theory meets apparatus: three laboratory systems — magnetic levitation, two-tank process control, and a mechatronic system — get first-principles models (nonlinear physics → linearization around an operating point), then the closed-loop identification machinery of ch7-8 is run on real input-output data from the running (feedback-stabilized) rigs. The unstable magnetic levitation plant is the stress test: it cannot be identified open-loop because it cannot be run open-loop.

## Frameworks Introduced
- **Physical (gray-box) modeling workflow (10.2-10.4)**: Newton/continuity laws → nonlinear model → linearize at the operating point (incremental variables x = X − X₀, v = V − V₀) → transfer function with physically meaningful coefficients (a_mc0, b_mc0).
- **Magnetic levitation case**: electromagnetic force ∝ V²/X²; linearized plant has real poles symmetric about the imaginary axis — intrinsically unstable; must operate closed loop (phase-lead controller + amplifier).
- **Two-tank process**: interacting/noninteracting tank dynamics (process-control standard); slow, integrating-ish dynamics, disturbance-sensitive.
- **Mechatronic system**: motor-driven dynamics with position feedback.
- **Closed-loop identification on real data**: the ch8 scheme applied to each rig; model validation against held-out loop data.
- **Model hierarchy discipline**: physics gives structure and parameter meaning; identification refines the coefficients; discrepancy localizes unmodeled effects.

## Key Concepts
- Unstable plants force closed-loop identification — the practical reason ch8 exists.
- Linearization is a modeling act: incremental variables around (X₀, V₀); accuracy is local by construction.
- Physical parameters make identification diagnostics meaningful (a coefficient drifting = a physical change).
- Real data bring colored noise, sensor dynamics, actuator saturation — the ch7 residual-analysis and ch8 loop handling are not optional.
- The three rigs span the application range: fast unstable (maglev), slow process (tanks), servo (mechatronic).

## Mental Models
- "Physics proposes, identification adjusts": gray-box structure + LS/PEM coefficients.
- "Unstable means closed loop": if the plant can't stand alone, its data are loop data by necessity.
- "Operating point is part of the model": linear models are local; changing the point changes a_mc0, b_mc0.
- "Case studies are regression tests": each rig tests the whole pipeline, not one chapter.

## Anti-patterns
- **Identifying an unstable plant open-loop** — impossible in practice; use the closed-loop scheme.
- **Linear-model confidence far from the operating point** — nonlinearity (V²/X²) grows fast.
- **Treating rig data as clean** — sensor/actuator dynamics belong in the integrated model (ch1).

## Key Takeaways
Gray-box modeling + closed-loop identification is the working recipe for real physical systems.
The three rigs validate the book's pipeline end to end and set up ch11-13's diagnosis/soft-sensor applications.

## Connects To
ch1's integrated model, ch7's methods, ch8's closed-loop scheme; ch11 diagnoses faults on these rigs; ch13's fault-tolerant control runs on the velocity/motor system.
