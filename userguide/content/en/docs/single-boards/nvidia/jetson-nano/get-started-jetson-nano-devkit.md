---
Title: Getting Started with Jetson Nano Developer Kit
linkTitle: Get Started
categories: ["jetson nano"]
---

<style> 
.center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  
}
</style>

## **Introduction**
The [NVIDIA® Jetson Nano™ Developer Kit](https://developer.nvidia.com/embedded/buy/jetson-nano-devkit) is a small AI computer for makers, learners, and developers. After following along with this brief guide, you’ll be ready to start building practical AI applications, cool AI robots, and more.



1.	microSD card slot for main storage
2.	40-pin expansion header
3.	Micro-USB port for 5V power input, or for Device Mode
4.	Gigabit Ethernet port
5.	USB 3.0 ports (x4)
6.	HDMI output port
7.	DisplayPort connector
8.	DC Barrel jack for 5V power input
9.	MIPI CSI-2 camera connectors



### Included in the Box
Your Jetson Nano Developer Kit box includes:
*	NVIDIA Jetson module and reference carrier board
*	Small paper card with quick start and support information
*	Folded paper stand
### Items not Included
You’ll also need:
*	microSD card (32GB UHS-1 minimum recommended)
*	USB keyboard and mouse
*	Computer display (HDMI or DP)
*	Micro-USB power supply

## **Prepare for Setup**
### Items for Getting Started
#### microSD Card
The Jetson Nano Developer Kit uses a microSD card as a boot device and for main storage. It’s important to have a card that’s fast and large enough for your projects; the minimum recommended is a 32 GB UHS-1 card.

See the instructions below to flash your microSD card with operating system and software.

#### Micro-USB Power Supply
You’ll need to power the developer kit with a good quality power supply that can deliver 5V⎓2A at the developer kit’s Micro-USB port. Not every power supply promising “5V⎓2A” will actually do this.

As an example of a good power supply, NVIDIA has validated [Adafruit’s 5V 2.5A Switching Power Supply with 20AWG MicroUSB Cable (GEO151UB-6025)](https://www.adafruit.com/product/1995). It was specifically designed to overcome common problems with USB power supplies; see the linked product page for details.


Note:
The stated power output capability of a USB power supply can be seen on its label.

Actual power delivery capabilities of USB power supplies do vary. Please see the [Jetson Nano Developer Kit User Guide](https://developer.nvidia.com/embedded/downloads#?search=Jetson%20Nano%20Developer%20Kit%20User%20Guide) for additional information.


## **Write Image to the microSD Card**
To prepare your microSD card, you’ll need a computer with Internet connection and the ability to read and write SD cards, either via a built-in SD card slot or adapter.
1.	Download the [Jetson Nano Developer Kit SD Card Image](https://developer.nvidia.com/jetson-nano-sd-card-image), and note where it was saved on the computer.
2.	Write the image to your microSD card by following the instructions below according to your computer’s operating system: Windows, macOS, or Linux.
### Instructions for Windows
Format your microSD card using SD Memory Card Formatter from the SD Association.

<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Windows-SD_Card_Formatter.png"><br>

1.	Download, install, and launch [SD Memory Card Formatter for Windows](https://www.sdcard.org/downloads/formatter_4/eula_windows/).
2.	Select card drive
3.	Select “Quick format”
4.	Leave “Volume label” blank
5.	Click “Format” to start formatting, and “Yes” on the warning dialog

Use Etcher to write the Jetson Nano Developer Kit SD Card Image to your microSD card
1.	Download, install, and launch [Etcher](https://www.balena.io/etcher)

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Windows-Etcher.png"><br>

2.	Click “Select image” and choose the zipped image file downloaded earlier.
3.	Insert your microSD card if not already inserted.
	Click Cancel (per this explanation) if Windows prompts you with a dialog like this:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Windows-Etcher_Cancel.png"><br>

4.	Click “Select drive” and choose the correct device.

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Windows-Etcher_Select_Drive.png"><br>

5.	Click “Flash!” It will take Etcher about 10 minutes to write and validate the image if your microSD card is connected via USB3.
6.	After Etcher finishes, Windows may let you know it doesn’t know how to read the SD Card. Just click Cancel and remove the microSD card.

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Windows-SD_Card_Prompt.png">

After your microSD card is ready, proceed to [set up your developer kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#setup).



### Instructions for Mac OS
You can either write the SD card image using a graphical program like Etcher, or via command line.

#### Etcher Instructions
1.	Do not insert your microSD card yet.
2.	Download, install, and launch [Etcher](https://www.balena.io/etcher).

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Etcher.png"><br>

3.	Click “Select image” and choose the zipped image file downloaded earlier.
4.	Insert your microSD card. Click Ignore if your Mac shows this window:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Disk_readable.png"><br>

5.	If you have no other external drives attached, Etcher will automatically select the microSD card as target device. Otherwise, click “Select drive” and choose the correct device.
6.	Click “Flash!” Your Mac may prompt for your username and password before it allows Etcher to proceed

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Etcher_permission.png">
	It will take Etcher about 10 minutes to write and validate the image if your microSD card is connected via USB3.

7.	After Etcher finishes, your Mac may let you know it doesn’t know how to read the SD Card. Just click Eject and remove the microSD card.

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Disk_readable.png"><br>

#### Command Line Instructions
1.	Do not insert your microSD card yet. Waiting will help you discover correct disk device name in steps below.
2.	Open the Terminal app:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Terminal_app.png"><br>

3.	Use this command to list any external disk devices already attached to your Mac:
	```bash
	diskutil list external | fgrep '/dev/disk'
	```
	For example, if you already have a USB drive attached to your Mac, the result will look similar to this:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Terminal_disk_already_attached.png"><br>

4.	Insert your microSD card. Click Ignore if your Mac shows this window:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Disk_readable.png"><br>

5.	Use the same command as before to list external disk devices. The newly listed disk device is the microSD card (/dev/disk2 in this example):

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Terminal_list_disks.png"><br>

6.	Use this command to remove any existing partitions from the microSD card, ensuring MacOS will let you write to it. ***BE VERY CAREFUL to specify the correct disk device***.
	```bash
	sudo diskutil partitionDisk /dev/disk<n> 1 GPT "Free Space" "%noformat%" 100%
	```
	For example:
	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Terminal_partitions.png"><br>

7.	Use this command to write the zipped SD card image to the microSD card. Note the use of /dev/rdisk instead of /dev/disk:
	```bash
	/usr/bin/unzip -p ~/Downloads/jetson_nano_devkit_sd_card.zip | sudo /bin/dd of=/dev/rdisk<n> bs=1m
	```
	For example:
	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Terminal_write_zipped_SD_card.png"><br>

8.	There will be no indication of progress (unless you signal with CTRL-t). When the dd command finishes, your Mac will let you know it cannot read the microSD card. Just click Eject:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Mac-Disk_readable.png"><br>

After your microSD card is ready, proceed to [set up your developer kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#setup).

### Instructions for Linux
You can either write the SD card image using a graphical program like Etcher, or via command line.

#### Etcher Instructions
1.	Download, install, and launch [Etcher](https://www.balena.io/etcher).
	
	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Linux-Etcher.png"><br>

2.	Click “Select image” and choose the zipped image file downloaded earlier.
3.	Insert your microSD card. If you have no other external drives attached, Etcher will automatically select the microSD card as target device. Otherwise, click “Change” and choose the correct device.

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Linux-Etcher_Select_Drive.png"><br>

4.	Click “Flash!” Your OS may prompt for your username and password before it allows Etcher to proceed.

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Linux-Etcher_Password.png"><br>
	It will take Etcher 10-15 minutes to write and validate the image if your microSD card is connected via USB3.

5.	After Etcher finishes, eject the SD Card using Files application:
	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Linux-Files_App.png"><br>

6.	Physically remove microSD card from the computer.

#### Command Line Instructions
1.	Open the Terminal application by pressing `Ctrl` + `Alt` + `t`.
2.	Insert your microSD card, then use a command like this to show which disk device was assigned to it:
	```bash
	dmesg | tail | awk '$3 == "sd" {print}'
	```
	In this example, we can see the 16GB microSD card was assigned /dev/sda:

	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Linux-Terminal_Disk_Assign.png"><br>

3.	Use this command to write the zipped SD card image to the microSD card:
	```bash
	/usr/bin/unzip -p ~/Downloads/jetson_nano_devkit_sd_card.zip | sudo /bin/dd of=/dev/sd<x> bs=1M status=progress
	```
	For example:
	<img class="center" src="https://developer.nvidia.com/sites/default/files/akamai/embedded/images/jetsonNano/gettingStarted/Jetson_Nano-Getting_Started-Linux-Terminal_Disk_Write.png"><br>

	When the dd command finishes, eject the disk device from the command line:
	```bash
	sudo eject /dev/sd<x>
	```
4.	Physically remove microSD card from the computer.

After your microSD card is ready, proceed to [Setup your developer kit](https://developer.nvidia.com/embedded/learn/get-started-jetson-nano-devkit#setup).

## **Setup and First Boot**
### Initial Setup with Display Attached
### Initial Setup in Headless Mode

## **Next Steps**
### Find Your Way Around
### Projects and Learning

## **Troubleshooting**
### Power
### Display