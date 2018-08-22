# Command Basics

## What are Commands?

Commands are what you type at the command prompt. Once you type a command, you can press ++enter++ to execute that command. Commands can take arguments, sometimes called parameters, and options, sometimes called flags, that change the behavior of the command. We'll see more about using arguments and options later.

## Where are Commands Located?

### Internal and External Commands

Commands are either built into the shell or located somewhere on the file system. Commands that are built into the shell are called **internal commands**. Commands that are not built-in are called **external commands**.

To check if a command is an internal or external command you can use the `type` command. 

!!! example "Example: Check the type of the `echo` command."
    ```
    $ type echo
    echo is a shell builtin
    ```
    The `echo` command is an internal command.

!!! example "Example: Check the type of the `ping` command."
    ```
    $ type ping
    ping is /usr/bin/ping
    ```
    The `ping` command is an external command located at `/usr/bin/ping`.

Based on the above examples we know that the `echo` command is a shell built-in, but how did the shell know that the `ping` command was located in the `/usr/bin` directory? We'll cover that next.

### Finding External Commands

The shell uses the **path** to find external commands. The path is a colon delimited list of directories that the shell searches when you run a command. The value of the path is held in a variable called `$PATH` which you can see using the `echo` command.

!!! example "Example: Printing the `$PATH` variable."
    ```
    $ echo $PATH
    /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/vagrant/.local/bin:/home/vagrant/bin
    ```

The shell will search for commands in each location specified by the `$PATH` variable from left to right until it finds the first match or no match. Given the `$PATH` variable above, when we run the `ping` command the shell will first look for the `ping` command inside the `/usr/local/bin` directory. If nothing matches it will search inside the `/usr/bin` directory and keep searching until it finds the first match or no match at all. If there is no match the shell will throw an error.

!!! example "Example: Cannot find a command on the path."
    ```
    $ pingg
    -bash: pingg: command not found
    ```

Aside from using the path to find commands, you can run a command using an absolute or relative path. Running the command `./ping` will run the `ping` command located in the current directory. Running the command `/tmp/ping` will run the `ping` command located in the `/tmp` directory. 

Knowing the difference between internal and external commands is important, but knowing how to use commands effectively is far more important. Let's look at some common commands next.
