---
linkTitle: Xbox 360 v1 Camera
title: Xbox 360 v1 Camera

---

# Setting up the Xbox 360 v1 Camera on Jetson Nano with Ubuntu

## Overview
In this tutorial, we will cover the steps to set up the Xbox 360 v1 camera on a Nvidia Jetson Nano running Ubuntu. This camera can be used for various applications such as computer vision and machine learning.

## Requirements
- Nvidia Jetson Nano with Ubuntu installed
- USB 2.0 cable (for connecting the Xbox 360 v1 camera to the Jetson Nano)
- Xbox 360 v1 camera

## Steps
1. Connect the Xbox 360 v1 camera to the Jetson Nano using a USB 2.0 cable.
2. Open a terminal window on the Jetson Nano by clicking on the top-left corner of the screen and selecting "Terminal".
3. Update the package lists by running the following command:
   ```
   sudo apt update
   ```
4. Install libuvc, which is required to communicate with the Xbox 360 v1 camera:
   ```
   sudo apt install libuvc-dev
   ```
5. Reboot the Jetson Nano by running the following command:
   ```
   sudo reboot
   ```
6. After the reboot, open a new terminal window and run the following command to verify that the Xbox 360 v1 camera is recognized by the system:
   ```
   ls /dev/video*
   ```
   You should see an output similar to this:
   ```
   /dev/video0
   ```
7. Run the following command to test the camera feed in VLC media player:
   ```
   vlc v4l2:// :v4l-vbi-fmt=none :v4l-chroma=h264 :v4l-chroma-cap=0 :v4l-fps=30 :v4l-input=1 :v4l-std=pal :v4l-frequency=525 :live-caching=300
   ```
8. If the camera feed is working correctly, you can proceed to develop your computer vision or machine learning applications using libraries like OpenCV.

## Conclusion
In this tutorial, we covered the steps to set up the Xbox 360 v1 camera on a Nvidia Jetson Nano running Ubuntu. By following these steps, you should be able to use the camera for various applications such as computer vision and machine learning.
