---
linktitle: OpenCV
title: OpenCV

---




## Install OpenCV 4.6
By default on the jetson nano we have OpenCV 4.1.x installed and as i like to have everything up to date we also going to update this one.

### Step 01

1.	a fresh start, so check for updates
	```bash
	sudo apt update
	```
	```bash
	sudo apt upgrade
	```
2.	install nano
	```bash
	sudo apt install nano
	```
3.	install dphys-swapfile
	```bash
	sudo apt install dphys-swapfile -y
	```
4.	enlarge the boundary (4.5.2 and higher)
	```bash
	sudo nano /sbin/dphys-swapfile
	```
	1.	Find: `CONF_MAXSWAP=2048`
	2.	Replace: `CONF_MAXSWAP=6144`
5.	give the required memory size
	```bash
	sudo nano /etc/dphys-swapfile
	```
	1.	Find: `#CONF_SWAPSIZE=`
	2.	Replace: `CONF_SWAPSIZE=6144`
6.	reboot afterwards
	```bash
	sudo reboot
	```
*	See more about [GB to MB](https://www.gbmb.org/gb-to-mb)


### Step 02
1.	check your memory first
	```bash
	free -m
	```
2.	you need at least a total of 8.5 GB!
	if not, enlarge your swap space as explained in the guide
	```bash
	wget https://github.com/Qengineering/Install-OpenCV-Jetson-Nano/raw/main/OpenCV-4-6-0.sh
	```
	```bash
	sudo chmod 755 ./OpenCV-4-6-0.sh
	```
	```bash
	./OpenCV-4-6-0.sh
	```
3.	once the installation is done...
	```bash
	rm OpenCV-4-6-0.sh
	```
4.	remove the dphys-swapfile now
	```bash
	sudo /etc/init.d/dphys-swapfile stop
	```
	```bash
	sudo apt-get remove --purge dphys-swapfile
	```
5.	just a tip to save an additional 275 MB
	```bash
	sudo rm -rf ~/opencv
	```
	```bash
	sudo rm -rf ~/opencv_contrib
	```

### Step 03
1.	reveal the CUDA location
	```bash
	sudo sh -c "echo '/usr/local/cuda/lib64' >> /etc/ld.so.conf.d/nvidia-tegra.conf"
	sudo ldconfig
	```
2.	third-party libraries
	```bash
	sudo apt install build-essential cmake git unzip pkg-config zlib1g-dev
	sudo apt install libjpeg-dev libjpeg8-dev libjpeg-turbo8-dev
	sudo apt install libpng-dev libtiff-dev libglew-dev
	sudo apt install libavcodec-dev libavformat-dev libswscale-dev
	sudo apt install libgtk2.0-dev libgtk-3-dev libcanberra-gtk*
	sudo apt install python-dev python-numpy python-pip
	sudo apt install python3-dev python3-numpy python3-pip
	sudo apt install libxvidcore-dev libx264-dev libgtk-3-dev
	sudo apt install libtbb2 libtbb-dev libdc1394-22-dev libxine2-dev
	sudo apt install gstreamer1.0-tools libgstreamer-plugins-base1.0-dev
	sudo apt install libgstreamer-plugins-good1.0-dev
	sudo apt install libv4l-dev v4l-utils v4l2ucp qv4l2
	sudo apt install libtesseract-dev libxine2-dev libpostproc-dev
	sudo apt install libavresample-dev libvorbis-dev
	sudo apt install libfaac-dev libmp3lame-dev libtheora-dev
	sudo apt install libopencore-amrnb-dev libopencore-amrwb-dev
	sudo apt install libopenblas-dev libatlas-base-dev libblas-dev
	sudo apt install liblapack-dev liblapacke-dev libeigen3-dev gfortran
	sudo apt install libhdf5-dev libprotobuf-dev protobuf-compiler
	sudo apt install libgoogle-glog-dev libgflags-dev
	```










