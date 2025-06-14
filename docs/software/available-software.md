# Available Software on REPACSS

This document provides a formal summary of software environments currently available on the REPACSS high-performance computing system. Software is managed and accessed using the **environment module framework**, which allows users to dynamically configure their shell environments to access compilers, libraries, and applications relevant to their research or instructional activities.

---

## Software Module Locations

Software modules are organized within predefined repository paths. The following modules are currently available for loading and execution:

### `/opt/apps/nfs/modules/zen4/rocky9.4/openmpi/4.1.6-vhun5qt/Core`

- `fftw/3.3.10`  
  *Fast Fourier Transform library used in signal and image processing applications.*
sss
- `hdf5/1.10.11`  
  *Hierarchical Data Format library for managing large and complex data collections.*

### `/opt/apps/nfs/modules/zen4/rocky9.4/Core`

- `gcc/14.2.0`   
  *GNU Compiler Collection supporting C, C++, and Fortran languages.*

- `openmpi/4.1.6`   
  *High-performance implementation of the Message Passing Interface (MPI) standard.*

!!! note 
    The `(L)` designation indicates that the module is currently loaded in the user’s active environment.

---

## Guidance for Module Usage

Users are advised to utilize the following commands for listing and managing software modules:

### Display All Available Modules

```bash
module avail
```

### Display Only Default Modules

In the case of an extensive list, users may restrict output to default modules:

```bash
module --default avail
# or
ml -d av
```

### View Module Categories and Quantities

To obtain a summary overview of available module categories and counts:

```bash
module overview
# or
ml ov
```

### Discover All Installed Modules and Extensions

To enumerate all possible software packages and extensions, regardless of default visibility:

```bash
module spider
```

---

## Loading Software Modules

To access a software environment, load the corresponding module. For example:

```bash
module load gcc/14.2.0
```

To verify currently loaded modules:

```bash
module list
```

To unload a module:

```bash
module unload <module_name>
```

---

## Additional Support and Documentation

Users seeking more detailed instructions for using the module system are encouraged to consult the [Module System User Guide](module-system.md).

If software needed for your research or coursework is not listed among available modules, you may submit a request to the REPACSS support team for consideration.

For further assistance, please contact:

```
REPACSS System Administration
repacss.support@ttu.edu
```
