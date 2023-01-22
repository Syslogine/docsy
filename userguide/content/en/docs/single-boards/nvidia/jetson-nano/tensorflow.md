---
linktitle: TensorFlow
title: TensorFlow
---



1.	get a fresh start
	```bash
	sudo apt update
	sudo apt upgrade
	```
2.	install pip and pip3
	```bash
	sudo apt install python-pip python3-pip
	```
3.	remove old versions, if not placed in a virtual environment (let pip search for them)
	```bash
	sudo pip uninstall tensorflow
	sudo pip3 uninstall tensorflow
	```
4.	install the dependencies (if not already onboard)
	```bash
	sudo apt install gfortran &&\
	sudo apt install libhdf5-dev libc-ares-dev libeigen3-dev &&\
	sudo apt install libatlas-base-dev libopenblas-dev libblas-dev &&\
	sudo apt install liblapack-dev &&\
	sudo -H pip3 install Cython==0.29.21
	```
5.	install h5py with Cython version 0.29.21 (± 6 min @1950 MHz)
	```bash
	sudo -H pip3 install h5py==2.10.0
	sudo -H pip3 install -U testresources numpy
	```
6.	upgrade setuptools 39.0.1 -> 53.0.0
	```bash
	sudo -H pip3 install --upgrade setuptools
	sudo -H pip3 install pybind11 protobuf google-pasta
	sudo -H pip3 install -U six mock wheel requests gast
	sudo -H pip3 install keras_applications --no-deps
	sudo -H pip3 install keras_preprocessing --no-deps
	```
7.	install gdown to download from Google drive
	```bash
	sudo -H pip3 install gdown
	```
8.	download the wheel
	```bash
	gdown https://drive.google.com/uc?id=1DLk4Tjs8Mjg919NkDnYg02zEnbbCAzOz
	```
9.	install TensorFlow (± 12 min @1500 MHz)
	```bash
	sudo -H pip3 install tensorflow-2.4.1-cp36-cp36m-linux_aarch64.whl
	```


## TensorFlow 2.4 C++ API.
If you are planning to program in C++, you will  need the C++ API build of TensorFlow instead of the Python version. Installing the C ++ library using the pre-build tarball from our GitHub page saves you a lot of time. Please follow the procedure below.

1.	get a fresh start
	```bash
	sudo apt-get update
	sudo apt-get upgrade
	```
2.	remove old versions (if found)
	```bash
	sudo rm -r /usr/local/lib/libtensorflow*
	sudo rm -r /usr/local/include/tensorflow
	```
3.	the dependencies
	```bash
	sudo apt-get install wget curl libhdf5-dev libc-ares-dev libeigen3-dev
	sudo apt-get install libatlas-base-dev zip unzip
	```
4.	install gdown to download from Google drive (if not already done)
	```bash
	pip install gdown
	```
5.	download the tarball
	```bash
	gdown https://drive.google.com/uc?id=1zJ_EF2aFkr8JU8JgTLfKMxC6KxE3DRD4
	```
6.	unpack the ball
	```bash
	sudo tar -C /usr/local -xzf libtensorflow-2.4.1-JetsonNano.tar.gz
	```











