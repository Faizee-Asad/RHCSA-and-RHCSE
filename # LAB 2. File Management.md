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
### Output Redirection

* By default output of a command is derived on the terminal from where the command is executed. but we can redirect the output at some other location. It is called output redirection.
* Locations:
* on another terminal [Team Collaboration]
* in a file [Create history/ report file]
* to /dev/null [discard the output lines]
```
# > sign is used to redirect the output
e.g command option value > location
```
### Error redirection

* By default error of a command is derived on the terminal from where the command is executed. but we can redirect the error at some other location. It is called output redirection.
* Locations:
* on another terminal [Team Collaboration]
* in a file [Create history/ report file]
* to /dev/null [discard the error lines]
```
# 2> sign is used to redirect the error.
e.g command option value 2> location
# &> sign is used to redict both output as well as error.
e.g command option value &> location
```
* In case of  redirection n a file
* > sign will either create a new file or overwrite the existing file.
* >> sign will either create a new file or append data in the existing file.

```
# tty
# date
# date /dev/pts/1
# date > /output.txt
# who > /dev/null
# DATE
# DATE 2> /dev/pts/1
# DATE 2> /error.txt
# cat error.txt
# WHO 2> /dev/null
# uname -r &> /dev/pts/1
# unAme -r &> /dev/pts/1
# who >> /output.txt
# cat /output.txt
# WHO 2>> /error.txt
# cat /error.txt
```
