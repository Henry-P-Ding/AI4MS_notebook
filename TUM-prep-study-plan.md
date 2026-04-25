---
title:      "TUM PREP Learning Plan: ML for Ab Initio Physics"
date:       2026-04-16
tags:       [ml, physics, tumprep, learning, boss, mace, gaussian-processes]
identifier: "20260416T220000"
---

## Phase 1: ML and Python Foundations (Weeks 1–2)

Compressed relative to the original plan. Don't need deep learning fluency to start this project — need enough to read the MACE paper and run the code. But *do* need solid Python scientific stack skills.

### Week 1 (April 20–26) — Core ML & PyTorch

**Goals:** Gradient descent, backprop, training loops, regularization, train/val/test hygiene.

- **Primary:** Andrej Karpathy's *Neural Networks: Zero to Hero*, lectures 1–3 (`micrograd` and `makemore`). Reimplement in Neovim.
- **Reading:** Nielsen, *Neural Networks and Deep Learning* Ch. 1–3 (free online).
- **Tooling:** Fresh conda/mamba env with PyTorch, NumPy, SciPy, matplotlib, ASE, scikit-learn. Get comfortable in Jupyter via `jupytext` or similar so I can stay in Neovim.

**Deliverable:** Train an MLP on MNIST. Explain backprop to myself out loud.

### Week 2 (April 27–May 3) — Scientific Python + ASE

**Goals:** Atomic Simulation Environment fluency, handling atomic structures programmatically.

- Work through the `ASE` tutorials: building structures, reading/writing cif/xyz, running calculators, geometry optimization.
- Get `MACE` installed (via `mace-torch` on PyPI) and run the quick-start example predicting energies/forces on a small molecule.
- Skim Karpathy lectures 4–5 on attention — won't need transformers immediately but MACE-related papers reference them.
- **Reading:** Carleo et al. (2019) *Rev. Mod. Phys.* "Machine learning and the physical sciences" — sections on materials and sampling.

**Deliverable:** A short script that builds a small cluster (say Au₁₃ or a water dimer), runs `MACE-MP-0` on it, and plots an energy profile along some structural coordinate.

---

## Phase 2: Gaussian Processes (Weeks 3–4)

Center of gravity of the project. Invest heavily.

### Week 3 (May 4–10) — Gaussian Processes from Scratch

**Goals:** Own GPs at the level where I could implement one myself and know every hyperparameter's role.

- **Primary text:** Rasmussen & Williams, *Gaussian Processes for Machine Learning* (free PDF). Chapters 1, 2, 4, 5. Read actively, with pen and paper.
- **Concepts to nail:** prior → posterior, kernel functions (RBF, Matérn, linear), marginal likelihood maximization, noise hyperparameters, computational cost ($O(N^3)$) and why it matters for BO.
- **Hands-on:** Implement 1D GP regression from scratch using only NumPy. Then re-implement with `GPyTorch` or `scikit-learn`. Compare.
- **Physics grounding:** Fit a 1D model potential (Morse, LJ) with GP, visualize posterior mean and uncertainty bands. The uncertainty bands are what drive BO.

**Deliverable:** A notebook comparing kernels (RBF vs. Matérn-5/2 vs. Matérn-3/2) on noisy sine data. Understand why Matérn kernels are usually preferred for PES work.

### Week 4 (May 11–17) — Bayesian Optimization and BOSS

**Goals:** Understand acquisition functions, exploration-exploitation, and the specific algorithmic choices in BOSS.

- **Primary paper (essential):** Todorović, Gutmann, Corander, Rinke (2019) — "Bayesian inference of atomistic structure in functional materials," *npj Comput. Mater.* **5**, 35. **This is the BOSS paper.** Read it three times.
- **Supporting reading:**
  - Shahriari et al. (2016) "Taking the human out of the loop: A review of Bayesian optimization," *Proc. IEEE* **104**, 148. Canonical BO review.
  - Frazier (2018) "A tutorial on Bayesian optimization," arXiv:1807.02811. More mathematical, very clear.
- **Acquisition functions to understand deeply:** Expected Improvement (EI), Upper Confidence Bound (UCB), Lower Confidence Bound for minimization (LCB), Thompson Sampling. Know when each fails.
- **Hands-on:** Install **BOSS** (`pip install aalto-boss`) and run the tutorial examples from the BOSS documentation. Also reproduce a toy 2D BO problem from scratch using GPy/BoTorch so I see the pieces without BOSS's abstractions.
- **Dimensionality awareness:** Read about high-dimensional BO issues (TuRBO, local BO) — relevant for larger structural searches.

**Deliverable:** A BOSS run on a simple system (try optimizing adsorbate positions on a surface from the BOSS examples). Document the hyperparameter choices and what each does.

---

## Phase 3: MLIPs in Practice (Week 5)

