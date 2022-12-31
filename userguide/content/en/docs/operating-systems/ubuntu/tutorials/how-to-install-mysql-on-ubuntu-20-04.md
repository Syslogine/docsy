---
linkTitle: MySQL on 20.04
title: How To Install MySQL on Ubuntu 20.04
tags: ['how to', 'install', 'mysql', 'ubuntu', '20.04']
---

## Introduction
[MySQL](https://www.mysql.com/) is an open-source database management system, commonly installed as part of the popular LAMP (Linux, Apache, MySQL, PHP/Python/Perl) stack. It implements the relational model and uses Structured Query Language (better known as SQL) to manage its data.

This tutorial will go over how to install MySQL version 8.0 on an Ubuntu 20.04 server. By completing it, you will have a working relational database that you can use to build your next website or application.
## Prerequisites
To follow this tutorial, you will need:
*	One Ubuntu 20.04 server with a non-root administrative user and a firewall configured with UFW.
### Step 1 — Installing MySQL
On Ubuntu 20.04, you can install MySQL using the APT package repository. At the time of this writing, the version of MySQL available in the default Ubuntu repository is version 8.0.27.

To install it, update the package index on your server if you’ve not done so recently:
```bash
sudo apt update
```
Then install the `mysql-server` package:
```bash
sudo apt install mysql-server
```
Ensure that the server is running using the systemctl start command:
```bash
sudo systemctl start mysql.service
```
These commands will install and start MySQL, but will not prompt you to set a password or make any other configuration changes. Because this leaves your installation of MySQL insecure, we will address this next.

### Step 2 — Configuring MySQL
For fresh installations of MySQL, you’ll want to run the DBMS’s included security script. This script changes some of the less secure default options for things like remote root logins and sample users.

{{% alert title="Warning:" color="warning" %}}

As of July 2022, an error will occur when you run the `mysql_secure_installation` script without some further configuration. The reason is that this script will attempt to set a password for the installation’s **root** MySQL account but, by default on Ubuntu installations, this account is not configured to connect using a password.

Prior to July 2022, this script would silently fail after attempting to set the **root** account password and continue on with the rest of the prompts. However, as of this writing the script will return the following error after you enter and confirm a password:
```output
 ... Failed! Error: SET PASSWORD has no significance for user 'root'@'localhost' as the authentication method used doesn't store authentication data in the MySQL server. Please consider using ALTER USER instead if you want to change authentication parameters.

New password:
```
This will lead the script into a recursive loop which you can only get out of by closing your terminal window.

Because the `mysql_secure_installation` script performs a number of other actions that are useful for keeping your MySQL installation secure, it’s still recommended that you run it before you begin using MySQL to manage your data. To avoid entering this recursive loop, though, you’ll need to first adjust how your **root** MySQL user authenticates.

First, open up the MySQL prompt:
```bash
sudo mysql
```
Then run the following `ALTER USER` command to change the **root** user’s authentication method to one that uses a password. The following example changes the authentication method to `mysql_native_password`:
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
After making this change, exit the MySQL prompt:
```bash
exit
```
Following that, you can run the `mysql_secure_installation` script without issue.

Once the security script completes, you can then reopen MySQL and change the **root** user’s authentication method back to the default, `auth_socket`. To authenticate as the **root** MySQL user using a password, run this command:
```bash
mysql -u root -p
```
Then go back to using the default authentication method using this command:
```bash
ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
```
This will mean that you can once again connect to MySQL as your **root** user using the `sudo mysql` command.
{{% /alert %}}

### Step 3 — Creating a Dedicated MySQL User and Granting Privileges
### Step 4 — Testing MySQL
## Conclusion