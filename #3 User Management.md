# User Management

## Server access types:

### OS Access: Performed by admins and developer for administration and development.
### Application Access: Performed by end users for accessing application.

## User types:

1. Local user: End user with limited privileges.
2. Super user: Admin user with full privileges. [root]
3. System user: Inbuilt user used by the OS and Applications internally [we cannot login with this user]

## AAA Proccess:

A -> Authentication - Kaun hai.
A -> Authorization - Kya yah kar sakta hai.
A -> Accounting - kya kya kiya.

* Credential or token user for AAA is called user.
* To secure the access of a usser, We must define a password.
* When we create a user in linux: it gets created in locked state.
* To unlock a user: it is mandotory to either seta password or disable password.

## Commands for basic user management.
```
# useradd jane              -  Add a user account.
# usermod -l jack jane      -  Change a username.
# passwd jane               -  Set/Change password for a user.
# passwd -d jane            -  Remove password from a user.
# passwd -l harry           -  Lock a user account.
# passwd -u harry           -  Unlock a user account.
# su - jane                 -  Switch user on same terminal with home directory.
# chfn harry                -  Add finger (Personal) info.
# finger harry              -  View finger info. [https://www.geeksforgeeks.org/finger-command-in-linux-with-examples/]
# userdel harry             -  Delete a user (without deleting home directory)
# userdel -r harry          -  Delete a user recursively (with home directory)
# getent passwd jane        -  Get info of a user account.
# getent passwd             -  List all existing users.  
```

# Password Management

## Password Aging policies.

1. Default: Password are encrypted using SHA512 algorithm (non human readable)
2. Default: Dictionary check / Palindrome check (single character)/ Systematic & simplistic check (abc@123)
3. Default: There are also password complexity policies like inclusion of upper-case,lower-case,characters,digits,special characters and minimum password lenght.
4. Configured by admin:
     * Password aging policies are critical for user security.
     * There are 4 main password aging policies
     * Minimum age[0]: 3 [Days gap between two password change]
     * Maximum age[9999]: 60 [Days after which password is expired]
     * Warning age[7]: 5 [Days before password expiry, that user is warned]
     * Password inactive[-1]: 2 [Days after password expiray, that account is disabled]
```
# chage jane    - To change aging policy of a user.
# chage -l jane - To check aging policy of a user.
```

## Groups Management

* A group is a set of multiple users.
* With every user, a default group is created.
* The name of default group is same as the name of user.
* By default: Every user is associate with its own group.
* root can create additonal groups
* Just creating group is not enough. group and user must be associated.
* A user can associate with multiple groups.

sales <--(S)-- ganesh --(P)--> ganesh 
              |
              |
              ^
             mumbai

    mahesh --(P) --> sales
* A user is user, a group is a group
* Their association is either primary or supplementary
* A user can have multiple groups associated as supplementary. but their can be only one primary group for a user.

  User                            groups
  ganesh     -- (associated) -->  ganesh
  manesh     -- (associated) -->  manesh
                                  mumbai
                                  delhi
                                  hr
                                  sales

  ```
  # groupadd sales -  To create a group
  # groupdel sales -  To delete a group
  # usermod -g sales ganes - To create primary association
  # usermod -aG acounts ganesh - To create supplementary association
  # id ganesh - Check group association of a user
  # getent group sales - Check exitence of group
  # gretent group
  ```

  ## Advance user management

  user
          | - Primary association
  group
  UID [for user]
  GID [for group]
  Home direcotry
  Personal profile files
      - Personal
          * Present in the home directory
          * File name is .bashrc
          * Personal for every user
      - Common
          * A common profile file for all users.
          * file name is /etc/profile
          * Only root can modify this file.
  User login
      |
      |-- .bashrc
      |-- /etc/profile

Minimum UID and GID value for local users and groups is 1000
UID and GID 'O' is always assigned to root and its group
1-999 is reserved for system users and groups
Default maximum limit for UID and GID is 6000<-- Configration

** Every user is given profile files. Profiles are scripts that are executed every time when a user will login. If there is any command that you want to autorun at user login. You can put it in the profile file.

Default values that useradd command use while creating a user are stored in 2 files:
    
    /etc/default/useradd
    home = /home
    shell = /bin/bash
    inactive = -1

    /etc/login.defs
    min uid 1000
    max uid 6000
    min gid 1000
    min gid 6000
    min age 0
    max age 99999
    warn age 7 

Shell
    - Interactive 
          - sh
          - bash
          - zsh
    - Non interactive
          - /sbin/nologin
          - /bin/false

* By default useradd command refers default values for creating a user from /etc/login.defs and /etc/default/useradd file.
* Admin can create a customzied user by mentioning the values in the command
* Such command is called an extended useradd command.
  ```
  Command lifeline
  # useradd --help
  # ls --help
  # man useradd
  # man tar
  ```
Example 

```
Create a user 'harry' with UID as 6003
# useradd -u 6003 harrt
Create a user 'susan' with home directory is /usr/local
# useradd -b /usr/local susan
Create a user 'Donald' with a no login shell
# useradd -s /sbin/nologin
Lets understand this command
# useradd -u 9993 -b /usr/local/bin -G hr nashta
# chage -l ganesh
  Last password : Jan 30,2025
  Password expires : Mar 16, 2025
  Password inactive : Mar 17, 2025
  Account expires : Never
  Minimum number of days  between password change: 3
  Maximum number of dyas between password change: 45
  Maximun number of days of warning before password expires: 5
# chage ganesh
# chage -l ganesh

Command for Group:
getent group  - check existence of groups  
```

