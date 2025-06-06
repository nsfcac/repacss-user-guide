# File Transfer Guide

> ⚠️ **Notice:** *Globus Connect is currently unavailable.*  

---



Efficient file transfer is essential for working with data on the REPACSS HPC cluster. This guide outlines best practices and supported methods.

---

## 🚫 Avoid Direct SCP/SFTP/Rsync to Login Nodes

To preserve login node performance, **do not** use:
- `scp`
- `sftp`
- `rsync` directly to login nodes

Instead, use **Globus Connect** for large and reliable transfers.

---

## 🌐 Using Globus Connect

### ✅ Benefits
- High-speed, parallel data transfer
- Automatic retry on failure
- Web interface for ease of use
- No load on login nodes

### 🔧 Setup Steps

1. Install Globus Connect Personal:
   - [Windows Guide](https://docs.globus.org/globus-connect-personal-windows-installation-guide/)
   - [Mac Guide](https://docs.globus.org/globus-connect-personal-mac-installation-guide/)
   - [Linux Guide](https://docs.globus.org/globus-connect-personal-linux-installation-guide/)

2. Create a personal endpoint (your local computer)

3. Search for endpoint: `REPACSS`

4. Authenticate with your TTU credentials

5. Select paths:
   - `/home/USERNAME`
   - `/scratch/USERNAME`
   - `/work/USERNAME`

6. Start transfers using the web portal

> 📧 Questions? Contact: repacss.globus@ttu.edu

---

## 📂 Best Practices

- Use **scratch** for active workloads, not for archiving
- Store long-term data in **archive** locations
- Monitor your quota usage: `df -h /mnt/$(id -gn)`
- Clean up temporary or unused data

---

## 🔗 Related Docs

- [File Management](file-management.md)
- [System Overview](system-overview.md)
- [Getting Started](getting-started.md)
