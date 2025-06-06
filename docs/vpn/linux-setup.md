# 🐧 VPN Setup Guide for Linux

## Overview

This guide provides detailed instructions for setting up and using the GlobalProtect VPN on **Linux** systems to access REPACSS resources. VPN is **mandatory** for all users, on- or off-campus.

---

## ✅ Prerequisites

- Valid **eRaider account**
- **Ubuntu 20.04+** or similar supported distro
- **Sudo/root** access
- **Microsoft MFA** configured
- Internet connection
- At least **100MB** free disk space

### Required packages (Ubuntu):
```bash
sudo apt-get update
sudo apt-get install libc6 libstdc++6 libpam0g libx11-6 libxcb1 \
libxcomposite1 libxcursor1 libxdamage1 libxext6 libxfixes3 libxi6 \
libxrandr2 libxrender1 libxtst6 libnss3 libgtk-3-0
```

---

## 📝 Step 1: Request VPN Access

1. Fill out the [VPN Request Form](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8)
2. Under **Type of Assistance**, select `Enable`
3. For the reason, enter:  
   `"Need TTUnet VPN to access REPACSS"`
4. Set up [Microsoft MFA](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)

---

## 💾 Step 2: Download & Install

1. Visit the [TTU Software Center](https://software.ttu.edu/global-protect)
2. Log in with your eRaider credentials
3. Download the GlobalProtect **Linux** installer

### 🐧 Debian/Ubuntu:
```bash
sudo dpkg -i GlobalProtect_<version>_amd64.deb
```

### 🎩 RHEL/CentOS:
```bash
sudo rpm -i GlobalProtect_<version>_x86_64.rpm
```

---

## 🔧 Step 3: Connect to VPN

1. Launch the UI:
   ```bash
   globalprotect launch-ui
   ```

2. In the portal field, enter:
   ```
   vpn.ttu.edu
   ```

3. Click **Connect**

4. Sign in with your **eRaider** credentials and complete MFA

---

## ✅ Verify Connection

Check your VPN status:
```bash
globalprotect show --status
```

Expected output should include:
```
Status: Connected
```

---

## ❗ Important Notes

> **VPN is mandatory** for all REPACSS access.

- Use **vpn.ttu.edu** only
- Allow GlobalProtect through firewalls
- Keep the GlobalProtect client up to date
- VPN is **not** for general internet browsing

---

## 🧰 Troubleshooting

### 🔧 Installation Fails
- Check missing dependencies
- Ensure system compatibility (64-bit)
- Clear cached packages
- Re-download installer

### 🌐 Connection Issues
- Check logs:
  ```bash
  journalctl -u globalprotect
  ```
- Ensure MFA is configured
- Restart GlobalProtect:
  ```bash
  globalprotect disconnect
  globalprotect connect
  ```

### 🔑 Authentication Problems
- Double-check credentials
- Try a private browser session
- Clear cookies and cache

### 🐢 Performance Issues
- Restart networking
- Kill other VPN processes
- Test connection speed

---

## ❌ Uninstallation

### Debian/Ubuntu:
```bash
sudo dpkg -r globalprotect
```

### RHEL/CentOS:
```bash
sudo rpm -e globalprotect
```

---

## 🔗 Related Resources

- [Main VPN Setup Guide](vpn-setup.md)
- [Getting Started](../getting-started.md)

---

## 🚀 Next Steps

1. Verify you're connected to the VPN
2. Proceed to [Getting Started](../getting-started.md)
3. Learn how to [Run Jobs](../running-jobs.md)

---

_Last updated: June, 2025_
