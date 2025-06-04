# File Management

## File Systems

Global file space on REPACSS is available on all compute, gpu, and login nodes. It is organized into the file systems shown in the table below. Access to the allocated file space is through the indicated directories that are setup automatically for every user.

| File System | Directory                | Environment Variable |
| ----------- | ------------------------ | -------------------- | 
| Home        | /mnt/GROUPID/home/USERID             | $HOME    |
| Work        | /mnt/GROUPID/work/USERID             | $WORK    |
| Scratch     | /mnt/GROUPID/scratch/USERID          | $SCRATCH |

## Checking Quotas
REPACSS storage space usage is currently organized by the REPACSS group. 
Use the following command to display your current file usage:

```bash
$ df -h /mnt/$(id -gn)

Filesystem              Size  Used Avail Use% Mounted on
10.102.95.220:/REPACSS  9.1T  162G  9.0T   2% /mnt/REPACSS
```

## File Transfer

> **Note:** Please refrain from using scp, sftp, rsync, or direct connections to the login nodes to transfer data. These methods can impact login node performance and are generally slower than Globus Connect.

### Using Globus Connect

REPACSS provides Globus Connect for efficient data transfer. Benefits include:
- High-speed, reliable transfers
- Automatic error detection and retry
- Multiple transfer streams
- No impact on login nodes
- Easy-to-use web interface

#### Setting Up Globus Connect

1. Install Globus Connect Personal on your computer:
   - [Windows Installation Guide](https://docs.globus.org/globus-connect-personal-windows-installation-guide/)
   - [Mac OS X Installation Guide](https://docs.globus.org/globus-connect-personal-mac-installation-guide/)
   - [Linux Installation Guide](https://docs.globus.org/globus-connect-personal-linux-installation-guide/)

2. Create a Globus Connect collection on your computer

3. Access REPACSS data:
   - Set endpoint to "REPACSS"
   - Navigate to your storage areas:
     - Home: `/home/USERID`
     - Scratch: `/scratch/USERID`
     - Work: `/work/USERID`

#### Transferring Between Sites

Many research organizations have Globus Connect endpoints. To transfer data:
1. Identify the remote site's Globus endpoint
2. Use the Globus web interface to transfer between endpoints
3. Set source/destination endpoints:
   - REPACSS: "REPACSS"
   - Remote site: Their endpoint name

Quesions? submit to repacss.globus@ttu.edu
## Best Practices

### Storage Management
- Keep home directory clean
- Use scratch for active computations
- Archive important data
- Monitor quotas regularly

### File Transfer
- Use Globus for large transfers
- Verify transfer completion
- Check file integrity
- Clean up temporary files

## Related Resources
- [Getting Started](getting-started.md)
- [Running Jobs](running-jobs.md)
- [Software](software.md)
- [Support](../support&resources/support.md) 
