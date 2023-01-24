---
linktitle: OpenCV
title: OpenCV
tags: ["opencv","jetson","nano"]
description: >
 With few simple steps you can install/upgrade OpenCV 4.6 on your own jetson nano.
---

## Install OpenCV 4.6
By default on the jetson nano we have OpenCV 4.1.x installed and as i like to have everything up to date we also going to update this one.

### Step 01

1.	a fresh start, so check for updates
	```bash
	sudo apt update
	```
	```bash
	sudo apt upgrade
	```
2.	install nano
	```bash
	sudo apt install nano
	```
3.	install dphys-swapfile
	```bash
	sudo apt install dphys-swapfile -y
	```
4.	enlarge the boundary (4.5.2 and higher)
	```bash
	sudo nano /sbin/dphys-swapfile
	```
	1.	Find: `CONF_MAXSWAP=2048`
	2.	Replace: `CONF_MAXSWAP=6144`
5.	give the required memory size
	```bash
	sudo nano /etc/dphys-swapfile
	```
	1.	Find: `#CONF_SWAPSIZE=`
	2.	Replace: `CONF_SWAPSIZE=6144`
6.	reboot afterwards
	```bash
	sudo reboot
	```
*	See more about [GB to MB](https://www.gbmb.org/gb-to-mb)


### Step 02
1.	check your memory first
	```bash
	free -m
	```
2.	you need at least a total of 8.5 GB!
	if not, enlarge your swap space as explained in the guide
	```bash
	wget https://github.com/Qengineering/Install-OpenCV-Jetson-Nano/raw/main/OpenCV-4-6-0.sh
	```
	```bash
	sudo chmod 755 ./OpenCV-4-6-0.sh
	```
	```bash
	./OpenCV-4-6-0.sh
	```
3.	once the installation is done...
	```bash
	rm OpenCV-4-6-0.sh
	```
4.	remove the dphys-swapfile now
	```bash
	sudo /etc/init.d/dphys-swapfile stop
	```
	```bash
	sudo apt remove --purge dphys-swapfile
	```
5.	just a tip to save an additional 275 MB
	```bash
	sudo rm -rf ~/opencv
	```
	```bash
	sudo rm -rf ~/opencv_contrib
	```
6.	Let's reboot system..
	```bash
	sudo reboot now
	```

### extra
1.	only install if you want Qt5
	to beautify your OpenCV GUI
	```bash
	sudo apt-get install qt5-default
	```