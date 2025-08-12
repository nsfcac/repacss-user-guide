# Running Ollama on REPACSS

A comprehensive guide for running Ollama (local LLM inference) on REPACSS GPU clusters using containers.

## 🎯 Overview

Ollama is a popular AI application for running large language models locally. This guide shows you how to deploy Ollama using containers on REPACSS GPU nodes.

**This is a trending AI application that uses containers for installation.** For general container usage, see [Using Containers](containers.md).

---

## 🚀 Quick Start Guide

### Prerequisites

- Access to REPACSS GPU nodes (h100 partition)
- `apptainer` module available
- Sufficient memory (64GB+ recommended)

### Step 1: Request GPU Resources

```bash
# Request interactive session with GPU
interactive -p h100 -t 02:00:00 -g 1
```

### Step 2: Set Up Ollama Environment

```bash
# Create project directory
cd $HOME
mkdir ollama-project
cd ollama-project

# Pull Ollama container (version 0.6.8 recommended)
apptainer pull ollama.sif docker://ollama/ollama:0.6.8

# Set scratch directory for models
export SCRATCH_BASE=/mnt/<Your Group Name>/home/$USER
```

### Step 3: Launch Ollama Server

```bash
# Start Ollama server in background
ollama serve &
```

### Step 4: Use Available Models

```bash
# List available models
ollama list

# Run a model (example with falcon3:1b)
ollama run falcon3:1b
```

### Step 5: Test Inference

```bash
# Test with a simple prompt
ollama run llama3.1:8b
>>> What is the capital of Texas?
```

---

## 📦 Installation Methods

### Method 1: Using Apptainer Container (Recommended)

```bash
# Pull the official Ollama container
apptainer pull ollama.sif docker://ollama/ollama:0.6.8

# Run Ollama from container
./ollama.sif serve &
```

### Method 2: Direct Installation

```bash
# Download Ollama binary
cd ~
mkdir ollama-0.9.2
cd ollama-0.9.2

# Download specific version for CUDA compatibility
wget https://ollama.com/download/ollama-linux-amd64.tgz?version=0.9.2 -O ollama-linux-amd64.tgz

# Extract and run
tar -zxvf ollama-linux-amd64.tgz
./ollama serve &
```

---

## 🔧 Advanced Configuration

### Using Shared Model Directory

REPACSS provides a shared LLM directory. Check available models first:

```bash
# List available models
ollama list

# Use existing models
ollama run falcon3:1b
```

### Pulling New Models

```bash
# Pull a new model
ollama pull llama3.1:8b

# Verify model is available
ollama list
```

### Environment Variables

```bash
# Set up port and host
export OLPORT=$(python -c "import socket; s = socket.socket(); s.bind(('', 0));print(s.getsockname()[1]);s.close()");
export OLLAMA_HOST=127.0.0.1:$OLPORT;
export OLLAMA_BASE_URL="http://localhost:$OLPORT";
```

---

## 🚀 Running Ollama in Different Modes

### Interactive Session

```bash
# Request GPU resources
srun --pty --partition=h100 --gres=gpu:1 --cpus-per-task=20 --mem=64G bash

# Load CUDA module
module load cuda/12.6.2

# Start Ollama server
ollama serve >ollama.log 2>ollama.err &

# Run models
ollama run llama3.2 --verbose
```

### Batch Job

```bash
#!/bin/bash
#SBATCH --job-name=ollama-inference
#SBATCH --partition=h100
#SBATCH --gres=gpu:1
#SBATCH --cpus-per-task=20
#SBATCH --mem=64G
#SBATCH --time=02:00:00
#SBATCH --output=ollama_%j.out
#SBATCH --error=ollama_%j.err

# Load required modules
module purge
module load cuda/12.6.2

# Start Ollama server
ollama serve >ollama.log 2>ollama.err &

# Wait for server to start
sleep 10

# Run inference
ollama run llama3.1:8b << EOF
What is the capital of France?
EOF

# Clean up
pkill ollama
```

---

## 🌐 Remote Access

### From Login Node

Check server status from a login node:

```bash
# Check if server is running
curl http://<hostname>:<port>

# You should see: "Ollama is running"
```

### Using Jupyter Notebook

From any node, launch Jupyter to interact with Ollama:

```bash
# Start Jupyter
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081

# Set up SSH tunnel from local machine
# ssh -L 8081:127.0.0.1:8081 -l <your_account> -fN repacss.ttu.edu
```

Then access `127.0.0.1:8081` in your browser to use the tutorial notebook.

---

## 🎯 Best Practices

### Resource Management

- **Use appropriate GPU resources** - Start with 1 GPU, scale as needed
- **Monitor memory usage** - Large models require significant RAM
- **Exit sessions promptly** - Don't leave GPU sessions idle
- **Use batch jobs** for long-running inference

### Model Selection

- **Start with smaller models** (1B-3B parameters) for testing
- **Use shared models** when available to save download time
- **Consider model requirements** - Some models need specific CUDA versions

### Performance Optimization

- **Use appropriate batch sizes** for your GPU memory
- **Monitor GPU utilization** with `nvidia-smi`
- **Consider model quantization** for faster inference

---

## 🛠️ Troubleshooting

### Common Issues

1. **CUDA not found**
   ```bash
   # Load CUDA module
   module load cuda/12.6.2
   ```

2. **Port conflicts**
   ```bash
   # Use dynamic port allocation
   export OLPORT=$(python -c "import socket; s = socket.socket(); s.bind(('', 0));print(s.getsockname()[1]);s.close()")
   ```

3. **Memory issues**
   ```bash
   # Reduce CPU count or use smaller models
   # Check available memory
   free -h
   ```

4. **Model download problems**
   ```bash
   # Check network connectivity
   # Use shared models when available
   ollama list
   ```

### Debug Mode

Enable debug output for troubleshooting:

```bash
export OLLAMA_DEBUG=1
ollama serve
```

### Log Files

Check log files for detailed information:

```bash
# Check server logs
tail -f ollama.log
tail -f ollama.err
```

---

## 📚 Related Documentation

- [Software Management Overview](index.md) - General software management
- [Using Containers](containers.md) - General container usage
- [Module System](module-system.md) - System software via modules
- [Running Jobs](../running-jobs/basics.md) - Job submission and management

---

## 🆘 Support

For Ollama-specific issues or assistance, contact:

```
repacss.support@ttu.edu
```
