# File Transfer with Globus

!!! warning "Avoid Direct Transfers via Login Nodes"
    Please refrain from using `scp`, `sftp`, `rsync`, or direct connections to the login nodes for data transfer. These methods can degrade system performance and are less efficient compared to Globus Connect.

---

## Overview

REPACSS supports high-performance data movement through **Globus Connect**, a robust tool designed to facilitate large-scale file transfers. It provides:

* High-speed, reliable transfers
* Automatic error detection and retry
* Multiple parallel streams for faster throughput
* No impact on login node performance
* User-friendly web-based interface

---

## Setting Up Globus Connect

Follow these steps to enable file transfers using Globus Connect Personal:

1. **Install Globus Connect Personal** on your local machine:

   * [Windows Installation Guide](https://docs.globus.org/how-to/globus-connect-personal-windows/)
   * [macOS Installation Guide](https://docs.globus.org/how-to/globus-connect-personal-mac/)
   * [Linux Installation Guide](https://docs.globus.org/how-to/globus-connect-personal-linux/)

2. **Create a Personal Collection**:

   * After installation, set up a Globus collection tied to your system.

3. **Access REPACSS Data**:

   * Set the endpoint to: `REPACSS`
   * Navigate to the appropriate storage paths:

     * Home: `/mnt/GROUPID/home/USERID`
     * Scratch: `/mnt/GROUPID/scratch/USERID`
     * Work: `/mnt/GROUPID/work/USERID`

---

## Transferring Data Between Sites

Many academic and research institutions have established Globus endpoints. To transfer data between REPACSS and other sites or to your own machine:

<!-- 0. Identify the remote institution’s Globus endpoint name. -->
1. Use the [Globus Web Interface](https://app.globus.org/file-manager) to configure transfers.
2. Specify the collection to be used:
   * **REPACSS Endpoint**: `REPACSS`
3. Locate and select the file(s) you intend to transfer, then click the `Transfer or Sync to...` button.
4. Select your destination collection.
5. Specify the target file path and click Start to initiate the transfer.


---

## Best Practices

<!-- * Ensure VPN access is active if required by your home network. -->
* Always verify file integrity post-transfer.
* Monitor job completion using the Globus web interface.

---

*Last updated: June 2025*
