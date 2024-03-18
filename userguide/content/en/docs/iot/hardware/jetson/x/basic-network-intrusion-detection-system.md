---
linkTitle: Basic Network Intrusion Detection System
title: Basic Network Intrusion Detection System using Python and Scapy on Nvidia Jetson Nano with Ubuntu
description: >
 In this tutorial, we will cover the steps to create a basic network intrusion detection system using Python and Scapy on your Nvidia Jetson Nano with Ubuntu. This intrusion detection system can be used to monitor network traffic for suspicious activity, such as unauthorized access attempts or malicious data transfers.
toc_hide: true
hide_summary: true
categories: ["jetson nano"]
---

## **Requirements**
- Nvidia Jetson Nano with Ubuntu installed
- Python 3 (https://www.python.org/downloads/)
- Pip (https://pypi.org/project/pip/)
- Scapy (https://scapy.net/)

## **Steps**
1. Connect your Jetson Nano to a computer using an SSH or USB connection.
2. Update the package lists and install the necessary packages for Python, Pip, and Scapy:
   ```bash
   sudo apt update
   sudo apt install -y python3-pip libpcap0.8-dev build-essential libssl-dev libffi-dev libcairo2-dev libgdk-pixbuf2.0-dev libjpeg8-dev libgif-dev libgtk2.0-dev libatk1.0-dev libcairo2-dev libpango1.0-dev libglib2.0-dev libxt6-dev
   sudo -H pip3 install scapy
   ```
3. Create a new Python file called `intrusion_detection.py` within the `/home/user/network_monitoring` directory on your Jetson Nano:
   ```bash
   nano /home/user/network_monitoring/intrusion_detection.py
   ```
4. Copy and paste the following code into the `intrusion_detection.py` file, replacing any existing content:

    ```python
	from scapy.all import *
	import datetime

	def process_packet(packet):
	    ip_layer = packet.getlayer("IP")
	    tcp_layer = packet.getlayer("TCP")

	    if ip_layer and tcp_layer:
	        ip_src = ip_layer.src
	        ip_dst = ip_layer.dst
	        tcp_sport = tcp_layer.sport
	        tcp_dport = tcp_layer.dport

	        # Check for unauthorized access attempts (e.g., SSH brute-force)
	        if tcp_dport == 22:  # SSH port number
	            print(f"[{datetime.datetime.now()}] Unauthorized access attempt detected from {ip_src} to {ip_dst}")

	        # Check for malicious data transfers (e.g., large file transfers)
	        if tcp_dport == 80 or tcp_dport == 443:  # HTTP and HTTPS ports
	            data = packet.getlayer("Raw").load
	            if len(data) > 1000:  # Arbitrary threshold for detecting large file transfers
	                print(f"[{datetime.datetime.now()}] Malicious data transfer detected from {ip_src} to {ip_dst}")

	# Start the packet sniffer and process each captured packet using the process_packet function
	sniff(prn=process_packet, filter="tcp")
    ```
5. Save and close the `intrusion_detection.py` file by pressing `Ctrl+X`, then `Y`, and finally `Enter`.
6. Run the intrusion detection system script by executing the following command in a terminal window on your Jetson Nano:
   ```bash
   python3 /home/user/network_monitoring/intrusion_detection.py
   ```
7. The script will now start capturing network traffic and processing each captured packet using the `process_packet` function. If any suspicious activity is detected, it will be printed to the console along with a timestamp indicating when the event occurred.
8. To stop the intrusion detection system script, simply press `Ctrl+C` in the terminal window where it is running.

## **Conclusion**
In this tutorial, we covered the steps to create a basic network intrusion detection system using Python and Scapy on your Nvidia Jetson Nano with Ubuntu. By following these steps, you should be able to monitor network traffic for suspicious activity, allowing you to identify potential security threats and respond appropriately.