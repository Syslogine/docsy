---
title: "Jetson Nano"
description: ""
weight: 1
---

# Jetson Nano with CrewAI, Claude and OpenAI

Yes you read this right im gonna build an nice system with the jetson nano that use ai and camera 

* Face Reconiziion
* Speeche Reconigzion 



## [First install](step-one) 






## useful links
*	https://repo.download.nvidia.com/jetson/
*	https://google.com
*	https://www.arducam.com/faq/kernel-camera-driver/


The four most improtant tool for your selever are

```bash
sudo apt-get install curl git nano wget
```





after making an `.sh` it need cmod to be able to use

```bash
sudo chmod +x mytools.sh
```


CSI Camera
```bash
sudo apt install libcanberra-gtk-module libcanberra-gtk3-module -y
```



List to do


-	Windows Disk wiper
-	Linux/Mac Disk wiper



How i work

1.	I use ChatGPT 3.5 for my normal converations of creating an basic script/code/text
2.	After i have the basic script, code, text or anything else to Claude for improving.


edit th l4t botloader to new version
```bash
sudo nano /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
```

This is nee

```bash

LABEL primary
      MENU LABEL primary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} root=PARTUUID=b49df890-238c-4497-99a6-0644b9077530 rootwait rootfstype=ext4

LABEL secondary
      MENU LABEL secondary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} quiet root=/dev/mmcblk0p1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0



```


    from pip._internal import main as pipmain

    print("Try to install jetson-stats...")
    pipmain(['install', 'jetson-stats'])

    print("Try to install v4l2-fix...")
    pipmain(['install', 'v4l2-fix'])

    from utils import ArducamUtils



When this pops up use `N`
```bash
Setting up nvidia-l4t-core (32.7.4-20230608212426) ...

Configuration file '/etc/ld.so.conf.d/nvidia-tegra.conf'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** nvidia-tegra.conf (Y/I/N/O/D/Z) [default=N] ? n
```

and

And then when this comes up u can select `Y`
```sh
Setting up nvidia-l4t-oem-config (32.7.4-20230608212426) ...

Configuration file '/etc/systemd/nv-oem-config-post.sh'
 ==> Deleted (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** nv-oem-config-post.sh (Y/I/N/O/D/Z) [default=N] ? y
```


remove all libreoffice
```bash
sudo apt-get autoremove libreoffice* -y
```

then 
```bash
sudo apt-get clean
```

### Install pip and pip3
```bash
sudo apt install python-pip python3-pip
```

### Install Jetson Stats
```bash
sudo pip3 install -U jetson-stats
```

Now reboot the jetson nano to use the `jtop` command
```bash
sudo reboot now
```

Open terminal back open and type
```bash
jtop
```

### Jetson Fan
Now to make the fans start at boot we need

1.	Open and edit `rc.local`
	```bash
	sudo nano /etc/rc.local
	```

	past this in 
	```sh
	#!/bin/bash
	sleep 10
	sudo /usr/bin/jetson_clocks
	sudo sh -c ‘echo 255 > /sys/devices/pwm-fan/target_pwm’
	exit 0
	```

2.	now we
	```bash
	sudo nano /etc/systemd/system/rc-local.service
	```
	past this in there
	```txt
	[Unit]
	 Description=/etc/rc.local Compatibility
	 ConditionPathExists=/etc/rc.local

	[Service]
	 Type=forking
	 ExecStart=/etc/rc.local start
	 TimeoutSec=0
	 StandardOutput=tty
	 RemainAfterExit=yes
	 SysVStartPriority=99

	[Install]
	 WantedBy=multi-user.target
	 ```

3.	Then add execute permission to `/etc/rc.local` file.
	```bash
	sudo chmod +x /etc/rc.local
	```

4.	After that, enable the service on system boot:
	```bash
	sudo systemctl enable rc-local
	```

5.	Now start the service
	```
	sudo systemctl start rc-local.service
	```


