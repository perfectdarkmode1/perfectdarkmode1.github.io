
This chapter describes the following major topics:

[![](images/00001.jpeg){.c37}]{.c36}Understand file systems and their
benefits, categories, and types

[![](images/00001.jpeg){.c37}]{.c36}Review file system types: Ext3/Ext4,
XFS, VFAT, and ISO9660

[![](images/00001.jpeg){.c37}]{.c36}Know file system administration
commandset

[![](images/00001.jpeg){.c37}]{.c36}Mount and unmount file systems
manually and persistently

[![](images/00001.jpeg){.c37}]{.c36}Determine and use UUID

[![](images/00001.jpeg){.c37}]{.c36}Apply and use file system label

[![](images/00001.jpeg){.c37}]{.c36}Monitor file system and directory
usage

[![](images/00001.jpeg){.c37}]{.c36}Create and mount different types of
local file systems in partitions

[![](images/00001.jpeg){.c37}]{.c36}Create and mount XFS file system in
VDO volume

[![](images/00001.jpeg){.c37}]{.c36}Create, mount, and resize Ext4 and
XFS file systems in LVM

[![](images/00001.jpeg){.c37}]{.c36}Create, mount, and expand Stratis
file system

[![](images/00001.jpeg){.c37}]{.c36}Understand, create, and activate
swap in partitions and LVM

[RHCSA Objectives:]{.c39}

