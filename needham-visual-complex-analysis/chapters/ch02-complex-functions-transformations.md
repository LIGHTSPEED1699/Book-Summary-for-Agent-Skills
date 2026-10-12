# Chapter 2: Complex Functions as Transformations

## Core Idea
Stop plotting complex functions as graphs — view them as mappings of one plane onto another: z → w. Under this lens polynomials multiply angles and raise moduli (zⁿ: n-gon preimages), the mystery of real radii of convergence dissolves (radius = distance to nearest COMPLEX singularity — the ±i volcanoes behind 1/(1+x²)), and Taylor and Fourier series are revealed as two slices of one complex power series. The chapter's tools: modular surfaces, discs of convergence, the identity theorem, and the exponential mapping z → e^z wrapping horizontal strips onto the punctured plane.

## Frameworks Introduced
- **Mapping viewpoint (II.1)**: w = zⁿ sends r e^{iθ} → rⁿ e^{inθ}; solving zⁿ = c = preimages of one point = regular n-gon (particle orbiting n times faster argument).
- **Cubics revisited (II.2)**: Cardano and Viète are the same formula — s³, t³ conjugates on circle radius p√p; the st = p constraint pairs conjugate cube roots; x = s + s̄ = 2√p cos((φ+2mπ)/3).
- **Cassinian curves (II.3)**: loci r₁·r₂ = const (product of distances to foci) = preimages of circles |w| = k² under Q(z) = (z−a₁)(z−a₂); lemniscate = figure-eight at the critical value; modular surface contour maps; n-foci Cassinians from degree-n polynomials; spiric sections of Perseus.
- **Power series (III)**: the real mystery (1/(1+x²) diverging at ±1 with no visible real singularity) solved by complex singularities at ±i; Abel's disc of convergence (converge inside a circle, diverge outside, ring-of-doubt bisection); uniform convergence on closed sub-discs; identity theorem/uniqueness (agreement on any curve segment or sequence with a limit point forces identical series); manipulation rules (add/multiply/divide as polynomials); ratio/root tests; R = distance to nearest singularity.
- **Fourier series as slices (III.7)**: Taylor and Fourier series are the same complex power series read along rays (r varies, θ fixed = Taylor) and around circles (θ varies, r fixed = Fourier); Fourier coefficients by algebra instead of tricky integrals; hints that differentiation and integration are secretly connected (Cauchy's payoff in ch8-9).
- **The exponential (IV)**: e^z = Σz^j/j! (everywhere convergent); e^{a+b} = e^a e^b by series multiplication; e^{x+iy} = e^x e^{iy}; geometry: horizontal lines → circles, vertical lines → rays, strips of height 2π → whole punctured plane, general lines → logarithmic spirals, period 2πi; alternative definition e^z = lim (1 + z/n)ⁿ (compound-interest twin).
- **Multifunctions (V-VI)**: periodicity of e^z ⟹ its inverse log z is infinitely many-valued (differ by 2πi); log z = ln|z| + i arg z; branch points at 0 and ∞; the Riemann surface of log as a helicoid (scaffolding for ch13); roots and powers as finite multifunctions; single-valuedness on restricted domains.

## Key Concepts
- Preimage counting: zⁿ = c has n solutions because the map wraps the circle n times — winding in embryo.
- Radius of convergence is governed by complex singularities even for real functions: "results about real functions trying to tell us about the complex plane."
- Identity theorem: a power series is determined by its values on any tiny arc — analytic rigidity, the seed of analytic continuation.
- Modular surface |f(z)|: cone-legs at roots, volcanoes at poles, contour lines = Cassinians; geometry of a function as terrain.
- e^z maps the plane onto C∖{0} infinitely often; strips of height 2π are fundamental domains; the imaginary axis wraps the unit circle (Euler again).
- Inverse of a many-to-one map is a multifunction: log z has one value per 2π of argument; branch points are where sheets meet.
- Fourier ↔ Taylor unity: one complex series, two real readings — and the coefficient recipes (differentiation vs integration) foreshadow Cauchy's formula.

## Mental Models
- "Function = transformation of the plane": ask what curves map to what curves, not what the graph looks like.
- "Convergence discs are singularity shadows": the nearest complex volcano sets the radius; real analysis alone is a flatland mystery.
- "Slice a complex series two ways": along a ray you get Taylor, around a circle you get Fourier.
- "e^z unrolls strips onto punctured planes; log coils surfaces into helicoids": periodicity and multivaluedness are two sides of one fact.
- "Count preimages by wrapping": n-gons from zⁿ, infinite log values from 2πi-periodicity — winding numbers everywhere.

## Anti-patterns
- **Judging convergence from the real graph** — 1/(1+x²) looks innocent on the real line; its ±i singularities control everything.
- **Treating Cardano and Viète as different methods** — same cube roots, different pairings.
- **Assuming a function agreeing with a real function on the real line is determined** — only power-series-ness (analyticity) buys uniqueness (identity theorem).
- **Forgetting log's branch structure** — arg z is multi-valued mod 2π; a "single" log requires choosing a sheet.
- **Uniform convergence sloppiness** — pointwise on the open disc, uniform only on closed sub-discs; error can blow up near the circle of convergence.

## Reference Tables
### e^z mapping dictionary
| In z-plane | In w-plane |
|---|---|
| horizontal line Im z = c | circle \|w\| = e^c |
| vertical line Re z = c | ray arg w = c |
| strip height 2π | whole plane minus 0 |
| general line | logarithmic spiral |
| small squares | near-squares (angle-preserving, ch4) |

### Series slice table
| Reading of Σ c_j z^j | Result |
|---|---|
| z = r e^{iθ}, θ fixed | Taylor series in r |
| z = r e^{iθ}, r fixed | Fourier series in θ |

## Key Takeaways
Complex functions are plane transformations; solve equations by counting preimages under wrappings.
The true reason power series stop converging is complex singularities — the real line is a shadow.
Taylor and Fourier series are one object seen along rays and circles.
e^z is the prototype: entire, periodic (2πi), strip-to-plane covering, inverse = infinitely valued log on a helicoid.
Uniqueness (identity theorem) makes analytic functions rigid — the theme that pays off in Cauchy's theorems.

## Connects To
Ch3's Möbius transformations are the next mapping family (and stereographic coordinates); ch4's amplitwist explains why e^z maps squares to near-squares (conformality); ch7's winding numbers formalize the preimage-counting here; ch8-9's Cauchy theory explains the differentiation/integration duality glimpsed in Fourier slices; ch11's Laurent series and ch13's Riemann surfaces complete the multifunction story. Strang's Laplace transform and Hubbard's exp map are engineering/calculus cousins of the same e^z geometry.
