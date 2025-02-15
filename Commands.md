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

# File Management

### 1 List directory contents
```
# ls
# ls -l # long listing formate
# ls -lh # human readable
```

### 2. Print name of current working directory
```
# pwd
```

### 3. Change directory
```
# cd
# cd /
```
### 4. Create a directory
```
# mkdir /dir1
# mkdir -p /linux/distros/redhat
# mkdir /linux/distros/{ubuntu,fedora,centos}
```
### 5. Create a file
```
# touch /file.txt
# touch /index.html
# touch /linux/distors/redhat/{rhel7,rhel8,rhel9}
```
* In linux there is no extention concept.

### 6. list contents of directory in a tree like format.
```
# tree /linux
```

### 7. To copy file or directory
```
# cp /file.txt /root/Music
```
### 8. To move file or direcotry
```
# mv /html /root/Desktop
```
### 9. To delete file or direcotry
```
# rm /file.txt
# rm -f /root/Music/*.txt # forcefully remove
# rm -rf /root/Music/html #  for directory
```
## Absolute path: Complete path from current locations to reach a destination file or directory is called absolute path.
* . current directory
*  .. previous directory
*  /root/Desktop - stating slash is called linux directory. and after root slash is a seprators.
*  ~ (tilda) -> Current user home directory
*  root: ~ = /root
*  asad: ~ = /home/asad

### . Find a path of the file
```
# locate 
```
* Depends o a local database file  /var/lib/mlocate/mlocate.db
* updatedb commands is used locate's database immediatedly.
```
# updatedb
```
Examples
```
# locate sshd config
# touch /lol.txt
# locate lol.txt
# updatedb
# locate lol.txt
``` 
### The Find Command
* It is a powerful utility used to search for files and directories within a directory hierachy.
* It support various criteria, such as name, type, size, permissions, modification and more.
* Key Flag:
* -name: Match file name
* -iname: Match case in-sensitive file name.
* -type: Specify file type ( f for files, d for directories)
* -size: Match file size
* -mtime: Match modification time.
* -atime: Match access time.
* -exec: Execute a command on matching files.
* -perm: Match permissions.
* -user: Match owner.
* -or: Find file matchning one condition OR another.
* Syntax: find /target-dir -criteria value (find file that match the criteria)
*         find /target-dir ! -criteria value (find files that do not match the criteria)

```
# find /etc -name "*.conf"
# find /etc -name "a*.conf"
# find /etc -name "[ad]*.conf"
# find /etc -name "[a-d]*.conf"
# find /etc -name "[a-c]*"
# find /etc -iname "[a-c]*"
# find /usr/bin -size +4M
# find /usr/bin -size +4M -size -30M
# find /simpledir -type f
# find /simpledir -type d 
# find /usr/bin -size +4M -exeec cp {} /root/Music \;
# find /root/Music -name "*" -type f -exec ls -lh {} \;
```

### Commads to read text files:
1. cat: simple text reading command. It print the whole file
```
# cat /etc/default/useradd
```
2. less: print the file page wise.
```
# less /var/log/messaages (use up/down arrow key to scroll and press 'q' to exit.)
```
3. head: print top lines of a file.
```
# head -5 /var/log/messaages (print the first 5 line) 
```
4. tail: print last lines of a file. 
```
# tail -5 /var/log/messaages (print the last 5 line)
```
5. grep: print lines that contain a particular word/phrase.
```
# cat /etc/password (print the whole file)
# grep "spool" /etc/passwd (print only those line that contain word "spool")
```
6. cut: print columns from a database file.
```
cut -f 3 -d : /etc/passwd (-d means delimiter/seprator and -f means field number)
```
7. | : pipeline 2 or more commands to work as a team and derive the output.
```
# grep "spool" /etc/passwd | cut -f 3,6 -d :
# date | cut -f 4,5 -d :
```
### Text editor: vi (vim) and nano

* Nano: easy to use; control short-curs are displayed on the screen;
* not so effective and fast; prefered by new comers.
```
# nano filenmae
```
* Vi (vim): Most powerful text editor; fastest text editor;
* tutorials require to use vi; most used editor on linux
```
# vi filename
```
* Mode
* |--execute (perform operations) * default mode (typing not allowed)
* |--insert (typing)

