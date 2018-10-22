# Device Configuration

Now that we understand what devices are and how they are named, let's see how we can configure a new device for use. We'll be focusing on hard disk devices since that's the most common device to add to a Linux system. We learned earlier that Linux does not have a concept of drive letters. Now we'll learn how to configure a new disk and add it to the file system hierarchy.

## Connecting the Disk

The first thing to do when configuring a new device for use is to add the device to the system. If you are working on a physical system, this is usually just as simple as connecting the device to the system and powering the system up. If you have followed the Getting Started guide for this course then your devices are already "plugged in" and ready to be configured. 

## Formatting the Disk

After the disk is connected, we can optionally format the disk to erase any existing partition tables and data. The best, and most dangerous way, to format a disk in Linux is using the `dd` command.

### `dd`

The `dd` command is used to perform a bit for bit copy of one block device onto another block device. Depending on who you speak to, the `dd` command stands for "disk duplicator" or "disk destroyer". It's a powerful command that should be used with caution as it provides no output and may take a long time depending on how large the block devices are. One common use case for the `dd` command is to format disks.

!!! example "Example: Usage of `dd`."

    Completely format the entire disk `/dev/sdb`.

    ```
    $ sudo dd if=/dev/zero of=/dev/sdb
    ```

    Completely format the first partition of the disk `/dev/sdb`.

    ```
    $ sudo dd if=/dev/zero of=/dev/sdb1
    ```

## Partitioning the Disk

In order to create a file system, you must first have a partition table on the disk. Disks can be partitioned using either the Master Boot Record (MBR) or GUID Partition Table (GPT) partition tables. Before you choose a partition table, keep in mind that MBR partitions can only have 4 partitions of up to 2.2 TiB each while GPT partitions can have "unlimited" partitions up to 1 billion TiB each.

There are a few commands you can use to create partition tables. One such command is `fdisk`, which is used to create MBR partition tables on a disk. Another command is `gdisk` which is used to create GPT partition tables on a disk. The other is `parted` which can create both MBR and GPT partition tables on a disk. In this course we'll focus solely on `fdisk`.

### `fdisk`

The `fdisk` command is used to create an MBR partition table on a disk. Be cautious when using this command as you can permanently corrupt your disk if you are not careful. Once you partition a disk, you'll see another entry when using the `lsblk` command.

!!! example "Example: Usage of `fdisk`."

    Use `fdisk` to begin partitioning the `/dev/sdb` disk. Once you are in `fdisk` you can use the `m` command to print the help for `fdisk`.

    ```
    $ sudo fdisk /dev/sdb
    ```

## Creating a File System on the Disk

Once you have a partition you can then create a file system on that partition. A file system is needed to read and write files to the disk. You can have different file systems on different partitions if you wish. Some of the common file systems in Linux are `ext3`, `ext4`, and `xfs`. For this course, we'll be using `xfs`.

To create a filesystem, we use the `mkfs.TYPE` command where `TYPE` is the type of filesystem you want to create. For example, to create an xfs file system, you would use the `mkfs.xfs` command.

!!! example "Example: Usage of `mkfs.xfs`."

    Create an `xfs` file system on the partition `/dev/sdb1`.

    ```
    $ sudo mkfs.xfs /dev/sdb1
    ```

    Create an `ext4` file system on the partition `/dev/sdb2`.

    ```
    $ sudo mkfs.ext4 /dev/sdb2
    ```

## Mounting and Unmounting the Disk

Before you can read and write files to and from a disk, the disk must be mounted. When you mount a disk, you assign a directory on the file system, usually called a mount point, to the disk. Any files inside this directory will be written to the assigned disk. If we mount the disk `/dev/sdb1` to the location `/mnt/data01`, any files written inside the `/mnt/data01` directory will be written to the disk `/dev/sdb1`. This is how Linux alleviates the need for drive letters. Keep in mind that the directory that you want to mount a disk at must already exist. Once you have a directory to use for mounting a disk, we can use the `mount` command to mount the disk.

### `mount`

The `mount` command is used to mount a disk to a directory. Disks mounted this way do not persist on a reboot. If you reboot your system, you must mount the disk again. We'll cover how to mount disks persistently shortly but for now remember that the directory that you want to use as the mount point must already exist.

!!! example "Example: Usage of `mount`."

    Mount the `/dev/sdb1` disk to the directory `/mnt/data01`.

    ```
    $ sudo mkdir /mnt/data01
    $ sudo mount /dev/sdb1 /mnt/data01
    ```

### `/etc/fstab`

If you want to mount a disk that will persist upon reboot, you must add a mount defition to the `/etc/fstab` file. An easy way to remember `/etc/fstab` is to know that "fstab" stands for "file system table". All of the persistent mount definitions for a system are located in the `/etc/fstab` file. Once you add a mount definition into `/etc/fstab` you can use the command `mount -a` to mount all definitions listed in `/etc/fstab`. This file has the following layout:

```
fs_spec fs_file fs_vfstype fs_mntops fs_freq fs_passno
```

These columns are detailed below:

