# Running Jobs

## Job Types {#types}

### Interactive Jobs
```bash
interactive -c 8 -p h100
```

### Batch Jobs
```bash
sbatch job.sh
sbatch -p zen4 job.sh
sbatch -p h100 job.sh
```

## Job Scripts {#scripts}

### Basic Template
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

### Python Template
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

### GPU Template
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

## Job Management {#management}

### Submission
```bash
sbatch job.sh
sbatch --array=1-10 job.sh
sbatch --dependency=afterok:12345 job.sh
```

### Monitoring
```bash
squeue -u $USER
squeue -p zen4
squeue -p h100
```

### Control
```bash
scancel 12345
scancel -u $USER
scancel -p zen4
```

## Resource Requests {#resources}

### CPU Jobs
- `--nodes`: Number of nodes
- `--ntasks`: Number of tasks
- `--cpus-per-task`: CPUs per task
- `--mem`: Memory per node

### GPU Jobs
- `--gres=gpu:1`: Request 1 GPU
- `--gres=gpu:2`: Request 2 GPUs
- `--gres=gpu:4`: Request 4 GPUs

### Python Jobs
- For Python-specific job configurations and environment setup, see [Python Environment Setup](python.md)
- Consider using `--cpus-per-task` for parallel Python processing
- Adjust `--mem` based on your data processing needs

## Related Resources

- [System Overview](system-overview.md)
- [Software](software.md)
- [File Management](file-management.md)
- [Python Environment Setup](python.md)
- [Support](../support&resources/support.md) 