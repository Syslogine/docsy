---
title: "Network Configuration"
description: "In Fedora Linux, you can configure network settings using various methods, including graphical tools and command-line utilities. This tutorial will cover the different approaches to configuring wired and wireless connections, DNS settings, and network interfaces."
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction to Network Configuration

Network configuration in Fedora Linux involves setting up various network components, such as wired or wireless connections, IP addresses, DNS servers, and network interfaces. Fedora provides several tools and utilities to manage network settings, catering to both graphical and command-line preferences.

## Graphical Network Configuration

### GNOME Network Settings

Fedora's default desktop environment, GNOME, includes a graphical network settings tool that allows you to easily configure network connections.

1. Open the GNOME Settings by clicking on the "Settings" icon in the Activities overview or by pressing the `Super` (Windows) key and typing "Settings".
2. Navigate to the "Network" section.
3. Here, you can view and manage your available network connections, including wired and wireless networks.
4. To configure a wired connection, click on the "Wired" tab and select your wired connection from the list.
5. To configure a wireless connection, click on the "Wireless" tab and select your desired wireless network from the list.
6. After selecting a network connection, you can configure various settings, such as the IPv4 or IPv6 method (automatic or manual), DNS servers, and other advanced options.

### NetworkManager TUI

In addition to the graphical tool, Fedora also provides a text-based user interface (TUI) for NetworkManager, which allows you to configure network settings from the command line.

1. Open a terminal window.
2. Run the command `nmtui` to launch the NetworkManager TUI.
3. Use the arrow keys and `Enter` key to navigate through the various options and configure your network connections.

## Command-Line Network Configuration

For more advanced or scripted network configuration, Fedora provides several command-line utilities.

### NetworkManager Command-Line Tool

NetworkManager is the default network management tool in Fedora. You can use the `nmcli` command-line tool to manage network connections and settings.

#### Configuring Wired Connection

1. Open a terminal window.
2. To list available wired connections, run `nmcli device status`.
3. To connect to a wired connection, run `nmcli connection up <connection-name>`, replacing `<connection-name>` with the name of your wired connection.
4. To modify the connection settings, run `nmcli connection modify <connection-name> <setting>.<property> <value>`, replacing `<connection-name>`, `<setting>`, `<property>`, and `<value>` with the appropriate values for your connection.

#### Configuring Wireless Connection

1. Open a terminal window.
2. To list available wireless networks, run `nmcli device wifi list`.
3. To connect to a wireless network, run `nmcli device wifi connect <ssid> password <password>`, replacing `<ssid>` with the name of the wireless network and `<password>` with the network password (if required).
4. To modify the wireless connection settings, use the `nmcli connection modify` command, as described in the wired connection section.

#### Configuring DNS Settings

1. Open a terminal window.
2. To view the current DNS settings, run `nmcli connection show <connection-name>`.
3. To modify the DNS settings, run `nmcli connection modify <connection-name> ipv4.dns "<dns1>,<dns2>"` or `nmcli connection modify <connection-name> ipv6.dns "<dns1>,<dns2>"`, replacing `<connection-name>`, `<dns1>`, and `<dns2>` with the appropriate values.

#### Managing Network Interfaces

1. Open a terminal window.
2. To list all available network interfaces, run `ip link show`.
3. To bring an interface up or down, run `ip link set <interface-name> up` or `ip link set <interface-name> down`, replacing `<interface-name>` with the name of the network interface.
4. To configure an IP address for an interface, run `ip addr add <ip-address>/<prefix-length> dev <interface-name>`, replacing `<ip-address>`, `<prefix-length>`, and `<interface-name>` with the appropriate values.

## Advanced Network Configuration

Fedora provides additional tools and utilities for more advanced network configuration scenarios, such as static IP address configuration, network bonding, network bridging, and virtual private network (VPN) setup.

### Static IP Address Configuration

If you need to configure a static IP address instead of using DHCP, you can use the `nmcli` command or modify the network configuration files directly.

1. Open a terminal window.
2. To configure a static IP address using `nmcli`, run `nmcli connection modify <connection-name> ipv4.method manual ipv4.addresses "<ip-address>/<prefix-length> <gateway>" ipv4.dns "<dns1>,<dns2>"`, replacing the placeholders with the appropriate values.
3. Alternatively, you can modify the network configuration files located in `/etc/sysconfig/network-scripts/` or `/etc/NetworkManager/system-connections/`.

### Network Bonding

Network bonding is a technique used to combine multiple network interfaces into a single logical interface, providing redundancy and increased throughput.

1. Install the required package: `sudo dnf install network-scripts-gre`
2. Create a bond configuration file in `/etc/sysconfig/network-scripts/`, such as `ifcfg-bond0`.
3. Configure the bond settings, such as the bonding mode, interfaces to be bonded, and IP address.
4. Restart the network service: `sudo systemctl restart network`

### Network Bridging

Network bridging is used to combine multiple network interfaces into a single virtual network, allowing communication between different network segments.

1. Install the required package: `sudo dnf install bridge-utils`
2. Create a bridge configuration file in `/etc/sysconfig/network-scripts/`, such as `ifcfg-br0`.
3. Configure the bridge settings, such as the interfaces to be bridged and IP address.
4. Restart the network service: `sudo systemctl restart network`

### Virtual Private Network (VPN)

Fedora supports various VPN protocols, including OpenVPN, IPsec, and more. You can use the NetworkManager GUI or command-line tools to configure and connect to VPN servers.

1. Open the GNOME Settings and navigate to the "Network" section.
2. Click on the "+" button in the VPN section and select the desired VPN protocol.
3. Enter the VPN server details, such as the server address, username, and password.
4. Save the VPN connection and connect to the VPN server.

Alternatively, you can use the `nmcli` command-line tool to configure and manage VPN connections.

## Troubleshooting Network Issues

If you encounter network issues in Fedora, you can use various tools and utilities to troubleshoot and diagnose the problem.

1. Use the `ping` command to test network connectivity: `ping <destination-address>`.
2. Use the `traceroute` command to trace the network path to a destination: `traceroute <destination-address>`.
3. Analyze network traffic using tools like `tcpdump` or `wireshark