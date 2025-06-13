# 📦 Installing Packages

This page provides guidance for installing additional software or Python packages in the REPACSS environment. Users can install packages in their own workspace without administrative privileges.

---

## 🐍 Python Packages

Python 3.11 is available via **Miniforge** and supports both `conda` and `pip` for managing packages.

### ✅ Activate Miniforge

First, activate your base Python environment:

```bash
source ~/miniforge3/etc/profile.d/conda.sh
conda activate base
```

If `conda` is not found, ensure Miniforge is installed in your home directory. Contact support if not available.

### 📥 Installing with Conda

Install packages into a named environment:

```bash
conda create -n myenv numpy scipy matplotlib
conda activate myenv
```

To add more packages later:

```bash
conda install pandas scikit-learn
```

### 📥 Installing with Pip

If your package is not available via conda:

```bash
pip install somepackage
```

You can install from a `requirements.txt` file:

```bash
pip install -r requirements.txt
```

---

## 💻 C/C++ or Fortran Libraries

If you need to install custom libraries (e.g., building from source):

1. Load the appropriate modules:

```bash
module load gcc/12.2.0 openmpi/4.1.5
```

2. Build and install:

```bash
./configure --prefix=$HOME/mylibs
make -j
make install
```

Add your installation path to the environment:

```bash
export PATH="$HOME/mylibs/bin:$PATH"
export LD_LIBRARY_PATH="$HOME/mylibs/lib:$LD_LIBRARY_PATH"
```

---

## ⚠️ Tips

* Avoid installing packages system-wide. Use local directories (e.g., `$HOME`, `$WORK`) for all custom installs.
* Use conda environments to keep package dependencies isolated and manageable.
* Consider using virtual environments or containers (e.g., conda, venv, or Apptainer) for reproducibility.

---

## 📚 Related Pages

* [Module System](module-system.md)
* [Available Software](available-software.md)
* [Python Environment Setup](python.md)
