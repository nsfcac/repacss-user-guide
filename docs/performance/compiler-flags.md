# Compiler Flags

!!! warning
    This page is currently under development. The following recommendations serve as a preliminary guide. Users are advised to verify the selected compiler options, version compatibility, and resulting performance gains through comprehensive testing.

Appropriate selection of compiler flags can significantly influence the computational performance and efficiency of applications executed on the REPACSS high-performance computing system. The following sections outline recommended practices and commonly used compiler options for different compiler toolchains available on REPACSS.

---

## General Guidelines

- Utilize optimization flags such as `-O2` or `-O3` to enhance application performance.
- Leverage architecture-specific options to tailor compiled code for REPACSS compute node hardware.
- Conduct benchmarking or profiling before and after applying new flags to quantitatively assess the performance impact.

---

## GCC (Version 12.2.0)

Recommended compiler flags for GCC:

```bash
-O3 -march=native -funroll-loops -ffast-math -fopenmp
```

Flag descriptions:

- `-O3` activates advanced optimization strategies.
- `-march=native` targets the local processor’s instruction set architecture.
- `-funroll-loops` may improve execution speed for loop-intensive code.
- `-fopenmp` enables support for OpenMP-based parallelism.

---

## Intel OneAPI (Version 2023.0)

Recommended compiler flags for Intel OneAPI compilers:

```bash
-O3 -xHost -qopenmp -fp-model fast=2
```

Flag descriptions:

- `-xHost` instructs the compiler to optimize for the host system’s maximum instruction set.
- `-qopenmp` enables multi-threaded parallelization using OpenMP.
- `-fp-model fast=2` allows the compiler to relax strict IEEE-754 compliance for faster floating-point operations.

---

## NVIDIA HPC SDK (Version 23.1)

Recommended compiler flags for NVIDIA's HPC SDK, targeting GPU acceleration:

```bash
-O3 -mp=gpu -gpu=cc90,fastmath -Minfo=accel
```

Flag descriptions:

- `-mp=gpu` enables GPU acceleration using OpenACC.
- `-gpu=cc90,fastmath` configures the compiler for CUDA Compute Capability 9.0 (H100 architecture) and enables fast math optimizations.
- `-Minfo=accel` displays compiler feedback on which sections of code were accelerated.

---

## Example Usage

To compile sample applications using various compilers:

GCC Example:

```bash
gcc -O3 -march=native -fopenmp mycode.c -o mycode
```

Intel OneAPI Example:

```bash
icx -O3 -xHost -qopenmp mycode.c -o mycode
```

NVIDIA HPC SDK Example:

```bash
nvc -O3 -mp=gpu mycode.c -o mycode
```

---

## Additional Resources

After compilation, it is recommended to consult the following documentation pages to evaluate application performance:

- [Profiling Tools](profiling-tools.md)
- [Scaling Tests](scaling-tests.md)
