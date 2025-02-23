---
title: "System Monitoring with systemd"
description: "In modern Linux distributions, systemd has become the de facto init system and service manager, replacing the traditional SysVinit. It not only manages system services but also provides a set of utilities for monitoring and analyzing system resources, services, and processes. This comprehensive tutorial will guide you through the various systemd utilities and commands that can be used for system monitoring on Fedora Linux."
icon: "code"
draft: false
toc: true
weight: 1
---

## Prerequisites

This tutorial assumes that you have a Fedora Linux system with systemd installed and configured. Additionally, you should have a basic understanding of the Linux command line and file system.

## Monitoring System Resources

systemd provides several utilities to monitor system resources, including CPU, memory, and disk usage.

### Monitoring CPU Usage

To monitor CPU usage, you can use the `systemd-cgtop` command, which displays a live view of the CPU usage for all running processes and services.

```
$ systemd-cgtop
```

This command provides a top-like interface, showing the CPU usage for each process or service, as well as the overall CPU usage for the system.

### Monitoring Memory Usage

To monitor memory usage, you can use the `systemd-cgtop` command with the `-m` or `--order=memory` option to sort the output by memory usage.

```
$ systemd-cgtop -m
```

Alternatively, you can use the `systemd-cgls` command to list all control groups (cgroups) and their memory usage.

```
$ systemd-cgls -m
```

This command shows the memory usage for each cgroup, including the total memory usage, as well as the usage of various memory types (e.g., RSS, cache, swap).

### Monitoring Disk Usage

To monitor disk usage, you can use the `systemd-cgtop` command with the `-d` or `--order=disk` option to sort the output by disk usage.

```
$ systemd-cgtop -d
```

This command displays the disk usage for each process or service, as well as the overall disk usage for the system.

## Monitoring System Services

systemd provides several utilities to monitor and manage system services.

### Listing Services

To list all available system services, you can use the `systemctl` command with the `list-unit-files` option.

```
$ systemctl list-unit-files
```

This command displays a list of all service units, along with their status (enabled or disabled).

### Checking Service Status

To check the status of a specific service, you can use the `systemctl` command with the `status` option, followed by the service name.

```
$ systemctl status <service_name>
```

For example, to check the status of the Apache web server service:

```
$ systemctl status httpd
```

This command displays detailed information about the service, including its current status (active, inactive, or failed), the process ID (PID), and any recent log entries.

### Starting, Stopping, and Restarting Services

You can use the `systemctl` command to start, stop, or restart a service.

- To start a service:

```
$ systemctl start <service_name>
```

- To stop a service:

```
$ systemctl stop <service_name>
```

- To restart a service:

```
$ systemctl restart <service_name>
```

### Enabling and Disabling Services

To ensure that a service starts automatically at system boot, you can enable it using the `systemctl` command with the `enable` option.

```
$ systemctl enable <service_name>
```

To disable a service and prevent it from starting automatically at boot, use the `disable` option.

```
$ systemctl disable <service_name>
```

## Monitoring Processes

In addition to monitoring system resources and services, systemd provides utilities for monitoring processes.

### Listing Running Processes

To list all running processes, you can use the `systemd-cgls` command with the `-p` or `--cgroup` option.

```
$ systemd-cgls -p
```

This command displays a list of all running processes, along with their respective cgroups and resource usage.

### Monitoring Process Resource Usage

To monitor the resource usage of a specific process, you can use the `systemd-cgtop` command with the `-a` or `--all` option to display all processes, or with the `-p` or `--print-pids` option to specify the process ID (PID) or name.

```
$ systemd-cgtop -a
$ systemd-cgtop -p <pid>
$ systemd-cgtop -p <process_name>
```

This command provides a live view of the resource usage for the specified process or processes, including CPU, memory, and disk usage.

## System Logging

systemd provides a powerful logging system called the Journal, which collects and manages log data from various system components, including services and processes.

### Viewing System Logs

To view the system logs, you can use the `journalctl` command.

```
$ journalctl
```

This command displays the entire log history, starting from the oldest entry.

You can use various options with `journalctl` to filter and format the log output. For example:

- To display the log entries for a specific service:

```
$ journalctl -u <service_name>
```

- To display the log entries for a specific process:

```
$ journalctl -p _PID=<pid>
```

- To display the log entries for a specific time range:

```
$ journalctl --since="YYYY-MM-DD HH:MM:SS" --until="YYYY-MM-DD HH:MM:SS"
```

- To display the log entries in a specific format (e.g., JSON, short, verbose):

```
$ journalctl -o <format>
```

### Clearing System Logs

In some cases, you may need to clear the system logs to free up disk space or for troubleshooting purposes.

To clear the system logs, you can use the `journalctl` command with the `--vacuum-size` option, followed by the desired size limit.

```
$ journalctl --vacuum-size=<size>
```

For example, to limit the log size to 100 MB:

```
$ journalctl --vacuum-size=100M
```

This command will remove the oldest log entries until the total log size is below the specified limit.

## Conclusion

systemd provides a comprehensive set of utilities for monitoring and managing system resources, services, processes, and logs on Fedora Linux. By leveraging these tools, you can gain valuable insights into your system's performance, troubleshoot issues, and optimize resource usage. This tutorial has covered the most essential systemd utilities for system monitoring, but there are many more advanced features and options available for exploration.