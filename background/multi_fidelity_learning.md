---
tags: [concept, ml, background]
---

# Multi-Fidelity Learning

## Summary
Multi-fidelity learning combines data from multiple computational models that predict the same property at different accuracy/cost trade-offs. The goal is to achieve near-high-fidelity accuracy while reducing total computational cost.

## Key Ideas
- **Low-fidelity source**: cheap but approximate (e.g., MACE universal potential)
- **High-fidelity source**: accurate but expensive (e.g., DFT)
- A multi-task GP models the correlation between fidelity levels
- Active sampling chooses which fidelity to query at each step

## Kennedy-O'Hagan Framework
The high-fidelity model is expressed as:
$$f_H(\mathbf{x}) = \rho \cdot f_L(\mathbf{x}) + \delta(\mathbf{x})$$
where $\rho$ is a scaling parameter and $\delta$ captures the discrepancy. Both are modeled as GPs.

## Task-Sampling Strategies
Choosing when to query low vs. high fidelity is critical. Key factors:
- Relative cost ratio between fidelities
- Current model uncertainty
- Information gain per unit cost

## Connection to This Project
Project 1 of NAT 09-AMOPT focuses on developing optimal task-sampling strategies for multi-fidelity BO that enhance model performance while minimizing computational cost. Combines MACE (low-fidelity) with DFT (high-fidelity).

## Connections
- [[gaussian_processes]] — multi-task GP formulation
- [[bayesian_optimization]] — BO loop
- [[MACE_notes/MACE_overview]] — low-fidelity model
- [[DFT_notes/DFT_overview]] — high-fidelity model
- [[BOSS_notes/BOSS_overview]] — implementation target

## References
- Kennedy & O'Hagan, *Predicting the output from a complex computer code* (2000)
