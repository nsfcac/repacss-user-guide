# Introduction to REPACSS: A Beginner’s Guide

!!! info "About this page"
    This document introduces the foundational steps for logging in, navigating storage environments, submitting jobs, and utilizing available software on the REPACSS cluster.

Welcome to REPACSS — Remotely-managed Power Aware Computing Systems and Services at Texas Tech University. This guide is designed for new users, including undergraduate students, graduate researchers, and others who are beginning their journey in high-performance computing (HPC). 

---

## Accessing the System

Before accessing REPACSS resources, users must be connected to TTUnet.

### SSH Login

To initiate a session:

```bash
ssh <your_username>@repacss.ttu.edu
```

During first-time access, the system may prompt you to verify the server’s RSA key fingerprint. Confirm by typing `yes`. You will then be required to enter your password.

!!! note
    Login nodes are reserved for light activities such as file management and job preparation. Computational tasks must be executed on compute nodes.

---

## Storage System Overview

REPACSS offers multiple storage environments optimized for different use cases:

| Storage Type  | Location              | Environment Variable                            |
|---------------|-----------------------|--------------------------------------------|
| Home          | `/mnt/GROUPID/home/USERID`   | $HOME |
| Scratch       | `/mnt/GROUPID/scratch/USERID`| $WORK |
| Work          | `/mnt/GROUPID/work/USERID`   | $SCRATCH  |


---

## Submitting Compute Jobs

Users must submit compute jobs through SLURM job scripts. Direct execution of heavy workloads on login nodes is prohibited.

### Example: Simple Job Script

Create a script file named `hello.sh`:

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

!!! example
    For example, to load Python in a job script:

    ```bash
    module load python
    ```

---

## Support and Resources

If issues arise or assistance is required, users are encouraged to:

- Refer to this user guide
- Consult with their research advisor or lab administrator
- Visit the [Support Page](support.md)

!!! tip
    When seeking help, include specific error messages and a description of the attempted task to expedite troubleshooting.

---

## Best Practices

As REPACSS is a shared infrastructure, users are expected to adhere to the following guidelines:

- Do not run compute-intensive tasks on login nodes
- Use the scratch directory for temporary data and clean it periodically

---

## Conclusion

With these steps, new users are now equipped with the foundational knowledge to:

- Establish a secure login
- Navigate the storage architecture
- Utilize the module system
- Submit and monitor jobs on the cluster

Users are encouraged to explore the extended documentation to deepen their understanding and optimize their use of REPACSS resources.

_Last updated: June, 2025_
