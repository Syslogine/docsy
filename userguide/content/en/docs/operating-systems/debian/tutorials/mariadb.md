---
linktitle: Install MariaDB
title: How To install MariaDB on Debian server.
categories: ["debian"]
tags: ["debian","how to","mariadb"]
weight: 1
description: >
 small and fast tutorial for installing MariaDB on a debian machine.
---


## Debian update, install some packages
### Video
<iframe width="560" height="315" src="https://www.youtube.com/embed/dXiodf31YSk" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

### Text
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
### video
<iframe width="560" height="315" src="https://www.youtube.com/embed/jUqDdp90P-s" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>


### txt
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




