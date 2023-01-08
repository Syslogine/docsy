---
linktitle: Cutsom install mariaDB
title: Cutsom install mariaDB
tags: ['how to', 'install', 'mariadb', 'ubuntu', '20.04']
categories: ["Ubuntu"]
description: >
  Cutsom install mariaDB
---


my way of install a mariadb on you ubunti mchine


let's check if we have soem updates before we begin
```bash
sudo apt update
```

now we going to install the latest version of mariadb
```bash
sudo apt install mariadb-server
```



Enable the mariadb systemdctl
```bash
sudo systemctl enable mariadb
```

now we going to start the mariadb if it's not already
```bash 
sudo systemctl start mariadb
```


{{% alert title="Note" %}}

You can use the commands 

*	start
	```bash
	sudo systemctl start mariadb
	```

*	restart
	```bash
	sudo systemctl restart mariadb
	```

*	status
	```bash
	sudo systemctl status mariadb
	```

{{% /alert %}}


Next

Now we goign to configure the mariadb
```bash
sudo mysql_secure_installation
```




LOLLLLLLLLLLLL