---
linkTitle: Simple Wi-Fi Sniffer
title: Simple Wi-Fi Sniffer with Nvidia Jetson Nano on Ubuntu
description: >
 In this tutorial, we will cover the steps to create a simple Wi-Fi sniffer using the Nvidia Jetson Nano on Ubuntu. This tool can be used to capture and analyze network traffic on nearby wireless networks, allowing you to gain insights into how data is transmitted over the air, identify potential security vulnerabilities, or potentially intercept sensitive information if no security measures are in place.
toc_hide: true
hide_summary: true
categories: ["jetson nano"]
---

## Requirements
- Nvidia Jetson Nano with Ubuntu installed
- A Wi-Fi adapter compatible with monitor mode (e.g., [Alfa AWUS036NH](https://www.amazon.com/s?k=Alfa-Network-AWUS036NH-Raspberry-Tinkerers) or any other compatible adapter)

## Steps
1. Connect your Jetson Nano to a power source and insert an SD card with Ubuntu installed.
2. Power on the device and connect it to a monitor, keyboard, and mouse.
3. Open a terminal window by clicking on the top-left corner of the screen and selecting "Terminal".
4. Update the package lists by running the following command:
   ```bash
   sudo apt update
   ```
5. Install the `aircrack-ng` suite of wireless security tools by running the following command:
   ```bash
   sudo apt install aircrack-ng
   ```
6. Connect your Wi-Fi adapter to one of the USB ports on your Jetson Nano and power it on.
7. Check if your Wi-Fi adapter is recognized by the system by running the following command (ensure your adapter supports monitor mode):
   ```bash
   ls /sys/class/net/
   ```
   You should see an output similar to this:
   ```bash
   eth0 wlan0
   ```
   If you do not see `wlan0` in the list of network interfaces, it may be because your Wi-Fi adapter is not compatible with monitor mode. In that case, you will need to use a different Wi-Fi adapter or follow alternative steps to enable monitor mode on your specific adapter.

8. Bring up the `wlan0` interface by running the following command:
   ```bash
   sudo ip link set wlan0 up
   ```
9. Put the `wlan0` interface into monitor mode by running the following command:
   ```bash
   sudo iw phy wlan0 interface add mon0 type monitor
   sudo ip link set mon0 up
   ```

10. Run a packet capture utility such as `tshark` to capture network traffic on the nearby wireless networks, and save the output to a file:
    ```bash
    tshark -i mon0 -f "wlan" -w wifi_capture.pcapng
    ```
11. Observe the captured network traffic in real-time by running the following command in another terminal window:
    ```bash
    tcpdump -r wifi_capture.pcapng
    ```

12. After you have collected enough network traffic data, stop the packet capture utility by pressing `Ctrl+C`. 

13. Analyze the captured network traffic using tools such as Wireshark or `aircrack-ng` to identify potential security vulnerabilities or other interesting patterns of behavior.

## Conclusion
In this tutorial, we covered the steps to create a simple Wi-Fi sniffer using the Nvidia Jetson Nano on Ubuntu. By following these steps, you should be able to use your new tool to capture and analyze network traffic on nearby wireless networks, potentially allowing you to identify potential security vulnerabilities or other interesting patterns of behavior.
