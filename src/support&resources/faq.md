# Frequently Asked Questions

## Account & Access {#account}

### How Do I Get an Account?
To obtain an account, follow these steps:

- Submit a Request
Visit repacss.org and fill out the account request form. Make sure to provide all required information accurately, including your contact details, organization, and reason for requesting access.

- Complete the Required Training
After submitting your request, you’ll need to complete a mandatory training module. This ensures that all users understand the system’s functionality, guidelines, and data usage responsibilities.

- Accept the Usage Policy
Once training is complete, you’ll be asked to review and accept the system’s usage policy. This agreement outlines your responsibilities as a user, including data security and proper access protocols.

- Wait for Approval
After completing the previous steps, your application will be reviewed by the administrative team. You’ll receive a notification once your account is approved and activated.

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
