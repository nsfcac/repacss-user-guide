# Frequently Asked Questions

## Account & Access {#account}

### How do I get an account?
- Submit request at repacss.org
- Complete training
- Accept usage policy
- Wait for approval

### How do I reset my password?


## Jobs & Computing {#jobs}

### How do I submit a job?
```bash
sbatch job.sh
sbatch -p zen4 job.sh
sbatch -p h100 job.sh
```

### How do I check job status?
```bash
squeue -u $USER
squeue -p zen4
squeue -p h100
```

### How do I cancel a job?
```bash
scancel <job_id>
scancel -u $USER
scancel -p zen4
```

## Storage & Files {#storage}

### What are the storage quotas?
- Home: 100GB per user
- Scratch: 1TB per project
- Archive: Custom allocation

### How do I transfer files?
```bash
# From local to REPACSS
scp file username@login.repacss.org:destination

# From REPACSS to local
scp username@login.repacss.org:file destination
```

## Software & Environment {#software}

### How do I load software?
```bash
module avail
module load <module-name>
module list
```

### How do I request new software?
- Submit request to support
- Provide documentation
- Specify requirements
- Wait for approval

## Related Resources

- [Support](support.md)
- [Training](training.md)
- [System Status](system-status.md)
- [Contact](contact.md) 