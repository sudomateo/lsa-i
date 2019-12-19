# Managing Users and Groups

Users and groups are used to manage access to files, directories, and other services provided by the Linux operating system. Users accounts must be created for any user that wishes to log into a Linux system. User accounts must be a member of at least one or more groups. Groups are used to group together users that share a common role. Every user and group has a user ID (UID) and group ID (GID) that uniquely identifies them on the system. Although we can give more human readable names to users and groups, Linux only ever uses the UID and GID when determining access to resources. A user can be a regular user or a system user. A regular user typically has a UID of `1000` or higher while a system users has a UID below `1000`. The `root` user has a UID of `0` and the `root` group has a GID of `0`. That's why we every time we use `sudo su -` to change to the `root` user we call it "dropping down to root". 

## Managing Users

User accounts can be up to 32 characters in length and like most things in Linux, they are case-sensitive. You can use the characters `a-z`, `A-Z`, `0-9`, `-`, and `_` in a user name but it is common convention to create a user in all lowercase letters. It's recommended to have a username policy to standardize username formats for your systems.

Information for all of the users on a Linux system is kept in the `/etc/passwd` file. This is a `:` delimited file that contains information about a user in the following format:

```
USERNAME:PASSWORD:UID:GID:GECOS:HOME:SHELL
```

| Field    | Description                                                        |
| -------- | ------------------------------------------------------------------ |
| USERNAME | The user's user name.                                              |
| PASSWORD | Not kept in `/etc/passwd`. Moved to `/etc/shadow` instead.         |
| UID      | The user ID of the user.                                           |
| GID      | The group ID of the user's primary group.                          |
| GECOS    | The text of a user. Usually contains the user's full name.         |
| HOME     | The user's home directory.                                         |
| SHELL    | The user's default shell.                                          |

!!! info "Info"
    A user's password is actually encrypted and kept in the `/etc/shadow` file for security reasons.

There are a few basic commands to use to manage users on a Linux machine. These commands are `useradd`, `userdel`, and `usermod` and they are used to add, remove, and modify users respectively.

### `useradd`

The `useradd` command is used to create a new user. This command takes many options that allow you to specific different parameters for the new user. You can also use this command to create a system user.

!!! example "Example: Usage of `useradd`."

    Create a new user named `alice`.

    ```
    $ sudo useradd alice
    ```

    Create a new system user named `alice_system`.

    ```
    $ sudo useradd -r alice_system
    ```

### `userdel`

The `userdel` command deletes a user. By default deleting a user does not delete their home directory. You can use the `-r` option to delete the home directory.

!!! example "Example: Usage of `userdel`."

    Delete the user `alice`.

    ```
    $ sudo userdel alice
    ```

    Delete the user `alice_system` and their home directory.

    ```
    $ sudo userdel -r alice_system
    ```

### `usermod`

The `usermod` command modifies an existing user account. You can do many things such as change the user's home directory, change the user's group memberships, and change the user's shell. One of the most common things to use `usermod` for is to add a user to an additional group.

!!! example "Example: Usage of `usermod`."

    Add the user `alice` to the `wheel` group.

    ```
    $ sudo usermod -aG wheel alice
    ```

## Managing Groups

Groups are used to group users together based on a common attribute such a job function or role. Groups can be empty or contain many members. Every user on a Linux system must belong to at least one group but can belong to many groups. If a user belongs to many groups, one of the groups must be designated as their primary group. A primary group is used as the default group owner for file permissions when a user creates or modifies a file.

Information for all of the groups on a Linux system is kept in the `/etc/group` file. This is a `:` delimited file that contains information about a group in the following format:

```
GROUPNAME:PASSWORD:GID:MEMBERS
```

| Field     | Description                                       |
| --------  | ------------------------------------------------- |
| GROUPNAME | The group name.                                   |
| PASSWORD  | The group password. Not utilized anymore.         |
| GID       | The group ID of the group.                        |
| MEMBERS   | A `,` delimited list of the members of the group. |

There are a few basic commands to use to manage groups on a Linux machine. These commands are `groupadd`, `groupdel`, and `groupmod` and they are used to add, remove, and modify groups respectively.

### `groupadd`

The `groupadd` command is used to create a new group. This command takes many options that allow you to specific different parameters for the new group. You can also use this command to create a system group.

!!! example "Example: Usage of `groupadd`."

    Create a new group named `engineering`.

    ```
    $ sudo groupadd engineering
    ```

    Create a new system group named `engineering_system`.

    ```
    $ sudo groupadd -r engineering_system
    ```

### `groupdel`

The `groupdel` command deletes a group.

!!! example "Example: Usage of `groupdel`."

    Delete the group `engineering`.

    ```
    $ sudo groupdel engineering
    ```

    Delete the group `engineering_system`.

    ```
    $ sudo groupdel engineering_system
    ```

### `groupmod`

The `groupmod` command modifies an existing group. The most common use-case for this command is to change the GID of the group.

!!! example "Example: Usage of `groupmod`."

    Change the GID of the `engineering` group to `1200`.

    ```
    $ sudo groupmod -g 1200 engineering
    ```

## Changing a Password

### `passwd`

The `passwd` command is used to change a user's password. Aside from chaning a user's password, this command can be used to lock and unlock a user's account.

!!! example "Example: Usage of `passwd`."

    Change the password for the `alice` user.

    ```
    $ sudo passwd alice
    ```
