---
title: Introduction to REPACSS
description: Beginner onboarding guide for logging in, navigating storage, and running jobs on the REPACSS HPC cluster.
tags:
  - onboarding
  - login
  - ssh
  - storage
  - slurm
  - modules
  - cluster usage
---

# Introduction to REPACSS: A Beginner’s Guide

!!! info "About this page"
    This document introduces the foundational steps for logging in, navigating storage environments, submitting jobs, and utilizing available software on the REPACSS cluster.

Welcome to REPACSS — Remotely-managed Power Aware Computing Systems and Services at Texas Tech University. This guide is designed for new users, graduate researchers, including educators and others who are beginning their journey in high-performance computing (HPC). 

---

## Accessing the System
Before accessing REPACSS resources, users must be connected to TTUnet or TTUnet VPN.   

!!! tip "TTUnet VPN Usage Cases"
    **On Campus**:   
        **-** You must be connected to **TTUnet**, either via wired Ethernet or the TTUnet Wi-Fi network.    
        **-** Other networks on campus (such as TTUguest or EduRoam) are not supported for direct access.  
    **Off Campus**:   
        **-** If you are connecting from any other network, including TTUguest, EduRoam, or external internet connections, you must use the TTU GlobalProtect Virtual Private Network (VPN).   
        **-** Instructions are available on the [VPN Setup Guide](connecting/vpn.md).   
    **Authentication**: All system access requires secure login via SSH or authorized web-based interfaces.  
    <br> 
    *Note: Users located within the Computer Science Department building may experience restricted access when using TTUnet Wi-Fi. If you encounter connectivity issues, connect via wired Ethernet or enable the VPN to ensure uninterrupted access.*



### SSH Login

To initiate a session:

```bash
ssh <your_username>@repacss.ttu.edu
```

During first-time access, the system may prompt you to verify the server’s RSA key fingerprint. Confirm by typing `yes`. You will then be required to enter your password.

!!! note
    Login nodes are reserved for light activities such as file management and job preparation. Computational jobs must be executed on compute nodes.

---
## System Overview
### Login Node

Login node is intended for **lightweight tasks** only. Users should use it to:

- Edit and manage files  
- Install user-level software or modules  
- Compile code (if lightweight)  
- Submit SLURM job scripts  

!!! warning
    Do not run compute-intensive applications or parallel jobs on the login node.


### Compute Nodes

All computational jobs should be submitted to the **compute nodes** via SLURM. The system includes:

- **110 CPU worker nodes** for general-purpose parallel and serial computing  
- **8 GPU worker nodes** for accelerated workloads (e.g., deep learning, GPU-based simulations)  
- **1 GPU build node** for compiling and testing GPU applications in a controlled environment

Any workload requiring high performance, extended runtime, or parallel execution should be run on these compute nodes.

### System Specifications Summary Table

| Node Type     | Total Nodes | CPU Model                | CPUs/Node | Cores/Node | Memory/Node | Storage/Node   | GPUs/Node | GPU Model                   |
| ------------- | ----------- | ------------------------ | --------- | ---------- | ----------- | -------------- | --------- | --------------------------- |
| CPU Nodes     | 110         | AMD EPYC 9754            | 2         | 256        | 1.5 TB DDR5 | 1.92 TB NVMe   | -         | -                           |
| GPU Nodes     | 8           | Intel Xeon Gold 6448Y    | 2         | 64         | 512 GB      | 1.92 TB SSD    | 4         | NVIDIA H100 NVL (94 GB HBM) |
| Login Nodes   | 3           | AMD EPYC 9254            | 2         | 48         | 256 GB      | 1.92 TB NVMe   | -         | -                           |
| Storage Nodes | 9           | Intel Xeon Gold (varied) | 2         | 8–32       | 512 GB–1 TB | 25.6–583.68 TB | -         | -                           |

---

### Storage System

REPACSS offers multiple storage environments optimized for different use cases:

| Storage Type  | Location              | Environment Variable                            |
|---------------|-----------------------|--------------------------------------------|
| Home          | `/mnt/GROUPID/home/USERID`   | $HOME |
| Scratch       | `/mnt/GROUPID/scratch/USERID`| $SCRATCH |
| Work          | `/mnt/GROUPID/work/USERID`   | $WORK  |

### Checking Quotas
REPACSS storage space usage is currently organized by the REPACSS group. 
Use the following command to display your current file usage:

```bash
$ df -h /mnt/$(id -gn)

Filesystem              Size  Used Avail Use% Mounted on
10.102.95.220:/REPACSS  9.1T  162G  9.0T   2% /mnt/REPACSS
```


---


<!-- ## Submitting Compute Jobs

Users must submit compute jobs through SLURM job scripts. Direct execution of heavy workloads on login nodes is prohibited. -->

<!-- ### Example: Simple Job Script

Create a script file named `hello.sh`: -->
<!-- 
```bash
#!/bin/bash
#SBATCH --job-name=hello
#SBATCH --output=hello.out
#SBATCH --time=00:05:00
#SBATCH --ntasks=1

echo "Hello from REPACSS!"
```

Submit the script using:

```bash
sbatch hello.sh
```

Monitor the job with:

```bash
squeue -u $USER
```
---
 -->


## Software Access and Modules

REPACSS provides software access via the environment module system. This system allows users to load and unload software packages as needed.

### Common Module Commands

```bash
module avail            # List available software modules
module load gcc         # Load a specific module
module list             # View loaded modules
module unload gcc       # Unload a module
```

Users should include required module commands at the beginning of their job scripts.

??? example "Load GCC module"
    For example, to load gcc in a job script:

    ```bash
    module load gcc
    ```
<small>*For additonal details, refer to the [Module System](software/module-system.md) documentation.*</small>

---
## Job Submission with C Program

This example demonstrates the procedure for compiling and executing a basic C program using a SLURM batch script.

### Create your source code
```c
#include <stdio.h>

int main(){
    printf("Hello from my SLURM job.\n");
    return 0;
}
```

### Create your Batch Script(`run_hello.sh`)
```bash
#!/bin/bash
#SBATCH --job-name=hello_job
#SBATCH --output=hello_output.out
#SBATCH --error=hello_error.err
#SBATCH --time=00:05:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=1

module load gcc

gcc hello.c -o hello

./hello
```
<small>*To determine your resource needs, refer to the [Determine Resource Needs](running-jobs/determining-resource-requirements.md) documentation.*</small>

### Submit Your Job
To submit the batch script to the SLURM workload manager, execute the following command:
```bash
sbatch run_hello.sh
```

!!! tip "How to monitor the job status?"
    To monitor the status of the submitted job, use:
    ```bash
    squeue --me
    ```

<small>*For additonal details, refer to the [Job Examples](running-jobs/examples.md) documentation.*</small>

---

## Support and Resources

If issues arise or assistance is required, users are encouraged to:

- Refer to this user guide
- Consult with their research advisor or lab administrator
- Visit the [Support Page](support.md)

!!! tip
    When seeking help, include specific error messages and a description of the attempted job to expedite troubleshooting.

<!-- ---

## Best Practices

As REPACSS is a shared infrastructure, users are expected to adhere to the following guidelines:

- Do not run compute-intensive jobs on login nodes
- Use the scratch directory for temporary data and clean it periodically

---

## Conclusion

With these steps, new users are now equipped with the foundational knowledge to:

- Establish a secure login
- Navigate the storage architecture
- Utilize the module system
- Submit and monitor jobs on the cluster

Users are encouraged to explore the extended documentation to deepen their understanding and optimize their use of REPACSS resources. -->

