# Installing User-Level Software Packages

This document provides guidance for installing additional software packages—particularly Python libraries—within the REPACSS computing environment. Users are permitted to install software in their own workspace without requiring administrative privileges, provided installations are performed in designated directories such as `$HOME` or `$WORK`.

---

## Python Package Management

Python 3.11 is available through the **Miniforge** distribution, which supports both `conda` and `pip` as package management tools. Users may create and manage isolated Python environments without elevated access.

### Activating Miniforge

To begin using Python in REPACSS, activate the Miniforge environment as follows:

```bash
source ~/miniforge3/etc/profile.d/conda.sh
conda activate base
```

If the `conda` command is not recognized, confirm that Miniforge is correctly installed in your home directory. If it is missing, please submit a support request.

---

### Installing Packages Using Conda

To install packages into a new isolated environment:

```bash
conda create -n myenv numpy scipy matplotlib
conda activate myenv
```

To install additional packages into an existing environment:

```bash
conda install pandas scikit-learn
```

---

### Installing Packages Using Pip

In cases where a package is unavailable via `conda`, the `pip` utility may be used within an activated environment:

```bash
pip install somepackage
```

To install from a `requirements.txt` file:

```bash
pip install -r requirements.txt
```

It is strongly recommended that `pip` be used only inside an activated conda or virtual environment to prevent unintended modifications to the base environment.

---

## C, C++, and Fortran Library Installation

For users developing or compiling C, C++, or Fortran libraries from source, the following procedure is advised:

1. Load required compiler and MPI modules:

```bash
module load gcc/14.2.0 openmpi/4.1.6
```

2. Build and install the library locally:

```bash
./configure --prefix=$HOME/mylibs
make -j
make install
```

3. Add the installation directory to the environment:

```bash
export PATH="$HOME/mylibs/bin:$PATH"
export LD_LIBRARY_PATH="$HOME/mylibs/lib:$LD_LIBRARY_PATH"
```

---

## Best Practices and Guidelines

- All software should be installed to user-controlled directories such as `$HOME` or `$WORK`. Installation to system directories is not permitted.
- Use `conda` environments or `venv` for managing dependencies and improving reproducibility.
- For large-scale or portable workflows, consider encapsulating environments using containers (e.g., Apptainer/Singularity).
- Maintain separate environments for distinct projects to prevent dependency conflicts.

---

## Additional Resources

For further configuration or software access guidance, refer to the following documentation:

- [Module System](module-system.md)
- [Available Software](available-software.md)

For additional support or to request software installation at the system level, please contact:

```
repacss.support@ttu.edu
```
