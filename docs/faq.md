# Frequently Asked Questions

---

## Account and Access

### How do I obtain access to the REPACSS system?

To gain access to the REPACSS high-performance computing environment, please follow the procedure outlined below:

1. Contact the REPACSS support team by email to initiate an access request.
2. Complete any mandatory training to demonstrate understanding of system usage policies and operational guidelines.
3. Review and acknowledge the REPACSS user policy agreement.
4. Await account approval and confirmation from system administrators.

### How do I reset my password?

Password management is handled through the institutional eRaider account system. Users may visit [https://eraider.ttu.edu](https://eraider.ttu.edu) to reset credentials. ACCESS users should consult their ACCESS identity management portal for related instructions.

---

## Job Submission and System Usage

### How do I submit a job?

To submit batch jobs to the Slurm workload manager, use the following command structures:

```bash
sbatch job.sh
sbatch -p zen4 job.sh
sbatch -p h100 job.sh
```

### How do I monitor the status of submitted jobs?

To monitor the status and queue placement of active or pending jobs, use the following commands:

```bash
squeue -u $USER
squeue -p zen4
squeue -p h100
```

### How do I cancel a submitted job?

To terminate an active or pending job, the following commands may be used:

```bash
scancel <job_id>
scancel -u $USER
scancel -p zen4
```

---

## Storage and Data Management

<!-- ### What are the default storage quotas for users?

The following quota allocations are in effect for REPACSS users:

- Home Directory: 100 GB per user
- Scratch Space: 1 TB per project group
- Archive Storage: Assigned on a per-project basis upon request -->

### How do I transfer files to and from the REPACSS system?

**Important Notice:** It is strongly recommended to use Globus for large-scale or frequent data transfers. Secure Copy Protocol (SCP) may be used for infrequent or small transfers.

```bash
# Upload to REPACSS
scp file username@login.repacss.org:/mnt/GROUPID/work/USERID/

# Download from REPACSS
scp username@login.repacss.org:/mnt/GROUPID/work/USERID/file ./destination
```

---

## Software Environment

### How do I view and load available software modules?

The Lmod module system is used to manage available software environments. Use the following commands to access and configure software:

```bash
module avail
module load <module-name>
module list
```

### How do I request the installation of new software?

To request the installation of additional software packages:

1. Contact the REPACSS support team with a formal request.
2. Include installation instructions, dependencies, and intended use case.
3. Indicate whether the request is for shared usage or for individual access.
4. Await review and approval by system administrators.
