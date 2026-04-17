---
tags: [concept, code, MACE]
---

# MACE Overview

## Summary
MACE (Multi-Atomic Cluster Expansion) is a universal interatomic potential based on equivariant message-passing neural networks. Trained on extensive DFT databases (e.g., Materials Project), it generalizes across the periodic table for predicting interatomic forces and energies.

## Key Features
- **Equivariant architecture**: respects rotational/translational/permutation symmetry by construction
- **Universal**: trained on broad datasets covering most elements
- **Fast**: orders of magnitude cheaper than DFT
- **Accuracy**: near-DFT accuracy for many systems; may struggle distinguishing low-energy configurations in specific systems

## Use in This Project
MACE serves as the **low-fidelity model** in multi-fidelity learning (Project 1). Its fast energy/force evaluations provide cheap data to inform the GP surrogate, reducing expensive DFT calls.

## Repository
- https://github.com/ACEsuit/mace

## Installation

```bash
pip install mace-torch
```

## Basic Usage

```python
from mace.calculators import mace_mp
calc = mace_mp(model="medium", dispersion=False, default_dtype="float32")

# Use as ASE calculator
atoms.calc = calc
energy = atoms.get_potential_energy()
forces = atoms.get_forces()
```

## Limitations
- May not distinguish closely competing low-energy configurations within a specific chemical system
- Trained on DFT-PBE; dispersion corrections may be needed

## Connections
- [[background/multi_fidelity_learning]] — role as low-fidelity model
- [[DFT_notes/DFT_overview]] — high-fidelity counterpart
- [[BOSS_notes/BOSS_overview]] — integration point

## References
- Batatia et al., *MACE: Higher Order Equivariant Message Passing Neural Networks for Fast and Accurate Force Fields* (2022)
