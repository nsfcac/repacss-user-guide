# Using Containers on REPACSS

This guide covers using Apptainer/Singularity containers for running **user-installed** pre-built applications and complex software stacks on REPACSS.

## 🎯 When to Use Containers

Use containers when you need:

- **Pre-built applications** that are difficult to install locally
- **Complex software stacks** with many dependencies
- **Reproducible environments** for research workflows
- **Software with specific system requirements**
- **Applications that conflict with system libraries**

---

## 🐳 Getting Started with Apptainer

### Check Apptainer Availability

Apptainer is available on REPACSS. Verify it's working:

```bash
apptainer --version
```

### Basic Container Operations

#### Pull a Container

```bash
# Pull from Docker Hub
apptainer pull docker://ubuntu:latest

# Pull from Singularity Hub
apptainer pull shub://vsoch/hello-world

# Pull from a specific registry
apptainer pull docker://registry.example.com/myapp:latest
```

#### Run a Container

```bash
# Execute a command in a container
apptainer exec ubuntu_latest.sif bash

# Run a container as an application
apptainer run ubuntu_latest.sif

# Shell into a container
apptainer shell ubuntu_latest.sif
```

---

## 🔧 Building Custom Containers

### Creating Definition Files

Create a definition file for your custom container:

```bash
cat > myapp.def << EOF
Bootstrap: docker
From: ubuntu:20.04

%post
    apt-get update
    apt-get install -y python3 python3-pip
    pip3 install numpy scipy matplotlib jupyter

%environment
    export PYTHONPATH=/usr/local/lib/python3.8/site-packages
    export LC_ALL=C

%runscript
    python3 "$@"

%labels
    Author Your Name
    Version v1.0
EOF
```

### Building the Container

```bash
# Build the container
apptainer build myapp.sif myapp.def

# Build with cache directory (recommended for large builds)
apptainer build --cache-dir /tmp/singularity-cache myapp.sif myapp.def
```

---

## 📁 Working with Data

### Binding Directories

Mount your data directories into the container:

```bash
# Bind a single directory
apptainer exec -B /path/to/data:/data myapp.sif bash

# Bind multiple directories
apptainer exec -B /path/to/data:/data,/path/to/results:/results myapp.sif bash

# Bind your home directory (common pattern)
apptainer exec -B $HOME myapp.sif bash
```

### Example: Data Analysis Workflow

```bash
# Create a working directory
mkdir -p ~/container-work

# Run analysis in container with data mounted
apptainer exec -B ~/container-work:/work myapp.sif python3 /work/analysis.py
```

---

## 🚀 Running Containers in Jobs

### Interactive Jobs

```bash
# Request an interactive session
srun --pty --partition=zen4 --cpus-per-task=4 --mem=8G bash

# Load any required modules
module load cuda/12.6.2  # if using GPU

# Run your container
apptainer exec myapp.sif python3 my_script.py
```

### Batch Jobs

Create a job script for batch execution:

```bash
#!/bin/bash
#SBATCH --job-name=container-job
#SBATCH --partition=zen4
#SBATCH --cpus-per-task=4
#SBATCH --mem=8G
#SBATCH --time=02:00:00
#SBATCH --output=container_%j.out
#SBATCH --error=container_%j.err

# Load modules if needed
module load cuda/12.6.2

# Run container with data binding
apptainer exec -B $HOME:/home/user myapp.sif python3 /home/user/my_analysis.py
```

---

## 🔍 Finding Containers

### Popular Container Sources

- **Docker Hub**: `docker://library/ubuntu`
- **Singularity Hub**: `shub://vsoch/hello-world`
- **NGC (NVIDIA)**: `docker://nvcr.io/nvidia/pytorch:23.12-py3`
- **Biocontainers**: `docker://biocontainers/fastqc:v0.11.9_cv8`

### Scientific Computing Containers

```bash
# PyTorch with CUDA
apptainer pull docker://nvcr.io/nvidia/pytorch:23.12-py3

# TensorFlow
apptainer pull docker://tensorflow/tensorflow:latest-gpu

# Jupyter with scientific stack
apptainer pull docker://jupyter/datascience-notebook:latest
```

### AI Applications

For trending AI applications like Ollama, see our dedicated guide:

- [Running Ollama](running-ollama.md) - Example of using containers for AI applications



---

## 🎯 Best Practices

### Container Management

- **Use descriptive names** for your containers
- **Version your containers** (e.g., `myapp_v1.0.sif`)
- **Store containers in `$WORK`** for large files
- **Document container contents** and dependencies

### Performance Considerations

- **Use local storage** (`$HOME` or `$WORK`) for containers
- **Bind only necessary directories** to avoid overhead
- **Consider container size** for transfer and storage
- **Use appropriate partitions** (GPU containers on h100)

### Security

- **Only use trusted container sources**
- **Verify container contents** before running
- **Don't run containers as root** unless necessary
- **Keep containers updated** for security patches

---

## 🛠️ Troubleshooting

### Common Issues

1. **Permission denied**: Ensure container file is executable
   ```bash
   chmod +x myapp.sif
   ```

2. **Cannot bind directory**: Check directory permissions and existence
   ```bash
   ls -la /path/to/data
   ```

3. **Container not found**: Verify container file exists and path is correct
   ```bash
   ls -la *.sif
   ```

4. **Out of disk space**: Use `$WORK` directory for large containers
   ```bash
   apptainer build $WORK/myapp.sif myapp.def
   ```

---

## 📚 Related Documentation

- [Software Management Overview](index.md) - General software management
- [Module System](module-system.md) - System software via modules
- [Building from Source](building-from-source.md) - Alternative to containers
- [Running Jobs](../running-jobs/basics.md) - Job submission and management

---

## 🆘 Support

For container-related issues or assistance, contact:

```
repacss.support@ttu.edu
```
