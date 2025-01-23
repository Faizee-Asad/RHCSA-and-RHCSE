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
