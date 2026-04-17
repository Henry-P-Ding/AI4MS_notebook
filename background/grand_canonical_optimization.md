---
tags: [concept, ml, background]
---

# Grand Canonical Optimization

## Summary
Grand canonical optimization extends conventional atomic structure search to explore structures across varying stoichiometries. Rather than fixing the number and type of atoms, the composition itself becomes an optimization variable.

## Key Ideas
- Conventional structure optimization: fixed $N$, fixed species, find minimum-energy arrangement
- Grand canonical: variable composition, find optimal $(N, \text{species}, \text{arrangement})$ jointly
- Connects to grand canonical ensemble in statistical mechanics (variable particle number at fixed $\mu$, $V$, $T$)

## Grand Canonical Ensemble
The relevant thermodynamic potential is the grand potential:
$$\Omega = F - \mu N$$
where $F$ is the Helmholtz free energy and $\mu$ is the chemical potential. Minimizing $\Omega$ over structures with variable $N$ gives the stable phase.

## Challenges
- Search space is combinatorially larger (composition + structure)
- Energy comparisons between different compositions require a reference (e.g., elemental chemical potentials)
- Convergence criteria more complex than fixed-composition search

## Connection to This Project
Project 2 of NAT 09-AMOPT proposes developing a grand canonical BO framework that explores materials with unknown optimal composition. Emerging area with significant potential for materials discovery.

## Connections
- [[bayesian_optimization]] — optimization framework
- [[gaussian_processes]] — surrogate model
- [[DFT_notes/DFT_overview]] — energy evaluations

## References
