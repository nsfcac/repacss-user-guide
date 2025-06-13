# 🎮 Interactive Sessions

Interactive sessions allow users to allocate resources in real time to run commands directly on compute nodes. This is useful for debugging, exploratory work, or running graphical applications. REPACSS supports interactive job allocation via the Slurm `salloc` command.

---

## 🚀 Allocating Resources

Use `salloc` to request an interactive session. This launches a shell on a compute node with the requested resources.

```bash
salloc --nodes=1 --ntasks=1 --cpus-per-task=8 --time=01:00:00 --partition=zen4
```

Or use the shortcut alias available on REPACSS:

```bash
interactive -c 8 -p h100
```

---

## 🎛️ Interactive Jobs on GPU Nodes

When working with GPU nodes, make sure to specify GPU resources:

```bash
salloc --nodes=1 --gpus=4 --time=01:00:00 --partition=h100
```

Then, within the session, use `srun` with GPU flags:

```bash
srun --gpus=4 ./my_gpu_program
```

!!! warning
    If you do not request GPUs with `--gpus`, CUDA applications may fail with errors like:

```
no CUDA-capable device is detected
```

---

## 🖥️ Interactive Jobs on CPU Nodes

To run on a CPU-only partition:

```bash
salloc --nodes=1 --ntasks=1 --cpus-per-task=8 --time=01:00:00 --partition=zen4
```

Use the shell to run commands interactively or launch parallel tasks with `srun`:

```bash
srun ./my_cpu_program
```

---

## ⏱️ Wait Limits and Timeout

Interactive jobs will be canceled if resources are not allocated within 6 minutes. To change this behavior, use the `--immediate` flag:

```bash
# Wait up to 10 minutes (600 seconds) for resources
salloc --nodes=1 --time=01:00:00 --partition=zen4 --immediate=600
```

---

## ⚠️ Common Errors

* **Missing GPUs in `srun`**: Always specify GPU count in both `salloc` and `srun`.
* **Account Errors**: Ensure you have a valid default account or specify one with `--account=<project>`.
* **No Resources Available**: Try a different partition or reduce requested time/nodes.

---

## 📚 Related Pages

* [Running Jobs](basics.md)
* [Queues](queues-charges.md)
* [Example Job Scripts](examples.md)
