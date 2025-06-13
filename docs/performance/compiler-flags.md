# ⚙️ Compiler Flags

!!! warning
    This page is still under development. Use these recommendations as a starting point and verify the compiler, versions and performance improvements through testing.

Choosing the right compiler flags can significantly impact the performance of your applications on REPACSS. This page provides guidance for commonly used compilers.

---

## 🧵 General Tips

* Always use optimization flags (e.g., `-O2` or `-O3`) for performance.
* Use architecture-specific flags to take advantage of REPACSS hardware.
* Profile before and after applying flags to measure impact.

---

## 🧰 GCC (12.2.0)

```bash
-O3 -march=native -funroll-loops -ffast-math -fopenmp
```

* `-O3` enables aggressive optimizations.
* `-march=native` targets the local CPU architecture.
* `-funroll-loops` can improve performance in some loops.
* `-fopenmp` enables OpenMP support.

---

## 💡 Intel OneAPI (2023.0)

```bash
-O3 -xHost -qopenmp -fp-model fast=2
```

* `-xHost` optimizes for the highest instruction set available on the host.
* `-qopenmp` enables OpenMP parallelism.
* `-fp-model fast=2` relaxes IEEE compliance for faster math.

---

## 🚀 NVIDIA HPC SDK (23.1)

```bash
-O3 -mp=gpu -gpu=cc90,fastmath -Minfo=accel
```

* `-mp=gpu` enables GPU acceleration with OpenACC.
* `-gpu=cc90,fastmath` targets H100 (CUDA compute capability 9.0).
* `-Minfo=accel` reports what loops are offloaded.

---

## 🧪 Example Usage

GCC:

```bash
gcc -O3 -march=native -fopenmp mycode.c -o mycode
```

Intel:

```bash
icx -O3 -xHost -qopenmp mycode.c -o mycode
```

NVIDIA:

```bash
nvc -O3 -mp=gpu mycode.c -o mycode
```

---

## 🧭 Next Steps

After compiling, use [Profiling Tools](profiling-tools.md) and [Scaling Tests](scaling-tests.md) to evaluate performance.
