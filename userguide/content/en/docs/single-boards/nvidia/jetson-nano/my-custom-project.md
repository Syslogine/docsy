---
title: My Custom AI project

---

List of dependencies i need for creatiing my project.



*	https://github.com/raymondlo84/nvidia-jetson-ai-monitor
*	https://github.com/OpenKinect/libfreenect



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

