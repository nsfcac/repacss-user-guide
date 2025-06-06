# File Management

## File Systems

All REPACSS nodes—compute, GPU, and login—have access to a shared global file space. Storage is organized into three main directories, automatically configured for each user:

| File System | Directory                         | Environment Variable |
|-------------|-----------------------------------|----------------------|
| Home        | /mnt/GROUPID/home/USERID          | $HOME               |
| Work        | /mnt/GROUPID/work/USERID          | $WORK               |
| Scratch     | /mnt/GROUPID/scratch/USERID       | $SCRATCH            |

Each of these serves a specific purpose:
- **Home**: Persistent personal space for configs, source code, and small data.
- **Work**: Mid-term storage for active projects.
- **Scratch**: Temporary space for job outputs and large, disposable files.

---

## Checking Quotas

Storage quotas are enforced at the group level. You can check your current usage using:

```bash
df -h /mnt/$(id -gn)
```

Example output:

```txt
Filesystem              Size  Used Avail Use% Mounted on
10.102.95.220:/REPACSS  9.1T  162G  9.0T   2% /mnt/REPACSS
```

---

## File Transfer

> ⚠️ **Important:** Avoid using `scp`, `sftp`, `rsync`, or any direct file transfers through login nodes. These methods degrade system performance and are slower than recommended alternatives.

---

### 🚀 Using Globus Connect

REPACSS recommends **Globus Connect** for transferring data in and out of the system. It offers:

- High-throughput, multi-threaded transfers
- Automatic error handling and retries
- Easy-to-use web interface
- No impact on login nodes

---

### 🔧 Setting Up Globus Connect

1. Install Globus Connect Personal:
   - [Windows Guide](https://docs.globus.org/globus-connect-personal-windows-installation-guide/)
   - [macOS Guide](https://docs.globus.org/globus-connect-personal-mac-installation-guide/)
   - [Linux Guide](https://docs.globus.org/globus-connect-personal-linux-installation-guide/)

2. Set up a collection (your local machine)

3. Access REPACSS files:
   - **Endpoint**: `REPACSS`
   - **Paths**:
     - Home: `/home/USERID`
     - Work: `/work/USERID`
     - Scratch: `/scratch/USERID`

---

### 🌐 Transferring Between Sites

Many research institutions have their own Globus endpoints.

To transfer between systems:
1. Identify the remote site’s Globus endpoint.
2. Go to [Globus Web App](https://app.globus.org).
3. Use the transfer interface:
   - **Source**: Your machine or external site
   - **Destination**: `REPACSS`

📬 Questions? Email: `repacss.globus@ttu.edu`

---

## Best Practices

### 🗃️ Storage Usage

- Keep your **home** directory minimal
- Use **scratch** for temporary and large active jobs
- Backup or archive important work in **work**
- Monitor disk usage frequently

### 📤 File Transfer

- Prefer **Globus** for large or multi-file transfers
- Always verify transfer completion
- Remove temporary files post-transfer
- Do not store large datasets in $HOME

---

## Related Resources

- [Getting Started](getting-started.md)
- [Running Jobs](running-jobs.md)
- [Available Software](software.md)
- [Support](../support&resources/support.md)
