---
linktitle: "SSH Creation and Usage Guide"
title: "SSH Creation and Usage Guide"
tags: ["ssh","rsa","dsa","ecdsa","eddsa"]
description: >
 Enhance your server security with our quick tutorial on creating and using SSH keys. Learn the essentials for a safer and more secure server environment.
---

<center>

![](/images/os/openssl.png)
</center>

## Info Table
|             | RSA             |	DSA	        | ECDSA  | 	EDDSA|
|-------------|-----------------|---------------|--------|-------|
| **POPULARITY**  | Most widely implemented and supported.| Its notorious security history makes it less popular. | Fairly new but not as popular as EdDSA. | Fairly new but favoured by most modern cryptographic libraries. |
| **PERFORMANCE** | Larger keys require more time to generate. | Faster for signature generation but slower for validation. | Public keys are twice the length of the desired bit security. | EdDSA is the fastest performing algorithm across all metrics. |
| **SECURITY**    | Specialized algorithms like Quadratic Sieve and General Number Field Sieve exist to factor integers with specific qualities. | DSA requires the use of a randomly generated unpredictable and secret value that, if discovered, can reveal the private key. | Vulnerable if pseudo random number aren't cryptographically strong. | EdDSA provides the highest security level compared to key length. It also improves on the insecurities found in ECDSA. |

## Install SSH
Ensure your system is equipped with the latest packages by running the following command:
```bash
sudo apt update
```

Once your system is up to date, proceed to install the `openssh-server` package:
```bash
sudo apt install openssh-server -y
```

Confirm that the SSH service is running smoothly:
```bash
sudo systemctl is-active sshd
```

Congratulations! Your SSH server is now up and running, ready to facilitate secure connections. Feel free to explore the next steps in configuring and maximizing the potential of your SSH setup.


## Create SSH Key
Now that your SSH is up and running, it's time to generate your SSH key.

### My Preferred Method:
Execute the following command to create an SSH key with enhanced security features:
```bash
ssh-keygen -o -a 1000 -t ed25519 -f ~/.ssh/id_ed25519
```

## Add Key to Server
Next, add your SSH key to the server with the following command:
```bash
ssh-copy-id syslogine@192.168.1.1
```

## Enhance Server Security
To strengthen server security, open the `sshd_config` file using the following command:
```bash
sudo nano /etc/ssh/sshd_config
```

Compare the differences between this version and your current setup. While this configuration suits my needs, you might have alternative preferences for setting up your server. Feel free to explore and adapt based on your specific requirements or discover new possibilities for optimizing your server environment.
```bash
Include /etc/ssh/sshd_config.d/*.conf

Port 3040
ListenAddress 192.168.1.1
HostKey /etc/ssh/ssh_host_ed25519_key
SyslogFacility AUTH
LogLevel VERBOSE
LoginGraceTime 60
PermitRootLogin no
StrictModes yes
MaxAuthTries 3
MaxSessions 2
PubkeyAuthentication yes
AuthorizedKeysFile     .ssh/authorized_keys
HostbasedAuthentication no
IgnoreRhosts yes
PasswordAuthentication no
PermitEmptyPasswords no
ChallengeResponseAuthentication no
UsePAM no
AllowAgentForwarding no
AllowTcpForwarding no
GatewayPorts no
X11Forwarding no
PrintMotd no
PrintLastLog yes
TCPKeepAlive yes
ClientAliveInterval 900
ClientAliveCountMax 0
UseDNS no
MaxStartups 2
PermitTunnel no
#Banner none
AcceptEnv LANG LC_*
Subsystem       sftp    /usr/lib/openssh/sftp-server
```
### Adjust Permissions for Additional Keys
After this step, set the permissions to 400 on the `authorized_keys` file to allow the addition of another key:
```bash
sudo chmod 400 ~/.ssh/authorized_keys
```
Alternatively, you can use `600`, but further testing is recommended.

### Resolve "Cannot Bind IP at Boot" Issue
If you encounter issues with IP binding at boot, follow these steps to introduce a 30-second delay to the `ssh.service`:

1. Open the `ssh.service` file for editing:
   ```bash
   sudo nano /etc/systemd/system/sshd.service
   ```

2. Locate the line:
   ```txt
   ExecStartPre=/usr/sbin/sshd -t
   ```

3. Add the following line before it:
   ```txt
   ExecStartPre=/bin/sleep 30
   ```

   The modified section should look like this:
   ```txt
   ExecStartPre=/bin/sleep 30
   ExecStartPre=/usr/sbin/sshd -t
   ```

## Explanation
The delay ensures that the `ssh.service` has adequate time during boot, addressing potential issues with IP binding. Adjusting the timing can contribute to a smoother and more reliable startup process.

```bash
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "john@example.com"
```

This `ssh-keygen` command generates an Ed25519 SSH key with increased security parameters and associates it with the specified email address. Customize the parameters based on your security preferences.

### EDDSA
- `-o`: Save the private key in the OpenSSH format rather than the PEM format. Implicitly used with the `ed25519` key type.
- `-a`: Sets the number of Key Derivation Function (KDF) rounds. Higher values increase resistance to brute-force attacks if the private key is compromised.
- `-t`: Specifies the key type, such as `ed25519`.
- `-f`: Sets the filename for the generated key. To be automatically discovered by the SSH agent, store it in the default `.ssh` directory in your home directory.
- `-C`: Adds a comment for informational purposes, often in the format `<login>@<hostname>`.

### RSA
- `-t`: Specifies the key type, such as `rsa`.
- `-b`: Sets the encryption bit, like `512`, `1024`, `2048`, or `4096`.
- `-f`: Sets the filename for the generated key. To be automatically discovered by the SSH agent, store it in the default `.ssh` directory in your home directory.

## Extra
Explore more about managing SSH service with commands like `restart`, `start`, `stop`, `status`, etc. Refer to [systemctl services](/docs/operating-systems/debian/tutorials/info_systemcrl) for detailed information.