# Advanced Package Installation

This document covers advanced scenarios for installing software packages on REPACSS when the standard approaches (module system and conda) are not sufficient.

## 🎯 When to Use This Guide

Use this guide when you need to:

- Install packages not available in the module system
- Install packages not available in conda-forge
- Set up specialized applications
- Install packages with specific version requirements

**For standard Python environments, see [Getting Started with MiniForge](miniforge.md) instead.**
**For containers, see [Using Containers](containers.md).**
**For source builds, see [Building from Source](building-from-source.md).**

---

## 📦 Installing Python Packages with Pip

When a package is unavailable via `conda`, you can use `pip` within an activated conda environment:

```bash
# Activate your conda environment first
conda activate myenv

# Install packages with pip
pip install somepackage

# Install from requirements.txt
pip install -r requirements.txt
```

!!! warning "Important"
    Always use `pip` inside an activated conda environment to prevent conflicts with system Python.

---

## 🎯 Best Practices

### Directory Structure

- Install user software in `$HOME` or `$WORK`
- Use descriptive directory names: `$HOME/software/myapp`
- Keep installations organized by project or purpose

### Environment Management

- Use conda environments for Python packages
- Use module system when possible
- Document your installation procedures
- Version your software installations

### Resource Considerations

- Install large software in `$WORK` directory
- Use symbolic links from `$HOME` if needed
- Clean up old installations regularly

---

## 🚨 Important Guidelines

- **Never install to system directories** (`/usr`, `/opt`, etc.)
- **Always use user-controlled directories** (`$HOME`, `$WORK`)
- **Test installations** before using in production workflows
- **Document dependencies** for reproducibility

---

## 📚 Related Documentation

- [Software Management Overview](index.md) - General software management
- [Module System](module-system.md) - Using pre-installed software
- [Getting Started with MiniForge](miniforge.md) - Python environment management
- [Using Containers](containers.md) - Container-based installations
- [Building from Source](building-from-source.md) - Source compilation

---

## 🆘 Support

For assistance with complex installations or to request system-level software, contact:

```
repacss.support@ttu.edu
```
