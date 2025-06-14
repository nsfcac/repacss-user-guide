# Job Queues on REPACSS

This page provides a comprehensive explanation of job queuing mechanisms on REPACSS and guidance for users on how to effectively manage their job submissions.

---

## Queue Overview

When a user submits a job to the REPACSS system, it is placed into a queue controlled by the Slurm workload manager. This queue is governed by a priority-based scheduling system, where jobs are executed based on criteria such as resource availability, job size, requested walltime, and policy-defined priorities.

Although all jobs are executed on the same underlying compute nodes, the order in which they begin is determined by these scheduling policies. Some jobs, especially those with smaller resource demands or shorter walltimes, may experience shorter wait times.

---

## Queue Wait Times

It is typical for submitted jobs to remain in the queue for a duration longer than their execution time. Factors influencing wait times include:

* Current system workload
* Availability of requested resources (e.g., nodes, CPUs, GPUs)
* Size and duration of the job
* Assigned job priority

Smaller or flexible jobs may benefit from earlier scheduling through the backfill mechanism.

---

## Viewing the Queue

Users may inspect the status of their queued jobs with the following command:

```bash
squeue -u $USER
```

To estimate when a job is expected to start, use:

```bash
squeue --start -j <job_id>
```

Pending jobs will include a status reason under the `NODELIST(REASON)` column, indicating why execution has not yet begun (e.g., "Resources", "Priority", or "Dependency").

---

## Scheduling Mechanics

REPACSS employs Slurm to manage job execution and optimize resource utilization.

### Priority and Job Aging

Each job is assigned a priority value that increases over time through a mechanism known as aging. This process ensures that jobs do not remain indefinitely in the queue. However, to maintain fairness, only a limited number of jobs per user can accumulate priority concurrently.

This approach prevents individual users from monopolizing the scheduling queue and promotes equitable access for all users.

### Scheduling Algorithms

Slurm uses two complementary scheduling strategies:

* **Immediate Scheduling**: Rapidly assembles a tentative schedule using the highest-priority jobs.
* **Backfill Scheduling**: Identifies and executes smaller jobs that can be run in time gaps without delaying higher-priority jobs.

This hybrid model enables efficient system utilization while allowing for the timely execution of short-duration tasks. Because the schedule is recalculated frequently, job start times shown by the scheduler may fluctuate.

---

## Recommendations for Efficient Scheduling

To minimize queue wait times and maximize job throughput, users are encouraged to:

* Provide accurate resource and time estimates
* Avoid requesting excessive compute resources
* Utilize interactive or shared job modes for testing
* Decompose large workflows into smaller, manageable tasks
* Employ job arrays for repetitive or parameterized workloads

---

## Interpreting Job States

Below is a summary of common Slurm job states:

| State            | Description                                   |
| ---------------- | --------------------------------------------- |
| `PENDING (PD)`   | Waiting for resources to become available     |
| `RUNNING (R)`    | Currently executing on allocated resources    |
| `COMPLETED (CD)` | Successfully finished execution               |
| `FAILED (F)`     | Terminated due to an error                    |
| `CANCELLED (CA)` | Cancelled by the user or system administrator |
| `TIMEOUT (TO)`   | Exceeded requested walltime                   |

To view historical job information:

```bash
sacct -u $USER --starttime today
```

---

## Additional Support

If a job remains in the queue unexpectedly or assistance is needed for job optimization, users may contact the system administrators or file a support request.

Help documentation for Slurm commands is also available:

```bash
squeue --help
sacct --help
```

Related documentation includes:

* [Job Basics](basics.md)
* [Example Scripts](examples.md)
* [Monitoring Tools](monitoring.md)
