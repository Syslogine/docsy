---
title: "Jetson Nano Setup Guide"
description: "A comprehensive guide to setting up your Jetson Nano."
weight: 1
---

## Introduction

Welcome to the Jetson Nano Setup Guide! This guide will walk you through the process of setting up your Jetson Nano developer kit, from downloading the system image to configuring advanced usage scenarios.

## Download Jetson Nano Image 

Before you begin, you'll need to download the system image for your Jetson Nano model:

- [Jetson Nano 2GB](https://developer.nvidia.com/embedded/l4t/r32_release_v7.1/jp_4.6.1_b110_sd_card/jetson_nano_2gb/jetson-nano-2gb-jp461-sd-card-image.zip)
- [Jetson Nano 4GB](https://developer.nvidia.com/embedded/l4t/r32_release_v7.1/jp_4.6.1_b110_sd_card/jetson_nano/jetson-nano-jp461-sd-card-image.zip)

## Fresh Install Setup Guide for Jetson Nano

Once your Jetson Nano board is up and running with Ubuntu Desktop, let's kickstart the setup process by opening the terminal and following these steps:

### Step 1: Update System

First, let's ensure your system is up to date:

```bash
sudo apt update -y
```

Next, upgrade your Jetson Nano:

```bash
sudo apt upgrade -y
```

During the upgrade process, you may encounter prompts for configuration files.

Select `Y` to install the package maintainer's version. 

```sh
Configuration file '/etc/ld.so.conf.d/nvidia-tegra.conf'
 ==> Modified (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** nvidia-tegra.conf (Y/I/N/O/D/Z) [default=N] ? Y
```

Again select `Y` to install the package maintainer's version. 

```sh
Configuration file '/etc/systemd/nv-oem-config-post.sh'
 ==> Deleted (by you or by a script) since installation.
 ==> Package distributor has shipped an updated version.
   What would you like to do about it ?  Your options are:
    Y or I  : install the package maintainer's version
    N or O  : keep your currently-installed version
      D     : show the differences between the versions
      Z     : start a shell to examine the situation
 The default action is to keep your current version.
*** nv-oem-config-post.sh (Y/I/N/O/D/Z) [default=N] ? Y
```

Additionally, if prompted to restart Docker, select `YES`.

Now, let's perform a distribution upgrade:

```bash
sudo apt dist-upgrade -y
```

### Step 2: Clean Up

Once the upgrade process is complete, let's tidy up by removing old packages:

```bash
sudo apt autoremove -y
```

And finally, let's clean up the cache:

```bash
sudo apt clean
```

### Step 3: Reboot

After these maintenance tasks, it's recommended to reboot your Jetson Nano for changes to take effect:

```bash
sudo reboot now
```


## Install Useful Tools

Here are some essential tools that are handy for almost every project:

```bash
sudo apt install git nano curl wget -y
```


## Uninstall LibreOffice

If you no longer need LibreOffice and want to reclaim some disk space, follow these steps to remove it:

```bash
sudo apt autoremove libreoffice* -y
```

This command will uninstall all LibreOffice packages from your system.

After removing LibreOffice, let's clean up the residual files:

```bash
sudo apt clean
```

This command will clean the package cache, freeing up additional disk space.

Your system is now free of LibreOffice and optimized for your needs.


## Installing pip and pip3

To install both pip and pip3, which are package managers for Python 2 and Python 3 respectively, run the following command:

```bash
sudo apt install python-pip python3-pip
```

This command will install pip for Python 2 and pip3 for Python 3 on your system.

You're all set with pip and pip3 installed and ready to manage Python packages!


## Installing Jetson Stats

To install Jetson Stats, a utility for monitoring and controlling NVIDIA Jetson devices, follow these steps:

{{< alert color="warning" title="Warning" >}}Before proceeding, ensure that you have pip3 installed on your system. If not, you can install it using `sudo apt install python3-pip`.{{< /alert >}}

```bash
sudo pip3 install -U jetson-stats
```

This command will install Jetson Stats and ensure that you have the latest version.

After installation, reboot your Jetson Nano to enable the `jtop` command:

```bash
sudo reboot now
```

Once your device has rebooted, reopen the terminal and type the following command to launch Jetson Stats:

```bash
jtop
```

This will open the Jetson Stats interface, allowing you to monitor various aspects of your Jetson Nano's performance.

You're now ready to utilize Jetson Stats for optimizing your Jetson Nano's performance!


## Configuring Jetson Fan to Start at Boot

To ensure your Jetson Nano's fans start automatically at boot, follow these steps:

1. Open and edit the `rc.local` file using the Nano text editor:

```bash
sudo nano /etc/rc.local
```

Paste the following lines into the file:

```sh
#!/bin/bash
sleep 10
sudo /usr/bin/jetson_clocks
sudo sh -c 'echo 255 > /sys/devices/pwm-fan/target_pwm'
exit 0
```

2. Next, create and edit the `rc-local.service` file:

```bash
sudo nano /etc/systemd/system/rc-local.service
```

Insert the following content:

```txt
[Unit]
Description=/etc/rc.local Compatibility
ConditionPathExists=/etc/rc.local

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
StandardOutput=tty
RemainAfterExit=yes
SysVStartPriority=99

[Install]
WantedBy=multi-user.target
```

3. Ensure the `rc.local` file has execute permissions:

```bash
sudo chmod +x /etc/rc.local
```

4. Now, enable the `rc-local` service to run on system boot:

```bash
sudo systemctl enable rc-local
```

5. Start the `rc-local` service:

```bash
sudo systemctl start rc-local.service
```

Your Jetson Nano's fans will now start automatically at boot, ensuring optimal cooling performance.



## Advanced Usage Examples

### 1. Machine Learning Frameworks

**Example**: Install and configure popular machine learning frameworks like TensorFlow, PyTorch, or MXNet to leverage the Jetson Nano's GPU for accelerated deep learning tasks.

**Guide**:
- Follow the official documentation or community tutorials for each framework to install the required dependencies and set up GPU support.
- Utilize pre-trained models or train custom models using datasets optimized for inference on edge devices.
- Explore optimizations such as TensorRT integration for improved inference performance on the Jetson Nano.

### 2. Dockerized Applications

**Example**: Containerize applications using Docker to simplify deployment and manage dependencies on the Jetson Nano.

**Guide**:
- Install Docker CE (Community Edition) on the Jetson Nano by following the official Docker documentation.
- Create Dockerfiles to define the application environment and dependencies.
- Build Docker images for your applications and run them in containers on the Jetson Nano.
- Explore Docker Compose for orchestrating multi-container applications or deploying services with dependencies.

### 3. IoT Integration

**Example**: Integrate the Jetson Nano into IoT (Internet of Things) projects for edge computing and sensor data processing.

**Guide**:
- Interface sensors or peripherals with the Jetson Nano using GPIO pins, I2C, SPI, or USB interfaces.
- Develop applications to collect, process, and transmit sensor data to cloud services or local IoT gateways.
- Implement edge AI algorithms for real-time analytics, anomaly detection, or predictive maintenance in IoT deployments.
- Explore MQTT (Message Queuing Telemetry Transport) or other IoT protocols for communication between devices and cloud services.

### 4. Computer Vision Applications

**Example**: Build computer vision applications using libraries like OpenCV or specialized frameworks for object detection, image recognition, or facial recognition.

**Guide**:
- Install OpenCV and other relevant libraries using package managers or by compiling from source.
- Experiment with pre-trained models for tasks like object detection (YOLO, SSD), image classification (ResNet, MobileNet), or semantic segmentation (DeepLab, Mask R-CNN).
- Capture and process video streams from cameras or video files for real-time analysis or surveillance applications.
- Explore techniques for optimizing computer vision algorithms for performance on resource-constrained devices like the Jetson Nano.

### 5. Robotics Projects

**Example**: Use the Jetson Nano as the brain of robotic systems for tasks such as autonomous navigation, object manipulation, or drone control.

**Guide**:
- Interface sensors, actuators, and motor controllers with the Jetson Nano to enable sensing and control capabilities.
- Develop control algorithms using frameworks like ROS (Robot Operating System) or libraries like Jetson.GPIO for GPIO control.
- Implement perception algorithms for environment mapping, obstacle detection, or localization using onboard sensors or external cameras.
- Integrate AI models for tasks like object detection, gesture recognition, or path planning to enable autonomous behavior in robotic systems.

These advanced usage examples demonstrate the versatility of the Jetson Nano for a wide range of applications beyond basic system setup and configuration.




## Troubleshooting

### 1. Network Connectivity Issues

**Problem**: Unable to connect to the internet or download packages during setup.

**Solution**: 
- Check the network connection by running `ping google.com`. If there is no response, ensure that the Jetson Nano is properly connected to the network and that the router or modem is functioning correctly.
- Verify network settings, including IP configuration and DNS servers, by running `ifconfig` and `cat /etc/resolv.conf`.
- If using Wi-Fi, ensure that the correct SSID and password are entered, and try restarting the network interface with `sudo systemctl restart networking`.

### 2. Package Installation Errors

**Problem**: Encounter errors while installing packages with `apt`.

**Solution**:
- Check for any typos in the package names or repository URLs.
- Ensure that the package repositories are configured correctly by inspecting `/etc/apt/sources.list` and files in `/etc/apt/sources.list.d/`.
- If encountering dependency issues, try running `sudo apt --fix-broken install` to resolve them automatically.

### 3. Hardware Compatibility Issues

**Problem**: Certain hardware components or peripherals are not recognized or functioning properly.

**Solution**:
- Verify that the hardware is compatible with the Jetson Nano by checking manufacturer specifications or community forums.
- Check for any firmware updates or driver installations required for the hardware to work with the Jetson Nano.
- Test the hardware on another device or platform to confirm functionality, if possible.

### 4. System Freezes or Crashes

**Problem**: The Jetson Nano freezes or crashes unexpectedly during operation.

**Solution**:
- Check system resource usage using tools like `top` or `htop` to identify any processes consuming excessive CPU or memory.
- Ensure that the power supply is adequate and stable, as insufficient power can cause system instability.
- Check system logs for error messages or warnings that might indicate the cause of the issue (`/var/log/syslog`, `/var/log/kern.log`, etc.).

### 5. Display or Graphics Issues

**Problem**: Encounter issues with the display output or graphics acceleration.

**Solution**:
- Verify that the display cable is securely connected to the Jetson Nano's HDMI or DisplayPort interface.
- Check display settings and resolution configuration using the system settings or `xrandr` command.
- Ensure that the appropriate NVIDIA drivers are installed and configured correctly for graphics acceleration.

If you encounter any other issues not covered here, feel free to seek assistance from the Jetson Nano community forums or NVIDIA support resources.

