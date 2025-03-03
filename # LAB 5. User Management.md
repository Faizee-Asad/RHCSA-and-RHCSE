
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

### Command for Basic user management

```
# useradd jane (add a user account)
# usermod -l jake jane (change a username)
# passwd jane  (set/change password for a user)
# passwd -d jane (remove password for a user)
# passwd -l harry (Lock a user account)
# passwd -u harry (Unlock a user account)
# su - jane (switch user on same terminal with home dirctory)
# chfn harry (Add finger [Personal] info)
# finger harry (view finger info)
# userdel harry (Delete a user [without deleting home direcotry])
# userdel harry (Delete a user recursively [with Home directory])
# getent passwd jane (get info. of a user account)
# getent passwd (list all existing users.)
```

## Password management

* Password Aging Policies

* Default : Passowrd are encrypted using SHA512 algorithm [Non Human Readable]
* Default : (single character) abc@123 : Dictionary check/ Palindrome check / systematic & simplistic check.
* Default : There are also password complexity policies like inclusion of upper case; lower case characters; digit; special character; minimum password length.
* Configured by admin:
* Password aging policies are critical for user security.
* there are 4 main password aging policies:
* Minimum age [0]: 3 (days gap between password change)
* Maximum age [99999]: 60 (days after which password is expired)
* Warning age [7]: 5 (days before password expiry; that user is warned)
* Password inactive [-1]: 2 (days after password expiry; that account is disabled)

```
To change aging policy of a user
# chage jane
To check aging policy of a user
# chage -l jane
```
## Groups Management

* A group is a set of multiple users.
* With every user a default group is created.
* The name of default group is same as the name of user.
* By default every user is associated with its own group.
* Root can create additional groups. 
```
User      Assocaited
-----------------------------
Ganesh    ganesh
Mahesh    mahesh
          mumbai
          hr
          sales
```
* But Creating group is not enough group and user must be associated.
* A user can associate with multiple groups.
```
Sale <--S-- ganesh --P--> ganesh
              |
              S
              |
           Mumbai           
```
* A user is user, a group is group
* Their association is either **Primary** or **Supplementory**
* A user can have multiple groups associated as supplementory but their can be only 1 primary group for a user.

```
# groupadd sales (to Create a group)
# usermod -g sales ganesh (to create primary association)
# id ganesh (check group assocation of a user)
# groupdel sales (to delete a group)
# getent group sales (check existeance of group)
# getent group (list all existing groups.)
```

## Advance user management

```
User  --|
           --> Primary association
Group --|

UID (for user)
GID (for group)
Home directory
Personal profile files
```
* Personal:
*           Present in the home directory of every user
*           File name is .bashrc
*           Personal for every user
* Common:
*           A common profile file for all users.
*           File name is /etc/profile
*           Only root can modify this file

* Minimum UID and GID value for local users and group is 1000
* UID and GID '0' is always assigned to root and its group.
* 1-999 is reserved for system users and groups
* Default maximum limit for UID and GID is 6000 <-- Configurable

* Every user is given profile file. Profiles are scripts that are executed every time when a user will login.
* If there is any command that you want to autorun at run login, you can put it in the profile file.

* Default values that useradd command use while creating a user are stored in 2 files:
* /etc/default/useradd - home = /home - shell = /bin/bash - inactive = -1
* /etc/login.defs - min uid 1000 - max uid 6000 - min gid 1000 - max gid 6000 - min age 0 - max age 99999 - warn age 7.

```
          Interactive --> sh, bash, zsh
Shell -->
          Non-Interactive --> /sbin/nologon, /bin/false
```
* By default useradd command refers default values for creating a user from /etc/login.defs and /etc/default/useradd file.
* Admin can create a custominzed user by mentioning the value in the command.
* Such command is called and extended useradd command.

```
# useradd -u 6003 harry (create a user harry with UID as 6003)
# useradd -b /usr/local susan (create a user susan with home directory is /usr/local)
# useradd -s /sbin/nologin donald (reate a user donald wtih no login shell.)
```
## Advance user management

* Users and groups are just entries in some database files.
* The four user and group database files are:
* /etc/passwd - user database
* /etc/shadow - password database
* /etc/group - group database
* /etc/gshadow - group database
* This files have multiple columns knownas fields.
* Each fields contains information related to user or group.

* /etc/passwd is actual user database file.
* A users existance depend on this file.
* /etc/passwd is a file with 7 fields delimited by ':'
```
| ganesh : x : 1000 : 1003 : finger info : /home/ganesh : /bin/absh
```
* The 7 diffrent fields are:
* Login name
* Password
* UID
* GID of primary group
* gecos
* default directory
* default shell.

* /etc/shadow is a password database file.
* It contains to main infomation - encrypted password and password aging policies.
* /etc/shadow is a file with 9 fields delimited by ':'
```
| gabesh : $6$... : 19730 : 0 : 99999 : 7: : :  |
```
* The 9 different fields are:
* login name
* encrypted password [SHA521]
* Days since 1 jan 1970 , that password was last change
* max age
* min age
* warn age
* password inactive
* days since 1 jan 1970 , that account was last disableed
* empty

* /etc/group  is a group database file.
* It consists of 4 fields delimited by ':'.
```
| hr : x : 1003 : ram,shyam|
```
* The 4 different fields are:
* group name
* password
* gid
* member users

* /etc/gshadow  is a group database file.
* It consists of 4 fields delimited by ':'.
```
| hr : ! : describe : ram,shyam|
```
* The 4 different fields are:
* group name
* encrypted password
* like gecos
* member users

```
# getent passwd
# getent shadow
# getent groups
# getent gshadow
```
