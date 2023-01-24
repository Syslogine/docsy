---
linktitle: Create and use SSH
title: Create and use SSH
tags: ["ssh","rsa","dsa","ecdsa","eddsa"]
description: >
 Some security for your server is not always bad, so we made a quick tut for creating and use of SSH key.
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

1.	Be sure your system is up to date with packages
	```bash
	sudo apt update
	```
2.	Now we can install the `openssh-server` package
	```bash
	sudo apt install openssh-server -y
	```
3.	Check if `SSH` is running
	```bash
	sudo systemctl is-active sshd
	```
Congratulations now you got a SSH server.


## Create SSH Key
Now that we have a working ssh we can generate a SSH key

{{< alert color="warning" title="Warning" >}}Be sure when you do this step your on client device/machine and not on the server!{{< /alert >}}

*	My way of creating ssh key	
	```bash
	ssh-keygen -o -a 1000 -t ed25519 -f ~/.ssh/id_ed25519
	```

## Add Key to server
*	You can do this
	```bash
	ssh-copy-id syslogine@192.168.1.1
	```

## Secure Server
Open the file `sshd_config`
```bash
sudo nano /etc/ssh/sshd_config
```

Check the diffrence between this version and the one you ahev now currently... As this setup will work for me but maybe you have a other idea how to want setup your server.
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
After this set the permissions on 400 so there can be added a other key
```bash
sudo chmod 400 ~/.ssh/authorized_keys
```
Or it can be `600` but i need to test this...


### Fix Cannot Bind IP at Boot
at boot soo lets fix this issue with giving the ssh.service a delay of 30 seconds...

1.	Lets open the ssh.service
	```bash
	sudo nano /etc/system/
	```

2.	Find 
	```txt
	ExecStartPre=/usr/sbin/sshd -t
	```

3.	Add this in front of it !!!!!
	```txt
	ExecStartPre=/bin/sleep 30
	```

So it will looks like this:
```txt
ExecStartPre=/bin/sleep 30
ExecStartPre=/usr/sbin/sshd -t
```

## Explanation
```bash
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "john@example.com"
```

You’ll be asked to enter a passphrase for this key, use the strong one. You can also use the same passphrase like any of your old SSH keys.

### EDDSA
*	`-o` : Save the private-key using the new OpenSSH format rather than the PEM format. Actually, this option is implied when you specify the key type as `ed25519`.
*	`-a`: It’s the numbers of KDF (Key Derivation Function) rounds. Higher numbers result in slower passphrase verification, increasing the resistance to brute-force password cracking should the private-key be stolen.
*	`-t`: Specifies the type of key to create, in our case the `Ed25519`.
*	`-f`: Specify the filename of the generated key file. If you want it to be discovered automatically by the SSH agent, it must be stored in the default `.ssh` directory within your home directory.
*	`-C`: An option to specify a comment. It’s purely informational and can be anything. But it’s usually filled with `<login>@<hostname>` who generated the key.

### RSA
*	`-t`: Specifies the type of key to create, in our case the `rsa`.
*	`-b`: Set the bit of the encryption like: `512`, `1024`, `2048` and `4096`
*	`-f`: Specify the filename of the generated key file. If you want it to be discovered automatically by the SSH agent, it must be stored in the default `.ssh` directory within your home directory.

## Extra
How to `restart`, `start`, `stop`, `status`, etc etc. SSH service check further on: [systemctl services](/docs/operating-systems/debian/tutorials/info_systemcrl)





## Secure server