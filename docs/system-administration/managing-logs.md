# Managing Logs

Log files are the best source of information about what's happening on the system. The kernel, processes, and other services write their events to log files which are normally located inside the `/var/log` directory. Logs are normally written to a file on disk but can be configured to be sent to a centralized log management service if desired.

## Writing Logs

### `rsyslogd`

The `rsyslogd` daemon is responsible for reading logs from a source and routing them to the appropriate destination. The `rsyslogd` service implements the syslog protocol to determine how to handle logs. When logs are sent to `rsyslogd`, they are given a facility and a priority. These two parameters let `rsyslogd` know how to route the logs.

## Reading Logs

Most logs for a system are located in the `/var/log` directory. To read the logs you can use your favorite text editor such as `vi` or other commands to read files. Although reading log files like this is inefficient, there may be times where this is the only acceptable way to read logs.

### `journalctl`

A better way to read logs is the use the `journalctl` command. Now keep in mind that `journalctl` may not contain all logs, but it will contain most of the logs from the system and the services running on it. 

!!! example "Example: Usage of `journalctl`."

    Read all the logs `journalctl` knows about, starting from the earliest.

    ```
    $ sudo journalctl
    ```
    
    Read all the logs `journalctl` knows about as they come in live.

    ```
    $ sudo journalctl -f
    ```
    
    Read all the logs `journalctl` knows about, starting from `2018-09-01 18:00:00`.

    ```
    $ sudo journalctl --since 2018-09-01 18:00:00
    ```
