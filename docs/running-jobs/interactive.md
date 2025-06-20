# Interactive Sessions

This section provides official guidance on initiating interactive sessions on the REPACSS high-performance computing system. Interactive sessions allow users to request computational resources in real time and execute commands directly on compute nodes. This method is particularly suitable for software testing, debugging, exploratory tasks, and graphical application workflows.

!!! warning  
    Interactive sessions should be used exclusively for development and debugging purposes. Once your job is ready for full execution, please submit it using a SLURM batch job and `exit` from the resources.

---

## Requesting Interactive Resources

To start an interactive session, use the `interactive` command. This command wraps around the resource request process, performs additional setup, and launches a shell on a compute node once resources are allocated.

```bash
interactive -c 8 -p h100
```

This method is the **recommended** way to start interactive sessions on REPACSS.

!!! tip  
    Do not call `salloc` directly unless instructed otherwise. The `interactive` command performs important environment configuration steps that `salloc` alone does not handle.

---

## Interactive Sessions on GPU Nodes

When working with graphical processing units (GPUs), use the `interactive` command with the appropriate GPU partition and core count. For example:

```bash
interactive -c 8 -p h100
```

Within the session, use `srun` to launch your GPU applications:

```bash
srun --gres=gpu:nvidia_h100_nvl:1 ./my_gpu_program
```

!!! warning  
    If GPU resources are not explicitly requested, applications relying on GPU acceleration (e.g., CUDA) may fail with an error such as:

```
no CUDA-capable device is detected
```

---

## Interactive Sessions on CPU-Only Nodes

For CPU-only workloads, use the `interactive` command with a CPU-only partition such as `zen4`:

```bash
interactive -c 8 -p zen4
```

Once the session begins, you can run programs directly or use `srun` for launching parallel tasks:

```bash
srun ./my_cpu_program
```

---

## Resource Allocation Timeout and Immediate Scheduling

By default, interactive job requests will time out if resource allocation is not completed within six (6) minutes. If needed, a custom wait limit can be applied using:

```bash
interactive -c 8 -p zen4 --immediate=600
```

This example waits up to 600 seconds (10 minutes) for compute resources.

!!! note  
    If your connection is lost, the interactive session will terminate and any unsaved progress may be lost.

---

## Common Issues and Resolutions

- **GPU Execution Errors**: Confirm that GPU resources are requested in the interactive session and in any `srun` commands.
- **Invalid Account Settings**: Contact [REPACSS Support](../support.md).
- **Unavailable Resources**: If nodes are unavailable, consider lowering resource requests or choosing a less busy partition.

---

## Additional Documentation

- [Running Jobs](basics.md)  
- [Job Queues and Scheduling](scheduling.md)  
- [Example Job Scripts](examples.md)
