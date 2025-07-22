# What is DNS?
* DNS, or Domain Name System is the internet service that translates humnan-friendly domain names like www.example.com into machine-readable IP address.

# Lets setup our own webserver
* Installion (centos or redhat)
* Package we need to install
```
# sudo yum install httpd
# systemctl start/stop/status httpd (httpd is the proccess or service name)

* Enable the service in firewall
# firewall-cmd --add-service=http --permanent
# firewall-cmd-reload
```

# webserver config file under
* /var/www/html/index.html
* /etc/httpd/cong/httpd.conf

# Let's setup our own DNS Server
* Installion (centos or redhat)
* Package we need to install for the DNS is BIND (Berkeley Insternet Name Domain)
```
# sudo yum install bind bind-utils
# systemctl start/stop/status named (named is the proccess or service name)

* Enable the service in firewall
# firewall-cmd --add-service=dns --permanent
# firewall-cmd-reload
```
# DNS config file under
* /etc/named.conf
# Directory where all the zone filed are present where you define hostname to IP etc
* /var/named

# DNS Translate
* Hostname to 192.168.0.12 (called A Record)
* 192.168.0.12 to hostname ( called PTR Record)
* hostname to hostname (Called hostname Record)

# Zones files
* Forward zone - resolve Domain to IP
* Reverse zone - resolve IP to Domain

# Here's how to configure your DNS settings on different operating systems.
* Windows: Go to control panel > Network and internet > Network and sharing center > change adaptor settingd. Right click your network connections, select properties, then select internet protocol version 4 (TCP/IPv4) or internet protocol version 6 (TCP/IPv6) and click properties. here you can set your preferred DNS server.
* macOS: Go to system perferences > network , select your network interface, click advanced, and go to the DNS tab.you can add you DNS server here.
* Linux: This depends on your distribution and network manager inteface, click 
