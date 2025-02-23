---
linktitle: Wipe disks with dd
title: Wipe your SD/SSD disks with dd
tags: ['Wipe', 'sd', 'ssd', 'disks', 'dd']
categories: ["Ubuntu"]
weight: 2
---

soo i found this on the internet and i thought its very useful to make sure your micro SD card is nulled so we can make a fresh clean install on the SD and be sure there no left overs on the card

So i know there are more ways to do this but this is what i found and also use


You can wipe the SD card out by the following command (let's assume, that your SD card is /dev/sdb):
and to be really sure use the
```bash
lsblk
```
So now we know for sure it's on the right one let's go to the next step

Do not interrupt this command or it could possibly brick the SD card.
```bash
sudo dd if=/dev/zero of=/dev/sdd bs=8192
```
<b>Note:</b> If this command does not complete successfully and you have to abort it, then most likely it is recoverable with disk partition recovery programs covered in other posts.
It can take some time depending on size and speed of SD card.

If you are convinced, that CIA would like to recover your files, then overwrite the SD card with urandom instead of zero:
```bash
sudo dd if=/dev/urandom of=/dev/sdd bs=8192
```
dd command from above examples will erase whole SD card, leaving it without any partitions, even with no partition table. So you will need to recreate partition on SD card. You can do this by any partitioning tool like cfdisk, parted (my recommendation) or gparted.<br>
And one more thing: <b>be extremely careful when calling dd command</b>. A typo in `of=` argument value can cause disaster.