# Task 1: Force Linux to use kernel assigned drivers for netwrok cards:
*'udevd' Utility renames kernel asssigned device drivers to BIOS assigned device drivers for netwrok cards. It technically makes no difference, but we still have to stop this renaming:

* Step 1 : Identify the device driver of your network card.
```
# dmesg | grep eth
```
* Step 2: Edit grup to disable the renaming of the device driver.
```
# vi /etc/default/grub
```
* Step 3: Add some parameter
```
add net.ifnames=0 biosdevname=0 at the end of line stating with CMDLINE_LINUX
## You can also sed command to add
# sed -i '/CMDLINE/' s/"\(.*\)"/"\1 net.ifnames=0 biosdevname=0"/' /etc/default/grub
```
* Step 4: Apply Changes to the main GRUB2 config file
```
# grub2-mkconfig -o /boot/grub2/grub.cfg

ouput:
done - it indicates you did no mistake
```
Step 5: Reboot the server to apply the changes.
```
# reboot
```
Step 6: After reboot, confirm that the device driver name did not change
```
# dmesg | grep eth
(no outpu)
```

# Task 2: Configure IP with 'nmcli' utility

* Step 1: Check Network Manager Service Active and Enable
```
# systemctl status NetwrokManager
press q to exit
```
* Step 2: list all connections in nmcli
```
# nmcli con show
```
* Step 3: Delete a network connection from nmcli
```
# nmcli con del "Wired connection 1"
# nmcli con del "enp1s0"
# nmcli con show
```
* Step 4: Add a netwrok connection in nmcli
```
# nmcli con add con-name eth0 ifname eth0 type ethernet save yes
# nmcli con show
```
Step 5: Configure IPv4 and IPv6  address  (Dual stock) on a network connection
```
# nmcli con mod eth0 ipv4.addresses 10.0.0.111/24 ipv4.method manual ipv6.addresses 10::111/64 ipv6.method manual
```
Step 6: Restart NetworkManager serivce and  apply new changes
```
# nmcli con reload
# nmcli con down eth0
# nmcli con up eth0 
```
Step 7: Check the IP
```
# ip a s
```
