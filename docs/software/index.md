# Software Management on REPACSS

This section covers all aspects of software management on REPACSS, organized by package management approach and use case.

## 🎯 Software Management Categories

### 1. **HPC Applications & System Software** → Spack + Module System
For HPC applications, compilers, libraries, and system-level software managed through Spack and loaded via the Lmod environment module system.

**Start here:** [Module System](module-system.md)

### 2. **Data Science Applications** → Conda/MiniForge
For Python/R-based data science, machine learning, and scientific computing packages using MiniForge (conda) environments. This includes applications like Jupyter Notebook for interactive development.

**Start here:** [Getting Started with MiniForge](miniforge.md)

### 3. **User Self-Installed Software** → Custom Solutions
For software not available through the above methods, users can install their own software using:

#### 3.1 **Containers (Apptainer)** → Pre-built Binaries
For pre-built applications, complex software stacks, and reproducible environments.

**Start here:** [Using Containers](containers.md)

#### 3.2 **Building from Source** → Custom Compilation
For software that needs to be compiled from source code with specific configurations.

**Start here:** [Building from Source](building-from-source.md)

#### 3.3 **Trending AI Applications** → Specialized AI Tools
For popular AI applications that use containers for deployment.

**Start here:** [Running Ollama](running-ollama.md)

---

## 📋 Quick Reference

| Category | Use Case | Solution | Documentation |
|----------|----------|----------|---------------|
| HPC Applications | Compilers, MPI, scientific libraries | Module system | [Module System](module-system.md) |
| Data Science | Python/R packages, ML frameworks, Jupyter | MiniForge (conda) | [Getting Started with MiniForge](miniforge.md) |
| Pre-built Applications | Complex software stacks | Apptainer containers | [Using Containers](containers.md) |
| Custom Software | Source compilation, specialized tools | Build from source | [Building from Source](building-from-source.md) |
| AI Applications | LLM models, trending AI tools | Containers + specialized guides | [Running Ollama](running-ollama.md) |

---

## 🚀 Getting Started

1. **HPC applications?** Check available modules: `module avail`
2. **Data science work?** Set up MiniForge: See [Getting Started with MiniForge](miniforge.md)
3. **Custom software?** Choose containers or source build based on your needs

---

## 📚 Documentation Structure

### Core Package Managers
- [Module System](module-system.md) - HPC applications via Spack + Lmod
- [Getting Started with MiniForge](miniforge.md) - Data science with conda (includes Jupyter)

### User Self-Installation
- [Using Containers](containers.md) - Apptainer/Singularity containers
- [Building from Source](building-from-source.md) - Source compilation
- [Running Ollama](running-ollama.md) - Trending AI application using containers

---

## 🆘 Need Help?

For software-related issues or to request new software installations, contact:
```
repacss.support@ttu.edu
```
