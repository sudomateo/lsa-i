# Common Commands

Now that we know what commands are, where they are located, and how to run them, let's go over some common commands that you'll need to know when using Linux.

## Commands

### `cd`

The `cd` command, short for "change directory", is used to change your directory. This is how you move around the file system. When used without any arguments, it will take you back to your home directory. 

!!! example "Example: Using `cd`"
    
    The following command places you into the `/tmp` directory.
 
    ```
    $ cd /tmp
    ```

    The following commands both change into the current user's home directory.
 
    ```
    $ cd
    $ cd ~
    ```

### `pwd`

The `pwd` command, short for "print working directory", is used to print your current working directory. This is the location on the file system that you are currently in. When you first login, this will most likely be your home directory.

!!! example "Example: Using `pwd`"

    ```
    $ pwd
    /home/vagrant
    $ cd /tmp
    $ pwd
    /tmp
    $ cd
    $ pwd
    /home/vagrant
    ```

### `echo`

The `echo` command is used to print out strings of text to the screen.

!!! example "Example: Using `echo` to print a string."

    ```
    $ echo "Hello World"
    Hello World
    ```

The `echo` command can also be used to print the _value_ of variables. We've seen this earlier with the `$SHELL` and `$PATH` variables.

!!! example "Example: Using `echo` to print the value of variables."

    ```
    $ echo $SHELL
    /bin/bash
    $ echo $PATH
    /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/vagrant/.local/bin:/home/vagrant/bin
    ```

When printing strings with echo, there is a difference between using double quotes and single quotes. Using double quotes prints the characters `a-z`, `A-Z`, and `0-9` normally but may interpret special characters differently. If you want to print a special character literally when using double quotes, you'll have to escape that character with a `\`. This is important when trying to use characters such as `$` because the shell interprets strings that begin with `$` differently. On the other hand, single quotes print every character literally.

!!! example "Example: Difference between double and single quotes."

    ```
    $ echo $SHELL
    /bin/bash
    $ echo "$SHELL"
    /bin/bash
    $ echo '$SHELL'
    $SHELL
    $ echo "\$SHELL"
    $SHELL
    ```

### `which`

The `which` command tells us the absolute path of a command. It essentially just searches the `$PATH` variable for the command and returns its location. This is useful when you have two commands that are named the same on your path and you want to find out which command you are actually using. The `which` command takes the command\(s\) that you want to search for as arguments. This works on both internal and external commands.

!!! example "Example: Using `which`"

    ```
    $ which echo
    /usr/bin/echo
    $ which ping
    /usr/bin/ping
    ```

### `clear`

The `clear` command clears the screen of all past commands and output. It reset your command prompt to the top of the visible screen. It's useful when you've been working on the CLI and there's a lot of unneeded output on the screen.

!!! example "Example: Using `clear`."

    ```
    $ clear
    ```

### `time`

The `time` command tells us how long a program took to execute. It displays the total execution time, user CPU time, and system CPU time. It's useful for checking how long a program takes to do something such as a large file copy or a long running script.

!!! example "Example: Using `time`."

    ```
    $ time which ping
    /usr/bin/ping

    real    0m0.002s
    user    0m0.001s
    sys	    0m0.001s
    ```

### `cat`

The `cat` command is used to print the contents of a file to the screen. Many people confuse the `cat` command with the `echo` command. To help you understand the differences, the `cat` command is used to print the contents of a file while the `echo` command is used to print strings to the screen or the values of variables. Learning the differences between `cat` and `echo` is very important and probably the biggest challenge new Linux users face early on.

!!! example "Example: Comparison of `cat` and `echo`."

    ```
    $ cat /etc/system-release
    CentOS Linux release 7.5.1804 (Core)
    $ echo /etc/system-release
    /etc/system-release

    $ cat "Hello"
    cat: Hello: No such file or directory
    $ echo "Hello"
    Hello

    $ cat $PATH
    cat: /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/vagrant/.local/bin:/home/vagrant/bin: No such file or directory
    $ echo $PATH
    /usr/local/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/home/vagrant/.local/bin:/home/vagrant/bin
    ```

!!! warning "Warning"

    Don't try to use the `cat` command to show the contents of programs or commands. It will fill your screen with binary characters and possibly cause your system to hang. If you're really curious, try to run `cat $SHELL` and see what happens.

### `less`

The `less` command is used to view the contents of a file or command using a pager. A pager is how you can limit the output of a file or command to display one page at a time. When using the pager, you can press ++space++ to jump down a page and ++b++ to jump up a page. To quit, press ++q++. The ++up++ and ++down++ arrows take you up or down line by line. This is useful for viewing large text or log files.

!!! example "Example: Using `less`."

    ```
    $ less /path/to/my/file
    ```

### `head`

The `head` command is used to view the first 10 lines of a file or command. You can use the `-n` option to change the number of lines you want to view.

!!! example "Example: Using `head`."

    ```
    $ head /etc/passwd
    root:x:0:0:root:/root:/bin/bash
    bin:x:1:1:bin:/bin:/sbin/nologin
    daemon:x:2:2:daemon:/sbin:/sbin/nologin
    adm:x:3:4:adm:/var/adm:/sbin/nologin
    lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
    sync:x:5:0:sync:/sbin:/bin/sync
    shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
    halt:x:7:0:halt:/sbin:/sbin/halt
    mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
    operator:x:11:0:operator:/root:/sbin/nologin
    ```

### `tail`

The `tail` command is used to view the last 10 lines of a file or command. You can use the `-n` option to change the number of lines you want to view. You can also use the `-f` option to view changes to the file in real-time. This is called following the file and it's useful for viewing log files live.

!!! example "Example: Using `tail`."

    ```
    $ tail /etc/passwd
    systemd-network:x:192:192:systemd Network Management:/:/sbin/nologin
    dbus:x:81:81:System message bus:/:/sbin/nologin
    polkitd:x:999:998:User for polkitd:/:/sbin/nologin
    rpc:x:32:32:Rpcbind Daemon:/var/lib/rpcbind:/sbin/nologin
    rpcuser:x:29:29:RPC Service User:/var/lib/nfs:/sbin/nologin
    nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
    sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
    postfix:x:89:89::/var/spool/postfix:/sbin/nologin
    chrony:x:998:996::/var/lib/chrony:/sbin/nologin
    vagrant:x:1000:1000:vagrant:/home/vagrant:/bin/bash
    ```

### `grep`

The `grep` command is used to search for lines withing files that contain specific regular expression patterns or strings. It's very similar to a CLI version of ++ctrl+f++. By default `grep` is case sensitive. You can use the `-i` option to ignore case sensitivity.

!!! example "Example: Using `grep`."

    Searching for the text `root` in the file `/etc/passwd`.

    ```
    $ grep root /etc/passwd
    root:x:0:0:root:/root:/bin/bash
    operator:x:11:0:operator:/root:/sbin/nologin
    ```

    Searching for the text `Root` in the file `/etc/passwd`.

    ```
    $ grep Root /etc/passwd
    ```

    Performing a case insensitve search for `root` in the file `/etc/passwd`.

    ```
    $ grep -i Root /etc/system-release
    root:x:0:0:root:/root:/bin/bash
    operator:x:11:0:operator:/root:/sbin/nologin
    ```
