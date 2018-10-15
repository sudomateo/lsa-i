# Device Basics

Linux stores data on devices just like many other operating systems. There are many different types of devices but the most common ones are hard disk drives (HDD) and solid state drives (SSD). These devices may be connected to different interfaces on your system. We'll go over a few of these interfaces now.

## Device Interfaces

There are many different types of devices ranging from CDs all the way to SSDs. These devices all connect to the system through a varying range of interfaces detailed below.

| Interface                                        | Description                                                           |
| ------------------------------------------------ | --------------------------------------------------------------------- |
| Serial Advanced Technology Attachment (SATA)     | This is the most widely used interface in mainstream systems.         |
| mini SATA (mSATA)                                | A smaller interface for SATA drives designed to save space.           |
| Universal Serial Bus (USB)                       | Interface used for portable disks and other peripherals.              |
| Next Generation Form Factor (M.2)                | Replacement for mSATA with higher transfer rates.                     |
| Small Computer System Interface (SCSI)           | Usually found in servers but unpopular today due to SATA advancement. |
| Peripheral Component Interconnect Express (PCIe) | Used for graphics cards and other system devices.                     |

## Device Naming Conventions

Disks are located in the `/dev` directory and follow a specific naming convention. Entire disks are often named using the format `/dev/sda`, `/dev/vda`, or `/dev/hda` while partitions of a disk are named using the format `/dev/sda1`, `/dev/vda1`, and `/dev/hda1`. Entire disks start their naming at `a` and partitions start at `1`. Given a disk named `/dev/sdb3` we can determine that this is the third partition on the second disk. Disks that begin with `sd`, `vd`, or `hd` refer to SATA disks, virtualized disks, and IDE disks respectively although many modern technologies abstract this away from the user and usually present disks using the `sd` prefix.

!!! example "Example: Showing the differences between disk names."
    
    The entire first SATA disk

    ```
    /dev/sda
    ```

    The first partition on the second virtualized disk

    ```
    /dev/vdb1
    ```

    The second partition on the first IDE disk

    ```
    /dev/hda2
    ```

## Finding Block Devices

### `lsblk`

The `lsblk` command is used to list all block devices that are currently attached to the system. This is useful for seeing if your newly attached device is being seen by the system.

!!! example "Example: Usage of `lsblk`."
    
    List all block devices attached to the system.

    ```
    $ lsblk
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

    List all block devices attached to the system and their file system type.

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
    sdc
    ```
