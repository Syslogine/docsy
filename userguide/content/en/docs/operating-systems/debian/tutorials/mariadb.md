---
linktitle: Install MariaDB
title: How To install MariaDB on Debian server.
categories: ["debian"]
tags: ["debian","how to","mariadb"]
weight: 1
description: >
 small and fast tutorial for installing MariaDB on a debian machine.
---


## Update, Install packages
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/dXiodf31YSk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></center>
<br>

1.  First we need to login into `root` account
    ```bash
    su -
    ```
    Type your `root` password

2.  after we are in the root account we can `update`
    ```bash
    apt update
    ```
3.  If there are packages need to eb upgarded we use
    ```bash
    apt upgrade -y
    ```
4.  So now install some packages we need for MariaDB and for later use.
    ```bash
    apt install nano sudo git curl
    ```
5.  Can clean if want... Not really needed
    ```bash
    apt autoremove -y && apt clean
    ```


## Create sudo user
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/jUqDdp90P-s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></center>
<br>

1.  Lets login into `root` user
    ```bash
    su -
    ```
    Enter `root` passwd

2.  We need to edit the `sudoers` file
    ```bash
    visudo
    ```

3.  Replace `unknown` with your own username
    ```txt
    unknown ALL=(ALL) NOPASSWD:ALL
    ```
    To exit nano press: `Ctrl` + `X` and then it will ask if wan to save it so press `Y` adn then `Enter`

4.  Now we can exit the `root` user account
    ```bash
    exit
    ```

5.  Now its time to test if our useraccount has rood priviliges.
    ```bash
    sudo apt update
    ```
    Now enter your `useraccount` password.


## Installing and configuring MariaDB
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/pnZAxSXGDhs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></center>
<br>

1.  Now we can install `mariadb-server`
    ```bash
    sudo apt install mariadb-server
    ```
2.  Check status of mariadb
    ```bash
    sudo systemctl status mariadb
    ```
3.  Now that we know MariaDB server is active and running we need to secure it a little.
    ```bash
    sudo mysql_secure_installation
    ```
    1.  Enter current password for root (enter for none): `enter`
    2.  Switch to unix_socket authentication [Y/n]: `n`
    3.  Change the root password? [Y/n]: `y`
        *   Create a password
        *   type again password
    4.  Remove anonymous users? [Y/n]: `y`
    5.  Disallow root login remotely? [Y/n]: `y`
    6.  Remove test database and acces to it? [Y/n]: `y`
    7.  Reload privilege tables now? [Y/n]: `y`
4.  Not really needed but he lets restart our mariadb server
    ```bash
    sudo systemctl restart mariadb
    ```

## Create mysql user
<center><iframe width="560" height="315" src="https://www.youtube.com/embed/bYsvrI1dwdc" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe></center>
<br>

1.  Lets login into MariaDB `root` account and create a user
    ```bash
    mysql -u root -p
    ```
    enter your `mariadb root` password.

2.  Lets create a user
    *   Replace `syslogine` with your wanted username
    *   Replace `localhost` with `%` or `IP` if want other conenction
    *   Replace `password`
    ```mysql
    CREATE USER 'syslogine'@'localhost' IDENTIFIED BY 'password';
    ```

3.  Give the new created permissions
    *   Replace `syslogine` with new created user
    *   Replace `localhost` with `%` or `IP` if want other conenction
    ```mysql
    GRANT ALL PRIVILEGES ON *.* TO 'syslogine'@'localhost' WITH GRANT OPTION;
    ```
4.  Now flush it.
    ```mysql
    FLUSH PRIVILEGES;
    ```
5.  Now we exit mysql with
    ```mysql
    exit
    ```

Done...
