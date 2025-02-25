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

# Task 3: Configuure Link Aggregation with 'nmcli' utility
* Link Aggregation means grouping multiple network cards on server to form a logincal netwrok card. it is mainly used to increase the troughput of server's network connection.

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
# nmcli con del "Wired connection 2"
# nmcli con del "enp1s0"
# nmcli con show
```
* Step 4: Create a new "bond" interface
```
# nmcli con add con-name bond0 ifname bond0 type bond save yes
# nmcli con show

```
* Step 5: Add 'eth0' and 'eth1' netwrok connection in nmcli as slaves of 'bond0'
```
# nmcli con add con-name eth0 ifname eth0 type bond-slave master bond0 save yes
# nmcli con add con-name eth1 ifname eth1 type bond-slave master bond0 save yes
# nmcli con show

```
*  Step 6: Configure IPv4 and IPv6  address  (Dual stock) on bond network connection
```
# nmcli con mod bond0 ipv4.addresses 10.0.0.50/24 ipv4.method manual ipv6.addresses 10::50/64 ipv6.method manual
```
*  Step 7: Restart NetworkManager serivce and  apply new changes
```
# nmcli con reload
# nmcli con down bond0
# nmcli con down eth0
# nmcli con down eth1
# nmcli con up bond0
# nmcli con up eth0
# nmcli con up eth1
```
* Step 8: Check the IP
```
# ip a s
```
* Step 9: Test connectivity with other  machince in the netwrok
```
# ping -c 3 10.0.0.50
# ping 10::50 -c 3
# ping 10.0.0.111 -c 3
# ping 10.0.0.112 -c 3
# ping 10::111 -c 3 
```

___________________________________________________________________________________________________________________________________________________________________________

![{5F6F98FC-4293-4A19-AA08-FE421BC3993C}](https://github.com/user-attachments/assets/eea228b3-5c63-4450-86d7-c15004aa651d)
![Uploading WhatsApp Image 2025-02-25 at 14.55.48_cabb3830.jpg…]()


```
server 1(HOST OS): GUI Server 2,3,4(GUEST OS): CLI

server 2:
dmesg|grep eth
sed -i '/CMDLINE/  s/"\(.*\)"/"\1 net.ifnames=0 biosdevname=0"/'  /etc/default/grub
grub2-mkconfig -o /boot/grub2/grub.cfg
reboot
dmesg|grep eth    (no output)
systemctl status NetworkManager
nmcli con show
nmcli con delete "connection_name"
nmcli con add con-name eth0 ifname eth0 type ethernet save yes
nmcli con show
nmcli con mod eth0 ipv4.addresses 10.0.0.111/24 ipv4.method manual ipv6.addresses 10::111/64 ipv6.method manual
nmcli con reload
nmcli con down eth0
nmcli con up eth0
ip a s
===========================================================================================
server 3:
dmesg|grep eth
sed -i '/CMDLINE/  s/"\(.*\)"/"\1 net.ifnames=0 biosdevname=0"/'  /etc/default/grub
grub2-mkconfig -o /boot/grub2/grub.cfg
reboot
dmesg|grep eth    (no output)
systemctl status NetworkManager
nmcli con show
nmcli con delete "connection_name"
nmcli con add con-name eth0 ifname eth0 type ethernet save yes
nmcli con show
nmcli con mod eth0 ipv4.addresses 10.0.0.112/24 ipv4.method manual ipv6.addresses 10::112/64 ipv6.method manual
nmcli con reload
nmcli con down eth0
nmcli con up eth0
ip a s
ping 10.0.0.111 -c 4
ping 10::111 -c 3

===========================================================================================
server 4:
dmesg|grep eth
sed -i '/CMDLINE/  s/"\(.*\)"/"\1 net.ifnames=0 biosdevname=0"/'  /etc/default/grub
grub2-mkconfig -o /boot/grub2/grub.cfg
reboot
dmesg|grep eth    (no output)
systemctl status NetworkManager
nmcli con show
nmcli con delete "connection_name"
nmcli con show
nmcli con delete "connection_name"
nmcli con add con-name bond0 ifname bond0 type bond save yes
nmcli con add con-name eth0 ifname eth0 type bond-slave master bond0 save yes
nmcli con add con-name eth1 ifname eth1 type bond-slave master bond0 save yes
nmcli con show

nmcli con show
nmcli con mod bond0 ipv4.addresses 10.0.0.50/24 ipv4.method manual ipv6.addresses 10::50/64 ipv6.method manual
nmcli con reload
nmcli con down bond0
nmcli con up bond0
ip a s
ping 10.0.0.111 -c 4
ping 10::111 -c 3
```
