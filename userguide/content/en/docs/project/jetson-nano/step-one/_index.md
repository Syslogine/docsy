---
title: "step one"
description: ""
weight: 1
---


### Required Items

-	Nvidia Jeton Nano
-	MicroSD card
-	Nocuafan
-	Powersupply 5w
-	Keyboard/mouse
-	Internet cable
-	External SSD or M2 harddrive
-	WiFi



NOTE: This will eb the simpel version as i will make an other guide how to update the iso with new kernel without breaking stuff. It has been a while that Nvidia has been updating there Jetson Nano iso.

## Setting up the MicroSD with Ubuntu using balenaEther

1.	Go to this [website](https://developer.nvidia.com/embedded/downloads#?tx=$product,jetson_nano)
2.	Find and download `Jetson Nano Developer Kit SD Card Image`
3.	Download and install [balenaEtcher](https://etcher.balena.io/)
4.	Open `balenaEthcer` 
	1.	Select: `Flash from file`
	2.	Select: `jetson-nano-jp461-sd-card-image.zip`
	3.	Select the MicroSD card 
	4.	Flash!
5.	Place the MicroSD back into the jetson nano and start.


## Setting up Ubuntu on Jetson Nano

1.	Powerup the Jetson Nano and let the device bootup fully
2.	



## Make Jetson Nano ready

```bash
sudo systemctl enable ssh
```

```bash
sudo reboot now
```


check what versions we have
```bash
docker --version
python --version
python3 --version
git --version
```


Login with 
```bash
sudo apt update && sudo apt upgrade
```


```bash
git clone https://github.com/jetsonhacksnano/bootFromUSB
```

```bash
cd bootFromUSB
```

```bash
./copyRootToUSB.sh -p /dev/sda1
```




# Jetson Nano with CrewAI, Claude and OpenAI

Yes you read this right im gonna build an nice system with the jetson nano that use ai and camera 

* Face Reconiziion
* Speeche Reconigzion 





## Items
*	[Samsung EVO microSDXC 64GB](https://www.samsung.com/us/computing/memory-storage/memory-cards/evo-plus-adapter-microsdxc-64gb-mb-mc64sa-am/)
*	[Noctua NF-A4x20 5V PWM](https://noctua.at/en/nf-a4x20-5v-pwm)
*	[Wall power supply](https://www.adafruit.com/product/1466)



## useful links
*	https://repo.download.nvidia.com/jetson/
*	https://google.com
*	https://www.arducam.com/faq/kernel-camera-driver/





### BootfromUSB

```bash

LABEL primary
      MENU LABEL primary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} root=PARTUUID=b49df390-238c-4497-99a6-0643b9077530 rootwait rootfstype=ext4

LABEL secondary
      MENU LABEL secondary kernel
      LINUX /boot/Image
      INITRD /boot/initrd
      APPEND ${cbootargs} quiet root=/dev/mmcblk0p1 rw rootwait rootfstype=ext4 console=ttyS0,115200n8 console=tty0 fbcon=map:0 net.ifnames=0



```



### Other

```bash
sudo nano /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
```

```sh
# SPDX-FileCopyrightText: Copyright (c) 2019-2021 NVIDIA CORPORATION & AFFILIATES. All rights reserved.
# SPDX-License-Identifier: LicenseRef-NvidiaProprietary
#
# NVIDIA CORPORATION, its affiliates and licensors retain all intellectual
# property and proprietary rights in and to this material, related
# documentation and any modifications thereto. Any use, reproduction,
# disclosure or distribution of this material and related documentation
# without an express license agreement from NVIDIA CORPORATION or
# its affiliates is strictly prohibited.

deb https://repo.download.nvidia.com/jetson/common r32.7 main
deb https://repo.download.nvidia.com/jetson/t210 r32.7 main
```



### IMX298 CAM Arducam

CSI Camera
```bash
sudo apt install libcanberra-gtk-module libcanberra-gtk3-module -y
```

pip tools needed
```bash
sudo pip3 install -U jetson-stats v4l2-fix
```




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

