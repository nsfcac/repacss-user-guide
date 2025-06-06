# 🧠 HPC Best Practices

Maximize your productivity and minimize downtime by following these high-performance computing (HPC) best practices when using the REPACSS cluster.

---

## ✅ General Guidelines

- Always **connect through GlobalProtect VPN** before using SSH
- Do not run compute-heavy jobs on login nodes
- Organize your files logically: separate input, output, and scripts
- Use version control (e.g., Git) for your scripts and workflows
- Log important output and job diagnostics

---

## 🧪 Job Submission

### Use Batch Jobs Whenever Possible
```bash
sbatch job_script.sh
```

### Specify Resource Needs Accurately
- Don’t over-request memory or CPUs unless necessary
- Use SLURM directives to match your workload:
  ```bash
  #SBATCH --mem=16G
  #SBATCH --cpus-per-task=4
  ```

### Monitor Your Jobs
```bash
squeue -u $USER
```

### Cancel Jobs Responsibly
```bash
scancel <job_id>
```

---

## 🧹 File & Storage Management

### Use Correct File Spaces
| Type     | Use For                  | Location Example              |
|----------|--------------------------|-------------------------------|
| `$HOME`  | Configs & scripts        | `/mnt/GROUPID/home/USERID`   |
| `$WORK`  | Shared project data      | `/mnt/GROUPID/work/USERID`   |
| `$SCRATCH` | Temporary, high-speed I/O | `/mnt/GROUPID/scratch/USERID` |

### Clean Up Regularly
- Delete unused scratch data
- Archive finished projects
- Monitor quotas:
  ```bash
  df -h /mnt/$(id -gn)
  ```

---

## 🐍 Environment Management

### Use Conda for Reproducibility
- Create named environments per project:
  ```bash
  conda create -n proj_env python=3.11
  conda activate proj_env
  ```

- Export your environment for reuse:
  ```bash
  conda env export > environment.yml
  ```

### Load Only What You Need
- Minimize module clutter:
  ```bash
  module list
  module unload <module>
  ```

---

## 📤 File Transfers

### Use Globus for Large Data Transfers
- Avoid `scp` to login nodes for large datasets
- Follow [file transfer guidelines](file-transfer.md)

---

## ⚙️ Debugging & Optimization

- Use test runs with short time limits:
  ```bash
  #SBATCH --time=00:05:00
  ```
- Log stderr and stdout:
  ```bash
  #SBATCH --output=job.out
  #SBATCH --error=job.err
  ```
- Check node availability:
  ```bash
  sinfo
  ```

---

## 🔒 Security & Conduct

- Never share your credentials
- Don’t store sensitive data without approval
- Follow all usage policies and data retention guidelines

---

## 🧭 Helpful Resources

- [Running Jobs](running-jobs.md)
- [File Management](file-management.md)
- [Software Modules](modules.md)
- [Troubleshooting](troubleshooting.md)
- [Python Setup](python.md)

---

_Stay respectful, efficient, and informed. A little effort in best practices goes a long way in a shared HPC environment._

_Last updated: June 2025_
