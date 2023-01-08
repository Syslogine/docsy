---
linkTitle: Create Sudo user on 20.04
title: How To Create A New Sudo Enabled User on Ubuntu 20.04
tags: ['how to', 'create', 'sudo', 'user', 'ubuntu', '20.04']
categories: ["Ubuntu"]
description: >
  This tutorials will explain how to create a sudo user on Ubuntu 20.04
---


## Introduction
When managing a server, you’ll sometimes want to allow users to execute commands as “root,” the administrator-level user. The `sudo` command provides system administrators with a way to grant administrator privileges — ordinarily only available to the **root** user — to normal users.

In this tutorial, you’ll learn how to create a new user with `sudo` access on Ubuntu 20.04 without having to modify your server’s `/etc/sudoers` file.
{{< alert >}}If you want to configure `sudo` for an existing user, skip to step 3.{{< /alert >}}

### Step 1 — Logging Into Your Server
SSH in to your server as the **root** user:
```bash
ssh root@your_server_ip_address
```

### Step 2 — Adding a New User to the System
Use the adduser command to add a new user to your system:
```bash
adduser sammy
```
Be sure to replace `sammy` with the username that you want to create. You will be prompted to create and verify a password for the user:
```
Enter new UNIX password:
Retype new UNIX password:
passwd: password updated successfully
```
Next, you’ll be asked to fill in some information about the new user. It is fine to accept the defaults and leave this information blank:
```
Changing the user information for sammy
Enter the new value, or press ENTER for the default
    Full Name []:
    Room Number []:
    Work Phone []:
    Home Phone []:
    Other []:
Is the information correct? [Y/n]
```

### Step 3 — Adding the User to the sudo Group
Use the `usermod` command to add the user to the **sudo** group:
```bash
usermod -aG sudo sammy
```
Again, be sure to replace `sammy` with the username you just added. By default on Ubuntu, all members of the **sudo** group have full `sudo` privileges.

### Step 4 — Testing sudo Access
To test that the new `sudo` permissions are working, first use the `su` command to switch to the new user account:
```bash
su - sammy
```
As the new user, verify that you can use `sudo` by prepending `sudo` to the command that you want to run with superuser privileges:
```bash
sudo command_to_run
```
For example, you can list the contents of the `/root` directory, which is normally only accessible to the root user:
```bash
sudo ls -la /root
```
The first time you use `sudo` in a session, you will be prompted for the password of that user’s account. Enter the password to proceed:
```
[sudo] password for sammy:
```
{{< alert >}}This is *not* asking for the **root** password! Enter the password of the sudo-enabled user you just created.{{< /alert >}}

If your user is in the proper group and you entered the password correctly, the command that you issued with `sudo` will run with **root** privileges.

## Conclusion
In this quickstart tutorial, we created a new user account and added it to the **sudo** group to enable `sudo` access.
