# AI4MS Lab Notebook — NAT 09-AMOPT

Lab notebook for the **TUM PREP Summer Research Program** at the [AI-based Materials Science (AI4MS) group](https://www.ai4ms.de/), Technische Universität München.

- **Project**: NAT 09 — Optimisation in Atomistic Machine Learning
- **Supervisor**: Prof. Patrick Rinke (patrick.rinke@tum.de)
- **Co-supervisor**: Dr. Casper Larsen (casper.larsen@tum.de)
- **Location**: James-Franck-Str. 1, D-85748 Garching
- **Duration**: Summer 2026

---

## Project Overview

Atomistic modeling plays a central role in materials science, enabling researchers to understand and predict the behavior of materials at the atomic scale. This project focuses on **global optimization of atomic structures** using machine learning methods, with two possible research directions:

**Project 1: Multi-task Learning**
Multi-task Gaussian processes for multi-fidelity learning — combining fast, lower-fidelity models (e.g., MACE) with accurate but expensive methods (DFT) to accelerate global optimization. Implemented into the [BOSS code](https://codebase.helmholtz.cloud/boss/boss).

**Project 2: Grand Canonical Optimization**
Extending atomic structure optimization to explore structures across varying stoichiometries, integrating property optimization with free energy minimization for functional materials discovery.

**Tasks:**
1. Review existing literature and identify promising solutions
2. Implement suitable algorithms into the BOSS code
3. Test and validate the implemented methods
4. Apply the methods to atomic systems of interest to the AI4MS group

---

## Notebook Structure

This notebook uses a three-tier knowledge system, designed for [Obsidian](https://obsidian.md/) and written in portable Markdown.

### 1. Daily Entries (`entries/`)
Atomic, step-by-step daily logs. One file per day (`YYYY-MM-DD.md`). Each entry captures exactly what was done and is reproducible from scratch.

### 2. Concept Files (topic directories)
Compiled notes synthesizing understanding of specific tools, methods, and ideas. Updated as knowledge accumulates. Organized by topic:

| Directory | Contents |
|---|---|
| `background/` | Core ML and materials science concepts |
| `BOSS_notes/` | BOSS code documentation and usage |
| `MACE_notes/` | MACE universal interatomic potential |
| `DFT_notes/` | Density functional theory reference |
| `HPC_notes/` | HPC/cluster computing at TUM |

### 3. Experiments (`experiments/`)
Computational experiments: Jupyter notebooks, Python scripts, SLURM job scripts, and output data. Subdirectories named by experiment.

### 4. Papers (`papers/`)
Literature notes using BibLaTeX citation keys as filenames (e.g., `@rinke2024.md`). Integrated with Zotero via Better BibLaTeX. Bibliography in `TUM_PREP.bib`.

### 5. Templates (`templates/`)
Consistent templates for daily entries and concept files.

---

## Setup

```bash
git clone https://github.com/Henry-P-Ding/TUM_PREP_notebook.git
```

Open the cloned directory as a vault in Obsidian. Install the **Better BibLaTeX** community plugin for citation integration.
