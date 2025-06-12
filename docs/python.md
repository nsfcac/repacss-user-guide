# Python Environment Setup

## Overview

REPACSS offers Python via the module system, but for better control and reproducibility, users are encouraged to set up their own conda environments using **Miniforge**.

Miniforge is a minimal installer for Conda that defaults to the **conda-forge** channel. It is recommended because:

- ✅ **Community-driven** with up-to-date packages
- 🚫 No reliance on the `defaults` channel (avoids conflicts)
- 🪶 Lightweight footprint
- 🔄 Better compatibility with HPC and scientific libraries

---

## Prerequisites

- Access to REPACSS login nodes
- Familiarity with the Linux shell
- Basic understanding of Python packaging

---

## Removing Old Conda Installations

Before installing Miniforge, remove any previous Conda installations to avoid conflicts.

```bash
conda --version     # If not found, you're good to go

ls -al | grep conda # Check for conda files
find . -maxdepth 1 -name "*conda*" -exec rm -ir {} +
```

---

## Installing Miniforge

1. Download the installer:
```bash
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
```

2. Make it executable and run:
```bash
chmod +x Miniforge3-Linux-x86_64.sh
./Miniforge3-Linux-x86_64.sh
```

3. Choose `/home/$USER/miniforge3` as the install path.

4. Source your shell config:
```bash
source ~/.bashrc
```

---

## Basic Conda Usage

### 🔧 Managing Environments

```bash
conda create -n myenv python=3.11     # Create
conda activate myenv                  # Activate
conda install numpy pandas scipy      # Install packages
conda deactivate                      # Deactivate
```

Use `pip` for additional packages as needed.

---

## Best Practices

### 🧪 Environment Management

```bash
# Export current environment
conda env export > environment.yml

# Re-create from file
conda env create -f environment.yml
```

- Keep environments separate per project
- Avoid modifying the base environment
- Update Conda regularly:
```bash
conda update conda
```

### 💾 Storage Tips

- Install environments in `$HOME`
- Use `$SCRATCH` for datasets or large files
- Clean unused envs:
```bash
conda env remove -n old_env
```

---

## Running Python on REPACSS

### 🧑‍💻 Interactive Mode

```bash
interactive -c 8 -p h100
conda activate myenv
python script.py
```

### 🗂 Batch Script

Create `run_python.sh`:

```bash
#!/bin/bash
#SBATCH --job-name=python_job
#SBATCH --output=python_job.out
#SBATCH --error=python_job.err
#SBATCH --time=01:00:00
#SBATCH --partition=h100
#SBATCH --nodes=1
#SBATCH --ntasks=1
#SBATCH --cpus-per-task=8
#SBATCH --mem=32G

module load gcc

source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv

python script.py
```

Submit it:
```bash
sbatch run_python.sh
```

---

## Troubleshooting

### ❌ Environment Doesn’t Activate
- Miniforge might not be sourced. Run:
```bash
source ~/miniforge3/etc/profile.d/conda.sh
```

### 📦 Package Won’t Install
- Use the conda-forge channel:
```bash
conda install -c conda-forge package_name
```

### 🧠 Memory Errors
- Adjust memory in your `#SBATCH --mem` line
- Monitor usage with `htop`

---

## Related Resources

- [Getting Started](getting-started.md)
- [Running Jobs](running-jobs.md)
- [Software](software.md)
- [File Management](file-management.md)
- [Support](../support&resources/support.md)
