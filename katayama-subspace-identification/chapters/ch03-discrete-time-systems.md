# Chapter 3: Discrete-Time Linear Systems

## Core Idea
Discrete-time LTI systems have three equivalent faces — impulse response/convolution, transfer function (Z-transform), and state-space — and realization theory converts between them. The state-space order that realizes a given transfer function is pinned down by reachability and observability; the minimal one is read off the Hankel matrix (matrix version of Lemma 2.14), balanced by equalizing controllability/observability Gramians, and reduced by truncating small balanced modes. This is the deterministic half of the machinery subspace identification will run on data.

## Frameworks Introduced
- **Z-transform (3.1)**: one-sided and two-sided; radius/annulus of convergence; inversion by contour integral = sum of residues at poles; properties: linearity, time shift (one-sided picks up initial-condition terms), convolution → product, partial sums, differences.
- **LTI systems & convolution (3.2)**: output = impulse response ∗ input; transfer function = Z(impulse response).
- **Stability (3.3)**: BIBO ⟺ absolutely summable impulse response ⟺ poles inside unit circle; exponential stability of A ⟺ spectral radius < 1.
- **Signal/system norms (3.4)**: ℓ₂ signal norm; H∞/H₂ system norms (energy and peak gain).
- **State-space & Lyapunov (3.5-3.6)**: x(t+1) = Ax(t) + Bu(t), y(t) = Cx(t) + Du(t); stability via Lyapunov equation AᵀPA − P = −Q; positive-real-type lemmas used throughout the book.
- **Reachability & observability (3.7)**: reachability matrix [B AB … A^{n−1}B], observability [C; CA; …]; rank conditions; Gramians WR = Σ A^k BBᵀA^kT, WO = Σ A^kT CC A^k solve discrete Lyapunov equations; reachable/observable canonical forms.
- **Balanced realization & model reduction (3.8)**: coordinate where WR = WO = diag(σᵢ); balanced truncation drops small σᵢ with H∞ error bound = sum of discarded σ.
- **Realization theory (3.9)**: matrix Hankel built from Markov parameters D, CA^k B; rank n ⟺ minimal realization of order n; Ho-Kalman algorithm extracts (A,B,C) from rank factorization of the Hankel matrix.

## Key Concepts
- Markov parameters: g₀ = D, g_k = CA^{k−1}B — the entries of the Hankel matrix and the bridge from frequency/impulse data to state-space.
- Minimal realization = reachable + observable; any non-minimal one has redundant states (unreachable or unobservable subspace).
- Similarity transforms x → Tx preserve input-output behavior; realization is unique only up to similarity — hence subspace methods need no canonical parametrization.
- Balanced truncation is near-optimal reduction; the Hankel singular values σᵢ are the "energy" of each mode.
- Cayley-Hamilton makes the Markov sequence satisfy the characteristic recursion — consistent with Lemma 2.14.

## Mental Models
- "Hankel rank = McMillan degree": count the rank, get the order — no search.
- "Realization is up to similarity": the state coordinates are gauge freedom; algorithms may pick any basis (subspace methods pick the data-driven one).
- "Balance = the right coordinates": Gramians equal ⇒ modes are individually meaningful and truncation is principled.
- "Three faces, one system": impulse response ↔ transfer function ↔ (A,B,C,D); identification is choosing which face the data speaks and converting.

## Anti-patterns
- **Realizing non-minimal models** — unreachable/unobservable states hide in data matrices as numerically tiny Hankel singular values; check rank before fixing order.
- **Truncating in unbalanced coordinates** — mode size is coordinate-dependent; balance first.
- **Ignoring one-sided vs two-sided Z-transform** — one-sided shift brings initial-condition terms; closed-loop/finite-data arguments in ch11 depend on this.
- **Confusing BIBO with internal stability** — pole-zero cancellation can hide an unstable hidden mode; observability/reachability ranks are the real test.

## Reference Tables
### Realization ladder
| Given | Tool | Get |
|---|---|---|
| Impulse response | Hankel rank + SVD | order n |
| Markov parameters | Ho-Kalman | (A,B,C) |
| Any realization | Gramians + balancing transform | balanced (A,B,C) |
| Balanced model | truncate small σ | reduced model, H∞ bound |

### Canonical forms (ch3)
| Form | Structure | Used for |
|---|---|---|
| Observable canonical | companion C-block | observer design, PEM parametrization |
| Reachable canonical | companion B-block | controller forms |
| Balanced | WR = WO = Σ | reduction, subspace algorithms |

## Key Takeaways
Every LTI system is a Hankel matrix in disguise; its rank is the order, its SVD gives a minimal realization (Ho-Kalman).
Minimal ⟺ reachable + observable; realizations are unique only up to similarity — the fact that frees subspace methods from canonical forms.
Balanced Gramians make model reduction quantitative (drop small Hankel singular values).

## Connects To
Lemma 2.14 (Hankel rank) becomes the matrix realization theorem here; ch6 re-runs this whole chapter on finite data matrices (LQ decomposition, MOESP-style); ch7-8 do the stochastic analogue (covariance Hankel); ch9 ORT realizes from projected data; Doraiswami ch1/ch7 cover the same three-faces view for practitioners.
