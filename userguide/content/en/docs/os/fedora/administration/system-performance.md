---
title: "System Performance Tuning"
description: "Fedora Linux is a powerful and versatile operating system that can be used for a wide range of tasks, from personal computing to enterprise server solutions. However, like any other operating system, Fedora's performance can be affected by various factors such as hardware resources, software configuration, and system load. In this tutorial, we'll explore several techniques and tools to help you optimize your Fedora system's performance and ensure that it runs smoothly and efficiently." 
icon: "code"
draft: false
toc: true
weight: 1
---

## Introduction

System performance tuning is the process of adjusting various system components and configurations to optimize the overall performance of your computer. This process can involve tweaking settings related to disk usage, memory management, CPU usage, and networking, among others.

It's important to note that performance tuning is a complex topic, and the techniques discussed in this tutorial may not be suitable for all systems or use cases. It's recommended to thoroughly understand the implications of each change and to perform thorough testing before implementing any changes in a production environment.

## Disk Usage Optimization

Disk performance plays a crucial role in overall system performance, as it affects file access times and data transfer rates. Here are some techniques to optimize disk usage on your Fedora system.

### Monitoring Disk Usage

Before attempting any disk optimization, it's essential to understand your system's current disk usage patterns. You can use the following tools to monitor disk usage:

- `df` (Disk Free): This command displays the amount of available disk space on mounted file systems.
- `du` (Disk Usage): This command shows the disk usage of files and directories.
- `iotop`: This tool displays real-time disk I/O statistics and can help identify processes that are causing high disk activity.

```bash
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/nvme0n1p3   50G   12G   36G  25% /
/dev/nvme0n1p1  976M  280M  637M  31% /boot

$ du -sh /var/log
1.2G    /var/log
```

### Identifying and Removing Unnecessary Files

Over time, your system can accumulate unnecessary files, such as old log files, temporary files, and package caches. Removing these files can free up disk space and potentially improve performance. However, be cautious when deleting system files, as it may cause issues if done incorrectly.

You can use the following commands to identify and remove unnecessary files:

```bash
# Clear package cache
sudo dnf clean all

# Remove old kernel versions (keep the current and one previous version)
sudo package-cleanup --oldkernels --count=2 --verbose

# Remove old log files
sudo journalctl --vacuum-size=500M
```

### Enabling Disk Caching

Disk caching can significantly improve read and write performance by storing frequently accessed data in memory. On Fedora, you can enable disk caching using the `vm.vfs_cache_pressure` kernel parameter.

To adjust the `vm.vfs_cache_pressure` value, open the `/etc/sysctl.conf` file and add the following line:

```
vm.vfs_cache_pressure=50
```

This sets the cache pressure to 50, which means the kernel will cache more data in memory. Higher values (up to 100) increase the cache size, potentially improving performance but also consuming more memory.

After making the change, run the following command to apply the new setting:

```bash
sudo sysctl -p
```

### Optimizing File System

The choice of file system can also affect disk performance. Fedora uses the XFS file system by default, which is generally considered a high-performance and scalable file system. However, in some cases, you may want to consider using alternative file systems like ext4 or btrfs, depending on your specific needs and workloads.

To check the file system type of a mounted partition, use the `df -T` command:

```bash
$ df -T
Filesystem     Type 1K-blocks   Used Available Use% Mounted on
/dev/nvme0n1p3 xfs   51475204 9212592 42262612  18% /
```

If you decide to change the file system, you'll need to back up your data, create a new partition with the desired file system, and restore the data. This process can be complex and should be carefully planned and executed.

## Memory Management

Effective memory management is crucial for overall system performance, as it affects the responsiveness of applications and the ability to handle multiple tasks simultaneously.

### Monitoring Memory Usage

Before optimizing memory usage, it's essential to understand how your system is currently utilizing memory. You can use the following tools to monitor memory usage:

- `free`: This command displays the total amount of free and used memory in the system.
- `vmstat`: This tool provides detailed information about memory usage, including virtual memory statistics.
- `top` or `htop`: These interactive process viewers show the memory usage of running processes, allowing you to identify memory-intensive applications.

```bash
$ free -h
              total        used        free      shared  buff/cache   available
Mem:           7.8G        1.2G        5.6G        9.0M        1.0G        6.3G
Swap:          2.0G          0B        2.0G
```

### Adjusting Swappiness

The Linux kernel uses a "swappiness" value to determine how aggressively it should swap out inactive processes from memory to disk. A higher swappiness value means the kernel will swap more aggressively, while a lower value means the kernel will try to keep more processes in memory.

In most cases, the default swappiness value of 60 works well. However, if you have a system with a lot of available RAM and want to minimize disk swapping, you can lower the swappiness value. On the other hand, if you have a system with limited RAM and want to free up memory more aggressively, you can increase the swappiness value.

To adjust the swappiness value, open the `/etc/sysctl.conf` file and add the following line:

```
vm.swappiness=10
```

This sets the swappiness value to 10, which is a relatively low value that will minimize disk swapping. After making the change, run the following command to apply the new setting:

```bash
sudo sysctl -p
```

### Enabling Zram

Zram (Compressed RAM) is a kernel module that creates a compressed block device in memory, which can be used as a swap device or a compressed cache for certain workloads. Enabling Zram can improve system performance by reducing disk swapping and improving responsiveness, especially on systems with limited RAM.

To enable Zram on Fedora, follow these steps:

1. Install the required packages:

   ```bash
   sudo dnf install zram-generator
   ```

2. Enable and start the `zram-generator` service:

   ```bash
   sudo systemctl enable --now zram-generator
   ```

3. Verify that the Zram device is active:

   ```bash
   $ cat /proc/swaps
   Filename                Type        Size        Used        Priority
   /dev/zram0              partition   2097148     0           5
   ```

By default, Zram will allocate up to 50% of your system's RAM for the compressed block device. If you need to adjust this value, you