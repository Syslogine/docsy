---
linktitle: Cutsom install mariaDB
title: Cutsom install mariaDB
tags: ['how to', 'install', 'mariadb', 'ubuntu', '20.04', "22.04"]
categories: ["Ubuntu"]
description: >
  Cutsom install for mariaDB on Ubuntu server or desktop
---


my way of installing a MariaDB server on you Ubuntu sevrer or dekstop


let's check if we have some updates before we begin with installing MariaDB
```bash
sudo apt update
```

Now that we know our system is up to date can we begin with installing of MariaDB
```bash
sudo apt install mariadb-server
```


After the install of MariaDB we can enableing the systemctl with just typing
```bash
sudo systemctl enable mariadb
```

Just to be sure mariadb is running we can just start the server with
```bash 
sudo systemctl start mariadb
```


{{% alert title="Note" %}}

Common command for your mariadb server..

*	Use `start` for starting the server
	```bash
	sudo systemctl start mariadb
	```
*	Use `stop` For stopping the server
	```bash
	sudo systemctl stop mariadb
	```
*	Use `restart` For restarting the server
	```bash
	sudo systemctl restart mariadb
	```
*	Use `status` For checking te status of server
	```bash
	sudo systemctl status mariadb
	```

{{% /alert %}}


Next

Now we going to configure the mariadb server and securing it by the following steps
```bash
sudo mysql_secure_installation
```

BE NOTED THIS WILL BE FIXED SOME TIME... BUT NOW NOW



### Hello you...
```bash
mysql -u root -p
```

*	Only `localhost` is allowd to connect... 
	```mysql
	CREATE USER 'local_user'@'localhost' IDENTIFIED BY 'password';
	```

* Now you can login from any IP to your
	```mysql
	CREATE USER 'local_user'@'%' IDENTIFIED BY 'password';
	```

* This will allow you only to login from specific IP
	```mysql
	CREATE USER 'local_user'@'192.168.1.1' IDENTIFIED BY 'password';
	```

## Hi hi

```mysql
GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
```

```mysql
FLUSH PRIVILEGES;
```


LOLLLLLLLLLLLL