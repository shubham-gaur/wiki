---
title: Automount USB
description: Mount USB drives in raspberry-pi
published: true
date: 2021-10-09T16:11:33.730Z
tags: 
editor: markdown
dateCreated: 2021-10-09T16:11:12.336Z
---

# USB Mount

* Check blkid of partitions
`sudo blkid`

* Check fstab status
```
pi@raspberrypi:~ $ sudo cat /etc/fstab
proc            /proc           proc    defaults          0       0
PARTUUID=6f8ee2db-01  /boot           vfat    defaults          0       2
PARTUUID=6f8ee2db-02  /               ext4    defaults,noatime  0       1
# a swapfile is not a swap partition, no line here
#   use  dphys-swapfile swap[on|off]  for that
```

* Update fstab for dev partion to be auto mounted across restarts
`PARTUUID=244E-F1E2 /media/usbdrv ext4 defaults,nofail 0 0`

* Create a mount point
`sudo mkdir /media/usbdrv`

* *umask* is required to provide write and read permissions in drive
`sudo mount /dev/sda1 /media/usbdrv -o umask=000`

> Warning: Mount has to be triggered after replugging drive