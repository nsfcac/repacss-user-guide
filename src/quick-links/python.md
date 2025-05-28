# Python Environment Setup

## Overview

REPACSS provides Python through the module system, but for better control and reproducibility, users are encouraged to set up their own conda environments. This guide will help you create and manage your Python environments using Miniforge.

Miniforge is a minimal installer for Conda that includes the Mamba libraries. It allows users to install the Conda package manager with conda-forge set as the default channel. We recommend Miniforge over Miniconda or Anaconda for several reasons:

- **Community-Focused**: Miniforge is a community-driven project specifically designed to work seamlessly with the conda-forge channel, ensuring access to a vast and frequently updated collection of packages.
- **No Default Channels**: Unlike Anaconda and Miniconda, which include the "defaults" channel that may lead to outdated packages or conflicts, Miniforge sets up and is only dependent on conda-forge, providing a more consistent and reliable package management experience.
- **Lightweight Installation**: Miniforge provides a minimal installer, which means it occupies less disk space and allows users to install only the packages they need.
- **Enhanced Compatibility**: Using conda-forge as the primary channel improves compatibility with numerous scientific packages that may not be available in the default channels.

## Prerequisites

1. Access to REPACSS login nodes
2. Basic knowledge of Linux commands
3. Understanding of Python package management

## Removing Existing Conda Installations

Before installing Miniforge, it's recommended to remove any existing conda installations to avoid conflicts.

### Check for Existing Conda Installations

1. Check if conda is installed:
```bash
conda --version
```
If conda is not installed, you will receive a "command not found" error and can proceed with the installation.

2. Verify existing conda installations:
```bash
ls -al | grep conda
```

3. Remove any existing conda-related directories and files:
```bash
find . -maxdepth 1 -name \*conda\* -exec rm -ir {} +
```
This command will ask for confirmation before deleting each file or directory. Answer:
- `y` to remove the item
- `n` to keep the item

## Setting Up Miniforge

### Installation

1. Download Miniforge:
```bash
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-Linux-x86_64.sh
```

2. Make the installer executable:
```bash
chmod +x Miniforge3-Linux-x86_64.sh
```

3. Run the installer:
```bash
./Miniforge3-Linux-x86_64.sh
```

4. Follow the prompts and accept the license agreement
5. When asked for the installation location, use your home directory:
```bash
/home/$USER/miniforge3
```

6. Initialize Miniforge:
```bash
source ~/.bashrc
```

### Basic Usage

1. Create a new environment:
```bash
conda create -n myenv python=3.11
```

2. Activate your environment:
```bash
conda activate myenv
```

3. Install packages:
```bash
conda install numpy pandas scipy
# or
pip install package_name
```

4. Deactivate environment:
```bash
conda deactivate
```

## Best Practices

### Environment Management

1. Create separate environments for different projects
2. Use environment.yml files for reproducibility:
```bash
# Export environment
conda env export > environment.yml

# Create environment from file
conda env create -f environment.yml
```

3. Keep your base environment clean
4. Regularly update conda:
```bash
conda update conda
```

### Storage Considerations

- Store environments in your home directory
- Use scratch space for large datasets
- Clean up unused environments:
```bash
conda env remove -n envname
```

## Running Python Jobs

### Interactive Sessions

1. Request an interactive session:
```bash
interactive -c 8 -p h100
```

2. Activate your environment:
```bash
conda activate myenv
```

3. Run Python:
```bash
python script.py
```

### Batch Jobs

Create a job script (e.g., `run_python.sh`):
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

# Load any required modules
module load gcc

# Activate conda environment
source ~/miniforge3/etc/profile.d/conda.sh
conda activate myenv

# Run Python script
python script.py
```

Submit the job:
```bash
sbatch run_python.sh
```

## Common Issues and Solutions

1. **Environment Activation Fails**
   - Ensure Miniforge is properly initialized
   - Check if the environment exists: `conda env list`

2. **Package Installation Issues**
   - Try installing from conda-forge channel:
     ```bash
     conda install -c conda-forge package_name
     ```
   - Use pip as a fallback

3. **Memory Issues**
   - Monitor memory usage: `top` or `htop`
   - Adjust batch job memory requests

## Related Resources

- [Getting Started](getting-started.md)
- [Running Jobs](running-jobs.md)
- [Software](software.md)
- [File Management](file-management.md)
- [Support](../support&resources/support.md)
