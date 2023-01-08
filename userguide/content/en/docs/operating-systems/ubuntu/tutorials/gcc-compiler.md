---
linktitle: Install GCC Compiler
title: How to Install GCC Compiler on Ubuntu 18.04
tags: ['how to', 'install', 'GCC', 'Compiler', 'ubuntu', '18.04']
categories: ["Ubuntu"]
weight: 2
description: >
  Installing GCC Compiler on a Ubuntu machine with just two commands.
---


The GNU Compiler Collection (GCC) is a collection of compilers and libraries for C, C++, Objective-C, Fortran, Ada, Go , and D programming languages. Many open-source projects, including the GNU tools and the Linux kernel, are compiled with GCC.<br>
This tutorial covers the steps required to install the GCC compiler on Ubuntu 18.04. We will show you how to install the distro stable version and the latest version of GCC.
The same instructions apply for Ubuntu 16.04 and any Ubuntu-based distribution, including Kubuntu, Linux Mint and Elementary OS.
## Prerequisites
Te able to add new repositories and install packages on your Ubuntu system, you must be logged in as root or user with sudo privileges .
## Installing GCC on Ubuntu
The default Ubuntu repositories contain a meta-package named build-essential that contains the GCC compiler and a lot of libraries and other utilities required for compiling software.

Perform the steps below to install the GCC Compiler Ubuntu 18.04:
*	Start by updating the packages list:
	```bash
	sudo apt update
	```
*	Install the build-essential package by typing:
	```bash
	sudo apt install build-essential
	```
	The command installs a bunch of new packages including gcc, g++ and make.
*	To validate that the GCC compiler is successfully installed, use the `gcc --version` command which prints the GCC version:
	```bash
	gcc --version
	```