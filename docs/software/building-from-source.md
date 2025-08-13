# Building Software from Source

This guide covers compiling and installing **user-installed** software from source code on REPACSS when pre-built packages are not available or don't meet your requirements.

## 🎯 When to Build from Source

Build from source when you need:

- **Custom configurations** not available in pre-built packages
- **Latest versions** of software not yet packaged
- **Patches or modifications** to existing software
- **Optimizations** for specific hardware or use cases
- **Software not available** through other package managers

---

## 🔧 Prerequisites

### Load Required Modules

Before building software, load the necessary compiler and library modules:

```bash
# Load compiler
module load gcc/14.2.0

# Load MPI (if needed)
module load openmpi/5.0.4

# Load other dependencies
module load hdf5/1.14.5
module load netcdf-c/4.9.2
```

### Check Available Modules

```bash
# List available modules
module avail

# Show module details
module show gcc/14.2.0
```

---

## 🏗️ Basic Build Process

### 1. Download and Extract Source

```bash
# Download source code
wget https://example.com/software-1.0.tar.gz

# Extract source
tar -xzf software-1.0.tar.gz
cd software-1.0
```

### 2. Configure the Build

```bash
# Basic configuration
./configure --prefix=$HOME/software/myapp

# With specific options
./configure \
    --prefix=$HOME/software/myapp \
    --enable-shared \
    --with-mpi \
    --with-hdf5=$HDF5_ROOT
```

### 3. Compile and Install

```bash
# Compile (use multiple cores for speed)
make -j$(nproc)

# Install
make install
```

### 4. Set Up Environment

Add the installation to your environment:

```bash
# Add to PATH
export PATH="$HOME/software/myapp/bin:$PATH"

# Add to library path
export LD_LIBRARY_PATH="$HOME/software/myapp/lib:$LD_LIBRARY_PATH"

# Add to pkg-config path
export PKG_CONFIG_PATH="$HOME/software/myapp/lib/pkgconfig:$PKG_CONFIG_PATH"
```

Add these lines to your `~/.bashrc` for persistence.

---

## 🔍 Common Build Systems

### Autotools (./configure)

```bash
# Basic autotools build
./configure --prefix=$HOME/software/myapp
make -j$(nproc)
make install
```

### CMake

```bash
# Create build directory
mkdir build && cd build

# Configure with CMake
cmake .. \
    -DCMAKE_INSTALL_PREFIX=$HOME/software/myapp \
    -DCMAKE_BUILD_TYPE=Release

# Build and install
make -j$(nproc)
make install
```

### Make

```bash
# Edit Makefile or use make variables
make PREFIX=$HOME/software/myapp
make PREFIX=$HOME/software/myapp install
```

### Python Setup

```bash
# Install Python package from source
python setup.py install --user

# Or with pip
pip install --user .
```

---

## 📦 Building with Dependencies

### Example: Building with MPI

```bash
# Load MPI module
module load openmpi/5.0.4

# Configure with MPI support
./configure \
    --prefix=$HOME/software/myapp \
    --with-mpi \
    CC=mpicc \
    CXX=mpicxx \
    FC=mpif90

make -j$(nproc)
make install
```

### Example: Building with HDF5

```bash
# Load HDF5 module
module load hdf5/1.14.5

# Configure with HDF5
./configure \
    --prefix=$HOME/software/myapp \
    --with-hdf5=$HDF5_ROOT \
    CPPFLAGS="-I$HDF5_ROOT/include" \
    LDFLAGS="-L$HDF5_ROOT/lib"

make -j$(nproc)
make install
```

---

## 🎯 Best Practices

### Directory Organization

```bash
# Create organized directory structure
mkdir -p $HOME/software/{bin,lib,include,share}
mkdir -p $HOME/software/myapp/{bin,lib,include,share}

# Use descriptive names
mkdir -p $HOME/software/myapp-v1.0
```

### Version Management

```bash
# Keep multiple versions
$HOME/software/myapp-v1.0/
$HOME/software/myapp-v1.1/
$HOME/software/myapp -> myapp-v1.1/  # symlink to current version
```

### Environment Setup

Create a module-like environment script:

```bash
# Create setup script
cat > $HOME/software/myapp/setup.sh << EOF
#!/bin/bash
export PATH="$HOME/software/myapp/bin:\$PATH"
export LD_LIBRARY_PATH="$HOME/software/myapp/lib:\$LD_LIBRARY_PATH"
export PKG_CONFIG_PATH="$HOME/software/myapp/lib/pkgconfig:\$PKG_CONFIG_PATH"
EOF

# Source when needed
source $HOME/software/myapp/setup.sh
```

---

## 🚀 Building in Jobs

### Interactive Build Session

```bash
# Request interactive session for building
interactive -p zen4 -c 8 -m 16G

# Load modules and build
module load gcc/14.2.0
cd $HOME/software-src/myapp
./configure --prefix=$HOME/software/myapp
make -j8
make install
```

### Batch Build Job

```bash
#!/bin/bash
#SBATCH --job-name=build-myapp
#SBATCH --partition=zen4
#SBATCH --cpus-per-task=8
#SBATCH --mem=16G
#SBATCH --time=02:00:00
#SBATCH --output=build_%j.out
#SBATCH --error=build_%j.err

# Load required modules
module load gcc/14.2.0
module load openmpi/5.0.4

# Build software
cd $HOME/software-src/myapp
./configure --prefix=$HOME/software/myapp
make -j8
make install
```

---

## 🛠️ Troubleshooting

### Common Issues

1. **Missing dependencies**: Install required libraries
   ```bash
   # Check what's missing
   ./configure 2>&1 | grep "not found"
   
   # Load missing modules
   module load missing-library
   ```

2. **Compiler errors**: Check compiler and flags
   ```bash
   # Use specific compiler
   CC=gcc CXX=g++ ./configure --prefix=$HOME/software/myapp
   ```

3. **Permission errors**: Check directory permissions
   ```bash
   # Ensure write permissions
   chmod -R u+w $HOME/software/myapp
   ```

4. **Library path issues**: Set correct paths
   ```bash
   # Add library paths
   export LD_LIBRARY_PATH="$HOME/software/myapp/lib:$LD_LIBRARY_PATH"
   ```

### Debugging Builds

```bash
# Verbose output
make VERBOSE=1

# Check configuration
./config.log

# Test installation
make check
make test
```

---

## 📚 Related Documentation

- [Software Management Overview](index.md) - General software management
- [Module System](module-system.md) - System software via modules
- [Using Containers](containers.md) - Alternative to source builds
- [Getting Started with MiniForge](miniforge.md) - Python package management with conda

---

## 🆘 Support

For build-related issues or assistance, contact:

```
repacss.support@ttu.edu
```
