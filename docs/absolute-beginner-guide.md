# Welcome Home: A Beginner’s Guide to Using REPACSS

Welcome to REPACSS! Whether you’re an undergraduate student, a new graduate researcher, or just someone eager to get started with high-performance computing, this guide is for you. Our goal is to walk you through the basics of using the REPACSS cluster — from logging in to running your first job.

To make things easier to understand, we’ll use the analogy of a house. REPACSS is like a shared home. You enter through the front door (logging in), have your own room for small items (your home directory), a few common areas like closets and garages for larger items (project and scratch storage), and a kitchen (compute nodes) where the real work happens.

---

## 🔑 Unlocking the Front Door: Logging In

Before you can start working on REPACSS, you need to log in to the system using SSH.

### SSH Login (The Front Door)

To log in from your local terminal:

```bash
ssh <your_username>@repacss.hpcc.ttu.edu
```

If this is your first time connecting, you'll likely be prompted to verify the server's RSA key fingerprint. Type `yes` to continue. You’ll then enter your password and any additional multi-factor authentication code if your account has MFA enabled.

!!! note 
    Login nodes are for setup and light work only — like standing in your foyer. Heavy lifting (computation) should always be done on the compute nodes.

---

## 🗄 This House Has Closets: Navigating Storage

REPACSS provides different types of storage spaces based on what you’re doing.

| Storage Type  | Location              | Purpose                                |
|---------------|-----------------------|----------------------------------------|
| Home          | `/home/$USER`         | Permanent space for small files/scripts |
| Scratch       | `/scratch/$USER`      | Fast temporary storage during jobs     |
| Project/Group | `/project/<group>`    | Shared space for team/project data     |

Your home directory is like your room. Keep only essentials here — it’s backed up and secure. Scratch is like the garage: great for big, messy projects in progress, but regularly cleaned out. Project storage is your shared closet with teammates.

!!! warning
    Files in `/scratch` may be automatically deleted if left inactive for too long. Always back up important work!

---

## 🍳 Cooking with Fire: Running Jobs

Now that you’re inside the house, it’s time to use the kitchen — the compute nodes.

You can’t just start computing from the login node. Instead, you must write and submit a **job script** to run your program on compute nodes.

### Example: A Simple Job Script

Create a file called `hello.sh`:

```bash
#!/bin/bash
#SBATCH --job-name=hello
#SBATCH --output=hello.out
#SBATCH --time=00:05:00
#SBATCH --ntasks=1
#SBATCH --partition=standard

echo "Hello from REPACSS!"
```

Submit it with:

```bash
sbatch hello.sh
```

Check its status with:

```bash
squeue -u $USER
```

!!! tip
    The `--partition` flag selects which group of compute nodes to use. Common options include `standard`, `gpu`, and `debug`.

---

## 📦 Recipe Book: Software and Modules

REPACSS uses a **module system** to manage software packages. Instead of installing everything yourself, just load what you need!

### Common Module Commands

```bash
module avail            # See available software
module load gcc         # Load a module
module list             # View currently loaded modules
module unload gcc       # Unload a module
```

If your job needs specific software, include the `module load` commands at the top of your job script.

!!! example
    To use Python in a job, your script might start with:

    ```bash
    module load python
    ```

---

## 🧠 Helpful Hints and Where to Get Help

Everyone starts somewhere — and nobody knows everything. If you run into trouble:

- Check this user guide
- Ask your PI, research group, or lab manager
- Visit [Support](support.md) to contact the REPACSS team

!!! tip
    When asking for help, include error messages and describe what you were trying to do. The more detail, the better!

---

## 🧹 House Rules: Good HPC Citizenship

Because REPACSS is a shared resource, there are a few best practices to follow:

- **Don’t compute on the login node.**
- **Use scratch for temporary work**, but clean it regularly.
- **Keep jobs short in the `debug` partition**; use `standard` for production runs.
- **Be respectful of shared storage**; avoid hoarding large files.

---

## 🏁 Make Yourself at Home

Congratulations! You now understand the basics of REPACSS:

- You’ve logged in
- Learned the storage layout
- Loaded software
- Written and submitted a job

This is just the beginning — explore more detailed topics in the rest of the documentation as you grow comfortable.

Happy computing — and welcome to the cluster!
