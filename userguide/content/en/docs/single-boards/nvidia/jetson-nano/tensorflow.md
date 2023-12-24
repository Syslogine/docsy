---
linktitle: TensorFlow
title: TensorFlow 2.4 Installation on Nvidia Jetson Nano
categories: ["jetson nano"]
---

## **Python API Installation**

### **1. Update and Upgrade System Packages**
```bash
sudo apt update
sudo apt upgrade
```
Ensures your system is up-to-date.

### **2. Install pip and pip3**
```bash
sudo apt install python-pip python3-pip
```
Installs pip for Python 2 and Python 3.

### **3. Uninstall and Reinstall Numpy**
```bash
sudo -H pip3 uninstall numpy && sudo -H pip3 install numpy==1.18.5
```
Ensures the correct version of Numpy is installed.

### **4. Remove Old TensorFlow Versions**
```bash
sudo pip uninstall tensorflow && sudo pip3 uninstall tensorflow
```
Removes any existing TensorFlow installations.

### **5. Install Dependencies**
```bash
sudo apt install gfortran -y &&\
sudo apt install libhdf5-dev libc-ares-dev libeigen3-dev -y &&\
sudo apt install libatlas-base-dev libopenblas-dev libblas-dev -y &&\
sudo apt install liblapack-dev -y &&\
sudo -H pip3 install Cython==0.29.21
```
Installs necessary dependencies.

### **6. Install H5py with Specific Cython Version**
```bash
sudo -H pip3 install h5py==2.10.0
sudo -H pip3 install -U testresources numpy
```
Installs H5py with specific Cython version.

### **7. Upgrade Setuptools and Install Additional Packages**
```bash
sudo -H pip3 install --upgrade setuptools
sudo -H pip3 install pybind11 protobuf google-pasta
sudo -H pip3 install -U six mock wheel requests gast
sudo -H pip3 install keras_applications --no-deps
sudo -H pip3 install keras_preprocessing --no-deps
```
Upgrades setuptools and installs additional packages.

### **8. Install gdown to Download from Google Drive**
```bash
sudo -H pip3 install gdown
```
Installs gdown.

### **9. Download TensorFlow Wheel**
```bash
gdown https://drive.google.com/uc?id=1DLk4Tjs8Mjg919NkDnYg02zEnbbCAzOz
```
Downloads TensorFlow wheel from Google Drive.

### **10. Install TensorFlow**
```bash
sudo -H pip3 install tensorflow-2.4.1-cp36-cp36m-linux_aarch64.whl
```
Installs TensorFlow.

## **TensorFlow 2.4 C++ API Installation**

### **1. Update and Upgrade System Packages**
```bash
sudo apt update
sudo apt upgrade
```
Ensures your system is up-to-date.

### **2. Remove Old TensorFlow Versions**
```bash
sudo rm -r /usr/local/lib/libtensorflow*
sudo rm -r /usr/local/include/tensorflow
```
Removes any existing TensorFlow installations.

### **3. Install Dependencies**
```bash
sudo apt install wget curl libhdf5-dev libc-ares-dev libeigen3-dev
sudo apt install libatlas-base-dev zip unzip
```
Installs necessary dependencies.

### **4. Install gdown to Download from Google Drive**
```bash
pip install gdown
```
Installs gdown.

### **5. Download TensorFlow C++ API Tarball**
```bash
gdown https://drive.google.com/uc?id=1zJ_EF2aFkr8JU8JgTLfKMxC6KxE3DRD4
```
Downloads TensorFlow C++ API tarball from Google Drive.

### **6. Unpack the Tarball**
```bash
sudo tar -C /usr/local -xzf libtensorflow-2.4.1-JetsonNano.tar.gz
```
Unpacks the tarball.

Now your Nvidia Jetson Nano is equipped with TensorFlow 2.4, ready to empower your machine learning projects!
