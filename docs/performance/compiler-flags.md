# Compiler Flags

!!! warning
    This page is currently under development. The following recommendations serve as a preliminary guide. Users are strongly encouraged to validate compiler flags against their own applications through testing and performance benchmarking.

Optimizing compilation flags is essential to maximizing application performance on the REPACSS high-performance computing system. The recommended flags below are tailored for the compiler toolchains available via REPACSS environment modules.


## General Optimization Guidelines

- Use `-O2` or `-O3` for performance optimization.
- Enable vectorization and loop unrolling where beneficial.
- Use architecture-specific flags (e.g., `-march=native`) to generate code optimized for REPACSS hardware.
- Profile and benchmark performance before and after applying new flags.
- Use `-fopenmp` to enable multithreading where applicable.

## GCC (Version 14.2.0)

**Recommended Flags:**

```bash
-O3 -march=native -funroll-loops -ffast-math -fopenmp
```

**Descriptions:**

- `-O3`: Enables aggressive optimization.
- `-march=native`: Targets the specific microarchitecture of the compute node.
- `-funroll-loops`: Enhances performance for loop-heavy code.
- `-ffast-math`: Permits faster floating-point operations (may break strict IEEE compliance).
- `-fopenmp`: Enables OpenMP multithreading.

## Example Compilation Command

**GCC Example:**

```bash
gcc -O3 -march=native -fopenmp mycode.c -o mycode
```

!!! note
    For best results, benchmark with realistic datasets and verify correctness after applying aggressive optimizations.


<!-- ## Additional Resources

After compilation, it is recommended to consult the following documentation pages to evaluate application performance:

- [Profiling Tools](profiling-tools.md)
- [Scaling Tests](scaling-tests.md) -->
