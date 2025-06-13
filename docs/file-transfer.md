# 📂 File Transfer

!!! warning
    The **Globus Connect** service may be unreliable. Please use one of the SSH-based alternatives below for secure and consistent file transfers.

REPACSS supports file transfers using standard tools available on most systems. These include **SCP**, **rsync**, and **SFTP**. All tools use **SSH** for secure authentication.

---

## 📦 SCP (Secure Copy)

SCP is a simple and fast way to copy files between your local machine and REPACSS.

### 🔼 Upload a file

```bash
scp myfile.txt username@login.repacss.ttu.edu:/mnt/DISCL/home/username/
```

### 🔽 Download a file

```bash
scp username@login.repacss.ttu.edu:/mnt/DISCL/home/username/data.csv ./data.csv
```

!!! tip
    Use `-r` to copy directories recursively:  
    `scp -r myfolder/ username@login.repacss.ttu.edu:/mnt/DISCL/home/username/`

---

## 🔁 Rsync (Recommended for Large Transfers)

`rsync` is great for syncing entire folders and resuming interrupted transfers.

### 🔼 Upload a directory

```bash
rsync -avh myfolder/ username@login.repacss.ttu.edu:/mnt/DISCL/home/username/myfolder/
```

### 🔽 Download from REPACSS

```bash
rsync -avh username@login.repacss.ttu.edu:/mnt/DISCL/home/username/project/ ./project/
```

!!! tip
    Add `-P` to track progress and allow resuming:
    ```bash
    rsync -avhP myfolder/ username@login.repacss.ttu.edu:/mnt/DISCL/home/username/
    ```

---

## 🖥️ SFTP (Interactive Terminal)

SFTP allows interactive browsing of files on REPACSS.

### Start session:

```bash
sftp username@login.repacss.ttu.edu
```

### Common SFTP commands:

```bash
cd /mnt/DISCL/home/username/
put myfile.txt     # Upload
get output.log     # Download
ls                 # List directory contents
exit               # Close connection
```

!!! note
    Unlike SCP or rsync, SFTP lets you navigate the remote file structure before transferring.

---

## 🪟 Windows Users

!!! tip
    Windows 10+ includes `scp`, `sftp`, and `ssh` in PowerShell by default.

If you prefer graphical interfaces:

- **[WinSCP](https://winscp.net)** – supports SCP and SFTP
- **[FileZilla](https://filezilla-project.org/)** – easy drag-and-drop transfers

Or use **WSL** to access Linux-style CLI tools like `rsync`.

---

## 🧭 Tips & Troubleshooting

- Always use your **eRaider username**
- Use the **TTUnet VPN** before initiating transfers
- Make sure file paths are correct, especially when uploading to subdirectories

!!! note
    For large files or many files, prefer `rsync` over `scp` due to its error recovery and syncing capabilities.

---

## 🔗 Related Links

- [Connecting to REPACSS](connecting/index.md)
- [VPN Setup Guide](connecting/vpn.md)
