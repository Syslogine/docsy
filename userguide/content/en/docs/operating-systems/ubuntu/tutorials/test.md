---
linktitle: "Tips and Tricks"
title: Useful tips and tricks for Ubuntu
tags: ['ubuntu','tips','tricks']
weight: 1
---

## apt fun

### apt update
  Before we begin we update our packages list
  ```bash
  sudo apt update
  ```

### apt upgrade
When we have packages that can be upgraded we do
```bash
sudo apt upgrade
```
After this command it will ask if you would like to proceed so press `Y` then `ENTER`



### apt update && upgrade
Now we can run these commands also just in one command by

```bash
sudo apt update && sudo apt upgrade -y
```

### apt install
By using this command we can install packagename.
```bash
sudo apt install packagename
```
NOTE: replace ```packagename``` with your package like ```filezilla```

### apt remove
if we want to remove the binaries, but not the configuration or data files of the ```packagename```
```bash
sudo apt remove packagename
```


### apt purge
if we wanna remove everything from this packagename, is this the way
```bash
sudo apt purge packagename
```
NOTE: replace ```packagename``` with you package like ```filezilla```


### apt clean
Always keep it clean..
```bash
sudo apt clean
```

## move 
### move item
This will be the command if need to move a item
```bash
mv /home/folder1/item /home/folder2/item
```

## rename
### rename file
well u can use the same command `mv` to rename like
```bash
sudo mv item1.txt item2.txt
```


## copy 
### copy item
to copy a item use this
```bash
cp /home/folder/item /home/folder/item1
```

## create folder/item
### create item
if you want to create a item but no content in it.
```bash
touch /home/item
```
If wanna create a item but with content
```bash
nano /home/item
```
### create folder
yes we all need to create folders.
```bash
mkdir /home/folder
```

## remove item/folder
### remove item
```bash
rm /home/item
```

### remove folder
```bash
rm -r /home/folder
```

## go/back folder
### go folder forwards
```bash
cd folder
```

### go folder back
```bash
cd ..
```

## shutdown/restart

### reboot server
To restart server us this
```bash
sudo reboot now
```
This will work aswell
```bash
sudo reboot .
```

### shutdown server
If u want to shutdown the server use
```bash
sudo shutdown now
```
or you can use this to poweroff you're machine 
```bash
sudo poweroff
```


## Other
### enter root account
sometimes we need to have the root account

Here it will ask to promt `root` password
```bash
su -
```

This one will ask the password of current user
```bash
sudo su -
```

### clear
so now you have allot of text in your command console and like to celan it up...
```bash
clear
```

### force package upgrade
Well some times u got a issue a package needs to be upgraded but does not upgrade when use the command `apt upgrade`
```bash
sudo apt dist-upgrade
```

