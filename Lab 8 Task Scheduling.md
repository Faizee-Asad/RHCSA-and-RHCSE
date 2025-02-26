# Crontab

* Task scheduling helps admin to automate a task execution at a particular date/time or at system reboot.
* In all Linux flavors, there is a default tool called crontab to schedule taask.
* Crontab is a service-based task scheduler that's allows admin to schedule a task for a particular data/time or at system reboot.
* Admin should make sure that **crond service** is running all the time using command.
```
# systemctl status crond
```
* crond service checks for all minutely, hourly, daliy, monthely and yearly scheduled tasks and executes them
* Task scheduled in crontab are called **cron jobs**.
* All users can schedule tasks in crontab.
* For every user, crontab defines a separate **cron table**.
* A local user can only manage his own cron table.
* root can manage other user's cron table.
* root can also deny a local user from using crontab by marking entry of that user in /etc/cron.deny file.
* Crontab is used for recurring tasks.

# at - software
* atd (service) is a job scheduler daemon that runs jobs scheduled for later execution. These jobs are one-time-task (not recurring) at a specific time scheduled using 'at' utility

* Crontab allows admin to use combination of 5 times to schedule a cron job
```
*  *  *  *  *  command to be executed

1. min (0-59)
2. hour (0-23)
3. day of the month (1-31)
4. month (1-12)
5. day of week (0-7) (Sunday=0 or 7)

e.g:

05  *  *  *  *  echo "hello there" > /dev/ptd/1
30  07  *  *  06  /prgs/sh3
@reboot  echo "Server started at `date`" > /s.boots
*/3 *  *  *  *  (after every three minutes)
```

## Crontab
```
To check whether crontab is installed:
# rpm -q crontabs
# dnf list crontabs

To check whether crond is running:
# systemctl status crond

To add/remove cronjobs:
# crontab -e

To list cronjobs:
# crontab -l

To flush a crontable:
# crontab -r

As an admin list user cronjob
# crontab -l -u ganesh

As an admin flush user crontable
# crontab -r  -u ganesh

Ban user to use crontab
# echo "ganesh" >> /etc/cron.deny
```
# at
```
To check whether at is installed:
# rpm -q at
# dnf list at

To check whether atd is running:
# systemctl status atd

# at 21:00
at> echo hi
at> Ctrl+D

# at now +5hours
# at now +3days
# at 13:15 +3days
# at 20:00 tomorrow
# at 06:30 03/15/2025

# atq (to list your pending at jobs )
# at -c 1 (view the details of a specific job.)
# atrm 2 (Use the atrm command followed by the job ID to delete a specific job, e.g., atrm 1.)
# atq
```
