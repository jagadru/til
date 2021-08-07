# What is crontab?

The crontab utility is the program used to install, deinstall or list the tables used to drive the cron daemon. Each user can have their own crontab, and they are not intended to be edited directly.
The cron daemon to schedule obvious things, such as regular backups that occur daily at 2 a.m.

Each user, including root, can have a cron file. These files don't exist by default, but can be created in the /var/spool/cron directory using the crontab -e command that's also used to edit a cron file

## How to use it?
- Open Terminal, type crontab -e and hit Enter.
- Then press "i" on the keyboard to activate Insert Mode (with Vim, obviously)
- List all the commands you want to run (you can use the following example as guidance)

```
# crontab -e
SHELL=/bin/bash
MAILTO=root@example.com
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed

# backup using the rsbu program to the internal 4TB HDD and then 4TB external
01 01 * * * /usr/local/bin/rsbu -vbd1 ; /usr/local/bin/rsbu -vbd2

# Set the hardware clock to keep it in sync with the more accurate system clock
03 05 * * * /sbin/hwclock --systohc
```
- Once you have done this, press ESC to exit Insert mode. Then type ":wq" to save your changes.

## For more info:
 - Run `man 5 crontab`
 - [How to use cron in Linux](https://opensource.com/article/17/11/how-use-cron-linux)
 - [CronHowTo](http://bit.ly/CronHowTo)
