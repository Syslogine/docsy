---
linktitle: "Tips and Tricks"
title: Tips and Tricks for Ubuntu
tags: ['ubuntu','tips','tricks']
categories: ["Ubuntu"]
weight: 1
---

## Managing Packages with apt

### apt update
Before we begin, we update our packages list with the following command:

```bash
sudo apt update
```

### apt upgrade
When there are packages that can be upgraded, we can do so using the following command:

```bash
sudo apt upgrade
```
After running this command, you will be prompted to confirm whether or not you want to proceed with the updates. Simply press `Y` followed by `ENTER`.

### Combining update and upgrade commands
To save time, you can also combine the `apt update` and `apt upgrade` commands into a single command:

```bash
sudo apt update && sudo apt upgrade -y
```

The `-y` flag automatically answers `Y` to any prompts that may appear during the upgrade process.

### Installing packages with apt
To install a package, use the following command:

```bash
sudo apt install packagename
```

Replace `packagename` with the name of the package you want to install. For example, if you wanted to install the `filezilla` FTP client, you would use the following command:

```bash
sudo apt install filezilla
```

### Removing packages with apt
To remove a package and its configuration files, use the following command:

```bash
sudo apt remove packagename
```

Replace `packagename` with the name of the package you want to remove. For example, if you wanted to remove the `filezilla` FTP client, you would use the following command:

```bash
sudo apt remove filezilla
```

### Purging packages with apt
If you want to remove a package as well as any configuration files that may have been created by it, use the following command:

```bash
sudo apt purge packagename
```

Replace `packagename` with the name of the package you want to remove. For example, if you wanted to remove the `filezilla` FTP client along with any associated configuration files, you would use the following command:

```bash
sudo apt purge filezilla
```

### Cleaning up apt packages
To free up disk space by removing downloaded package files that are no longer needed, use the following command:

```bash
sudo apt clean
```

### Moving and renaming files/directories
To move a file or directory to another location on your system, use the `mv` command followed by the source file or directory and its destination path. For example, if you wanted to move a file named `sourcefile.txt` from your home directory to the `/home/destination/` directory, you would use the following command:

```bash
mv /home/sourcefile.txt /home/destination/
```

To rename a file or directory, use the same `mv` command followed by the source file or directory and its new name. For example, if you wanted to rename a file named `sourcefile.txt` to `destfile.txt`, you would use the following command:

```bash
mv /home/sourcefile.txt /home/destfile.txt
```

### Copying files/directories
To copy a file or directory from one location on your system to another, use the `cp` command followed by the source file or directory and its destination path. For example, if you wanted to copy a file named `sourcefile.txt` from your home directory to the `/home/destination/` directory, you would use the following command:

```bash
cp /home/sourcefile.txt /home/destination/
```

To create an empty file or directory, use the `touch` command followed by the path of the new item. For example, if you wanted to create an empty text file named `newfile.txt` in your home directory, you would use the following command:

```bash
touch /home/newfile.txt
```

To create a new directory with the specified name, use the `mkdir` command followed by the path of the new directory. For example, if you wanted to create a new directory named `newfolder` in your home directory, you would use the following command:

```bash
mkdir /home/newfolder
```

### Removing files/directories
To remove a file or directory from your system, use the `rm` command followed by the path of the item to be removed. For example, if you wanted to remove a file named `sourcefile.txt` from your home directory, you would use the following command:

```bash
rm /home/sourcefile.txt
```

To remove a directory along with its contents, use the `-r` flag with the `rm` command followed by the path of the directory to be removed. For example, if you wanted to remove a directory named `newfolder` along with its contents from your home directory, you would use the following command:

```bash
rm -r /home/newfolder
```

### Changing directories
To navigate to a different directory on your system, use the `cd` command followed by the path of the directory you want to move to. For example, if you wanted to change to the `/home/destination/` directory from your current location, you would use the following command:

```bash
cd /home/destination/
```

To move up one level in the directory hierarchy, use the `..` notation with the `cd` command. For example, if you were in the `/home/destination/` directory and wanted to move back to your home directory, you would use the following command:

```bash
cd ..
```

### Rebooting and shutting down your system
To restart your server, use the following command:

```bash
sudo reboot now
```

This will prompt your server to perform a graceful reboot. If you prefer, you can also use the following shorthand version of the command:

```bash
sudo reboot .
```

To shut down your server, use the following command:

```bash
sudo shutdown now
```

This will immediately initiate a system shutdown. Alternatively, you can use the following command to power off your machine:

```bash
sudo poweroff
```

### Switching to the root user account
To switch to the root user account and gain full administrative privileges on your system, use either of the following commands:

```bash
su -
sudo su -
```

The first command will prompt you for the root password, while the second command will prompt you for the password of the current user.

### Clearing the terminal screen
To clear all text from your terminal screen, use the following command:

```bash
clear
```

This will erase any output displayed on the screen, leaving only your system's command prompt.

### Forcing package upgrades
If a package is not being upgraded when you run the `apt upgrade` command, you can try using the following command to force an upgrade:

```bash
sudo apt dist-upgrade
```

This will attempt to resolve any dependencies that may be preventing a package from being upgraded.