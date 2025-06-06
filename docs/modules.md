# Module System (Lmod)

## 📘 What Are Modules?
Modules dynamically configure your environment to access compilers, libraries, and applications without permanently changing your shell configuration.

## 🔧 Basic Module Commands
```bash
module avail              # List available modules
module load gcc/12.2.0    # Load a specific module
module list               # Show currently loaded modules
module unload gcc         # Unload a module
module purge              # Unload all modules
```

## 🔍 Search Modules
```bash
module spider python      # Search for a module
module spider openmpi
```

## 💡 Commonly Used Modules
```bash
module load gcc
module load openmpi
module load cuda
```

## 🛠 Auto-load on Login
To auto-load modules every time you log in, add them to your `.bashrc` or `.bash_profile`:
```bash
module load gcc
module load openmpi
```

## 🧠 Tips & Best Practices
- Always load the compiler before dependent libraries
- Unload conflicting modules to avoid errors
- Use `module purge` if you're unsure what's active

## 🔗 Related Pages
- [Available Software](available-software.md)
- [Python Setup](python.md)
