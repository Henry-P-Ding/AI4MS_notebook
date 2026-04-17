---
tags: [concept, ml, background]
---

# Bayesian Optimization

## Summary
Bayesian optimization (BO) is a sequential strategy for optimizing expensive black-box functions. It uses a surrogate probabilistic model (typically a GP) to approximate the objective and an acquisition function to decide where to evaluate next.

## Key Ideas
- **Surrogate model**: GP fitted to existing evaluations; gives prediction + uncertainty
- **Acquisition function**: balances exploration vs. exploitation to pick next query
- **Update**: after each evaluation, refit the surrogate and re-maximize acquisition
- Efficient for expensive functions (e.g., DFT energy calculations)

## Acquisition Functions
- **Expected Improvement (EI)**: $\text{EI}(\mathbf{x}) = \mathbb{E}[\max(f(\mathbf{x}) - f^+, 0)]$
- **Upper Confidence Bound (UCB)**: $\text{UCB}(\mathbf{x}) = \mu(\mathbf{x}) + \kappa \sigma(\mathbf{x})$
- **Probability of Improvement (PI)**

## Application to Atomic Structure Optimization
BO explores the potential energy surface (PES) to find minimum-energy configurations:
- Input space: atomic coordinates / degrees of freedom
- Objective: total energy from DFT or ML potential
- Goal: find global minimum with fewest function evaluations

## Connections
- Surrogate model: [[gaussian_processes]]
- Implementation: [[BOSS_notes/BOSS_overview]]
- Multi-fidelity extension: [[multi_fidelity_learning]]

## References
- Shahriari et al., *Taking the Human Out of the Loop* (2016)
