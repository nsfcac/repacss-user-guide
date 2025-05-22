# File Management

## File Systems

Global file space on REPACSS is available on all compute and login nodes. It is organized into the file systems shown in the table below. Access to the allocated file space is through the indicated directories that are setup automatically for every user.

| File System | Directory                | Environment Variable | Storage Hardware | File Space Quota | File Counts Quota | Comments                                                                                                                                                                                                                                                                   |
| ----------- | ------------------------ | -------------------- | ---------------- | ---------------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Home        | /home/USERID             | $HOME                | NVMe             | 100 GB           | 10000             | Upon login, you will be situated in **/home/$USER**. The use of this area is for small-to-modest amounts of processing: small software, scripts, compiling, editing. Its space and file count limits are not extensible.                                                   |
| Scratch     | /scratch/USERID     | $SCRATCH             | NVMe             | 1 TB             | 250000            | This is high performance storage intended to temporarily hold larger files and is for on-going processing that uses them. **It is NOT backed up nor is it intended as long-term storage.** Please delete or move out of these area any files that are not frequently used. |
| Work     | /work/USERID | $Work             | NVMe             | 5 TB             | 500000            |                      |

## Checking Quotas
ref: https://www.nccs.nasa.gov/nccs-users/instructional/using-discover/file-system-storage/show-quota
Use the `showquota` command to display your current file usage:

```bash
$ showquota

Your current disk quotas are:
Disk                  Disk Usage      Limit   File Usage      Limit
/home/username              1.4G     100.0G         3661      10000
/scratch/user/username    117.6G       1.0T        24226     250000
/scratch/group/projectid  510.5G       5.0T       128523     500000
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
     - Project: `/work/USERID`

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