# Getting Started

## Prerequisites {#prerequisites}

### Account Requirements
- **Current Status (TTU Users Only)**
  - Valid TTU eRaider account
  - Active REPACSS project
  - Completed training requirements

- **Future Status (ACCESS Integration)**
  - TTU users: TTU eRaider account
  - ACCESS users: ACCESS account
  - Active project allocation
  - Completed training requirements

### System Access
- SSH client
- VPN connection (if off-campus)
- Two-factor authentication

## Initial Setup {#setup}

### Account Activation
1. Submit account request
   - TTU users: Submit through TTU portal
   - ACCESS users: Coming soon through ACCESS portal
2. Complete training
3. Accept usage policy
4. Set up 2FA

### First Login
```bash
# TTU users
ssh username@repacss.ttu.edu

# ACCESS users (Coming soon)
ssh username@
```

### Environment Setup
```bash
module load 
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
sbatch  # Submit job
squeue  # Check status
scancel # Cancel job
```

## Next Steps {#next}

- [System Overview](system-overview.md)
- [Running Jobs](running-jobs.md)
- [File Management](file-management.md)
- [Software](software.md)

## Related Resources

- [Training](../support&resources/training.md)
- [Support](../support&resources/support.md)
- [FAQ](../support&resources/faq.md) 