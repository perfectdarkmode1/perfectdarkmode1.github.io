---
title: The Linux Filesystem
date: 2023-11-06T06:20:36-07:00
draft: true
---
Filesystem Hierarchy

$ ls -l /

/ \- The root directory of the entire filesystem hierarchy, everything is nested under this directory.

/bin - Essential ready-to-run programs (binaries), includes the most basic commands such as ls and cp.

/boot - Contains kernal boot loader files.

/dev - Device files.

/etc - Core system configuration directory, should hold only configuration files and not any binaries.

/home - Personal directories for users

/lib - Holds library files that binaries can use.

/media - Used as an attachment point for removable media like USB drives.

/mnt - Temporarily mounted filesystems

/opt - Optional application software packages.

/proc - info about currently running processes

/root - The root user's home directory

/run - information about the running system since the last boot.

/sbin - Contains essential system binaries, usually can only be ran by root.

/srv - Site-specific data which are served by the system.

/tmp - Storage for temporary files

/usr - Meant for user installed software and utilities. Inside this directory are sub directories for /usr/bin, /usr/local, etc.

/var - Variable directory, used for system logging, user tracking, caches, etc. Things that are subject to change all the time.

Filesystem Types

Virtual File System (VFS) abstraction layer.

The layer between appllications and the different file system types.

Journaling

Comes by default on MOST filesystem types. A log file that keeps track of what you are doing when moving files. Will keep track of where you left off in case the system loses power.

Common Desktop Filesystem types

ext4 - This is the most current version of native Linux filesystems. Compatible with the older ext2 and ext3 versions. Supports disk volumes up to 1 exabyte and file sizes up yo 16 terabytes and more. Standard choice for Linux filesystems.

Btrfs - "Better or Butter FS" it is a new filesystem for Linux that comes with snapshots, incremental backups, performance increase and much more. It is widely available, but not quite stable/ compatible yet.

XFS - High performance journaling file system, great for system with large files such as media server,

NTFS and FAT - Windows Filesystems

HFS+ - Macintosh filesystem

$ df -T

reports filesystem  disk space usage and other details about your disk.

Anatomy of a disk

Partition table

Every disk has a partition tables that shows the system how the disk is partitioned. It shows how partitions begin and end, which partitions are bootable, what sectors of the disk are allocated to what partition, etc. There are two main partition tables schemes used, Master Boot Record (MBR) and GUID Partition Table (GAPT)

Partition

Partitions can't overlap each other. Free space is disk space that is not allocated to a partition.

MBR

\- Traditional partition table

\- Can have primary, extended, and logical partitions

\- MBR has a limit of four primary partitions

\- Additional partitions can be made by making a primary partition into an extended partition (there can only be one extended partition on a disk). Then inside the extended partition you add logical partitions.

\- Supports disks up to 2 Terabytes.

GPT

\- GUID Partition Table (GPT) is becoming the new standard for disk partitioning.

\- Has only one type of partition and you can make many of them.

\- Used mostly in conjunction with UEFI based booting

Filesystem structure

Boot block

Located int the first few sectors of the filesystem. It is not really used by the filesystem. It contains information used to boot the operating system. Only one boot block is needed by the operating system. There are unused boot blocks in partitions that don't have boot info.

Super block

A single block that comes after the boot block that contains info about the filesystem. Info includes the size of the inode table, size of logical blocks , and size of the filesystem.

Inode table

The database that manages files. Each file or directory has a unique entry in the inode table and it has various info about the file.

Data blocks

The actual data for the files and directories.

$ sudo  parted -l

to view a partition table

Disk /dev/sda: 21. 5GB 
Sector size (logical/phystcal) 
Partition Table: msdos 
Disk Flags: 
Number start 
1049kB 
539MB 
539MB 
End 
538MB 
21.5GB 
21.5GB 
size 
537MB 
20 .9GB 
20 .9GB 
: 51281512B 
T ype 
primary 
extended 
Logical 
File system 
fa t32 
Flags 
boot ">

( MBR example )

Disk Partitioning

Tools to partition a disk

fdisk - basic command-line partitioning tool, it does not support GPT

parted - command line tool that supports both MBR and GPT partitioning

gparted - GUI version of parted

gdisk - fdisk, but only supports GPT

$ sudo parted

Enters the parted tool

select /dev/sdb2

selects the device

mkpart primary 123 4567

to make the partition

$ resize 2 1234 3456

