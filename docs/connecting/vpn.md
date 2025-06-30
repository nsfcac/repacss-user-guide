# VPN Setup Guide for REPACSS

This document outlines the procedure for configuring and utilizing the GlobalProtect VPN client to securely access the REPACSS high-performance computing (HPC) infrastructure at Texas Tech University (TTU).

---

## Overview

All users must establish a secure network connection via TTU’s GlobalProtect VPN to access REPACSS (`repacss.ttu.edu`). VPN access requires:

- Use of the portal address `vpn.ttu.edu`
- Authentication through a valid TTU eRaider account
- An active Microsoft Multi-Factor Authentication (MFA) configuration

This guide provides setup instructions for the following operating systems:

- Microsoft Windows
- Apple macOS
- GNU/Linux distributions

---

## Step 1: Request VPN Access

Prior to installing the VPN client, users must formally request access:

1. Navigate to the [TTU VPN Access Request Form](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8) and make sure you are signed-in to see the form.
2. Under "Type of Assistance," select: `Enable`
3. Provide the following justification:
   ```
   Need TTUnet VPN to access REPACSS TTU Cluster
   ```
4. Confirm that [Microsoft MFA](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed) is active and functional

---

## Windows Configuration

### Installation

1. Visit the [TTU Software Distribution Portal](https://software.ttu.edu/global-protect)
2. Download the appropriate `.msi` file (32-bit or 64-bit)
3. Execute the installer and follow the on-screen instructions
4. Reboot if prompted

*For more info please see [IT Help Central's official document](https://www.askit.ttu.edu/vpn).*

### VPN Connection Procedure

1. Launch the GlobalProtect application
2. Enter the portal address:
   ```
   vpn.ttu.edu
   ```
3. Authenticate using TTU eRaider credentials and approve the MFA prompt
4. Upon successful connection, status will display as **Connected**

---

## macOS Configuration

### Installation

1. Download the GlobalProtect `.pkg` installer from [TTU Software Distribution Portal](https://software.ttu.edu/global-protect)
2. Launch the installer and complete all prompts
3. Grant required permissions if prompted by the operating system

### VPN Connection Procedure

1. Open GlobalProtect from the menu bar
2. Enter the portal:
   ```
   vpn.ttu.edu
   ```
3. Authenticate using TTU eRaider credentials and Microsoft MFA
4. Confirm connection status in the application interface   

*For more info please see [IT Help Central's official document](https://www.askit.ttu.edu/vpn).*

---

## Linux Configuration

### Prerequisites (Ubuntu/Debian)

Install system dependencies:

```bash
sudo apt-get update
sudo apt-get install libc6 libstdc++6 libpam0g libx11-6 libxcb1 \
libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 \
libxrandr2 libxrender1 libxtst6 libnss3 libgtk-3-0
```

### Installation

1. Visit [TTU Software Distribution Portal](https://software.ttu.edu/global-protect)
2. Download the appropriate `.deb` or `.rpm` package

Install the package:

**Debian/Ubuntu**
```bash
sudo dpkg -i GlobalProtect_<version>_amd64.deb
```

**RHEL/CentOS**
```bash
sudo rpm -i GlobalProtect_<version>_x86_64.rpm
```

*For more info please see [IT Help Central's official document](https://www.askit.ttu.edu/vpn).*

### VPN Connection Procedure

Launch the client UI:

```bash
globalprotect launch-ui
```

1. Input portal:
   ```
   vpn.ttu.edu
   ```
2. Authenticate using your TTU eRaider credentials and MFA

Verify connection status:

```bash
globalprotect show --status
```

Expected output:
```
Status: Connected
```

---

## Disconnecting from VPN

**Windows/macOS:**  
Click the GlobalProtect icon and select **Disconnect**

**Linux:**

```bash
globalprotect disconnect
```

---

## Troubleshooting

### Authentication Issues

- Verify username and MFA credentials
- Attempt login in a private browser session
- Clear stored cookies and cached credentials

### Connection Errors

- Confirm the portal address is correct: `vpn.ttu.edu`
- Restart GlobalProtect and your device
- Ensure firewall settings permit VPN traffic

### Installation Failures

- Ensure administrative privileges are granted
- Validate that system requirements are met
- Re-download installer from official TTU source

---

## Additional Resources

- [Getting Started at REPACSS](../getting-started-at-REPACSS.md)
- [Running Jobs on REPACSS](../running-jobs/basics.md)

---

