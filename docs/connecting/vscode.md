# Visual Studio Code
Visual Studio Code is a modern, lightweight IDE (Integrated Development Environment) that supports remote development through SSH. It is highly customizable and offers a wide range of extensions for languages and workflows common in HPC environments, such as Python, C/C++, Fortran, and more.

---

## Connecting with VSCode Remote SSH

Connecting to REPACSS via the [Remote - SSH extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh) allows you to edit files, run terminals, and debug code directly on the system — just like you would on your local machine.

By default, VSCode will connect you to a REPACSS **login node**, which is suitable for lightweight tasks like editing code or running small programs. For heavy workloads, you should request access to a compute node using Slurm.

!!! warning
    If your home directory on REPACSS exceeds its quota, VSCode Remote SSH connections may silently fail. Be sure to check your usage and offload files if needed.

---

## SSH Configuration for REPACSS

To streamline your VSCode connection, add the following to your `~/.ssh/config` file **on your local machine**:

```ssh
# Login node configuration
Host repacss
    HostName repacss.hpcc.ttu.edu
    User your_ttu_username
    IdentityFile ~/.ssh/repacss
    IdentitiesOnly yes
    ForwardAgent yes
    LogLevel QUIET
```

If you're on **Windows**, you can add the same block in:
```
C:\Users\YourUsername\.ssh\config
```

Make sure your SSH key is added to your ssh-agent and that your eRaider account has VPN and MFA enabled (see [VPN Setup](vpn.md) and [MFA Setup](mfa.md)).

---

## VSCode Settings

To ensure smooth operation on compute nodes, add the following settings to your VSCode `settings.json`:

```json
"remote.SSH.maxReconnectionAttempts": 2,
"remote.SSH.useFlock": false
```

This prevents file-locking issues and handles session timeouts when your compute allocation ends.

---

## Requesting a Compute Node

Once connected to the REPACSS login node via VSCode or terminal:

```bash
salloc --nodes=1 --ntasks=1 --time=01:00:00 --partition=standard
```

This requests a compute node for 1 hour on the `standard` partition.

Wait for the job to be granted, and note the node name (e.g., `rpc-97-1`):

```bash
salloc: Nodes rpc-97-1 are ready for job
```

---

## Connect to the Compute Node

Now, back in your SSH config, you can optionally create a direct host entry:

```ssh
Host repacss-compute
    HostName rpc-97-1
    ProxyJump repacss
    User your_ttu_username
    IdentityFile ~/.ssh/repacss
    IdentitiesOnly yes
    ForwardAgent yes
    LogLevel QUIET
```

Then in VSCode, press `F1`, choose **Remote-SSH: Connect to Host**, and pick `repacss-compute`.

!!! tip
    Once connected to the compute node, you can compile or run heavier jobs without overloading the login node.
