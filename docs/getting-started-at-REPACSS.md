# Getting Started at REPACSS

!!! success "About this page"
    This page will guide you through the basics of accessing, connecting to, and beginning work on the REPACSS High-Performance Computing (HPC) cluster.

Welcome to REPACSS — Texas Tech University's research and educational platform for advanced computing support services. This guide is tailored to new users who are preparing to run jobs on the cluster for the first time.

---

## 🧾 Account Access

To use REPACSS resources, you must have a valid TTU or ACCESS account.

### TTU Users

- Complete the [REPACSS Access Request Form](https://repacss.org/request-access).
- Requires a valid `ttu.edu` email address.
- Access is typically granted within 2–3 business days.

### ACCESS Users

- Must have an [ACCESS allocation](https://access-ci.org).
- Contact REPACSS support with your ACCESS project ID and intended use.

!!! note "Account prerequisites"
    New users must have their accounts approved before attempting to log in to the cluster.

---

## 🔐 Multi-Factor Authentication (MFA) & VPN

To connect to REPACSS, you must be connected to the TTU GlobalProtect VPN and have MFA enabled.

- [VPN Setup Instructions](connecting/vpn.md)
- [MFA Configuration Guide](connecting/mfa.md)

!!! warning "MFA and VPN required"
    All login attempts from outside TTU’s network must be authenticated through VPN and MFA.

---

## 💻 Connecting to the Cluster

Once your account is active and your VPN/MFA setup is complete, connect via SSH:

```bash
ssh <your-ttu-username>@login.repacss.ttu.edu
```

You can also connect via Visual Studio Code:

- [Connecting via VSCode](connecting/vscode.md)

!!! tip "First-time login tip"
    On first login, review your disk quota using `quota -s` and check available modules with `module avail`.

---

## 📁 Transferring Files

You can move data to and from REPACSS using the following methods:

- Command line: `scp`, `rsync`
- GUI: [WinSCP](https://winscp.net), [Cyberduck](https://cyberduck.io)
- [Globus Transfer Guide](file-transfer.md)

!!! note "Storage areas"
    Use `/home` for persistent scripts, `/work` for active jobs, and `/scratch` for temporary data.

---

## ⚙️ Environment Setup

REPACSS uses a module system to manage software:

```bash
module avail         # See available modules
module load gcc/12   # Example: Load GCC 12
```

- [Using Modules](software/module-system.md)
- [Available Software](software/available-software.md)
- [Installing Your Own Packages](software/installing-packages.md)

---

## 🧪 Submitting Your First Job

REPACSS uses the SLURM workload manager. Jobs are submitted using a script like:

```bash
#!/bin/bash
#SBATCH --job-name=test
#SBATCH --output=output.txt
#SBATCH --ntasks=1
#SBATCH --time=00:05:00

hostname
```

Submit the job using:

```bash
sbatch job.slurm
```

Monitor your job with:

```bash
squeue -u <your-username>
```

- [SLURM Job Basics](running-jobs/basics.md)
- [Example Job Scripts](running-jobs/examples.md)

---

## 🆘 Getting Help

Need assistance? Visit the [Support Page](support.md) or join our user Slack (coming soon).

!!! info "Support hours"
    Monday–Friday, 9am–5pm Central Time. Submit tickets via [repacss.org](https://repacss.org).

---

_Last updated: June 12, 2025_
