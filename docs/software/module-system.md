# Using Software Modules on REPACSS

REPACSS offers a wide selection of **system-provided** research and instructional software using the **Spack package manager** and **Lmod environment module system**. This guide shows you how to find, load, and manage software modules, and provides an up-to-date summary of available software environments.

**This covers system-provided HPC applications, compilers, and system software - no installation required, just load what you need.** For user-installed data science applications, see [Getting Started with MiniForge](miniforge.md) next.

---

## Available Software Modules

Software modules are grouped by repository path and hardware partition. You can load any module on any partition, but only GPU-enabled packages can utilize GPU resources when running on the GPU (h100) partition. Some modules (such as MPI libraries) are available in both partitions, but with different capabilities.

### zen4 Partition

#### `/opt/apps/nfs/modules/zen4/rocky9.4/Core`

| Module                | Version        | Description                                                      |
|-----------------------|---------------|------------------------------------------------------------------|
| boost                 | 1.86.0        | C++ libraries for tasks and structures                           |
| bwa                   | 0.7.17        | Burrows-Wheeler Aligner for sequence alignment                   |
| eigen                 | 3.4.0         | C++ template library for linear algebra                          |
| ffmpeg                | 6.1.1         | Audio and video processing tools                                 |
| gdal                  | 3.10.0        | Geospatial Data Abstraction Library                              |
| geos                  | 3.13.0        | Geometry Engine - Open Source                                    |
| gcc                   | 14.2.0        | GNU Compiler Collection (C, C++, Fortran)                        |
| gsl                   | 2.8           | GNU Scientific Library                                           |
| gnuplot               | 6.0.0         | Portable command-line driven graphing utility                    |
| htop                  | 3.3.0         | Interactive process viewer                                       |
| imagemagick           | 7.1.1-39      | Image manipulation tools                                         |
| intel-oneapi-compilers| 2023.0.0      | Intel OneAPI Compilers (C++, Fortran)                           |
| metis                 | 5.1.0         | Serial graph partitioning and fill-reducing matrix ordering      |
| **mpich**             | 4.1.2         | MPI implementation (default)                                     |
| ninja                 | 1.12.1        | Small build system with a focus on speed                         |
| openblas              | 0.3.28        | Optimized BLAS library                                           |
| **openmpi**           | 5.0.4         | High-performance MPI (default)                                   |
| proj                  | 9.4.1         | Cartographic projections and coordinate transformations          |
| python                | 3.10.10       | Python programming language                                      |
| **python**            | 3.12.5        | Python programming language (default)                            |
| r                     | 4.4.1         | Statistical computing and graphics                               |
| samtools              | 1.19.2        | Tools for manipulating next-generation sequencing data           |
| sparsehash            | 2.0.4         | Memory-efficient hash map implementation                         |
| swig                  | 4.1.0-fortran | Simplified Wrapper and Interface Generator for Fortran           |
| tmux                  | 3.4           | Terminal multiplexer                                             |

#### `/opt/apps/nfs/modules/zen4/rocky9.4/mpich/4.1.2-a5xh3ge/Core`
!!! note
    These modules are only available after loading the `mpich` module (default in zen4). Run:
    
    ```bash
    module load mpich
    ```
    before using any of these packages.
    To make sure you are loading the default zen4 mpich, not the h100 mpich. After loading, check the module path with:
    
    ```bash
    module show mpich
    ```
    The path should include `/opt/apps/nfs/modules/zen4/rocky9.4/mpich/4.1.2-a5xh3ge/Core`.
    
    

| Module                | Version        | Description                                                      |
|-----------------------|---------------|------------------------------------------------------------------|
| fftw                  | 3.3.10        | Fast Fourier Transform library used in signal and image processing|
| hdf5                  | 1.14.5        | Hierarchical Data Format library for large/complex data           |
| lammps                | 20240829.1    | Molecular dynamics simulator                                     |
| netcdf-c              | 4.9.2         | Data format for array-oriented scientific data                    |
| openfoam              | 2312          | Open source computational fluid dynamics toolbox                  |
| p3dfft3               | 3.0.0         | Parallel 3D FFT library                                          |
| quantum-espresso      | 7.4           | Electronic-structure and materials modeling suite                 |
| scotch                | 7.0.4         | Graph partitioning, static mapping, and clustering library        |
| wrf                   | 4.6.1         | Weather Research and Forecasting Model                           |
| wps                   | 4.5           | WRF Preprocessing System                                         |

#### `/opt/apps/nfs/modules/zen4/rocky9.4/oneapi/2023.0.0`
!!! note
    These modules are only available after loading the `intel-oneapi-compilers` module. Run:
    
    ```bash
    module load intel-oneapi-compilers
    ```
    before using any of these packages.

| Module                | Version        | Description                                                      |
|-----------------------|---------------|------------------------------------------------------------------|
| intel-oneapi-mkl      | 2024.2.2      | Intel Math Kernel Library                                        |
| intel-oneapi-mpi      | 2021.4.0      | Intel MPI Library                                                |

#### `/opt/apps/nfs/modules/zen4/rocky9.4/intel-oneapi-mpi/2021.4.0-5ksoj4d/oneapi/2023.0.0`
!!! note
    These modules are only available after loading the `intel-oneapi-mpi` module. Run:
    
    ```bash
    module load intel-oneapi-mpi
    ```
    before using any of these packages.

