# Running Jobs

## Job Types

### 🧪 Interactive Jobs

Run a job interactively on a specific partition:

```bash
interactive -c 8 -p h100
```

### 🗃️ Batch Jobs

Submit job scripts for queued execution:

```bash
sbatch job.sh
sbatch -p zen4 job.sh
sbatch -p h100 job.sh
```

---

## Job Script Templates

### 📄 Basic SLURM Script

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

# Load required modules
module load <your_module>

# Run your application
./my_program
```

### 🐍 Python Job Script

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

# Load modules
module load gcc

# Activate conda environment
source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv

# Execute Python script
python script.py
```

### 🎮 GPU Job Script

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

# Load GPU libraries
module load cuda

# Run your GPU program
./gpu_program
```

---

## Job Management

### 📤 Submitting Jobs

```bash
sbatch job.sh                        # Basic job submission
sbatch --array=1-10 job.sh           # Job array
sbatch --dependency=afterok:12345 job.sh  # Dependent job
```

### 👀 Monitoring Jobs

```bash
squeue -u $USER                      # View jobs by user
squeue -p zen4                       # Jobs on Zen4 partition
squeue -p h100                       # Jobs on H100 partition
```

### ❌ Canceling Jobs

```bash
scancel 12345                        # Cancel by job ID
scancel -u $USER                     # Cancel all jobs for user
scancel -p zen4                      # Cancel jobs in zen4 partition
```

---

## Resource Requests

### 🧮 CPU-Based Jobs

- `--nodes`: Number of compute nodes
- `--ntasks`: Total parallel tasks (often 1 per CPU)
- `--cpus-per-task`: Threads per task
- `--mem`: Memory per node

### 🖥️ GPU-Based Jobs

- `--gres=gpu:1`: Request 1 GPU
- `--gres=gpu:2`: Request 2 GPUs
- `--gres=gpu:4`: Request 4 GPUs

### 🐍 Python Job Tips

- Use `--cpus-per-task` to leverage multithreading
- Allocate sufficient memory via `--mem`
- Reference [Python Environment Setup](python.md) for conda usage

---

## Related Resources

- [System Overview](system-overview.md)
- [Available Software](software.md)
- [File Management](file-management.md)
- [Python Environment Setup](python.md)
- [Support](../support&resources/support.md)
