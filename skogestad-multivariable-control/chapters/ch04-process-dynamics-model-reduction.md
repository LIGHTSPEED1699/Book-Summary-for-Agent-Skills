# Chapter 4: Dynamics of Process Plants and Model Reduction

## Core Idea
Get the model's *structure* right — poles, zeros (with directions), delays — because control limitations are properties of these objects; reduce everything else, but never reduce away delays, RHP zeros, or dynamics near the crossover frequency.

## Frameworks Introduced
- **Pole polynomial via minors (Theorem 4.8, MacFarlane-Karcanias)**: the pole polynomial of a minimal realization = least common denominator of ALL non-identically-zero minors of ALL orders of G(s) (after canceling common factors in each minor). Works for hand calculation and for plants with delays/improper elements that have no state-space form.
- **MIMO zeros with directions**: p is a zero of G(s) if rank G(p) < normal rank; the input direction u_z that produces zero output (Gu_z(p) = 0) and output direction y_z are part of the zero. Poles and zeros at the same location do NOT cancel unless their directions match. det G(s) alone is a crude detector (misses pole/zero pairs in different directions; e.g. G with det = 1 but real poles AND zeros at −1, −2).
- **System norms as performance answers** ("given allowed inputs, how big can outputs get?"):
  - **H2**: strictly proper required; = √(Σᵢ‖impulse response from input i‖²) = √tr(CPCᵀ) via controllability Gramian P (Lyapunov AP + PAᵀ + BBᵀ = 0); stochastic meaning: rms output to white noise (LQG cost).
  - **H∞**: peak of σ̄(G(jω)); = worst-case 2-norm amplification (induced norm); the norm behind weighted sensitivity specs; time-domain meaning: worst steady-state sinusoidal gain.
  - **Hankel**: Γ = spectral radius √(ρ(PQ)) = max Hankel singular value (HSVA); "swing pumping" picture: best energy transfer from past input to future output; norm of best stable approximation; used for balanced truncation.
- **Balanced truncation (preview, full in Ch 11)**: balance controllability/observability Gramians (P = Q = diag(σ_i)), truncate states with small Hankel singular values; error bound ‖G − G_r‖∞ ≤ 2 Σ(truncated σ_i).
- **Delay handling**: e^{−θs} is nonrational, infinite-dimensional; approximate with Padé for analysis (Pade(2) example: adds RHP zero at 6/θ — a modeling artifact, not physics); for control limits treat delay directly (phase −ωθ).
- **Internal stability (4.8)**: a controller is internally stabilizing iff no unstable pole-zero cancellations between G and K and the closed loop is well-posed and stable; improper G needs care (properness of K).

## Key Concepts
- **Self-regulating vs integrating processes**: most processes self-regulate (gain k = dy_ss/du); integrating processes (level, batch composition) have pole at 0; the gain k still matters for controllability (Ch 6).
- **Minimal realization**: no uncontrollable/unobservable states; pole count from A-matrix only valid if minimal (naive combination of 5 second-order elements gave 15 states where 4 suffice).
- **Normal rank**: rank of G(s) for almost all s; zeros defined relative to it.
- **Interlacing of poles/zeros (SISO)**: real RHP zero z and pole p constrain achievable shapes (all-pass factor (z−s)/(z+s)).
- **Hankel singular values (HSV)**: σ_i(PQ)^½; energy relevance of each state; the reduction currency.
- **Residue/direction data**: for reduced models keep gain, delay, and RHP zero/pole locations near ω_c; drop fast LHP poles/lags into delay or ignore.

## Mental Models
- "Count poles/zeros from minors, not from det" — det hides directional cancellations in MIMO.
- "A zero is a location AND a pair of directions" — before worrying about a zero, check whether the control directions actually excite it.
- "Reduce lags into delay, never delay into nothing" — a cluster of small lags near the input can be lumped as extra delay; delays and RHP zeros near ω_c must survive reduction.
- "Pick the norm to match the question": impulse-energy performance → H2; worst-case sinusoid/robustness → H∞; state-reduction energy → Hankel.

## Anti-patterns
- **Canceling a pole-zero pair at the same s in MIMO without checking directions** — they don't interact if directions differ.
- **Using a high-order Padé of a delay as if physical** — its RHP zeros are artifacts; they can mislead RGA/zero analysis.
- **Balanced-truncating away slow-but-weak states blindly** — Hankel values weight energy, not control relevance; a "small-σ" state can carry an integrating mode or RHP zero that dominates loop limits.
- **Non-minimal realizations feeding pole computations** — spurious poles pollute analysis (always minimal first).

## Reference Tables

### Which norm when
| Question | Norm | Formula (state-space) | Requires |
|---|---|---|---|
| rms output to white noise / impulse energy | H2 | √tr(CPCᵀ), AP+PAᵀ+BBᵀ=0 | strictly proper |
| worst-case gain (sinusoid, any freq) | H∞ | max_ω σ̄(G(jω)) | proper, stable |
| state energy / reduction | Hankel | √ρ(PQ) | stable, proper |

### Model reduction checklist (process plants)
| Keep | Why |
|---|---|
| All time delays | phase at ω_c; ω_c < 1/θ limit |
| RHP zeros (location + directions) | ω_c < z/2 limit; RGA fragility |
| Integrating poles | structural (level/mass balance) |
| Steady-state gain matrix G(0) + directions | Ch 5-6 controllability analysis |
| LHP poles/zeros near ω_c | shape of S/T near crossover |
| Drop | fast LHP lags ≫ ω_c (lump into delay), high-frequency resonances unless they excite uncertainty weights |

## Key Takeaways
1. Poles = eigenvalues of A (minimal realization) or LCD of all minors of G(s); zeros = rank drops of G(s) with input/output directions attached.
2. MIMO pole-zero "cancellations" at the same location are harmless iff directions differ — check before reducing.
3. H2/H∞/Hankel answer different performance questions; H∞ is the book's workhorse because weights turn specs into ‖·‖∞ < 1.
4. Hankel singular values rank states by energy; balanced truncation error ≤ 2Σ(dropped HSVs).
5. Delays: keep them explicit for control analysis; Padé RHP zeros are artifacts.
6. A good reduced model for control = gain + delay + RHP zeros + integrators + dynamics near ω_c, nothing else.

## Connects To
- **Ch 3**: σ̄/σ̲ and directions used everywhere here; H∞ weights from Ch 2-3.
- **Ch 5-6**: RHP zeros/delays/integrators become the controllability limits.
- **Ch 11**: balanced truncation / balanced residualization / optimal Hankel norm approximation in full.
- **Appendix A**: Gramians, Lyapunov equations, spectral radius facts.