| Module                | Version        | Description                                                      |
|-----------------------|---------------|------------------------------------------------------------------|
| fftw                  | 3.3.10        | Fast Fourier Transform library used in signal and image processing|
| hdf5                  | 1.14.5        | Hierarchical Data Format library for large/complex data           |

### h100 (GPU Partition)

#### `/opt/apps/nfs/modules/h100/rocky9.4/Core`

These modules are GPU-enabled. To access them, prepend the h100 path to your MODULEPATH (see MPI section below):

| Module   | Version        | Description                                 |
|----------|---------------|---------------------------------------------|
| cuda     | 12.6.2        | NVIDIA CUDA Toolkit                         |
| cudnn    | 9.2.0.82-12   | NVIDIA CUDA Deep Neural Network library     |
| mpich    | 4.1.2         | MPI implementation (GPU-enabled)            |
| nccl     | 2.22.3-1      | NVIDIA Collective Communications Library    |
| openmpi  | 5.0.4         | High-performance implementation of MPI (GPU-enabled)      |

---

## MPI Implementations and Usage Guidance

### Overview

Three MPI implementations are available: **OpenMPI**, **MPICH**, and **Intel MPI**. OpenMPI and MPICH are provided for both CPU (zen4) and GPU (h100) partitions, while Intel MPI is only available in the CPU (zen4) partition. The h100 versions are CUDA-enabled for GPU workloads.

- **zen4**: CPU-only MPI modules (default: mpich, openmpi) + Intel MPI (after loading intel-oneapi-compilers)
- **h100**: GPU-enabled MPI modules (mpich, openmpi)

### Using MPI-Dependent Packages

Some software packages in the zen4 partition require specific MPI modules to be loaded first. Two sets of MPI-dependent packages are available:

#### MPICH-Dependent Packages

Software packages like `fftw`, `hdf5`, `lammps`, `openfoam`, `quantum-espresso`, `wrf`, etc. (see the [MPICH table above](#optappsnfsmoduleszen4rocky94mpich412-a5xh3gecore)) require the `mpich` module to be loaded first:

```bash
module load mpich
```

To make sure you are loading the default zen4 mpich, not the h100 mpich, verify with:

```bash
module show mpich
```

The output should reference `/opt/apps/nfs/modules/zen4/rocky9.4/mpich/4.1.2-a5xh3ge/Core`.

#### Intel MPI-Dependent Packages

Software packages like `fftw` and `hdf5` (see the [Intel MPI table above](#optappsnfsmoduleszen4rocky94intel-oneapi-mpi202140-5ksoj4doneapi202300)) require the Intel MPI environment to be loaded first:

```bash
module load intel-oneapi-compilers
module load intel-oneapi-mpi
```

### Running MPI Applications

When running MPI applications, use the appropriate launcher for your MPI implementation:

- **For OpenMPI and MPICH**: Use `srun` (SLURM's native launcher)
  ```bash
  srun -n 4 ./your_mpi_program
  ```

- **For Intel MPI**: Use `mpirun` (Intel MPI's launcher)
  ```bash
  mpirun -np 4 ./your_mpi_program
  ```

This ensures optimal performance and compatibility with each MPI implementation.



### Accessing GPU-Enabled MPI Modules

To use CUDA-enabled `mpich` or `openmpi` in the GPU (h100) partition:
1. Prepend the h100 module path to your MODULEPATH:
   ```bash
   module use /opt/apps/nfs/modules/h100/rocky9.4/Core
   ```
2. Load the desired MPI module (e.g., `mpich` or `openmpi`).

### Switching Between MPI Implementations

To switch from one MPI implementation to another, use:
```bash
module swap mpich openmpi
```
This unloads the current MPI module and loads the new one, updating your environment automatically.

---

## How to Use Modules

### List Available Modules

Show all modules you can load:

```bash
module avail
```

Show only default modules:

```bash
module --default avail
# or
ml -d av
```

See module categories and counts:

```bash
module overview
# or
ml ov
```

### Search for Modules

Find all available software and extensions:

```bash
module spider
```

Search for a specific module or keyword:

```bash
module spider python
```

Get details for a specific version:

```bash
module spider python/3.11.0
```

---

## Loading and Unloading Modules

Load a module to use its software:

```bash
module load gcc/14.2.0
module load openmpi/4.1.6
```

You can load multiple modules at once:

```bash
module load gcc/14.2.0 cuda/12.0
```

Specifying exact versions is recommended for reproducibility.

To remove a specific software module from the current environment:

```bash
module unload gcc/14.2.0
```

To remove all loaded modules and restore a clean environment:

```bash
module purge
```

---

## Viewing Module Details and Loaded Modules

See what a module changes in your environment:

```bash
module show hdf5
```

List all modules currently loaded:

```bash
module list
```

This helps with troubleshooting and documenting your environment.

---

## Best Practices for Job Scripts

- Start job scripts with `module purge` for a clean environment.
- Load only the modules you need.
- Record loaded modules for reproducibility.

---

## More Information and Support

For a full list of available software, see the tables above.

For Python-specific help, see the [Installing Packages](installing-packages.md) guide.

Need help? Contact REPACSS support:

```
repacss.support@ttu.edu
```
