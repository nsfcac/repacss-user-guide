# 🧾 Job Queues on REPACSS

This page explains how job queues work on REPACSS and how users can effectively navigate the system to manage their job submissions.

---

## 🧵 What Is a Queue?

When you submit a job on REPACSS, it is placed in a **queue** managed by the **Slurm workload manager**. This queue operates on a priority-based system, meaning jobs are sorted and run based on several factors such as available resources, job size, and scheduling policies.

Think of the queue like a line for a theme park ride—everyone waits their turn, but some might have express passes or meet special conditions that allow them to go sooner. All jobs, regardless of their type, eventually run on the same compute nodes, but some may have shorter wait times based on priority.

---

## 🕒 Queue Wait Times

Jobs may wait in the queue for longer than their actual runtime. This is a normal part of using a shared HPC system. The wait time depends on:

* System load
* Resource availability (number of nodes, CPUs, GPUs, etc.)
* Job size and walltime requested
* Scheduling priority

If your job is small or flexible (for example, it can run on shared nodes or has a short walltime), it may start sooner.

---

## 📋 Viewing the Queue

To check your job’s position and queue status, use the `squeue` command:

```bash
squeue -u $USER
```

This will show all your jobs and their current status (e.g., pending, running). You can also estimate start times with:

```bash
squeue --start -j <job_id>
```

If your job is pending, Slurm will show the reason (e.g., Resources, Priority, Dependency) in the `NODELIST(REASON)` column.

---

## ✅ Job Scheduling Tips

* Submit jobs with accurate resource and time estimates
* Avoid over-requesting nodes or time
* Use shared or interactive modes for smaller or test jobs
* Consider breaking up large jobs into smaller chunks
* Use job arrays when submitting many similar jobs

---

## 🧠 Understanding Job States

Here are the most common job states you’ll encounter:

| State            | Description                                      |
| ---------------- | ------------------------------------------------ |
| `PENDING (PD)`   | Job is waiting for resources to become available |
| `RUNNING (R)`    | Job is currently executing on allocated nodes    |
| `COMPLETED (CD)` | Job finished successfully                        |
| `FAILED (F)`     | Job terminated with an error                     |
| `CANCELLED (CA)` | Job was cancelled by the user or admin           |
| `TIMEOUT (TO)`   | Job ran out of the requested walltime            |

You can check completed jobs using:

```bash
sacct -u $USER --starttime today
```

---

## 🔍 Need Help?

If you’re unsure why your job is not starting, or want help with optimizing your job submission, contact the system administrators or open a support ticket.

Use the `--help` flag with any Slurm command to learn more:

```bash
squeue --help
sacct --help
```

For further help, refer to:

* [Job Basics](basics.md)
* [Example Scripts](examples.md)
* [Monitoring Tools](monitoring.md)
