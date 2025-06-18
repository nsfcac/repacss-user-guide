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
