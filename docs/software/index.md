# Software Management on REPACSS

This section covers all aspects of software management on REPACSS, organized by package management approach and use case.

## 🎯 Software Management Categories

### 1. **HPC Applications & System Software** → Spack + Module System
**System-provided software** - Users simply load what they need.

For HPC applications, compilers, libraries, and system-level software managed through Spack and loaded via the Lmod environment module system. **No installation required** - just load the modules you need.

**Start here:** [Module System](module-system.md)

### 2. **Data Science Applications** → Conda/MiniForge
**User-installed software** - Users install locally, then add packages.

For Python/R-based data science, machine learning, and scientific computing packages using MiniForge (conda) environments. **Requires local installation** of MiniForge, then install packages like [Jupyter Notebook](jupyter-notebook.md) for interactive development.

**Start here:** [Getting Started with MiniForge](miniforge.md)

### 3. **User Self-Installed Software** → Custom Solutions
**User-installed software** - Users install their own software using:

#### 3.1 **Containers (Apptainer)** → Pre-built Binaries
For pre-built applications, complex software stacks, and reproducible environments. Examples include [Ollama](running-ollama.md) for AI applications.

**Start here:** [Using Containers](containers.md)

#### 3.2 **Building from Source** → Custom Compilation
For software that needs to be compiled from source code with specific configurations.

**Start here:** [Building from Source](building-from-source.md)

---

## 🚀 Popular User Applications

### **Commonly Used Software** → User-Installed Applications
Popular applications that users frequently install and use, demonstrating how to use the package management methods above:

- **[Running Jupyter Notebook](jupyter-notebook.md)** - Using conda (category 2) for interactive development
- **[Running Ollama](running-ollama.md)** - Using containers (category 3.1) for AI applications

---

## 📋 Quick Reference

| Category | Installation Type | Use Case | Solution | Documentation |
|----------|-------------------|----------|----------|---------------|
| HPC Applications | **System-provided** | Compilers, MPI, scientific libraries | Module system | [Module System](module-system.md) |
| Data Science | **User-installed** | Python/R packages, ML frameworks | MiniForge (conda) | [Getting Started with MiniForge](miniforge.md) |
| Pre-built Applications | **User-installed** | Complex software stacks | Apptainer containers | [Using Containers](containers.md) |
| Custom Software | **User-installed** | Source compilation, specialized tools | Build from source | [Building from Source](building-from-source.md) |

### Popular User Applications
| Application | Package Management Method | Installation Type | Documentation |
|-------------|---------------------------|-------------------|---------------|
| Jupyter Notebook | Conda (Data Science) | User-installed | [Running Jupyter Notebook](jupyter-notebook.md) |
| Ollama | Containers (User Self-Install) | User-installed | [Running Ollama](running-ollama.md) |

---

## 🚀 Getting Started

1. **HPC applications?** Check available modules: `module avail` (system-provided)
2. **Data science work?** Set up MiniForge: See [Getting Started with MiniForge](miniforge.md) (user-installed)
3. **Custom software?** Choose containers or source build based on your needs (user-installed)
4. **Want popular applications?** See commonly used software: [Popular User Applications](#popular-user-applications)

---

## 📚 Documentation Structure

### Package Management Methods
- [Module System](module-system.md) - **System-provided** HPC applications via Spack + Lmod
- [Getting Started with MiniForge](miniforge.md) - **User-installed** data science with conda
- [Using Containers](containers.md) - **User-installed** Apptainer/Singularity containers
- [Building from Source](building-from-source.md) - **User-installed** source compilation
- [Advanced Installation](advanced-installation.md) - General installation guidance

### Popular User Applications
- [Running Jupyter Notebook](jupyter-notebook.md) - Using conda for interactive development
- [Running Ollama](running-ollama.md) - Using containers for AI applications

---

## 🆘 Need Help?

For software-related issues or to request new software installations, contact:
```
repacss.support@ttu.edu
```
