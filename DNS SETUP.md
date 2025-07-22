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
* 
