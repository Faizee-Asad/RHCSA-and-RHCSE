## What is SELinux?

* Stands for Security Enhanced Linux
* A linux kernel security module
* Provides additional layer of access control and Mandatory Access Control (MAC) to enhance the security.

* A project of US NSA (National Security Agency) with SELinux Community

## DAC vs MAC
* DAC - Discretionary Access Control
* chmod
* users
* -rwx  rw-  r--

## SELinux Options

* Enforcing (By default enable in Redhat)
* Permissive (disable but logs the activity)
* Disable

## How to check SElinux status?
```
# sestatus
# getenforce
```

## Change SELinux settings?
```
# setenforce 0 = Permissive/Disable
# setenforce 1 = Enable
```

## Change SELinux settings permanent?

* /etc/selinux/config
* SELINUX=enforcing/disable/permissive

## Create a file before rebooting
```
#fixfiles -F onboot
/.autorelable
```
* To prevent incorrectly labeled and unlabeled files causing problems, SELinux automatically relables file system when chaning from the disable state to permissive or enforcing mode.
* Before rebooting the system for relabeling, make sure the system will boot in permissive mode, for example by using the enforcing = 0 kernel option.

* !!! Warning !!!
* Its a good practice to take snapshot of your system before making change to SELinux

## Two main concepts of SElinux
* Labrling
* Type enforcement

## To check the label if a file or a directory
```
# ls -lZ
```

## To check the label of a process (ex:httpd)
```
# ps axZ | grep httpd
```

## To check the lable of a socket (ex:httpd)
```
# netstate -taZ | grep https
```

## Checking error related to SELinux
```
# journalctl
```

## Change type in a label
```
chcon -t <TYPE> FILENAME
```
## Where the context stored?

etc/selinux/contexts/files/file_coontexts

# Boolean
* Just by setting some pre-defined properties to either ON or OFF
* EX: ftp server to access home dir

# To check Boolean
```
# getsebool -a
# semange boolean -l
```

# to set boolean
```
# setsebool -P bool_name on/off
```
______________________________________________________________________________________________________________________________

# How to install SELinux on Ubuntu Server 22.04

# Remove apparmor
```
AppArmor is a Linux kernel security module that enhances Ubuntu's security by restricting the capabilities of applications.
```

## The first thing to do is remove AppArmor. Log into your Ubuntu Server and stop the service with the command:
```
sudo systemctl stop apparmor
```
## Now we can remove AppArmor with the command:
```
sudo apt-get remove apparmor -y
```
## Once AppArmor has been removed, reboot your system with:
```
sudo reboot
```

# How to install SELinux
## Now we can install SELinux. Back at the terminal window, issue the command:
```
sudo apt-get install policycoreutils selinux-utils selinux-basics -y
```
## When the installation completes, activate SELinux with the command:
```
sudo selinux-activate
```
## Set SELinux to enforcing mode with:
```
sudo selinux-config-enforcing
```
## Finally, reboot your system once again with:
```
sudo reboot
```
## When the system comes back up, check to make sure SELinux is enabled with the command:
```
sestatus
```
## You should see something like:
```
SELinux status: enabled
SELinuxfs mount: /sys/fs/selinux
SELinux root directory: /etc/selinux
Loaded policy name: default
Current mode: permissive
Mode from config file: enforcing
Policy MLS status: enabled
Policy deny_unknown status: allowed
Memory protection checking: requested (insecure)
Max kernel policy version: 31
```
## And that’s all there is to install SELinux on Ubuntu Server 20.04. If you’re already familiar with this security system, you can jump in and start securing your server.

## Reference (https://www.techrepublic.com/article/how-to-install-selinux-on-ubuntu-server-20-04/)

______________________________________________________________________________________________________________________________________

# GOt an issue after enable and reboot. filed to start relabe all file system.

1. Reboot the system.
2. press shift to GRUB Scrren
3. select the first Ubuntu kernel and press e to edit.
4. find starting line
```
linux /vmlinx...
```
5. Go to end of that line remove 0 and add this :
```
security=selinux selinux=0 enforcing=0 init=/bin/bash
```
6. press ctrl+X or F10 to boot.

7. remount the root filesystem as read write.
```
# mount -o remount,rw /
```
8. Edit the SELinux config file
```
nano /etc/selinux/config
```
```
SELINUX=disable
```
9. SAVE THE FILE WITH:
```
Ctrl+O then enter
Ctrl+X to exit 
```
10. sync and reboot
```
reboot -f
```

___________________________________________________________________________________