* Options
*  i                    -->  enter into insert mode
*  esc                  -->  enter into execution mode
*  esc:w                -->  write changes
*  esc:w /apple.txt     -->  write changes with file name
*  esc:wq               -->  write changes and quit the file
*  esc:wq /apple.txt    -->  write changes with file name
*  esc:q                -->  quit the file
*  esc:q!               -->  quit without saving changes
*  yy                   -->  to copy current line
*  p                    -->  to paste copied line below current line
*  10yy                 -->  copy 10 lines
*  dd                   -->  delete current lines
*  10dd                 -->  delete 10 lines
*  o                    -->  open a new line below current line
*  shfit + o            -->  open a new line above current line
*  u                    -->  undo changes
*  esc:81               -->  go to line 81
*  esc:$                -->  see line numbers
*  esc:set nu           -->  set line numbers
*  esc:set nonu         -->  hide line numbers
*  esc:/word            -->  jump to the number containing word/phrase

### diff commnad
* The diff command in Unix/Linux is used to compare two file line  by line display the differences between them.
* It provide insight into what has changes, been added, or been remove in text files.
```
# diff file1.txt file2.txt (compare two file)
# diff -y file1.txt file2.txt (show differences side-by-side)
# diff --suppress-common-lines -y file1.txt file2.txt (suppress common lines)
# diff -q file1.txt file2.txt  (output only whether files differ)
```

### 'patch' command
* The patch command reads a patch file (output of diff -u ) and  applies the differences to the original file(s), updating them as specified.
```
# diff -u original_file modified_file > changes.patch (using diff, create a unified diff file)
# patch original_file < changes.patch (to apply the patch to the original file)
# patch -R original_file < changes.patch (to undo a patch that was applied)
```

### sed commond
* sed --> Print the modified version of a file
* sed -i --> save modification in the file

```
# cat linux.txt
# sed s/unix/linux/ /linux.txt
# sed s/unix/linux/2 /linux.txt
# sed s/unix/linux/g /linux.txt
# cat linux.txt
# sed '3a This is a new line' /linux.txt
# sed '3i This is a new line' /linux.txt
# cat linux.txt
# sed -i 's/unix/linux/g;3d;$a This is new line' linux.txt
# cat linux.txt
```

### awk file programming
* The awk command is a powerful text processing tool commonly used in Unix/Linux environment for pattern scanning and processing.
* It processes text line-by-line and applies operations baesd on patterns and actions defined by the user.
* The default delimiter for awk is a space
```
# awk '{print}' filename (to print entire file)
# awk '{print $2}' filename {to print specific field like cut command}
# awk '/pattern/{print}' filename {to print lines containing pattern word.}
# awk '$3>50{print}' filename (to print lines with conditions. print lines whether value in the third column is greater than 50)
# awk -f "," '{print $1,$2}' filename (To specify a delimiter)
# awk '{print NR,$0}' filename (To print file with line number)
```
## Archiving and compression

* Backup data is generally in-frequently accessed. 
* To save storage spcace on server, the best practice is to keep backup data in comparessed form.
* In all linux flavous, there are multiple compression tools that can work with tR archive manager to compress the archived data.

* Various comparession tools are:
* gzip -> fast performance speed, average compression ratio.
* bzip2 -> bit slow performance speed, better compression ratio.
* xzip -> very slow performance speed, best compression ratio.

* Combination can be either tar & gzip or tar & bzip2 or tar & xzip
* Eg:
* tar cf /data.tar /usr/bin - tar cf /data.tar /usr/bin
* gzip /data.tar - bzip2 /data.tar
* gunzip /data.tar.gz - bunzip2 /data.bz2

```
## Compression using tar and gzip
# du -h /usr/sbin (to know directory size)
# tar zcf /bin.tar.gz /usr/sbin (to create an archive) 
# ls -lh /bin.tar.gz (to know the size of compressed archive)
# tar ztvf /bin.tar.gz (to list contents of an archive)
# tar zxf /bin.tar.gz (to extract full content)
# tar zxf /bin.tar.gz usr/sbin/nvme usr/sbin/ledmon (to extract some content)
# tar zxf /bin.tar.gz -C /home (to extract in different directory)

## Compression using tar and bzip2
# tar jcf /bin.tar.bz2 /usr/sbin (to create an archive)
# tar jtvf /bin.tar.bz2  (to list contents of an archive)
# tar jxf /bin.tar.bz2  (to extract content)

## Compression using tar and xzip
# tar Jcf /bin.tar.xz /usr/bin (To create an atchive)
# tar Jtvf /bin.tar.xz (to list contents of an archive)
# tar Jxf /bin.tar.xz  (to extract content)
```

# Users Management

## Server access type
* OS access: performed by admins and developers for administration and development.
* Application access: performed by end users for accessing applications.
* User Type:
* local user: end user with limited privileges.
* super user: admin user with full privileges [root].
* system user: inbuilt user used by the OS and application internally [we can not login with this users]
* AAA Process:
* A -> Authentication  -> kon hai
* A -> Authorization   -> kya yeh kar sakte hai
* A -> Accounting      -> kya kya kiya
