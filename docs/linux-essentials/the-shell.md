# The Shell

## Types of Shells

Shells are the interface between the user and the kernel. Contrary to popular belief, shells can be a **command-line interface** \(CLI\) or a **graphical user interface** \(GUI\).

### Common CLI Shells

| Shell  | Name               | Description                                  |
| ------ | ------------------ | -------------------------------------------- |
| `sh`   | Bourne shell       | One of the first shells used in Linux/Unix.  |
| `bash` | Bourne again shell | Improved Bourne shell.                       |
| `ksh`  | Korn shell         | Early attempt at improving the Bourne shell. |
| `csh`  | C shell            | Early shell designed for programmers.        |
| `tcsh` | T shell            | More advanced version of the C shell.        |
| `zsh`  | Z shell            | Popular merge of C and Korn shell.           |

### Common GUI Shells

| Name          | Description                           |
| ------------- | ------------------------------------- |
| Windows shell | GUI in the Windows operating system.  |
| X-Window      | GUI shell for Linux systems.          |
| Wayland       | A modern GUI shell for Linux systems. |

## Using a Shell

In modern Linux distributions, the default shell is normally `bash`. When you log into your machine you will be placed into the bash shell and be presented with a **command prompt**. The command prompt often ends with a `$` or a `#` depending if you are logged in as a normal user or the root user. The command prompt waits for a user to type one or more commands and press ++enter++ to execute these commands.

### Running a Command

!!! example "Example: Printing the default shell for the current user"
    ```
    $ echo $SHELL
    /bin/bash
    ```
    The above command returned `/bin/bash` which means that your default shell is the `bash` shell and it is located in the `/bin` directory.

### Exiting the Shell

!!! example "Example: Exiting the shell"
    ```
    $ exit
    ```

