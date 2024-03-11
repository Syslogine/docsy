---
title: "Power Management Configuration in Fedora Linux"
description: "Power management is an essential aspect of modern computing, especially for laptops and mobile devices, as it helps conserve battery life and reduce power consumption. Fedora Linux provides various tools and options to configure power management settings, allowing users to balance performance and battery life according to their needs. This tutorial will guide you through the process of configuring power management settings in Fedora Linux."
icon: "code"
draft: false
toc: true
weight: 1
---

## Understanding Power Management Components

Before diving into the configuration process, it's essential to understand the key components involved in power management:

1. **CPU Frequency Scaling**: This feature allows the system to dynamically adjust the CPU frequency based on the current workload, reducing power consumption when the system is idle or under low load.
2. **Display Power Management**: This includes settings for screen brightness, display sleep, and screen blanking, which help conserve battery life by reducing power consumption when the display is not in use.
3. **Disk and Device Power Management**: This feature allows the system to spin down hard disks and put devices into low-power modes when they are not in use, reducing overall power consumption.
4. **Battery Management**: This component monitors and reports the battery status, providing information about the remaining battery life and enabling battery-saving modes.

## Configuring Power Management Settings

Fedora Linux provides several graphical and command-line tools to configure power management settings. We'll cover both methods in this tutorial.

### Using the GNOME Power Manager (Graphical Interface)

The GNOME Power Manager is a graphical utility that allows you to configure various power management settings for your Fedora Linux system. To access the Power Manager, follow these steps:

1. Click on the "Activities" icon (the top-left corner of the desktop).
2. Search for "Power" and select "Power" from the search results.
3. The Power Manager window will open, providing access to various power management settings.

#### Display Settings

1. In the Power Manager window, click on the "Displays" section.
2. Here, you can adjust the screen brightness and configure display sleep and screen blanking settings.
3. Drag the "Brightness" slider to adjust the screen brightness according to your preference.
4. Set the "Turn off after" and "Blank after" values to specify the duration after which the screen will turn off or go blank when the system is idle.

#### Power Settings

1. In the Power Manager window, click on the "Power" section.
2. Here, you can configure power management settings for various power sources (battery and AC power).
3. Adjust the "Blank screen" and "Suspend" values to specify the duration after which the screen will go blank or the system will enter suspend mode when idle.
4. Enable or disable the "Automatic Suspend" and "Automatic Brightness" options according to your preferences.

#### Battery Settings

1. In the Power Manager window, click on the "Battery" section.
2. Here, you can view the current battery status and configure battery-related settings.
3. Enable or disable the "Battery Percentage" option to show or hide the battery percentage indicator in the top bar.
4. Adjust the "Critical Battery Action" setting to specify the action the system should take when the battery reaches a critical level.

### Using Command-Line Tools

Fedora Linux also provides command-line tools for configuring power management settings. These tools are particularly useful for server environments or situations where the graphical interface is not available.

#### TLP (Thermal, Linux Power)

TLP is a command-line utility that provides advanced power management features for Linux systems. It can optimize power consumption, CPU frequency scaling, disk spin-down, and more. To install TLP, run the following command:

```
sudo dnf install tlp tlp-rdw
```

After installation, TLP is enabled and starts automatically at system boot. You can configure TLP by editing the `/etc/tlp.conf` file. Here are some common settings you can adjust:

```
# CPU Frequency Scaling
CPU_SCALING_GOVERNOR_ON_BAT=powersave
CPU_MAX_PERF_ON_BAT=30

# Disk Power Management
DISK_IOSCHED=cfq
DISK_APM_LEVEL_ON_BAT=1

# Display Power Management
RADEON_POWER_PROFILE_ON_BAT=low
RADEON_DPM_STATE_ON_BAT=battery
RADEON_DPM_PERF_LEVEL_ON_BAT=auto

# Battery Management
START_CHARGE_THRESH_BAT0=75
STOP_CHARGE_THRESH_BAT0=80
```

After making changes to the configuration file, you can apply the new settings by running:

```
sudo tlp start
```

#### CPUFreq Utils

The `cpufreq-utils` package provides tools for configuring CPU frequency scaling. You can install it with the following command:

```
sudo dnf install kernel-tools
```

Once installed, you can use the `cpufreq-info` command to view the current CPU frequency scaling settings and the available governors:

```
cpufreq-info
```

To change the CPU frequency scaling governor, use the `cpufreq-set` command:

```
sudo cpufreq-set -g powersave
```

This command sets the CPU frequency scaling governor to "powersave" mode, which favors power efficiency over performance.

## Additional Tips and Best Practices

- Use power-saving modes when running on battery power to extend battery life.
- Adjust screen brightness and sleep settings according to your usage patterns.
- Disable unnecessary services and background processes to reduce power consumption.
- Keep your system up-to-date with the latest software and kernel updates, as they often include power management improvements.
- Consider using tools like PowerTOP or TLP to analyze and optimize power consumption on your system.

## Conclusion

Power management configuration is crucial for maximizing battery life and reducing power consumption on Fedora Linux systems, especially for laptops and mobile devices. By following this tutorial, you should now have a solid understanding of the various power management components and the tools available for configuring them. Remember to adjust the settings based on your specific needs and usage patterns to strike the right balance between performance and power efficiency.