# 💻 Available Software

REPACSS provides a wide range of software environments for computational research and education. These include optimized compilers, mathematical libraries, domain-specific tools, and GPU-accelerated frameworks.

> ℹ️ Most software is accessed using the environment [module system](module-system.md).

---

## 🔧 Compilers

The following compilers are available on REPACSS:

* **GCC** 12.2.0 – General-purpose open-source compiler
* **Intel OneAPI** 2023.0 – Optimized for Intel CPUs and vector operations
* **NVIDIA HPC SDK** 23.1 – High-performance compiler suite for NVIDIA GPU programming

---

## 📚 Scientific Libraries

Libraries supporting scientific computing and high-performance simulations:

* **OpenMPI** 4.1.5 – Message Passing Interface for parallel jobs
* **CUDA** 12.0 – NVIDIA’s GPU computing toolkit
* **BLAS / LAPACK** – Linear algebra libraries
* **FFTW** – Fast Fourier Transforms in one or more dimensions
* **HDF5** – Hierarchical data format for large datasets
* **ScaLAPACK** – Distributed memory linear algebra
* **NetCDF** – Scientific data formats for array-oriented data

---

## 🧪 Applications

Commonly used applications and environments for simulation, data analysis, and AI workflows:

* **Python** 3.11 (via Miniforge) – Versatile scripting language for scientific work

  * Install packages via `conda` or `pip` (see [Python Environment Setup](python.md))
* **R** 4.3.0 – Statistical computing and visualization
* **TensorFlow**, **PyTorch** – GPU-accelerated machine learning frameworks
* **GROMACS**, **LAMMPS**, **Quantum ESPRESSO** – Molecular dynamics and quantum chemistry (check availability)

---

## 📦 Software Access

To load available software, use the module system:

```bash
module avail       # Show available software modules
module load gcc/12.2.0
```

See the [Module System](module-system.md) page for more guidance.