| Column       | Descripton                                                                                               |
| ------------ | -------------------------------------------------------------------------------------------------------- |
| `fs_spec`    | The device or UUID of a device to be mounted.                                                            |
| `fs_file`    | The directory to mount the device at.                                                                    |
| `fs_vfstype` | The filesystem type. Usually `ext4` or `xfs`.                                                            |
| `fs_mntops`  | The mount options to use for mounting. Usually set to `defaults`.                                        |
| `fs_freq`    | Whether the filesystem should be dumped. Usually set to `0`.                                             |
| `fs_passno`  | The order that the file systems will be checked by `fsck`. Usually set to `1` for `/` and `2` otherwise. |

!!! warning "Warning"

    Corrupting the `/etc/fstab` file can render your system unusable. Always make sure to double check your edits.

!!! example "Example: Overview of `/etc/fstab`."

    Show the entries in `/etc/fstab`.

    ```
    $ sudo cat /etc/fstab

    #
    # /etc/fstab
    # Created by anaconda on Sat May 12 18:50:26 2018
    #
    # Accessible filesystems, by reference, are maintained under '/dev/disk'
    # See man pages fstab(5), findfs(8), mount(8) and/or blkid(8) for more info
    #
    /dev/mapper/VolGroup00-LogVol00 /                       xfs     defaults        0 0
    UUID=570897ca-e759-4c81-90cf-389da6eee4cc /boot                   xfs     defaults        0 0
    /dev/mapper/VolGroup00-LogVol01 swap                    swap    defaults        0 0
    ```

    Adding an entry for the disk `/dev/sdb1` to `/etc/fstab` and then mounting the entries using `mount -a`.

    ```
    $ lsblk -f
    NAME                    FSTYPE      LABEL UUID                                   MOUNTPOINT
    sda
    ├─sda1
    ├─sda2                  xfs               570897ca-e759-4c81-90cf-389da6eee4cc   /boot
    └─sda3                  LVM2_member       vrrtbx-g480-HcJI-5wLn-4aOf-Olld-rC03AY
      ├─VolGroup00-LogVol00 xfs               b60e9498-0baa-4d9f-90aa-069048217fee   /
      └─VolGroup00-LogVol01 swap              c39c5bed-f37c-4263-bee8-aeb6a6659d7b   [SWAP]
    sdb
    └─sdb1                  xfs               2350706e-ff89-4292-a9e2-02d0c614b93d
    sdc

    $ sudo echo "UUID=2350706e-ff89-4292-a9e2-02d0c614b93d /mnt xfs defaults 0 2" >> /etc/fstab
    $ sudo mount -a
    ```

### `umount`

The `umount` command is used to unmount a disk. This command is often mispelled `unmount` but it is indeed `umount`. You can unmount a disk using the mount point or the disk name.

!!! example "Example: Usage of `umount`."

    Unmounting a device that's mounted at `/mnt/data01`.

    ```
    $ sudo umount /mnt/data01
    ```

    Unmounting the device `/dev/sdb1` regardless where it's mounted.

    ```
    $ sudo umount /dev/sdb1
    ```

## Disk Usage

There are two major commands to use to determine the disk usage. These commands are `df` which stands for "disk free" and `du` which stands for "disk usage". The difference between these commands are that `df` shows the usage per mount point while `du` shows the usage of files.

### `df`

!!! example "Example: Usage of `df`."

    Show the file system disk usage.

    ```
    $ sudo df
    Filesystem                      1K-blocks   Used Available Use% Mounted on
    /dev/mapper/VolGroup00-LogVol00  39269648 835700  38433948   3% /
    devtmpfs                           931672      0    931672   0% /dev
    tmpfs                              941416      0    941416   0% /dev/shm
    tmpfs                              941416   8668    932748   1% /run
    tmpfs                              941416      0    941416   0% /sys/fs/cgroup
    /dev/sda2                         1038336  64076    974260   7% /boot 
    tmpfs                              188284      0    188284   0% /run/user/1000
    ```

    Show the file system disk usage in human readable format.

    ```
    $ df -h
    Filesystem                       Size  Used Avail Use% Mounted on
    /dev/mapper/VolGroup00-LogVol00   38G  817M   37G   3% /
    devtmpfs                         910M     0  910M   0% /dev
    tmpfs                            920M     0  920M   0% /dev/shm
    tmpfs                            920M  8.5M  911M   1% /run
    tmpfs                            920M     0  920M   0% /sys/fs/cgroup
    /dev/sda2                       1014M   63M  952M   7% /boot
    tmpfs                            184M     0  184M   0% /run/user/1000
    ```

### `du`

!!! example "Example: Usage of `du`."

    Show the disk usage of all files in the `/etc` directory.

    ```
    $ sudo du /etc
    ...
    12	/etc/audit
    148	/etc/postfix
    0	/etc/qemu-ga/fsfreeze-hook.d
    4	/etc/qemu-ga
    4	/etc/sudoers.d
    30612	/etc
    ```
    
    Show the disk usage of all files in the `/etc` directory in human readable format.

    ```
    $ sudo du -h /etc
    ...
    12K	/etc/audit
    148K	/etc/postfix
    0	/etc/qemu-ga/fsfreeze-hook.d
    4.0K	/etc/qemu-ga
    4.0K	/etc/sudoers.d
    30M	/etc
    ```

    Show the summary of disk usage of the entire `/etc` directory.

    ```
    $ sudo du -s /etc
    30612 /etc
    ```

