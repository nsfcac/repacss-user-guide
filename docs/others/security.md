# 🔐 Security Policy

This guide outlines the security practices and requirements for using REPACSS resources responsibly and safely. All users must adhere to these policies to ensure system integrity, data protection, and compliance.

---

## 👤 Account Security <a id="account"></a>

### 🔑 Password Policy

To protect user accounts and sensitive information, all users must follow these rules:

- **Minimum Length**: Passwords must be at least **8 characters**.
- **Character Complexity**: Include a mix of **uppercase, lowercase, numbers, and special characters** (e.g., @, #, $, %).
- **Regular Updates**: Change your password **periodically** to reduce long-term risk.
- **No Reuse**: Avoid reusing previous passwords.

> Passwords should be unique, confidential, and stored securely using a trusted password manager.

---

### 🔒 Two-Factor Authentication (2FA)

- **Mandatory for all users**
- Use a **mobile authenticator app** (e.g., Microsoft Authenticator, Google Authenticator)
- Save **backup codes** securely in case of device loss
- **Immediately report lost/stolen devices** to IT Help Central

---

## 🗂️ Data Security <a id="data"></a>

### 🔖 Data Classification

Understand the sensitivity of your data:

| Classification | Description                       |
|----------------|-----------------------------------|
| **Public**     | Freely shareable, non-sensitive   |
| **Internal**   | Internal use only, not public     |
| **Confidential** | Sensitive, restricted to projects |
| **Restricted** | Highly sensitive, access-controlled |

---

### 📦 Data Handling Guidelines

- Use designated **secure storage areas** (`/home`, `/scratch`, `/project`)
- Follow REPACSS **retention and archival policies**
- **Encrypt** confidential or restricted data in transit and at rest
- Promptly **report any data incidents** to the security team

---

## 🖥️ System Security <a id="system"></a>

### 🚪 Access Control

- **Use SSH Keys**: Password login is discouraged; generate a secure key pair and protect your private key.
- **Restrict Permissions**: Set strict file permissions using `chmod` and `chown` to limit unauthorized access.
- **Least Privilege Principle**: Only grant the minimum permissions required to perform a task.
- **Report Suspicious Activity**: Notify admins of any unauthorized access attempts or unusual behavior.

---

### 🧰 Security Best Practices

- **Keep Software Updated**: Regularly patch and update your tools and environments.
- **Use Encrypted Connections**: Always prefer **SSH, HTTPS, and SFTP** over unencrypted protocols.
- **Monitor Your Jobs and Files**: Watch for unexpected activity or performance issues.
- **Report Vulnerabilities**: If you notice a system vulnerability, report it to `repacss.support@ttu.edu`.

---

## 📜 Compliance <a id="compliance"></a>

### 🔖 Policies to Follow

- **Acceptable Use Policy**
- **Data Protection Policy**
- **Incident Response Policy**
- **Privacy and Confidentiality Policy**

### ✅ User Responsibilities

- Complete any **required training**
