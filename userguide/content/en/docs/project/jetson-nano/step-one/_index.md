---
title: "step one"
description: ""
weight: 1
---


### Required Items

-	Nvidia Jeton Nano
-	MicroSD card
-	Nocuafan
-	Powersupply 5w
-	Keyboard/mouse
-	Internet cable
-	External SSD or M2 harddrive
-	WiFi



NOTE: This will eb the simpel version as i will make an other guide how to update the iso with new kernel without breaking stuff. It has been a while that Nvidia has been updating there Jetson Nano iso.

## Setting up the MicroSD with Ubuntu using balenaEther

1.	Go to this [website](https://developer.nvidia.com/embedded/downloads#?tx=$product,jetson_nano)
2.	Find and download `Jetson Nano Developer Kit SD Card Image`
3.	Download and install [balenaEtcher](https://etcher.balena.io/)
4.	Open `balenaEthcer` 
	1.	Select: `Flash from file`
	2.	Select: `jetson-nano-jp461-sd-card-image.zip`
	3.	Select the MicroSD card 
	4.	Flash!
5.	Place the MicroSD back into the jetson nano and start.


## Setting up Ubuntu on Jetson Nano

1.	Powerup the Jetson Nano and let the device bootup fully
2.	



## Make Jetson Nano ready

```bash
sudo systemctl enable ssh
```

```bash
sudo reboot now
```


check what versions we have
```bash
docker --version
python --version
python3 --version
git --version
```


Login with 
```bash
sudo apt update && sudo apt upgrade
```


```bash
git clone https://github.com/jetsonhacksnano/bootFromUSB
```

```bash
cd bootFromUSB
```

```bash
./copyRootToUSB.sh -p /dev/sda1
```




# Jetson Nano with CrewAI, Claude and OpenAI

Yes you read this right im gonna build an nice system with the jetson nano that use ai and camera 

* Face Reconiziion
* Speeche Reconigzion 





## Items
*	[Samsung EVO microSDXC 64GB](https://www.samsung.com/us/computing/memory-storage/memory-cards/evo-plus-adapter-microsdxc-64gb-mb-mc64sa-am/)
*	[Noctua NF-A4x20 5V PWM](https://noctua.at/en/nf-a4x20-5v-pwm)
*	[Wall power supply](https://www.adafruit.com/product/1466)



## useful links
*	https://repo.download.nvidia.com/jetson/
*	https://google.com
*	https://www.arducam.com/faq/kernel-camera-driver/





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

