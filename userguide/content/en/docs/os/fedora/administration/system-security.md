---
title: "System Security Best Practices"
description: "Securing a Fedora Linux system is essential to protect it from potential threats and unauthorized access. This tutorial will guide you through various best practices to enhance the security of your Fedora installation. It covers topics such as user authentication, file permissions, system hardening, and more."
icon: "code"
draft: false
toc: true
weight: 1
---

## 1. User Authentication

### 1.1 Strong Password Policies

Implement strong password policies to prevent brute-force attacks and unauthorized access. Here are some recommendations:

- Set a minimum password length (e.g., 12 characters)
- Require a combination of uppercase, lowercase, numbers, and special characters
- Enable password aging and expiration policies
- Disable password reuse

To configure password policies, edit the `/etc/security/pwquality.conf` file and modify the relevant settings.

### 1.2 Restrict Root Access

Avoid using the root account for daily tasks, as it grants unrestricted access to the system. Instead, create non-privileged user accounts and use `sudo` to perform administrative tasks when necessary.

To configure `sudo` access, edit the `/etc/sudoers` file using the `visudo` command. Here, you can specify which users or groups are allowed to run specific commands with elevated privileges.

### 1.3 Enable Multi-Factor Authentication (MFA)

Implement multi-factor authentication (MFA) for an additional layer of security. MFA requires users to provide a second form of authentication, such as a one-time password (OTP) or a hardware token, in addition to their regular password.

There are various solutions for enabling MFA on Fedora, such as Google Authenticator or YubiKey.

## 2. File Permissions

### 2.1 Principle of Least Privilege

Apply the principle of least privilege to file permissions. This means granting users and processes only the minimum permissions necessary to perform their intended tasks. Regularly audit and adjust file permissions to ensure they are not unnecessarily permissive.

### 2.2 Restrict Access to Sensitive Files

Sensitive files, such as configuration files, logs, and private data, should have restricted access permissions. Use commands like `chmod`, `chown`, and `chgrp` to set appropriate permissions and ownership.

For example, to restrict access to a sensitive file (`/etc/shadow`) to the root user only, you can use the following command:

```bash
chmod 600 /etc/shadow
```

### 2.3 Disable Unnecessary Services

Disable or remove unnecessary services and daemons to reduce the attack surface. Only enable services that are strictly required for your system's intended purpose.

You can use the `systemctl` command to list, enable, disable, or stop services. For example, to disable the `cups` service (Common UNIX Printing System), you can run:

```bash
systemctl disable cups
```

## 3. System Hardening

### 3.1 Keep the System Up-to-Date

Regularly update your Fedora system with the latest security patches and software updates. This helps mitigate known vulnerabilities and protect against potential exploits.

Use the `dnf` package manager to update your system:

```bash
sudo dnf update
```

### 3.2 Enable Firewall

Enable the firewall to control incoming and outgoing network traffic. Fedora comes with the `firewalld` service, which provides a dynamic firewall management solution.

To enable the firewall, run:

```bash
sudo systemctl enable firewalld
sudo systemctl start firewalld
```

You can then use the `firewall-cmd` utility to configure firewall rules and open or close ports as needed.

### 3.3 Secure SSH Access

If you use SSH for remote access, configure it securely by following these best practices:

- Disable root login over SSH
- Use SSH keys instead of passwords for authentication
- Set a stronger ciphers and key exchange algorithms
- Limit access to specific users or IP addresses

Edit the `/etc/ssh/sshd_config` file to customize SSH settings according to your security requirements.

### 3.4 Enable Auditing and Logging

Enable system auditing and logging to monitor and track system events, user activities, and potential security incidents. Fedora uses the `auditd` service for auditing and `rsyslog` for logging.

Regularly review audit logs and system logs for any suspicious or unauthorized activities.

### 3.5 Implement SELinux

SELinux (Security-Enhanced Linux) is a mandatory access control system that enforces security policies on processes, files, and resources. It provides an additional layer of security by restricting what actions a process can perform, even if the user has root privileges.

Fedora comes with SELinux enabled by default, but you should ensure it is configured according to your security requirements. You can use the `sestatus` command to check the current SELinux status and the `semanage` utility to manage SELinux policies.

## 4. Additional Security Measures

### 4.1 Secure Network Services

If you are running network services like web servers, databases, or mail servers, ensure they are configured securely. Follow best practices specific to each service, such as enabling encryption, disabling unnecessary modules, and limiting access.

### 4.2 Implement Intrusion Detection/Prevention Systems

Consider implementing an Intrusion Detection System (IDS) or Intrusion Prevention System (IPS) to monitor network traffic and system activities for potential threats or malicious activities. Popular IDS/IPS solutions for Linux include Snort, Suricata, and OSSEC.

### 4.3 Perform Regular Security Audits

Regularly perform security audits to identify and address potential vulnerabilities in your Fedora system. This can include vulnerability scanning, penetration testing, and reviewing system configurations and logs.

### 4.4 Follow Security Best Practices

Stay up-to-date with the latest security best practices and guidelines from trusted sources, such as the Fedora Project, Red Hat, and industry-recognized security organizations.

## Conclusion

Implementing these system security best practices can significantly enhance the security of your Fedora Linux installation. However, it's important to note that security is an ongoing process, and you should regularly review and update your security measures to stay ahead of emerging threats and vulnerabilities.

Remember to always back up your system and data before making any significant changes, and consult official documentation or seek professional assistance if you are unsure about any security configuration or implementation.