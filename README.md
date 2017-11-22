# ALIXBoard
How to install an OS on a memory card for PCEngines ALIX board (or raspberry pi) on OSX


- Install VirtualBox
- Download a linux iso (make sure it is a 32-bit version)
- create a VM with a virtual disk that is a bit smaller than the size of your memory card (SD, CF, usb, whatever).  Use the slider to set the size, as the disk has to fit block boundaries. Initialize it as a fixed size disk, and not dynamically allocated.
- install os on the virtual disk, then shut down
- convert the disk to a raw image: 
```
VBoxManage clonehd VirtualBox\ VMs/blossom/blossom.vdi blossom.raw --format RAW
```
- copy to memory car using dd
```
dd if=blossom.raw bs=1m | pv | sudo dd of=/dev/rdisk2 bs=1m
```
- after the copy, make a vmdk that points to the memory card
```
ls -l /dev/disk2
sudo chown tschweiger /dev/disk2
VBoxManage internalcommands createrawvmdk -filename blossom.vmdk -rawdisk /dev/disk2
```
- create a new VM that uses this disk and make sure it runs ok

If the raw disk is bigger than the memory card, use parted to resize the swap partition, so that the needed parts are actually on the disk.


