---
title: "Network Configuration"
description: "Instructions for configuring network settings during the Debian installation, including wired and wireless connections, IP address assignment, and DNS settings."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

Configuring network settings during the Debian installation is essential for establishing network connectivity and accessing online resources. This tutorial provides step-by-step instructions for configuring wired and wireless connections, assigning IP addresses, and configuring DNS settings during the Debian installation process.

## Prerequisites

Before you begin, make sure you have:

- Booted into the Debian installer environment
- Access to a wired or wireless network connection

## Step 1: Launch the Installer

1. Boot your computer from the Debian installation media (USB drive, DVD, etc.).
2. Follow the on-screen prompts to access the Debian installer environment.

## Step 2: Access Network Configuration

1. Select "Configure the network" or a similar option from the Debian installer menu.
2. Choose the network interface (e.g., eth0 for wired connections, wlan0 for wireless connections) to configure.

## Step 3: Configure Wired Connection

1. Select the wired network interface (e.g., eth0) from the list of available interfaces.
2. Choose the option to configure the interface using DHCP (Dynamic Host Configuration Protocol) if your network uses DHCP.
3. If DHCP is not available, choose the option to manually configure the interface and enter the IP address, subnet mask, gateway, and DNS server information provided by your network administrator.

## Step 4: Configure Wireless Connection

1. Select the wireless network interface (e.g., wlan0) from the list of available interfaces.
2. Choose the option to scan for wireless networks and select your network from the list.
3. Enter the security key or passphrase for your wireless network if prompted.
4. Choose the option to configure the interface using DHCP or manually configure the interface as described in Step 3.

## Step 5: Verify Network Configuration

1. Review the network settings to ensure they are configured correctly.
2. Test the network connection by pinging a known IP address or domain name (e.g., `ping google.com`).
3. Verify that you can access online resources and proceed with the installation process.

## Conclusion

By following these steps, you can successfully configure network settings during the Debian installation process. Establishing network connectivity is crucial for accessing online resources, downloading updates, and completing the Debian installation.
