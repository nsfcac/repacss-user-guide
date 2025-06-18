# Interactive Sessions

This section provides official guidance on initiating interactive sessions on the REPACSS high-performance computing system. Interactive sessions allow users to request computational resources in real time and execute commands directly on compute nodes. This method is particularly suitable for software testing, debugging, exploratory tasks, and graphical application workflows.

!!! warning
    Interactive sessions should be used exclusively for development and debugging purposes. Once your job is ready for full execution, please submit it using a SLURM batch job.

---

## Requesting Interactive Resources

To initiate an interactive session, use the `salloc` command to request computational resources. This command will launch a shell on a compute node once the resources have been successfully allocated.

```bash
salloc --nodes=1 --ntasks=1 --cpus-per-task=8 --time=01:00:00 --partition=zen4
```

REPACSS also provides a predefined alias for simplified interactive session initiation:

```bash
interactive -c 8 -p h100
```

---

## Interactive Sessions on GPU Nodes

When conducting work that requires access to graphical processing units (GPUs), it is mandatory to specify the required number of GPUs using the `--gpus` option:

```bash
salloc --nodes=1 --gpus=4 --time=01:00:00 --partition=h100
```

Within the session, execute applications using the `srun` command with appropriate GPU specifications:

```bash
srun --gpus=4 ./my_gpu_program
```

!!! warning
    If GPU resources are not explicitly requested with the `--gpus` flag, GPU-based applications such as those relying on CUDA may return an error such as:

```
no CUDA-capable device is detected
```

---

## Interactive Sessions on CPU-Only Nodes

For CPU-based workflows, request resources from a CPU-only partition such as `zen4`:

```bash
salloc --nodes=1 --ntasks=1 --cpus-per-task=8 --time=01:00:00 --partition=zen4
```

Once the session begins, users may execute applications directly in the terminal or utilize `srun` for launching parallel tasks:

```bash
srun ./my_cpu_program
```

---

## Resource Allocation Timeout and Immediate Scheduling

By default, interactive job requests will time out if resource allocation is not completed within six (6) minutes. To modify this behavior, the `--immediate` option can be used to set a custom wait limit in seconds:

```bash
# Wait up to 600 seconds (10 minutes) for resources
salloc --nodes=1 --time=01:00:00 --partition=zen4 --immediate=600
```

!!! note
    If your connection is lost, the interactive session will be terminated and any unsaved results may be lost.

---

## Common Issues and Resolutions

- **GPU Execution Errors**: Ensure GPU requests are made consistently in both `salloc` and `srun`.
- **Invalid Account Settings**: If you encounter account-related errors, verify your default allocation or specify a valid project account using the `--account=<project>` flag.
- **Resource Availability**: If resources are not immediately available, consider adjusting your request parameters (e.g., reducing walltime or number of nodes) or selecting a different partition.

---

## Additional Documentation

For further information and related procedures, refer to the following documentation:

- [Running Jobs](basics.md)
- [Job Queues and Scheduling](scheduling.md)
- [Example Job Scripts](examples.md)
