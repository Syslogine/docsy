---
linktitle: Upgrade Python
title: Upgrade Python to Version 3.7 on Ubuntu
categories: ["jetson nano"]
---

## **Version Check**

Run the following command to check the current version of Python installed:
```bash
python3 --version
```

**Output:**
```txt
Python 3.6.9
```

## **Download and Install Python 3.7**

Update the packages list:
```bash
sudo apt update
```

Install Python 3.7:
```bash
sudo apt-get install python3.7 -y
```

## **Add Python 3.6 & Python 3.7 to update-alternatives**

Add Python 3.6 and Python 3.7 to the update-alternatives system:
```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
```
```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
```

## **Update Python 3 to Point to Python 3.7**

Configure Python 3 to use Python 3.7:
```bash
sudo update-alternatives --config python3
```
Choose the selection number corresponding to Python 3.7.

## **Alternative: Update Python 3 to Point to Python 3.7**

If you prefer a direct symlink update, run the following commands:
```bash
sudo rm /usr/bin/python3
sudo ln -s python3.7 /usr/bin/python3
```

## **Test the New Version of Python3**

Check the new Python 3 version:
```bash
python3 -V
```

**Output:**
```txt
Python 3.7.5
```

Now you have successfully upgraded Python to version 3.7 on your Ubuntu system. This is particularly useful for accessing the latest features and improvements in Python 3.7.