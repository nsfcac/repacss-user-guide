# 📦 Module System

REPACSS uses the **Lmod module system** to manage software environments. Modules allow users to dynamically modify their shell environment by loading and unloading installed software packages.

---

## 🔍 Checking Available Modules

To see all available software modules:

```bash
module avail
```

You can search for a specific module by name:

```bash
module avail python
```

---

## 🕷️ Using `module spider`

`module spider` offers advanced search capabilities and provides information about module versions and dependencies.

Search for all matching modules:

```bash
module spider python
```

To get detailed info about a specific version:

```bash
module spider python/3.11.0
```

---

## 📥 Loading a Module

To use a software package, load its module:

```bash
module load gcc/12.2.0
module load openmpi/4.1.5
```

You can load multiple modules at once:

```bash
module load gcc/12.2.0 cuda/12.0
```

---

## 📤 Unloading a Module

To unload a specific module:

```bash
module unload gcc/12.2.0
```

Unload all loaded modules:

```bash
module purge
```

---

## 📄 Viewing Module Details

To inspect the environment changes a module will make:

```bash
module show hdf5
```

---

## 🧾 Listing Loaded Modules

To see which modules you have currently loaded:

```bash
module list
```

---

## 💡 Tips

* Load required modules in your job scripts before launching your application.
* Use `module purge` at the top of scripts to ensure a clean environment.
* If you encounter conflicts, try purging and reloading modules.

---

## 📚 Learn More

Visit the [Available Software](available-software.md) page for a list of software provided on REPACSS.

For Python-related setups, see [Installing Packages](installing-packages.md).
