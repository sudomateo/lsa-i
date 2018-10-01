# Services

A long running process is called a daemon or service. Services normally provide some function to users such as serving a website or running an application. When Linux boots up, there are a number of services that start up with it. These services all combine to boot the operating system.

## Systemd

When Linux boots up, the kernel will load the first process. This first process has PID 1 and is responsible for loading all other processes that are required to boot. In CentOS 7, the first process is called `systemd` and it is located at `/usr/lib/systemd/systemd`.

Linux uses what are called targets to determine what services get started upon boot. These targets use systemd unit files to start other services. Common targets are detailed below.

| Target              | Description                      |
| ------------------- | -------------------------------- |
| `poweroff.target`   | Powers off the system            |
| `rescue.target`     | Switches to single user mode     |
| `multi-user.target` | Multi-user mode, console login   |
| `graphical.target`  | Multi-user mode, graphical login |
| `reboot.target`     | Reboots the system               |

The systemd unit files define how to start a given service. These files usually end in `.service` and are located in two locations on the file system. The first location is `/usr/lib/systemd/system` and the second is `/etc/systemd/system`. If a file with the same name is located in both locations, the file in `/etc/systemd/system` takes precedence. This allows package maintainers to ship a systemd unit file for their service that lives in `/usr/lib/systemd/system` while allowing the system administrator to override that file in `/etc/systemd/system` if necessary.

## Service Commands

It's nice to know where the configuration files for services live, but it's even better to know how to manage these services. Let's take a look at the one command that is used to manage all aspects of a service, `systemctl`.

### `systemctl`

The `systemctl` command is used to manage services. It can start, stop, restart, reload, and check the status of services as well as other things. Let's take a look at some examples on how to use `systemctl`.

!!! example "Example: Usage of `systemctl`."

    Show the state of the `chronyd` service.

    ```
    $ sudo systemctl status chronyd
    ```

    Start the `chronyd` service.

    ```
    $ sudo systemctl start chronyd
    ```

    Stop the `chronyd` service.

    ```
    $ sudo systemctl stop chronyd
    ```

    Restart the `chronyd` service.

    ```
    $ sudo systemctl restart chronyd
    ```

    Reload the `chronyd` service.

    ```
    $ sudo systemctl reload chronyd
    ```

    Enable the `chronyd` service to start on boot.

    ```
    $ sudo systemctl enable chronyd
    ```

    Disable the `chronyd` service from starting on boot.

    ```
    $ sudo systemctl disable chronyd
    ```
