# Basics of Running Jobs

REPACSS utilizes the **Slurm Workload Manager** for resource allocation and job scheduling across its high-performance computing infrastructure. Slurm manages the assignment of compute resources, oversees execution and monitoring, and enables the scheduling of tasks for future execution.

---

## Additional Resources

* [Slurm Documentation](https://slurm.schedmd.com/documentation.html)
* [Slurm Tutorials](https://slurm.schedmd.com/tutorials.html)
* [Slurm Manual Pages](https://slurm.schedmd.com/man_index.html)
* [Slurm FAQ](https://slurm.schedmd.com/faq.html)

---

## Job Definition

A **job** is defined as an allocation of compute resources granted to a user for a specified duration. Jobs may be executed interactively or as batch processes (via job scripts) and can be scheduled to run at a future time.

!!! note
    REPACSS provides sample job submission scripts and templates for common workloads.

Upon accessing REPACSS, users arrive at a **login node**, which is intended for job preparation activities such as file editing or code compilation. **All computational jobs must be submitted to compute nodes** using Slurm commands.

The platform supports a wide range of workflows including interactive sessions, serial executions, GPU-based applications, and large-scale parallel computations.

---

## Submitting Jobs

### `sbatch`

Submit a batch script:

```bash
$ sbatch my_job.sh
Submitted batch job 864933
```

Job scripts should include `#SBATCH` directives and one or more `srun` commands.

### `interactive`

Request an interactive session using the recommended wrapper script:

```bash
$ interactive -c 8 -p zen4
```

!!! tip  
    The `interactive` command wraps around Slurm's allocation mechanisms and handles additional environment setup required for compute node access. **Avoid using `salloc` directly** — especially in environments like Visual Studio Code — as it may fail to configure session parameters properly.

An interactive shell will be initiated on a compute node once resources are allocated.

### `srun`

Execute a job step in real-time:

```bash
$ srun -n 4 ./program
```

May be used within job scripts or interactive sessions.

---

## Commonly Used Options

| Option (long)     | Short | Description                               | sbatch | srun |
| ----------------- | ----- | ----------------------------------------- | ------ | ---- |
| `--time`          | `-t`  | Maximum wall clock time                   | ✅      | ❌    |
| `--nodes`         | `-N`  | Number of nodes                           | ✅      | ✅    |
| `--ntasks`        | `-n`  | Number of parallel tasks (e.g., MPI)      | ✅      | ✅    |
| `--cpus-per-task` | `-c`  | CPU cores allocated per task              | ✅      | ✅    |
| `--gpus`          | `-G`  | Number of GPUs requested                  | ✅      | ✅    |
| `--constraint`    | `-C`  | Specific hardware or node type constraint | ✅      | ❌    |
| `--qos`           | `-q`  | Quality of Service tier                   | ✅      | ❌    |
| `--account`       | `-A`  | Project account for usage tracking        | ✅      | ❌    |
| `--job-name`      | `-J`  | Name assigned to the job                  | ✅      | ❌    |

!!! tip
    It is advisable to use long-form flags (e.g., `--nodes=2`) in scripts for clarity and maintainability.

---

## Writing a Job Script

Sample job script:

```bash
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --nodes=2
#SBATCH --time=01:00:00
#SBATCH --partition=<your_partition>   # e.g. zen4 or h100 — run `sinfo` to see available partitions

module load gcc

srun -n 4 ./a.out
```

!!! tip
    Not sure what partition to use? Run `sinfo` to see all available partitions.

Slurm options may also be specified at the command line:

```bash
sbatch -N 2 -p <your_partition> ./job.sh
```

---

## Option Inheritance and Overriding

Slurm options may be declared within the job script via `#SBATCH` or specified directly on the command line. If both are present, command line options take precedence.

Environment variables such as `SLURM_JOB_NUM_NODES` are automatically populated and propagated to `srun`. Avoid redundant overrides within the script unless necessary. Behavior may vary when using non-Slurm launch mechanisms.

---

## Sample Python Job Script

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

python3 script.py
```
!!! warning "Miniforge Required"
    This script requires Miniforge to be installed on your account. If you haven't installed it yet, refer to the [Miniforge](../software/miniforge.md) documentation before running this script.

??? example "No conda? Use this instead"
    If you don't have Miniforge installed, you can run a basic Python script directly:

```bash
    #!/bin/bash
    #SBATCH --job-name=python_job
    #SBATCH --ntasks=1
    #SBATCH --cpus-per-task=8
    #SBATCH --mem=32G
    #SBATCH --time=01:00:00
    #SBATCH --partition=zen4

    python3 script.py
```
---

## Submitting GPU Jobs

!!! warning
    CUDA modules are only available on GPU nodes, not on the login node. To use CUDA, you must first request a GPU node either through an interactive session or a batch job.
    *For detailed usage examples, please refer to the [Job Examples](examples.md) section.*

To request GPU resources, use the `--gres` flag:

```bash
#SBATCH --gres=gpu:nvidia_h100_nvl:1
```
Before submitting a GPU job, verify that the GPU is accessible by running `nvidia-smi` in your job script:

```bash
#SBATCH --gres=gpu:nvidia_h100_nvl:1

nvidia-smi
```
Ensure required modules such as CUDA are loaded:

!!! note
    `module load cuda` is not yet available. CUDA 13.1 is accessible through the NVIDIA driver automatically when you request a GPU node.

If you request a GPU but forget the `--gres` flag, you may see:

```
No CUDA-capable device is detected
```

This means no GPU was allocated to your job. Make sure `--gres=gpu:nvidia_h100_nvl:1` is included in your script.
---

## Job Monitoring

Check job queue status:

```bash
squeue -u $USER
```

Estimate job start time:

```bash
squeue --start -j <job_id>
```

Review completed job statistics:

```bash
sacct -j <job_id>
```

---

## Troubleshooting

* Verify group disk quotas: `df -h /mnt/$(id -gn)`
* Ensure job script includes required Slurm options
* Confirm partition and hardware constraints match available resources
* Load relevant modules before execution
* Inspect job output files (`.out`, `.err`) for detailed error messages

---

## Additional Documentation

* [Job Examples](examples.md)
* [Monitoring Jobs](monitoring.md)
* [Interactive Sessions](interactive.md)
* [Best Practices](best-practices.md)
