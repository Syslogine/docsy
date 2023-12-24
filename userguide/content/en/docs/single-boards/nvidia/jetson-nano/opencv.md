---
linktitle: OpenCV
title: Upgrade OpenCV to Version 4.6 on Nvidia Jetson Nano
tags: ["opencv","jetson","nano"]
description: >
 With few simple steps you can install/upgrade OpenCV 4.6 on your own jetson nano.
---

By default, the Nvidia Jetson Nano comes with OpenCV 4.1.x pre-installed. This guide will help you upgrade to OpenCV 4.6 for the latest features and improvements.

## **Step 1: Preparing the System**

### **1. Start with a Fresh Update**
```bash
sudo apt update
sudo apt upgrade
```
Ensures your system is up-to-date.

### **2. Install Nano and dphys-swapfile**
```bash
sudo apt install nano
sudo apt install dphys-swapfile -y
```
Installs the Nano text editor and the swap file manager.

### **3. Enlarge Swap Boundary**
```bash
sudo nano /sbin/dphys-swapfile
```
Find `CONF_MAXSWAP=2048` and replace it with `CONF_MAXSWAP=6144`. Save the changes.

### **4. Set Swap Size**
```bash
sudo nano /etc/dphys-swapfile
```
Find `#CONF_SWAPSIZE=` and replace it with `CONF_SWAPSIZE=6144`. Save the changes.

### **5. Reboot System**
```bash
sudo reboot
```
Reboots the system to apply changes.

## **Step 2: OpenCV 4.6 Installation**

### **1. Check Available Memory**
```bash
free -m
```
Ensures you have a total of at least 8.5 GB available.

### **2. Download and Install OpenCV 4.6 Script**
```bash
wget https://github.com/Qengineering/Install-OpenCV-Jetson-Nano/raw/main/OpenCV-4-6-0.sh
sudo chmod 755 ./OpenCV-4-6-0.sh
./OpenCV-4-6-0.sh
```
Downloads and runs the script for OpenCV 4.6 installation.

### **3. Post-Installation Cleanup**
```bash
rm OpenCV-4-6-0.sh
sudo /etc/init.d/dphys-swapfile stop
sudo apt remove --purge dphys-swapfile
```
Cleans up installation files and removes the dphys-swapfile.

### **4. Additional Tips**
```bash
sudo rm -rf ~/opencv
sudo rm -rf ~/opencv_contrib
```
Saves an additional 275 MB by removing unnecessary files.

### **5. Reboot System**
```bash
sudo reboot now
```
Ensures all changes take effect.

## **Extra: Install Qt5 (Optional)**
Only install if you want Qt5 to beautify your OpenCV GUI.
```bash
sudo apt-get install qt5-default
```