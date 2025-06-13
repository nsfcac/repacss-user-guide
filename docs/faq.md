# Frequently Asked Questions

---

## 🔐 Account & Access

### How do I get an account?

To request access to REPACSS:

1. **Submit a request** via the account form at [repacss.org](https://repacss.org)
2. **Complete required training** to ensure familiarity with system use and policies
3. **Review and accept the usage policy**
4. **Wait for approval** — you’ll be notified once your access is granted

### How do I reset my password?

Password resets are handled through your eRaider account at [eraider.ttu.edu](https://eraider.ttu.edu). If you are an ACCESS user, refer to your ACCESS identity portal.

---

## 🖥️ Jobs & Computing

### How do I submit a job?

```bash
sbatch job.sh
sbatch -p zen4 job.sh
sbatch -p h100 job.sh
```

### How do I check my job status?

```bash
squeue -u $USER
squeue -p zen4
squeue -p h100
```

### How do I cancel a job?

```bash
scancel <job_id>
scancel -u $USER
scancel -p zen4
```

---

## 🗃️ Storage & Files

### What are the storage quotas?

- **Home**: 100 GB per user
- **Scratch**: 1 TB per project
- **Archive**: Allocated per project basis

### How do I transfer files?

!!! warning
    Use **Globus** for large or frequent transfers. Use `scp` only for quick one-time needs.

```bash
# Upload to REPACSS
scp file username@login.repacss.org:/mnt/GROUPID/work/USERID/

# Download from REPACSS
scp username@login.repacss.org:/mnt/GROUPID/work/USERID/file ./destination
```

---

## 📦 Software & Environment

### How do I load software?

```bash
module avail
module load <module-name>
module list
```

### How do I request new software?

- Contact the REPACSS support team
- Provide installation instructions and dependencies
- Specify whether it’s for shared use or personal use
- Wait for confirmation from the system admin team