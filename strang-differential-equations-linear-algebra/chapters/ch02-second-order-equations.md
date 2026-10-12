# Chapter 2: Second-Order Equations

## Core Idea
Ay″ + By′ + Cy = f(t) with constant coefficients is solved by the characteristic polynomial As² + Bs + C: its two roots s1, s2 decide everything — overdamped (real), critical (equal, second solution te^{st}), underdamped (complex a ± iω giving e^{at}(C1cosωt + C2sinωt)). The impulse response g(t) (rest at 0, unit kick) is the fundamental solution: every forced response is the convolution ∫g(t−s)f(s)ds, and its Laplace transform is the transfer function Y(s) — the bridge to frequency-domain thinking.

## Frameworks Introduced
- **Second derivatives in science (2.1)**: mass-spring (my″ + By′ + ky = F), pendulum, circuits — the same equation everywhere; damping B and stiffness k.
- **Complex numbers toolkit (2.2)**: conjugate, modulus, angle; e^{iθ} rotation; complex arithmetic as the language of oscillation.
- **Characteristic equation (2.3)**: y = e^{st} ⟹ As² + Bs + C = 0; discriminant B² − 4AC trichotomy; damping ratio ζ = B/√(4AC) with roots −ζωn ± iωn√(1−ζ²), ωn = √(C/A) — the control-shelf standard form; repeated roots need y2 = te^{st}.
- **Forced oscillations (2.4)**: exponential response e^{st}/P(s) (resonance when P(s) = 0); sinusoidal steady state: input cosωt, output |G(iω)|cos(ωt + phase); undetermined coefficients.
- **Networks and mechanics (2.5)**: impedance Z = iwL + R + 1/(iwC); series/parallel combination mirrors parallel springs; mechanical-electrical dictionary (m↔L, B↔R, k↔1/C, force↔voltage, velocity↔current).
- **Solution methods (2.6)**: undetermined coefficients (guess the form of f); variation of parameters (c1(t)y1 + c2(t)y2, Wronskian integrals); convolution with the fundamental solution g.
- **Laplace preview (2.7)**: Y(s) = transform of g(t) = transfer function; integration ↔ division by s; "calculus in the time domain becomes algebra in the frequency domain"; step response = integral of impulse response.

## Key Concepts
- Stability = roots in the left half-plane (negative real parts); damping ratio ζ < 1 oscillates, ζ > 1 overdamped, ζ = 1 critical.
- The fundamental solution g: Ag″ + Bg′ + Cg = δ(t), g(0) = 0, g′(0) = 1/(A) — one function answers every forcing via convolution.
- Transfer function H(s) = 1/P(s); frequency response H(iω) gives gain and phase — Bode language in embryo.
- Resonance: forcing at a natural frequency (P(iω) = 0 undamped) makes amplitude grow without bound.
- Impedance addition rules: series adds Z, parallel adds 1/Z — exactly the spring combination laws.
- Undetermined coefficients works when f is built from e^{st}, cos, sin, polynomials; resonance case multiplies the guess by t.

## Mental Models
- "Roots decide the story": read the characteristic polynomial, know the time behavior — the shelf's most-used reflex (poles = modes).
- "One g(t) to rule all forcings": impulse response + convolution = the linear-systems worldview; Y(s) = L{g} is its frequency twin.
- "ζ and ωn are the coordinates of second-order behavior": every second-order system in engineering lives at (ζ, ωn).
- "Electrical = mechanical with renamed parts": the impedance dictionary transfers intuition across domains.
- "Frequency domain = algebra domain": differential equations become rational functions of s (fully in 8.5).

## Anti-patterns
- **Missing the te^{st} second solution at repeated roots** — the solution family collapses without it.
- **Undamped resonance at natural frequency** treated as bounded — amplitude grows linearly (or worse).
- **Forgetting the resonance multiply-by-t rule** in undetermined coefficients when the forcing matches a root.
- **Confusing circular frequency ω with frequency f** (ω = 2πf) in the 60 Hz examples.
- **Reading stability from coefficients alone** — check the roots (or for second order: all coefficients same sign is necessary and sufficient).

## Reference Tables
### Characteristic roots → behavior (Ay″+By′+Cy=0)
| Discriminant | Roots | Solution | Name |
|---|---|---|---|
| B² > 4AC | real s1, s2 | c1e^{s1t} + c2e^{s2t} | overdamped |
| B² = 4AC | s = −B/2A | (c1 + c2t)e^{st} | critical |
| B² < 4AC | −ζωn ± iωd | e^{−ζωnt}(C1cosωdt + C2sinωdt) | underdamped |

### Control-shelf dictionary (Strang ↔ Skogestad/Stengel)
| Strang | Shelf term |
|---|---|
| P(s) = As²+Bs+C | characteristic polynomial / denominator |
| roots s1, s2 | poles |
| ζ = B/√(4AC), ωn = √(C/A) | damping ratio, natural frequency |
| g(t) | impulse response |
| Y(s) = 1/P(s) | transfer function |
| ∫g(t−s)f(s)ds | convolution output |
| Z(iω) | frequency response |

## Key Takeaways
The characteristic polynomial's roots are the system's modes; stability is left-half-plane.
The impulse response g and its convolution give every forced response; its transform is the transfer function.
Damping ratio ζ organizes second-order behavior into three regimes.
Impedance and mechanical analogies make the same math portable across physical domains.
Frequency-domain algebra is the payoff of the Laplace viewpoint (completed in 8.5).

## Connects To
Ch3's nonlinear stability linearizes back to these roots; ch6's eigenvalues are the multi-dimensional characteristic roots (stability of y′ = Ay); ch8's Laplace transform and convolution formalize 2.4/2.7. Directly feeds the control shelf: SIMC tuning targets (ζ, ωn)-like closed-loop shapes, Bode plots are |H(iω)|, and transfer-function models in Skogestad are this chapter's Y(s).
