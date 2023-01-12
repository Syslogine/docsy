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
6.  `clear` page or `restart`.. Again both not needed ;)
    ```bash
    clear
    ```
    or
    ```bash
    reboot now
    ```