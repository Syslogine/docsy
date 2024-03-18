---
linkTitle: Set Up SSD on Nvidia Jetson Nano
title: How To Set Up SSD on Nvidia Jetson Nano
description: >
 Learn how to mount and configure an SSD on your Nvidia Jetson Nano, transitioning from a MicroSD setup. This step-by-step guide will walk you through the process.
categories: ["jetson nano"]
---

## **Prerequisites**

- Nvidia Jetson Nano
- SSD
- MicroSD card
- Terminal access

## **Steps**

### **1. Wipe SSD Using Terminal**
1. Connect the SSD to your Jetson Nano.
2. Open a terminal.
3. Use the `fdisk` command to manage partitions:
    ```bash
    sudo fdisk /dev/sda
    ```
4. Delete existing partitions by typing `d` and follow the on-screen prompts.
5. Create a new partition by typing `n` and follow the prompts. Choose `Primary` and use the default values.
6. Set the partition type to Linux (`83`) by typing `t` and choosing `83`.
7. Write the changes and exit by typing `w`.

### 2. Format and Mount the SSD
1. Format the SSD partition with the Ext4 file system:
    ```bash
    sudo mkfs.ext4 /dev/sda1
    ```
2. Create a mount point:
    ```bash
    sudo mkdir /media/ssd
    ```
3. Mount the SSD:
    ```bash
    sudo mount /dev/sda1 /media/ssd
    ```
4. Confirm that the SSD is mounted:
    ```bash
    df -h
    ```
5. Make the SSD mount automatically on boot by adding an entry to `/etc/fstab`:
    ```bash
    echo '/dev/sda1 /media/ssd ext4 defaults 0 0' | sudo tee -a /etc/fstab
    ```
6. Check the entry in `/etc/fstab`:
    ```bash
    cat /etc/fstab
    ```

### 3. Additional Configuration (Optional)
1. If you want to set up a SWAP partition (optional), you can create and enable it using the following commands:
    ```bash
    sudo fallocate -l 4G /media/ssd/swapfile
    sudo chmod 600 /media/ssd/swapfile
    sudo mkswap /media/ssd/swapfile
    sudo swapon /media/ssd/swapfile
    ```
2. To make the SWAP file permanent, add an entry to `/etc/fstab`:
    ```bash
    echo '/media/ssd/swapfile none swap sw 0 0' | sudo tee -a /etc/fstab
    ```

### Conclusion
You have successfully wiped, formatted, and mounted your SSD using the terminal on your Nvidia Jetson Nano.


### **2. Download and Move Files**
0. After the SSD is mounted, open `Terminal` to install `nano`:
    ```bash
    sudo apt install nano
    ```
1. Download the `bootFromUSB` repository from [JetsonHacks](https://github.com/jetsonhacks/bootFromUSB):
    ```bash
    git clone https://github.com/jetsonhacks/bootFromUSB
    ```
2. Enter the `bootFromUSB` folder:
    ```bash
    cd bootFromUSB
    ```
3. Obtain the SSD UUID:
    ```bash
    ./partUUID.sh
    ```
   Remember the output: `root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060`.
4. Move files from MicroSD to SSD:
    ```bash
    ./copyRootToUSB.sh -p /dev/sda1
    ```

### 3. Configure SSD
1. Navigate to the SSD folders:
    ```bash
    cd /media/syslogine/myproject/boot/extlinux
    ```
2. Open `extlinux.conf`:
    ```bash
    sudo nano extlinux.conf
    ```
3. Replace:
    ```
    root=/dev/mmcblk0p1
    ```
    with the SSD UUID obtained earlier:
    ```
    root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060
    ```
4. Save and exit `nano` (`Ctrl` + `X`, `Y`, `Enter`).
5. Shutdown Jetson Nano:
    ```bash
    sudo poweroff
    ```
6. After your Jetson Nano powers off, remove the MicroSD card and power it on again. The system should now boot from the SSD instead of the MicroSD card.

## Conclusion
Congratulations! You have successfully set up your SSD on Nvidia Jetson Nano, enhancing storage and performance.
