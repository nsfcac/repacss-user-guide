# Determining Resource Requirements


Before submitting production workloads to REPACSS, it is essential to accurately estimate the resources your jobs will require. Overestimating or underestimating resources can lead to inefficient scheduling, failed jobs, or unnecessary queuing delays. This exercise guides you through strategies to test and fine-tune resource requests in your SLURM job scripts.

---

## Overview of SLURM Resource Requests

SLURM provides several directives to declare resource needs in your job script:

- `--ntasks`: Number of tasks to launch (often `1` for serial jobs).
- `--cpus-per-task`: Number of CPU cores required per task.
- `--mem`: Amount of memory needed per node.
- `--time`: Estimated maximum runtime for the job.
- `--gres`: Specification for special resources, such as GPUs.

Explicitly specifying these parameters is recommended, especially when submitting multiple or resource-intensive jobs.

---

## Consequences of Incorrect Resource Requests

### Underestimating Resources

If your job exceeds the allocated resources (for example, memory), SLURM will terminate the job. Partial results may be lost. Therefore, it is critical to request sufficient resources to avoid interruptions.

### Overestimating Resources

Excessive resource requests can increase wait times, as fewer nodes have sufficient free resources to start your job. Over-requesting also limits availability for other users. For fairness and efficiency, request only what you expect to use.

---

## Estimating Resource Requirements

If you are unsure of your job’s memory or disk usage, you have two main options:

- **Estimate requirements in advance** using local tests and monitoring.
- **Run a test job** with conservative resource allocations and measure actual usage.

---

### Observing Memory Usage Locally
!!! warning "Important:" Do **not** execute computationally intensive jobs on shared login nodes. Use your personal workstation or a designated test environment to avoid interfering with other users.

On macOS or Windows, you can monitor processes using Activity Monitor or Task Manager. On Linux, the `ps` and `top` utilities can help track memory usage.

**Example: Using `ps`**

```bash
ps ux
```

The `RSS` column shows approximate memory usage in kilobytes.

**Example: Using `top`**

```bash
top -u <username>
```

The `RES` column shows memory usage in real time. Press `q` to exit.

---

### Estimating Disk Usage

Disk usage includes:

- Executable binaries
- Input files transferred to the job
- Output files generated during execution
- Temporary files created by your application

You can check file sizes on a local system with:

```bash
ls -lh
du -sh
```

---

## Determining Resource Requirements by Running Test Jobs (Recommended)

The most reliable method to measure your job’s resource needs is to submit a small-scale test job and examine the SLURM job statistics after completion.

**Example Test Script**

```python
#!/usr/bin/env python3
import time
size = 1000000
numbers = [str(i) for i in range(size)]
with open('numbers.txt', 'w') as f:
    f.write(' '.join(numbers))
time.sleep(60)
```

**Example SLURM Job Script (`test_job.slurm`)**

```bash
#!/bin/bash
#SBATCH --job-name=resource_test
#SBATCH --output=resource_test.out
#SBATCH --error=resource_test.err
#SBATCH --time=00:05:00
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=1G

module load python

srun python test_script.py
```

Submit the job:

```bash
sbatch test_job.slurm
```

When the job completes, check memory and CPU usage:

```bash
seff <jobid>
```

**Example `seff` Output:**

```
Job ID: 12345
State: COMPLETED (exit code 0)
Cores: 1
CPU Utilized: 00:01:00
Memory Utilized: 98.50 MB
```

---

## Specifying Resource Requests in Job Scripts

Based on test job results, update your SLURM script with appropriate resource estimates, rounding up modestly to allow for variability:

```bash
#SBATCH --mem=120M     # Rounded up from ~99 MB
```

**Important Notes:**

- `--mem` units default to megabytes unless you specify `G` for gigabytes.
- `--time` should reflect the maximum expected runtime.
- `--cpus-per-task` should match the number of threads used by your program.

---

## Verification

After updating your job script:

1. Re-submit the job.
2. Confirm successful completion.
3. Review `seff` or `sacct` output to ensure your estimates were adequate.
4. Adjust further if needed.

If the job failed due to memory or runtime limits, increment your requests incrementally and re-test.

---

## Example of Updated Job Script

```bash
#!/bin/bash
#SBATCH --job-name=final_run
#SBATCH --output=final_run.out
#SBATCH --error=final_run.err
#SBATCH --time=00:10:00
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=200M

module load python

srun python production_script.py
```

---

If you have any questions about estimating resource requirements or interpreting SLURM job reports, please contact REPACSS support.
