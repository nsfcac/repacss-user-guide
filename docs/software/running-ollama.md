# Running Ollama on REPACSS

A comprehensive guide for running Ollama (local LLM inference) on REPACSS GPU clusters using containers.

## 🎯 Overview

Ollama is a popular AI application for running large language models locally. This guide shows you how to deploy Ollama using containers on REPACSS GPU nodes.


**This is an example of using containers (user-installed) for AI applications.** For general container usage, see [Using Containers](containers.md).

The REPACSS team also provides a repository with pre-configured scripts (`https://github.com/nsfcac/ollama_repacss.git`) that includes:
- Helper scripts for easy setup
- Example Python scripts for testing
- Jupyter notebook tutorials
- Pre-configured environment settings

---

## 🚀 One-Time Setup

### Clone the Repository (Only Once)

Choose a directory and clone the Ollama configuration repository. This only needs to be done once:

```bash
cd $HOME
mkdir <your_ollama_working_dir>
cd <your_ollama_working_dir>
git clone https://github.com/nsfcac/repacss_ollama_configuration.git
```

This repository contains:
- **`setup_ollama.sh`**: A setup script to install and launch the Ollama server
- **`ollama.sh`**: A script to set the configurations of the Ollama server
- **`test.py`**: An example Python script to verify your Ollama server is working
- **`tutorial.ipynb`**: A Jupyter notebook that connects to your Ollama server
- **`requirements.txt`**: Python libraries needed to run the notebook

---

## 🧪 Running Ollama (Every Time)

### Step 1: Request GPU Resources

Use the following command to start an interactive job with 1 GPU for 2 hours:

```bash
interactive -p h100 -t 02:00:00 -g 1
```

### Step 2: Set Up Environment and Start Ollama

We are using ollama 0.6.8 in this version. The first time will take several minutes to download the .sif engine file:

```bash
# Navigate to your repository
cd $HOME/<your_ollama_working_dir>/repacss_ollama_configuration

# Set up and launch the Ollama server
source setup_ollama.sh
```

---

## 🎯 Using Ollama

### Step 1: Check Available Models

We are using a shared LLM directory on REPACSS. Check the model list first:

```bash
ollama list
```

### Step 2: Run Inference with Existing Models

Use existing models (example with falcon3:1b):

```bash
ollama run falcon3:1b
```

### Step 3: Pull and Use New Models (Optional)

If you want to use a new model, choose a model supported by Ollama and pull it:

```bash
# Pull a new model
ollama pull llama3.1:8b

# Test the new model
ollama run llama3.1:8b
>>> what is the capital of Texas?
```

### Step 4: Verify Server Status from Login Node

From a login node (not the GPU node), check if the Ollama server is running:

```bash
curl http://<hostname>:<port>
```

You can find a `host.txt` and `port.txt` in your `<your_ollama_working_dir>/ollama` folder. Replace `<hostname>` with your GPU node's hostname and `<port>` with your Ollama server's port number.

You should see:

```
Ollama is running
```

## 📋 Running Ollama in Batch Mode

For production workloads or long-running inference, use batch jobs:

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

### Using Jupyter Notebook

You can also access Ollama through Jupyter Notebook for interactive development:

```bash
# From login node, start Jupyter
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081

# From your local machine, create SSH tunnel
ssh -L 8081:127.0.0.1:8081 -l <your_account> -fN repacss.ttu.edu
```

Then open `http://127.0.0.1:8081` in your browser and explore the `tutorial.ipynb` notebook.

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


1. **Port conflicts**
   ```bash
   # Use dynamic port allocation
   export OLPORT=$(python -c "import socket; s = socket.socket(); s.bind(('', 0));print(s.getsockname()[1]);s.close()")
   ```

2. **Memory issues**
   ```bash
   # Reduce CPU count or use smaller models
   # Check available memory
   free -h
   ```

3. **Model download problems**
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
