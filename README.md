Before you start, make sure you have a USB drive an Arch Linux ISO image. It is also important that you have a stable and fast internet connection, as you will need to download packages during the installation. This guide uses kernel: 6.2.1.

##  0-Set up your keyboard the way you want (Optional)
```
loadkeys YOURDISTRIBUTION (en=english, es=spanish, etc.)
```

##  1-Wifi (Optional)
```
iwctl
|_  device list
    |_  station YOURNETWORK connect "NAME OF YOUR NETWORK"
```

##  2-Create and resize partitions (part 1)
```
lsblk
|_  gdisk /dev/DISK TO ERASE
    |_  z
        |_  x
            |_  z
                |_  y
                    |_  y
```

##  3-Create and resize partitions (part 2)
```
cfdisk
|_  gpt
    |_  
```
