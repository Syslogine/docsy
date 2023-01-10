---
title: My Custom AI project

tags: ["ubuntu","jetson","nano","project","ai","awesome","custom"]
---

List of dependencies i need for creatiing my project.



*	https://github.com/raymondlo84/nvidia-jetson-ai-monitor
*	https://github.com/OpenKinect/libfreenect


## Material i used

*	Jetson Nano Developer Kit 4GB
*	Wall power supply
*	Samsung Class 10 MicroSD 32GB
*	120GB SSD
*	Sata to usb 3 cable
*	Noctua NF-A4x20-PWM
*	Xbox Kinect v1


## Download jetson nano 
1.	Download the [Jetson Nano Developer Kit SD Card Image](https://developer.nvidia.com/jetson-nano-sd-card-image), and note where it was saved on the computer.
2.	Write the image to your microSD card with [Etcher](https://www.balena.io/etcher/).


## Install Ubuntu
1.	Select **`I accept the terms of the licenses`** and continue
2.	Select a language
3.	Select keyboard layout
4.	Select time zone
5.	Choose `computer name`, `username`, `create password` and then keep the **`Require my password to login`**
6.	Select the max size of the usb as the MicroSD is temporary use
7.	Select the `MAXN - (Default)` and click continue to start install
8.	After install login with new created account as steps above
9.	After first login it will pop a annoying `Keyboard Shortcuts` window.... Close this
10.	And close the other welcome window...


## Updating Jetson Nano
1.	Now we need to update our packages list so open `terminal` and type
	```bash
	sudo apt update
	```
2.	Now we need to upgrade the packages
	```bash
	sudo apt upgrade -y
	```
3.	After this is done.. just reboot your device
	```bash
	sudo reboot now
	```
4.	Once again after login open `terminal` as we need to clean a bit so type
	```bash
	sudo apt autoremove -y && sudo apt clean
	```




## Wipe SSD and Moving MicroSD to SSD
### Without Video
1.	Mount the SSD in your Jetson Nano
2.	Open `Disks`
3.	Select the SSD Disk and Press `Ctrl` + `F`
	*	**`Erase`**: `Don't overwrite existing data (Quick)` or `Overwrite existing data with zeroes (slow)`
	*	**`Partitioning`**: `Compatitble with modern systems and hard disks > 2TB (GPT)`
4.	Click `Format...`
5.	Again click on `Format` and wait..... Depends on what u selected (Quick) or (Slow)
6.	Now Click on the `+` Create Patrtition
7.	I have set the Partition size to 110GB for SWAP (We will use this later this page)
8.	Click Next
	*	**`Volume Name`**: Create one
	*	**`Type`**: `Internal disk for use with Linux systems only (Ext4)`
9.	Click on `Create`
10.	Finnaly mount the SSD
11.	After the SSD is mounted open `Terminal` as we need to update and upgrade our packages
	```bash
	sudo apt update && sudo apt upgrade -y
	```
12.	We also need to install `nano` as this is not installed by default and we use this later on
	```bash
	sudo apt install nano
	```
12.	Now we download the repository `bootFromUSB` from [JetsonHacks](https://github.com/jetsonhacks)
	```bash
	git clone https://github.com/jetsonhacks/bootFromUSB
	```
13.	Enter the bootFromUSB folder
	```bash
	cd bootFromUSB
	```
14.	We need to have the SSD UUID so
	```bash
	./partUUID.sh
	```

	This will output ssomething like this

	```
	PARTUUID of Partition: /dev/sda1
	a40b6c71-ca35-79d3-8an0-d6v66749e060

	Sample snippet for /boot/extlinux/extlinux.conf entry:
	APPEND ${cbootargs} root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060 rootwait rootfstype=ext4
	```

	We only need this part to remember so note this on a text file or open a new ternimal en keep this one open..
	```
	root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060
	```
15. Now let's move the files from MicroSD to SSD
	```bash
	./copyRootToUSB.sh -p /dev/sda1
	```

	And yes im very aware of that we have now upgraded the Jetson Nano, Reason is why upgrade on slow MicroSD when we can do this ona faster SSD ;)

16.	Now we need to change one part in our SSD
	```bash
	cd /media
	```
17.	When we use the command `ls` will see a our current user for me is it `syslogine`
	```bash
	ls
	```
	```
	syslogine
	```
	So we enter the folder
	```bash
	cd syslogine
	```
18.	again when we do the `ls` command we can see our new created SSD for me it is `myproject`
	```bash
	ls
	```

	```
	myproject
	```
	So we enter the folder
	```bash
	cd myproject
	```
19.	After were in the right SSD folder go to 
	```bash
	cd boot/extlinux
	```
20.	edit `extlinux.conf`
	```bash
	sudo nano extlinux.conf
	```
21.	Replace
	```
	root=/dev/mmcblk0p1
	```
	with your SSD one, the one we early noted some where or still have that terminal open
	```
	root=PARTUUID=a40b6c71-ca35-79d3-8an0-d6v66749e060
	```
	Save and close Nano with `Ctrl` + `X` and then `Y` then `Enter`

22.	Finnaly... Lets shutdown Jetson Nano
	```bash
	sudo poweroff
	```
23.	After your Jetson Nano is powered off remove the MicroSD card and power on the device again





#####

```bash
mkdir project && cd project
```


#### Installation of libusb

Get the latest version of `libusb`
```bash
wget https://github.com/libusb/libusb/releases/download/v1.0.26/libusb-1.0.26.tar.bz2
```

Now we need to extract it..
```bash
tar -xvjf libusb-1.0.26.tar.bz2
```

And i love to work with folder with smaller names so rename it
```bash
mv libusb-1.0.26 libusb
```

now we enter the folder we renamed
```bash
cd libusb
```


```bash
./configure --prefix=/usr --disable-static &&
make
```

```bash
sudo make install
```

after `make install` was succesful we can remove the .tar.bz2
```bash
cd .. && rm libusb-1.0.26.tar.bz2
```

