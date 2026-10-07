# Patterns — Adaptive Control (Åström & Wittenmark)

## Design patterns

### 1. Find the underlying design problem
Every adaptive scheme = a classical design (pole placement, min variance, LQ, receding horizon) run on estimates. Ask "what design would I do if parameters were known?" — that's what the loop converges to, and its conditioning is the loop's conditioning.

### 2. Two-loop skeleton (STR)
Estimation loop (RLS + guards) → design block (Diophantine/spectral factorization) → fixed-form regulator. Keep the pieces independently analyzable; the glue (rates, filters, modes) is where practice lives.

### 3. Reparameterize to kill the design block (direct STR / implicit GPC)
Run the design identity as an operator on y(t); estimate controller parameters directly. Price: minimum phase + known relative degree. Benefit: no on-line solve, no Diophantine conditioning.

### 4. Certainty equivalence + excitation management
Use estimates as if true, but engineer the experiment: startup dither, periodic re-tuning, setpoint activity. Certainty equivalence never probes for you.

### 5. Observer polynomial as noise budget
A_o filters the estimation side without touching regulation poles. Tune adaptation speed vs parameter chatter with it.

### 6. Schedule coarse, adapt fine
Gain-schedule on the physics-driven variable for the big variation; adapt only the residual. Cheapest robust architecture (Ch 1, Ch 9).

### 7. Force the oscillation when excitation matters (SOAS / relay dither)
If identification must never go stale, close the loop so it self-oscillates: guaranteed PE, continuous (K_u,T_u) tracking.

### 8. Robust-first triage
Before adapting: can a fixed (Horowitz/LTR) or gain-scheduled loop meet spec over the range? Adaptation is justified by closed-loop evidence, not open-loop variation (abuse test).

### 9. Performance-dial interface
Expose bandwidth/M_s/LQ weight to the user; hide raw parameters. Same principle as M_s-based PID tuning.

## Diagnosis playbook (symptom → likely cause → chapter)

### Adaptive loop misbehaves
- **Parameter jumps after quiet periods** → covariance wind-up (λ<1 + no excitation) → constant trace / directional forgetting / leakage (Ch 11)
- **Oscillation/chaos when adaptation sped up** → γ past bifurcation bound → average analysis, lower γ (Ch 5-6)
- **Instability only with fast unmodeled dynamics** → turn-off phenomenon → normalize/filter regressors, dead zone, σ-mod (Ch 6, 10)
- **Estimates biased but loop stable** → noise-regressor correlation (equation-error bias) → output-error/prediction-error model, whitening filter C(q) (Ch 2, 4)
- **Parameters never converge, control OK** → direct scheme in null space of regressor — fine if behavior converges; add PE if you need parameters (Ch 6)
- **Control signal blows up suddenly** → design-map singularity (near pole-zero cancellation) or r̂₀ → 0 in direct STR → conditioning check, projection (Ch 3, 11)
- **Loop fine until setpoint quiet, then drifts** → integral action starves estimator of low-frequency information → inject dither (Ch 11)
- **Adaptive worse than PID** → no pre-tuning (wrong time scales/sampling) → auto-tune first (Ch 8)

### Tuning an auto-tuner
- Relay amplitude too small → no limit cycle; too large → nonlinear regime; pick d for ~10-20% overshoot regime (Ch 8)
- Multiple limit cycles / asymmetric oscillation → describing-function assumption broken → don't tune that loop with relay (Ch 8, 10)

## Estimator hardening checklist (Ch 11)
- Projection set D for θ̂ (also guards r₀ ≠ 0)
- Dead zone / conditional updating on the innovation
- Forgetting paired with excitation guard (constant trace or directional)
- UDUᵀ square-root form
- Data filter F aligned with control criterion
- Model order ≥ plant; delay term for computational delay
- Covariance trace alarm; residual (innovation) monitor

## Algorithm selection tree
- Known dynamics vs measurable variable → **gain scheduling** (Ch 9)
- Unknown but slowly varying, specifiable design → **STR indirect** (Ch 3-4)
- Minimum phase + known delay, want no on-line solve → **direct STR** (Ch 3.5)
- Reference-model spec, simple structure → **MRAS Lyapunov** (Ch 5)
- Need guaranteed excitation / continuous re-ID → **SOAS/relay** (Ch 10)
- Uncertainty range known, fast changes → **robust high-gain** (Ch 10)
- Just commissioning/maintenance → **auto-tuning** (Ch 8, 12)
