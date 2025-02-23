---
linktitle: MariaDB on 20.04
title: How To Install MariaDB on Ubuntu 20.04
tags: ['how to', 'install', 'mariadb', 'ubuntu', '20.04']
categories: ["Ubuntu"]
description: >
  This tutorial will show you how to install a MariaDB on Ubuntu 20.04
---

## Introduction
[MariaDB](https://mariadb.org/) is an open-source relational database management system, commonly used as an alternative for MySQL as the database portion of the popular [LAMP](https://www.digitalocean.com/community/tutorials/how-to-install-linux-apache-mysql-php-lamp-stack-on-ubuntu-20-04) (Linux, Apache, MySQL, PHP/Python/Perl) stack. It is intended to be a drop-in replacement for MySQL.

The short version of this installation guide consists of these three steps:
*	Update your package index using `apt`
*	Install the `mariadb-server` package using `apt`. The package also pulls in related tools to interact with MariaDB
*	Run the included `mysql_secure_installation` security script to restrict access to the server
```bash
sudo apt update
sudo apt install mariadb-server
sudo mysql_secure_installation
```

```bash
sudo apt update &&\
sudo apt install mariadb-server -y &&\
sudo mysql_secure_installation
```

This tutorial will explain how to install MariaDB on an Ubuntu 20.04 server and verify that it is running and has a safe initial configuration.

## Prerequisites
To follow this tutorial, you will need a server running Ubuntu 20.04. This server should have a non-root administrative user and a firewall configured with UFW. Set this up by following [our initial server setup guide for Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu-20-04).

### Step 1 — Installing MariaDB
As of this writing, Ubuntu 20.04’s default APT repositories include MariaDB version `10.3`.

To install it, update the package index on your server with `apt`:
```bash
sudo apt update
```
Then install the package:
```bash
sudo apt install mariadb-server
```
Ensure that MariaDB is running with the `systemctl start` command:
```bash
sudo systemctl start mariadb.service
```
These commands will install and start MariaDB, but will not prompt you to set a password or make any other configuration changes. Because the default configuration leaves your installation of MariaDB insecure, we will use a script that the `mariadb-server` package provides to restrict access to the server and remove unused accounts.

### Step 2 — Configuring MariaDB
For new MariaDB installations, the next step is to run the included security script. This script changes some of the less secure default options for things like remote **root** logins and sample users.

Run the security script:
```bash
sudo mysql_secure_installation
```
This will take you through a series of prompts where you can make some changes to your MariaDB installation’s security options. The first prompt will ask you to enter the current database **root** password. Since you have not set one up yet, press `ENTER` to indicate “none”.
```
NOTE: RUNNING ALL PARTS OF THIS SCRIPT IS RECOMMENDED FOR ALL MariaDB
      SERVERS IN PRODUCTION USE!  PLEASE READ EACH STEP CAREFULLY!

In order to log into MariaDB to secure it, we'll need the current
password for the root user.  If you've just installed MariaDB, and
you haven't set the root password yet, the password will be blank,
so you should just press enter here.

Enter current password for root (enter for none):
```
The next prompt asks you whether you’d like to set up a database **root** password. On Ubuntu, the **root** account for MariaDB is tied closely to automated system maintenance, so we should not change the configured authentication methods for that account. Doing so would make it possible for a package update to break the database system by removing access to the administrative account. Type `N` and then press `ENTER`.
```
. . .
OK, successfully used password, moving on...

Setting the root password ensures that nobody can log into the MariaDB
root user without the proper authorisation.

Set root password? [Y/n] N
```
Later, we will cover how to set up an additional administrative account for password access if socket authentication is not appropriate for your use case.

From there, you can press `Y` and then `ENTER` to accept the defaults for all the subsequent questions. This will remove some anonymous users and the test database, disable remote **root** logins, and load these new rules so that MariaDB immediately implements the changes you have made.

With that, you’ve finished MariaDB’s initial security configuration. The next step is an optional one, though you should follow it if you prefer to authenticate to your MariaDB server with a password.

### Step 3 — (Optional) Creating an Administrative User that Employs Password Authentication
On Ubuntu systems running MariaDB 10.3, the **root** MariaDB user is set to authenticate using the `unix_socket` plugin by default rather than with a password. This allows for some greater security and usability in many cases, but it can also complicate things when you need to allow an external program (e.g., phpMyAdmin) administrative rights.

Because the server uses the **root** account for tasks like log rotation and starting and stopping the server, it is best not to change the **root** account’s authentication details. Changing credentials in the `/etc/mysql/debian.cnf` configuration file may work initially, but package updates could potentially overwrite those changes. Instead of modifying the **root** account, the package maintainers recommend creating a separate administrative account for password-based access.

To this end, we will create a new account called **admin** with the same capabilities as the **root** account, but configured for password authentication. Open up the MariaDB prompt from your terminal:
```bash
sudo mariadb
```
Then create a new user with **root** privileges and password-based access. Be sure to change the username and password to match your preferences:
```bash
GRANT ALL ON *.* TO 'admin'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;
```
Flush the privileges to ensure that they are saved and available in the current session:
```bash
FLUSH PRIVILEGES;
```
Following this, exit the MariaDB shell:
```bash
exit
```
Finally, let’s test the MariaDB installation.

### Step 4 — Testing MariaDB
When installed from the default repositories, MariaDB will start running automatically. To test this, check its status.
```bash
sudo systemctl status mariadb
```
You’ll receive output that is similar to the following:
```
● mariadb.service - MariaDB 10.3.22 database server
     Loaded: loaded (/lib/systemd/system/mariadb.service; enabled; vendor preset: enabled)
     Active: active (running) since Tue 2020-05-12 13:38:18 UTC; 3min 55s ago
       Docs: man:mysqld(8)
             https://mariadb.com/kb/en/library/systemd/
   Main PID: 25914 (mysqld)
     Status: "Taking your SQL requests now..."
      Tasks: 31 (limit: 2345)
     Memory: 65.6M
     CGroup: /system.slice/mariadb.service
             └─25914 /usr/sbin/mysqld
. . .
```
If MariaDB isn’t running, you can start it with the command `sudo systemctl start mariadb`.

For an additional check, you can try connecting to the database using the `mysqladmin` tool, which is a client that lets you run administrative commands. For example, this command says to connect to MariaDB as **root** using the Unix socket and return the version:
```bash
sudo mysqladmin version
```
You will receive output similar to this:
```
mysqladmin  Ver 9.1 Distrib 10.3.22-MariaDB, for debian-linux-gnu on x86_64
Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.

Server version		10.3.22-MariaDB-1ubuntu1
Protocol version	10
Connection		Localhost via UNIX socket
UNIX socket		/var/run/mysqld/mysqld.sock
Uptime:			4 min 49 sec

Threads: 7  Questions: 467  Slow queries: 0  Opens: 177  Flush tables: 1  Open tables: 31  Queries per second avg: 1.615
```
If you configured a separate administrative user with password authentication, you could perform the same operation by typing:
```bash
mysqladmin -u admin -p version
```
This means that MariaDB is up and running and that your user is able to authenticate successfully.

## Conclusion
In this guide you installed the MariaDB relational database management system, and secured it using the `mysql_secure_installation` script that it came installed with. You also had the option to create a new administrative user that uses password authentication before testing the MariaDB server’s functionality.