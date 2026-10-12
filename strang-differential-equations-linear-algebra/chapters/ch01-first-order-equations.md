# Chapter 1: First-Order Equations

## Core Idea
dy/dt = ay + q(t) is the whole first course in one line: the solution splits as y = Yn + Yp — the null (homogeneous) part Ce^{at} carrying the initial condition, and the particular part carrying the source, built by superposition as the integral ∫e^{a(t−s)}q(s)ds. Everything else in the chapter (sinusoids, growth models, logistic, separable equations) elaborates that split or shows where linearity breaks.

## Frameworks Introduced
- **Linear vs nonlinear (1.1)**: linear in y and y′ (variable coefficients allowed, e.g. y′ = 2ty); nonlinear (y²) solutions blow up in finite time.
- **Calculus toolkit (1.2)**: the essential list — e^x as solution of y′=y; sum/product/chain rules; FTC as "sum of differences"; three uses of dy/dx ≈ Δy/Δx (linear approximation, Newton's method, finite differences); centered differences as the first→second order leap; Taylor series.
- **The exponential (1.3)**: e^t = Σtⁿ/n! (each term is the derivative of the next); e^{a+b} = e^a e^b proved two ways from uniqueness; compound interest (1+aΔt)^N → e^{at} — difference equations as discrete twins; Euler's formula e^{it} = cos t + i sin t via the i,-1,-i,1 cycle; preview e^{At} with the warning e^{At}e^{Bt} ≠ e^{(A+B)t} unless AB = BA.
- **Yn + Yp split (1.4)**: complete solution = null solution + particular solution; the picture (parallel affine line through a particular point) that repeats for Ax = b forever after; integrating factor e^{−at} derives Yp = ∫e^{a(t−s)}q(s)ds — input q(s) grows/decays over remaining time t−s (impulse-response thinking).
- **Sinusoids (1.5)**: real and complex sinusoids; cos/sin as even/odd parts of e^{it}; frequency, amplitude, phase.
- **Growth/decay models (1.6)**: data-driven a from two measurements; variation of parameters as the general Yp recipe.
- **Logistic equation (1.7)**: y′ = y − y² (and y′ = ay − by² carrying capacity K = a/b): S-curves, stable/unstable steady states read off the f(y) graph, harvesting h and critical harvesting (double steady state, saddle-node before the term exists), threshold equation backward in time.
- **Separable and exact (1.8)**: dy/f(y) = g(t)dt integrates both sides; exact equations via potential ψ with ψ_t = ..., integrating factor as the rescue.

## Key Concepts
- Superposition: linear equations add, their solutions add — the source integral is a continuum of impulses.
- Steady states Y: solve f(Y) = 0; stability read from the slope df/dY (negative stable, positive unstable) — the graphical dynamics that grows into ch3's phase plane.
- Blowup: nonlinear y′ = y² escapes to ∞ at finite t; linear equations never do.
- Euler's method is compound interest: Y_{n+1} = (1+aΔt)Yn; forward underestimates e^{aΔt}, backward (dividing) overshoots.
- e^{it} unifies oscillation with growth: a = iu gives pure rotation, Re/Im parts give cos/sin.
- Particular solution choice Yp(0) = 0 is a convention, not a requirement — the complete solution is the same affine family.

## Mental Models
- "y = Yn + Yp": initial condition and input are separate accounts; the book's central picture (repeated for Ax = b and y′ = Ay).
- "Input q(s) multiplied by e^{a(t−s)} and summed": the exponential is the growth factor of a remembered impulse — the transfer-function seed of the whole shelf.
- "Graph f(y), find where it crosses zero, check the slope": stability without solving.
- "Discrete mirrors continuous": (1+aΔt)^N ↔ e^{at}; difference equations are the computational twin (and the bank's reality).
- "i, −1, −i, 1 cycling": rotation is what imaginary exponents do.

## Anti-patterns
- **Adding "solutions" for nonlinear equations**: y′ = y + 1 is not solved by e^t + t; superposition is a linearity privilege.
- **Forgetting e^{At}e^{Bt} = e^{(A+B)t} needs AB = BA** (the matrix warning planted here).
- **Trusting Taylor series past its radius**: 1 + x + x² + … = 1/(1−x) only for |x| < 1; blowup at x = 1 shows in the series.
- **Overharvesting blindness**: when 4h > a² the logistic-with-harvest steady states go complex and every solution crashes — the model's cliff edge.
- **Forward-difference accuracy complacency**: first order vs centered second order is "the key step in scientific computing" per Strang.

## Reference Tables
### y′ = ay + q solution anatomy
| Piece | Formula | Carries |
|---|---|---|
| Null Yn | Ce^{at} | initial condition y(0) |
| Particular Yp | ∫₀ᵗ e^{a(t−s)}q(s)ds | the source, Yp(0)=0 |
| Complete | Yn + Yp | everything |

### Stability of steady states (y′ = f(y))
| f(Y) = 0 and | Behavior |
|---|---|
| f′(Y) < 0 | stable (solutions approach) |
| f′(Y) > 0 | unstable |
| double root (critical harvest) | semistable knife-edge |

### Discrete twins
| Continuous | Forward Euler | Backward Euler |
|---|---|---|
| e^{aΔt} | 1 + aΔt (under) | 1/(1 − aΔt) (over) |

## Key Takeaways
Every first-order linear equation splits into null + particular; the particular solution is the superposition integral of the source against the exponential.
Stability is read from the f(y) graph, not from solving.
The exponential, its series, its difference-equation twin, and Euler's formula form the analytic engine for everything after.
Nonlinearity brings S-curves, thresholds, and finite-time blowup — no superposition.

## Connects To
Ch2 doubles the order (characteristic roots replace single a); ch3 generalizes stability to phase planes; ch4-5 replay Yn + Yp as nullspace + particular for Ax = b; ch6 replaces a with matrix A and e^{at} with e^{At}; ch8's convolution is the superposition integral in transform dress. On the control shelf: y′ = ay + q is the first-order plant; the e^{a(t−s)} impulse integral is the convolution/transfer-function foundation of Skogestad and Stengel.