[31]{#part0027_split_000.html#id_797 .calibre10}[.]{.c29}Configure
systems to mount file systems at boot by Universally Unique ID (UUID) or
label

[32]{#part0027_split_000.html#id_798 .calibre10}[.]{.c29}Add new
partitions and logical volumes, and swap to a system nondestructively
(the first part of this objective is covered in more detail in Chapter
14)

[33]{#part0027_split_000.html#id_799 .calibre10}[.]{.c29}Create, mount,
unmount, and use vfat, ext4, and xfs file systems

35[.]{.c29}Extend existing logical volumes (more details in Chapter 14
also)

::: {#part0027_split_000.html#calibre_pb_1 .calibre12}
:::

[]{#part0027_split_001.html}

[ F]{.c42}[ile]{.c43} systems are the most common structures created in
partitions and volumes regardless of the underlying storage management
solution employed. They are logical containers employed for file storage
and can be optimized, resized, mounted, and unmounted independently.
They must be connected to the root of the directory hierarchy in order
to be accessed by users and applications. This may be accomplished
automatically at system boot or manually when required. File systems can
be mounted or unmounted using their unique identifiers, labels, or
device files. There is a whole slew of commands available for file
system creation and administration; some of them are file system type
specific while others are general.

The other common structure created in partitions and logical volumes is
the swap space. Swapping provides a mechanism to move out and in pages
of idle data between the physical memory and the swap. Swap areas act as
extensions to the physical memory, and they may be activated or
deactivated independent of swap spaces located in other partitions and
volumes.

This chapter is the last one in the three chapter series (the other two
being [Chapters 13](#part0025_split_000.html#page_301){.calibre5} and
[14](#part0026_split_000.html#page_321){.calibre5}) on storage
management. It elaborates on file systems and swap, and demonstrates
their creation and management in several exercises. It also highlights
the tools to monitor their usage.

**[File]{#part0027_split_001.html#id_405 .calibre10} Systems and File
System Types**

A *file system* is a logical container that stores files and
directories. Each file system is created in a discrete partition, VDO
volume, logical volume, or Stratis pool. A typical production RHEL
system usually has numerous file systems. During OS installation, only
two file systems---*/* and */boot*---are created in the default disk
layout, but you can design a custom disk layout and construct separate
containers to store dissimilar information. Typical additional file
systems created during an installation are */home*, */opt*, */tmp*,
*/usr*, and */var*. The two mandatory file systems---*/* and
*/boot*---are required for installation and booting.

Storing disparate data in distinct file systems versus storing all data
in a single file system offers the following advantages:

[![](images/00562.jpeg){.image2}]{.c1568a}Make any file system
accessible (mount) or inaccessible (unmount) to users independent of
other file systems. This hides or reveals information contained in that
file system.

[![](images/00562.jpeg){.image2}]{.c1568a}Perform file system repair
activities on individual file systems

[![](images/00562.jpeg){.image2}]{.c1568a}Keep dissimilar data in
separate file systems

[![](images/00562.jpeg){.image2}]{.c1568a}Optimize or tune each file
system independently

[![](images/00562.jpeg){.image2}]{.c1568a}Grow or shrink a file system
independent of other file systems

RHEL supports several types of file systems that may be categorized in
three basic groups: *disk-based*, *network-based*, and *memory-based*.
Disk-based file systems are typically created on physical drives using
SATA, USB, Fibre Channel, and other technologies. Network-based file
systems are essentially disk-based file systems shared over the network
for remote access. Memory-based file systems are virtual; they are
created at system startup and destroyed when the system goes down.
Disk-based and network-based file systems store information
persistently, while any data saved in virtual file systems does not
survive across system reboots.

[Table 15-1](#part0027_split_001.html#id_743){.calibre5} lists and
explains various common disk-and network-based file system types
supported in RHEL 8.

::: c49
  ---------------------- -------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **File System Type**   **Category**   **Description**
  Ext3                   Disk           The third generation of the extended file system. It supports metadata journaling for faster recovery, offers superior reliability, allows the creation of up to 32,000 subdirectories, and supports larger file systems and bigger files than its predecessor.
  Ext4                   Disk           The fourth generation of the extended file system developed as the successor to Ext3. It supports all features of Ext3 in addition to a larger file system size, bigger file size, an unlimited number of subdirectories, metadata and quota journaling, and extended user attributes.
  XFS                    Disk           XFS is a highly scalable and high-performing 64-bit file system. It supports metadata journaling for faster crash recovery, and online defragmentation, expansion, quota journaling, and extended user attributes. XFS is the default file system type in RHEL 8.
  VFAT                   Disk           This file system is used for post-Windows 95 file system formats on hard disks, USB drives, and floppy disks.
  ISO9660                Disk           This is used for optical file systems such as CD and DVD.
  NFS                    Network        Network File System. A shared directory or file system for remote access by other Linux systems.
  AutoFS                 Network        Auto File System. An NFS file system set to mount and unmount automatically on remote client systems.
  ---------------------- -------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0027_split_001.html#id_743} 15-1 File System Types**
:::

This chapter covers Ext3, Ext4, XFS, and VFAT file systems at length. It
also touches upon mounting and unmounting ISO9660. For a brief
discussion on memory-based file systems, see [Chapter
02](#part0014_split_000.html#page_35){.calibre5} "Initial Interaction
with the System". NFS and AutoFS are discussed in [Chapter
17](#part0029_split_000.html#page_399){.calibre5} "Network File System".

**[Extended]{#part0027_split_001.html#id_406 .calibre10} File Systems**

*Extended file systems* have been part of RHEL for many years. The first
generation is obsolete and is no longer supported. The second, third,
and fourth generations are currently available and supported. The fourth
generation is the latest in the series and is superior in features and
enhancements to its predecessors.

The structure of an extended file system is built on a partition or
logical volume at the time of file system creation. This structure is
divided into two sets. The first set holds the file system's metadata
and it is very tiny. The second set stores the actual data, and it
occupies almost the entire partition or the logical volume (VDO, LVM,
and Stratis) space.

The metadata includes the *superblock*, which keeps vital file system
structural information, such as the type, size, and status of the file
system, and the number of data blocks it contains. Since the superblock
holds such critical information, it is automatically replicated and
maintained at various known locations throughout the file system. The
superblock at the beginning of the file system is referred to as the
*primary superblock*, and all of its copies as *backup superblocks*. If
the primary superblock is corrupted or lost, it renders the file system
inaccessible. One of the backup superblocks is then used to supplant the
corrupted or lost primary superblock to bring the file system back to
its normal state.

The metadata also contains the *inode table*, which maintains a list of
*index node* (*inode*) numbers. Each file is assigned an inode number at
the time of its creation, and the inode number holds the file's
attributes such as its type, permissions, ownership, owning group, size,
and last access/modification time. The inode also holds and keeps track
of the pointers to the actual data blocks where the file contents are
located.

The Ext3 and Ext4 file systems support a journaling mechanism that
provides them with the ability to recover swiftly after a system crash.
Both Ext3 and Ext4 file systems keep track of recent changes in their
metadata in a *journal* (or log). Each metadata update is written in its
entirety to the journal after completion. The system peruses the journal
of each extended file system following the reboot after a crash to
determine if there are any errors, and it recovers the file system
rapidly using the latest metadata information stored in its journal. The
ext2 file system does not support journaling, but the support for
journaling may be added to it if required.

In contrast to Ext3 that supports file systems up to 16TiB and files up
to 2TiB, Ext4 supports very large file systems up to 1EiB (ExbiByte) and
files up to 16TiB (TebiByte). Additionally, Ext4 uses a series of
contiguous physical blocks on the hard disk called *extents*, resulting
in improved read and write performance with reduced fragmentation. Ext4
supports extended user attributes, acl mount options (to support file
permission allocation to specific users and groups), as well as metadata
and quota journaling.

**[XFS]{#part0027_split_001.html#id_407 .calibre10} File System**

The *X File System* (XFS) is a high-performing 64-bit extent-based
journaling file system type. XFS allows the creation of file systems and
files up to 8EiB (ExbiByte). It does not run file system checks at
system boot; rather, it relies on you to use the *xfs_repair* utility to
manually fix any issues. XFS sets the extended user attributes and acl
mount options by default on new file systems. It enables defragmentation
on mounted and active file systems to keep as much data in contiguous
blocks as possible for faster access. The only major caveat with using
XFS is its inability to shrink.

Like Ext3 and Ext4, XFS also uses journaling for metadata operations,
guaranteeing the consistency of the file system against abnormal or
forced unmounting. The journal information is read and any pending
metadata transactions are replayed when the XFS file system is
remounted.

XFS uses sophisticated techniques in its architecture for speedy
input/output performance. It can be snapshot in a mounted, active state.
The snapshot can then be used for backup or other purposes.

**[VFAT]{#part0027_split_001.html#id_408 .calibre10} File System**

VFAT (*Virtual File Allocation Table*) is an extension to the legacy
*FAT* file system type, also called *FAT16*, that was introduced in
early versions of MS-DOS. The support for FAT16 was later added to
Microsoft Windows, MacOS, and some UNIX versions, enabling them to read
and write files written in that format. FAT16 had limitations; it was
designed to use no more than 8.3 characters in filenames, limiting
filenames to a maximum of eight characters plus three characters as an
extension. Moreover, it only allowed filenames to begin with a letter or
number and to not contain spaces. FAT16 treated lowercase and uppercase
letters alike.

VFAT was introduced with Microsoft Windows 95 and it has since been
available. It supports 255 characters in filenames including spaces and
periods; however, it still does not differentiate between lowercase and
uppercase letters. VFAT support was added to Linux several years ago. A
VFAT file system may be created on hard drives, but it is primarily used
on removable media, such as floppy and USB flash drives, for exchanging
data between Linux and Windows.

**[ISO]{#part0027_split_001.html#id_409 .calibre10}9660 File System**

This file system type conforms to the ISO 9660 standard, hence the name.
It is used for removable optical disc media such as CD/DVD drives for
transporting software and patches, and operating system images in ISO
format between computers. The ISO9660 format originated from the
*High-Sierra File System* (HSFS) format, and it has now been enhanced to
include innovative features.

**[File]{#part0027_split_001.html#id_410 .calibre10} System Management**

Managing file systems involves such operations as creating, mounting,
labeling, viewing, growing, shrinking, unmounting, and removing them.
These management tasks are common to both Extended and XFS types. Most
of these functions are also applicable to VFAT and a few to optical file
systems.

In [Chapters 13](#part0025_split_000.html#page_301){.calibre5} and
[14](#part0026_split_000.html#page_321){.calibre5}, you created several
partitions, VDO volumes, LVM logical volumes, and Stratis volumes.
However, you did not initialize them with a file system type (except for
Stratis), and therefore you could not mount or use them. Later, you
destroyed all the partitions and the volumes that were created. You also
deleted the LVM volume group and the Stratis pool. All the disks were
returned to their unused state after the completion of the exercises.

Here is a listing of the block devices to confirm the current state of
the disks:

![](images/00752.jpeg){.image2}

The output verifies the unused state and availability status for all the
disks---*sdb* through *sdh*. You should be able to reuse them in the
exercises in this chapter.

**[File]{#part0027_split_001.html#id_411 .calibre10} System
Administration Commands**

In order to create and manage file systems, RHEL offers a number of
commands of which some are limited to their operations on the Extended,
XFS, or VFAT file system type, while others are general and applicable
to all file system types. [Table
15-2](#part0027_split_001.html#id_744){.calibre5} describes common file
system administration commands.

::: c49
  ---------------------------------- -------------------------------------------------------------------------------------------------------------------
  **Command**                        **Description**
  **Extended File System**           
  e2label                            Modifies the label of a file system
  mke2fs                             Creates a file system. Can also be invoked as mkfs.ext3, mkfs.ext4, mkfs -t ext3, and mkfs -t ext4.
  resize2fs                          Resizes a file system. This command is automatically invoked when the lvresize command is run with the -r switch.
  tune2fs                            Tunes or displays file system attributes
  **XFS**                            
  mkfs.xfs                           Creates a file system. Can also be invoked as mkfs -t xfs.
  xfs_admin                          Tunes file system attributes
  xfs_growfs                         Extends the size of a file system
  xfs_info                           Exhibits information about a file system
  **VFAT**                           
  mkfs.vfat                          Creates a file system. It is equivalent to using mkfs -t vfat.
  **General File System Commands**   
  blkid                              Displays block device attributes including their UUIDs and labels
  df                                 Reports file system utilization
  du                                 Calculates disk usage of directories and file systems
  lsblk                              Lists block devices and file systems and their attributes including their UUIDs and labels
  mount                              Mounts a file system for user access. Displays currently mounted file systems.
  umount                             Unmounts a file system
  ---------------------------------- -------------------------------------------------------------------------------------------------------------------

**[Table]{#part0027_split_001.html#id_744} 15-2 File System Management
Commands**
:::

Most of these commands are used in this chapter.

**[Mounting]{#part0027_split_001.html#id_412 .calibre10} and Unmounting
File Systems**

In order to enable users to access files and application programs in a
file system, the file system must be connected to the directory
structure at a desired attachment point, which is referred to as the
*mount point*. A mount point in essence is any empty directory that is
created and used for this purpose.

There are many file systems already mounted on your system, such as the
root file system mounted on */* and the boot file system mounted on
*/boot*. Both of them are empty directories and are reserved to connect
the two file systems to the directory hierarchy. You can use the *mount*
command to view information about mounted file systems. The following
shows the XFS file systems only:

![](images/00753.jpeg){.image2}

The "-t xfs" option makes the command to only show the file systems
initialized with the XFS type.

The *mount* command is also used for mounting a file system to a mount
point, and this action is performed with the *root* user privileges. The
command requires the absolute pathnames of the file system block device
and the mount point name. It also accepts the UUID or label of the file
system in lieu of the block device name. Options are available with this
command to mount all or a specific type of file system. The *mount*
command is also used to mount other types of file systems such as those
located in removable media. Upon successful mount, the kernel places an
entry for the file system in the **proc*self/mounts* file.

![](images/00002.jpeg){.image} A mount point should be empty when an
attempt is made to mount a file system on it, otherwise the content of
the mount point will hide. As well, the mount point must not be in use
or the mount attempt will fail.

The *mount* command supports numerous options that may be used as
required to override its default behavior. We can also specify multiple
comma-separated options. [Table
15-3](#part0027_split_001.html#id_745){.calibre5} describes some common
options.

::: c49
  --------------- ------------------------------------------------------------------------------------------------------------------------
  **Option**      **Description**
  acl (noacl)     Enables (disables) the support for ACLs
  auto (noauto)   Mounts (does not mount) the file system when the -a option is specified
  defaults        Mounts a file system with all the default values (async, auto, rw, etc.)
  \_netdev        Used for a file system that requires network connectivity in place before it can be mounted. VDO and NFS are examples.
  remount         Remounts an already mounted file system to enable or disable an option
  ro (rw)         Mounts a file system read-only (read/write)
  --------------- ------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0027_split_001.html#id_745} 15-3 Common mount Command
Options**
:::

The opposite of the *mount* command is *umount*, which is used to detach
a file system from the directory hierarchy and make it inaccessible to
users and applications. This command expects the absolute pathname to
the block device containing the file system or its mount point name in
order to detach it. Options are available with *umount* to unmount all
or a specific type of file system. The kernel removes the corresponding
file system entry from the **proc*self/mounts* file after it has been
successfully disconnected.

**[Determining]{#part0027_split_001.html#id_413 .calibre10} the UUID of
a File System**

Every Extended and XFS file system has a 128-bit (32 hexadecimal
characters) UUID (*Universally Unique IDentifier*) assigned to it at the
time of its creation. In contrast, UUIDs assigned to vfat file systems
are 32-bit (8 hexadecimal characters) in length. Assigning a UUID makes
the file system unique among many other file systems that potentially
exist on the system. The primary benefit of using a UUID is the fact
that it always stays persistent across system reboots. A UUID is used by
default in RHEL 8 in the **etc*fstab* file for any file system that is
created by the system in a standard partition.

![](images/00002.jpeg){.image} RHEL attempts to mount all file systems
listed in the **etc*fstab* file at reboots. Each file system has an
associated device file and UUID, but may or may not have a corresponding
label. The system checks for the presence of each file system's device
file, UUID, or label, and then attempts to mount it.

The */boot* file system, for instance, is located in a partition and the
device file associated with it is on *server2* is **dev*sda1*. You can
use the *xfs_admin* command, the *blkid* command, or the *lsblk* command
as follows to determine its UUID:

![](images/00754.jpeg){.image2}

The UUID reported by the above commands for the */boot* file system is
\"c1ff315e-4320-442c-a3c5-36db403b53f2\". If you *grep* for the string
"boot" on the **etc*fstab* file, you will see that the system uses this
UUID to mount */boot*. A discussion on the **etc*fstab* file is provided
later in this chapter.

![](images/00002.jpeg){.image} For extended file systems, you can use
the *tune2fs* command in addition to the *blkid* and *lsblk* commands to
determine the UUID.

[**EXAM TIP:**]{.c56} Knowing how to find the UUID of a file system
created in a standard partition or with Stratis is important.

A UUID is also assigned to a file system that is created in a VDO or LVM
volume; however, it need not be used in the *fstab* file, as the device
files associated with the logical volumes are always unique and
persistent.

**[Labeling]{#part0027_split_001.html#id_414 .calibre10} a File System**

A unique label may be used instead of a UUID to keep the file system
association with its device file exclusive and persistent across system
reboots. A label is limited to a maximum of 12 characters on the XFS
file system and 16 characters on the Extended file system. By default,
no labels are assigned to a file system at the time of its creation.

The */boot* file system is located in the **dev*sda1* partition and its
type is XFS. You can use the *xfs_admin* command, the *blkid* command,
or the *lsblk* command as follows to determine its label:

![](images/00755.jpeg){.image2}

The output discloses that there is currently no label assigned to the
*/boot* file system.

A label is not needed on a file system if you intend to use its UUID or
if it is created in a VDO or LVM logical volume; however, you can still
apply one using the *xfs_admin* command with the -L option. Labeling an
XFS file system requires that the target file system be unmounted.

The following example demonstrates the steps to unmount */boot*, set the
label "bootfs" on its device file, and remount it:

![](images/00756.jpeg){.image2}

You can confirm the new label by executing **sudo xfs_admin -l
*dev*sda1**, **sudo blkid *dev*sda1**, or **sudo lsblk -f *dev*sda1**.

![](images/00002.jpeg){.image} For extended file systems, you can use
the *e2label* command to apply a label and the *tune2fs*, *blkid*, and
*lsblk* commands to view and verify.

Now you can replace the UUID=\"c1ff315e-4320-442c-a3c5-36db403b53f2\"
for */boot* in the *fstab* file with LABEL=bootfs, and unmount and
remount */boot* as demonstrated above for confirmation.

A label may also be applied to a file system created in a VDO or LVM
volume; however, it is not recommended for use in the *fstab* file, as
the device files for these logical volumes are always unique and remain
persistent across system reboots.

**[Automatically]{#part0027_split_001.html#id_415 .calibre10} Mounting a
File System at Reboots**

File systems defined in the **etc*fstab* file are mounted automatically
at reboots. This file must contain proper and complete information for
each listed file system. An incomplete or inaccurate entry might leave
the system in an undesirable or unbootable state. Another benefit of
adding entries to this file is that you only need to specify one of the
four attributes---block device name, UUID, label, or mount point---of
the file system that you wish to mount manually with the *mount*
command. The *mount* command obtains the rest of the information from
this file. Similarly, you only need to specify one of these attributes
with the *umount* command to detach it from the directory hierarchy.

The default *fstab* file contains entries for file systems that are
created at the time of installation. On *server2*, for instance, this
file currently has the following three entries:

![](images/00757.jpeg){.image2}

[**EXAM TIP:**]{.c56} Any missing or invalid entry in this file may
render the system unbootable. You will have to boot the system in
emergency mode to fix this file. Ensure that you understand each field
in the file for both file system and swap entries.

The format of this file is such that each row is broken out into six
columns to identify the required attributes for each file system to be
successfully mounted. Here is what the columns contain:

**Column 1:** Defines the physical or virtual device path where the file
system is resident, or its associated UUID or label. There can be
entries for network file systems here as well.

**Column 2:** Identifies the mount point for the file system. For swap
partitions, use either "none" or "swap".

**Column 3:** Specifies the type of file system such as Ext3, Ext4, XFS,
VFAT, or ISO9660. For swap, the type "swap" is used. You may use "auto"
instead to leave it up to the *mount* command to determine the type of
the file system.

**Column 4:** Identifies one or more comma-separated options to be used
when mounting the file system. See [Table
15-3](#part0027_split_001.html#id_745){.calibre5} for a description of
some of the options, consult the manual pages of the *mount* command or
the *fstab* file for additional options and details.

**Column 5:** Is used by the *dump* utility to ascertain the file
systems that need to be dumped. A value of 0 (or the absence of this
column) disables this check. This field is applicable only on Extended
file systems; XFS does not use it.

**Column 6:** Expresses the sequence number in which to run the *e2fsck*
(file system check and repair utility for Extended file system types)
utility on the file system at system boot. By default, 0 is used for
memory-based, remote, and removable file systems, 1 for */*, and 2 for
*/boot* and other physical file systems. 0 can also be used for */*,
*/boot*, and other physical file systems you don't want to be checked or
repaired. This field is applicable only on Extended file systems; XFS
does not use it.

![](images/00002.jpeg){.image} A 0 in columns 5 and 6 for XFS, virtual,
remote, and removable file system types has no meaning. You do not need
to add them for these file system types.

This file is edited manually, so care must be observed to circumvent
syntax and typing errors.

**[Monitoring]{#part0027_split_001.html#id_416 .calibre10} File System
Usage**

On a live system, you'll often need to check file system usage to know
if a mounted file system requires an expansion for growth or a clean up
to generate free space. This involves examining the used and available
spaces for a file system. The *df* (*disk free*) command has been used
for this purpose. It reports usage details for mounted file systems. By
default, this command reports the numbers in KBs unless the -m or -h
option is specified to view the sizes in MBs or human-readable format.

![](images/00002.jpeg){.image} This command may not produce correct
information for VDO and Stratis file systems. Use their own tools for
viewing usage.

Let's run this command with the -h option on *server2*:

![](images/00758.jpeg){.image2}

The output shows the file system device file or type in column 1,
followed by the total, used, and available spaces in columns 2, 3, and
4, and then the usage percentage and mount point in columns 5 and 6.

There are a few other useful flags available with the *df* command that
can produce the desired output. These flags include:

-T to add the file system type to the output (example: **df -hT**)

-x to exclude the specified file system type from the output (example:
**df -hx tmpfs**)

-t to limit the output to a specific file system type (example: **df -t
xfs**)

-i to show inode information (example: **df -hi**)

You may use -h with any of these examples to print information in
human-readable format.

**[Calculating]{#part0027_split_001.html#id_417 .calibre10} Disk Usage**

In contrast to the *df* command that returns usage information for an
entire file system, the *du* command reports the amount of space a file
or directory occupies. By default, it shows the output in KBs; however,
you can use the -m or -h option to view the output in MBs or
human-readable format. In addition, you can view a usage summary with
the -s switch and a grand total with -c.

Let's run this command on the **usr*bin* directory to view the usage
summary:

![](images/00759.jpeg){.image2}

To add a "total" row to the output and with numbers displayed in KBs:

![](images/00760.jpeg){.image2}

Try this command with different options on the **usr*sbin/lvm* file and
observe the results.

**Exercise 15-1: Create and Mount Ext4, VFAT, and XFS File Systems in
Partitions**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create 2 x 100MB partitions on the **dev*sdb*
disk, initialize them separately with the Ext4 and VFAT file system
types, define them for persistence using their UUIDs, create mount
points called */ext4fs1* and */vfatfs1*, attach them to the directory
structure, and verify their availability and usage. Moreover, you will
use the disk **dev*sdc* and repeat the above procedure to establish an
XFS file system in it and mount it on */xfsfs1*.

1[.]{.c19}Apply the label "msdos" to the *sdb* disk using the *parted*
command:

![](images/00761.jpeg){.image2}

2[.]{.c19}Create 2 x 100MB primary partitions on *sdb* with the *parted*
command:

![](images/00762.jpeg){.image2}

3[.]{.c19}Initialize the first partition (*sdb1*) with Ext4 file system
type using the *mkfs* command:

![](images/00763.jpeg){.image2}

4[.]{.c19}Initialize the second partition (*sdb2*) with VFAT file system
type using the *mkfs* command:

![](images/00764.jpeg){.image2}

5[.]{.c19}Initialize the whole disk (*sdc*) with the XFS file system
type using the *mkfs.xfs* command. Add the -f flag to force the removal
of any old partitioning or labeling information from the disk.

![](images/00765.jpeg){.image2}

6[.]{.c19}Determine the UUIDs for all three file systems using the
*lsblk* command:

![](images/00766.jpeg){.image2}

7[.]{.c19}Open the **etc*fstab* file, go to the end of the file, and
append entries for the file systems for persistence using their UUIDs:

![](images/00767.jpeg){.image2}

8[.]{.c19}Create mount points */ext4fs1*, */vfatfs1*, and */xfsfs1* for
the three file systems using the *mkdir* command:

![](images/00768.jpeg){.image2}

9[.]{.c19}Mount the new file systems using the *mount* command. This
command will fail if there are any invalid or missing information in the
file.

![](images/00769.jpeg){.image2}

10[.]{.c23}View the mount and availability status as well as the types
of all three file systems using the *df* command:

![](images/00770.jpeg){.image2}

The output verifies the creation and availability status of the three
file systems. They are added to the *fstab* file for persistence. A
system reboot at this point will remount them automatically. These file
systems may now be used to store files.

**[Exercise]{#part0027_split_001.html#id_418 .calibre10} 15-2: Create
and Mount XFS File System in VDO Volume**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create a VDO volume called *vdo1* of logical
size 16GB on the *sdf* disk (the actual size of this disks is 4GB). You
will initialize the volume with the XFS file system type, define it for
persistence using its device files, create a mount point called
*/xfsvdo1*, attach it to the directory structure, and verify its
availability and usage.

Prior to proceeding, ensure that the steps outlined in [Exercise
13-6](#part0025_split_001.html#id_370){.calibre5} for VDO software
installation and service startup have been accomplished.

1[.]{.c19}Create a VDO volume *vdo1* on the *sdf* disk with a logical
size of 16GB and a slab size of 128MB:

![](images/00771.jpeg){.image2}

2[.]{.c19}List the new VDO volume using the *vdo* and *lsblk* commands:

![](images/00772.jpeg){.image2}

The output shows the logical volume size (16GB), type (vdo), and the
actual size (4GB) of the underlying disk.

3[.]{.c19}Initialize the VDO volume with the XFS file system type with
the *mkfs.xfs* command. The VDO volume device file is **dev*mapper/vdo1*
as indicated in the output in step 1. Add the -f flag to force the
removal of any old partitioning or labeling information from the disk.

![](images/00773.jpeg){.image2}

4[.]{.c19}Open the **etc*fstab* file, go to the end of the file, and
append the following entry for the file system for persistence using its
device file:

![](images/00774.jpeg){.image2}

Make sure to include the option **x-systemd.requires=vdo.service** (or
try \_netdev instead) with the file system entry in the *fstab* file or
your system will land into the emergency target on the next reboot. This
option holds the *mount* command from mounting this file system until
the *vdo.service* service has been operational.

5[.]{.c19}Create the mount point */xfsvdo1* using the *mkdir* command:

![](images/00775.jpeg){.image2}

6[.]{.c19}Mount the new file system using the *mount* command. This
command will fail if there are any invalid or missing information in the
file.

![](images/00776.jpeg){.image2}

The *mount* command with the -a flag is a validation test for the
*fstab* file. It should always be executed after updating this file and
before rebooting the server to avoid landing the system in an unbootable
state.

7[.]{.c19}View the mount and availability status as well as the types of
the VDO file system using the *lsblk* and *df* commands:

![](images/00777.jpeg){.image2}

The *lsblk* command output illustrates the VDO volume name (*vdo1*) ,
the disk it is located on (*sdf*), the actual (4GB) and logical (16GB)
sizes, and the mount point (*/xfsvdo1*) where the file system is
connected to the directory structure.

The *df* command shows the logical size of the file system and its usage
status, but it does not reveal the underlying disk information. This
file system is added to the *fstab* file for persistence, meaning a
future system reboot will remount it automatically. This file system may
now be used to store files.

Refer to [Chapter 13](#part0025_split_000.html#page_301){.calibre5}
"Basic Storage Partitioning" for details on VDO.

**[Exercise]{#part0027_split_001.html#id_419 .calibre10} 15-3: Create
and Mount Ext4 and XFS File Systems in LVM Logical Volumes**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create a volume group called *vgfs* comprised
of a 160MB physical volume created in a partition on the **dev*sdd*
disk. The PE size for the volume group should be set at 16MB. You will
create two logical volumes called *ext4vol* and *xfsvol* of sizes 80MB
each and initialize them with the Ext4 and XFS file system types. You
will ensure that both file systems are persistently defined using their
logical volume device filenames. You will create mount points called
*/ext4fs2* and */xfsfs2*, mount the file systems, and verify their
availability and usage.

1[.]{.c19}Create a 150MB partition on the *sdd* disk using the *parted*
command:

![](images/00778.jpeg){.image2}

2[.]{.c19}Initialize the *sdd1* partition for use in LVM using the
*pvcreate* command:

![](images/00779.jpeg){.image2}

3[.]{.c19}Create the volume group *vgfs* with a PE size of 16MB using
the physical volume *sdd1*:

![](images/00780.jpeg){.image2}

The PE size is not easy to alter after a volume group creation, so
ensure it is defined as required at creation.

4[.]{.c19}Create two logical volumes *ext4vol* and *xfsvol* of size 80MB
each in *vgfs* using the *lvcreate* command:

![](images/00781.jpeg){.image2}

5[.]{.c19}Format the *ext4vol* logical volume with the Ext4 file system
type using the *mkfs.ext4* command:

![](images/00782.jpeg){.image2}

You may alternatively use **sudo mkfs -t ext4 *dev*vgfs/ext4vol**.

6[.]{.c19}Format the *xfsvol* logical volume with the XFS file system
type using the *mkfs.xfs* command:

![](images/00783.jpeg){.image2}

You may use **sudo mkfs -t xfs *dev*vgfs/xfsvol** instead.

7[.]{.c19}Open the **etc*fstab* file, go to the end of the file, and
append entries for the file systems for persistence using their device
files:

![](images/00784.jpeg){.image2}

8[.]{.c19}Create mount points */ext4fs2* and */xfsfs2* using the *mkdir*
command:

![](images/00785.jpeg){.image2}

9[.]{.c19}Mount the new file systems using the *mount* command. This
command will fail if there is any invalid or missing information in the
file.

![](images/00786.jpeg){.image2}

Fix any issues in the file if reported.

10[.]{.c23}View the mount and availability status as well as the types
of the new LVM file systems using the *lsblk* and *df* commands:

![](images/00787.jpeg){.image2}

The *lsblk* command output illustrates the LVM logical volumes
(*ext4vol* and *xfsvol*), the disk they are located on (*sdd*), the
sizes (80MB), and the mount points (*/ext4fs2* and */xfsfs2*) where the
file system are connected to the directory structure.

The *df* command shows the size and usage information. Both file systems
are added to the *fstab* file for persistence, meaning future system
reboots will remount them automatically. They may now be used to store
files.

**[Exercise]{#part0027_split_001.html#id_420 .calibre10} 15-4: Resize
Ext4 and XFS File Systems in LVM Logical Volumes**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will grow the size of the *vgfs* volume group that
was created in [Exercise
15-3](#part0027_split_001.html#id_419){.calibre5} by adding the whole
*sde* disk to it. You will extend the *ext4vol* logical volume along
with the file system it contains by 40MB using two separate commands.
You will extend the *xfsvol* logical volume along with the file system
it contains by 40MB using a single command. You will verify the new
extensions.

1[.]{.c19}Initialize the *sde* disk and add it to the *vgfs* volume
group:

![](images/00788.jpeg){.image2}

2[.]{.c19}Confirm the new size of *vgfs* using the *vgs* and *vgdisplay*
commands:

![](images/00789.jpeg){.image2}

There are now two physical volumes in the volume group and the total
size increased to 400MiB.

3[.]{.c19}Grow the logical volume *ext4vol* and the file system it holds
by 40MB using the *lvextend* and *fsadm* command pair. Make sure to use
an uppercase L to specify the size. The default unit is MiB. The plus
sign (+) signifies an addition to the current size.

![](images/00790.jpeg){.image2}

The *resize* subcommand instructs the *fsadm* command to grow the file
system to the full length of the specified logical volume.

4[.]{.c19}Grow the logical volume *xfsvol* and the file system (-r) it
holds by (+) 40MB using the *lvresize* command:

![](images/00791.jpeg){.image2}

5[.]{.c19}Verify the new extensions to both logical volumes using the
*lvs* command. You may also issue the *lvdisplay* or *vgdisplay* command
instead.

![](images/00792.jpeg){.image2}

6[.]{.c19}Check the new sizes and the current mount status for both file
systems using the *df* and *lsblk* commands:

![](images/00793.jpeg){.image2}

The outputs reflect the new sizes (128MB) for both file systems. They
also indicate their mount status.

This concludes the exercise.

**Exercise 15-5: Create, Mount, and Expand XFS File System in Stratis
Volume**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create a Stratis pool called *strpool* and a
file system (*strfs2*) in it (the file system type will be XFS) by
reusing the 1GB *sdg* disk from [Chapter
14](#part0026_split_000.html#page_321){.calibre5}. You will display
information about the pool, file system, and device used. You will
expand the pool to include another 1GB disk *sdh* and confirm.

For further details on Stratis storage management solution, refer to
[Chapter 14](#part0026_split_000.html#page_321){.calibre5} "Advanced
Storage Partitioning". Prior to proceeding, ensure that the steps
outlined in [Exercise 14-7](#part0026_split_001.html#id_391){.calibre5}
for Stratis software installation and service startup have been
accomplished.

1[.]{.c19}Create a pool called *strpool* using the *sdg* disk and verify
the creation:

![](images/00794.jpeg){.image2}

The pool is created with a single disk included, and confirmed.

2[.]{.c19}Show the block device used in the pool:

![](images/00795.jpeg){.image2}

3[.]{.c19}Create a file system called *strfs2* in the pool and verify
the creation:

![](images/00796.jpeg){.image2}

4[.]{.c19}Determine the UUID of the new file system to be added to the
*fstab* file:

![](images/00797.jpeg){.image2}

5[.]{.c19}Open the **etc*fstab* file, go to the end of the file, and
append the following entry for the file system for persistence using the
UUID:

![](images/00798.jpeg){.image2}

Make sure to include the option **x-systemd.requires=stratisd.service**
(or try \_netdev instead) with the file system entry in the *fstab* file
or your system will land into the emergency target on the next reboot.
This option holds the *mount* command from mounting this file system
until the *stratisd.service* service has been started successfully.

6[.]{.c19}Create the mount point */strfs2*:

![](images/00799.jpeg){.image2}

7[.]{.c19}Mount the new file system using the *mount* command as
follows. This command will fail if there are any invalid or missing
information in the file.

![](images/00800.jpeg){.image2}

8[.]{.c19}Check the pool usage:

![](images/00801.jpeg){.image2}

9[.]{.c19}Check the file system usage:

![](images/00802.jpeg){.image2}

10[.]{.c23}Grow the pool by adding the *sdh* disk to it and confirm the
growth:

![](images/00803.jpeg){.image2}

The file system *strfs2* will automatically expand to take advantage of
the additional pool capacity when required.

This concludes the exercise.

**[Swap]{#part0027_split_001.html#id_421 .calibre10} and its
Management**

Physical memory (or main memory) in the system is a finite temporary
storage resource employed for loading kernel and running user programs
and applications. *Swap space* is an independent region on the physical
disk used for holding idle data until it is needed. The system splits
the physical memory into small logical chunks called *pages* and maps
their physical locations to virtual locations on the swap to facilitate
access by system processors. This physical-to-virtual mapping of pages
is stored in a data structure called *page table*, and it is maintained
by the kernel.

When a program or process is spawned, it requires space in the physical
memory to run and be processed. Although many programs can run
concurrently, the physical memory cannot hold all of them at once. The
kernel monitors the memory usage. As long as the free memory remains
below a high threshold, nothing happens. However, when the free memory
falls below that threshold, the system starts moving selected idle pages
of data from physical memory to the swap space in an effort to make room
to accommodate other programs. This piece in the process is referred to
as *page out*. Since the system CPU performs the process execution in a
round-robin fashion, when the system needs this paged-out data for
execution, the CPU looks for that data in the physical memory and a
*page fault* occurs, resulting in moving the pages back to the physical
memory from the swap. This return of data to the physical memory is
referred to as *page in*. The entire process of paging data out and in
is known as *demand paging*.

RHEL systems with less physical memory but high memory requirements can
become over busy with paging out and in. When this happens, they do not
have enough cycles to carry out other useful tasks, resulting in
degraded system performance. The excessive amount of paging that affects
the system performance is called *thrashing*.

When thrashing begins, or when the free physical memory falls below a
low threshold, the system deactivates idle processes and prevents new
processes from being launched. The idle processes are only reactivated
and new processes are only allowed to be started when the system
discovers that the available physical memory has climbed above the
threshold level and thrashing has ceased.

**[Determining]{#part0027_split_001.html#id_422 .calibre10} Current Swap
Usage**

The size of a swap area should not be less than the amount of physical
memory; however, depending on workload requirements, it may be twice the
size or larger. It is also not uncommon to see systems with less swap
than the actual amount of physical memory. This is especially witnessed
on systems with a huge physical memory size.

RHEL offers the *free* command to view memory and swap space
utilization. Use this command to view how much physical memory is
installed (total), used (used), available (free), used by shared library
routines (shared), holding data before it is written to disk (buffers),
and used to store frequently accessed data (cached) on the system. The
-h flag may be specified with the command to list the values in
human-readable format, otherwise -k for KB, -m for MB, -g for GB, and so
on are also supported. Add -t with the command to display a line with
the "total" at the bottom of the output. Here is a sample output from
*server2*:

![](images/00804.jpeg){.image2}

The output indicates that the system has 1.8GiB of total memory of which
895MiB is in use and 447MiB is free. It also shows on the same line the
current memory usages by temporary (tmpfs) file systems (20MiB) and
kernel buffers and page cache (486MiB). It also illustrates an estimate
of free memory available to start new processes (749MiB).

On the subsequent row, it reports the total swap space (1.0GiB)
configured on the system with a look at used (0 Bytes) and free (1.0GiB)
space. The last line prints the combined usage summary of the main
memory and swap.

Try **free -hts 3** and **free -htc 2** to refresh the output every
three seconds (-s) and to display the output twice (-c).

The *free* command reads memory and swap information from the
**proc*meminfo* file to produce the report. The values are shown in KBs
by default, and they are slightly off from what is shown in the above
screenshot with *free*. Here are the relevant fields from this file:

![](images/00805.jpeg){.image2}

This data depicts the system's runtime memory and swap usage, as it is
located in a virtual file.

**[Prioritizing]{#part0027_split_001.html#id_423 .calibre10} Swap
Spaces**

On many production RHEL servers, you may find multiple swap areas
configured and activated to meet the workload demand. The default
behavior of RHEL is to use the first activated swap area and move on to
the next when the first one is exhausted. The system allows us to
prioritize one area over the other by adding the option "pri" to the
swap entries in the *fstab* file. This flag supports a value between -2
and 32767 with -2 being the default. A higher value of "pri" sets a
higher priority for the corresponding swap region. For swap areas with
an identical priority, the system alternates between them.

**[Swap]{#part0027_split_001.html#id_424 .calibre10} Administration
Commands**

In order to create and manage swap spaces on the system, the *mkswap*,
*swapon*, and *swapoff* commands are available. Use *mkswap* to
initialize a partition for use as a swap space. Once the swap area is
ready, you can activate or deactivate it from the command line with the
help of the other two commands, or set it up for automatic activation by
placing an entry in the *fstab* file. The *fstab* file accepts the swap
area's device file, UUID, or label.

**[Exercise]{#part0027_split_001.html#id_425 .calibre10} 15-6: Create
and Activate Swap in Partition and Logical Volume**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create one swap area in a new 40MB partition
called *sdb3* using the *mkswap* command. You will create another swap
area in a 140MB logical volume called *swapvol* in *vgfs*. You will add
their entries to the **etc*fstab* file for persistence. You will use the
UUID and priority 1 for the partition swap and the device file and
priority 2 for the logical volume swap. You will activate them and use
appropriate tools to validate the activation.

[**EXAM TIP:**]{.c56} Use the lsblk command to determine available disk
space.

1[.]{.c19}Use the *parted*'s *print* subcommand on the *sdb* disk and
the *vgs* command on the *vgfs* volume group to determine available
space for a new 40MB partition and a 144MB logical volume:

![](images/00806.jpeg){.image2}

The outputs show 49MB (250MB minus 201MB) free space on the *sdb* disk
and 144MB free space in the volume group.

2[.]{.c19}Create partition called *sdb3* of size 40MB using the *parted*
command:

![](images/00807.jpeg){.image2}

3[.]{.c19}Create logical volume *swapvol* of size 144MB in *vgs* using
the *lvcreate* command:

![](images/00808.jpeg){.image2}

4[.]{.c19}Construct swap structures in *sdb3* and *swapvol* using the
*mkswap* command:

![](images/00809.jpeg){.image2}

5[.]{.c19}Edit the *fstab* file and add entries for both swap areas for
auto-activation on reboots. Obtain the UUID for partition swap with
**lsblk -f *dev*sdb3** and use the device file for logical volume.
Specify their priorities.

![](images/00810.jpeg){.image2}

[**EXAM TIP:**]{.c56} You will not be given any credit for this work if
you forget to add entries to the fstab file.

6[.]{.c19}Determine the current amount of swap space on the system using
the *swapon* command:

![](images/00811.jpeg){.image2}

There is one 1GB swap area on the system configured at the default
priority of -2.

7[.]{.c19}Activate the new swap regions using the *swapon* command:

![](images/00812.jpeg){.image2}

The command would display errors if there were any issues with swap
entries in the *fstab* file.

8[.]{.c19}Confirm the activation using the *swapon* command or by
viewing the **proc*swaps* file:

![](images/00813.jpeg){.image2}

The two new swap regions are activated and listed in the above outputs.
Their sizes and priorities are also visible. The device mapper device
files for the logical volumes and the device file for the partition swap
are also exhibited.

9[.]{.c19}Issue the *free* command to view the reflection of swap
numbers on the Swap and Total lines:

![](images/00814.jpeg){.image2}

The total swap is now 1.2GiB. This concludes the exercise.

**[Chapter]{#part0027_split_001.html#id_426 .calibre10} Summary**

This chapter covered two major storage topics: file systems and swap.
These structures are created in partitions or logical volumes
irrespective of the underlying storage management solution used to build
them.

The chapter began with a detailed look at the concepts, categories,
benefits, and types of file systems. We reviewed file system
administration and monitoring utilities. We discussed the concepts
around mounting and unmounting file systems. We examined the UUID
associated with file systems and applied labels to file systems. We
analyzed the file system table and added entries for auto-activating
file systems at reboots. We explored tools for reporting file system
usage and calculating disk usage. We performed a number of exercises on
file system creation and administration in partitions and VDO, LVM, and
Stratis volumes to reinforce the concepts and theory learned in this and
the last two chapters.

We touched upon the concepts of swapping and paging, and studied how
they work. We performed exercises on creating, activating, viewing,
deactivating, and removing swap spaces, as well as configuring them for
auto-activation at system reboots.

**[Review]{#part0027_split_001.html#id_427 .calibre10} Questions**

1[.]{.c19}Which two file systems are created in a default RHEL 8
installation?

2[.]{.c19}What would the command *lvresize -r -L +30 *dev*vg02/lvol2*
do?

3[.]{.c19}XFS is the default file system type in RHEL 8. True or False?

4[.]{.c19}What type of information does the *blkid* command display?

5[.]{.c19}What would the command *xfs_admin -L bootfs *dev*sda1* do?

6[.]{.c19}The *lsblk* command cannot be used to view file system UUIDs.
True or False?

7[.]{.c19}What is the process of paging out and paging in known as?

8[.]{.c19}What would the command *mkswap *dev*sdc2* do?

9[.]{.c19}What would happen if you mount a file system on a directory
that already contains files in it?

10[.]{.c23}A UUID is always assigned to a file system at its creation
time. True or False?

11[.]{.c23}Arrange the activities to create and activate a swap space
while ensuring persistence: (a) swapon, (b) update fstab, (c) mkswap,
and (d) reboot?

12[.]{.c23}The difference between the primary and backup superblocks is
that the primary superblock includes pointers to the data blocks where
the actual file contents are stored whereas the backup superblocks
don't. True or False?

13[.]{.c23}What would the command *mkfs.ext4 *dev*vgtest/lvoltest* do?

14[.]{.c23}Arrange the tasks in correct sequence: umount file system,
mount file system, create file system, remove file system.

15[.]{.c23}Which of these statements is wrong with respect to file
systems: (a) optimize each file system independently, (b) keep
dissimilar data in separate file systems, (c) grow and shrink a file
system independent of other file systems, and (d) file systems cannot be
expanded independent of other file systems.

16[.]{.c23}Which command can be used to create a label for an XFS file
system?

17[.]{.c23}What would the *mount* command do with the -a switch?

18[.]{.c23}What would the command *df -t xfs* do?

19[.]{.c23}What is the difference between the *mkfs.ext4* and *mke2fs*
commands?

20[.]{.c23}Which command can be used to determine the total and used
physical memory and swap in the system?

21[.]{.c23}Which virtual file contains information about the current
swap?

22[.]{.c23}The **etc*fstab* file can be used to activate swap spaces
automatically at system reboots. True or False?

23[.]{.c23}What is the default file system type used for optical media?

24[.]{.c23}The *xfs_repair* command must be run on a mounted file
system. True or False?

25[.]{.c23}Provide two commands that can be used to activate and
deactivate swap spaces manually.

26[.]{.c23}Provide the *fstab* file entry for an Ext4 file system
located in device **dev*mapper/vg20-lv1* and mounted with default
options on the */ora1* directory.

27[.]{.c23}What is the name of the virtual file that holds currently
mounted file system information?

28[.]{.c23}Which option must be specified with persistent VDO file
system mounting to avoid landing the system in an unbootable state?

29[.]{.c23}Both Ext3 and Ext4 file system types support journaling. True
or False?

30[.]{.c23}Name three commands that can be employed to view the UUID of
an XFS file system?

**[Answers]{#part0027_split_001.html#id_428 .calibre10} to Review
Questions**

1[.]{.c19}*/* and */boot*.

2[.]{.c19}The command provided will expand the logical volume *lvol2* in
volume group *vg02* along with the file system it contains by 30MB.

3[.]{.c19}True.

4[.]{.c19}The *blkid* command displays attributes for block devices.

5[.]{.c19}The command provided will apply the specified label to the XFS
file system in **dev*sda1*.

6[.]{.c19}False.

7[.]{.c19}The process of paging out and in is known as demand paging.

8[.]{.c19}The command provided will create swap structures in the
**dev*vdc2* partition.

9[.]{.c19}The files in the directory will hide.

10[.]{.c23}True.

11[.]{.c23}c/a/b or c/b/a.

12[.]{.c23}False.

13[.]{.c23}The command provided will format **dev*vgtest/lvoltest*
logical volume with Ext4 file system type.

14[.]{.c23}Create, mount, unmount, and remove.

15[.]{.c23}d is incorrect.

16[.]{.c23}The *xfs_admin* command can be used to create a label for an
XFS file system.

17[.]{.c23}The command provided will mount all file systems listed in
the **etc*fstab* file but are not currently mounted.

18[.]{.c23}The command provided will display all mounted file systems of
type XFS.

19[.]{.c23}No difference.

20[.]{.c23}The *free* command.

21[.]{.c23}The **proc*swaps* file contains information about the current
swap.

22[.]{.c23}True.

23[.]{.c23}The default file system type for optical devices is ISO9660.

24[.]{.c23}False.

25[.]{.c23}The *swapon* and *swapoff* commands.

26[.]{.c23}*dev*mapper/vg20-lv1 /ora1 swap defaults 0 0

27[.]{.c23}The *mounts* file under **proc*self* directory.

28[.]{.c23}The \_netdev option.

29[.]{.c23}True.

30[.]{.c23}You can use the *xfs_admin*, *lsblk*, and *blkid* commands to
view the UUID of an XFS file system.

**[Do-]{#part0027_split_001.html#id_429 .calibre10}It-Yourself Challenge
Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

To use the same storage that was used in the labs for [Chapters
13](#part0025_split_000.html#page_301){.calibre5} and
[14](#part0026_split_000.html#page_321){.calibre5}, destroy all traces
of the partitions, volume groups, and pools that were created before
proceeding. Alternatively, you can add more storage to *server2* for the
following labs.

**[Lab]{#part0027_split_001.html#id_430 .calibre10} 15-1: Create VFAT,
Ext4, and XFS File Systems in Partitions & Mount Persistently**

As *user1* with *sudo* on *server2*, create three 70MB primary
partitions on one of the available 250MB disks (*lsblk*) by invoking the
*parted* utility directly at the command prompt. Apply label "msdos" if
the disk is new. Initialize partition 1 with VFAT, partition 2 with
Ext4, and partition 3 with XFS file system types. Create mount points
*/vfatfs5*, */ext4fs5*, and */xfsfs5*, and mount all three manually.
Determine the UUIDs for the three file systems, and add them to the
*fstab* file. Unmount all three file systems manually, and execute
**mount -a** to mount them all. Run **df -h** for verification. (Hint:
File System Management).

**Lab 15-2: Create XFS File System in VDO Volume and Mount
Persistently**

As *user1* with *sudo* on *server2*, ensure that VDO software is
installed and the VDO service is enabled and started. Create a volume
*vdo5* with a logical size 16GB on an available 4GB disk (*lsblk*) using
the *vdo* command. Select an appropriate slab size for the volume.
Verify the volume creation with the *vdo*, *lsblk*, and *vdostats*
commands. Initialize the volume with XFS file system type. Create mount
point */vdofs5*, and mount it manually. Add the file system information
to the *fstab* file, and use "\_netdev" as a mount option. Unmount the
file system manually, and execute **mount -a** to mount it back. Run
**df -h** to confirm. (Hint: File System Management).

**[Lab]{#part0027_split_001.html#id_431 .calibre10} 15-3: Create Ext4
and XFS File Systems in LVM Volumes and Mount Persistently**

As *user1* with *sudo* on *server2*, initialize an available 250MB disk
for use in LVM (*lsblk*). Create volume group *vg200* with PE size 8MB
and add the physical volume. Create two logical volumes *lv200* and
*lv300* of sizes 120MB and 100MB. Use the *vgs*, *pvs*, *lvs*, and
*vgdisplay* commands for verification. Initialize the volumes with Ext4
and XFS file system types. Create mount points */lvmfs5* and */lvmfs6*,
and mount them manually. Add the file system information to the *fstab*
file using their device files. Unmount the file systems manually, and
execute **mount -a** to mount them back. Run **df -h** to confirm.
(Hint: File System Management).

**[Lab]{#part0027_split_001.html#id_432 .calibre10} 15-4: Extend Ext4
and XFS File Systems in LVM Volumes**

As *user1* with *sudo* on *server2*, initialize an available 250MB disk
for use in LVM (*lsblk*). Add the new physical volume to volume group
*vg200*. Expand logical volumes *lv200* and *lv300* along with the
underlying file systems to 200MB and 250MB. Use the *vgs*, *pvs*, *lvs*,
*vgdisplay*, and *df* commands for verification. (Hint: File System
Management).

**[Lab]{#part0027_split_001.html#id_433 .calibre10} 15-5: Create XFS
File System in Stratis Volume and Mount Persistently**

As *user1* with *sudo* on *server2*, confirm Stratis software is
installed and the Stratis service is enabled and started. Create pool
*strpool5* on an available 1GB disk and confirm. Create file system
*strfs5* in the pool and verify. Create mount point */strfs5*. Determine
the UUID of the Stratis file system and add it to the *fstab* file for
persistence. Use the x-systemd.requires=stratisd.service as a mount
option. Reboot the system and confirm mounting with **df -h**. (Hint:
File System Management).

**[Lab]{#part0027_split_001.html#id_434 .calibre10} 15-6: Create Swap in
Partition and LVM Volume and Activate Persistently**

As *user1* with *sudo* on *server2*, create two 100MB partitions on an
available 250MB disk (*lsblk*) by invoking the *parted* utility directly
at the command prompt. Apply label "msdos" if the disk is new.
Initialize one of the partitions with swap structures. Apply label
*swappart* to the swap partition, and add it to the *fstab* file.
Execute **swapon -a** to activate it. Run **swapon -s** to confirm
activation.

Initialize the other partition for use in LVM. Expand volume group
*vg200* (Lab 15-4) by adding this physical volume. Create logical volume
*swapvol* of size 180MB. Use the *vgs*, *pvs*, *lvs*, and *vgdisplay*
commands for verification. Initialize the logical volume for swap. Add
an entry to the *fstab* file for the new swap area using its device
file. Execute **swapon -a** to activate it. Run **swapon -s** to confirm
activation. (Hint: Swap and its Management).

[]{#part0028_split_000.html}
