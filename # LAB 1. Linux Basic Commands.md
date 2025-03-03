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

* Local terminal are called tty tty1 to tty6
* Remote terminal, gnome terminal. Tmux terminal are called pts, pts/0, pts/1, pts/2 ... etc.

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
### 2. Change hostname of a server
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
```
# bc
2+2
6-2
2*2
16/4
```
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
# uname # check systm kernel name 
# uname -r # check systm kernel version
# uname -m # check systm kernel architecture
# uname -a # check systm kernel all info.
```
### 3. Check OS version
```
# cat /etc/os-release
```
## Exploring User Login Information

### 1. Check which user is currently logged in.
```
# whoami
```
### 2. Check which users are logged in.
```
# users
```
### 3. Check which users are logged in. This also gives information of the terminal they are currently logged in on and since when.
```
# who
```
### 4. Shows server's uptime
```
# uptime
```
### 5. Check which users are logged in on which terminal, since when and what they are doing using the 'w' command.
```
# w
```
### 6. Continously monitor the "w" command using "watch w"
```
# watch w
```
* Exit "watch w" by pressing "ctrl+c"

## History of commands

```
# history
# history 15
# history -c
```
* history -c is not work in kali

## Powering System On or Off

### 1. Trun system off by using "poweroff"
```
# poweroff
```
### 2. Restart system by using "reboot"
```
# reboot
```

_________________________________________________________________________________________________________________________________________________________________________
# Lab 2: Basic Commands

## Task 1:  Managing the terminal

1. Clear the screen usiing "Clear" command or by pressing "ctrl+l"
2. Check the terminal you are working on by using "tty" command
3. Logout of the terminal by typing "exit" or by pressing "ctrl+d". "logout" command works only on the login terminals and not on the graphical terminals.

## Task 2: Managing System Name

1. Display system name using "hostname" command
2. To change hostname using "hostname <new hostname>" command. This change is temporary and will be reverted once you restart the system. This change is visible only once you exit the shell and reopen it.
3. Change hostname permanetly using "hostnamectl set-hostname <new hostname>" command. This changes will reflect only after exiting terminal and reopening it.

## Task 3: System Data

1. Display date using "date" command
2. Set system date using "data -s" command.
   ```
   # date -s "2025-01-23 21:49"
   ```

## Task 4: Exploring System Information

1. Check detailed system information using "hostnamectl" command
2. Check System kernel version using "uname -r" command
3. Checl system architecture using "uname -m" command
4. check all kernel information using "uname -a" commnad

## Task 5: Using Calender

1. Display calender of current month using "cal" command
2. Display calender for a particular year using "cal <year>" command
3. Display calender of previous, current and next month using "cal -3" command
4. Display calender of particular month and year "cal <month> <year>" command

## Task 6: Using Calculator
1. Use basic calculator application by type "bc"
2. Perform calculations without going in "bc" application by using "expr" command

## Task 7: Exploting User Login Information

1. Check which user is currently logged in using "whoami" command
2. Check which users are logged in using "users" command
3. Check which users are currently logged in the system using "who" command. This also gives information of the terminal they are currently logged in on and since when.
4. Check which users logged in, on which terminals, since when and what they are doing using the "w" command
5. Continuously monintor the "w" command using "watch w"
   (Exit "watch w" by pressing "ctrl+c")

## Task 8: History of commands

1. Check history of all previouly executed commands using "history" command
2. Check history of previouly executed 15 commands using "history 15" command

## Task 9: Powering System On and Off

1. Trun system off by using "poweroff" command
2. Restart system using "reboot" or "init 6" command
