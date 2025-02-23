---
title: "Firewall Configuration"
description: "Firewalls are essential security tools that help protect your system from unauthorized access and potential threats. In Fedora Linux, you have two main options for configuring the firewall: `firewalld` and `iptables`. This tutorial will guide you through the process of configuring the firewall using both methods."
icon: "code"
draft: false
toc: true
weight: 1
---

## Part 1: Configuring the Firewall with firewalld

Fedora Linux uses `firewalld` as the default firewall management tool. It provides a user-friendly interface for managing firewall rules and zones.

### 1.1 Checking the firewalld Status

Before you begin, ensure that `firewalld` is installed and running. You can check its status with the following command:

```
sudo systemctl status firewalld
```

If `firewalld` is not running, you can start it with:

```
sudo systemctl start firewalld
```

### 1.2 Understanding Zones

`firewalld` uses the concept of zones to manage firewall rules. Each zone represents a set of rules that apply to network interfaces. The default zone is the `public` zone, which is used for incoming connections that are not trusted.

To list all available zones, run:

```
sudo firewall-cmd --get-zones
```

### 1.3 Configuring Firewall Rules

You can configure firewall rules using the `firewall-cmd` command. Here are some common operations:

- Opening a port for a specific service:

```
sudo firewall-cmd --zone=public --add-service=http --permanent
```

This command opens port 80 (HTTP) in the `public` zone. The `--permanent` option makes the change persistent across reboots.

- Opening a specific port:

```
sudo firewall-cmd --zone=public --add-port=8080/tcp --permanent
```

This command opens port 8080 for TCP traffic in the `public` zone.

- Removing a service or port:

```
sudo firewall-cmd --zone=public --remove-service=http --permanent
sudo firewall-cmd --zone=public --remove-port=8080/tcp --permanent
```

- Listing all allowed services and ports:

```
sudo firewall-cmd --zone=public --list-services
sudo firewall-cmd --zone=public --list-ports
```

- Reloading the firewall rules:

```
sudo firewall-cmd --reload
```

After making changes, you must reload the firewall rules for them to take effect.

### 1.4 Configuring Firewall Zones

You can also change the zone for a specific network interface. For example, to change the zone for the `enp0s3` interface to the `trusted` zone, run:

```
sudo firewall-cmd --zone=trusted --change-interface=enp0s3 --permanent
```

### 1.5 Rich Rules

`firewalld` supports rich rules, which allow you to create more complex firewall rules based on various criteria, such as source and destination IP addresses, ports, and protocols. Rich rules are specified using a syntax similar to `iptables` rules.

To add a rich rule, use the `--add-rich-rule` option:

```
sudo firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.0/24" port port=22 protocol=tcp accept' --permanent
```

This rule allows incoming SSH connections from the 192.168.1.0/24 network on the `public` zone.

## Part 2: Configuring the Firewall with iptables

`iptables` is a low-level firewall management tool that provides granular control over network packet filtering. While `firewalld` is the recommended tool for Fedora Linux, some advanced users may prefer to use `iptables` directly.

### 2.1 Installing iptables

`iptables` is typically installed by default on Fedora Linux. If it's not installed, you can install it with:

```
sudo dnf install iptables-services
```

### 2.2 Understanding iptables Chains

`iptables` uses chains to organize firewall rules. The three built-in chains are:

- `INPUT`: Handles incoming packets.
- `OUTPUT`: Handles outgoing packets.
- `FORWARD`: Handles packets being routed through the system.

### 2.3 Configuring iptables Rules

You can configure `iptables` rules using the `iptables` command. Here are some common operations:

- Opening a port for a specific service:

```
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT
```

This command allows incoming TCP traffic on port 80 (HTTP).

- Blocking a specific IP address:

```
sudo iptables -A INPUT -s 192.168.1.100 -j DROP
```

This command drops all incoming packets from the IP address 192.168.1.100.

- Saving and restoring rules:

```
sudo iptables-save > /path/to/rules.v4
sudo iptables-restore < /path/to/rules.v4
```

`iptables` rules are not persistent across reboots. You can save and restore them using the `iptables-save` and `iptables-restore` commands.

### 2.4 Advanced iptables Rules

`iptables` supports advanced rule matching based on various criteria, such as source and destination IP addresses, ports, protocols, and packet states. Here's an example of a more complex rule:

```
sudo iptables -A INPUT -p tcp --dport 22 -m state --state NEW,ESTABLISHED -j ACCEPT
sudo iptables -A OUTPUT -p tcp --sport 22 -m state --state ESTABLISHED -j ACCEPT
```

These rules allow incoming and outgoing SSH connections while maintaining stateful tracking of the connections.

### 2.5 Flushing iptables Rules

To remove all existing `iptables` rules and start with a clean slate, use the following command:

```
sudo iptables -F
```

This command flushes all chains and removes all rules.

## Conclusion

Configuring the firewall is an essential task for securing your Fedora Linux system. This tutorial covered the two main methods for firewall configuration: `firewalld` and `iptables`. While `firewalld` is the recommended tool for most users, `iptables` provides more advanced options for experienced administrators.

Remember to carefully consider your security requirements and test your firewall rules to ensure that they are working as intended. Regular monitoring and maintenance of your firewall configuration are also recommended to keep your system secure.