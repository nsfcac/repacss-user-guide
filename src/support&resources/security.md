# Security

## Account Security {#account}

### Password Policy
- Minimum 8 characters
- Mix of character types
- Change every 90 days
- No reuse of passwords

### Two-Factor Authentication
- Required for all users
- Use authenticator app
- Backup codes provided
- Report lost devices

## Data Security {#data}

### Data Classification
- Public data
- Internal data
- Confidential data
- Restricted data

### Data Handling
- Use appropriate storage
- Follow retention policy
- Encrypt sensitive data
- Report incidents

## System Security {#system}

### Access Control
- Use SSH Keys
Always use SSH keys instead of passwords when accessing REPACSS or other remote systems. SSH keys provide a more secure, encrypted method of authentication that is significantly harder to compromise than traditional credentials. Make sure your private key is stored securely and never shared.

- Limit File Permissions
Restrict file permissions to only those who absolutely need access. This reduces the risk of unauthorized modifications or data leaks. Use operating system-level tools (like *chmod*) to ensure sensitive files are only readable or writable by the appropriate users.

- Follow the Principle of Least Privilege
Grant users and applications the minimum level of access necessary to perform their tasks. Avoid giving more privileges unless absolutely required. This limits potential damage in case of compromised accounts or software vulnerabilities.

- Report Unauthorized Access
If you detect any suspicious behavior or unauthorized access to systems or data, report it immediately to your security team or system administrator. Timely reporting helps prevent further damage, ensures incident response teams can act quickly, and contributes to overall system integrity.

### Best Practices
- Keep Software Updated
Regularly update all software, including operating systems, applications, and security tools. Applying patches and updates ensures protection against known vulnerabilities and reduces the risk of exploitation by attackers. Enable automatic updates when possible, and establish a routine schedule for checking and applying critical fixes.

- Use Secure Connections
Always use encrypted connections, such as HTTPS, SFTP, and SSH—to protect data in transit. Avoid unsecured protocols like HTTP or FTP, especially when handling sensitive information. Ensure SSL/TLS certificates are valid and up to date for all web-facing services.

- Monitor System Activity
Continuously monitor system activity to detect unusual behavior or unauthorized access and in real time. Anomalies in system performance, login patterns, or network traffic should be reported to be investigated promptly.

- Report Vulnerabilities
If you identify a potential vulnerability, please report it immediately through the appropriate channels. Prompt reporting enables faster mitigation and reduces the window of risk.

## Compliance {#compliance}

### Policies
- Acceptable use
- Data protection
- Security incident
- Privacy policy

### Requirements
- Follow guidelines
- Complete training
- Report violations
- Maintain compliance

## Related Resources

- [Support](support.md)
- [Training](training.md)
- [FAQ](faq.md)
- [Contact](contact.md)