Need *working* knowledge of MACE, not research-level depth. Goal is being able to use it as the lower-fidelity model in multi-fidelity workflows.

### Week 5 (May 18–24) — MACE and the MLIP Stack

**Goals:** Train, fine-tune, and deploy MACE; understand where it shines and where it fails.

- **Essential papers (read in order):**
  1. Behler & Parrinello (2007) *PRL* **98**, 146401 — historical foundation
  2. Schütt et al. (2017) — SchNet, the gentlest GNN entry
  3. Batzner et al. (2022) — NequIP, *Nature Commun.* **13**, 2453 — the equivariance argument
  4. Batatia et al. (2022) — MACE (NeurIPS) — current SOTA
  5. Batatia et al. (2023) — MACE-MP-0 preprint — the foundation model I'll likely use
- **Math background:** Spherical harmonics, Wigner matrices, Clebsch–Gordan coefficients (review from Sakurai). The `e3nn` tutorials ground this in code.
- **Hands-on:**
  - Fine-tune `MACE-MP-0` on a small dataset (MD17 or an rMD17 subset).
  - Run a short MD trajectory with ASE + MACE calculator.
  - Identify where MACE's energy predictions *disagree* with DFT (if I can obtain any DFT data) — this intuition is the motivation for multi-fidelity methods.
- **Review to skim:** Behler (2021) *Chem. Rev.* "Four Generations of High-Dimensional Neural Network Potentials."

**Deliverable:** Short write-up: "MACE error modes I observed." This is exactly the kind of practical insight that makes multi-fidelity methods interesting.

---

## Phase 4: Project-Specific Methods (Weeks 6–8)

Pivot from general background to the specific project.

### Week 6 (May 25–31) — Active Learning and Structure Search

**Goals:** Connect GPs and MLIPs to the structure-search problem. Understand how BOSS and similar tools explore configuration space.

- **Papers:**
  - Jørgensen et al. (2020) "Atomistic structure learning" — on GOFEE and related BO-guided structure search.
  - Bisbo & Hammer (2020) "Efficient global structure optimization with a machine-learned surrogate model," *PRL* **124**, 086102.
  - Järvi et al. (2020) "Detecting stable adsorbates of (1S)-camphor on Cu(111) with Bayesian optimization," *Beilstein J. Nanotechnol.* **11**, 1577 — classic BOSS application.
  - Any recent Rinke-group paper from 2024–2026 I can find on arXiv (search "Rinke atomistic Bayesian"). Want to know what the group has been publishing.
- **Concepts:** Active learning loops, committee uncertainty, D-optimal design, diversity in structure selection.
- **Hands-on:** Implement a toy active-learning loop: train a GP on 5 points, pick the next point by EI, retrain, iterate. Use a 2D Müller-Brown or similar test potential.

**Deliverable:** Active-learning loop notebook. Visualize how the GP's uncertainty evolves and where new points get placed.

### Week 7 (June 1–7) — Multi-Task and Multi-Fidelity Gaussian Processes

This is **Project 1** directly. Want to arrive knowing this literature.

- **Foundational papers:**
  - Bonilla, Chai, Williams (2007) "Multi-task Gaussian process prediction," *NeurIPS*. The intrinsic coregionalization model (ICM) — the standard multi-task GP.
  - Kennedy & O'Hagan (2000) "Predicting the output from a complex computer code when fast approximations are available," *Biometrika* **87**, 1. The canonical multi-fidelity paper; old but foundational.
  - Poloczek, Wang, Frazier (2017) "Multi-information source optimization," *NeurIPS*. Modern multi-fidelity BO.
- **Applications in chemistry/materials:**
  - Tran et al. (2020) "Multi-fidelity machine learning for materials discovery." Search Google Scholar for recent examples — the field moves fast.
  - Egorova, Hafizi, Woods, Day (2020) on multi-fidelity for crystal structure prediction.
  - Fare, Fenner, Benatan, Varsi, Pyzer-Knapp (2022) "A multi-fidelity machine learning approach to high throughput materials screening," *npj Comput. Mater.*
  - Recent Rinke/Larsen group papers on this exact problem — this is their active research area so there will be preprints.
