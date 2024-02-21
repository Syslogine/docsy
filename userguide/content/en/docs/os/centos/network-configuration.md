---
title: "CentOS Network Configuration"
linkTitle: "Network Configuration"
description: "Learn how to configure network settings on CentOS, including setting up static IP addresses, managing network interfaces, and troubleshooting common network issues."
date: 2023-02-21
weight: 2
---

# CentOS Network Configuration

Configuring network settings is crucial for ensuring your CentOS system can communicate with other devices on your network and the internet. This guide covers the basics of network configuration on CentOS, including static IP address assignment, DNS configuration, and troubleshooting.

## Understanding Network Interfaces

Before configuring your network, identify the network interfaces available on your system with:

```bash
nmcli device status
```

This command lists network devices and their status, helping you determine which interface(s) to configure.

## Setting a Static IP Address

CentOS uses NetworkManager and the `nmcli` tool for network configuration. To set a static IP address for an interface, follow these steps:

1. **Disable DHCP on the Interface**:
   ```bash
   nmcli con mod [interface-name] ipv4.method manual
   ```

2. **Assign the Static IP Address**:
   ```bash
   nmcli con mod [interface-name] ipv4.addresses [your-static-ip]/24
   ```

3. **Set the Default Gateway**:
   ```bash
   nmcli con mod [interface-name] ipv4.gateway [gateway-ip]
   ```

4. **Specify DNS Servers**:
   ```bash
   nmcli con mod [interface-name] ipv4.dns "[DNS1],[DNS2]"
   ```

5. **Restart NetworkManager** to apply the changes:
   ```bash
   systemctl restart NetworkManager
   ```

Replace `[interface-name]`, `[your-static-ip]`, `[gateway-ip]`, `[DNS1]`, and `[DNS2]` with your actual network interface name, desired IP address, gateway, and DNS servers.

## Configuring DNS

Edit `/etc/resolv.conf` to set your DNS servers manually:

```bash
nameserver [DNS1]
nameserver [DNS2]
```

This file may be managed by NetworkManager. If you're using static IP configuration as described above, setting DNS via `nmcli` is preferred.

## Troubleshooting Network Issues

If you encounter network connectivity issues:

- Ensure your network cable is properly connected and your router or switch is operational.
- Check your network configuration with `nmcli con show [interface-name]` and verify the settings.
- Test connectivity to your gateway and external addresses using `ping`.
- Review system logs with `journalctl -u NetworkManager` for any NetworkManager-related errors.

## Advanced Configuration

For more complex network setups, such as bonding, bridging, or VLAN tagging, refer to the [official CentOS documentation](https://www.centos.org/docs/). These scenarios often require additional configuration steps and understanding of network principles.

By following this guide, you should now have a basic understanding of how to configure network settings on your CentOS system. Remember, network configuration can vary widely based on your specific environment and requirements, so always tailor these instructions to fit your situation.