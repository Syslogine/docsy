---
title: "Setting Up a FiveM Server on Debian"
linktitle: "Debian FiveM Setup"
draft: false
description: "A comprehensive guide to setting up a FiveM server on a Debian-based system."
---

# Setting Up a FiveM Server on Debian

Creating a FiveM server on a Debian server involves several steps. This guide will walk you through the process from start to finish.

## Prerequisites

- A server running Debian or a Debian-based Linux distribution.
- Root or sudo access on the server.
- Basic knowledge of Linux command-line interface.

## Step 1: Installing Dependencies

Before installing the FiveM server, you need to install the required dependencies.

1. Update your package lists:
   ```bash
   sudo apt update
   ```

2. Install the necessary packages:
   ```bash
   sudo apt install git curl screen xz-utils wget -y
   ```

## Step 2: Creating a User for FiveM

It's a good practice to run services like FiveM under a separate user.

1. Create a new user:
   ```bash
   sudo adduser fivem
   ```

2. Switch to the new user:
   ```bash
   su - fivem
   ```

## Step 3: Downloading FiveM Server Files

1. Download the latest server artifact:
   ```bash
   wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/latest.tar.xz
   ```

2. Extract the server files:
   ```bash
   tar xf latest.tar.xz
   ```

## Step 4: Configuring the Server

1. Create a new configuration file (`server.cfg`):
   ```bash
   nano server.cfg
   ```

2. Populate the configuration file. A basic example can be found in the FiveM documentation.

3. Save and exit the editor.

## Step 5: Running the Server

1. Start the server using `screen` for background execution:
   ```bash
   screen -S fivem-server ./run.sh +exec server.cfg
   ```

## Step 6: Managing Your Server

- To detach from the `screen` session, press `Ctrl+A` then `Ctrl+D`.
- To reattach to the session, use `screen -r fivem-server`.

## Conclusion

You have now set up a FiveM server on Debian. Remember to manage your server responsibly and adhere to the FiveM terms of service.

---

For more advanced configurations and troubleshooting, refer to the [FiveM Documentation](https://docs.fivem.net/).