- **Hands-on:** `emukit` (Amazon's BO library) has clean multi-fidelity tutorials. `BoTorch` (Meta) has state-of-the-art implementations. Reproduce a 2-fidelity example where the cheap function is a noisy/biased version of the true function.

**Deliverable:** A 3–4 page literature synthesis on multi-fidelity BO for atomistic problems. Identify what task-sampling strategies exist and their trade-offs. **Bring this document to Munich.** Dr. Larsen will appreciate it enormously, and it signals real preparation.

### Week 8 (June 8–14) — Grand Canonical Optimization

This is **Project 2**. A genuinely newer, more open area.

- **Foundational:**
  - Grand canonical ensemble refresher — thermal physics course. Review chemical potential $\mu$, $\Omega(T, V, \mu)$, and particle number fluctuations.
  - Reuter & Scheffler (2001) "Composition, structure, and stability of RuO₂(110) as a function of oxygen pressure," *PRB* **65**, 035406 — ab initio thermodynamics, the gateway to this whole area.
- **Variable-composition structure search:**
  - Kang & Hautier (various years) on compositional optimization.
  - Deringer et al. on exploration of amorphous phases — related methodology.
  - Merchant et al. (2023) GNoME, *Nature* **624**, 80 — composition space exploration at scale.
  - Recent papers specifically on grand-canonical genetic algorithms (Mortensen / Hammer group at Aarhus) and grand-canonical Bayesian methods. Search "grand canonical optimization atomic structure" on arXiv, filtered to 2023–2026.
- **Concepts:** Variable-size search spaces, chemical potential constraints, convex hull construction, formation energy as objective.

**Deliverable:** A short write-up identifying 3–4 concrete open problems at the intersection of BO and grand canonical search. These will become conversation starters with Rinke and Larsen.

---

## Phase 5: Integration and Preparation (Weeks 9–10)

### Week 9 (June 15–21) — Mini-Project and BOSS Deep Dive

**Goals:** Stop consuming and produce something. Get fluent in the BOSS codebase so I can contribute on day one.

- **Read the BOSS source code.** Actually read it. Understand the main optimization loop, how the acquisition function is implemented, how kernels are defined, how user-defined tasks plug in. Take notes in the vault. This is the single highest-leverage activity of the entire 10 weeks — it's where I'll spend the summer.
- **Mini-project options** (pick one):
  1. **Multi-fidelity toy problem in BOSS style:** Build a 2-fidelity BO system for a known 2D test function where the "cheap" model has systematic bias. Compare to single-fidelity. This directly maps to Project 1.
  2. **Grand canonical toy:** Set up a toy search where atoms can be added/removed, optimize formation energy against a chemical potential. Visualize the convex hull that emerges. Maps to Project 2.
  3. **MACE-as-surrogate-for-DFT:** Take a small DFT dataset (from NOMAD or Materials Project), treat MACE predictions as low-fidelity, fit a multi-fidelity GP. The most ambitious option.
- **Communication prep:** Email Dr. Larsen (or whoever the day-to-day supervisor will be) in the last week of June with something like: *"I've been preparing for the project and have read [list]. I've also tried [mini-project]. A few questions I'm hoping to clarify early: [2–3 substantive questions]."* Supervisors love this. It demonstrates initiative without being presumptuous.

### Week 10 (June 22–28) — Consolidation and Logistics

- Re-read the BOSS paper and 2–3 of the most important multi-fidelity papers fresh.
- Review my own notes. Organize papers in papis with project tags.
- Handle logistics: Munich accommodation, travel, German bureaucracy if applicable, TUM IT onboarding.
- **Rest.** 40 hours/week for 6–10 weeks; arriving burned out is counterproductive.

---

## Papers to Have Read Before Day One (Priority Ordered)

Tier 1 — mandatory:

1. Todorović et al. (2019) — BOSS
2. Batatia et al. (2022) — MACE
3. Bonilla, Chai, Williams (2007) — multi-task GPs
4. Kennedy & O'Hagan (2000) — multi-fidelity
5. Shahriari et al. (2016) — BO review

Tier 2 — strongly recommended:

6. Rasmussen & Williams Ch. 2, 5 (textbook)
7. Behler (2021) *Chem. Rev.* review
8. Poloczek et al. (2017) — multi-information-source BO
9. Reuter & Scheffler (2001) — ab initio thermodynamics
10. At least three recent Rinke-group papers (2024–2026)

Tier 3 — good to have skimmed:

11. Frazier BO tutorial
12. MACE-MP-0 paper
13. One grand-canonical structure-search paper

---

## What I Should Be Able to Do by July 1

- Set up, run, and modify a BOSS optimization from the command line
- Train and fine-tune a MACE model on a small dataset
- Explain, at a whiteboard, the difference between single-task, multi-task, and multi-fidelity GPs and when each is appropriate
- Explain why expected improvement works and when it fails
- Describe at least two existing approaches to grand canonical structure search and name their limitations
- Read any current paper from the Rinke group with ~80% comprehension

That's a genuinely strong preparation — significantly better than most students arriving at a ten-week research program. The supervisors will notice.

---

## One Final Note

Don't over-plan. This schedule will slip in places and run ahead in others. If week 3 on GPs clicks and I finish in 4 days, push ahead. If equivariance in week 5 takes longer, compress something in week 8. The goal isn't to complete every item — it's to arrive on July 1 fluent enough to contribute, and curious enough to have questions ready.
