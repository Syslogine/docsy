---
linktitle: Create and use SSH

---



<center>

![](https://blog.apnic.net/wp-content/uploads/2019/10/OpenSSL_banner.png?v=bba6dede35671c7edca88c309d9c93fd)
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
Congratulations now you got a SSH server.


## Create SSH Key
Now that we have a working ssh we can generate a SSH key



*	My way of creating ssh key	
	```bash
	ssh-keygen -o -a 1000 -t ed25519 -f ~/.ssh/id_ed25519
	```




## Add Key to server
*	You can do this
	```bash
	ssh-copy-id syslogine@192.168.0.1
	```




## Explanation

```bash
ssh-keygen -o -a 100 -t ed25519 -f ~/.ssh/id_ed25519 -C "john@example.com"
```

You’ll be asked to enter a passphrase for this key, use the strong one. You can also use the same passphrase like any of your old SSH keys.

### EDDSA
*	`-o` : Save the private-key using the new OpenSSH format rather than the PEM format. Actually, this option is implied when you specify the key type as `ed25519`.
*	`-a`: It’s the numbers of KDF (Key Derivation Function) rounds. Higher numbers result in slower passphrase verification, increasing the resistance to brute-force password cracking should the private-key be stolen.
*	`-t`: Specifies the type of key to create, in our case the Ed25519.
*	`-f`: Specify the filename of the generated key file. If you want it to be discovered automatically by the SSH agent, it must be stored in the default `.ssh` directory within your home directory.
*	`-C`: An option to specify a comment. It’s purely informational and can be anything. But it’s usually filled with `<login>@<hostname>` who generated the key.



### RSA
*	`-t`: For rsa we use `rsa`
*	`-b`: Set the bit of the encryption like: `512`, `1024`, `2048` and `4096`









## Secure server