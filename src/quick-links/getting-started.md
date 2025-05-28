# Getting Started

## Prerequisites {#prerequisites}

### Account Requirements
- **Current Status (TTU Test Users Only)**
  - Valid TTU eRaider account
  - GlobalProtect VPN access

- **Future Status (ACCESS Integration)**
  - TTU users: TTU eRaider account
  - ACCESS users: ACCESS account
  - Active project allocation
  - Completed training requirements

### System Requirements
- SSH client (e.g., MobaXterm for Windows, Terminal for Mac/Linux)
- GlobalProtect VPN client
- Two-factor authentication (2FA) setup
- Basic knowledge of Linux command line

## Initial Setup {#setup}

### Request Access
1. Ensure you have a valid TTU eRaider account
2. Install and configure [GlobalProtect VPN](https://software.ttu.edu/global-protect)
3. Set up two-factor authentication
4. Contact system administrators for access approval

### Connect to REPACSS
> <span style="color: red">**Important**: All users must connect through GlobalProtect VPN, regardless of location (on-campus or off-campus)</span>

#### Windows Users
1. Download and install [MobaXterm](https://mobaxterm.mobatek.net)
2. Open MobaXterm and create a new SSH session
3. Enter the following connection details:
   ```
   Host: repacss.ttu.edu
   Username: your_eRaider_username
   ```

#### Mac/Linux Users
1. Open Terminal
2. Type in the following, substituting your own eRaider ID where "<eraider>" is shown:
   ```bash
   ssh username@repacss.ttu.edu
   ```

You will be prompted for your eraider password, type it in then press enter. Once you have successfully entered your eraider password, the system will respond back with:
   
 ```
***************************************************************
            Welcome to the REPACSS HPC Cluster

           ▗▄▄▖ ▗▄▄▄▖▗▄▄▖  ▗▄▖  ▗▄▄▖ ▗▄▄▖ ▗▄▄▖
           ▐▌ ▐▌▐▌   ▐▌ ▐▌▐▌ ▐▌▐▌   ▐▌   ▐▌
           ▐▛▀▚▖▐▛▀▀▘▐▛▀▘ ▐▛▀▜▌▐▌    ▝▀▚▖ ▝▀▚▖
           ▐▌ ▐▌▐▙▄▄▖▐▌   ▐▌ ▐▌▝▚▄▄▖▗▄▄▞▘▗▄▄▞▘
 ```
### Environment Setup
```bash
# Load required modules
module load <module_name>

# Set up your environment
source ~/.bashrc

# For Python users, set up Miniforge (see Python Environment Setup guide)
```

## Basic Commands {#commands}

### Navigation
```bash
pwd     # Current directory
ls      # List files
cd      # Change directory
```

### File Operations
```bash
cp      # Copy files
mv      # Move files
rm      # Remove files
mkdir   # Create directory
```

### Job Management
```bash
sbatch script.sh      # Submit a job
squeue -u username    # Check your job status
scancel job_id        # Cancel a job
sinfo                 # Check cluster status
```

## Next Steps {#next}

1. Review the [System Overview](system-overview.md) to understand REPACSS architecture
2. Learn about [Running Jobs](running-jobs.md) for computational tasks
3. Master [File Management](file-management.md) for efficient data handling
4. Explore available [Software](software.md) and tools
5. Set up your [Python Environment](python.md) if needed

## Related Resources

- [Training](../support&resources/training.md) - Learn about available training programs
- [Support](../support&resources/support.md) - Get help and support
- [FAQ](../support&resources/faq.md) - Find answers to common questions
- [Documentation](../documentation.md) - Access detailed documentation
- [Python Environment Setup](python.md) - Set up Python environments with Miniforge 