---
title: My Custom AI project

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


## Wipe SSD
1.	Plugin the SSD in
2.	Open Disks
3.	Select the SSD Disk and Press `Ctrl` + `F`
	*	`Erase`: **`Don't overwrite existing data (Quick)`** or **`Overwrite existing data with zeroes (slow)`**
	*	`Partitioning`: **`Compatitble with modern systems and hard disks > 2TB (GPT)`**
4.	Click `Format...`
5.	Again click on `Format` and wait..... Depends on what u selected (Quick) or (Slow)






## Moving MicroSD to SSD
### Without Video
1.	Login with your new created account as steps above
2.	After first login it will pop a annoying `Keyboard Shortcuts` window.... Close this
3.	And close the other welcome window...
4.	Open `Terminal` and type:
	```bash
	sudo apt update
	```
5.	Now download the files from JetsonHacks
	```bash
	git clone https://github.com/jetsonhacks/bootFromUSB
	```
6.	Enter the bootFromUSB folder
	```bash
	cd bootFromUSB
	```






### With Video
1.	I guess better just to follow his YouTube guide
	<iframe width="560" height="315" src="https://www.youtube.com/embed/53rRMr1IpWs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

	And this will help aswell: [bootFromUSB](https://github.com/jetsonhacks/bootFromUSB)








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

