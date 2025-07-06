# Getting Started with Conda at REPACSS

## Introduction

It is often useful to set up a fully customized set of software packages including Python and many other utility tools using the MiniForge package manager. For performance, consistency, and licensing flexibility, we recommend using **MiniForge** instead of tools distributed by Anaconda, Inc. such as Anaconda or Miniconda.

While Anaconda provides a broad suite of tools, it uses proprietary channels that can lead to outdated or restricted packages. MiniForge is a minimal, community-maintained Conda distribution that defaults to the **conda-forge** channel, providing access to the latest packages without commercial licensing concerns. MiniForge also includes the **Mamba** backend for faster environment solving and installation.

This guide explains the benefits of using MiniForge on REPACSS and provides step-by-step instructions for setup and environment management.

---

## Overview of Conda Ecosystem

- **Conda**: Cross-platform command-line tool for managing packages and environments.
- **Anaconda**: A commercial distribution that includes Conda and many preinstalled data science packages.
- **Miniconda**: A minimal Anaconda installer with basic tools and default channels.
- **MiniForge**: A minimal installer with only conda-forge preconfigured and no proprietary channels.
- **Mamba**: A drop-in replacement for Conda, built in C++ for speed and efficiency.

---

## Why Use MiniForge

- **Community-Centric**: Uses conda-forge as the default source of packages.
- **No Default Channel Conflicts**: Avoids Anaconda's proprietary defaults.
- **Minimal Footprint**: Lets you install only what you need.
- **Fast and Reliable**: Includes Mamba for faster package resolution.
- **Licensing Clarity**: No commercial restrictions.

---

## Removing Previous Conda Installations

If you previously installed Anaconda or Miniconda, we recommend removing them to avoid conflicts.

### Check for existing Conda

```bash
conda --version
```

### Locate old installations

```bash
ls -al | grep conda
```

### Remove directories

```bash
find . -maxdepth 1 -name '*conda*' -exec rm -ir {} +
find . -maxdepth 1 -name 'Miniforge*' -exec rm -ir {} +
find . -maxdepth 1 -name 'Mambaforge*' -exec rm -ir {} +
```

### Clean `.bashrc`

Remove any `conda` initialization lines and sign out and back in.

---

## Installing MiniForge

### Download and run installer

```bash
wget https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh
bash Miniforge3-$(uname)-$(uname -m).sh
```

Accept the license agreement and install to the default directory (e.g., `$HOME/miniforge3`).

### Initialize and prevent auto-activation

```bash
source ~/.bashrc
conda config --set auto_activate_base false
```

### Confirm installation

```bash
which conda
conda --version
```

---

## Adding Channels (Optional)

By default, MiniForge uses `conda-forge`. Additional channels can be added if needed.

### Set strict channel priority

```bash
conda config --set channel_priority strict
```

### Optional: Add Bioconda (for bioinformatics)

```bash
conda config --add channels bioconda
```

---

## Creating Virtual Environments

### Create a new environment

```bash
conda create -n <env_name> python=3.11 numpy scipy matplotlib
```

### Activate the environment

```bash
conda activate <env_name>
```

### List environments

```bash
conda env list
```

---

## Managing and Removing Environments

### Deactivate the current environment

```bash
conda deactivate
```

### Remove an environment

```bash
conda env remove --name <env_name>
```

---

## Optimizing Conda Initialization

Avoid installing all packages in the `base` environment. Create small, purpose-specific environments for each project.

### Prevent `base` from activating on login

```bash
conda config --set auto_activate_base false
```

### Check the configuration

```bash
conda config --show | grep auto_activate_base
```

---

## Notes on Anaconda Licensing

Anaconda, Inc. enforces licensing terms on their default channels and tools. Usage in commercial or research contexts may require a paid license.

To avoid licensing complications and ensure access to current packages, we recommend avoiding the Anaconda defaults and using MiniForge + conda-forge.

!!! Warning
    REPACSS does not cover licensing costs related to Anaconda. Users are responsible for any commercial usage compliance.

For more details, see: [Anaconda Terms of Service](https://www.anaconda.com/terms-of-service)
