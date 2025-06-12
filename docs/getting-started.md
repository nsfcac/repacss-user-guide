# Getting Started

Welcome to REPACSS! This guide will walk you through the steps required to access the system, configure your environment, and begin working with high-performance computing resources.

---

## ✅ Prerequisites

### 🔐 Account Access

**Current Users (TTU Test Phase):**
- Active **eRaider** account (TTU)
- Access to **GlobalProtect VPN**

**Future Users (ACCESS Integration):**
- TTU Users: eRaider account  
- ACCESS Users: ACCESS credentials  
- Approved project allocation  
- Completion of required onboarding and training

---

### 💻 System Requirements

Before connecting to REPACSS, ensure the following:

- **SSH Client**  
  - Windows: [MobaXterm](https://mobaxterm.mobatek.net)  
  - macOS/Linux: Terminal application
- **GlobalProtect VPN client**
- **Two-factor authentication (2FA)** (Microsoft MFA)

---

## 📝 Initial Setup

### Step 1: Request Access

1. Ensure your eRaider account is active.
2. Install and configure GlobalProtect VPN:  
   👉 [VPN Setup Guide](vpn/vpn-setup.md)
3. Enable Microsoft Multi-Factor Authentication (MFA):  
   👉 [MFA Setup Instructions](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)
4. Submit an access request to system administrators.

---

### Step 2: Connect to REPACSS

> ⚠️ **Note:** All users must connect via **GlobalProtect VPN**, whether on-campus or off-campus.

#### 🪟 For Windows (MobaXterm)

1. Download and install [MobaXterm](https://mobaxterm.mobatek.net).
2. Launch MobaXterm and create a new SSH session:
   ```
   Host: repacss.ttu.edu
   Username: <your_eRaider_username>
   ```

#### 🍎 For Mac/Linux (Terminal)

1. Open the Terminal.
2. Run the following command:
   ```bash
   ssh <your_eRaider_username>@repacss.ttu.edu
   ```

If successful, you will see the welcome banner:

```
***************************************************************
            Welcome to the REPACSS HPC Cluster

           ▗▄▄▖ ▗▄▄▄▖▗▄▄▖  ▗▄▖  ▗▄▄▖ ▗▄▄▖ ▗▄▄▖
           ▐▌ ▐▌▐▌   ▐▌ ▐▌▐▌ ▐▌▐▌   ▐▌   ▐▌
           ▐▛▀▚▖▐▛▀▀▘▐▛▀▘ ▐▛▀▜▌▐▌    ▝▀▚▖ ▝▀▚▖
           ▐▌ ▐▌▐▙▄▄▖▐▌   ▐▌ ▐▌▝▚▄▄▖▗▄▄▞▘▗▄▄▞▘
```

---

## 🧪 Environment Setup

Once connected to the cluster:

```bash
# Load required modules
module load <module_name>

# Apply your shell settings
source ~/.bashrc

# Optional: set up a Python environment
```
See the [Python Environment Setup](python.md) guide


---

## 🛠 Basic Linux Commands

### 📁 File Navigation

```bash
pwd      # Show current working directory
ls       # List files and directories
cd       # Change directory
```

### 📂 File Management

```bash
cp       # Copy files
mv       # Move or rename files
rm       # Delete files
mkdir    # Create new directory
```

### 🧑‍💻 Job Management with SLURM

```bash
sbatch script.sh         # Submit a batch job
squeue --me              # View your job queue
scancel <job_id>         # Cancel a job
sinfo                    # Show cluster node status
```

---

## 🚀 Next Steps

Once you're connected, check out the following guides:

- 📘 [System Overview](system-overview.md)  
- 🧬 [Running Jobs](running-jobs.md)  
- 📂 [File Management](file-management.md)  
- 🧰 [Available Software](software.md)  
- 🐍 [Python Environment Setup](python.md)

---

## 📎 Additional Resources

- 🎓 [Support & Training](support.md)  
- ❓ [Frequently Asked Questions (FAQ)](faq.md)
