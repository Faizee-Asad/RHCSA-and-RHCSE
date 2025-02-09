# Basic Commands

## Managing the terminals

### 1. Clear the screen using "clear" command or by pressing "ctrl+l"
```
# clear
```
### 2. Check the terminal you are working on by using "tty" command.
```
# tty
```
* Login screen are called terminals
* Type: GUI and CLI
* There are total 6 local terminals on RHEL - If Graphics is on : 1 GUI and 5 CLI. If Graphics is off : 6 CLI.
* ctrl + alt + fn key is used to switch between local terminal. If Graphics is on : f2 for GUI and f2..f6 CLI.
* Multiple CLI terminals for running parallel tasks.
* In Kali There are 7 local terminals: 1 GUI and 6 CLI - f1 to f6 for CLI and f7 for GUI. 

* CLI over GUI mode: Accessing linux command line on graphical terminal gnome terminal application is used multiple tabs can be opend a single gnome terminal.
* ctrl + shift + t is used to open gnome tabs.

* Open multiple tabs inside a single CLI terminal using Tmux application

```
# tmux
```
* Press and release ctrl + b and then press c to open a new tab in tmux.
* Press and release ctrl + b and then type tab number to jump on a tab in tmux.

** Local terminal are called tty tty1 to tty6
** Remote terminal, gnome terminal. Tmux terminal are called pts, pts/0, pts/1, pts/2 ... etc.

### 3. Logout of the terminal by typing "exit" or by pressing "ctrl+d". "logout" command works only on the login terminals and not on the graphical terminals.
```
# logout
# exit
```

## Managing the system name

### 1. Display the system name using "hostname" command - Check current server name 
```
# hostname
# hostnameclt
```
### 2. Check current login name
```
# whoami
```
### 3. Change hostname of a server
```
# hostnamectl set-hostname newname
```

## System date and Calender

### 1. Display date 
```
# date
```

### 2. Change date
```
# date -s "2021-07-23 11:15:00"
```
### 4. Display Calender
```
# cal
# cal -3
# cal 2022
# cal 08 2022
```
* For kali you need to install ncal tool.
```
sudo apt install ncal
```

## Using Calculator

### Basic calculator application
``
# bc
2+2
6-2
2*2
16/4
``
* To exit this tool use : "ctrl+c" and then type "quit".
* For kali you need to install bc tool.
```
# sudo apt install bc
```

### Perform calculations without going in "bc" application by using "expr" command

```
# expr 5 + 5
# expr 10 - 5
# expr 25 / 5
# expr 55 \* 11
```
## Exploring system information

### 1. Check detailed system information
```
# hostnamectl
```
### 2. Check system kernel information
```
uname # check systm kernel name 
uname -r # check systm kernel version
uname -m # check systm kernel architecture
uname -a # check systm kernel all info.
```
### 3. Check OS version
```
cat /etc/os-release
```
