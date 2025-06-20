# REPACSS Command Cheatsheet

Quick reference for commonly used commands and options on REPACSS.

---

## Job Submission

```bash
sbatch job.sh                    # Submit a batch job
interactive -c 8 -p zen4         # Start an interactive session (recommended)
srun ./program                   # Run a job step
```

!!! tip  
    Always use the `interactive` command for starting real-time sessions. It properly configures the environment and avoids common issues that arise when using `salloc` directly.

---

## Monitoring Jobs

```bash
squeue -u $USER                  # Show your jobs
sqs                              # Enhanced view of job queue
scontrol show job <jobid>       # Job details
```

---

## Cancel Jobs

```bash
scancel <jobid>                  # Cancel specific job
scancel -u $USER                 # Cancel all your jobs
```

---

## Modules

```bash
module avail                     # List available modules
module load gcc/12.2.0           # Load specific module
module list                      # Show loaded modules
module unload gcc/12.2.0         # Unload module
```

---

## Software Setup

```bash
conda activate myenv             # Activate Python environment
pip install mypackage            # Install Python package
spack install hdf5               # Install with Spack
```

---

## File Management

```bash
ls -lh                           # List files with size
du -sh *                         # Check folder sizes
df -h                            # Check disk usage
```

---

## Environment Variables

```bash
export OMP_NUM_THREADS=8         # Set OpenMP threads
export SBATCH_ACCOUNT=m1234      # Set default Slurm account
```

---

## Performance

```bash
time ./program                   # Quick runtime check
perf stat ./program              # Performance statistics (Linux)
```

---

## Help and Docs

```bash
man sbatch                       # Manual for sbatch
squeue --help                    # Help for squeue
module help gcc                  # Help for module
```
