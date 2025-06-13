# Establishing Connections

## REPACSS System Address

Before you can connect to REPACSS, ensure the following:

- ✅ You have an active TTU account
- ✅ You have configured your password and **Multi-Factor Authentication (MFA)**
- ✅ You are connected to the **TTU network**, either via campus Ethernet or **GlobalProtect VPN**

The system address used to connect is:

```
repacss.ttu.edu
```

## TTU Network & VPN Access

> ⚠️ **VPN Required Off-Campus:**  
> All users must be connected to the TTU network to access REPACSS.  
> Use **GlobalProtect VPN** when off-campus or when Wi-Fi-only in the CS Department building.

If you are on TTUnet (Wi-Fi) in the CS building and unable to access REPACSS, switch to VPN.

- 🔗 [TTU GlobalProtect VPN Setup Guide](https://www.depts.ttu.edu/itts/software/vpn.php)

---

## Connecting via SSH

### 🪟 For Windows (MobaXterm)

1. Download and install [MobaXterm](https://mobaxterm.mobatek.net).
2. Open MobaXterm and create a new SSH session:
   ```
   Remote Host: repacss.ttu.edu
   Username:   <your_eRaider_username>
   ```
3. Click OK to connect.

### 🍎 For Mac / Linux (Terminal)

Open your terminal and enter:

```bash
ssh <your_eRaider_username>@repacss.ttu.edu
```

Upon successful login, you will see:

```
***************************************************************
            Welcome to the REPACSS HPC Cluster

           ▗▄▄▖ ▗▄▄▄▖▗▄▄▖  ▗▄▖  ▗▄▄▖ ▗▄▄▖ ▗▄▄▖
           ▐▌ ▐▌▐▌   ▐▌ ▐▌▐▌ ▐▌▐▌   ▐▌   ▐▌
           ▐▛▀▚▖▐▛▀▀▘▐▛▀▘ ▐▛▀▜▌▐▌    ▝▀▚▖ ▝▀▚▖
           ▐▌ ▐▌▐▙▄▄▖▐▌   ▐▌ ▐▌▝▚▄▄▖▗▄▄▞▘▗▄▄▞▘
***************************************************************
```

---

## Troubleshooting

### "Permission Denied" or "Too Many Authentication Failures"

Possible causes:

- ❌ You mistyped your eRaider username or password.
- ❌ You're not connected to the TTU network or VPN.
- ❌ Your SSH client is trying too many keys. Add `IdentitiesOnly=yes`.

Example:

```bash
ssh -o IdentitiesOnly=yes <your_eRaider_username>@repacss.ttu.edu
```

---

### SSH Host Key Changed Warning

If you see:

```
WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!
```

Do the following:

1. Open `~/.ssh/known_hosts`
2. Remove the line associated with `repacss.ttu.edu`
3. Retry connecting and verify the new host fingerprint if prompted

---

### Still Can't Connect?

If you've verified VPN, credentials, and SSH setup but still cannot connect, contact:

- 📧 Email: [repacss-support@ttu.edu](mailto:repacss-support@ttu.edu)
- 💬 Include terminal output with `-vvv` for verbose SSH logging

---

## Coming Soon: SSH Certificate Authority

> 🚧 **Planned Feature:** We are working on adding SSH certificate authority support to streamline and secure SSH connections to REPACSS.
