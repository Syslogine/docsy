---
linktitle: "Pixxy"
title: "Pixxy Framework"
---


Login into root
1.	Install sudo
	```
	apt install sudo git -y
	```

2.	Give sudo eprmissions
	```
	usermod -aG sudo user
	```

3.	Reboot server
	```
	reboot server .
	```
---

After relog

1.	Add user for Fivem Server
	```
	adduser fivem
	```

2.	Then login into fivem user account
	```
	su - fivem
	```


3.	Clone the script
	```
	git clone https://github.com/Syslogine/fivem-server-manager.git
	```

4.	give permissions to run the script
	```
	 chmod +x fivemanager.sh
	 ```

5.	Run the script
	 ```
	 ./fivemanager.sh start
	 ```
---