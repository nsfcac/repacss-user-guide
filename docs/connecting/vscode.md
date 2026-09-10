# Visual Studio Code

Visual Studio Code is a modern, lightweight IDE (Integrated Development Environment) that supports remote development through SSH. It is highly customizable and offers a wide range of extensions for languages and workflows common in HPC environments, such as Python, C/C++, Fortran, and more.

!!! warning
    Do not connect VS Code to a REPACSS login node. VS Code Remote-SSH starts a VS Code Server and other processes on the remote host, so even an apparently light VS Code session is not permitted on a login node. Request a compute node first and connect VS Code to that allocated node.

!!! success
    Request the compute node from a standard terminal session, not from the VS Code integrated terminal. The `interactive` command performs the setup required for the session.

---

## Recommended workflow

The following workflow uses an interactive Slurm allocation. The allocation must remain active for as long as VS Code is connected to the compute node.

### 1. Request a compute node

From a normal terminal on your local computer, connect to REPACSS and start an interactive session. For example:

```bash
ssh repacss
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

Record the node name exactly. The REPACSS RPC compute-node names are in these ranges:

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

```ssh
# Login node (jump host)
Host repacss
    HostName repacss.hpcc.ttu.edu
    User your_ttu_username
    IdentityFile ~/.ssh/repacss
    IdentitiesOnly yes
    ForwardAgent yes
    LogLevel QUIET

# Current interactive compute-node allocation
Host repacss-compute
    HostName rpc-91-7
    User your_ttu_username
    IdentityFile ~/.ssh/repacss
    IdentitiesOnly yes
    ProxyJump repacss
    ForwardAgent yes
    LogLevel QUIET
```

Replace both instances of `your_ttu_username` with your TTU eRaider username, and replace `rpc-91-7` with the node name returned by `hostname`. The `ProxyJump repacss` line tells SSH to reach the compute node through the login node; your local computer does not need direct network access to the compute node.

If your existing `repacss` entry already contains the login-node settings, keep that entry and add only the `repacss-compute` block. When a later allocation uses a different node, update the `HostName` in this block before reconnecting.

On macOS/Linux, ensure the configuration file is private:

```bash
chmod 600 ~/.ssh/config
```

### 4. Test the proxy connection

Open a second local terminal so that the interactive allocation remains running, then test the new alias:

```bash
ssh repacss-compute
hostname
```

The final command should print the allocated compute node, such as `rpc-91-7`. If it prints `repacss` or another login-node name, stop and correct the SSH configuration before opening VS Code.

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

---

## SSH Configuration prerequisites

Before using the configuration above, make sure your SSH key is added to your ssh-agent and that your eRaider account has VPN and MFA enabled (see [VPN Setup](vpn.md) and [MFA Setup](mfa.md)).

You can verify the login-node alias independently with:

```bash
ssh repacss
```

Use `ssh repacss-compute` only after you have an active Slurm allocation on the node named in its `HostName` setting. Do not use the compute-node alias after the allocation has ended, because compute nodes are not general-purpose login hosts.
