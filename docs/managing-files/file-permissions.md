# File Permissions

Linux uses file permissions to control access to files and directories. Linux has a concept of basic and special permissions for files. Let's take a look at basic permissions first.

## Basic Permissions

There are three basic permissions in Linux as denoted by the following table.

| Permission | Letter | Octal | Description                                                                      |
| ---------- | ------ | ----- | -------------------------------------------------------------------------------- |
| read       | `r`    | `4`   | Grants the ability to read the file and list its permissions.                    |
| write      | `w`    | `2`   | Grants the ability to modify and delete the file.                                |
| execute    | `x`    | `1`   | Grants the ability to execute the file as a script or change into the directory. |

Each of these permissions can be applied to the file user owner (user), the file group owner (group), or everyone else (other). Since we have three permissions that can be assigned to three different entities we have nine different permissions as denoted below.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
 ^^^^^^^^^
```

### Letter Format

Let's break down some permissions in letter format.

!!! example "Example: Breaking down permissions in letter format."

    The first group of permissions are the user permissions which are `rw-`. This means the user owner has read and write permissions on the file.

    ```
    rw-rw-r--
    ^^^
    ```

    The second group of permissions are the group permissions which are `rw-`. This means the group owner has read and write permissions on the file.

    ```
    rw-rw-r--
       ^^^
    ```

    The third group of permissions are the other permissions which are `r--`. This means everyone else has read permissions on the file.

    ```
    rw-rw-r--
          ^^^
    ```

### Octal Format

Let's break down these same permissions again but in octal format.

!!! example "Example: Breaking down permissions in octal format."

    The first group of permissions are the user permissions which are `rw-`. In octal this would be `r + w = 4 + 2 = 6`.

    ```
    rw-rw-r--
    ^^^
    ```

    The second group of permissions are the group permissions which are `rw-`. In octal this would be `r + w = 4 + 2 = 6`.

    ```
    rw-rw-r--
       ^^^
    ```

    The third group of permissions are the other permissions which are `r--`. In octal this would be `r = 4`.

    ```
    rw-rw-r--
          ^^^
    ```

Putting all of these permissions together results in the octal number `0664`. The leading `0` is reserved for special permissions, which we'll cover shortly.

!!! example "Example: Decoding permissions into octal format."
    Given the permissions `rwxrw-r--`. We can determine the octal number is `0764`.

    * User permissions are `rwx` which is `r + w + x = 4 + 2 + 1 = 7`.
    * Group permissions are `rw-` which is `r + w = 4 + 2 = 6`.
    * Other permissions are `r--` which is `r = 4`.

## Special permissions

In addition to the three basic permissions, there are also three special permissions.

| Permission          | Letter (with execute) | Letter (without execute) | Octal | Description                                                                                                                          |
| ------------------- | --------------------- | ------------------------ | ----- | ------------------------------------------------------------------------------------------------------------------------------------ |
| set user ID (SUID)  | `s`                   | `S`                      | `4`   | This permission allows a file to be executed as the user owner of the file regardless of the user that actually executes the file.   |
| set group ID (SGID) | `s`                   | `S`                      | `2`   | This permission allows a file to be executed as the group owner of the file regardless of the group that actually executes the file. |
| Sticky bit          | `t`                   | `T`                      | `1`   | Files with this permission can only be deleted by the owner and `root`. Useful for shared directories like `/tmp`.                   |

If a special permission is lowercase, that means the underlying execute permission is granted (`x`). If a special permission is uppercase, that means the underlying execute permission is not granted (`-`).

!!! example "Example: Breaking down special permissions."

    The SUID permission and the underlying execute permission are set.

    ```
    rwsrwxrwx
      ^
    ```

    The SGID permission and the underlying execute permission are set.

    ```
    rwxrwsrwx
         ^
    ```

    The sticky bit permission and the underlying execute permission are set.

    ```
    rwxrwxrwt
            ^
    ```
    
    The SUID permission is set but NOT the underlying execute permission.

    ```
    rwSrw-rw-
      ^
    ```

    The SGID permission is set but NOT the underlying execute permission.

    ```
    rw-rwSrw-
         ^
    ```

    The sticky bit permission is set but NOT the underlying execute permission.

    ```
    rw-rw-rwT
            ^
    ```

In octal format, the special permissions are added to the front to create four digits.

!!! example "Example: Decoding special permissions."

    Given the permissions `rwsr-xr-x`. We can determine the octal number is `4755`.

    * Special permissions are `s--` which is `s = 4`.
    * User permissions are `rwx` which is `r + w + x = 4 + 2 + 1 = 7`.
    * Group permissions are `r-x` which is `r + x = 4 + 1 = 5`.
    * Other permissions are `r-x` which is `r + x = 4 + 1 = 5`.

    Given the permissions `rwxr-Sr-x`. We can determine the octal number is `2745`.

    * Special permissions are `-S-` which is `S = 2`.
    * User permissions are `rwx` which is `r + w + x = 4 + 2 + 1 = 7`.
    * Group permissions are `r--` which is `r = 4`.
    * Other permissions are `r-x` which is `r + x = 4 + 1 = 5`.


## File Permissions Commands

### `chown`

The `chown` command is used to change the ownership of a file. This can change both the user and group ownership.

!!! example "Example: Usage of `chown`."

    Change `file01` to be owned by the `vagrant` user.

    ```
    $ sudo chown vagrant file01
    ```

    Change `file01` to be owned by the `vagrant` user and `vagrant` group.

    ```
    $ sudo chown vagrant:vagrant file01
    ```

### `chgrp`

The `chgrp` command is used to change the group ownership of a file. Not too common since `chown` can do both.

!!! example "Example: Usage of `chgrp`."

    Change `file01` to be owned by the `vagrant` group.

    ```
    $ sudo chgrp vagrant file01
    ```

### `chmod`

The `chmod` command is used to change the permissions of a file. It accepts an octal number of permissions to set.

!!! example "Example: Usage of `chmod`."

    Change permissions `file01` to be `rwxr-xr--`.

    ```
    $ sudo chmod 0754 file01
    ```
