# Running Ollama on REPACSS

A comprehensive guide for running Ollama (local LLM inference) on REPACSS GPU clusters using containers.

## 🎯 Overview

Ollama is a popular AI application for running large language models locally. This guide shows you how to deploy Ollama using containers on REPACSS GPU nodes.

The REPACSS team provides a repository with pre-configured scripts (`https://github.com/nsfcac/ollama_repacss.git`) that includes:
- Helper scripts for easy setup
- Example Python scripts for testing
- Jupyter notebook tutorials
- Pre-configured environment settings

**This is an example of using containers (user-installed) for AI applications.** For general container usage, see [Using Containers](containers.md).

---

## 🚀 Quick Start

### Prerequisites

- Access to REPACSS GPU nodes (h100 partition)
- `apptainer` module available
- Sufficient memory (64GB+ recommended)

### Basic Setup

```bash
# 1. Request GPU resources
interactive -p h100 -t 02:00:00 -g 1

# 2. Clone the repository
cd $HOME
git clone https://github.com/nsfcac/ollama_repacss.git
cd ollama_repacss

# 3. Pull Ollama container
apptainer pull ollama.sif docker://ollama/ollama:0.6.8

# 4. Set environment and source wrapper
export SCRATCH_BASE=/mnt/<Your Group Name>/home/$USER
source ollama.sh

# 5. Start Ollama server
ollama serve &

# 6. List and use available models
ollama list
ollama run falcon3:1b
```

---

## 📦 Installation Methods

### Using REPACSS Repository (Recommended)

The REPACSS team provides a repository with pre-configured scripts for easy setup. This method includes helper scripts and examples.

#### Step 1: Request GPU Resources

```bash
# Request interactive session with GPU
interactive -p h100 -t 02:00:00 -g 1
```

#### Step 2: Clone the Ollama Repository

Clone the REPACSS Ollama repository which contains pre-written scripts for convenient setup:

```bash
cd $HOME
cd <your_project>
git clone https://github.com/nsfcac/ollama_repacss.git
cd ollama_repacss
```

This repository contains:
- **`ollama.sh`**: A helper script to launch and manage the Ollama server
- **`test.py`**: An example Python script to verify your Ollama server is working
- **`tutorial.ipynb`**: A Jupyter notebook that connects to your Ollama server
- **`requirements.txt`**: Python libraries needed to run the notebook

#### Step 3: Download Ollama and Configure Environment

Download the Ollama container (we recommend version 0.6.8 for REPACSS) and set up the environment:

```bash
# Pull Ollama container (version 0.6.8 recommended)
apptainer pull ollama.sif docker://ollama/ollama:0.6.8

# Set scratch directory for models
export SCRATCH_BASE=/mnt/<Your Group Name>/home/$USER
```

#### Step 4: Source the Ollama Wrapper

This sets up a wrapper function to easily start the Ollama server and issue commands:

```bash
source ollama.sh
```

#### Step 5: Launch Ollama Server

Ollama server has been launched in the background:

```bash
ollama serve &
```

#### Step 6: Use Available Models

REPACSS provides a shared LLM directory. Check available models first:

```bash
# List available models
ollama list

# Use existing models (example with falcon3:1b)
ollama run falcon3:1b
```

If you want to use a new model, choose a model supported by Ollama and pull it:

```bash
# Pull a new model
ollama pull llama3.1:8b
```

#### Step 7: Test Inference

Test the model directly with a simple prompt:

```bash
ollama run llama3.1:8b
>>> What is the capital of Texas?
```

### Step 8: Verify Server Status from Login Node

From login node (repacs.ttu.edu), check if the Ollama server is running:

```bash
curl http://<hostname>:<port>
```
You can find a host.txt and port.txt in your ~/ollama folder/ Replace <hostname> with your GPU node's hostname and <port> with your Ollama server's port number. 

You should see:

```
Ollama is running
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
interactive -p h100 -t 02:00:00 -g 1

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

From a login node (not the GPU node), check if the Ollama server is running:

```bash
curl http://<hostname>:<port>
```

You can find a `host.txt` and `port.txt` in your `~/ollama` folder. Replace `<hostname>` with your GPU node's hostname and `<port>` with your Ollama server's port number.

You should see:

```
Ollama is running
```

### Using Jupyter Notebook

From a login node (not the GPU node), or any other nodes, you can run:

```bash
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081
```

Then on your terminal of local machine:

```bash
ssh -L 8081:127.0.0.1:8081 -l <your_account> -fN repacss.ttu.edu
```

Then you can explore the `tutorial.ipynb` in your browser (`127.0.0.1:8081`).

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
- [Running Jupyter Notebook](jupyter-notebook.md) - Another trending application
- [Running Jobs](../running-jobs/basics.md) - Job submission and management

---

## 🆘 Support

For Ollama-specific issues or assistance, contact:

```
repacss.support@ttu.edu
```
