# Basic Commands

## 1. Clear the screen using "clear" command or by pressing "ctrl+l"
```
# clear
```
## 2. Check the terminal you are working on by using "tty" command.
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
