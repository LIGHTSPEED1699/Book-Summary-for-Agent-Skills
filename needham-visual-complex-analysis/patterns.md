# Patterns — Visual Complex Analysis (Needham)

Recurring proof and problem-solving moves across the book.

## 1. Reduce to one generator
Decompose a complicated map into simple ones and study only the hard generator. Möbius → translations + dilative rotations + one 1/z (ch3). Any power integral → the circular arc case, then deform (ch8). **Use when:** facing a composite transformation — isolate the nontrivial factor.

## 2. Zoom to the derivative (localize)
Understand a map by its infinitesimal action. Amplitwist (ch4): every analytic map is locally one complex multiplication. Jacobian taxonomy (ch4): equal expansion factors ⟺ CR. **Use when:** asked "is it conformal/analytic?" — check the infinitesimal square or the CR form in adapted coordinates.

## 3. Choose coordinates the geometry begs
CR has four dressings (Cart-Cart, Polar-Cart, Cart-Polar, Polar-Polar). Circles→lines problems use Polar-Cart (∂_θf = ir∂_r f). **Use when:** a computation fights you — the mesh you draw should match the mesh the answer respects (ch5).

## 4. Count, don't compute
Winding numbers, indices, residues convert geometry to arithmetic: N = ν[f(Γ),p] (ch7); ∮ = 2πi Σ ν·Res (ch9); Σ indices = 2−2g (ch10). **Use when:** asked "how many roots / what's the integral / what's the topology" — find the conserved integer.

## 5. Deform invariance
A quantity constant under continuous deformation (avoiding obstacles) depends only on a homotopy class. Cauchy/Deformation theorem (ch8); Hopf degree theorem (ch7); index invariance (ch10); flux/work deformation theorems (ch11). **Use when:** the contour/loop shape is arbitrary — shrink it to the easiest representative.

## 6. Boundary determines interior (rigidity)
Analytic functions are crystals: a curve's image, a circle's average, or boundary values fix everything inside. Rigidity (ch5); Cauchy's formula + Gauss MVT (ch9); maximum principle + Dirichlet (ch12). **Use when:** given partial data — extrapolate via the identity theorem / Poisson, don't re-solve.

## 7. Physics as a proof engine
Translate analysis to flow/force language and let intuition compute. ∮ H dz = work + i·flux of the Pólya field (ch11); Cauchy = Gauss+Stokes (ch11); residues = source/circulation strengths (ch11); Riemann map = matched flow grids (ch12); Green's function = temperature (ch12). **Use when:** an integral or existence proof resists symbols — build the fluid/electrostatic picture.

## 8. Conformal transport
Solve on the easy domain, map back. Harmonicity invariant under conformal maps (Δ scales by |f′|², ch12); flows map to flows (ch12); Poisson disc → half-plane → any region (ch12). **Use when:** the domain is awkward — find the map to the disc/half-plane, solve there, pull back.

## 9. Duality by rotation
Rotate a field by 90° to get a second valid solution with swapped roles (source↔vortex, Φ↔Ψ). Harmonic duals (ch12); conjugate flows (ch12). **Use when:** you have one potential problem solved — the dual is solved for free.

## 10. Multiplicity is one thing in three costumes
Algebraic (first nonzero Taylor term), geometric (image winds n times), topological (local degree) — equal for analytic maps (ch7). **Use when:** roots/branches/poles overlap — count via winding to get multiplicity automatically right.

## 11. The matrix picture classifies the dynamics
Möbius ↔ 2×2 matrices up to scale; fixed points = eigenvectors; multiplier λ₁/λ₂ gives the normal form and the elliptic/hyperbolic/loxodromic/parabolic type (ch3, ch6). **Use when:** iterating or classifying a transformation — diagonalize, read the multiplier.

## 12. Singularities are the whole story
Where a map fails (poles, branch points, critical points, pegs) controls convergence radii, integrals, and topology. Radius = distance to nearest singularity (ch9); residue at the peg (ch8-9); branch points as obstacles (ch2, ch9). **Use when:** a series or integral misbehaves — locate the singularity first.
