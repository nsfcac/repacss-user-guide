# 🥮 Basics of Running Jobs

REPACSS uses **Slurm** for cluster/resource management and job scheduling. Slurm is responsible for allocating resources to users, providing a framework for starting, executing and monitoring work on allocated resources, and scheduling work for future execution.

---

## 📚 Additional Resources

* [Slurm Documentation](https://slurm.schedmd.com/documentation.html)
* [Slurm Tutorials](https://slurm.schedmd.com/tutorials.html)
* [Slurm Manual Pages](https://slurm.schedmd.com/man_index.html)
* [Slurm FAQ](https://slurm.schedmd.com/faq.html)

---

## 🧪 Jobs

A **job** is an allocation of resources such as compute nodes assigned to a user for a specific amount of time. Jobs can be **interactive** or **batch** (via script) and may be scheduled for future execution.

!!! tip
    REPACSS provides example job scripts and templates.

When you log in to REPACSS, you land on a **login node**. Login nodes are meant for preparing jobs (e.g., editing, compiling). **Jobs must run on compute nodes**, and are submitted using Slurm commands.

The system supports a variety of workflows including interactive tasks, serial runs, GPU applications, and large-scale parallel computations.

---

## 🚀 Submitting Jobs

### `sbatch`

Used to submit a batch job script:

```bash
$ sbatch my_job.sh
Submitted batch job 864933
```

The script should include `#SBATCH` directives and typically one or more `srun` commands to launch tasks.

### `salloc`

Request resources for an interactive session:

```bash
$ salloc --nodes=1 --time=01:00:00 --partition=standard
```

This opens an interactive shell on a compute node where you can run `srun` manually.

### `srun`

Launches job steps in real time:

```bash
$ srun -n 4 ./program
```

Use inside a job script or interactively to execute code across allocated nodes.

---

## ⚙️ Commonly Used Options

| Option (long)     | Short | Description                               | sbatch/salloc | srun |
| ----------------- | ----- | ----------------------------------------- | ------------- | ---- |
| `--time`          | `-t`  | Max walltime                              | ✅             | ❌    |
| `--nodes`         | `-N`  | Number of compute nodes                   | ✅             | ✅    |
| `--ntasks`        | `-n`  | Total number of MPI tasks                 | ✅             | ✅    |
| `--cpus-per-task` | `-c`  | Number of CPU cores per task              | ✅             | ✅    |
| `--gpus`          | `-G`  | Number of GPUs                            | ✅             | ✅    |
| `--constraint`    | `-C`  | Node type or hardware constraint          | ✅             | ❌    |
| `--qos`           | `-q`  | Quality of service                        | ✅             | ❌    |
| `--account`       | `-A`  | Project account for charging compute time | ✅             | ❌    |
| `--job-name`      | `-J`  | Name of the job                           | ✅             | ❌    |

!!! tip
    We recommend using the long-form options (`--option=value`) in scripts for readability.

---

## 📝 Writing a Job Script

Basic format:

```bash
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --nodes=2
#SBATCH --time=01:00:00
#SBATCH --partition=h100
#SBATCH --account=mXXXX

module load gcc

srun -n 4 ./a.out
```

Scripts should always include required Slurm options. The values can also be passed on the command line:

```bash
sbatch -N 2 -p h100 ./job.sh
```

---

## 🤥 Options Inheritance

Slurm options can be declared:

* in the job script with `#SBATCH`
* or on the `sbatch` command line

If both are present, the **command line overrides the script**. Many values will automatically propagate to `srun` via environment variables (e.g., `SLURM_JOB_NUM_NODES`).

However, avoid manual overrides inside scripts unless necessary. Behavior might vary if `ssh` or `manual launch` techniques are used.

---

## 🐍 Example Script: Python

```bash
#!/bin/bash
#SBATCH --job-name=python_job
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --time=01:00:00
#SBATCH --partition=zen4

module load gcc
source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv

python script.py
```

---

## ⚠️ Defaults

If not explicitly set, Slurm applies default values:

| Option  | Default         |
| ------- | --------------- |
| nodes   | 1               |
| time    | 10 minutes      |
| qos     | `debug`         |
| account | default project |

Set permanent defaults via environment variables:

```bash
export SBATCH_ACCOUNT=m1234
export SALLOC_ACCOUNT=m1234
```

!!! warning
    Jobs **must specify a `--constraint`** (e.g., `h100`) or they may be rejected.

---

## 🎮 Running GPU Jobs

Use `--gpus` or `--gres=gpu:X` to request GPU access:

```bash
#SBATCH --gres=gpu:1
```

Failure to do so may cause errors such as:

```
No CUDA-capable device is detected
```

Always load the necessary modules:

```bash
module load cuda
```

---

## 🔍 Monitoring Jobs

Check status:

```bash
squeue -u $USER
```

Estimate start time:

```bash
squeue --start -j <job_id>
```

Check usage after job completes:

```bash
sacct -j <job_id>
```

---

## 🛠️ Troubleshooting

* Check quotas: `quota -s`
* Verify all required options are included
* Confirm partition and constraint match available hardware
* Load appropriate modules before execution
* Inspect job output files (`.out`, `.err`) for errors

---

## 📖 Learn More

* [Job Examples](examples.md)
* [Monitoring Jobs](monitoring.md)
* [Interactive Sessions](interactive.md)
* [Best Practices](best-practices.md)

