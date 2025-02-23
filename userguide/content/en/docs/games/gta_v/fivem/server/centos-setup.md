---
title: "Installing a FiveM Server on CentOS"
linktitle: "CentOS FiveM Setup"
draft: false
description: "This tutorial will guide you through the process of installing a FiveM server on a CentOS operating system."
---

# Installing a FiveM Server on CentOS



## Prerequisites

- A server running CentOS.
- Root or sudo access on the server.
- Basic knowledge of the Linux command-line interface.

## Step 1: Installing Dependencies

1. Update your system:
   ```bash
   sudo yum update
   ```

2. Install the EPEL repository:
   ```bash
   sudo yum install epel-release
   ```

3. Install required packages:
   ```bash
   sudo yum install git curl screen xz wget -y
   ```

## Step 2: Adding a New User for FiveM

It's recommended to run the FiveM server as a separate user for security purposes.

1. Create a new user:
   ```bash
   sudo adduser fivem
   ```

2. Switch to the new user:
   ```bash
   su - fivem
   ```

## Step 3: Downloading and Extracting FiveM Server Files

1. Download the latest server artifact:
   ```bash
   wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/latest.tar.xz
   ```

2. Extract the server files:
   ```bash
   tar xf latest.tar.xz
   ```

## Step 4: Configuring the Server

1. Create a server configuration file (`server.cfg`):
   ```bash
   nano server.cfg
   ```

2. Add basic configuration settings to `server.cfg`. Refer to the FiveM documentation for sample configurations.

3. Save and exit the nano editor.

## Step 5: Running the Server

1. Start the server using the `screen` utility:
   ```bash
   screen -S fivem-server ./run.sh +exec server.cfg
   ```

## Step 6: Server Management

- To detach from the `screen` session, press `Ctrl+A` followed by `Ctrl+D`.
- To return to the session, use `screen -r fivem-server`.

## Conclusion

Your FiveM server should now be operational on CentOS. Always manage your server responsibly and in compliance with FiveM's terms of service.

---

For detailed configuration options and more advanced settings, consult the [FiveM Documentation](https://docs.fivem.net/).
