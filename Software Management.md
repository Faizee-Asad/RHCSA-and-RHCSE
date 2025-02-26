# Software Management

* The only way to install software in Windows is using **setup.exe** file.
* Linux does not support .exe files
* There are 2 methods to install software in Linux:
  1. Source code (tarball) method.
  2. Package method.

## Source code (tarball) method

* We dowload entire source code of the software from the internet.
* Source code is a folder containing all the raw files used to build a software.
* The source code contains in-built scripts to install the software.
* Expertise required on scripting.
* This method is mostly preferred by developers who want to rebuild the software using source code and then install the new software.

## Package method

* We use ready-made package (setup) of the software for installation.
* Installers are used to install the packages.
```
_______________________________________
|                                     |
Package -----> Installer          Install
|                  |
|________ Open_____|
```

* For Redhat or Redhat based (CentOS, Fedora, etc...) Linux:
  1. Package format --> .rpm (xxxx.rpm)
  2. Installers --> RPM and DNF (YUM)

* For Debian or Debian based (Ubuntu, Kali, etc...) Linux:
  1. Package format --> .deb (xxxx.deb)
  2. Installers --> DPKG and APT

 * RPM installer vs DNF installer

1. RPM installer:
  * Traditional installer
  * Local installer
  * Does not resolve missing dependencies
```
Crontab
  |____vi (dependency missing)
```
  * Does not require initial configuration
  * Pros: fast and used directly.

2. DNF installer:
  * Advanced installer
  * Supports centralized software manager
  * Tries to resolve missing dependencies
  * Requires initial configuration

* Sources for packages:
    1. Internet
    2. Linux Installtion DVD (9000+ Application)

```
# DNF
/mnt
|_______BaseOS -----> Packages (Database of rpm file) (Need to have)
|_______AppStream -----> Packages (Database of rpm file) (Good to have)
```

## Commands
```
# RPM
# ls /mnt/BaseOs/Packages (list of rpm file)
# ls /mnt/AppStream/Packages (list of rpm file)
# rpm -q tar (Displays installed information along with package version and short description)
# rpm -q tar tree at gpm
# ls /mnt/AppStream/Packages/gpm*
# rpm -ivh /mnt/AppStream/Packages/gpm... (Install a package)
# ls /mnt/BaseOs/Packages/linuxconsoletools
# rpm -ivh /mnt/BaseOs/Packages/linuxconsoletools
# rpm -q gpm
# rpm -Uvh /mnt/AppStream/Packages/gpm... (Upgrades a package)
# rpm -e gpm (Erases or removes an installed package without checking for dependencies)
# rpm -q gpm

# DNF
# Initial Configuration

# vi /etc/yum.repos.d/server.repo
# cat /etc/yum.repos.d/server.repo
"
[repo1]
name = BaseOs
baseurl = file:///mnt/BaseOD
enabled = 1
gpgcheck = 0

[repo2]
name = AppStream
baseurl = file:///mnt/AppStream
enabled = 1
gpgcheck = 0
"
# dnf clean all
# dnf repolistall all
# dnf list gpm tar at trea
# dnf install gpm -y
# dnf update gpm -y
# dnf remove gpm -y
```
