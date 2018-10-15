# Exercises

1. Drop down to the `root` user using the command `sudo su -`.
2. Verify the `/dev/sdb` and `dev/sdc` devices are attached to your system by running the command `lsblk`. You should see output similar to the following:
```
[root@lsa-i ~]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                       8:0    0   40G  0 disk
├─sda1                    8:1    0    1M  0 part
├─sda2                    8:2    0    1G  0 part /boot
└─sda3                    8:3    0   39G  0 part
  ├─VolGroup00-LogVol00 253:0    0 37.5G  0 lvm  /
  └─VolGroup00-LogVol01 253:1    0  1.5G  0 lvm  [SWAP]
sdb                       8:16   0    1G  0 disk
sdc                       8:32   0    1G  0 disk
```
3. Run the command `fdisk /dev/sdb` to begin formatting the device `dev/sdb`. Follow the subtasks below to format the device with 1 partition that takes up all the space:
    1. Type `n` and hit ++enter++ to create a new partition.
    2. Type `p` and hit ++enter++ to make this a primary partition.
    3. Type `1` and hit ++enter++ to make this primary partition the first partition on this device.
    4. Hit ++enter++ to accept the default first sector.
    5. Hit ++enter++ to accept the default last sector.
    6. Type `p` and hit ++enter++ to print the proposed partition changes. You should see the partition `/dev/sdb1`.
    7. Type `w` and hit ++enter++ to write these changes to the device and exit.
4. Verify the `/dev/sdb1` partition was created successfully by running the command `lsblk`. You should see output similar to the following:
```
[root@lsa-i ~]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                       8:0    0   40G  0 disk
├─sda1                    8:1    0    1M  0 part
├─sda2                    8:2    0    1G  0 part /boot
└─sda3                    8:3    0   39G  0 part
  ├─VolGroup00-LogVol00 253:0    0 37.5G  0 lvm  /
  └─VolGroup00-LogVol01 253:1    0  1.5G  0 lvm  [SWAP]
sdb                       8:16   0    1G  0 disk
└─sdb1                    8:17   0 1023M  0 part
sdc                       8:32   0    1G  0 disk
```
5. Run the command `mkfs.xfs /dev/sdb1` to create an XFS file system on the `/dev/sdb1` partition.
6. Run the command `lsblk -f` to list the UUID and file system type of the `/dev/sdb1` partition. You'll need this information for the `/etc/fstab` file.
7. Run the command `mkdir /mnt/exercise01` to create a directory to use for mounting the `/dev/sdb1` partition.
8. Add an entry to the `/etc/fstab` file to mount your `/dev/sdb1` device to the `/mnt/exercise01` directory. Your new entry should be similar to the following:
```
UUID=<DEVICE_UUID> /mnt/exercise01 xfs defaults 0 2
```
9. Run the command `mount -a` to read the `/etc/fstab` file and mount all currently unmounted devices.
10. Verify the `/dev/sdb1` partition was mounted successfully by running the `lsblk` command. You should see output simiar to the following:
```
[root@lsa-i ~]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                       8:0    0   40G  0 disk
├─sda1                    8:1    0    1M  0 part
├─sda2                    8:2    0    1G  0 part /boot
└─sda3                    8:3    0   39G  0 part
  ├─VolGroup00-LogVol00 253:0    0 37.5G  0 lvm  /
  └─VolGroup00-LogVol01 253:1    0  1.5G  0 lvm  [SWAP]
sdb                       8:16   0    1G  0 disk
└─sdb1                    8:17   0 1023M  0 part /mnt/exercise01
sdc                       8:32   0    1G  0 disk
```
11. Run the command `df -h` to see the current disk usage of the system. Take note of the value in the Used column for `/dev/sdb1`. My output is below.
```
[root@lsa-i ~]# df -h
Filesystem                       Size  Used Avail Use% Mounted on
/dev/mapper/VolGroup00-LogVol00   38G  823M   37G   3% /
devtmpfs                         910M     0  910M   0% /dev
tmpfs                            920M     0  920M   0% /dev/shm
tmpfs                            920M  8.5M  911M   1% /run
tmpfs                            920M     0  920M   0% /sys/fs/cgroup
/dev/sda2                       1014M   63M  952M   7% /boot
tmpfs                            184M     0  184M   0% /run/user/1000
/dev/sdb1                       1020M   33M  988M   4% /mnt/exercise01
```
12. Run the command `dd bs=1M count=50 if=/dev/urandom of=/mnt/exercise01/myfile` to create a file /mnt/exercise01/myfile with a size of around 50 MiB. This command may take a few seconds to run.
13. Run the command `df -h` to see the current disk usage of the system. Take note of the value in the Used column for `/dev/sdb1`. Notice how the value has increased by roughly 50 MiB. My output is below.
```
[root@lsa-i ~]# df -h
Filesystem                       Size  Used Avail Use% Mounted on
/dev/mapper/VolGroup00-LogVol00   38G  823M   37G   3% /
devtmpfs                         910M     0  910M   0% /dev
tmpfs                            920M     0  920M   0% /dev/shm
tmpfs                            920M  8.5M  911M   1% /run
tmpfs                            920M     0  920M   0% /sys/fs/cgroup
/dev/sda2                       1014M   63M  952M   7% /boot
tmpfs                            184M     0  184M   0% /run/user/1000
/dev/sdb1                       1020M   83M  938M   9% /mnt/exercise01
```
14. Run the command `fdisk /dev/sdc` to begin formatting the device `/dev/sdc`. Follow the subtasks below to format the device with 2 partitions with 256 MiB and 512 MiB respectively:
    1. Type `n` and hit ++enter++ to create a new partition.
    2. Type `p` and hit ++enter++ to make this a primary partition.
    3. Type `1` and hit ++enter++ to make this primary partition the first partition on this device.
    4. Hit ++enter++ to accept the default first sector.
    5. Type `+256M` and hit ++enter++ to give the partition a size of 256 MiB.
    6. Type `p` and hit ++enter++ to print the proposed partition changes. You should see the partition `/dev/sdc1`.
    7. Type `n` and hit ++enter++ to create another new partition.
    8. Type `p` and hit ++enter++ to make this a primary partition.
    9. Type `2` and hit ++enter++ to make this primary partition the second partition on this device.
    10. Hit ++enter++ to accept the default first sector.
    11. Type `+512M` and hit ++enter++ to give the partition a size of 512 MiB.
    12. Type `p` and hit ++enter++ to print the proposed partition changes. You should see the partition `/dev/sdc2`.
    13. Type `w` and hit ++enter++ to write these changes to the disk and exit.
