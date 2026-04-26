# Example Job Scripts

This page provides structured job script examples adapted for REPACSS. For definitions and scheduler behavior, refer to the [Job Basics](basics.md) page. These examples are designed for CPU and GPU partitions such as `zen4`, `h100`, and `standard`.

---

!!! tip
    Interactive jobs in GPU partitions are granted scheduling priority on REPACSS.

!!! warning
    Each Slurm CPU is a hyperthread. To bind OpenMP threads to physical cores, use `--cpu-bind=cores`.

!!! note
    To run jobs in parallel, use `&`, and use `wait` to synchronize them.

---

## Job Types

Jobs on REPACSS can be submitted in two main forms:

* **Interactive Jobs**: Real-time sessions for testing and debugging.

  ```bash
  interactive -c 8 -p h100
  ```

* **Batch Jobs**: Scheduled jobs submitted via script.

```bash
  sbatch job.sh             # uses partition set inside the script,
                            # or zen4 if none is specified
  sbatch -p zen4 job.sh     # CPU partition
  sbatch -p h100 job.sh     # GPU partition
```
  !!! note
      If neither `-p` nor a `#SBATCH --partition=...` directive is
      provided, jobs are submitted to the default partition, **zen4**.
---

## Script Templates

### Basic MPI Job Script

