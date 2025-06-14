# Troubleshooting Guide

!!! warning
    This page is still under development. The content below may be incomplete or subject to revision.

Use this page to identify and resolve common issues encountered on REPACSS.

---

## Job Not Starting

- Check if your job is pending due to resource availability:
  
  ```bash
  squeue --me
  ```

- Look for the **NODELIST(REASON)** column for hints like:
  - `Resources`: Not enough nodes available.
  - `Priority`: Waiting for higher-priority jobs to clear.
  - `Dependency`: Job depends on another that hasn’t finished.

---

## Invalid Account or Partition

If you see:
```
sbatch: error: Job request does not match any supported policy.
```

- Ensure your account/project is valid and available for the selected partition.
- Set your account using:

  ```bash
  #SBATCH --account=m1234
  ```

---

## Python Module Not Found

If you get:
```
ModuleNotFoundError: No module named 'numpy'
```

- Check that you’ve activated the correct conda environment:
  ```bash
  conda activate myenv
  ```

- If it’s missing, reinstall it:
  ```bash
  pip install numpy
  ```

---

## SSH Connection Issues

- If login is slow or stuck:
  - Try verbose output to debug:
    ```bash
    ssh -vvv your_username@repacss.ttu.edu
    ```

- Make sure VPN is connected properly.

---

## "command not found"

If a common command like `gcc`, `python`, or `nvcc` fails:
- Check if the required module is loaded:
  ```bash
  module list
  module load gcc/12.2.0
  ```

---

## Poor Performance

- Check if you’re using correct compiler flags and parallel settings.
- Use profiling tools like:
  ```bash
  time ./a.out
  perf stat ./a.out
  ```

- Review CPU or GPU utilization via `sstat` or `jobstats`.

---

## Disk Quota or Storage Issues

If you see:
```
Disk quota exceeded
```

- Use `du -sh *` to identify large files.
- Remove or move unnecessary data.

---

## Data Transfer Fails

- If `scp` or `rsync` fails:
  - Double-check path and permissions.
  - For large transfers, consider:
    ```bash
    rsync -avzP source/ user@repacss.ttu.edu:/destination/
    ```

---

## Infinite Loop or Hanging Job

- Make sure loops have valid exit conditions.
- Add logging or print statements to verify execution flow.
- You can cancel the job with:
  ```bash
  scancel <jobid>
  ```

---

## Module Conflicts

- If loading a module breaks something:
  ```bash
  module purge
  module load only_what_you_need
  ```

---

## Need Help?

If all else fails:

- Reach out to your advisor or system admin.
- Provide job ID, error message, and the job script when asking for help.
```
