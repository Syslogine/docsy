---
title: "Installing SSH Keys on Windows"
linkTitle: "Basic SSH"
description: "A guide to setting up SSH keys on Windows desktops and servers"
weight: 1
---

![alt text](/images/os/windows/windows_ssh.jpeg) 

# Installing and Setting Up SSH Keys on Windows

This guide explains how to install and configure SSH keys on Windows machines, whether you're working on a desktop or a server. SSH keys provide a secure way to authenticate with remote systems without needing a password.

## Prerequisites
- A Windows machine (Windows 10, 11, or Windows Server)
- Administrative access (for some steps)
- Internet connection (for downloading tools)

## Step 1: Check for Existing SSH Tools
Windows 10 (version 1809 and later) and Windows 11 come with a built-in OpenSSH client. To check if it's available:

1. Open a Command Prompt or PowerShell:
   - Press `Win + R`, type `cmd` or `powershell`, and hit Enter.
2. Run this command:
   ```
   ssh -V
   ```
3. If you see a version number (e.g., `OpenSSH_8.1p1`), the OpenSSH client is installed. Skip to Step 3.
4. If you get an error (e.g., "'ssh' is not recognized"), proceed to Step 2.

## Step 2: Install OpenSSH (if not already present)
### Option 1: Enable OpenSSH via Windows Features (Windows 10/11)
1. Open Settings:
   - Press `Win + I`.
2. Go to `Apps` > `Optional Features`.
3. Click `Add a feature`, search for "OpenSSH Client", and install it.
4. Verify installation:
   ```
   ssh -V
   ```

### Option 2: Install Git Bash (Alternative for Older Systems or Additional Tools)
1. Download Git for Windows from [git-scm.com](https://git-scm.com).
2. Run the installer, ensuring "Git Bash" is selected.
3. After installation, open Git Bash (search for it in the Start menu).
4. Use Git Bash as your terminal for SSH commands.

### Option 3: Install OpenSSH Server (For Windows Servers)
If you’re setting up a server to accept SSH connections:
1. Open PowerShell as Administrator:
   - Press `Win + X`, select `Windows PowerShell (Admin)`.
2. Install the OpenSSH Server:
   ```
   Add-WindowsCapability -Online -Name OpenSSH.Server~~~~0.0.1.0
   ```
3. Start the SSH server:
   ```
   Start-Service sshd
   Set-Service -Name sshd -StartupType 'Automatic'
   ```
4. Verify it’s running:
   ```
   Get-Service sshd
   ```

## Step 3: Generate SSH Keys
1. Open a terminal (Command Prompt, PowerShell, or Git Bash).
2. Generate a new SSH key pair:
   ```
   ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
   ```
   - `-t rsa`: Specifies RSA key type.
   - `-b 4096`: Sets key length to 4096 bits for extra security.
   - `-C`: Adds a comment (e.g., your email) to identify the key.
3. Press Enter to accept the default file location (`C:\Users\YourUsername\.ssh\id_rsa`).
4. Enter a passphrase (optional but recommended for added security) or leave blank.

   Output will look like:
   ```
   Your public key has been saved in /c/Users/YourUsername/.ssh/id_rsa.pub
   ```

## Step 4: Locate and Copy Your Public Key
1. Navigate to the SSH directory:
   ```
   cd %userprofile%\.ssh
   ```
2. Display your public key:
   ```
   type id_rsa.pub
   ```
   - Copy the entire output (starts with `ssh-rsa` and ends with your email).
   - Alternatively, open `id_rsa.pub` in Notepad and copy it.

## Step 5: Add the Public Key to the Remote Server
1. Log in to the remote server (via password or existing method).
2. Append your public key to the `~/.ssh/authorized_keys` file:
   - On the remote server, run:
     ```
     echo "your_public_key_here" >> ~/.ssh/authorized_keys
     ```
   - Replace `your_public_key_here` with the key you copied.
3. Ensure correct permissions (if using Git Bash or a Linux-like terminal):
   ```
   chmod 600 ~/.ssh/authorized_keys
   chmod 700 ~/.ssh
   ```

## Step 6: Configure SSH Client (Optional)
1. Create or edit the SSH config file:
   ```
   notepad %userprofile%\.ssh\config
   ```
2. Add an entry for your server:
   ```
   Host myserver
       HostName server_ip_or_domain
       User your_username
       IdentityFile ~/.ssh/id_rsa
   ```
3. Save and close the file.

## Step 7: Test the SSH Connection
1. Test your connection:
   ```
   ssh myserver
   ```
   - If you set up a config file with "myserver", this works. Otherwise, use:
     ```
     ssh your_username@server_ip_or_domain
     ```
2. If prompted, enter your passphrase (if you set one).

## Troubleshooting
- **"Permission denied"**: Ensure your public key is correctly added to the remote server’s `authorized_keys`.
- **"ssh not recognized"**: Verify OpenSSH is installed (Step 2).
- **Connection refused**: Ensure the remote server’s SSH service (sshd) is running and port 22 is open.

## Additional Tips
- **Backup Keys**: Copy your `.ssh` folder to a secure location.
- **Multiple Keys**: Use different filenames (e.g., `ssh-keygen -f ~/.ssh/my_server_key`) for multiple servers.
- **Windows Server**: If setting up a server, configure the firewall:
  ```
  New-NetFirewallRule -Name sshd -DisplayName 'OpenSSH Server (sshd)' -Enabled True -Direction Inbound -Protocol TCP -Action Allow -LocalPort 22
  ```

Now you’re ready to use SSH keys on your Windows machine!