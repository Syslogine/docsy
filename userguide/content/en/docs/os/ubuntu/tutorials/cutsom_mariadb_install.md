---
linktitle: Cutsom install mariaDB
title: Cutsom install mariaDB
tags: ['how to', 'install', 'mariadb', 'ubuntu', '20.04', "22.04"]
categories: ["Ubuntu"]
description: >
  Cutsom install for mariaDB on Ubuntu server or desktop
---




# Custom tutorial for MariaDB on Ubuntu.


## Step 1
1.	Before we begin we need to update our apt packages with
	```bash
	sudo apt updates
	```
2.	After we updates our packages we can install `mariadb-server`
	```bash
	sudo apt install mariadb-server
	```
3.	Now MariaDB server is installed we can check if it's running
	```bash
	sudo systemctl status mariadb
	```

## Step 2
1.	Now we need to secure our MariaDB so type
	```bash
	sudo mysql_secure_installation
	```
2.	It will start with asking for root password for mariadb, just press `enter`





{{% alert title="Common commands" %}}

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



### examples for `localhost`, `%`, `specific`

*	Only `localhost` is allowd to connect... 
	```mysql
	CREATE USER 'local_user'@'localhost' IDENTIFIED BY 'password';
	```

* Now you can login from `any` IP to your
	```mysql
	CREATE USER 'local_user'@'%' IDENTIFIED BY 'password';
	```

* This will allow you only to login from `specific` IP
	```mysql
	CREATE USER 'local_user'@'192.168.1.1' IDENTIFIED BY 'password';
	```

## Giving user grant all privileges
1.	Let's login with our `root` use in MariaDB
	```bash
	mysql -u root -p
	```

2.	Replace `syslogine` with your own enw created used and replace `localhost` if want.
	```mysql
	GRANT ALL PRIVILEGES ON *.* TO 'syslogine'@'localhost' WITH GRANT OPTION;
	```

3.	Lets save it.
	```mysql
	FLUSH PRIVILEGES;
	```

4.	Yes now we can exit the `mysql`
	```mysql
	exit
	```


## Edit MariaDB `50-server.cnf`
```bash
cd /etc/mysql



LOLLLLLLLLLLLL