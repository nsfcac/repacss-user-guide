# Getting Started at REPACSS

!!! info "About this page"
    This page will guide you through the basics of accessing, connecting to, and beginning work on the REPACSS High-Performance Computing (HPC) cluster.

Welcome to REPACSS — Texas Tech University's research and educational platform for advanced computing support services. This guide is tailored to new users who are preparing to run jobs on the cluster for the first time.

---

## Account Access

To utilize REPACSS resources, users must have a valid TTU account and a [TTUnet VPN access](connecting/vpn.md).

### TTU Users

- Access must be requested through the system administrator.
- A valid institutional email address (ending in `ttu.edu`) is required.
- Provisioning typically takes 2–3 business days after the request is approved.

<!-- ### ACCESS Users

!!! warning
    ACCESS users are currently unable to log in to the REPACSS system. This capability is under development. -->

---

## Multi-Factor Authentication (MFA) and VPN

All users accessing the system remotely must use TTU’s GlobalProtect VPN and have Microsoft Multi-Factor Authentication (MFA) configured.

- [VPN Setup Instructions](connecting/vpn.md)
- [MFA Configuration Guide](connecting/mfa.md)

!!! warning "MFA and VPN required"
    Login attempts from outside the TTU network require both MFA and VPN authentication.

---

## Connecting to the Cluster

Once account provisioning and secure connection setup are complete, users may connect via Secure Shell (SSH):

```bash
ssh <your-ttu-username>@repacss.ttu.edu
```

Access via Visual Studio Code is also supported:

- [Connecting via VSCode](connecting/vscode.md)

!!! tip "First-time login tip"
    On initial login, run `quota -s` to review disk usage, and `module avail` to browse available software modules.

---

!!! note "Storage areas"
    - Use `/home` for scripts and long-term storage.
    - Use `/work` for project-related data under active development.
    - Use `/scratch` for temporary data during compute jobs.

---

## Environment Setup

REPACSS uses an environment module system to manage software packages.

```bash
module avail         # List available modules
module load gcc/12   # Load a specific version
```

Resources:

- [Using Modules](software/module-system.md)
- [Available Software](software/index.md)
---

## Submitting Your First Job

REPACSS employs the SLURM workload manager to schedule jobs.   

!!! tip
    Interactive sessions should be used exclusively for development and debugging purposes. Once your job is ready for full execution, please submit it using a SLURM batch job.
### Sample SLURM Script

```bash
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --output=output.txt
#SBATCH --ntasks=1
#SBATCH --time=00:05:00

srun ./my_program
```

Submit the job with:

```bash
sbatch job.slurm
```

Monitor your job with:

```bash
squeue -u <your-username>
```

Resources:

- [SLURM Job Basics](running-jobs/basics.md)
- [Example Job Scripts](running-jobs/examples.md)

---

## Getting Help

If assistance is required:

- Visit the [Support Page](support.md)
<!-- - Join the REPACSS user Slack workspace (coming soon) -->

---

