# ALIXBoard
How to install an operating system on a memory card for PCEngines ALIX board (or raspberry pi, or otherwise make a disk image that you can copy onto some other physical medium) on OSX

- Install VirtualBox
- Download a linux iso (make sure it is a 32-bit version for the ALIX board)
- attach you memory card to the Mac, then unmount the disk and give yourself permissions (note that at different times you should check and re-asser the permissions):
```
diskutil list
diskutil info /dev/disk2
diskutil unmountDisk /dev/disk2
ls -l /dev/disk2*
sudo chmod 777 /dev/disk2*
```
- make a vmdk that points to the memory card, check and re-asser your permissions: 
```
VBoxManage internalcommands createrawvmdk -filename blossom.vmdk -rawdisk /dev/disk2
diskutil unmountDisk /dev/disk2
ls -l /dev/disk2*
sudo chmod 777 /dev/disk2*
```
- create a VM that points to the vmdk as its disk, and its optical drive to the ISO 
- start the VM and run your install.  After you partition the disk, check and re-assert permissions
- powerdown and boot again the VM (check and re-assert permissions)
- powerdown, and eject
```
diskutil eject /dev/disk2
```
- install into your ALIX board, power-up and celebrate!


# Below didn't work, but has useful commands

- Install VirtualBox
- Download a linux iso (make sure it is a 32-bit version for the ALIX board)
- create a VM with a virtual disk that is the same size a bit smaller than the size of your memory card (SD, CF, usb, whatever).  Use the slider to set the size, as the disk has to fit block boundaries, or else get the size of the card in bytes using `diskutil info /dev/diskX` and past that. Initialize it as a fixed size disk, and not dynamically allocated.
- install os on the virtual disk, then shut down
- convert the disk to a raw image: 
```
VBoxManage clonehd <hostname>.vdi <hostname>.raw --format RAW
```
- insert your memory card, find out where it is (/dev/disk2 in this example), and umnount it:
```
diskutil list
diskutil info /dev/disk2
diskutil unmountDisk /dev/disk2
```
- copy to memory card using dd.  Writing to 'rdiskX' instead of 'diskX' is about five times faster.
```
 sudo dd if=<hostname>.raw of=/dev/rdisk2 bs=1m
```
or if you want to see progress, install pv using homebrew:
```
dd if=<hostname>.raw bs=1m | pv | sudo dd of=/dev/rdisk2 bs=1m
```
- after the copy, make a vmdk that points to the memory card.  Take ownership of the card so that you can read from it.  
```
ls -l /dev/disk2
sudo chown <username> /dev/disk2
VBoxManage internalcommands createrawvmdk -filename blossom.vmdk -rawdisk /dev/disk2
```
- create a new VM that uses this disk and make sure it runs ok

If the raw disk is bigger than the memory card, use parted to resize the swap partition, so that the needed parts are actually on the disk.


