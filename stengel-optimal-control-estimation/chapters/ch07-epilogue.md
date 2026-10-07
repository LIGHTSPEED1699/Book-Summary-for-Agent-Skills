# Epilogue (Chapter 7): Closing Perspective

## Core Idea
Stochastic optimal control is a *systematic generator of feasible solutions*, not an oracle: it answers exactly the question you pose — "ask the wrong question, and it most surely will give the wrong answer" — so the designer's judgment in choosing models and indices is the irreplaceable input.

## Key Points
- The theory supplies equations and algorithms that produce answers once model + performance indices are specified; it does **not** tell you which indices are good or what values are satisfactory.
- Its principal benefit: feasible solution families that can be **expanded or simplified to match the problem and its practical constraints** (from full nonlinear dual control down to constant-gain LQG).
- Solutions may be counterintuitive yet correct — trust a well-posed problem over intuition.
- The application challenge: match methodology understanding + system knowledge + realistic performance expectations.

## Mental Models
- "Garbage in, optimal garbage out": the optimizer is literal; cost-function authorship is the design act.
- "Right-size the theory": the book's hierarchy (dual control → CE/LQG → scheduled gains → PI) is a menu to scale to the problem's actual uncertainty.

## Key Takeaways
1. Optimal control machinery is judgment amplification, not judgment replacement.
2. The whole book's arc exists so you can pick the smallest rung of the hierarchy that honestly covers the uncertainty.

## Connects To
- Every chapter: the hierarchy it systematizes.
