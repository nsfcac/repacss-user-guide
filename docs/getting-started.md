# Getting Started

## Prerequisites

### ✅ Account Access

**Current Users (TTU Test Phase)**  
- Valid **eRaider** account (TTU)
- Access to **GlobalProtect VPN**

**Future Users (Post ACCESS Integration)**  
- TTU Users: eRaider account  
- ACCESS Users: ACCESS account  
- Active project allocation  
- Completed required training

---

### 🖥 System Requirements

- SSH client  
  *(e.g., [MobaXterm](https://mobaxterm.mobatek.net) for Windows, Terminal for Mac/Linux)*
- GlobalProtect VPN client
- Two-factor authentication (2FA) enabled

---

## Initial Setup

### 📝 Request Access

1. Ensure your **eRaider** account is active.
2. Install & configure GlobalProtect VPN:  
   👉 [VPN Setup Guide](vpn/vpn-setup.md)
3. Set up two-factor authentication:  
   👉 [Microsoft MFA Setup](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)
4. Contact the system administrators to request access.

---

### 🔐 Connect to REPACSS

> ⚠️ **Important:** All users (on-campus or off-campus) must connect via **GlobalProtect VPN**.

#### For Windows (MobaXterm)

1. Install [MobaXterm](https://mobaxterm.mobatek.net)
2. Open it and create a new SSH session:
   ```
   Host: repacss.ttu.edu  
   Username: <your_eRaider_username>
   ```

#### For Mac / Linux

1. Open your terminal.
2. Connect using SSH:
   ```bash
   ssh <your_eRaider_username>@repacss.ttu.edu
   ```

After entering your password, you should see:

```
***************************************************************
            Welcome to the REPACSS HPC Cluster

           ▗▄▄▖ ▗▄▄▄▖▗▄▄▖  ▗▄▖  ▗▄▄▖ ▗▄▄▖ ▗▄▄▖
           ▐▌ ▐▌▐▌   ▐▌ ▐▌▐▌ ▐▌▐▌   ▐▌   ▐▌
           ▐▛▀▚▖▐▛▀▀▘▐▛▀▘ ▐▛▀▜▌▐▌    ▝▀▚▖ ▝▀▚▖
           ▐▌ ▐▌▐▙▄▄▖▐▌   ▐▌ ▐▌▝▚▄▄▖▗▄▄▞▘▗▄▄▞▘
```

---

### 🧪 Environment Setup

Once logged in:

```bash
# Load necessary modules
module load <module_name>

# Source your environment settings
source ~/.bashrc

# (Optional) Set up Python via Miniforge
# See: Python Environment Setup guide
```

---

## 🛠 Basic Commands

### File Navigation

```bash
pwd     # Show current directory
ls      # List files
cd      # Change directory
```

### File Management

```bash
cp      # Copy files
mv      # Move or rename files
rm      # Remove files
mkdir   # Create a new directory
```

### Job Management

```bash
sbatch script.sh       # Submit a SLURM job
squeue -u <username>   # Check your job queue
scancel <job_id>       # Cancel a job
sinfo                  # Show node/cluster status
```

---

## 🚀 What’s Next?

Continue learning with these resources:

- 📘 [System Overview](system-overview.md)  
- 🧬 [Running Jobs](running-jobs.md)  
- 📂 [File Management](file-management.md)  
- 🧰 [Available Software](software.md)  
- 🐍 [Python Setup](python.md)

---

## 🔗 Related Resources

- 🎓 [Training & Support](support.md)  
- ❓ [FAQ](faq.md)
