---
linkTitle: Set Up SSD on Nvidia Jetson Nano
title: How To Set Up SSD on Nvidia Jetson Nano
description: >
 Learn how to mount and configure an SSD on your Nvidia Jetson Nano, transitioning from a MicroSD setup. This step-by-step guide will walk you through the process.
categories: ["jetson nano"]
---

## Prerequisites

- Nvidia Jetson Nano
- SSD
- MicroSD card
- Terminal access

## Steps

### 1. Wipe SSD
1.1. Mount the SSD on your Jetson Nano.
1.2. Open the `Disks` utility.
1.3. Select the SSD Disk and press `Ctrl` + `F`.
   - **Erase**: Choose either `Don't overwrite existing data (Quick)` or `Overwrite existing data with zeroes (slow)`.
   - **Partitioning**: Select `Compatitble with modern systems and hard disks > 2TB (GPT)`.

1.4. Click `Format...`.
1.5. Click `Format` and wait for the process to complete (duration depends on the chosen quick or slow format).
1.6. Click the `+` to create a new partition.
1.7. Set the Partition size to 110GB for SWAP.
1.8. Click `Next`.
   - **Volume Name**: Create one.
   - **Type**: Choose `Internal disk for use with Linux systems only (Ext4)`.

1.9. Click `Create`.
1.10. Finally, mount the SSD.
1.11. After the SSD is mounted, open `Terminal` to install `nano`:
    ```bash
    sudo apt install nano
    ```

### 2. Download and Move Files
2.1. Download the `bootFromUSB` repository from [JetsonHacks](https://github.com/jetsonhacks/bootFromUSB):
    ```bash
    git clone https://github.com/jetsonhacks/bootFromUSB
    ```
2.2. Enter the `bootFromUSB` folder:
    ```bash
    cd bootFromUSB
    ```
2.3. Obtain the SSD UUID:
    ```bash
    ./partUUID.sh
    ```
   Remember the output: `root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060`.

2.4. Move files from MicroSD to SSD:
    ```bash
    ./copyRootToUSB.sh -p /dev/sda1
    ```

### 3. Configure SSD
3.1. Navigate to the SSD folders:
    ```bash
    cd /media/syslogine/myproject/boot/extlinux
    ```
3.2. Open `extlinux.conf`:
    ```bash
    sudo nano extlinux.conf
    ```
3.3. Replace:
    ```
    root=/dev/mmcblk0p1
    ```
    with the SSD UUID obtained earlier:
    ```
    root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060
    ```
3.4. Save and exit `nano` (`Ctrl` + `X`, `Y`, `Enter`).
3.5. Shutdown Jetson Nano:
    ```bash
    sudo poweroff
    ```
3.6. After your Jetson Nano powers off, remove the MicroSD card and power it on again. The system should now boot from the SSD instead of the MicroSD card.

## Conclusion
Congratulations! You have successfully set up your SSD on Nvidia Jetson Nano, enhancing storage and performance.
