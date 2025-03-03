# FTP Server

* File Transfer Protocol Service is used to upload or download data on or from the server.
* It is a TCP based service.
* It is uses **TCP port 21** to connect with clients and **TCP port 20** for data transfer.
* vsftpd application is used to make a linux system as an FTP server.
* ftp tool is used on client to connect with server.
```
                -- cli ftp tool
Client Tools --
                -- winscp, lftp, sftp, filezilla
```
* By default, FTP server works as an anonymous server (where login happen with anonymous user)
* (Disable anonymous login and enable real user login)
* **Application name: vsftpd**
* **Service name: vsftpd**
* **Main config file: /etc/vsftpd/vsftpd.cong**

* Linux server has an in-built firewall to protect itself from unauthorized data payloads.
* **firewalld** serivce works as the firewall.
* By default, firewalld allow SSH, cockpit and DHCP client payloads only (ICMP Ping)
* On FTP server, we need to allow FTP payload on firewall.
* **setlinux** is the application-level security and should be disabled on FTP server.

# Centralized DNF (Installer)

* In a datacenter, it is preferred to centralize package (software) management by implementing a centralized DNF solution.
* A DNF server will act as a central repository for all rpm packages.
* All other linux servers will act as client and will download required rpm packages from DNF server for installation.
* DNF server will use FTP service in background to allow donwload of rpm packages on all other linux.

![1740999676472](https://github.com/user-attachments/assets/bdada5bf-d898-43ca-a0f2-5daa779e1d2b)
