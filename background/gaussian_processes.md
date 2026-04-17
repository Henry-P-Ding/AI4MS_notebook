---
tags: [concept, ml, background]
---

# Gaussian Processes

## Summary
A Gaussian process (GP) is a probability distribution over functions. Any finite collection of function values follows a multivariate Gaussian distribution. GPs are fully specified by a mean function $m(\mathbf{x})$ and a covariance (kernel) function $k(\mathbf{x}, \mathbf{x}')$.

## Key Ideas
- Non-parametric: the model complexity grows with data
- Provides both predictions and uncertainty estimates
- Kernel encodes prior assumptions about smoothness/structure
- Posterior update is exact (closed-form) for Gaussian likelihoods

## GP Regression
Given training data $\{(\mathbf{x}_i, y_i)\}$, the posterior predictive distribution at a new point $\mathbf{x}_*$ is:

$$\mu_* = k_*^T (K + \sigma_n^2 I)^{-1} \mathbf{y}$$
$$\sigma_*^2 = k_{**} - k_*^T (K + \sigma_n^2 I)^{-1} k_*$$

where $K$ is the kernel matrix, $k_* = [k(\mathbf{x}_*, \mathbf{x}_i)]$, $k_{**} = k(\mathbf{x}_*, \mathbf{x}_*)$.

## Common Kernels
- **Squared exponential (RBF)**: $k(\mathbf{x}, \mathbf{x}') = \sigma_f^2 \exp\left(-\frac{|\mathbf{x}-\mathbf{x}'|^2}{2\ell^2}\right)$
- **Matérn**: smoother alternative with explicit smoothness parameter $\nu$

## Multi-task GPs
Extend standard GPs to model correlations between multiple outputs (tasks). Coregionalization models the inter-task covariance. Relevant for multi-fidelity learning where outputs share structure.

## Connections
- Used in [[bayesian_optimization]] as the surrogate model
- Multi-task GPs are central to [[multi_fidelity_learning]]

## References
- Rasmussen & Williams, *Gaussian Processes for Machine Learning* (2006)
