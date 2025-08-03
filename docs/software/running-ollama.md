# Running Ollama on REPACSS

This guide provides instructions for running the Ollama large language model (LLM) management server on the REPACSS cluster in a batch or interactive session. A couple of variations are included below for you to experiment with. Please choose the minimum amount of resources if you use this program, as described below, as it is resource-intensive and other cluster account holders may also be in contention for these resources.

**Important: A session on the h100 GPU partition is required for most models.** Although it is technically possible to run on one of the CPU partitions (zen4), performance will be very slow for all except the smallest models, even with a full node request in terms of the number of cores. The h100 partition has multiple GPUs per node, and availability varies by usage, so to minimize contention, we suggest that you minimize long-term intensive use or long interactive sessions to keep these resources available for as many people as possible. **If using an interactive session, please exit as soon as you are done and do not leave the session idle.**

**The current version of CUDA on the h100 partition is 12.6.2. The most recent version of Ollama that supports this version of CUDA in the prebuilt tarball is 0.9.2 and the instructions below are set up for this version only. You can replace this with any previous version but until the h100 partition has been upgraded, please do not exceed this version.**

---

## Step by Step Guide

### 1. Preparation (Can be done on login nodes)

Create a directory called ollama in your home area and cd into it:

```bash
cd ~
mkdir ollama-0.9.2
cd ollama-0.9.2
```

