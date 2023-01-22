---
linktitle: Upgrade Python
title: Upgrade Python

---

### Version Check
Run below command to test the current version installed of python.
```bash
python3 --version
```

OUTPUT:
```txt
Python 3.6.9
```


### Download and Install Python 3.7

Update the packages list
```bash
sudo apt update
```

Install Python 3.7
```bash
sudo apt-get install python3.7 -y
```


### Add python 3.6 & python 3.7 to update-alternatives
erer
```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 1
```
```bash
sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.7 2
```


### Update python 3 to point to python 3.7
By default, Python 3.6 is pointed to Python 3. That means when we run python3 it will execute as python3.6 binary but we want to execute this as python3.7.

Type this command to configure python3:
```bash
sudo update-alternatives --config python3
```
You should get the above output. Now type 2 and hit enter for Python 3.7. Remember the selection number may differ so choose the selection number which is for Python 3.7.


### Alternative update python 3 to point to python3.7
/usr/bin/python3 is just a symlink. Delete it and make a new symlink to
python3.7:
```bash
sudo rm /usr/bin/python3
sudo ln -s python3.7 /usr/bin/python3
```

### Test the new version of python3
```bash
python3 -V
```
OUTPUT:
```txt
Python 3.7.5
```




