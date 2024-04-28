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


## Items
*	[Samsung EVO microSDXC 64GB](https://www.samsung.com/us/computing/memory-storage/memory-cards/evo-plus-adapter-microsdxc-64gb-mb-mc64sa-am/)
*	[Noctua NF-A4x20 5V PWM](https://noctua.at/en/nf-a4x20-5v-pwm)
*	[Wall power supply](https://www.adafruit.com/product/1466)



## useful links
*	https://repo.download.nvidia.com/jetson/
*	https://google.com
*	https://www.arducam.com/faq/kernel-camera-driver/



## Fresh Install Setup Guide for Jetson Nano

Once your Jetson Nano board is up and running with Ubuntu Desktop, let's kickstart the setup process by opening the terminal and following these steps:

### Step 1: Update System

First, let's ensure your system is up to date:

```bash
sudo apt update -y
```

Next, upgrade your Jetson Nano:

```bash
sudo apt upgrade -y
```

During the upgrade process, you may encounter prompts for configuration files. For each prompt, such as `'/etc/ld.so.conf.d/nvidia-tegra.conf'` and `'/etc/systemd/nv-oem-config-post.sh'`, select `Y` to install the package maintainer's version.

Additionally, if prompted to restart Docker, select `YES`.

Now, let's perform a distribution upgrade:

```bash
sudo apt dist-upgrade -y
```

### Step 2: Clean Up

Once the upgrade process is complete, let's tidy up by removing old packages:

```bash
sudo apt autoremove -y
```

And finally, let's clean up the cache:

```bash
sudo apt clean
```

### Step 3: Reboot

After these maintenance tasks, it's recommended to reboot your Jetson Nano for changes to take effect:

```bash
sudo reboot now
```


## Install Useful Tools

Here are some essential tools that are handy for almost every project:

```bash
sudo apt install git nano curl wget -y
```


## Uninstall LibreOffice

If you no longer need LibreOffice and want to reclaim some disk space, follow these steps to remove it:

```bash
sudo apt autoremove libreoffice* -y
```

This command will uninstall all LibreOffice packages from your system.

After removing LibreOffice, let's clean up the residual files:

```bash
sudo apt clean
```

This command will clean the package cache, freeing up additional disk space.

Your system is now free of LibreOffice and optimized for your needs.


## Installing pip and pip3

To install both pip and pip3, which are package managers for Python 2 and Python 3 respectively, run the following command:

```bash
sudo apt install python-pip python3-pip
```

This command will install pip for Python 2 and pip3 for Python 3 on your system.

You're all set with pip and pip3 installed and ready to manage Python packages!


## Installing Jetson Stats

To install Jetson Stats, a utility for monitoring and controlling NVIDIA Jetson devices, follow these steps:

{{< alert color="warning" >}}efore proceeding, ensure that you have pip3 installed on your system. If not, you can install it using `sudo apt install python3-pip`.{{< /alert >}}

```bash
sudo pip3 install -U jetson-stats
```

This command will install Jetson Stats and ensure that you have the latest version.

After installation, reboot your Jetson Nano to enable the `jtop` command:

```bash
sudo reboot now
```

Once your device has rebooted, reopen the terminal and type the following command to launch Jetson Stats:

```bash
jtop
```

This will open the Jetson Stats interface, allowing you to monitor various aspects of your Jetson Nano's performance.

You're now ready to utilize Jetson Stats for optimizing your Jetson Nano's performance!


## Configuring Jetson Fan to Start at Boot

To ensure your Jetson Nano's fans start automatically at boot, follow these steps:

1. Open and edit the `rc.local` file using the Nano text editor:

```bash
sudo nano /etc/rc.local
```

Paste the following lines into the file:

```sh
#!/bin/bash
sleep 10
sudo /usr/bin/jetson_clocks
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
exit 0
```

2. Next, create and edit the `rc-local.service` file:

```bash
sudo nano /etc/systemd/system/rc-local.service
```

Insert the following content:

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

3. Ensure the `rc.local` file has execute permissions:

```bash
sudo chmod +x /etc/rc.local
```

4. Now, enable the `rc-local` service to run on system boot:

```bash
sudo systemctl enable rc-local
```

5. Start the `rc-local` service:

```bash
sudo systemctl start rc-local.service
```

Your Jetson Nano's fans will now start automatically at boot, ensuring optimal cooling performance.





### Other

```bash
sudo nano /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
```

```sh
# SPDX-FileCopyrightText: Copyright (c) 2019-2021 NVIDIA CORPORATION & AFFILIATES. All rights reserved.
# SPDX-License-Identifier: LicenseRef-NvidiaProprietary
#
# NVIDIA CORPORATION, its affiliates and licensors retain all intellectual
# property and proprietary rights in and to this material, related
# documentation and any modifications thereto. Any use, reproduction,
# disclosure or distribution of this material and related documentation
# without an express license agreement from NVIDIA CORPORATION or
# its affiliates is strictly prohibited.

deb https://repo.download.nvidia.com/jetson/common r32.7 main
deb https://repo.download.nvidia.com/jetson/t210 r32.7 main
```



### IMX298 CAM Arducam

CSI Camera
```bash
sudo apt install libcanberra-gtk-module libcanberra-gtk3-module -y
```

pip tools needed
```bash
sudo pip3 install -U jetson-stats v4l2-fix
```


### BootfromUSB

```bash

LABEL primary
      MENU LABEL primary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} root=PARTUUID=b49df390-238c-4497-99a6-0643b9077530 rootwait rootfstype=ext4

LABEL secondary
      MENU LABEL secondary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} quiet root=/dev/mmcblk0p1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0



```

