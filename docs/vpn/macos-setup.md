# 🍎 VPN Setup Guide for macOS

## Overview

This guide walks you through installing and configuring the **GlobalProtect VPN** on macOS to access REPACSS. A VPN connection is required for all users, whether on- or off-campus.

---

## ✅ Prerequisites

- Active **eRaider account**
- **Administrator privileges** on your Mac
- **Microsoft MFA** enabled
- Stable internet connection
- At least **100MB** free disk space

---

## 📝 Step 1: Request VPN Access

1. Visit the [VPN request form](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8)
2. Select **Enable** under “Type of Assistance”
3. For the reason, enter:  
   `"Need TTUnet VPN to access REPACSS"`
4. Make sure you’ve set up [Microsoft MFA](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)

---

## 💾 Step 2: Download & Install

1. Download the installer from the [eRaider Software Portal](https://software.ttu.edu/)  
   ![Download Package](images/mac/pkg.png)

2. Open the `.pkg` file from your Downloads folder
3. Click **Continue**  
   ![Install Start](images/mac/install.png)

4. Choose a destination disk  
   ![Select Destination](images/mac/install-10.png)

5. Select the “GlobalProtect” component  
   ![Select Component](images/mac/install-1.png)

6. Click **Install**  
   ![Install Button](images/mac/install-2.png)

7. Authenticate with Touch ID or your Mac password  
   ![Authentication](images/mac/install-3.png)

8. If prompted, allow access to your Downloads folder  
   ![Allow Access](images/mac/install-5.png)

9. Click **Close** after installation completes  
   ![Install Complete](images/mac/install-6.png)

10. Choose whether to move the installer to trash  
   ![Cleanup](images/mac/install-7.png)

11. Configure notifications as needed  
   ![Notifications](images/mac/install-8.png)

---

## 🔌 Step 3: Connect to VPN

### Launch GlobalProtect
1. Click the GlobalProtect icon in your **menu bar**  
   ![Menu Bar Icon](images/mac/connect.png)

2. In the **Portal** field, type:
   ```
   vpn.ttu.edu
   ```
3. Click **Connect**  
   ![Connect Dialog](images/mac/connect-1.png)

### Authenticate
1. Wait while GlobalProtect retrieves the configuration  
   ![Configuration](images/mac/connect-2.png)

2. Your default browser will open for sign-in  
   ![Browser Sign-in](images/mac/connect-3.png)

3. If not, open the browser manually
4. Sign in using your **eRaider credentials**
5. Click **"Open GlobalProtect.app"** when prompted  
   ![Open App](images/mac/connect-4.png)

6. If prompted for **PanGPS**, enter your Mac password  
   ![PanGPS](images/mac/connect-5.png)

---

## ✅ Verify Connection

- Wait for the connection to complete
- The menu bar icon will change to show an **active VPN connection**  
   ![Connected](images/mac/connect-6.png)

---

## ❎ Disconnect from VPN

1. Click the GlobalProtect icon  
   ![Menu Bar Icon](images/mac/disconnect.png)

2. Click **Disconnect**  
   ![Disconnect Button](images/mac/disconnect-1.png)

3. Wait while the connection terminates  
   ![Disconnecting](images/mac/disconnect-2.png)

---

## ⚠️ Important Notes

> **VPN is mandatory for accessing REPACSS**

- Use only the portal: `vpn.ttu.edu`
- Keep GlobalProtect updated
- Allow GlobalProtect in **System Preferences → Security & Privacy**
- VPN is for **TTU network access only**, not general web browsing

---

## 🧰 Troubleshooting

### 🔧 Installation Fails
- Run installer as admin
- Allow apps from identified developers
- Review **System Preferences → Security & Privacy**
- Clear temporary files
- Re-download if needed

### 🌐 Connection Issues
- Check MFA and credentials
- Verify correct portal
- Restart GlobalProtect
- Check firewall and network settings

### 🔑 Authentication Problems
- Double-check eRaider username/password
- Clear cookies and browser cache
- Ensure GlobalProtect is allowed in macOS settings

### 🐢 Performance Issues
- Free up system memory
- Test your network speed
- Reboot your Mac

---

## 🔗 Related Resources

- [Main VPN Setup Guide](vpn-setup.md)
- [Getting Started](../getting-started.md)

---

## 🚀 Next Steps

1. Verify your VPN connection
2. Visit [Getting Started](../getting-started.md)
3. Learn how to [Submit Jobs](../running-jobs.md)

---

_Last updated: June, 2025_
