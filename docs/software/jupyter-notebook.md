# Running Jupyter Notebook on REPACSS

A comprehensive guide for running Jupyter Notebook for interactive Python development on REPACSS using conda environments.

## 🎯 Overview

Jupyter Notebook is a popular application for interactive Python development that can be installed in your conda environments. This guide shows you how to set up and run Jupyter Notebook on REPACSS.

**This is an example of using conda (user-installed) for interactive Python development.** For general conda setup, see [Getting Started with MiniForge](miniforge.md).

---

## 🚀 Quick Start

### Prerequisites

- Conda environment with Jupyter installed
- Access to REPACSS login nodes or compute nodes

### Basic Setup

```bash
# Activate your conda environment
conda activate myenv

# Install Jupyter if not already installed
conda install jupyter notebook ipykernel

# Launch Jupyter
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081
```

---

## 📦 Installing Jupyter in Your Environment

### Step 1: Set Up Conda Environment

Before setting up Jupyter Notebook, you need to have conda available on your system. If you haven't set up conda yet, please follow our [Getting Started with MiniForge](miniforge.md) guide first.

Once conda is installed, verify it's working:

```bash
conda --version
```

You should see output similar to:

```bash
repacss:$ conda --version
conda 25.5.1
```

### Step 2: Create and Activate Environment

```bash
# Create a new environment for your project
conda create -n jupyter_env python=3.10 jupyter ipykernel -y

# Activate the environment
conda activate jupyter_env
```

You should now see your prompt change to:

```bash
(jupyter_env) repacss:$
```

### Step 3: Install Additional Packages

```bash
# Install common data science packages
conda install numpy scipy matplotlib pandas scikit-learn

# Install additional Jupyter extensions (optional)
conda install jupyter_contrib_nbextensions
```

---

## 🚀 Launching Jupyter Notebook

### On Login Node

```bash
# Start Jupyter on login node
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081
```

You'll see output like:

```bash
To access the server, open this file in a browser:
    file:///mnt/REPACSS/home/username/.local/share/jupyter/runtime/jpserver-1341111-open.html
Or copy and paste one of these URLs:
    http://127.0.0.1:8081/tree?token=...
```

### On Compute Nodes (Recommended for Heavy Work)

```bash
# Request an interactive session
interactive -p zen4 -c 4 -m 8G

# Activate your environment
conda activate jupyter_env

# Launch Jupyter
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081
```

---

## 🌐 Accessing Jupyter Remotely

### Setting Up SSH Tunnel

If you're running Jupyter on a remote server, set up an SSH tunnel from your local machine:

```bash
ssh -L 8081:127.0.0.1:8081 -l <your_username> -fN repacss.ttu.edu
```

Replace `<your_username>` with your actual username.

### Accessing in Browser

Then open `http://127.0.0.1:8081/` in your local browser.

You should now see the Jupyter interface.

---

## 🔥 Running Jupyter on GPU Nodes

For GPU-accelerated work:

### Step 1: Request GPU Resources

```bash
# Request interactive session with GPU
interactive -p h100 -t 02:00:00 -g 1
```

### Step 2: Set Up Environment

```bash
# Activate your environment
conda activate jupyter_env

# Load CUDA module if needed
module load cuda/12.6.2
```

### Step 3: Set Up SSH Tunnel to GPU Node

From your local machine, set up tunnel to the specific GPU node:

```bash
ssh -L 8081:rpg-93-1:8081 -l <username> -fN repacss.ttu.edu
```

Replace `rpg-93-1` with your actual GPU node name.

### Step 4: Launch Jupyter

```bash
# Launch Jupyter on GPU node
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081
```

You are now running Jupyter Notebook with access to GPU resources!

---

## 🛑 Stopping Jupyter Notebook

### Graceful Shutdown

To stop the Jupyter server, go to the terminal where it's running and:

- Press `Ctrl + C`, then type `y` and press `Enter`
  **OR**
- Press `Ctrl + C` twice quickly to force shutdown

### Example:

```bash
^C
Shutdown this notebook server (y/[n])? y
[C 12:00:00.000 NotebookApp] Shutdown confirmed
```

### Clean Up

Also remember to:
- Close the SSH tunnel if it's still active
- Exit the compute node session when done: `exit`

---

## 🎯 Best Practices

### Resource Management

- **Use compute nodes** for heavy computational work
- **Request appropriate resources** - don't over-allocate
- **Exit sessions promptly** when done
- **Use batch jobs** for long-running notebooks

### Security

- **Use SSH tunnels** for remote access
- **Don't expose Jupyter** to external networks
- **Use tokens** for authentication
- **Keep your environment updated**

### Performance

- **Use GPU nodes** for machine learning workloads
- **Monitor resource usage** during execution
- **Close unused notebooks** to free memory
- **Use appropriate kernels** for your environment

---

## 🛠️ Troubleshooting

### Common Issues

1. **Port already in use**
   ```bash
   # Find and kill processes using the port
   lsof -ti:8081 | xargs kill -9
   ```

2. **Cannot connect to Jupyter**
   - Check if SSH tunnel is active
   - Verify the correct port is being used
   - Ensure Jupyter is running on the expected IP

3. **Environment not found**
   ```bash
   # List available environments
   conda env list
   
   # Recreate environment if needed
   conda create -n jupyter_env python=3.10 jupyter ipykernel
   ```

4. **GPU not available**
   ```bash
   # Check if you're on a GPU node
   nvidia-smi
   
   # Request GPU resources if needed
   interactive -p h100 -t 02:00:00 -g 1
   ```

### Debug Mode

Enable debug output for troubleshooting:

```bash
jupyter notebook --debug --no-browser --ip=127.0.0.1 --port=8081
```

---

## 📚 Related Documentation

- [Getting Started with MiniForge](miniforge.md) - Setting up conda environments
- [Software Management Overview](index.md) - General software management
- [Running Jobs](../running-jobs/basics.md) - Job submission and management
- [Running Ollama](running-ollama.md) - Another trending application

---

## 🆘 Support

For Jupyter-specific issues or assistance, contact:

```
repacss.support@ttu.edu
```
