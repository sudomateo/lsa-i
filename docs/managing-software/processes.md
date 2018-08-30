# Processes

Once you have installed some software on your Linux system, you might want to start using this software. Running software can be as simple as running a command to start a process. A process is nothing more than an instance of a program that is currently being executed. Every process on a Linux system has a process ID number (PID). This PID is used to uniquely identify processes across your system. Let's take a look at some common commands to use when managing processes.

## Process Commands

### `sleep`

The `sleep` command tells the shell to sleep for a specified number of seconds. It's a good way to pause in the middle of a script. The `sleep` command isn't really a process command, but we'll utilize it here to illustrate starting and stopping a process. By default, a process executes in the foreground, where your command prompt is. You can send a process to the background using `&`. Let's take a look at that now.

!!! example "Example: Usage of `sleep`."

    Sleep for 5 seconds.

    ```
    $ sleep 5
    ```

    Sleep for 5 seconds but send the execution to the background.

    ```
    $ sleep 5 &
    ```

### `ps`

The `ps` command is used to show information about processes that are running on the system. This command will give you useful information such as the processs ID number and the command that was executed to start this process.

!!! example "Example: Usage of `ps`."

    Show the processes being executed by the current user.

    ```
    $ ps
    ```

    Sleep for 30 seconds and view the new process.

    ```
    $ sleep 30 &
    $ ps
    ```

    Show all of the processes currently running on the system.

    ```
    $ ps aux
    ```

### `top`

The `top` command is used to show all of the processes on a system and their resource usage. This is a great command to use when troubleshooting a system. To exit top, press ++q++.

!!! example "Example: Usage of `top`."

    Use top to view processes and their usage.

    ```
    $ top
    ```

### `jobs`

The `jobs` command is used to view commands that are running in the current shell session. This is useful to view background process ID numbers.

!!! example "Example: Usage of `jobs`."

    Sleep for 30 seconds and view the jobs.

    ```
    $ sleep 30 &
    $ jobs
    ```

### `nice`

Every process in Linux has a priority assigned to it. The priority is used to change how much resources a process is given. The nice priorities range from `-20` to `19` where the lower number means the higher the priority. The `nice` command is used to start a new process with a given priority.

!!! example "Example: Usage of `nice`."

    Run the `sleep` command with a priority of `15`.

    ```
    $ nice -n 15 sleep 30 &
    ```

### `renice`

The `renice` command is used to change the priority of an already running process. 

!!! example "Example: Usage of `renice`."

    Change the priority of PID `27799` to `7`.

    ```
    $ renice 7 27799
    ```

### `kill`

The `kill` command is used to stop processes. There are two common ways to use the `kill` command. One way to kill a process is by sending it a `SIGTERM` signal. A `SIGTERM` tells a process to stop executing and exit gracefully. The other way to kill a process is by sending it a `SIGKILL` signal. A `SIGKILL` forcefully kills a process without notification. When killing a process you should always try a `SIGTERM` before a `SIGKILL`.

!!! example "Example: Usage of `kill`."

    Send a `SIGTERM` to PID `27799`.

    ```
    $ sudo kill -15 27799
    ```

    Send a `SIGKILL` to PID `27799`.

    ```
    $ sudo kill -9 27799
    ```
