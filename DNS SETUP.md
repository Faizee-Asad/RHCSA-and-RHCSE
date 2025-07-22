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
* 
