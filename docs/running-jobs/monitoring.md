# Monitoring Jobs

!!! note
    Avoid running multiple instances of `watch squeue` or `watch sqs`. This can overload the scheduler, which is a shared system resource. If you must use watch, use `watch -n 60` and stop the process when finished.

---

## Using `squeue`

The `squeue` command provides real-time job queue information directly from the Slurm scheduler. It is helpful for checking the current state of jobs, such as `PENDING`, `RUNNING`, or `COMPLETED`.

```bash
squeue --me          # Shows your jobs
squeue -u $USER      # Equivalent to --me
squeue --me -t R     # Only running jobs
squeue --me -t PD    # Only pending jobs
squeue -j 1234,1235  # Filter by job IDs
```

To show jobs by account:

```bash
squeue -A your_project_name
```

To view job steps:

```bash
squeue --steps 1001.0
```

---

## Using `sacct`

The `sacct` command retrieves accounting information about active and completed jobs.

Basic usage:

```bash
sacct
```

Customize output by specifying fields:

```bash
sacct --format=JobID,JobName,State,Start,Elapsed
```

Filter jobs by date:

```bash
sacct -S 2024-06-01 -E 2024-06-13
```

Display only failed jobs:

```bash
sacct -X --format=User,JobName,State -s F --start=2024-06-01 --end=now
```

Filter by specific job IDs:

```bash
sacct -j 123456,123457
```

---

## Using `sstat`

Use `sstat` to report resource usage for jobs that are currently running:

```bash
sstat -j 123456 -o JobID,MaxRSS
```

---

## Using `jobstats`

`jobstats` is a Python-based reporting tool that summarizes job activity using data from `sacct`, `squeue`, and `sreport`.

```bash
module load python
jobstats
```

Example usage:

```bash
jobstats --user elvis --start 2024-06-01 --end 2024-06-13
```

To display all options:

```bash
jobstats --help
```

---

## Email Notifications

To receive notifications when your job begins, ends, or fails, add the following directives to your Slurm job script:

```bash
#SBATCH --mail-type=begin,end,fail
#SBATCH --mail-user=your@email.com
```

---

## Accessing Compute Nodes During Job Execution

To securely access a compute node while your job is running:

1. Determine the node list assigned to your job:

   ```bash
   scontrol show job <jobid> | grep -oP 'NodeList=nid(\[.+\]|.+)'
   ```

2. SSH into any of the listed nodes:

   ```bash
   ssh nid000123
   ```

To identify the batch host:

```bash
scontrol show job <jobid> | grep -oP 'BatchHost=\K\w+'
```

!!! note
    You can only SSH into compute nodes while your job is actively running.

---

## Modifying or Canceling Jobs

To cancel a job:

```bash
scancel 123456
```

To cancel multiple jobs:

```bash
scancel 123456 123457
```

To cancel all jobs submitted by your user:

```bash
scancel -u $USER
```

To update a job’s time limit:

```bash
scontrol update jobid=123456 timelimit=02:00:00
```

---

## Holding, Releasing, and Requeuing Jobs

Place a job on hold (prevent scheduling):

```bash
scontrol hold 123456
```

Release a held job:

```bash
scontrol release 123456
```

Requeue a job (e.g., after failure or timeout):

```bash
scontrol requeue 123456
```
