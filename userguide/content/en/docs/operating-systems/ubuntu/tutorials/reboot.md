---
linktitle: "shutdown/reboot"
title: How to shutdown or reboot
weight: 2
tags: ['how to', 'shutdown', 'reboot', 'ubuntu', 'server', 'desktop']
categories: ["Ubuntu"]
---

How to shutdown or reboot your Ubuntu machine from the command line?

Well it is actually one of the first things you learn when you administer servers via ssh, let’s start with restart.
```bash
reboot
```
You need to be root to be able to restart a Ubuntu system, or you can use sudo (provided you are in the sudoers file)
```bash
sudo reboot
```
Another way to do it is to use shutdown command.
```bash
shutdown -r now
```
The `-r` switch will That will reboot the machine inmediately, if you want to add a delay.
```bash
shutdown -r +15
```
That command will reboot the machine 15 minutes after the issue of the command. You might also want to reboot the machine at a specific time:
```bash
shutdown -r 17:15
```
This is pretty self explanatory, it will restart at 17:15 hours, be sure to use the 24 hours format. Let’s now write about shutdown instead of reboot.

We are going to use the same shutdown command, just this time with h switch instead of r. The h stands for halt and the r for reboot. So to turn off the machine at this very moment use this command.
```bash
shutdown -h now
```
And if you want to do it with a delay.
```bash
shutdown -h +15
```
That will enter a fifteen minutes delay after the issue of the command. If you want to turn it off at a specific time.
```bash
shutdown -h 17:15
```
Just like with the reboot example, this will turn the Ubuntu machine off at 17:15, and once again you need to use the 24 time format.

