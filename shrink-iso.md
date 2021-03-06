# Shrink your ISO

## Shrink it
* Mount the image using another Linux (a Raspberry-Pi works).
* Find the name of the device using *sudo fdisk -l* (in our case it's /dev/sda)
* Resize the filesystem
    * *sudo e2fsck -f /dev/sda2*
    * *sudo resize2fs /dev/sda2 2500M* (2.5G should be enough for us)
* Resize the partition
    * *sudo parted /dev/sda resizepart 2 2700M* (The partition must be larger than the file system)

##  Expand it on first boot
* Boot on the card freshly shrinked
* Run raspi-config to expand the partition
    * *sudo raspi-config --expand-rootfs*
* Halt the system

## Make an image file
 * copy the image using dd and count
    * *sudo dd bs=1m count=3000 if=/dev/rdisk2 of=$(date +%F)-poppy-ergo-jr.img*