to resize a partition. Select the partition number and then start and end points of where you want to resize it to.

Creating filesystems

$ sudo mkfs -t ext4 /dev/sdb2

Allows you to specify the type of filesystem and where it goes. You only want to create a filesystem on a newly partitioned disk or if you are repartitioning an old one. (Otherwise it will probably get corrupted.

Mount and umount

A new filesystem must be mounted before you can view its contents. You want to mount it to a mount point.

What you need:

- Device Location
- Filesystem type
- Mount point

Mount Point = Directory that the filesystem attaches to:

Mount filesystem

$ sudo mount -t ext4 /dev/sdb2 /mydrive

Unmount

$ sudo umount /mydrive

Or

$ sudo umount /dev/sdb2

- Kernel names devices in the order it finds them
- Device name could change after you mount it
- You can use the devices UUID to identify it instead of a name

View UUIDs for block devices (device name, UUID, filesystem type

$ sudo blkid

Mount w/ UUID

$ sudo mount UUID=(insert ID here) /my drive

- Secondary hard drives must be mounted by UUID

/etc/fstab ("eff es tab") (filesystem table)

- List of mounted filesystems

Show contents of /etc/fstab (UUID, mount point, filesystem type, options dump, pass)

$ cat /etc/fstab

Dump = used by dumb utility to decide when to take a backup (default is 0)

Pass = used by fsck to decide what order to check filesystems - value of 0 will not be checked

- You can add an entry manually by editing the file syntax matching other entries

SWAP

- Storage if you are low on memory
- Space for idle processes to go to make room in RAM
- Allocate twice as much swap as memory (usually)

Steps to use a partition as swap space:

1.  Use an empty partition
2.  Initialize swap areas

$ mkswap /dev/sdb2

1.  Enable swap device

$ swapon  /sdb2/dev

1.  Add entry to /etc/fstab (so this swap partition persists on bootup)

1.  Use "sw" for filesystem type

Remove swap

$ swapoff /dev/sdb2

Disk Usage

Show filesystem utilization (disk free)

$ df -h

- -h = human readable
- shows current directory

Show filesystem (disk usage)

$ du -h

- See what files are taking up space in the current directory

Show disk usage for root

$ du -h /

Filesystem Repair

- Sudden shutdowns can corrupt data

Filesystem check (fsck)

- Check consistency of a filesystem
- Attempt to repair filesystem
- Ran before disk is mounted on boot

Run fsck Manually (from a rescue disk because filesystem being checked cannot be mounted)

$ sudo fsck /dev/sda

Inodes (Index Nodes)

The Filesystem

Inodes (Index Nodes)

Inode Table: database that manages files in the filesystem

Inode: Entry in the inode table that describes each file (1 Inode for each file)

Every # must be unique

cannot be referenced across different filesystems

Contains:

filetype

\- regular

\- directory

\- Character device

\- etc.

owner

group

Access Permissions

Timestamps

\- mtime (time last modified)

\- ctime (attribute change)

\- atime (last access)

\# of hardlinks

File Sizw

\# of blocks

Pointers to data blocks (important)

Does not contain the filename or the file itself

When inodes are created

Space for inodes is allocated when the filesystem is created

Algorithm determines amount of space needed

out of inode space errors can occur

View inodes/ how many are left:

$ df -i

Inode Information

Identified by numbers

files get inode number when they are created

numbers are assigned in sequential order

numbers are reused after the old inode is deleted

view inode numbers

$ls -li

View detailed info about file and the inode

$stat ~/Desktop/

How Inodes locate files

point to files in the data blocks

usually contain 15 pointers

13th pointer points to block containing other pointers

14th pointer points to more pointers

15th pointer points to more pointers

1st 12 pointers can find small files quickly

Symlinks (symbolic links)

3rd field in ls command is link count (hard links)

equivalent of windows shortcuts

Hard Link= file with a link to an inode

Create a symlink

$ln -s myfile myfile4

ls -li

1598657 -rw-rw-r-- 1 david.thomas david.thomas 7 Jul 21 14:19 myfile

1581638 lrwxrwxrwx 1 david.thomas david.thomas 6 Aug 4 14:21 myfile4 -> myfile

New inode is created

File gets modified

Can be referenced accross different filesystems

Hardlinks

Hard link a file

$ln myfile myhardlinkls

Will show the same inode#

Modifications to one file will change both

Link count goes down when file is removed

Inode gets deleted once all hardlinks are removed
