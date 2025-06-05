# VPN Setup Guide for macOS

## Overview {#overview}
This guide provides detailed instructions for setting up and using the GlobalProtect VPN on macOS systems to access REPACSS resources. The VPN connection is required for all users, regardless of whether they are on-campus or off-campus.

## Prerequisites {#prerequisites}
- Valid TTU eRaider account
- Administrator privileges on your Mac
- Microsoft Multi-Factor Authentication (MFA) configured
- Internet connection
- At least 100MB of free disk space

## Installation Steps {#installation}

### 1. Request VPN Access {#request-access}
1. Complete the [VPN request form](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8)
2. Under **Type of Assistance**, select **Enable**
3. For the reason, enter: "Need TTUnet VPN to access REPACSS"
4. Ensure you have configured [Microsoft Multi-Factor Authentication (MFA)](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)

### 2. Download and Install {#download-install}
1. Download the GlobalProtect installation package from the [eRaider Software Downloads page](https://software.ttu.edu/)<br>
![Download Package](images/mac/pkg.png)<br>

2. Locate and open the downloaded file (typically in Downloads folder)
3. Click Continue to begin the installation process<br>
![Install Start](images/mac/install.png)<br>

4. Select the installation destination disk<br>
![Select Destination](images/mac/install-10.png)<br>

5. Select the checkbox labeled "GlobalProtect"<br>
![Select Component](images/mac/install-1.png)<br>

6. Click Install to proceed<br>
![Install Button](images/mac/install-2.png)<br>

7. When prompted, use Touch ID or enter administrator credentials<br>
![Authentication](images/mac/install-3.png)<br>
![Authentication Dialog](images/mac/install-4.png)<br>

8. Allow Installer access to your Downloads folder if prompted<br>
![Allow Access](images/mac/install-5.png)<br>

9. Click Close when installation is complete<br>
![Install Complete](images/mac/install-6.png)<br>

10. Choose whether to keep or move the installation package to trash<br>
![Cleanup](images/mac/install-7.png)<br>

11. Configure notification preferences when prompted<br>
![Notifications](images/mac/install-8.png)<br>
![Background Item](images/mac/install-9.png)<br>

## Connecting to VPN {#connecting}

### 1. Launch GlobalProtect {#launch}
1. Click the GlobalProtect icon in your Mac's menu bar<br>
![Menu Bar Icon](images/mac/connect.png)<br>

2. In the Portal field, enter: `vpn.ttu.edu`
3. Click Connect<br>
![Connect Dialog](images/mac/connect-1.png)<br>

### 2. Authentication {#authentication}
1. Wait while GlobalProtect retrieves the configuration<br>
![Configuration](images/mac/connect-2.png)<br>

2. Your default browser will open automatically for sign-in<br>
![Browser Sign-in](images/mac/connect-3.png)<br>

3. If browser doesn't open automatically, launch it manually
4. Sign in with your eRaider credentials
5. Click "Open GlobalProtect.app" when prompted<br>
![Open App](images/mac/connect-4.png)<br>

6. If prompted regarding PanGPS, enter administrator credentials<br>
![PanGPS](images/mac/connect-5.png)<br>

### 3. Verify Connection {#verify}
1. Wait while the VPN connection is established
2. The GlobalProtect icon will indicate an active connection<br>
![Connected](images/mac/connect-6.png)<br>

## Disconnecting from VPN {#disconnecting}

### 1. Disconnect {#disconnect}
1. Click the GlobalProtect icon in the menu bar<br>
![Menu Bar Icon](images/mac/disconnect.png)<br>

2. Click Disconnect<br>
![Disconnect Button](images/mac/disconnect-1.png)<br>

3. Wait while the VPN connection is terminated<br>
![Disconnecting](images/mac/disconnect-2.png)<br>

## Important Notes {#notes}
> <span style="color: red">**Important**: VPN connection is mandatory for all REPACSS access</span>

- Keep your GlobalProtect client updated
- Use the official TTU VPN portal only
- Allow GlobalProtect in System Preferences > Security & Privacy if prompted
- The TTUnet VPN service provides a secure connection to the Texas Tech University (TTU) network only
- It is not designed for general-purpose internet encryption

## Troubleshooting {#troubleshooting}
### Common Issues
1. **Installation Fails**
   - Ensure you have administrator privileges
   - Check System Preferences > Security & Privacy
   - Allow installation from identified developers
   - Clear temporary files
   - Try downloading the installer again

2. **Connection Issues**
   - Verify MFA is properly configured
   - Check network settings
   - Ensure correct portal address (vpn.ttu.edu)
   - Restart GlobalProtect
   - Check System Preferences > Security & Privacy settings

3. **Authentication Problems**
   - Verify eRaider credentials
   - Check MFA status
   - Clear browser cache and cookies
   - Check System Preferences > Security & Privacy settings

4. **Performance Issues**
   - Check system resources
   - Verify network speed
   - Close unnecessary applications
   - Restart your Mac if problems persist


## Related Resources {#resources}
- [Main VPN Setup Guide](vpn-setup.md)
- [Getting Started Guide](../getting-started.md)

## Next Steps {#next}
1. Verify VPN connection
2. Proceed to [Getting Started](../getting-started.md)
3. Learn about [Running Jobs](../running-jobs.md)

---

*Last updated: June 5, 2025* 