This example demonstrates how to run a pure MPI application. For details on available MPI implementations and their usage, see [MPI Implementations and Usage Guidance](../software/module-system.md#mpi-implementations-and-usage-guidance).

!!! note
    Steps 1-2 below show how to create and compile a test program. If you already have your own MPI program compiled, you can skip to step 3 and use your program instead.

1. Create a file named `mpi_program.c` with the following content:
```c
#include <stdio.h>
#include <mpi.h>

int main(int argc, char **argv) {
    int rank, size;
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);
    MPI_Get_processor_name(processor_name, &name_len);

    printf("Hello from processor %s, rank %d out of %d processors\n",
           processor_name, rank, size);

    MPI_Finalize();
    return 0;
}
```

2. Load the required modules and compile the program:
```bash
module load gcc/14.2.0
module load mpich/4.1.2
mpicc mpi_program.c -o mpi_program
```

3. Create a file named `mpi_job.sh` with the following contents:
```bash
#!/bin/bash
#SBATCH --job-name=mpi_job
#SBATCH --output=mpi_job.out
#SBATCH --error=mpi_job.err
#SBATCH --partition=zen4
#SBATCH --time=01:00:00
#SBATCH --nodes=2
#SBATCH --ntasks=8
#SBATCH --cpus-per-task=1
#SBATCH --mem-per-cpu=2G

# Load modules
module load gcc/14.2.0
module load mpich/4.1.2

# Run MPI program using srun (for OpenMPI/MPICH)
srun -n 8 ./mpi_program
```
<small>*To determine your resource needs, refer to the [Determine Resource Needs](determining-resource-requirements.md) documentation.*</small>

4. Make the script executable and submit it using `sbatch`:
```bash
sbatch mpi_job.sh
```

!!! note
    For Intel MPI, use `mpirun -np 8 ./mpi_program` instead of `srun`. See [MPI Implementations and Usage Guidance](../software/module-system.md#mpi-implementations-and-usage-guidance) for details.

### Hybrid MPI+OpenMP Job Script

This example demonstrates how to run a hybrid MPI+OpenMP application that uses both MPI for inter-node communication and OpenMP for intra-node parallelism.

!!! note
    Steps 1-2 below show how to create and compile a test program. If you already have your own hybrid MPI+OpenMP program compiled, you can skip to step 3 and use your program instead.

1. Create a file named `hybrid_program.c` with the following content:
```c
#include <stdio.h>
#include <mpi.h>
#include <omp.h>

int main(int argc, char **argv) {
    int rank, size;
    int thread_id, num_threads;
    char processor_name[MPI_MAX_PROCESSOR_NAME];
    int name_len;

    MPI_Init(&argc, &argv);
    MPI_Comm_rank(MPI_COMM_WORLD, &rank);
    MPI_Comm_size(MPI_COMM_WORLD, &size);
    MPI_Get_processor_name(processor_name, &name_len);

    #pragma omp parallel private(thread_id, num_threads)
    {
        thread_id = omp_get_thread_num();
        num_threads = omp_get_num_threads();
        printf("MPI rank %d/%d on %s: OpenMP thread %d/%d\n",
               rank, size, processor_name, thread_id, num_threads);
    }

    MPI_Finalize();
    return 0;
}
```

2. Load the required modules and compile the program:
```bash
module load gcc/14.2.0
module load mpich/4.1.2
mpicc -fopenmp hybrid_program.c -o hybrid_program
```

3. Create a file named `hybrid_job.sh` with the following contents:
```bash
#!/bin/bash
#SBATCH --job-name=hybrid_job
#SBATCH --output=hybrid_job.out
#SBATCH --error=hybrid_job.err
#SBATCH --partition=zen4
#SBATCH --time=01:00:00
#SBATCH --nodes=2
#SBATCH --ntasks=4
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=2G

# Load modules
module load gcc/14.2.0
module load mpich/4.1.2

# Set OpenMP threads per MPI task
export OMP_NUM_THREADS=4

# Run hybrid program with CPU binding to physical cores
srun --cpu-bind=cores -n 4 ./hybrid_program
```
<small>*To determine your resource needs, refer to the [Determine Resource Needs](determining-resource-requirements.md) documentation.*</small>

4. Make the script executable and submit it using `sbatch`:
```bash
sbatch hybrid_job.sh
```

!!! tip
    This example uses 2 nodes with 4 MPI tasks and 4 OpenMP threads per task, for a total of 16 parallel threads. The `--cpu-bind=cores` flag ensures OpenMP threads are bound to physical cores rather than hyperthreads. Adjust `--ntasks`, `--cpus-per-task`, and `OMP_NUM_THREADS` based on your application's needs.

!!! note
    For more information on MPI implementations and launchers, see [MPI Implementations and Usage Guidance](../software/module-system.md#mpi-implementations-and-usage-guidance). 


### Python Job Script
1. Create a Python file named `script.py` with the following example content:
```bash
import time
import platform

print("SLURM Python job started.")
print("Running on:", platform.node())
time.sleep(10)  # Simulate workload
print("Job complete. Goodbye!")
```

2. Create a file named `submit_python_job.sh` with the following content:
```bash
#!/bin/bash
#SBATCH --job-name=python_job
#SBATCH --output=python_job.out
#SBATCH --error=python_job.err
#SBATCH --time=01:00:00
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G

# Load required modules
module load gcc

# Activate conda environment
source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv

# Run Python script
python script.py
```
<small>*To determine your resource needs, refer to the [Determine Resource Needs](determining-resource-requirements.md) documentation.*</small>

3. Make the script executable and submit it to SLURM:
```bash
sbatch submit_python_job.sh
```

### GPU Job Script
!!! warning  
    We are currently working to make the CUDA module available system-wide for all users. In the meantime, please use CUDA via a Conda environment as described below.

1. Create and activate a new Conda environment
```bash
conda create --name cuda-env python=3.10 -y
conda activate cuda-env
```

2. Install the CUDA Toolkit with nvcc support
```bash
conda install -c nvidia cuda-toolkit=12.9
```

3. Install a compatible GCC toolchain (GCC 11)
```bash
conda install -c conda-forge gxx_linux-64=11
```

4. Create a sample CUDA program: gpu_program.cu
```cpp
#include <stdio.h>
#include <cuda_runtime.h>

__global__ void hello_from_gpu() {
    printf("Hello from GPU thread %d!\n", threadIdx.x);
}

int main() {
    printf("Starting GPU job...\n");
    hello_from_gpu<<<1, 64>>>();

    cudaError_t err = cudaGetLastError();
    if (err != cudaSuccess) {
        fprintf(stderr, "Kernel launch failed: %s\n", cudaGetErrorString(err));
        return 1;
    }

    err = cudaDeviceSynchronize();
    if (err != cudaSuccess) {
        fprintf(stderr, "CUDA error after kernel: %s\n", cudaGetErrorString(err));
        return 1;
    }

    printf("GPU job finished.\n");
    return 0;
}
```

5. Compile the CUDA program for NVIDIA H100 GPUs (sm_90)
```bash
nvcc -arch=sm_90 \
  -ccbin "$CONDA_PREFIX/bin/x86_64-conda-linux-gnu-g++" \
  -I"$CONDA_PREFIX/targets/x86_64-linux/include" \
  -L"$CONDA_PREFIX/targets/x86_64-linux/lib" \
  -o gpu_program gpu_program.cu
```

6. Create the SLURM job script: `gpu_job.slurm`
```bash
#!/bin/bash
#SBATCH --job-name=gpu_hello
#SBATCH --output=gpu_hello.out
#SBATCH --error=gpu_hello.err
#SBATCH --partition=h100
#SBATCH --gres=gpu:nvidia_h100_nvl:1
#SBATCH --cpus-per-task=2
#SBATCH --mem=4G
#SBATCH --time=00:05:00

source ~/miniforge3/etc/profile.d/conda.sh
conda activate cuda-env

./gpu_program
```
<small>*To determine your resource needs, refer to the [Determine Resource Needs](determining-resource-requirements.md) documentation.*</small>

7. Submit the job to SLURM
```bash
sbatch gpu_job.slurm
```



<!-- 1. Create a file named `gpu_program.cu` with the following basic CUDA code: -->
<!-- ```bash
#include <stdio.h>

__global__ void hello_from_gpu() {
    printf("Hello from GPU thread %d!\\n", threadIdx.x);
}

int main() {
    printf("Starting GPU job...\\n");

    hello_from_gpu<<<1, 8>>>();
    cudaDeviceSynchronize();

    printf("GPU job finished.\\n");
    return 0;
}
``` -->

<!-- 2. Load the CUDA module and compile using `nvcc`: -->
<!-- ```bash
module load cuda
nvcc gpu_program.cu -o gpu_program
``` -->

<!-- 3. Create a file named `submit_gpu_job.sh` -->

---

## Job Management

### Submission

```bash
sbatch job.sh                       # Submit job
sbatch --array=1-10 job.sh          # Submit job array
sbatch --dependency=afterok:12345 job.sh  # Submit with dependency
```

### Monitoring

```bash
squeue -u $USER           # View user's jobs
squeue -p zen4            # View jobs on zen4 partition
squeue -p h100            # View jobs on h100 partition
```

### Control

```bash
scancel 12345             # Cancel a specific job
scancel -u $USER          # Cancel all user's jobs
scancel -p zen4           # Cancel all jobs in zen4 partition
```

---

## Resource Requests

* **CPU Jobs**: Specify `--nodes`, `--ntasks`, `--cpus-per-task`, and `--mem`
* **GPU Jobs**: Include `--gres=gpu:1` or more as needed
* **Python Jobs**:

  * See Python environment setup
  * Use `--cpus-per-task` for multi-threading
  * Set `--mem` appropriately for data requirements

For additional guidance, consult [Slurm Documentation](https://slurm.schedmd.com/documentation.html) and REPACSS-specific resources.
