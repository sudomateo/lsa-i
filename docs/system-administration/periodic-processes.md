# Periodic Processes

Sometimes you will need to run commands or scripts on a recurring schedule. Linux has a built-in mechanism for running periodic processes called `cron`. Let's take some time to go over how to manage cron jobs.

## Cron

Cron jobs can either be system-level or user-level. The difference between these two types are where they are configured. System-level cron jobs are configured in `/etc/crontab` while user-level cron jobs are configured using `crontab -e` as the user that needs to run the job. System-level cron jobs are more common so we'll cover those. The `/etc/crontab` file has the following format:

```
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root

# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed
```

In addition to the configuration above, the crontab file can also contain the following special characters:

| Character | Description                           |
| --------- | ------------------------------------- |
| `*`       | Matches every value in the column.    |
| `-`       | A range of values in the column.      |
| `,`       | A list of values in the column.       |
| `/`       | Identifies an offset between a value. |

The use of cron jobs are best specified through example.

!!! example "Example: Create cron jobs."

    A system-level cron job that runs the `date` command as the `root` user every minute of every day.

    ```
    * * * * * root date
    ```

    A system-level cron job that runs the `date` command as the `root` user every day at 3:57.

    ```
    57 3 * * * root date
    ```
    
    A system-level cron job that runs the `date` command as the `root` user every 1st and 15th every month at 3:57.

    ```
    57 3 1,15 * * root date
    ```

    A system-level cron job that runs the `date` command as the `root` user every 1st and 15th of the months January, February, and March at 3:57.

    ```
    57 3 1,15 1-3 * root date
    ```
    
    A system-level cron job that runs the `date` command as the `root` user every 1st and 15th of the months January, February, and March at 3:57 only if that day happens to be on Saturday or Sunday.

    ```
    57 3 1,15 1-3 0,6 root date
    ```
    
    A system-level cron job that runs the `date` command as the `root` user every 15 minutes from 1:00 to 3:45 on every weekday.

    ```
    */15 1-4 * * 1-5 root date
    ```
