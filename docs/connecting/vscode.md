# Visual Studio Code

Visual Studio Code is a modern, lightweight IDE (Integrated Development Environment) that supports remote development through SSH. It is highly customizable and offers a wide range of extensions for languages and workflows common in HPC environments, such as Python, C/C++, Fortran, and more.

!!! warning
    Do not connect VS Code to a REPACSS login node. VS Code Remote-SSH starts a VS Code Server and other processes on the remote host, so even an apparently light VS Code session is not permitted on a login node. Request a compute node first and connect VS Code to that allocated node.

!!! success
    Request the compute node from a standard terminal session, not from the VS Code integrated terminal. The `interactive` command performs the setup required for the session.

---

## Create an SSH key pair

If you do not already have an SSH key, create one **on your local computer** before configuring VS Code. Do not generate the key on a REPACSS login or compute node.

If you already have an SSH key that you want to use, skip the generation commands and use that key's path in the `IdentityFile` settings below.

On macOS or Linux, run:

```bash
mkdir -p ~/.ssh
ssh-keygen -t ed25519 -f ~/.ssh/repacss
```

On Windows, open PowerShell and run:

```powershell
New-Item -ItemType Directory -Force "$env:USERPROFILE\.ssh"
ssh-keygen -t ed25519 -f "$env:USERPROFILE\.ssh\repacss"
```

When prompted, enter a passphrase to protect the key. The command creates two files:

- `repacss` — your **private key**. Keep it secret and do not upload or email it.
- `repacss.pub` — your **public key**. This is the file that must be provided through the REPACSS SSH-key registration process. If no registration process has been provided for your account, contact [REPACSS Support](mailto:repacss.support@ttu.edu).

If the registration process asks you to paste the public key, display the complete one-line contents with `cat ~/.ssh/repacss.pub` on macOS/Linux or `Get-Content "$env:USERPROFILE\.ssh\repacss.pub"` in Windows PowerShell.

If a key with this name already exists, do not overwrite it unless you are sure it is no longer needed. Choose another filename and use that same filename in both `IdentityFile` settings in the SSH configuration below.

If REPACSS allows users to register keys through their home directory, copy the public key to your REPACSS account. On Linux, or on macOS if `ssh-copy-id` is installed, run:

```bash
ssh-copy-id -i ~/.ssh/repacss.pub your_ttu_username@repacss.ttu.edu
```

If `ssh-copy-id` is not available, use this macOS/Linux alternative:

```bash
cat ~/.ssh/repacss.pub | ssh your_ttu_username@repacss.ttu.edu 'umask 077; mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys'
```

On Windows PowerShell, run:

```powershell
Get-Content "$env:USERPROFILE\.ssh\repacss.pub" | ssh your_ttu_username@repacss.ttu.edu 'umask 077; mkdir -p ~/.ssh; cat >> ~/.ssh/authorized_keys'
```

These commands copy **only the public key** and may prompt for your REPACSS password and MFA. If REPACSS has given you a different key-registration procedure, follow that procedure instead. Never copy the private key.

Test the key after registration:

```bash
ssh -i ~/.ssh/repacss your_ttu_username@repacss.ttu.edu
```

On Windows PowerShell, use:

```powershell
ssh -i "$env:USERPROFILE\.ssh\repacss" your_ttu_username@repacss.ttu.edu
```

After the public key has been registered, add the private key to your local SSH agent to avoid entering its passphrase repeatedly:

```bash
# macOS/Linux
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/repacss
```

```powershell
# Windows PowerShell
Start-Service ssh-agent
ssh-add "$env:USERPROFILE\.ssh\repacss"
```

If Windows reports that the `ssh-agent` service is disabled, enable **OpenSSH Authentication Agent** in the Windows Services app, then run the commands above again.

---

## Before you begin

Make sure your eRaider account has VPN and MFA enabled (see [VPN Setup](vpn.md) and [MFA Setup](mfa.md)), and that your public SSH key has been registered with REPACSS. The private key must remain on your local computer.

