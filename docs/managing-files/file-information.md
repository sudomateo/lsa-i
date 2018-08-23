# File Information

We saw earlier than running the `ls -l` command produces a long listing of the files at a given file path. This long listing looks like the following.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
```

Let's disect what this output means.

The first character indicates the type of the file. A `-` is a regular file, a `d` is a directory, and an `l` is a link.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
^
```

These next nine characters indicate the permissions for the file. We'll discuss permissions in depth later.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
 ^^^^^^^^^
```

This next character indicates if the file has an access control list configured on it. A `.` indicates the file has an SELinux context while a `+` indicates a general file access control list.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
          ^
```

The meaning of this character varies whether the file is a file or directory. If the file is a file, this indicates the number of links the file has. If the file is a directory, this indicates the number of subdirectories.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
            ^
```

This indicates the user that owns the file.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
              ^^^^^^^
```

This indicates the group that owns the file.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
                      ^^^^^^^
```

This indicates the size of the file in bytes.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
                              ^
```

This indicates the date and time the file was last modified.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
                                ^^^^^^^^^^^^
```

This is the name of the file.

```
-rw-rw-r--. 1 vagrant vagrant 0 Aug 22 03:04 file01
                                             ^^^^^^
```
