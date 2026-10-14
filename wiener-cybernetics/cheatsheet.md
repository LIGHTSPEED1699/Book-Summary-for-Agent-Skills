# Cheatsheet — Cybernetics (Wiener)

## Formulas
- Information: I = −Σ p_i log₂ p_i bits; continuous: −∫ p log p dx; entropy S = −k∫p log p dΓ; information = −ΔS.
- Causal LTI operator: φ(t) = ∫₀^∞ a(τ) f(t−τ) dτ; eigenfunction e^{zt} → A(z); feedback: A/(1+λA).
- Stability: −1/λ exterior of A(iy) curve = stable; interior = increasing oscillation; boundary = sustained. Incipient frequency = rightmost boundary point on negative real axis.
- Load sensitivity: (dA/A) → (dA/A)/(1+λA).
- Autocorrelation: φ(τ) = lim_{T→∞} (1/2T)∫_{-T}^{T} f(t+τ)f*(t) dt; power spectrum = Fourier transform of φ (Wiener–Khinchin).
- Binary recording cost: one scale ∝ A·2^I; N scales ∝ A·N·2^{I/N} → minimized per-bit by 2-level scales.
- Multi-stage reliability: p = q^n (n stages, per-stage q); 0.75 over 5 stages → need q ≈ 0.946.
- Spectrum sampling error: RMS ≈ sqrt(2B/A) relative units (B = autocorrelation cutoff time, A = record length).
- Chess minimax sketch (1948): expand n moves, static valuation (mate ≫ pieces ≫ mobility/development), back up max–min, play the max.

## Stability table (open-loop operator → max feedback λ)
| A(z) | curve A(iy) | feedback limit |
|---|---|---|
| z (pure differentiator) | imaginary axis | unlimited |
| 1/(1+kz) | circle |∣½, r=½ | unlimited |
| 1/(1+kz)² | cardioid-ish | unlimited |
| 1/(1+kz)³ | 3-lobed, encloses −⅛ | λ < 1/8 |
| e^{−Tz} (pure delay) | unit circle | λ ≤ 1 |
| kz³ (ship steering) | left-half interior | **none stabilizes**; add inner loop → k₁z²+k₂z |

## Numbers & exemplars
- Clonus: predicted 13.9/s from neuromuscular-arc conduction times vs observed 12–17 (range 7–30) — servo hunting-frequency math on a nerve arc.
- Body homeostasis: temperature ±0.5°C; slow feedbacks via non-myelinated fibers + hormones.
- Samuel's checkers machine beats its programmer after 10–20 operating hours (1959-61).
- Cortical area ratio sight:sound ≈ 100:1 → sensory substitution bandwidth ~1% of vision.
- Alpha rhythm ~10 Hz; sharp power drop at 9.05 Hz; gating delays ~1/10 s (Lindsley); circadian 23.5 h entrained to 24 h.
- Fusion interval: coincident synaptic arrival within ~0.01–0.1 s decides firing (gating window).
- 10⁹-step computations make single component failure near-certain → majority voting + spare search.

## Diagnostic signatures
- Overshoot-and-correct behavior → feedback loop present (find the criterion signal).
- Non-sinusoidal steady oscillation → non-linear (relaxation) oscillator, determinate amplitude.
- Tremor only at rest → postural loop (brain stem); tremor only in task → servo loop (cerebellum).
- Sudden total failure after invisible degradation → p^(1/n) compounding cliff.
- Spectral clumps with adjacent gaps → coupled oscillators with frequency attraction.
- Response latency = constant + two uniform ~0.1 s parts → clocked gating.

## Wiener's one-liners worth quoting
- "For effective action, it is not enough that we possess good effectors; the performance of these effectors must be properly monitored back."
- "The information about the past does not enable us to compute the present and future unless we know something about the statistical structure of the ensemble."
- "The brain is not the complete analogue of the computing machine but rather the analogue of a single run on such a machine."
- "What I tell you three times is true" (majority-vote redundancy).
- "The State is stupider than most of its components."
- Social science: "never good to more than a very few decimal places."
- "A learning machine operates by non-linear feedback."
- "If we ask for victory and do not know what we mean by it, we shall find the ghost knocking at our door."
