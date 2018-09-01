# Privilege Escalation

Linux has a user named `root` that has full privileges over the entire system. This `root` user is often called the superuser or a privileged user. In Windows parlance, the `root` user is similar to the Administrator user. 

The `root` user can do *anything*, even crash the system if you are not careful. There is no undo once you type a command as the `root` user, so always double check before executing a command.

Generally, it's considered bad practice to log in directly as the `root` user. In order to use the `root` user, we must learn how to elevate our privileges so that we may act as the `root` user to perform actions that require more access than a normal user has. Whenever you log in as the `root` user, the command prompt will change from `$` to `#` so that you have a visual indication that you are running as `root`.

Let's take a look on a few ways to elevate our privileges.

## `sudo`

The sudo command allows you to run a single command as another user. If no user is specified, the root user is assumed.

In order to run a command using sudo, you must be given sudo permissions on the system. One way to grant a user sudo privileges is to add the desired user to the `wheel` group. Another way is to modify the sudoers configuration file using the `visudo` command.

On most Linux systems, when you run the `sudo` command for the first time you are showed a warning and prompted for your password. Since we are running our Linux instance using Vagrant, we will not get this warning.

!!! example "Example: Show the message that's given the first time you run `sudo`."
    ```
    $ sudo echo “Hello”
    
    We trust you have received the usual lecture from the local System Administrator. It usually boils down to these three things:

      #1) Respect the privacy of others.
      #2) Think before you type.
      #3) With great power comes great responsibility.

    [sudo] password for vagrant:
    Hello
    ```

!!! example "Example: Running the `cat` command as the `root` user."
    ```
    $ sudo cat /etc/passwd
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
    games:x:12:100:games:/usr/games:/sbin/nologin
    ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
    nobody:x:99:99:Nobody:/:/sbin/nologin
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

## `su`

The `su` command is used to switch to another user. If no other user is specified, the `root` user is assumed by default. Running the su command will prompt you for the password of the user you are switching to, not the password of your current user. The `-` option is used to simulate a fresh login for the user you are switching to. This is helpful to run user startup scripts and load user specific variables.

!!! example "Example: Use the `su -` command to switch to the `root` user by giving the `root` user's password."
    ```
    $ su -
    Password:
    #
    ```

## Switching to `root`

In my experiences, the best way to elevate your privileges is to combine the `sudo` and `su` commands to log in as `root`. This setup allows system administrators to give normal users `root` access without giving away the `root` user's password.

!!! example "Example: Switching to the `root` user."
    ```
    $ sudo su -
    [sudo] password for vagrant:
    #
    ```

The command `sudo su -` seems overwhelming and redundant at first, but it is essentially just running the `su -` command via the `sudo` method. This allows users to log in as `root` without know the `root` password. In so many words, the `sudo` command allows the user to run the `su -` command as `root` and since `root` doesn’t need permission to do anything, the now privileged `su -` command simulates a fresh login as the `root` user, logging you in to a `root` shell. This entire processing is called "dropping down to root" and is how you can perform many actions on your Linux virtual machine.
