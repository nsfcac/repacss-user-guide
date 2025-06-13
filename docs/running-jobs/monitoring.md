# Monitoring Jobs

!!! note
    Avoid running multiple instances of `watch squeue` or `watch sqs`. This can overload the scheduler, which is a shared system resource. If you must use watch, do `watch -n 60` and stop the process when you're done.

---

## 🔍 Using `squeue`

`squeue` shows job queue information directly from Slurm. It's useful for checking job status like `PENDING`, `RUNNING`, or `COMPLETED`.

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

## 📋 Using `sacct`

`sacct` displays accounting information for active and completed jobs.

Basic usage:

```bash
sacct
```

Format output by fields:

```bash
sacct --format=JobID,JobName,State,Start,Elapsed
```

Filter by date range:

```bash
sacct -S 2024-06-01 -E 2024-06-13
```

Show failed jobs:

```bash
sacct -X --format=User,JobName,State -s F --start=2024-06-01 --end=now
```

Filter by job ID:

```bash
sacct -j 123456,123457
```

---

## 📈 Using `sstat`

`sstat` reports resource usage for **running** jobs:

```bash
sstat -j 123456 -o JobID,MaxRSS
```

---

## 📊 Using `jobstats`

`jobstats` (Python-based tool) gives a summary of job activity from `sacct`, `squeue`, and `sreport`.

```bash
module load python
jobstats
```

Example:

```bash
jobstats --user elvis --start 2024-06-01 --end 2024-06-13
```

To view options:

```bash
jobstats --help
```

---

## 📮 Email Notifications

Add these lines to your job script to get notified:

```bash
#SBATCH --mail-type=begin,end,fail
#SBATCH --mail-user=your@email.com
```

---

## 🧠 Logging into Compute Nodes

To SSH into a node while your job is running:

1. Find your job's nodes:

   ```bash
   scontrol show job <jobid> | grep -oP 'NodeList=nid(\[.+\]|.+)'
   ```

2. SSH into any of the listed nodes:

   ```bash
   ssh nid000123
   ```

To get the head node:

```bash
scontrol show job <jobid> | grep -oP 'BatchHost=\K\w+'
```

!!! note
    SSH access only works **while the job is running**.

---

## 🧹 Updating or Canceling Jobs

Cancel job:

```bash
scancel 123456
```

Cancel multiple jobs:

```bash
scancel 123456 123457
```

Cancel all your jobs:

```bash
scancel -u $USER
```

Update job time:

```bash
scontrol update jobid=123456 timelimit=02:00:00
```

---

## ⛔ Holding or Releasing Jobs

Hold a job (pause scheduling):

```bash
scontrol hold 123456
```

Release a held job:

```bash
scontrol release 123456
```

Requeue (rerun) a job:

```bash
scontrol requeue 123456
```
