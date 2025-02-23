---
linktitle: "normal user sudo permissions"
weight: 2
---


## How to create a new normal user with sudo permission in Kali Linux


Kali Linux, the pentester’s Linux does not need an introduction. Today, I’ll show you how to create a normal user under Kali Linux. You might ask, Why would someone want to create a normal/standard user in Kali? What’s wrong with root only? Well, simply saying, being root all the time is not so good. Some applications won’t work in root. (Google chrome won’t work in root by default). If you want to use Kali as a day to day operating system, I’d suggest you to create a standard user and use it. If you want to do pentesting and stuff, you could ‘sudo’ or just log in as root.


Here’s how you will create a normal user

Open a terminal and issue the following command.
```bash
useradd -m username
# -m creates a home directory for the user.
```
Now we have to set a password for the user.
```bash
passwd username
```
It will ask you to create a new password.


At this point, we have a new user account. But we might want to add our new user to the “sudoers” group, so that we can use “sudo” to do administrative actions.
```bash
usermod -a -G sudo username
```
The option -a means to add and ‘-G sudo’ means to add the user to the sudo group. If you want to know more about the usermod command, issue man usermod command to know more about usermod


Now we have to specify the shell for our new user.
```bash
chsh -s /bin/bash username
```
chsh command is used to change the login shell for a user.


All done.! you are all set. You could logout and login to your new account.