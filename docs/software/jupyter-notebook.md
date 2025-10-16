# Running Jupyter Notebook on REPACSS

A comprehensive guide for running Jupyter Notebook for interactive Python development on REPACSS using conda environments.

## 🎯 Overview

Jupyter Notebook is a popular application for interactive Python development that can be installed in your conda environments. This guide shows you how to set up and run Jupyter Notebook on REPACSS.

**This is an example of using conda (user-installed) for interactive Python development.** For general conda setup, see [Getting Started with MiniForge](miniforge.md).

---

## 🚀 Quick Start

### Prerequisites

- Conda environment with Jupyter installed
- Access to REPACSS compute nodes (zen4 for CPU jobs and h100 for GPU jobs)
- Jupyter must run inside an interactive job on compute nodes (login node is not allowed)

### Basic Setup

```bash
# Request an interactive session (login node not allowed)
interactive -p zen4 -c 4 -m 8G   # use -p h100 -g 1 for GPU

# Activate your conda environment
conda activate myenv

# Install Jupyter if not already installed
conda install jupyter notebook ipykernel

# Launch Jupyter
jupyter notebook --no-browser --ip=0.0.0.0 --port=8081
```

Note: If port `8081` is already in use, Jupyter may automatically select the next available port (for example, `8082`). Always use the actual port shown in Jupyter's startup output when creating your SSH tunnel and in your browser URL.

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

### Login Node (Not Allowed)

Running Jupyter on the login node is not allowed. Please request an interactive session on a compute node (see below) and launch Jupyter there.

### On Compute Nodes (Intended for Heavy Work)

```bash
# Request an interactive session
interactive -p zen4 -c 4 -m 8G

# Activate your environment
conda activate jupyter_env

# Launch Jupyter
jupyter notebook --no-browser --ip=0.0.0.0 --port=8081
```

Once the interactive session starts, note the allocated node name. For CPU `zen4` jobs it looks like `rpc-xx-x`; for GPU `h100` jobs it looks like `rpg-xx-x`. You can print it with:

```bash
hostname
```

---

## 🌐 Accessing Jupyter Remotely

### Setting Up SSH Tunnel

If you're running Jupyter on a remote server, set up an SSH tunnel from your local machine:

```bash
# For zen4 CPU nodes (hostnames look like rpc-xx-x)
ssh -L <your-local-port>:rpc-xx-x:<remote-port> -l <your_username> -fN repacss.ttu.edu

# For h100 GPU nodes (hostnames look like rpg-xx-x)
ssh -L <your-local-port>:rpg-xx-x:<remote-port> -l <your_username> -fN repacss.ttu.edu
```

Replace `<your_username>` with your actual username, `rpc-xx-x`/`rpg-xx-x` with the node name printed by `hostname`, `<remote-port>` with the real port printed by Jupyter on the compute node (e.g., `8081`, `8082`, etc.), and choose `<your-local-port>` for your machine (for example, `8081`). You can find the `<remote-port>` in the startup message like `http://127.0.0.1:<remote-port>/tree?token=...` or by running `jupyter server list` on the compute node.

### Accessing in Browser

Then open `http://127.0.0.1:<your-local-port>/` in your local browser.
Example: if you used `8081` locally, open `http://127.0.0.1:8081/`.

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

### Step 3: Launch Jupyter

```bash
# Launch Jupyter on GPU node
jupyter notebook --no-browser --ip=127.0.0.1 --port=8081
```

Note: Jupyter may auto-select a different port if `8081` is taken. Use the port printed in the startup output (the `<remote-port>` in the URL) or run `jupyter server list` on the node to discover it.

### Step 4: Set Up SSH Tunnel to GPU Node

From your local machine, set up tunnel to the specific GPU node using the `<remote-port>` from the previous step:

```bash
ssh -L <your-local-port>:rpg-xx-x:<remote-port> -l <username> -fN repacss.ttu.edu
```

Replace `rpg-xx-x` with your actual GPU node name (GPU nodes start with `rpg-`) and `<remote-port>` with the actual Jupyter port shown in the GPU node's startup output. Use `jupyter server list` on the node if unsure.

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
   - Alternatively, start Jupyter with your preferred port and let it auto-select the next available port. Then update your SSH tunnel to use the actual port shown in the Jupyter startup message.
   - To discover the active port, check the startup output for a URL like `http://127.0.0.1:<port>/...` or run:
   - To discover the active port, check the startup output for a URL like `http://127.0.0.1:<remote-port>/...` or run:
     ```bash
     jupyter server list
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
