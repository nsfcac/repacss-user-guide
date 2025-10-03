# Checkpoint/Restart

Checkpoint/restart (C/R) functionality allows you to save the state of a running application and later resume it from that saved state. This is particularly useful for long-running jobs that may be interrupted due to system maintenance, job time limits, or other issues. REPACSS supports transparent checkpoint/restart using DMTCP (Distributed MultiThreaded CheckPointing).

---

## Overview

DMTCP (Distributed MultiThreaded CheckPointing) provides transparent checkpoint/restart capabilities for serial, threaded, and MPI applications. It automatically saves the complete state of your application, including memory, file descriptors, and process state, allowing you to resume execution from exactly where it left off.

### Benefits of Transparent C/R

- **Fault Tolerance**: Resume jobs after system failures or maintenance
- **Time Limit Management**: Extend job execution beyond partition time limits
- **Resource Optimization**: Save computational progress and resume on different nodes
- **Development Efficiency**: Test long-running applications without losing progress

---

## DMTCP on REPACSS

DMTCP is available as a module on REPACSS systems. To use checkpoint/restart functionality:

```bash
module load dmtcp
```

### Key DMTCP Commands

- `dmtcp_launch`: Start an application with checkpointing enabled
- `dmtcp_restart`: Resume an application from a checkpoint
- `dmtcp_command`: Send commands to the DMTCP coordinator
- `dmtcp_coordinator`: Start the DMTCP coordinator (usually automatic)

---

## Checkpoint/Restart for Serial and Threaded Applications

### Interactive Checkpointing

For interactive sessions, you can enable checkpointing when starting your application:

```bash
# Start an interactive session
interactive -c 8 -p zen4

# Load DMTCP module
module load dmtcp

# Launch your application with checkpointing
dmtcp_launch --interval 300 ./my_program
```

The `--interval 300` option creates automatic checkpoints every 5 minutes.

### Manual Checkpointing

You can also create checkpoints manually during execution:

```bash
# Start application with DMTCP
dmtcp_launch ./my_program

# In another terminal, create a checkpoint
dmtcp_command --checkpoint

# Or create a checkpoint and kill the application
dmtcp_command --kcheckpoint
```

### Restarting from Checkpoint

To resume your application from a checkpoint:

```bash
# Restart from the most recent checkpoint
dmtcp_restart ckpt_*.dmtcp

# Or restart from a specific checkpoint
dmtcp_restart ckpt_my_program_*.dmtcp
```

---

## Batch Job Checkpointing

### Basic Batch Job with Checkpointing

Create a job script that enables checkpointing:

```bash
#!/bin/bash
#SBATCH --job-name=checkpoint_job
#SBATCH --output=checkpoint_job.out
#SBATCH --error=checkpoint_job.err
#SBATCH --time=02:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=16G
#SBATCH --partition=zen4

# Load required modules
module load gcc
module load dmtcp

# Set checkpoint directory
export DMTCP_CHECKPOINT_DIR=$PWD/checkpoints
mkdir -p $DMTCP_CHECKPOINT_DIR

# Launch application with automatic checkpointing every 10 minutes
dmtcp_launch --interval 600 --ckptdir $DMTCP_CHECKPOINT_DIR ./my_program
```

### Advanced Batch Job with Manual Checkpointing

For more control over checkpoint timing:

```bash
#!/bin/bash
#SBATCH --job-name=manual_checkpoint
#SBATCH --output=manual_checkpoint.out
#SBATCH --error=manual_checkpoint.err
#SBATCH --time=04:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --partition=zen4

module load gcc
module load dmtcp

# Set checkpoint directory
export DMTCP_CHECKPOINT_DIR=$PWD/checkpoints
mkdir -p $DMTCP_CHECKPOINT_DIR

# Start application without automatic checkpointing
dmtcp_launch --interval 0 --ckptdir $DMTCP_CHECKPOINT_DIR ./my_program &

# Wait for application to start
sleep 30

# Create checkpoints at specific intervals
for i in {1..10}; do
    sleep 1800  # Wait 30 minutes
    dmtcp_command --checkpoint
    echo "Checkpoint $i created at $(date)"
done

wait
```

### Restart Job Script

Create a separate script to restart from checkpoints:

```bash
#!/bin/bash
#SBATCH --job-name=restart_job
#SBATCH --output=restart_job.out
#SBATCH --error=restart_job.err
#SBATCH --time=02:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=16G
#SBATCH --partition=zen4

module load dmtcp

# Restart from the most recent checkpoint
cd $PWD/checkpoints
dmtcp_restart ckpt_*.dmtcp
```

---

