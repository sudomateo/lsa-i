# The File System

## Filesystem Basics

In order to understand more about using a shell, we must go over how files are handled in Linux. This can be summed up in one sentence.

**Everything in Linux is treated as a file!**

Linux treats everything as a file, including directories, links, programs, storage devices, the keyboard, and the monitor. When you log into your Linux machine and start a shell session, you will be located at a specific location on the filesystem. The default directory that a user is placed into when they log in is called the **home directory**. By default, a user's home directory is located at `/home/username` where _username_ is the name of the user. For example, a user named _vagrant_ may have a home directory of `/home/vagrant`. 

As you move around the file system your **current working directory** will change. The current working directory is the **file path** of the directory you currently reside in. A file path is how you reference a file on the filesystem. There are two types of file paths; an **absolute path** and a **relative path**. Knowing the difference between them will help prevent mistakes. An absolute path is the entire location of a file beginning with `/`. For example, a file `/home/vagrant/myfile`is an absolute path. A relative path is the location of a file relative to your current working directory. For example, assuming your current working directory is `/home/vagrant` a relative file path may simply be `myfile`. When using a relative path, Linux is essentially concatenating the current working directory with the relative path to make an absolute path. It's always preferably to access a file using an absolute path, especially when accessing a file via a script or other program.

I mentioned earlier that an absolute path begins with `/`, commonly called the root of the filesystem. If you are coming from the Windows world, file paths usually start with a letter such as `C:\Users\username` or `D:\Data`. Since Linux does not have a concept of drive letters like Windows, all files begin at the root of the filesystem, or `/`. In an absolute path, only the leading `/` is special, every other`/` is just a separator between directories and files. For example we can break down an absolute path for the file `/home/vagrant/myfile` to be:

```text
/                    # The root of the filesystem
└── home             # A directory named home
    └── vagrant      # A directory named vagrant
        └── myfile   # A file named myfile
```

No matter which drive a file resides on, every absolute path to that file will start with `/`. Since Linux does not have a concept of drive letters, you can have a file located at `/home/vagrant/myfile` reside on a completely different drive than a file located at `/var/log/mylog`.

In Linux, files are case sensitive. That means a file named `/home/vagrant/myfile` is different than a file named `/home/vagrant/MyFile`. Because of this, it's considered best practice to keep all files lower-case. 

## Filesystem Syntax

There are a few special characters that you can use as a shorthand when working with files:

| Character  | Name          | Description                                                      |
| ---------- | ------------- | ---------------------------------------------------------------- |
| `~`        | tilde         | Refers to the current user's home directory.                     |
| `.`        | dot           | Refers to the current working directory or a hidden file.        |
| `..`       | dot dot       | Refers to the parent directory of the current working directory. |
| `/`        | forward slash | The root of a filesystem or a separator for directories.         |
