# Running Jobs

## Job Types {#types}

### Interactive Jobs
```bash
srun --pty bash
srun -p zen4 --pty bash
srun -p h100 --pty bash
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
module load default

# Run program
./my_program
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

## Related Resources

- [System Overview](system-overview.md)
- [Software](software.md)
- [File Management](file-management.md)
- [Support](../support&resources/support.md) 