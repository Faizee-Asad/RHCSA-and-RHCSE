# Accessing DVD ROM

1. Mount DVD ROM on mount point.
```
# ls /mnt
# mount /dev/sr0 /mnt
```
2. Access data via mount point
```
# ls /mnt
```
3. Unmount DVD Rom from mount point
```
# unmount /mnt
# ls /mnt
```
* Deviec driver for DVD Rom is /dev/sr0
* /mnt is by default available in Linux for mounting DVD Rom or USB drive
* Installation DVD of RHEL 9 contains setup of 9000+ opensouce software.

# Creating and Accessing ISO image

* Steps to manages and IOS image of a DVD Rom.
1. Create an ISO image from a DVD Rom
```
# dd if=/dev/sr0 of=/usr/sbin/rhel9.iso (if - input file and of - output file)
# dd is an inbuilt utility to create ISO images
```
2. Verify the new ISO image file
```
# ls -lh /usr/sbin/rhel9.iso
```
3. Mount ISO image on a directory
```
# mount -o lopp /usr/sbin/rhel9.iso /mnt
# loop is the logical device driver for ISO images
```
4. Make mounting persistent
```
# echo "/usr/sbin/rhel9.iso /mnt iso9660 defaults 0 0" >> /etc/fstab
# /etc/fstab is a file used for storing persistent mount entires
# reboot
# ls /mnt
```
