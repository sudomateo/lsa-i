# Configuring the System

## Setting the Hostname

A hostname is used to identify the system on the network. The hostname is normally configured the first time you install the operating system. If you want to change the hostname, you can use the `hostnamectl` command.

### `hostnamectl`

!!! example "Example: Usage of `hostnamectl`."

    Set the hostname to `host01`.

    ```
    $ sudo hostnamectl set-hostname host01
    ```

## Setting the Time

Maintaining proper time on a Linux system is extremely important. Imagine trying to troubleshoot an issue across multiple systems whose times are all out of sync. This may seem like a trivial task, but you'll be glad your systems have the correct time when a major issue hits.

Linux uses Coordinated Universal Time (UTC) for its system clock. All events written to the logs are logged with this time. You can set a time zone on the system which will be used to convert the UTC time into the configured time zone's time. The `timedatectl` command can be used the time, date, and time zone. The most common use-case is to change the time zone.

### `timedatectl`

!!! example "Example: Usage of `timedatectl`."

    Set the time zone to `America/New_York`.

    ```
    $ sudo timedatectl set-timezone America/New_York
    ```

Setting the time on each system manually can become unwieldy when managing hundreds of systems. A better approach is to use the Network Time Protocol (NTP) to automatically sync the correct time to your systems. A common package to use to configure NTP is named `chrony`. Once this package is installed you can edit its configuration file at `/etc/chrony.conf` to configure the NTP servers used to sync time from. Afterwards you can restart and enable the `chronyd` service using `systemctl restart chronyd` and `systemctl enable chronyd`.