15. Verify the `/dev/sdc1` and `/dev/sdc2` partitions were created successfully by running the command `lsblk`. You should see output similar to the following:
```
[root@lsa-i ~]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                       8:0    0   40G  0 disk
├─sda1                    8:1    0    1M  0 part
├─sda2                    8:2    0    1G  0 part /boot
└─sda3                    8:3    0   39G  0 part
  ├─VolGroup00-LogVol00 253:0    0 37.5G  0 lvm  /
  └─VolGroup00-LogVol01 253:1    0  1.5G  0 lvm  [SWAP]
sdb                       8:16   0    1G  0 disk
└─sdb1                    8:17   0 1023M  0 part /mnt/exercise01
sdc                       8:32   0    1G  0 disk
├─sdc1                    8:33   0  256M  0 part
└─sdc2                    8:34   0  512M  0 part
```
16. Run the command `mkfs.ext4 /dev/sdc1` to create an EXT4 file system on the `/dev/sdc1` partition.
17. Run the command `mkfs.xfs /dev/sdc2` to create an XFS file system on the `/dev/sdc2` partition.
18. Run the command `lsblk -f` to list the UUIDs and file system types of the `/dev/sdc1` and `/dev/sdc2` partitions. You'll need this information for the `/etc/fstab` file.
19. Run the command `mkdir /mnt/small` to create a directory to use for mounting the `/dev/sdc1` partition.
20. Run the command `mkdir /mnt/large` to create a directory to use for mounting the `/dev/sdc2` partition.
21. Add two entries to the `/etc/fstab` file to mount your `/dev/sdc1` and `/dev/sdc2` devices to the `/mnt/small` and `/mnt/large` directories respectively. Your new entries should be similar to the following:
```
UUID=<DEVICE_UUID> /mnt/small ext4 defaults 0 2
UUID=<DEVICE_UUID> /mnt/large xfs defaults 0 2
```
22. Run the command `mount -a` to read the `/etc/fstab` file and mount all currently unmounted devices.
23. Verify the `/dev/sdc1` and `/dev/sdc2` partitions were mounted successfully by running the `lsblk` command. You should see output simiar to the following:
```
[root@lsa-i ~]# lsblk
NAME                    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda                       8:0    0   40G  0 disk
├─sda1                    8:1    0    1M  0 part
├─sda2                    8:2    0    1G  0 part /boot
└─sda3                    8:3    0   39G  0 part
  ├─VolGroup00-LogVol00 253:0    0 37.5G  0 lvm  /
  └─VolGroup00-LogVol01 253:1    0  1.5G  0 lvm  [SWAP]
sdb                       8:16   0    1G  0 disk
└─sdb1                    8:17   0 1023M  0 part /mnt/exercise01
sdc                       8:32   0    1G  0 disk
├─sdc1                    8:33   0  256M  0 part /mnt/small
└─sdc2                    8:34   0  512M  0 part /mnt/large
```
24. Practice these and other commands until you feel comfortable with them. You'll need to run `vagrant destroy` and then `vagrant up` to reset your virtual machine if you wish to do these exercises over.
25. When finished, use the exit command to exit the shell and logout.
