# Module System

The REPACSS high-performance computing system utilizes the **Lmod environment module system** to manage access to installed software packages. This mechanism allows users to dynamically modify their shell environment, facilitating the configuration of compilers, libraries, and applications as needed for research and instructional activities.

---

## Listing Available Modules

To display all software modules currently available on the system, use the following command:

```bash
module avail
```

<!-- To filter results and search for specific software (e.g., Python), use: -->

<!-- ```bash
module avail python
``` -->

---

## Searching with `module spider`

The `module spider` command enables advanced search functionality. It is particularly useful for identifying available versions and any associated dependencies or prerequisites.

To locate all modules related to a specific keyword:

```bash
module spider python
```

To obtain detailed information for a specific module version:

```bash
module spider python/3.11.0
```

---

## Loading Modules

To configure the environment for use with a specific software package, load its module using:

```bash
module load gcc/14.2.0
module load openmpi/4.1.6
```

Multiple modules may be loaded simultaneously:

```bash
module load gcc/14.2.0 cuda/12.0
```

It is strongly recommended to specify exact version numbers to ensure consistency across computational workflows.

---

## Unloading Modules

To remove a specific software module from the current environment:

```bash
module unload gcc/14.2.0
```

To remove all loaded modules and restore a clean environment:

```bash
module purge
```

---

## Viewing Module Details

To review the environment modifications introduced by a specific module:

```bash
module show hdf5
```

This command will display paths, environment variables, and any dependencies configured upon loading.

---

## Listing Active Modules

To view all software modules currently loaded in your session:

```bash
module list
```

This is useful for troubleshooting and for documenting your computational environment.

---

## Recommendations for Use in Job Scripts

1. Begin job scripts with `module purge` to ensure a clean environment.
2. Load only the required modules for the task at hand.
3. Document loaded modules as part of your reproducibility best practices.

---

## Additional Information

For a comprehensive list of software packages available on REPACSS, refer to the [Available Software](available-software.md) documentation.

Users working in Python environments should also consult the [Installing Packages](installing-packages.md) guide for additional configuration instructions.

For support inquiries, contact the REPACSS administration team at:

```
repacss.support@ttu.edu
```
