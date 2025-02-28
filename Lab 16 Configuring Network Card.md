# Before configure let's understand Basic of networking

* A Network Interface Card is required on every device to get connected on network.
* A NIC is also known as ethernet card.
* There can multiple ethernet cards on a server.
* Since ethernet card is a hardware, it will need device driver to functions on the OS.
* Linux kernel assigns **/dev/eth** series drivers to ethernet cards.
* e.g /dev/eth0, /dev/eth1, /dev/eth2 and so no.
* **dmesg|grep eth** is used to know the available ethernet cards.
* Boteh kernel and the BIOS assigns device drivers to ethernet cards.
* From kernel version 3.x onwards, the udevd utility renames kernel assigned drivers with BIOS assign drivers.
* Sometimes, it is difficult to remember this drivers.
* we can stop this renaming of drivers by performing following steps,
```
# vi /etc/default/grub
  add net.ifnames=0 biosdevname=0 at the end of line starting with CMDLINE_LINUX
# grub2mkconfig -o /boot/grub2/grub.cfg
# reboot
```

* Every ethernet card has a globally unique 48bit address called MAC addess (2a:3b:1c:09:34:d8).
* Also, every device needs an IP address for communication.
* There are 2 families of IP address: IPv4 and IPv6.
* IPv4 is a 32-bit decimal address divided into 4 octets.
* IPv4 range: 0.0.0.0 - 255.255.255.255
* **IANA** divided IPv4 addresses into multiple Class
```
Class  Range    Prefix  Mask            IP scope
A      1-126    /8      255.0.0.0       16,777,216 addresses per netwrok
B      128-191  /16     255.255.0.0     65,536 addresses per netwrok
C      192-223  /24     255.255.255.0   256 addresses per netwrok
```
```
10.0.0.0/8
10.10.0.0/16
10.10.10.0/24
```
* **IANA** also divided IPv4 addresses into 2 types: **Private IP** and **Public IP**.
* Private IP addresses can be used within a private network.
* Private IP cannot travel on public network like internet.
* For communication on internet, only Public IP must be used.

* All IP addresses of class A,B and C are public. But IANA has reserved a range of addresses in each class as private.
* Private IP addresses ranges are:
```
10.0.0.0 - 10.255.255.255
172.16.0.0 - 172.31.255.255
192.168.0.0 - 192.168.255.255
```
* 127.0.0.0/8 is reserved for loop back purpose.
* Every computer has a default logical network interface called **loopback** interface with IP address _**127.0.0.1**_.

* IPv6 addresses are 128-bit long hexa-decimal address with a default fixed mask 64 bits.
* e.g 3ffe:0c1a:0000:73b9:2201:af1b:6c00:093b/64
```
0000 --> ffff
no private and public separate range
IPv4 + IPv6 = Dual Stock
10::1/64
10::2/64
``` 
* Device can communicate directly only if their IP address belong to same network.
* For devices that are in different network to communicate with each other , We need a **Router**.
* Router routes between 2 or more networks.
* Router can also connect a private network with internet..
* Router's IP address is called default gateway address in the OS.
* To secure access of a network or resources in a network from hackera and unauthorized access we need to deploy a **Firewall**.
* Firewall filters the incoming and outgoing traffic of a network using various factors like Source/destination address, protocol (tcp,udp,icmp) and service port number.

```
Manual --> admin assigned (fixed)
Auto --> DHCP assigned (random)

eth0 (mac address)
  |__ IP address/ Mask
  |__ Gateway address

```

# Link Aggregation
* Ehternet cards with fixed  bandwidth (10mbps, 100mbps, 1gbps, 10gbps, 100gbps).
* If bandwidth of a single network card on a server is insufficient to handle network payload, then we can add more network cards on the server and logically group them to increase throughput.
* This machanism is called link aggregation.
* In link aggregation, a logical network interface called bond interface is created.
* Bond interface becomes the **master** and the physical cards (eth0, eth1) become **slave of bond**.
* IP address is configure on bond anf not on physical cards.
* MAC address still stays on physical cards.
* All the network traffic will be load balanced between slave cards by bond interface, thus provide **High throughput**.
* Also, if one of the network cards fails, bond continues the communication with rest network cards in the group, thus providing **redundancy (failover) of network cards**.
* LACP protocol is used.
* A single bond interface can have up to 16 network cards. 

![Screenshot_20250225-112117 1](https://github.com/user-attachments/assets/77030bdc-dea8-46bd-ab28-6b348fcbff54)



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
![WhatsApp Image 2025-02-25 at 14 55 48_cabb3830](https://github.com/user-attachments/assets/5e75205e-3015-4143-ae72-4a842512cdf9)


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
