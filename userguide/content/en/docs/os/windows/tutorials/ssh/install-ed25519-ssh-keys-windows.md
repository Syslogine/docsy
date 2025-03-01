---
title: "Installing Ed25519 SSH Keys on Windows"
linkTitle: "Ed25519"
description: "A guide to generating and configuring Ed25519 SSH keys on Windows desktops and servers"
weight: 2
---

![alt text](/images/os/windows/windows_ed25519.jpeg) 

# Installing and Setting Up Ed25519 SSH Keys on Windows

This guide focuses on generating and configuring Ed25519 SSH keys on Windows machines (desktops or servers). Ed25519 is a modern, secure, and efficient elliptic curve cryptography algorithm, offering better performance and security compared to older key types like RSA.

## Why Ed25519?
- **Security**: Resistant to certain cryptographic attacks and side-channel vulnerabilities.
- **Speed**: Faster key generation and authentication.
- **Compact**: Smaller key size (256 bits) with equivalent security to larger RSA keys.

## Prerequisites
- A Windows machine (Windows 10, 11, or Windows Server).
- Administrative access (for some steps).
- Internet connection (for tool installation if needed).

## Step 1: Verify OpenSSH Availability
Windows 10 (version 1809+) and Windows 11 include a built-in OpenSSH client. Check if it’s installed:

1. Open Command Prompt or PowerShell:
   - Press `Win + R`, type `cmd` or `powershell`, and press Enter.
2. Run:
   ```
   ssh -V
   ```
3. If a version appears (e.g., `OpenSSH_8.1p1`), proceed to Step 3.
4. If not (e.g., "'ssh' is not recognized"), continue to Step 2.

## Step 2: Install OpenSSH Client (if needed)
1. Open Settings:
   - Press `Win + I`.
2. Navigate to `Apps` > `Optional Features`.
3. Click `Add a feature`, search for "OpenSSH Client", and install it.
4. Verify:
   ```
   ssh -V
   ```

## Step 3: Generate an Ed25519 SSH Key
1. Open a terminal (Command Prompt, PowerShell, or Git Bash if installed).
2. Generate the key pair:
   ```
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   - `-t ed25519`: Specifies the Ed25519 key type.
   - `-C`: Adds a comment (e.g., your email) for identification.
3. Press Enter to accept the default location (`C:\Users\YourUsername\.ssh\id_ed25519`).
4. Enter a passphrase (recommended for security) or leave blank.

   Output example:
   ```
   Your public key has been saved in C:\Users\YourUsername\.ssh\id_ed25519.pub
   ```

## Step 4: Copy Your Public Key
1. Navigate to the SSH directory:
   ```
   cd %userprofile%\.ssh
   ```
2. Display the public key:
   ```
   type id_ed25519.pub
   ```
   - Copy the output (starts with `ssh-ed25519` and ends with your comment).

## Step 5: Add the Public Key to a Remote Server
1. Access the remote server (via password or existing method).
2. Append your public key to `~/.ssh/authorized_keys`:
   ```
   echo "your_public_key_here" >> ~/.ssh/authorized_keys
   ```
   - Replace `your_public_key_here` with the copied key.
3. Set permissions (if using a Linux-like terminal):
   ```
   chmod 600 ~/.ssh/authorized_keys
   chmod 700 ~/.ssh
   ```

## Step 6: Test the Connection
1. Test the SSH connection:
   ```
   ssh your_username@server_ip_or_domain
   ```
2. Enter your passphrase if set. Success means you’re authenticated with your Ed25519 key!

## Optional: Configure SSH Client
1. Create/edit the SSH config file:
   ```
   notepad %userprofile%\.ssh\config
   ```
2. Add:
   ```
   Host myserver
       HostName server_ip_or_domain
       User your_username
       IdentityFile ~/.ssh/id_ed25519
   ```
3. Save and test:
   ```
   ssh myserver
   ```

## Troubleshooting
- **"Permission denied"**: Verify the public key is correctly added to the remote server’s `authorized_keys`.
- **"ssh not recognized"**: Ensure OpenSSH is installed (Step 2).
- **Connection issues**: Confirm the remote server supports Ed25519 (OpenSSH 6.5+ required).

## Additional Tips
- **Backup**: Save your `.ssh` folder securely.
- **Custom Filename**: Use `-f ~/.ssh/custom_name` with `ssh-keygen` for multiple keys.
- **Windows Server Setup**: If hosting SSH, install OpenSSH Server and configure the firewall:
   ```
   Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
   Start-Service sshd
   Set-Service -Name sshd -StartupType 'Automatic'
   New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
   ```

You’re now set with a secure Ed25519 SSH key on Windows!
