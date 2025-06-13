# 🔐 VPN Setup Guide

## Overview

To securely access the REPACSS HPC system, all users — both on-campus and off-campus — must connect through the **GlobalProtect VPN** provided by Texas Tech University (TTU). This guide outlines how to request access, install the client, and troubleshoot issues.

---

## ✅ Prerequisites

Before proceeding, ensure the following:

- You have a **valid eRaider** account
- **Microsoft Multi-Factor Authentication (MFA)** is enabled
- You have **administrator privileges** on your computer
- You are connected to the internet

---

## 📝 Request TTU VPN Access

1. Fill out the [TTU VPN request form](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8):
   - Under **Type of Assistance**, select **Enable**
   - For the reason, write: `Need TTUnet VPN to access REPACSS`

2. Set up [Microsoft MFA](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed) if you haven't already.

---

## 💻 Installation Guides

Choose your operating system and follow the corresponding instructions:

- 🪟 [Windows Setup Guide](windows-setup.md)
- 🍎 [macOS Setup Guide](macos-setup.md)
- 🐧 [Linux Setup Guide](linux-setup.md)

---

## ⚠️ Important Notes

> All users must be connected to the TTU network to access REPACSS. This is typically achieved by using **GlobalProtect VPN** when off-campus. However, users in the Computer Science Department building may experience issues accessing REPACSS even when connected to TTUnet (the campus wireless network). For these users, it is recommended to use GlobalProtect VPN as a workaround to ensure proper access.

- Use **only** the official **TTU VPN portal**: `vpn.ttu.edu`
- Keep the GlobalProtect client **up to date**
- VPN is for **TTU resource access only**, not general internet use
- Confirm that MFA is configured and working before attempting connection

---

## 🧰 Troubleshooting

### 1. Connection Fails
- Verify your internet is working
- Check that your credentials are correct
- Make sure the portal address is `vpn.ttu.edu`
- Restart the GlobalProtect app
- Double-check that MFA is set up

### 2. Installer Issues
- Run the installer **as administrator**
- Clear temporary files or cache
- Ensure your system meets requirements
- Reboot and retry installation

### 3. Authentication Errors
- Make sure your **eRaider credentials** are up-to-date
- Re-enroll or verify **MFA status**
- Clear browser cookies/cache if using web authentication

---

## 🔗 Related Resources

- 📘 [System Overview](../system-overview.md)
- 🚀 [Getting Started](../getting-started.md)

---

## 📌 Next Steps

1. Complete the [VPN access request](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=a990ee5ddbdf41144d17266e139619f8)
2. Set up [Microsoft MFA](https://askit.ttu.edu/sp?id=sc_cat_item&sys_id=77057d80874eb5509a3a539d3fbb35ed)
3. Install GlobalProtect using your OS-specific guide
4. Confirm your connection to the TTU VPN
5. Proceed to [Getting Started](../getting-started.md) for cluster access

---

_Last updated: June 5, 2025_