## Checkpoint/Restart for MPI Applications

For MPI applications, DMTCP works with MANA (MPI-Agnostic Network-Agnostic) to provide transparent checkpointing:

```bash
#!/bin/bash
#SBATCH --job-name=mpi_checkpoint
#SBATCH --output=mpi_checkpoint.out
#SBATCH --error=mpi_checkpoint.err
#SBATCH --time=02:00:00
#SBATCH --nodes=2
#SBATCH --ntasks=4
#SBATCH --cpus-per-task=2
#SBATCH --mem=32G
#SBATCH --partition=zen4

module load gcc
module load dmtcp

# Set checkpoint directory
export DMTCP_CHECKPOINT_DIR=$PWD/checkpoints
mkdir -p $DMTCP_CHECKPOINT_DIR

# Launch MPI application with checkpointing
dmtcp_launch --interval 600 --ckptdir $DMTCP_CHECKPOINT_DIR srun -n 4 ./my_mpi_program
```

---

## Practical Examples

### Example 1: Long-Running Scientific Simulation

```bash
#!/bin/bash
#SBATCH --job-name=simulation
#SBATCH --output=simulation.out
#SBATCH --error=simulation.err
#SBATCH --time=08:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=16
#SBATCH --mem=64G
#SBATCH --partition=zen4

module load gcc
module load dmtcp

# Create checkpoint directory
export DMTCP_CHECKPOINT_DIR=$PWD/checkpoints
mkdir -p $DMTCP_CHECKPOINT_DIR

# Launch simulation with checkpointing every 30 minutes
dmtcp_launch --interval 1800 --ckptdir $DMTCP_CHECKPOINT_DIR ./simulation_program
```

### Example 2: Machine Learning Training with Checkpoints

```bash
#!/bin/bash
#SBATCH --job-name=ml_training
#SBATCH --output=ml_training.out
#SBATCH --error=ml_training.err
#SBATCH --time=12:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G
#SBATCH --partition=zen4

module load gcc
module load dmtcp

# Activate conda environment
source ~/miniforge3/etc/profile.d/conda.sh
conda activate ml_env

# Set checkpoint directory
export DMTCP_CHECKPOINT_DIR=$PWD/checkpoints
mkdir -p $DMTCP_CHECKPOINT_DIR

# Launch training with checkpointing
dmtcp_launch --interval 3600 --ckptdir $DMTCP_CHECKPOINT_DIR python train_model.py
```

---

## Best Practices

### Checkpoint Frequency

- **Frequent checkpoints**: Use shorter intervals (5-15 minutes) for critical applications
- **Infrequent checkpoints**: Use longer intervals (30-60 minutes) for stable applications
- **Manual checkpoints**: Use `dmtcp_command --checkpoint` for strategic timing

### Storage Considerations

- Checkpoints can be large (several GB for memory-intensive applications)
- Store checkpoints in your home directory or project space
- Clean up old checkpoints regularly to save disk space

### Application Compatibility

- DMTCP works with most standard applications
- Some applications with custom signal handlers may need modification
- Test checkpoint/restart functionality before relying on it for production jobs

---

## Troubleshooting

### Common Issues

**Checkpoint files not created:**
```bash
# Check if DMTCP coordinator is running
dmtcp_command --status

# Verify checkpoint directory permissions
ls -la $DMTCP_CHECKPOINT_DIR
```

**Application fails to restart:**
```bash
# Check checkpoint file integrity
file ckpt_*.dmtcp

# Verify environment variables are set
echo $DMTCP_CHECKPOINT_DIR
```

**Permission errors:**
```bash
# Ensure checkpoint directory is writable
chmod 755 $DMTCP_CHECKPOINT_DIR
```

### Debugging Tips

1. **Enable verbose output:**
   ```bash
   dmtcp_launch --verbose ./my_program
   ```

2. **Check DMTCP logs:**
   ```bash
   dmtcp_command --status
   ```

3. **Test with simple applications first:**
   ```bash
   # Simple test program
   echo 'int main(){while(1)sleep(1);}' > test.c
   gcc test.c -o test
   dmtcp_launch ./test
   ```

---

## Additional Resources

- [DMTCP Documentation](http://dmtcp.sourceforge.net)
- [DMTCP GitHub Repository](https://github.com/dmtcp/dmtcp)
- [Slurm Job Management](basics.md)
- [Interactive Sessions](interactive.md)
- [Job Examples](examples.md)

---

## Support

For checkpoint/restart issues specific to REPACSS, please contact [REPACSS Support](../support.md) with:
- Your job script
- Error messages
- Checkpoint file locations
- Application details
