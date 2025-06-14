# Example Job Scripts

This page provides structured job script examples adapted for REPACSS. For definitions and scheduler behavior, refer to the [Job Basics](basics.md) page. These examples are designed for CPU and GPU partitions such as `zen4`, `h100`, and `standard`.

---

!!! tip
    Interactive jobs in GPU partitions are granted scheduling priority on REPACSS.

!!! warning
    Each Slurm CPU is a hyperthread. To bind OpenMP threads to physical cores, use `--cpu-bind=cores`.

!!! note
    To run jobs in parallel, use `&`, and use `wait` to synchronize them.

---

## Job Types

Jobs on REPACSS can be submitted in two main forms:

* **Interactive Jobs**: Real-time sessions for testing and debugging.

  ```bash
  salloc -c 8 -p h100
  ```

* **Batch Jobs**: Scheduled jobs submitted via script.

  ```bash
  sbatch job.sh
  sbatch -p zen4 job.sh
  sbatch -p h100 job.sh
  ```

---

## Script Templates

### Basic Job Script

```bash
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --output=test.out
#SBATCH --error=test.err
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --mem=4G

# Load modules
module load

# Run program
./my_program
```

### Python Job Script

```bash
#!/bin/bash
#SBATCH --job-name=python_job
#SBATCH --output=python_job.out
#SBATCH --error=python_job.err
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G

# Load required modules
module load gcc

# Activate conda environment
source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv

# Run Python script
python script.py
```

### GPU Job Script

```bash
#!/bin/bash
#SBATCH --job-name=gpu_test
#SBATCH --output=gpu_test.out
#SBATCH --error=gpu_test.err
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1
#SBATCH --gres=gpu:1

# Load modules
module load cuda

# Run program
./gpu_program
```

---

## Job Management

### Submission

```bash
sbatch job.sh                       # Submit job
sbatch --array=1-10 job.sh          # Submit job array
sbatch --dependency=afterok:12345 job.sh  # Submit with dependency
```

### Monitoring

```bash
squeue -u $USER           # View user's jobs
squeue -p zen4            # View jobs on zen4 partition
squeue -p h100            # View jobs on h100 partition
```

### Control

```bash
scancel 12345             # Cancel a specific job
scancel -u $USER          # Cancel all user's jobs
scancel -p zen4           # Cancel all jobs in zen4 partition
```

---

## Resource Requests

* **CPU Jobs**: Specify `--nodes`, `--ntasks`, `--cpus-per-task`, and `--mem`
* **GPU Jobs**: Include `--gres=gpu:1` or more as needed
* **Python Jobs**:

  * See Python environment setup
  * Use `--cpus-per-task` for multi-threading
  * Set `--mem` appropriately for data requirements

For additional guidance, consult [Slurm Documentation](https://slurm.schedmd.com/documentation.html) and REPACSS-specific resources.
