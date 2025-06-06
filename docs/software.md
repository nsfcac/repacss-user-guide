# Software

## Available Software

REPACSS provides a range of compilers, libraries, and applications to support high-performance and scientific computing workloads.

### 🧰 Compilers

- GCC 12.2.0
- Intel OneAPI 2023.0
- NVIDIA HPC SDK 23.1

### 📚 Libraries

- OpenMPI 4.1.5
- CUDA Toolkit 12.0
- BLAS / LAPACK
- FFTW
- HDF5

### 🧪 Applications

- Python 3.11  
  *(See [Python Environment Setup](python.md) for Miniforge installation guidance)*
- R 4.3.0

---

## Module System

REPACSS uses the Lmod module system to manage software environments efficiently. Modules allow users to dynamically modify their environment to access various software versions.

### 🔧 Basic Commands

```bash
module avail             # List all available modules
module load gcc/12.2.0   # Load a specific module
module list              # Show currently loaded modules
module unload gcc        # Unload a module
```

### ⚙️ Common Modules

```bash
module load default      # Load default environment
module load gcc          # Load GCC compiler
module load openmpi      # Load OpenMPI stack
module load cuda         # Load CUDA libraries
```

---

## Custom Software

Users may install and manage their own software stacks within their home or work directories.

### 🛠 Requesting Installation

- Submit a request to system administrators
- Include documentation and installation instructions
- Ensure software is compatible with the target environment
- Follow REPACSS software policy

### 🧪 User Environments

When setting up custom tools:

- Use the module system to avoid conflicts
- Configure `PATH`, `LD_LIBRARY_PATH`, or `PYTHONPATH` as needed
- Use virtual environments or conda environments for Python
- Document your setup for reproducibility

👉 For Python environments, follow the [Python Environment Setup](python.md) guide.

---

## Related Resources

- [System Overview](system-overview.md)
- [Running Jobs](running-jobs.md)
- [File Management](file-management.md)
- [Python Environment Setup](python.md)
- [Support](../support&resources/support.md)
