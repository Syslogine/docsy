---
linkTitle: Basic Port Scanner
title: Basic Port Scanner with Nvidia Jetson Nano on Ubuntu
description: >
 In this tutorial, we will cover the steps to create a basic port scanner using the Nvidia Jetson Nano on Ubuntu. This tool can be used to scan for open ports on remote computers or devices, potentially allowing you to identify potential security vulnerabilities or other interesting patterns of behavior.
toc_hide: true
hide_summary: true
categories: ["jetson nano"]
---

## Requirements
- Nvidia Jetson Nano with Ubuntu installed
- Python 3.x installed (usually comes pre-installed on most modern distributions)

## Steps
1. Connect your Jetson Nano to a power source and insert an SD card with Ubuntu installed.
2. Power on the device and connect it to a monitor, keyboard, and mouse.
3. Open a terminal window by clicking on the top-left corner of the screen and selecting "Terminal".
4. Update the package lists by running the following command:
   ```
   sudo apt update
   ```
5. Install the `nmap` network exploration tool by running the following command:
   ```
   sudo apt install nmap
   ```
6. Create a new directory to store your port scanning scripts by running the following command:
   ```
   mkdir port_scanner
   cd port_scanner
   ```
7. Create a new Python script named `port_scanner.py` in your port_scanner directory by running the following command:
   ```
   nano port_scanner.py
   ```
8. Copy and paste the following code into your port_scanner.py file, replacing the placeholders with your own values:

```python
import argparse
import socket
import subprocess
import sys

# Define a function to perform a basic TCP port scan on a single IP address
def tcp_port_scan(ip_address, port_start, port_end):
    # Loop through each port in the specified range and attempt to establish a TCP connection
    for port in range(port_start, port_end + 1):
        try:
            # Create a socket object and connect to the target IP address on the current port number
            with socket.create_connection((ip_address, port), timeout=5) as sock:
                print(f"Port {port} is open.")
                
        except (socket.timeout, ConnectionRefusedError):
            # If the connection attempt fails, it may be because the target IP address is not reachable or the port is closed
            pass
        
# Define a function to parse command-line arguments and perform a basic TCP port scan on a range of IP addresses
def main():
    parser = argparse.ArgumentParser(description="Basic Port Scanner")
    parser.add_argument("start_ip", type=str, help="The starting IP address to scan (e.g., 192.168.0.1)")
    parser.add_argument("end_ip", type=str, help="The ending IP address to scan (e.g., 192.168.0.255)")
    parser.add_argument("--ports", type=int, nargs="+", default=[22, 80, 443], help="The list of ports to scan (default: [22, 80, 443])")
    
    args = parser.parse_args()
    
    # Loop through each IP address in the specified range and perform a basic TCP port scan on it
    for ip_address in range(int(args.start_ip.split(".")[0]), int(args.end_ip.split(".")[0]) + 1):
        for ip_part in args.start_ip.split(".")[1:]:
            if ip_part == "":
                ip_part = "0"
            
            ip_address = f"{ip_address}.{ip_part}"
            
            # Perform a basic TCP port scan on the current IP address using the specified list of ports
            tcp_port_scan(ip_address, args.ports[0], args.ports[-1])
        
# Run the main function
if __name__ == "__main__":
    main()
```

or

```python
import argparse
import socket
import threading

# Define a function to perform a basic TCP port scan on a single IP address
def tcp_port_scan(ip_address, port):
    try:
        # Create a socket object and connect to the target IP address on the specified port number
        with socket.create_connection((ip_address, port), timeout=5) as sock:
            print(f"Port {port} is open on {ip_address}.")
            
    except (socket.timeout, ConnectionRefusedError):
        # If the connection attempt fails, it may be because the target IP address is not reachable or the port is closed
        pass

# Define a function to scan a range of ports for a single IP address
def scan_ports(ip_address, ports):
    for port in ports:
        tcp_port_scan(ip_address, port)

# Define a function to perform a basic TCP port scan on a range of IP addresses
def main():
    parser = argparse.ArgumentParser(description="Basic Port Scanner")
    parser.add_argument("start_ip", type=str, help="The starting IP address to scan (e.g., 192.168.0.1)")
    parser.add_argument("end_ip", type=str, help="The ending IP address to scan (e.g., 192.168.0.255)")
    parser.add_argument("--ports", type=int, nargs="+", default=[22, 80, 443], help="The list of ports to scan (default: [22, 80, 443])")

    args = parser.parse_args()

    # Loop through each IP address in the specified range and perform a basic TCP port scan on it
    for ip_address in range(int(args.start_ip.split(".")[0]), int(args.end_ip.split(".")[0]) + 1):
        for ip_part in args.start_ip.split(".")[1:]:
            if ip_part == "":
                ip_part = "0"

            ip_address = f"{ip_address}.{ip_part}"

            # Perform a basic TCP port scan on the current IP address using threading
            threading.Thread(target=scan_ports, args=(ip_address, args.ports)).start()

# Run the main function
if __name__ == "__main__":
    try:
        main()
    except KeyboardInterrupt:
        print("\nPort scanning interrupted. Exiting.")
        sys.exit(0)
```

9. Save and exit your port_scanner.py file by pressing `Ctrl+X`, then `Y`, then `Enter`.
10. Run your port_scanner.py script by running the following command:
    ```
    python3 port_scanner.py 192.168.1.1 192.168.1.255 --ports 22 80 443
    ```
    This will scan for open ports on all IP addresses in the range from `192.168.1.1` to `192.168.1.255`, using a list of default ports such as SSH (port 22), HTTP (port 80), and HTTPS (port 443).
    
11. Observe the results of your port scanning attempt, which may include a list of open ports on each IP address that was scanned.

## Conclusion
In this tutorial, we covered the steps to create a basic port scanner using the Nvidia Jetson Nano on Ubuntu. By following these steps, you should be able to use your new tool to scan for open ports on remote computers or devices, potentially allowing you to identify potential security vulnerabilities or other interesting patterns of behavior.