You will also need a local installation of [Visual Studio Code](https://code.visualstudio.com/) and permission to request an interactive Slurm allocation.

---

## Recommended workflow

The following workflow uses an interactive Slurm allocation. The allocation must remain active for as long as VS Code is connected to the compute node.

### 1. Request a compute node

From a normal terminal on your local computer, connect to REPACSS and start an interactive session. Use your actual TTU eRaider username. If you created the key with the commands above, explicitly provide it when making the initial connection. If you are using a different key, replace the path after `-i` with that key's path:

```bash
ssh -i ~/.ssh/repacss your_ttu_username@repacss.ttu.edu
```

On Windows PowerShell, use:

```powershell
ssh -i "$env:USERPROFILE\.ssh\repacss" your_ttu_username@repacss.ttu.edu
```

After you are connected to the login node, request the allocation:

```bash
interactive -p zen4 -c 8 -t 04:00:00
```

Use the partition and resource options appropriate for your work; see [Interactive Sessions](../running-jobs/interactive.md) for more examples. Wait until Slurm grants the allocation and places you on a compute node.

!!! warning
    Do not run `interactive` from the VS Code integrated terminal. Keep the original terminal session open because closing it or exiting the interactive shell can end the allocation and disconnect VS Code.

### 2. Find the allocated node

After the interactive session starts, run `hostname` in the shell on the compute node:

```bash
hostname
```

For additional confirmation, you can display the job ID and the node list:

```bash
echo "$SLURM_JOB_ID"
scontrol show job "$SLURM_JOB_ID" | grep 'NodeList='
```

Record the node name exactly. REPACSS RPC compute-node names generally begin with `rpc-`. The ranges below show naming patterns; the bracket notation is not part of the hostname and should not be copied into `HostName`:

```text
rpc-91-[1-20]
rpc-92-[1-20]
rpc-94-[1-20]
rpc-95-[1-10]
rpc-96-[1-20]
rpc-97-[1-20]
```

For example, `hostname` might return `rpc-91-7`. The name assigned to your job can change each time you request a new allocation, so repeat this step for every new interactive session.

### 3. Add the compute node to your local SSH configuration

Open the SSH configuration file **on your local computer**, not in your REPACSS home directory:

- macOS/Linux: `~/.ssh/config`
- Windows: `C:\Users\YourUsername\.ssh\config`

Keep a login-node entry as the jump host, then add an entry for the node that Slurm assigned. In this example, the assigned node is `rpc-91-7`:

!!! note "About `IdentityFile`"
    `IdentityFile` points to the **private SSH key on your local computer**. In `~/.ssh/repacss`, `~` means your local home directory and `repacss` is the key's filename; it is not a path on REPACSS. This example assumes your key is named `repacss` and has no file extension. If your key has a different name, replace both `IdentityFile ~/.ssh/repacss` lines with its path—for example, `IdentityFile ~/.ssh/id_ed25519` on macOS/Linux or `IdentityFile C:/Users/YourUsername/.ssh/id_ed25519` on Windows. Never share or upload the private-key file.

```ssh
# Login node (jump host)
Host repacss
    HostName repacss.ttu.edu
    User your_ttu_username
    IdentityFile ~/.ssh/repacss
    IdentitiesOnly yes

# Current interactive compute-node allocation
Host repacss-compute
    HostName rpc-91-7
    User your_ttu_username
    IdentityFile ~/.ssh/repacss
    IdentitiesOnly yes
    ProxyJump repacss
```

Replace both instances of `your_ttu_username` with your TTU eRaider username, replace `rpc-91-7` with the node name returned by `hostname`, and confirm that both `IdentityFile` lines point to the private key you use for REPACSS. The `ProxyJump repacss` line tells SSH to reach the compute node through the login node; your local computer does not need direct network access to the compute node.

If your existing `repacss` entry already contains the login-node settings, keep that entry and add only the `repacss-compute` block. When a later allocation uses a different node, update the `HostName` in this block before reconnecting.

On macOS/Linux, ensure the configuration file is private:

```bash
chmod 600 ~/.ssh/config
```

### 4. Test the proxy connection

Open a second local terminal so that the interactive allocation remains running. Test the new alias:

```bash
ssh repacss-compute
hostname
```

The final command should print the allocated compute node, such as `rpc-91-7`. If it prints `repacss` or another login-node name, stop and correct the SSH configuration before opening VS Code.

If you want to test the login-node alias separately, run `ssh repacss` from the same local terminal. This should connect to the login node; exit that session before continuing.

### 5. Connect VS Code to the compute node

1. Install the [Remote - SSH extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) on your local VS Code installation.
2. Open the Command Palette and select **Remote-SSH: Connect to Host...**.
3. Select `repacss-compute` (the alias whose `HostName` is the allocated `rpc-*` node).
4. Complete the authentication prompts and choose the appropriate platform if VS Code asks.
5. Open a folder and use the integrated terminal only for work that belongs to this allocation.

Check the host shown in the lower-left Remote-SSH indicator and run the following in the VS Code terminal:

```bash
hostname
```

It must report the allocated `rpc-*` compute node, never `repacss` or another login node.

## Ending the session

When finished, close the VS Code Remote-SSH window and exit the test SSH connection. Then return to the original terminal running the interactive allocation and run:

```bash
exit
```

This releases the compute-node allocation. VS Code connections are valid only while the allocation is active; when the wall time expires or the allocation is released, the remote VS Code session will disconnect.

!!! warning
    If your home directory on REPACSS exceeds its quota, VS Code Remote-SSH connections may silently fail. Be sure to check your usage and offload files if needed.
