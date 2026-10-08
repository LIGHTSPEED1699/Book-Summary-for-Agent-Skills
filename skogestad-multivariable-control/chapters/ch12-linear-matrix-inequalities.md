# Chapter 12: Linear Matrix Inequalities (brand new in 2e; Turner & Herrmann)

## Core Idea
A huge class of control analysis/synthesis problems — stability, H∞, μ upper bounds, multi-objective design — reduce to **convex feasibility in a matrix variable**: find x such that F(x) = F₀ + Σ xᵢFᵢ ≺ 0 (Hermitian). Convex ⇒ reliable numerical solvers, no local minima.

## Frameworks Introduced
- **LMI**: F(x) = F₀ + Σᵢ XᵢGᵢHᵢ < 0; the unknowns x (or matrix variable X) enter affinely.
  - How: express the requirement as an affine Hermitian matrix inequality; hand to an LMI solver; feasibility or a certificate of infeasibility.
- **Systems of LMIs**: several inequalities F₁(X) ≺ 0, …, F_k(X) ≺ 0 simultaneously — still convex; conjunctions of design specs become one problem.
- **Standard equivalences used constantly**:
  - Lyapunov stability: ∃P ≻ 0: AᴴP + PA ≺ 0.
  - Bounded real / H∞ norm ‖G‖∞ < γ: LMI in P (no frequency grid).
  - Schur complement: [A B; Bᴴ C] ≺ 0 ⇔ C ≺ 0 and A − BC⁻¹Bᴴ ≺ 0 — the workhorse for turning rational conditions into LMIs.
- **Hermitian block tricks**: complex Q = Q_re + jQ_im positive-definiteness expanded to real block form (Exercise 12.1).

## Key Concepts
- **Convexity is the point**: unlike μ lower bounds or D-K (local minima), an LMI problem has no local minima; infeasibility is a proof, not a failed search.
- **Analysis LMIs vs synthesis LMIs**: analysis (fixed controller) is directly convex; synthesis (controller entries as unknowns) is bilinear — linearize via change of variables (e.g., Y = KX for state feedback) or use the Youla/Q parametrization to stay convex.
- **Bilinear matrix inequalities (BMIs)**: what you get when controller and Lyapunov variables multiply; not convex — handled by iteration/fixing one side (the D-K flavor).
- **LMI form of μ upper bound**: the D-scaling condition sup_ω σ̄(DND⁻¹) < 1 becomes an LMI in the D variables at fixed frequency grid — connects this chapter to ch8's machinery.

## Mental Models
- Think "satisfiability with matrices": each spec is one affine slab; the intersection either has a point or an LMI dual proves it doesn't.
- When a problem is convex in the *closed-loop* data but bilinear in the *controller*, change variables (Y = KX, or Q in Youla) before reaching for a BMI solver.

## Anti-patterns
- **Grid-free claims from frequency-sampled μ**: LMI versions avoid frequency grids for the bounded-real step; don't reintroduce grids where the LMI handles them.
- **Feeding BMIs to LMI solvers**: solvers only accept affine inequalities; a bilinear product must be linearized, fixed, or iterated — and then convexity guarantees are gone.
- **Ignoring numerical conditioning**: high-order plants + tight γ make LMIs ill-conditioned; balance/reduce (ch11) before solving.

## Key Takeaways
1. LMI = affine Hermitian matrix inequality; convex; solver-grade.
2. Lyapunov, bounded-real, Schur complement are the three rewriting rules that get you there.
3. Analysis is convex; synthesis needs a variable change (Y = KX / Youla Q) or becomes a BMI.
4. This chapter is the computational backend for ch8 (μ/D-scaling) and ch9 (H∞ synthesis) claims.

## Connects To
- **Ch 4**: Lyapunov/coprime machinery supplies the inequalities.
- **Ch 8**: D-scaling μ upper bounds as LMIs.
- **Ch 9**: H∞ state-feedback/filter synthesis solved as coupled LMIs.
- **Ch 11**: reduction keeps LMI problems well-conditioned.
