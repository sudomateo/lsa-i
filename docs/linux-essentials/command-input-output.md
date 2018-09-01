# Command Input and Output

## File Descriptors

Commands may take input and produce output. The input may be the data supplied to an argument or the name of a file for the command to operate on. The output may be information regarding the status of a command or errors detailing what went wrong. Understanding this input and output is important should we wish to manipulate it. 

As we covered earlier, everything in Linux is treated as a file, even the keyboard and screen. Linux uses what are called **file descriptors** to identify which input or output device to work with. There are three basic file descriptors that we can use to manipulate input and output in Linux. These file descriptors are standard input (`STDIN`), standard output (`STDOUT`), and standard error (`STDERR`) and they are often referred to by the numbers `0`, `1`, and `2` respectively.

| Name     | File Descriptor | Description                                                            |
| -------- | --------------- | ---------------------------------------------------------------------- |
| `STDIN`  | `0`             | Used to read input into a command. Usually the keyboard.               |
| `STDOUT` | `1`             | Used to show output of a command. Usually the terminal window.         |
| `STDERR` | `2`             | Used to show error messages of a command. Usually the terminal window. |

## Redirection

Command input and output can be redirected to files, other commands, or other terminals. Redirecting input and output is how you can create files to store output for later processing or just send the uneeded output to another location to save space. Generally, redirecting output is much more common that redirecting input. The common input and output redirection operators are detailed in the following table.

| Operator | Description                                                                                                             |
| -------- | ----------------------------------------------------------------------------------------------------------------------- | 
| `>`      | Redirects `STDOUT` to a file. *Overwrites* the file if it already exists, otherwise creates the file.                   |
| `>>`     | Redirects `STDOUT` to a file. *Appends* to the file if it already exists, otherwise creates the file.                   |
| `2>`     | Redirects `STDERR` to a file. *Overwrites* the file if it already exists, otherwise creates the file.                   |
| `2>>`    | Redirects `STDERR` to a file. *Appends* to the file if it already exists, otherwise creates the file.                   |
| `&>`     | Redirects both `STDOUT` and `STDERR` to a file. *Overwrites* the file if it already exists, otherwise creates the file. |
| `&>>`    | Redirects both `STDOUT` and `STDERR` to a file. *Appends* to the file if it already exists, otherwise creates the file. |
| `<`      | Reads `STDIN` from a file or command. Useful to process large files of data.                                            |

!!! info "Info"
    It's important to understand the difference between overwriting and appending to a file. The `>` operator always overwrites while the `>>` operator always appends.

!!! example "Example: Send the output of the `echo` command to `file01`, overwriting the file."
    ```
    $ echo "Hello" > file01
    $ cat file01
    Hello
    ```

!!! example "Example: Send the output of the `echo` command to `file01`, appending to the file."
    ```
    $ echo "World" >> file01
    $ cat file01
    Hello
    World
    ```

!!! example "Example: Send the output of the `echo` command to `file01`, overwriting the file."
    ```
    $ echo "Goodbye" > file01
    $ cat file01
    Goodbye
    ```

## Pipes

The `|` (pipe) symbol is used to link two or more commands together. When two commands are separated by a `|`, the output of the command on the left is sent as input to the command on the right. You can pipe more than two commands together to create a complex command.

!!! example "Example: Send the output of the `cat` command as input to the `grep` command."
    ```
    $ cat /etc/passwd | grep -i root
    root:x:0:0:root:/root:/bin/bash
    operator:x:11:0:operator:/root:/sbin/nologin
    ```

You can combine redirection and pipes to perform advanced actions.

!!! example "Example: Send the output of the `cat` command as input to the `grep` command while sending that output to a file."
    ```
    $ cat /etc/passwd | grep -i root > file01
    $ cat file01
    root:x:0:0:root:/root:/bin/bash
    operator:x:11:0:operator:/root:/sbin/nologin
    ```
