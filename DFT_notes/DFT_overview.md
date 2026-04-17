---
tags: [concept, DFT, background]
---

# Density Functional Theory — Overview

## Summary
DFT is the workhorse of computational materials science. It solves the many-body electronic structure problem by mapping it onto an effective single-particle problem via the exchange-correlation functional, within the Kohn-Sham framework.

## Key Ideas
- **Hohenberg-Kohn theorems**: ground-state energy is a unique functional of electron density $n(\mathbf{r})$
- **Kohn-Sham equations**: introduce non-interacting reference system with same density
$$\left[-\frac{\hbar^2}{2m}\nabla^2 + V_\text{eff}(\mathbf{r})\right]\psi_i(\mathbf{r}) = \varepsilon_i \psi_i(\mathbf{r})$$
- **Exchange-correlation**: approximated (LDA, GGA/PBE, hybrid functionals)
- Self-consistent field (SCF) iteration to convergence

## Use in This Project
DFT provides the **high-fidelity energy evaluations** for atomic structure optimization. Each DFT call is expensive ($\sim$minutes to hours), motivating the use of ML surrogates to reduce the number of required calls.

## Common DFT Codes
- **FHI-aims**: all-electron, numeric atom-centered orbitals
- **VASP**: plane-wave basis, widely used in materials science
- **Quantum ESPRESSO**: plane-wave, open-source

## Typical Workflow
1. Define structure (cell + atomic positions)
2. Specify k-point mesh, basis set / cutoff, XC functional
3. Run SCF to converge electron density
4. Extract total energy, forces, stress

## Connections
- [[background/multi_fidelity_learning]] — DFT as high-fidelity model
- [[background/bayesian_optimization]] — DFT energy as objective function
- [[BOSS_notes/BOSS_overview]] — BOSS calls DFT as oracle

## References
- Giustino, *Materials Modelling using Density Functional Theory* (2014)
- Kohn & Sham, *Phys. Rev.* 140, A1133 (1965)
