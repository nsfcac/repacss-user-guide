# Best Practices for REPACSS Users

This document provides formal guidance for effective and responsible utilization of the REPACSS computing infrastructure. Adherence to these practices ensures optimal system performance, equitable access for all users, and improved job throughput across the cluster.

---

## General Usage Recommendations

Users are required to specify realistic job durations using the `--time` directive. Accurately estimating wall time enables efficient scheduling and backfilling, while overestimation may delay other users’ jobs. Underestimation, on the other hand, may result in the premature termination of running jobs.

Resource requests submitted via `--nodes`, `--ntasks`, and `--cpus-per-task` must reflect the actual needs of the application. Unnecessary overprovisioning leads to inefficient use of shared computing resources and may increase queue times.

When submitting large numbers of similar short jobs, it is advisable to use job arrays via the `--array` directive. This approach significantly reduces the overhead imposed on the job scheduler.

To ensure fair usage, users must refrain from launching multiple monitoring commands in parallel, such as multiple instances of `watch squeue`. If use of `watch` is necessary, the polling interval should be set to 60 seconds or longer.

Users are encouraged to automate job submission and data processing workflows through the use of scripts. This practice promotes consistency, reduces manual errors, and supports long-term reproducibility.

Project directories should be organized in a structured manner. Output files, logs, and job scripts should be stored in logically named subdirectories to facilitate navigation and archival.

---

## Development and Production Job Workflow

Prior to submitting large-scale jobs, users must perform validation using short, small-scale test jobs. Such tests should employ reduced node counts and minimal wall time limits to identify and resolve application errors efficiently.

After successful execution of a small-scale job, users may scale up their resource requests incrementally. This ensures that production jobs are submitted only after validating the program’s correctness and performance.

For debugging and development purposes, users are **strongly encouraged** to initiate interactive sessions using the `interactive` command rather than calling `salloc` directly. The `interactive` command handles additional environment configuration and resource setup critical for successful session initialization.

A one-hour interactive session using one or two compute nodes is generally sufficient for most diagnostic tasks. For example:

```bash
interactive -c 8 -p zen4
```

!!! tip  
    Using the `interactive` command is the officially recommended method for launching temporary, real-time compute jobs. Avoid using `salloc` directly, especially when working through environments like Visual Studio Code or remote shells, as this may bypass necessary setup steps.

Upon completion of any job, users should assess system utilization using tools such as `sacct`, `sstat`, or `jobstats`. This post-job analysis enables performance tuning and resource optimization.

---

## Job Submission and Scheduling Conduct

Repeated cancellation and resubmission of jobs is discouraged. Doing so interferes with the efficiency of the job scheduler and may negatively impact the scheduling of other users’ jobs.

In cases where a job should be temporarily paused, the recommended procedure is to place the job on hold using the `scontrol hold` command. Once the job is ready for execution, it can be released using `scontrol release`.

Users must cancel any jobs that are no longer required or that have remained in the pending state for extended periods without justification. The `scancel` command should be used to remove such jobs from the queue promptly.

---

## Monitoring and Diagnostic Tools

During job execution, users may retrieve diagnostic information by executing `scontrol show job <jobid>` and identifying the compute nodes assigned to the job. Secure shell (SSH) access to these nodes is permitted only while the job is actively running.

Monitoring tools such as `squeue`, `sacct`, and `jobstats` are available for tracking job states, resource utilization, and job history. When using the `watch` utility for monitoring, users must ensure that the polling interval does not fall below 60 seconds to minimize scheduler impact.

To receive email notifications on job state changes, users may include the following SLURM directives in their job submission scripts:

```bash
#SBATCH --mail-type=begin,end,fail
#SBATCH --mail-user=you@example.com
```

---

## File Management and Data Storage

Upon job completion, users are expected to delete all temporary files, logs, and intermediate data that are no longer needed. This ensures sufficient storage space is available for all users.

Users should regularly archive output data to long-term storage systems or transfer it to local infrastructure. Large result sets should not remain on cluster storage indefinitely.

To avoid exceeding storage quotas, users must monitor disk usage and maintain a manageable project footprint. File compression and proper archiving practices are encouraged.

---

## Documentation and Research Reproducibility

Users must document all job parameters, including SBATCH directives, environment configurations, input datasets, and output expectations. These records are critical for reproducing results and auditing scientific workflows.

Version control systems such as Git should be used to track source code, job scripts, and configuration files. Committing all components of a research workflow ensures consistency and traceability.

Each project directory should include a README file that describes the folder structure, data input requirements, and interpretation of output files. This is especially important in collaborative environments.

---

## Collaboration and Support Channels

In collaborative projects, shared scripts must be clearly documented and free of user-specific paths or variables. Project members should coordinate job submissions to avoid contention for resources.

If technical issues arise, users are expected to submit a support ticket through the appropriate channels. The request should include job IDs, error logs, and relevant command history.

All users should stay informed of REPACSS operational updates by monitoring official announcements, maintenance notifications, and policy changes issued by the system administrators.

---

For further assistance, please consult the [Support page](../support.md).