Download the latest AMD64 architecture tarball from the GitHub web site for ollama ([https://github.com/ollama/ollama/releases](https://github.com/ollama/ollama/releases)). For example, the current one can be fetched with the command:

```bash
wget https://ollama.com/download/ollama-linux-amd64.tgz?version=0.9.2 -O ollama-linux-amd64.tgz
```

Then unpack this in your ollama directory with:

```bash
tar -zxvf ollama-linux-amd64.tgz
```

### 2. Requesting Resources

For most problems you will want to run ollama with GPU assistance. For each interactive or batch session on h100, you can request either one or two GPUs and a suitable number of CPUs. You can choose any number from 1 to 20 CPUs for a single GPU job or from 1 to 40 CPUs for a 2-GPU job. For further information, see our [Job Submission Guide](../running-jobs/basics.md).

For example, if trying this interactively, the commands would be either:

```bash
# for a 1-GPU interactive job, use the command below
srun --pty --partition=h100 --gres=gpu:1 --cpus-per-task=20 --mem=64G bash
```

or

```bash
# for a 2-GPU job, same considerations as above
srun --pty --partition=h100 --gres=gpu:2 --cpus-per-task=40 --mem=128G bash
```

You can check the number of GPUs in your session with the **nvidia-smi** command. The default memory allocations made by the scheduler in each case should be fine.

### 3. Loading Required Modules

Once you have an interactive session on the h100 partition, load the CUDA module:

```bash
module load cuda/12.6.2
```

You can verify the CUDA installation with:

```bash
nvcc --version
```

### 4. Running Ollama

The commands below can be used in either the run script for a batch or in an interactive session.

Get a free port number and start an instance of the ollama server on it in the background as follows:

```bash
export OLPORT=$(python -c "import socket; s = socket.socket(); s.bind(('', 0));print(s.getsockname()[1]);s.close()");
export OLLAMA_HOST=127.0.0.1:$OLPORT;
export OLLAMA_BASE_URL="http://localhost:$OLPORT";
~/ollama-0.9.2/bin/ollama serve >ollama_$OLPORT.log 2>ollama_$OLPORT.err &
```

Within that same session, you should be able to connect to the running ollama server on that node and port using the command:

```bash
~/ollama-0.9.2/bin/ollama
```

For example, the command below should work to start an instance of the llama3.2 model running on that particular ollama server in the background. This is just an example; you should be able to choose any of the available models from the ollama library. The "--verbose" flag is optional but will allow you to see the speed of the responses to your prompts. If further information is needed, you can add "export OLLAMA_DEBUG=1" to the commands issued before starting the server above.

```bash
~/ollama-0.9.2/bin/ollama run llama3.2 --verbose
```

**The startup for this command may take several seconds if the model has already been downloaded, or longer if the model is being fetched for the first time.** Once the session starts, response will depend on the complexity of your prompt, the model chosen, and other factors.

Optionally, you could add the ~/ollama/bin directory to your PATH to avoid having to type that part in explicitly:

```bash
export PATH=~/ollama-0.9.2/bin:$PATH
```

To check that this is finding your Ollama executable, issue the command:

```bash
which ollama
```

---

## Batch Job Example

Running any production studies once your code is working is best done in batch jobs. This approach is preferable once you have your planned commands worked out for the set of work you would like to do, since this will not require waiting for an interactive session to open up. Details on how to set up a batch job are described in the [Job Submission Guide](../running-jobs/basics.md).

Here's an example batch script for running Ollama:

```bash
#!/bin/bash
#SBATCH --job-name=ollama-test
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

# Set up Ollama environment
export OLPORT=$(python -c "import socket; s = socket.socket(); s.bind(('', 0));print(s.getsockname()[1]);s.close()");
export OLLAMA_HOST=127.0.0.1:$OLPORT;
export OLLAMA_BASE_URL="http://localhost:$OLPORT";

# Start Ollama server
~/ollama-0.9.2/bin/ollama serve >ollama_$OLPORT.log 2>ollama_$OLPORT.err &

# Wait for server to start
sleep 10

# Run your Ollama commands here
~/ollama-0.9.2/bin/ollama run llama3.2 --verbose << EOF
What is the capital of France?
EOF

# Clean up
pkill ollama
```

---

## Overall Information

The session you are in should pick up and respect the OLLAMA_HOST and OLLAMA_BASE environmental variables defined above, which will point the client command to the right server instance. If running in batch, you may wish to feed the prompt(s) you want to the ollama client. There are several ways to do this, including either feeding the prompt in the ollama run command, skipping the client entirely and simply interacting with the running ollama instance on that port using curl, etc., so you can tune this step towards a useful batch workflow depending on your needs.

The ollama server background session will terminate automatically when you sign out of the interactive session or when your batch job terminates. This procedure should keep separate instances from colliding with each other in simultaneous interactive or batch jobs, even if other REPACSS account holders run this or similar programs on the same nodes up to their batch resource limits.

You can experiment with the number of CPUs in your session, though since there are multiple GPUs in each h100 node, there is usually no harm in asking for the number of CPUs that corresponds to your GPU request as above, and with either running two separate ollama client/server instances using only one GPU at a time per session as above, or with using both GPUs in a single session to see if this will result in faster processing of your prompts.

One final note: availability of the h100 partition varies greatly. You may need to wait for some time for an interactive session if the partition is busy, or for a batch job to start, especially if you have been making a lot of use of the partition, depending on the current activity and your recent history of usage. This is why we recommend setting your work up to run as batch jobs if possible.

---

## Troubleshooting

### Common Issues

1. **CUDA not found**: Make sure you've loaded the CUDA module:
   ```bash
   module load cuda/12.6.2
   ```

2. **Port already in use**: The script automatically finds a free port, but if you encounter issues, you can manually specify a port:
   ```bash
   export OLPORT=12345
   ```

3. **Model download issues**: Some models are large and may take time to download. Check the log files for progress:
   ```bash
   tail -f ollama_$OLPORT.log
   ```

4. **Memory issues**: If you encounter memory problems, try reducing the number of CPUs or using a smaller model.

### Debugging

To enable debug output, add this before starting the server:

```bash
export OLLAMA_DEBUG=1
```

Check the log files for detailed information:

```bash
cat ollama_$OLPORT.log
cat ollama_$OLPORT.err
```

---

## More Information and Support

For a full list of available software modules, see the [Module System](module-system.md) guide.

For job submission help, see the [Running Jobs](../running-jobs/basics.md) guide.

Need help? Contact REPACSS support:

```
repacss.support@ttu.edu
```
