# Chapter 4: Elements of Linear System Theory (new in 2e; state-space machinery consolidated)

## Core Idea
Everything the rest of the book computes — poles, zeros, internal stability, coprime robustness, balanced reduction — is cleanest in state space with **minimal realizations** and direction-aware definitions.

## Frameworks Introduced
- **Minimal realization**: no pole-zero cancellation between (A,B) and (C,A); order = degree of pole polynomial.
  - How: check controllability + observability; uncontrollable or unobservable modes can be removed without changing G(s).
- **Controllability/observability tests (2e version)**: Gramians W_c = ∫e^{At}BBᵀe^{Aᵗt}dt, W_o dual; PBH rank tests [sI−A, B] and [sI−A; C].
  - 2e note: reformulated tests, equivalent to the old ones.
- **Pole polynomial**: least common denominator of all nonzero minors of all orders of G(s); its roots = eigenvalues of A in any minimal realization (Thm 4.8).
- **MIMO zeros**: s = z where rank G(z) < normal rank; input direction u_z (G(z)u_z = 0), output direction y_z (y_zᴴG(z) = 0).
- **Internal stability**: all four transfer maps between the two internal signals stable; ⇔ all proper closed-loop transfers from every internal break stable. External stability is not enough.
- **Stabilizing controllers / Youla Q(s)**: all stabilizing K parametrized by free stable Q; fixes one stabilizing K₀ and sweeps Q.
- **Coprime factorization**: G = N M⁻¹ (right) or M⁻¹N (left); normalized left coprime (M,N) is the currency of the stability-radius robustness test in ch9.

## Key Concepts
- **Hidden modes**: unstable but unobservable → G(s) looks stable, internals blow up; internal stability catches them.
- **Nonminimum phase zeros in state space**: zeros of the invariant zeros of (A,B,C,D); RHP zeros constrain any feedback regardless of structure.
- **Interconnection rule**: series/parallel/feedback of minimal realizations may not be minimal — always check for cancellations after connecting blocks.

## Mental Models
- G(s) is the *external shadow* of (A,B,C,D); internal stability asks about the object casting the shadow.
- Youla: "one stabilizing controller unlocks all of them" — performance tuning happens inside Q without touching stability.
- Coprime view: robustness = distance from G to the set of unstable-plant plants in the gap/metric; normalized coprime factors make that distance computable.

## Anti-patterns
- **Canceling an RHP plant zero with a controller pole**: internally unstable — the canceled mode lives on in one of the four internal maps.
- **Checking only loop transfer L for stability**: external-only; use the four-map test or Youla construction.
- **Pole polynomial from one element g₁₁**: must be the lcm over all minors — element-wise denominators lie in MIMO.

## Key Takeaways
1. Minimality first: every structural claim (poles, zeros, Gramians) assumes it.
2. Poles = roots of pole polynomial of G; zeros = rank drops of G, with directions.
3. Internal stability = all internal maps stable; cancellations of RHP/unstable modes are forbidden.
4. Youla Q + coprime factors are the two algebraic tools ch8–ch9 lean on.

## Connects To
- **Ch 8**: N-Δ form and μ need the internal-map machinery.
- **Ch 9**: normalized coprime factorization → γ_opt stability radius.
- **Ch 11**: Gramians → balanced truncation.
- **Ch 12**: Lyapunov/LMI versions of these tests.
