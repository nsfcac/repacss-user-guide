# Software

## Available Software {#available}

### Compilers
- GCC 12.2.0
- Intel 2023.0
- NVIDIA 23.1

### Libraries
- OpenMPI 4.1.5
- CUDA 12.0
- BLAS/LAPACK
- FFTW
- HDF5

### Applications
- Python 3.11 (see [Python Environment Setup](python.md) for recommended Miniforge installation)
- R 4.3.0

## Module System {#modules}

### Basic Commands
```bash
# List available modules
module avail

# Load a module
module load gcc/12.2.0

# List loaded modules
module list

# Unload a module
module unload gcc
```

### Common Modules
```bash
# Load default environment
module load default

# Load compiler
module load gcc

# Load MPI
module load openmpi

# Load CUDA
module load cuda
```

## Custom Software {#custom}

### Installation
- Request installation
- Provide documentation
- Test compatibility
- Follow guidelines

### Environment
- Use modules
- Set paths
- Check dependencies
- Document setup
- For Python environments, use Miniforge (see [Python Environment Setup](python.md))

## Related Resources

- [System Overview](system-overview.md)
- [Running Jobs](running-jobs.md)
- [File Management](file-management.md)
- [Python Environment Setup](python.md)
- [Support](../support&resources/support.md) 