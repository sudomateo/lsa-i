# File Basics

## File Naming

File names in Linux are case-sensitve and may contain the characters `a-z`, `A-Z`, `0-9`, `.`, `-`, and `_`. A file named `file01` is different than a file named `FiLe01`.

Linux also does not have a concept of file extensions. A file named `file.txt` might be a video file while a file named `file.mp3` might be a picture. File extensions are there for human readability.

## File Commands

### `ls`

The `ls` command is used to list all of the files and directories that reside in a given file path.

!!! example "Example: Usage of `ls`."
    
    To list the files and directories of a given path.

    ```
    $ ls /
    bin   dev  home  lib64  mnt  proc  run   srv  tmp  vagrant
    boot  etc  lib   media  opt  root  sbin  sys  usr  var
    ```

    The `-l` option shows a long listing of each file. It also shows file information which we'll cover in detail later.

    ```
    $ ls -l /
    total 16
    lrwxrwxrwx.   1 root    root       7 May 12 18:50 bin -> usr/bin
    dr-xr-xr-x.   5 root    root    4096 May 12 18:55 boot
    drwxr-xr-x.  18 root    root    2960 Jul 22 21:02 dev
    drwxr-xr-x.  77 root    root    8192 Jul 22 21:02 etc
    drwxr-xr-x.   3 root    root      21 May 12 18:54 home
    lrwxrwxrwx.   1 root    root       7 May 12 18:50 lib -> usr/lib
    lrwxrwxrwx.   1 root    root       9 May 12 18:50 lib64 -> usr/lib64
    drwxr-xr-x.   2 root    root       6 Apr 11 04:59 media
    drwxr-xr-x.   2 root    root       6 Apr 11 04:59 mnt
    drwxr-xr-x.   2 root    root       6 Apr 11 04:59 opt
    dr-xr-xr-x. 100 root    root       0 Jul 22 21:02 proc
    dr-xr-x---.   2 root    root     137 May 12 18:55 root
    drwxr-xr-x.  25 root    root     840 Jul 22 21:02 run
    lrwxrwxrwx.   1 root    root       8 May 12 18:50 sbin -> usr/sbin
    drwxr-xr-x.   2 root    root       6 Apr 11 04:59 srv
    dr-xr-xr-x.  13 root    root       0 Jul 22 21:02 sys
    drwxrwxrwt.  10 root    root     198 Jul 22 23:18 tmp
    drwxr-xr-x.  13 root    root     155 May 12 18:50 usr
    drwxr-xr-x.   2 vagrant vagrant   25 Jul 22 18:58 vagrant
    drwxr-xr-x.  18 root    root     254 Jul 22 21:02 var
    ```

    The `-a` option shows hidden files as well.

    ```
    $ ls -a /home/vagrant
    .  ..  .bash_logout  .bash_profile  .bashrc  .ssh
    ```

### `touch`

The `touch` command is used to update file modification and access times. While we won't use it for that purpose here, `touch` also creates empty files.

!!! example "Example: Usage of `touch`."

    To create an empty file named `/tmp/file01`.

    ```
    $ touch /tmp/file01
    $ ls /tmp
    file01
    ```

### `mkdir`

The `mkdir` command is used to create directories.

!!! example "Example: Usage of `mkdir`."

    To create a directory.

    ```
    $ mkdir /tmp/dir01
    $ ls /tmp
    dir01 file01
    ```

    All parent directories must exist when using `mkdir` or you'll see an error.

    ```
    $ mkdir /tmp/parent_dir/child_dir
    mkdir: cannot create directory ‘/tmp/parent_dir/child_dir’: No such file or directory
    ```

    To have `mkdir` create all parent directories for you, use the `-p` option.

    ```
    $ mkdir -p /tmp/parent_dir/child_dir
    $ ls /tmp
    dir01 file01 parent_dir
    $ ls /tmp/parent_dir
    child_dir
    ```

### `cp`

The `cp` command is used to copy a file from one location to another. You can use absolute or relative paths when copying files. You can also change the name of the destination file.

!!! example "Example: Usage of `cp`."

    To copy a file.

    ```
    $ cp /home/vagrant/file01 /tmp/file01
    ```

    To copy a file and change the name.

    ```
    $ cp /home/vagrant/file01 /tmp/newfile
    ```

### `mv`

The `mv` command is used to move files. You can use absolute or relative paths when moving files. You can also change the name of the destination file.

!!! example "Example: Usage of `cp`."

    To move a file.

    ```
    $ mv /home/vagrant/file01 /tmp/file01
    ```

    To move a file and change the name.

    ```
    $ cp /home/vagrant/file01 /tmp/newfile
    ```

