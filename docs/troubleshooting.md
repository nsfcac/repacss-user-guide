# 🔧 Troubleshooting Guide

Welcome to the REPACSS troubleshooting guide. This page provides help for resolving common problems users encounter when connecting, running jobs, transferring files, or managing environments.

---

## 🔐 Login & Connection Issues

### ❌ "Permission denied" when connecting via SSH
**Cause:** Incorrect username, VPN not connected, or wrong password  
**Solution:**
- Verify you are connected to GlobalProtect VPN
- Use your correct eRaider ID:
  ```bash
  ssh your_username@repacss.ttu.edu
  ```
- Make sure your account is approved and active

---

### ❌ SSH hangs or times out
**Cause:** VPN disconnected or blocked network  
**Solution:**
- Reconnect to VPN
- Restart your network connection
- Try from a different network or location

---

### ❌ "Host not found" error  
**Cause:** Incorrect hostname or DNS resolution failure  
**Solution:**
- Use the correct hostname: `repacss.ttu.edu`
- Check your spelling and VPN connection

---

## 📦 Job Submission Issues

### ❌ "sbatch: command not found"
**Cause:** Environment modules not loaded  
**Solution:**
```bash
module load slurm
```

---

### ❌ Job stuck in "PENDING" state
**Cause:** Insufficient resources or job queue overload  
**Solution:**
- Use `squeue -j <job_id>` and check the "REASON" column
- Try changing partition:
  ```bash
  sbatch -p h100 job.sh
  ```

---

### ❌ Job fails with "out of memory"
**Cause:** Job exceeds memory limit  
**Solution:**
- Increase memory in your SLURM script:
  ```bash
  #SBATCH --mem=32G
  ```
- Use `sacct -j <job_id>` to confirm the memory used

---

## 💾 File & Storage Issues

### ❌ "No space left on device"
**Cause:** You’ve exceeded your quota  
**Solution:**
- Check usage:
  ```bash
  df -h /mnt/$(id -gn)
  ```
- Delete or archive old data
- Use `scratch/` for temporary files

---

### ❌ Slow file transfer speed
**Cause:** Using SCP or SFTP instead of Globus  
**Solution:**
- Switch to [Globus Connect](file-transfer.md) (when available)
- Use `dtn.repacss.ttu.edu` for high-performance transfers

---

## 🐍 Python & Environment Issues

### ❌ "conda: command not found"
**Cause:** Miniforge not installed or not sourced  
**Solution:**
```bash
source ~/miniforge3/etc/profile.d/conda.sh
```

---

### ❌ Conda environment fails to activate
**Cause:** Environment not created or corrupted  
**Solution:**
```bash
conda info --envs
conda activate myenv
```
If it fails, try recreating the environment:
```bash
conda create -n myenv python=3.11
```

---

### ❌ Python job fails with "ModuleNotFoundError"
**Cause:** Environment was not activated in job script  
**Solution:**
Ensure your SLURM job includes:
```bash
source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv
```

---

## 📬 Still Need Help?

If your issue isn’t listed here:

1. Check [FAQ](faq.md)
2. Review the [Support Guide](support.md)
3. Contact the team:
   - ✉️ Email: repacss.support@ttu.edu

---

_Last updated: June 2025_
