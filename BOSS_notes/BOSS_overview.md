---
tags: [concept, code, BOSS]
---

# BOSS Overview

## Summary
BOSS (Bayesian Optimization Structure Search) is a software package implementing active Bayesian optimization for atomic structure search. Developed at Aalto University and the Helmholtz-Zentrum Hereon.

## Key Features
- GP-based surrogate model for potential energy surface
- Active learning: iteratively selects next structure to evaluate
- Interfaces with external energy codes (DFT, ML potentials)
- Particularly effective from sparse datasets

## Repository
- Codebase: https://codebase.helmholtz.cloud/boss/boss

## Installation

```bash
# TODO: fill in installation steps
```

## Basic Usage

```python
# TODO: fill in once familiar with the API
```

## Input / Output
- Input: initial structures, energy calculator, BO settings
- Output: trajectory of evaluated structures, predicted PES, optimal structure

## Key Parameters
| Parameter | Description |
|---|---|
| `kernel` | GP kernel type |
| `acquisition` | Acquisition function |
| `n_init` | Number of initial random evaluations |
| `n_iter` | Number of BO iterations |

## Connections
- [[background/bayesian_optimization]]
- [[background/gaussian_processes]]
- [[background/multi_fidelity_learning]]

## References
- BOSS documentation
