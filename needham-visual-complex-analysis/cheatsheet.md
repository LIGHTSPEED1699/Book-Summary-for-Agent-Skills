# Cheatsheet — Visual Complex Analysis (Needham)

## Derivative & CR
- f′(q) = amplitwist = |f′|e^{i arg f′}; local map: ξ ↦ f′(q)·ξ.
- CR (Cart-Cart): ∂ₓu = ∂_y v, ∂_y u = −∂ₓv ⟺ i∂ₓf = ∂_y f.
- f′ = ∂ₓf = −i∂_y f = e^{−iθ}∂_r f = −(i/z)∂_θ f.
- CR (Polar-Cart): ∂_θf = ir∂_r f.
- Analytic ⟺ Jacobian = [[a,−b],[b,a]] (complex multiplication); area magnification = |f′|².
- Critical point f′=0 (order k): angles ×(k+1). Branch point z^{1/n}: angles ×1/n.

## Möbius & inversion
- M(z)=(az+b)/(cz+d), ad−bc≠0; M(∞)=a/c, M(−d/c)=∞.
- Inversion in circle (centre q, radius R): z ↦ q + R²/(z̄−q̄); anticonformal; complex inversion 1/z conformal.
- Inversion preserves: generalized circles, angle magnitudes, symmetry pairs.
- Matrix class (multiplier k=λ₁/λ₂): elliptic |k|=1; hyperbolic k∈ℝ⁺; loxodromic general; parabolic k=1.
- Cross-ratio [z,a,b,c]=((z−a)(b−c))/((z−b)(c−a)); M fixed by images of 3 points.
- Disc automorphism (hyperbolic motion): (az+b)/(b̄z+ā). Sphere rotation: (az+b)/(−b̄z+ā).
- Hyperbolic distance: (R/2)·|log cross-ratio w.r.t. ideal endpoints|.

## Winding & topology
- ν(L,p) = net CCW revolutions of (z−p); constant on each region; crossing rule: cross L left→right ⇒ ν+1.
- Hopf: K ≃ L (avoiding p) ⟺ ν equal. Archetype z^ν.
- Argument Principle: N = ν[f(Γ),p] (analytic, with multiplicity).
- Rouché: |f−g|<|g| on Γ ⇒ same zero count inside. FTA: degree-n poly has n roots.
- Multiplicity: algebraic = geometric winding = topological degree (analytic ⇒ >0).
- Index of field V: ν_V[Γ]=ν[V(Γ),0]; root order n→n, pole order m→−m; Poincaré recipe ν=P−N.
- Index Theorem: ν[C] − Σν[Bⱼ] = Σν[sⱼ]. Poincaré-Hopf: Σ indices = 2−2g = χ.

## Integration & residues
- ∮ z̄ dz = 2i·(signed area) = 2i Σ νⱼAⱼ.
- ∮ z^m dz = 0 (m≠−1, any loop); ∮ dz/z = 2πi ν(C,0).
- Cauchy: analytic between paths ⇒ equal integrals; loop integral of analytic = 0.
- Deformation: drag contour through analytic points ⇒ value fixed.
- Cauchy formula: f(a)=(1/2πi)∮f(z)/(z−a)dz; general loop ⇒ ν[L,a]f(a).
- Gauss MVT: ⟨f⟩_circle = f(centre); harmonic functions too.
- f⁽ⁿ⁾(a) = (n!/2πi)∮ f(z)/(z−a)ⁿ⁺¹ dz.
- Taylor radius = distance to nearest singularity/branch point.
- Residue (order m): (1/(m−1)!)·[d^{m−1}/dz^{m−1}((z−a)^m f)]_{z=a}; simple pole P/Q: P(a)/Q′(a).
- Residue Theorem: ∮ f dz = 2πi Σ ν[L,aₙ] Res[f,aₙ].
- Real ∫_{−∞}^{∞}: close in half-plane where arc dies; = 2πi Σ upper residues.

## Vector fields & physics
- Pólya field of H: draw H̄ at z. ∮ H dz = W[H̄,K] + i F[H̄,K] (work + i·flux).
- H analytic ⟺ div H̄ = 0 and curl H̄ = 0 (CR in vector form).
- Flux F=∫(X·N)ds; work/circulation W=∫(X·T)ds; div=flux density, curl=work density (ω=2 curl).
- Gauss: ∮ X·N ds = ∫∫ div X dA; Stokes: ∮ X·T ds = ∫∫ curl X dA.
- Source strength S: V=S/(2π z̄)-type; flux across loop = S. Doublet = source+sink.

## Flows, harmonic, mapping
- Complex potential Ω=Φ+iΨ; dual Ĥ=iH swaps Φ↔Ψ (Φ̂=Ψ, Ψ̂=−Φ).
- Harmonic dual recipe: Ω′(z)=∇Φ(z,0) (evaluate on real axis, x→z).
- Laplacian meaning: ⟨Φ⟩_r − Φ(p) = (r²/4)ΔΦ; harmonic ⇒ circle balance.
- Conformal invariance: ΔΦ(z) = |f′(z)|² ΔΦ̃(f(z)); harmonicity preserved.
- ∂̄ calculus (Needham ∇): ∇̄f=0 ⟺ analytic; ∇f=2f′; Δ=∇∇̄; ∮f dz = i∫∫∇̄f dA.
- Riemann map: match flow grids; 3 dof = dipole position p (f(p)=0) + direction φ (arg f′(p)); |f′(p)|=dipole strength in disc.
- Green's function: G_p=−ln|f| (f:R→D, f(p)=0); G_p(q)=G_q(p); boundary flux Q=|f′|.
- Poisson (disc): T(re^{iθ})=(1/2π)∫T(φ)(1−r²)/(1−2r cos(θ−φ)+r²)dφ.

## Series
- Taylor: Σ f⁽ⁿ⁾(a)/n! (z−a)ⁿ (analytic disc).
- Laurent at pole order m: finitely many negative powers; residue = c₋₁.
- e^z entire; log z = ln|z| + i arg z (multivalued, +2πi n).
