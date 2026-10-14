# Ch5 — Computing Machines and the Nervous System

## Why binary wins (a cost argument, not a convention)
- Recording I bits on one accurate scale costs ∝ A·2^(I/1); split over N scales, cost ≈ A·N·2^(I/N), minimized as N→∞ with each scale carrying the least significant choice: **2 levels per scale = binary**. Decimal is "the historical accident of our fingers and thumbs."
- Analogy machines (Bush differential analyzer: continuous scales) vs numerical machines (choices among contingencies): for high accuracy, numerical — binary — wins; accuracy is set by how sharply alternatives are distinguished, not by scale craftsmanship.
- Keep humans at the ends of a computation only: "it is the slowest which gives the order of magnitude of the time constants of the entire system."

## The logical machine
- All data and all rules as choices between two alternatives; operations = new choices as functions of old: **the algebra of logic par excellence (Boolean)** — negation, logical addition, logical multiplication; binary arithmetic's multiplication table is logical multiplication.
- Machine = bank of two-state relays (mechanical, solenoid, gas tube, vacuum tube; stable-bistable or one-stable-plus-transient), clocked or ripple-clocked.

## The neuron as relay
- Neurons obey the **all-or-none** principle: rest → firing (stereotyped impulse at fixed conduction velocity) → **refractory period** (absolute then effective) → ready. Two-state device.
- Synapses: hundreds of inputs; firing iff enough fire within a **fusion interval** exceeding a threshold, after fixed synaptic delay; **inhibitory synapses** raise/block the threshold; weights and geometry matter; humoral influences act as slow secular parameter changes.
- Nervous system = the same relay-bank architecture, hence the computing-machine analogy is structural, not poetic.

## Memory taxonomy (brain ≠ machine, brain = one run of a machine)
- Working memory for the current process (fast write/read/erase) vs permanent file memory.
- Short-time memory by **closed reverberating circuit** — impulse circling until cleared; the physiological "specious present." Delay-line engineering: elastic vibrations preferred over light/electrical delay (cumulative distortion); **reshape/regenerate the impulse before blur accumulates**.
- Key asymmetry: the machine is cleared between runs; **"the brain, in the course of nature, never even approximately clears out its past records."** The brain is the analogue of a single run of a machine — this becomes the key to psychopathology in Ch7.

## Redundancy and error strategy ("What I tell you three times is true")
- A 10⁹-step computation makes component failure near-certain; step-by-step checking at machine speed is too costly (bulk factor ≫2–3).
- Better: run every operation on **two or three separate mechanisms**; two-way collation stops on discrepancy and dumps state to permanent storage; **three-way majority voting keeps running** and pinpoints the minority report.
- Spare-element organization: no element assigned to a stage; a searching process (like automatic telephone exchanges) grabs the first available element of a kind → defective parts replaced without delay.
- Wiener's guess for the brain: important messages never ride a single neuron or single mechanism; messages leave a level via alternative members of an **"internuncial pool"**; interchangeability highest in unspecialized association cortex, lowest in primary sensory cortex.

## Practitioner takeaways
- Cost-of-accuracy math justifies digital over analog at high precision — same argument underlies today's ADCs, digital control, and bit-level redundancy.
- Design for component failure with majority voting + hot spares, not per-step audit.
- Regenerate signals at intervals in any delay/storage medium.
- When modeling an adaptive system that never resets (agents, organizations), model it as a single continuous run — past state is never zero, so early states constrain late behavior (Ch7's vicious circles).
