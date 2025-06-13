# 📄 Example Job Scripts

This page contains structured job script examples tailored for REPACSS. For terminology and scheduler behavior, refer to the [Job Basics](basics.md) page. These examples are adapted for REPACSS CPU and GPU partitions like `zen4`, `h100`, and `standard`.

---

!!! tip
    On REPACSS, `interactive` jobs in GPU partitions get scheduling priority.

!!! warning
    Each Slurm "cpu" is a hyperthread. Use `--cpu-bind=cores` to pin OpenMP threads to physical cores.

!!! note
    Use `&` to run jobs in parallel and `wait` to synchronize.

---

## 💡 Basic MPI Batch Job (CPU)

Use this script to launch a standard MPI-based application across multiple nodes, where each node runs many MPI ranks.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --time=00:05:00
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=128
#SBATCH --constraint=zen4

srun ./mpi_app
```

</details>

---

## 🔧 Hybrid MPI + OpenMP Job

Hybrid jobs use both MPI for inter-node communication and OpenMP for intra-node threading. Useful for scaling efficiently across sockets.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=2
#SBATCH --cpus-per-task=64
#SBATCH --constraint=zen4
#SBATCH --time=01:00:00

export OMP_NUM_THREADS=64
srun --cpu-bind=cores ./hybrid_app
```

```bash
#!/bin/bash
#SBATCH --nodes=1
#SBATCH --ntasks=28
#SBATCH --cpus-per-task=32
#SBATCH --constraint=zen4
#SBATCH --time=02:00:00

export OMP_NUM_THREADS=32
srun --cpu-bind=cores ./hybrid_app
```

</details>

---

## 🪄 Interactive Jobs

Interactive jobs let you test and debug applications live in a shell on a compute node. Great for prototyping and short runs.

<details>
<summary>Show Script</summary>

```bash
salloc --nodes=1 --ntasks=1 --cpus-per-task=8 --time=01:00:00 --partition=h100
```

</details>

---

## 🔀 Sequential Parallel Jobs

This script runs several parallel jobs one after the other. Useful for workflows that require multiple independent steps.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --nodes=4
#SBATCH --time=01:00:00
#SBATCH --constraint=zen4

srun -N 1 ./job1
srun -N 1 ./job2
srun -N 1 ./job3
```

</details>

---

## ⬆️ Simultaneous Parallel Jobs

Run several parallel jobs at the same time using background execution. Useful for maximizing resource usage in workflows.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --nodes=8
#SBATCH --time=01:00:00
#SBATCH --constraint=zen4

srun -N 2 -n 176 -c 1 --cpu-bind=cores ./a.out &
srun -N 4 -n 432 -c 1 --cpu-bind=cores ./b.out &
srun -N 2 -n 160 -c 1 --cpu-bind=cores ./c.out &
wait
```

</details>

---

## 🚀 GPU Power Capping

Use this script to reduce GPU power usage. Great for energy-aware experiments and optimizing efficiency.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --gres=gpu:1
#SBATCH --constraint=h100
#SBATCH --time=01:00:00

nvidia-smi -pl 200
srun ./gpu_app
```

</details>

---

## 📆 Job Arrays

Submit many similar jobs at once using a single script. Ideal for parameter sweeps and embarrassingly parallel workloads.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --array=0-2
#SBATCH --nodes=1
#SBATCH --constraint=zen4
#SBATCH --time=00:02:00

echo "Running task ID: $SLURM_ARRAY_TASK_ID"
```

</details>

---

## ⚠️ Job Dependencies

Chain jobs together so one starts after another completes successfully. Useful for pipelining stages.

<details>
<summary>Show Script</summary>

```bash
jobid=$(sbatch --parsable job1.sh)
sbatch --dependency=afterok:$jobid job2.sh
```

</details>

---

## 📉 Shared Node Example

Use this when your job doesn’t need an entire node. Helps reduce queue time and resource waste.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --constraint=zen4
#SBATCH --ntasks=2
#SBATCH --cpus-per-task=2
#SBATCH --time=00:05:00

srun --cpu-bind=cores ./a.out
```

</details>

---

## 💻 Open MPI Example

Use Open MPI via `srun` after loading the appropriate module. Ensure compatibility with your compiled binaries.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --nodes=2
#SBATCH --constraint=zen4
#SBATCH --time=01:00:00

module load openmpi
srun ./openmpi_program
```

</details>

---

## ⏳ Preemptible Job

This type of job can be interrupted and restarted. Suitable for workflows that can checkpoint or tolerate interruptions.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH -C zen4
#SBATCH -N 1
#SBATCH --time=24:00:00
#SBATCH --signal=USR1@60 
#SBATCH --requeue

srun ./payload.sh
sleep 120
```

</details>

---

## 🔄 MPMD Example

Run multiple executables under the same job using different resource allocations. Used in coupled or multi-app workflows.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --nodes=3
#SBATCH --constraint=zen4
#SBATCH --time=01:00:00

srun -N 1 -n 64 ./a.out : -N 2 -n 32 ./b.out
```

</details>

---

## 📅 Job Arrays with Dependencies

Combine job arrays with dependencies for more advanced control over batch workflows.

<details>
<summary>Show Script</summary>

```bash
jobid1=$(sbatch --parsable job1.sh)
jobid2=$(sbatch --parsable --dependency=afterok:$jobid1 job2.sh)
jobid3=$(sbatch --parsable --dependency=afterok:$jobid1 job3.sh)
sbatch --dependency=afterok:$jobid2,afterok:$jobid3 final_job.sh
```

</details>

---

## 🤝 Real-Time Job

Submit jobs that need low-latency turnaround, often linked to live experiments or external instruments.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --constraint=zen4
#SBATCH --nodes=2
#SBATCH --ntasks-per-node=128
#SBATCH --time=01:00:00

srun ./mycode.exe
```

</details>

---

## 📂 Heterogeneous Job

Use this format to request different node types (e.g., CPU + GPU) in a single job.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --time=05:00:00

#SBATCH --constraint=zen4
#SBATCH --nodes=2
#SBATCH hetjob
#SBATCH --constraint=h100
#SBATCH --nodes=1

srun --het-group=0 ./cpu_task.sh
srun --het-group=1 ./gpu_task.sh
```

</details>

---

## ❌ Overrun Job

Submit a job using the overrun allocation when your project has exceeded its quota. Supports preemption.

<details>
<summary>Show Script</summary>

```bash
#!/bin/bash
#SBATCH --constraint=zen4
#SBATCH --time=04:00:00
#SBATCH --time-min=01:30:00

srun ./final_job.sh
```

</details>
