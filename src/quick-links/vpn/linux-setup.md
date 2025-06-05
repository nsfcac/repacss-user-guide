# VPN Setup Guide for Linux

## Overview {#overview}
This guide provides detailed instructions for setting up and using the GlobalProtect VPN on Linux systems to access REPACSS resources. The VPN connection is required for all users, regardless of whether they are on-campus or off-campus.

## Prerequisites {#prerequisites}
- Valid TTU eRaider account
- Ubuntu 20.04 LTS or later
- Administrator (sudo) access to your system
- Microsoft Multi-Factor Authentication (MFA) configured
- Internet connection
- At least 100MB of free disk space
- Required packages:
  ```bash
  sudo apt-get update
  sudo apt-get install libc6 libstdc++6 libpam0g libx11-6 libxcb1 libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 libxrandr2 libxrender1 libxtst6 libnss3 libgtk-3-0
  ```

## Installation Steps {#installation}

### 1. Request VPN Access {#request-access}
1. Complete the [VPN request form](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8)
2. Under **Type of Assistance**, select **Enable**
3. For the reason, enter: "Need TTUnet VPN to access REPACSS"
4. Ensure you have configured [Microsoft Multi-Factor Authentication (MFA)](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)

### 2. Download and Install {#download-install}
1. Visit [TTU Software Center](https://software.ttu.edu/global-protect)<br>
![Download Package](images/linux/download.png)<br>

2. Log in with your eRaider credentials
3. Download the Linux version of GlobalProtect

#### Debian/Ubuntu-based Systems
```bash
# Install dependencies
sudo apt-get update
sudo apt-get install libc6 libstdc++6 libpam0g

# Install GlobalProtect
sudo dpkg -i GlobalProtect_<version>_amd64.deb
```

#### RHEL/CentOS-based Systems
```bash
# Install dependencies
sudo yum update
sudo yum install glibc libstdc++ pam

# Install GlobalProtect
sudo rpm -i GlobalProtect_<version>_x86_64.rpm
```

### 3. Configure {#configure}
1. Launch GlobalProtect from the terminal:
   ```bash
   globalprotect launch-ui
   ```
2. Enter the portal address: `vpn.ttu.edu`
3. Click "Connect"
4. Enter your eRaider credentials when prompted
5. Complete two-factor authentication if required

### 4. Verify Connection {#verify}
1. Check connection status in the terminal:
   ```bash
   globalprotect show --status
   ```
2. Look for "Connected" status
3. Verify network connectivity

## Important Notes {#notes}
> <span style="color: red">**Important**: VPN connection is mandatory for all REPACSS access</span>

- Keep your GlobalProtect client updated
- Use the official TTU VPN portal only
- Allow GlobalProtect through your firewall if prompted
- The TTUnet VPN service provides a secure connection to the Texas Tech University (TTU) network only
- It is not designed for general-purpose internet encryption

## Troubleshooting {#troubleshooting}
### Common Issues
1. **Installation Fails**
   - Check system dependencies
   - Verify package manager repositories
   - Check system architecture compatibility
   - Clear package manager cache
   - Try downloading the installer again

2. **Connection Issues**
   - Check system logs: `journalctl -u globalprotect`
   - Verify network configuration
   - Check firewall settings
   - Verify MFA is properly configured
   - Check network manager configuration

3. **Authentication Problems**
   - Verify eRaider credentials
   - Check MFA status
   - Clear browser cache and cookies
   - Check system authentication logs

4. **Performance Issues**
   - Update system packages
   - Check for conflicting VPN software
   - Clear GlobalProtect cache
   - Check system resources
   - Verify network speed

## Uninstallation {#uninstall}
#### Debian/Ubuntu-based Systems
```bash
sudo dpkg -r globalprotect
```

#### RHEL/CentOS-based Systems
```bash
sudo rpm -e globalprotect
```

## Related Resources {#resources}
- [Main VPN Setup Guide](vpn-setup.md)
- [Getting Started Guide](../getting-started.md)

## Next Steps {#next}
1. Verify VPN connection
2. Proceed to [Getting Started](../getting-started.md)
3. Learn about [Running Jobs](../running-jobs.md)

---

*Last updated: June 5, 2025* 