### `rm`

The `rm` command is used to delete files and directories.

!!! example "Example: Usage of `rm`."

    To delete a file.

    ```
    $ rm /tmp/file01
    ```

    To recursively remove all files in a directory, use the `-r` option.

    ```
    $ rm -r /tmp/dir01
    ```

    To skip the confirmation prompt for removing a file, use the `-f` option.

    ```
    $ rm -f /tmp/file01
    ```

!!! danger "Danger"
    Be careful when using the `-r` and `-f` options with `rm`. It will remove files recursively without any notice. 

### `vi`

The `vi` command is used to edit files using a text editor. `vi` will be your text editor for the CLI and it's probably the most confusing command to learn. At it's core vi has two different modes named command mode and insert mode.

Command mode is the default mode that you will be in when you start `vi`. When using command mode it may look like you can just start typing but you cannot. This mode is used to run some `vi` commands that manipulate text. In order to master `vi` you must master this command mode. In this course we won't spend much time in command mode. 

When you start `vi`, you can press ++i++ to enter insert mode. Once you are in insert mode you can freely type text as you would in any text editor. This is the mode we'll mainly be using in this course.

!!! note "Note"
    We use `vi` instead of other text editors such as `emacs` and `nano` because `vi` is usually installed on most Linux distributions while other text editors are not.

Once you enter `vi`, you can quit by pressing ++escape++ and then typing `:q` and pressing ++enter++. There may be times when you get stuck in a certain part of command mode. To get out you can press ++escape++ a few times and then type `:q` and press ++enter++.

To discard any changes you've made to a file before quitting, press ++escape++ and then type `:q!` and hit ++enter++. 

To save any changes you've made to a file without quitting, press ++escape++ and then type `:w` and hit ++enter++.

To save any changes you've made to a file before quitting, press ++escape++ and then type `:wq` and hit ++enter++.

!!! example "Example: Usage of `vi`."

    You can use `vi` to edit an existing file or create a new file if it doesn't already exist.

    ```
    $ vi myfile
    ```

### `ln`

The `ln` command is used to create links between files. Links can be one of two types. The first type is a hard link which is what `ln` creates by default. A hard link is essentially a copy of a file. The second type is a soft link, or symbolic link, which is created with the `-s` option. Soft links are basically shortcuts to other files. We'll only use soft links in this course since they are more common.

!!! example "Example: Usage of `ln`."

    Create a soft link named `/tmp/mylink` that points to the file `/tmp/myfile`.

    ```
    $ ln -s /tmp/myfile /tmp/mylink
    ```

### `tar`

The `tar` command is used to create archives of files which are useful for backups.

This table details common options used with `tar`.

| Option | Description                                                 |
| ------ | ----------------------------------------------------------- |
| `-c`   | Creates a new archive                                       |
| `-x`   | Extracts an archive                                         |
| `-v`   | Enables verbose mode                                        |
| `-f`   | Specifies the file name of the archive to create or extract |
| `-z`   | Compress the archive using `gzip`                           |
| `-C`   | Change to this directory before archiving or extracting     |

!!! example "Example: Usage of `tar`."

    Create a compressed archive named `/tmp/archive01.tgz` of all files in `/home/vagrant` including the parent directories.

    ```
    $ tar -zcvf /tmp/archive01.tgz /home/vagrant
    ```

    Extract a compressed archive named `/tmp/archive01.tgz`.

    ```
    $ tar -zxvf /tmp/archive01.tgz
    ```

    Create a compressed archive named `/tmp/archive02.tgz` of all files in `/home/vagrant` NOT including the parent directories.

    ```
    $ tar -zcvf /tmp/archive02.tgz -C /home/vagrant .
    ```

    Extract a compressed archive named `/tmp/archive02.tgz`.

    ```
    $ tar -zxvf /tmp/archive02.tgz
    ```

### `find`

The `find` command is used to recursively find files on the file system. You can find files based on size, ownership, name, date modified, etc.

!!! example "Example: Usage of `find`."

    Find all files in `/` that end in `.txt`.

    ```
    $ find / -name "*.txt"
    ```

    Find all files in `/tmp` that are older than 30 days.

    ```
    $ find /tmp -mtime +30
    ```

    Find all files in `/mnt` that are owned by `vagrant`.

    ```
    $ find /mnt -user vagrant
    ```

    Find all files in `/` that are larger than 10MiB.

    ```
    $ find / -size +10M
    ```
