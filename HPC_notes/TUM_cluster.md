---
tags: [concept, HPC]
---

# TUM HPC Cluster

## Summary
TUM provides HPC resources for computationally intensive research. The AI4MS group likely uses the LRZ (Leibniz Supercomputing Centre) systems.

## LRZ Systems
- **SuperMUC-NG**: main HPC cluster at LRZ Garching
- **Linux Cluster**: general-purpose cluster
- Access via LRZ login portal

## Login

```bash
ssh username@lxlogin1.lrz.de   # LRZ Linux Cluster
ssh username@skx.supermuc.lrz.de  # SuperMUC-NG Skylake
```

## Job Submission (SLURM)

```bash
sbatch job.sh       # submit job
squeue -u $USER     # check job status
scancel JOBID       # cancel job
sinfo               # check available partitions
```

## Example Job Script

```bash
#!/bin/bash
#SBATCH --job-name=boss_run
#SBATCH --output=boss_%j.out
#SBATCH --error=boss_%j.err
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --time=24:00:00
#SBATCH --partition=general

source activate myenv
python run_boss.py
```

## File System
| Path | Purpose |
|---|---|
| `$HOME` | Home directory (limited quota) |
| `$WORK` | Work directory (larger quota, not backed up) |
| `$SCRATCH` | Fast scratch space (purged periodically) |

## Modules

```bash
module avail          # list available modules
module load python    # load a module
module list           # loaded modules
```

## Connections
- [[HPC_notes/software_environment]]

## Notes
- TODO: fill in TUM/AI4MS specific cluster details once on-site
