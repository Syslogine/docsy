---
title: Debian Installation Guide
#linktitle: Installation Guide
categories: ["operating systems"]
tags: ["debian", "installation"]
weight: 1
description: >
  A step-by-step guide to installing Debian, a robust and versatile operating system.
---

# Debian Installation Guide

This guide will walk you through the steps to install Debian, a popular choice for both servers and desktops due to its stability and flexibility.

## Before You Begin

Before starting the installation process, ensure you have the following:

- A computer or virtual machine on which to install Debian.
- An internet connection for downloading the Debian ISO and updates.
- A USB flash drive (at least 4GB) or a blank DVD for the installation media.

## Step 1: Download Debian ISO

1. Visit the official Debian download page: [Debian Downloads](https://www.debian.org/download)
2. Choose the Debian version that suits your needs. For most users, the "stable" version is recommended.
3. Select the ISO image according to your system's architecture (most modern computers use `amd64`).
4. Download the ISO file to your computer.

## Step 2: Create Installation Media

### USB Flash Drive:

1. Insert your USB flash drive.
2. Use a tool like `balenaEtcher` (available for Windows, macOS, and Linux) to write the ISO image to the USB drive.
   - Download `balenaEtcher` from [https://www.balena.io/etcher/](https://www.balena.io/etcher/).
   - Open `balenaEtcher`, select the downloaded ISO file, and choose your USB drive as the target.
   - Click "Flash!" to start the process.

### DVD:

1. Insert a blank DVD into your DVD writer.
2. Use your operating system's built-in tool or a third-party application to burn the ISO image to the DVD.

## Step 3: Boot from Installation Media

1. Insert the USB drive or DVD into the computer where you want to install Debian.
2. Reboot the computer and enter the boot menu or BIOS setup (this usually involves pressing a key like F12, F2, or Del during boot-up).
3. Select the USB drive or DVD as the boot device.

## Step 4: Install Debian

1. Once booted from the installation media, you'll be presented with the Debian Installer menu.
2. Select "Graphical Install" for a user-friendly installation process.
3. Follow the on-screen instructions to:
   - Select your language, location, and keyboard layout.
   - Set up network settings (if available).
   - Partition your disk (for beginners, the guided partitioning option is recommended).
   - Enter user and password details.
   - Choose software packages to install (the "Debian desktop environment" and "standard system utilities" are selected by default).
4. Once the installation is complete, remove the installation media and reboot your computer.

## Step 5: First Boot and Update

1. On the first boot, log in with the username and password you created during the installation.
2. Open a terminal and run the following commands to update your system:

```shell
sudo apt update
sudo apt upgrade
```

Congratulations! You have successfully installed Debian. From here, you can explore Debian and customize your installation with additional software and settings.