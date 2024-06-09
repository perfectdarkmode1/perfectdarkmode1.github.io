## Chapter 13 {style="text-align: right"}

\

### Storage Management {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Master Boot Record vs. GUID Partition Table

\

Identify and understand disk partitions

\

The concept of thin provisioning, and its benefits

\

Create and delete partition on MBR disk

\

Create and delete partition on GPT disk

\

Describe Logical Volume Manager and its components

\

Understand various Logical Volume Manager management operations

\

Know Logical Volume Manager administration commands

\

Overview of Virtual Data Optimizer and how it conserves storage

\

Create and confirm physical volumes, volume groups, LVM logical volumes,
and VDO logical volumes

\

Rename, reduce, extend, and remove logical volumes

\

Extend, reduce, and remove volume groups

\

Remove physical volumes

\

#### RHCSA Objectives:

\

26\. List, create, and delete partitions on MBR and GPT disks

27\. Create and remove physical volumes

28\. Assign physical volumes to volume groups

29\. Create and delete logical volumes

31\. Add new partitions and logical volumes, and swap to a system
nondestructively (the swap portion of this objective is covered in
Chapter 14 )

35\. Extend existing logical volumes (additional coverage on this
objective is available in Chapter 14 )

::: {style="page-break-before: always;"}
:::

\

Data is stored on disks that are logically divided into partitions. A
partition can exist on a portion of a disk, on an entire disk, or it may
span multiple disks. Each partition is accessed and managed independent
of other partitions and may contain a file system or swap space.
Partitioning information is stored at special disk locations that the
system references at boot time. RHEL offers a number of tools for
partition management. Partitions created with a combination of most of
these tools can coexist on a single disk.

\

Thin provisioning is a powerful feature that guarantees an efficient use
of storage space by allocating only what is needed and by storing data
at adjacent locations. Many storage management solutions such as those
we discuss later in this chapter and in the next incorporate thin
provisioning technology in their core configuration.

\

Virtual Data Optimizer capitalizes on thin provisioning, de-duplication,
and compression technologies to conserve storage space, improve data
throughput, and save money.

\

::: {style="text-align: center;"}
![](image-ZC2N5YSX.jpg){height="100%"}
:::

The Logical Volume Manager solution sets up an abstraction layer between
the operating system and the storage hardware. It utilizes virtual
objects for storage pooling and allocation, and offers a slew of
commands to carry out management operations.

::: {style="page-break-before: always;"}
:::

[]{#chapter0387.html}

## Storage Management Overview {.style3}

\

A disk in RHEL can be carved up into several partitions. This partition
information is stored on the disk in a small region, which is read by
the operating system at boot time. This region is referred to as the
Master Boot Record (MBR) on the BIOS-based systems, and GUID Partition
Table (GPT) on the UEFI-based systems. At system boot, the BIOS/UEFI
scans all storage devices, detects the presence of MBR/GPT areas,
identifies the boot disks, loads the bootloader program in memory from
the default boot disk, executes the boot code to read the partition
table and identify the /boot partition, loads the kernel in memory, and
passes control over to it. Though MBR and GPT are designed for different
PC firmware types, their job is essentially the same: to store disk
partition information and the boot code.

::: {style="page-break-before: always;"}
:::

[]{#chapter0388.html}

## Master Boot Record (MBR) {.style3}

\

The MBR resides on the first sector of the boot disk. MBR was the
preferred choice for saving partition table information on x86-based
computers. However, with the arrival of bigger and larger hard drives, a
new firmware specification (UEFI) was introduced. MBR is still widely
used, but its use is diminishing in favor of UEFI.

\

MBR allows the creation of three types of partition---primary, extended,
and logical---on a single disk. Of these, only primary and logical can
be used for data storage; the extended is a mere enclosure for holding
the logical partitions and it is not meant for data storage. MBR
supports the creation of up to four primary partitions numbered 1
through 4 at a time. In case additional partitions are required, one of
the primary partitions must be deleted and replaced with an extended
partition to be able to add logical partitions (up to 11) within that
extended partition. Numbering for logical partitions begins at 5. MBR
supports a maximum of 14 usable partitions (3 primary and 11 logical) on
a single disk.

\

MBR cannot address storage space beyond 2TB. This is due to its 32-bit
nature and its 512-byte disk sector size. The MBR is non-redundant; the
record it contains is not replicated, resulting in an unbootable system
in the event of corruption. If your disk is smaller than 2TB and you
don't intend to build more than 14 usable partitions, you can use MBR
without issues. For more information on MBR, refer to Chapter 11 "Boot
Process, GRUB2, and the Linux Kernel".

::: {style="page-break-before: always;"}
:::

[]{#chapter0389.html}

## GUID Partition Table (GPT) {.style3}

\

With the increasing use of disks larger than 2TB on x86 computers, a new
64-bit partitioning standard called Globally Unique Identifiers (GUID)
Partition Table (GPT) was developed and integrated into the UEFI
firmware. This new standard introduced plenty of enhancements, including
the ability to construct up to 128 partitions (no concept of extended or
logical partitions), utilize disks larger than 2TB, use 4KB sector size,
and store a copy of the partition information before the end of the disk
for redundancy.

\

Moreover, this standard allows a BIOS-based system to boot from a GPT
disk using the bootloader program stored in a protective MBR at the
first disk sector. In addition, the UEFI firmware also supports the
secure boot feature, which only allows signed binaries to boot. For more
information on UEFI and GPT, refer to Chapter 11 "Boot Process, GRUB2,
and the Linux Kernel".

::: {style="page-break-before: always;"}
:::

[]{#chapter0390.html}

## Disk Partitions {.style3}

\

The space on a storage device can be sliced into partitions. Care must
be taken when adding a new partition to elude data corruption with
overlapping an extant partition or wasting storage by leaving unused
space between adjacent partitions. On server1, the disk that was
allocated at the time of installation is recognized as sda (s for SATA,
SAS, or SCSI device) disk a, with the first partition identified as sda1
and the second partition as sda2. Any subsequent disks added to the
system will be known as sdb, sdc, sdd, and so on, and will use 1, 2, 3,
etc. for partition numbering.

\

RHEL offers a command called lsblk to list disk and partition
information. The following graphic illustrates the current storage
status on server1:

\

<div>

![](image-U3XAWUUX.jpg){height="100%"}

</div>

It reveals the presence of one 20GB disk, sda, with two partitions: sda1
and sda2. The first partition holds /boot, and the second one is an LVM
object encapsulating root (17GB) and swap (2GB) logical volumes within
it. Both sda1 and sda2 partitions occupy the entire disk capacity. The
sr0 represents the ISO image mounted as an optical medium.

\

LVM is discussed at length later in this chapter.

\

There are additional tools such as fdisk and parted available that can
be used to expose disk and partitioning information. Let's run fdisk
with -l and see what it reveals:

\

<div>

![](image-MLI4LMNG.jpg){height="100%"}

</div>

The output depicts the size of sda in GBs, bytes, and sectors, the type
of disk label (dos) the disk has, and the disk's geometry in the top
block. The second block shows the two disk partitions: sda1 as the
bootable partition marked with an asterisk (\*) and sda2 as an LVM
partition. It also exposes the starting and ending sector numbers, size
in 1KB blocks, and type of each partition. The identifiers 83 and 8e are
hexadecimal values for the partition types. The last two blocks are
specific to the LVM logical volumes that exist within the sda2
partition.

::: {style="page-break-before: always;"}
:::

[]{#chapter0391.html}

## Storage Management Tools {.style3}

\

RHEL offers numerous tools and toolsets for storage management, and they
include parted, gdisk, and LVM. There are other native tools available
in the OS, but their discussion is beyond the scope of this book.
Partitions created with a combination of most of these tools and
toolsets can coexist on the same disk.

\

parted is a simple tool that understands both MBR and GPT formats. gdisk
is designed to support the GPT format only, and it may be used as a
replacement of parted. LVM is a feature-rich logical volume management
solution that gives flexibility in storage management.

::: {style="page-break-before: always;"}
:::

[]{#chapter0392.html}

## Thin Provisioning {.style3}

\

Thin provisioning technology allows for an economical allocation and
utilization of storage space by moving arbitrary data blocks to
contiguous locations, which results in empty block elimination. With
thin provisioning support in LVM, you can create a thin pool of storage
space and assign volumes much larger storage space than the physical
capacity of the pool. Workloads begin consuming the actual allocated
space for data writing. When a preset custom threshold (80%, for
instance) on the actual consumption of the physical storage in the pool
is reached, expand the pool dynamically by adding more physical storage
to it. The volumes will automatically start exploiting the new space
right away. The thin provisioning technique helps prevent spending more
money upfront.

::: {style="page-break-before: always;"}
:::

[]{#chapter0393.html}

## Adding Storage for Practice {.style3}

\

This and the next chapter have a considerable number of exercises that
require block storage devices for practice. In Chapter 01 "Local
Installation" under "Lab Environment for Practice", we mentioned that
server2 will have 4x250MB and 1x5GB virtual disks for storage exercises.
We presume that server2 was built as part of Lab 1-1 and it is now
available for use.

::: {style="page-break-before: always;"}
:::

[]{#chapter0394.html}

## Exercise 13-1: Add Required Storage to server2 {.style3}

\

This exercise will add the required storage disks to server2 (RHEL9-VM2)
using VirtualBox.

\

In this exercise, you will start VirtualBox and add 4x250MB and 1x5GB
disks to server2 in preparation for exercises in this and the next
chapter.

\

1\. Start VirtualBox on your Windows/Mac computer and highlight the
RHEL9-VM2 virtual machine that you created in Lab 1-1. See Figure 13-1.

\

::: {style="text-align: center;"}
![](image-KEGS1BT1.jpg){height="100%"}
:::

Figure 13-1 VirtualBox Manager \| RHEL9-VM2 Selected

\

2\. Click Settings at the top and then Storage on the window that pops
up. Click on "Controller: SATA" to select it. Figure 13-2.

\

::: {style="text-align: center;"}
![](image-KWA12KXW.jpg){height="100%"}
:::

Figure 13-2 VirtualBox Manager \| Add Storage

\

3\. Click on the right-side icon next to "Controller: SATA" to add a
hard disk and then click Create (on the Medium Selector screen). Figure
13-3.

\

::: {style="text-align: center;"}
![](image-Q6NZNE81.jpg){height="100%"}
:::

Figure 13-3 VirtualBox Manager \| Medium Selector Screen

\

4\. Follow this sequence to add a 250MB disk: Click Next on the next two
screens to select the two defaults for the "VDI (Virtualization Disk
Image)" and "Dynamically allocated" options. Adjust the size on the
third screen to 250MB. Assign the disk a unique name and click Finish to
complete the process. Figure 13-4.

\

::: {style="text-align: center;"}
![](image-DPO9QA8O.jpg){height="100%"}
:::

Figure 13-4 VirtualBox Manager \| Create a Disk

\

5\. Repeat step 4 three more times to create additional disks of the
same size.

6\. Repeat step 4 one time to create a disk of size 5GB.

7\. On the Medium Selector screen, the five new disks will appear under
the Not Attached list of disks. Double-click on each one of them to add
to RHEL9-VM2.

\

::: {style="text-align: center;"}
![](image-I02OKCQR.jpg){height="100%"}
:::

Figure 13-5 VirtualBox Manager \| 5 New Disks Created

\

8\. The final list of disks should look similar to what is shown in
Figure 13-6 after the addition of all five disks (RHEL9-VM2_1 to
RHEL9-VM2_5). Disk names may vary.

\

::: {style="text-align: center;"}
![](image-38AAB6BK.jpg){height="100%"}
:::

Figure 13-6 VirtualBox Manager \| 5 New Disks Added

\

9\. Click OK to return to the main VirtualBox interface.

10\. Power on RHEL9-VM2.

11\. When the server is booted up, log on as user1 and run the lsblk
command to verify the new storage:

\

<div>

![](image-CYDQFW2E.jpg){height="100%"}

</div>

12\. The five new disks added to server2 are 250MB (sdb, sdc, sdd, and
sde) and 5GB (sdf).

\

This concludes the exercise for storage addition to server2.

::: {style="page-break-before: always;"}
:::

[]{#chapter0395.html}

## MBR Storage Management with parted {.style3}

\

parted (partition editor) is a popular tool in RHEL that can be used to
partition disks. This program may be run interactively or directly from
the command prompt. It understands and supports both MBR and GPT
schemes, and can be used to create up to 128 partitions on a single GPT
disk. parted provides an abundance of subcommands to perform disk
management operations such as viewing, labeling, adding, naming, and
deleting partitions. Table 13-1 describes these subcommands in that
sequence.

\

  ----------------------------------- -----------------------------------
  Subcommand                          Description

  print                               Displays the partition table that
                                      includes disk geometry and
                                      partition number, start and end,
                                      size, type, file system type, and
                                      relevant flags.

  mklabel                             Applies a label to the disk. Common
                                      labels are gpt and msdos.

  mkpart                              Makes a new partition

  name                                Assigns a name to a partition

  rm                                  Removes the specified partition
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 13-1 Common parted Subcommands

\

For the basic partition creation and deletion operations, Exercises 13-2
and 13-3 will show the use of this tool by directly invoking it from the
command prompt. You will use the /dev/sdb disk for these exercises.
After making a partition, use the print subcommand to ensure you created
what you wanted. The /proc/partitions file is also updated to reflect
the results of partition management operations.

::: {style="page-break-before: always;"}
:::

[]{#chapter0396.html}

## Exercise 13-2: Create an MBR Partition {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will assign partition type "msdos" to /dev/sdb for
using it as an MBR disk. You will create and confirm a 100MB primary
partition on the disk.

\

1\. Execute parted on /dev/sdb to view the current partition
information:

\

<div>

![](image-AJS3MV0N.jpg){height="100%"}

</div>

There is an error on line 1 of the output, indicating an unrecognized
label. This disk must be labeled before it can be partitioned.

\

2\. Assign disk label "msdos" to the disk with mklabel. This operation
is performed only once on a disk.

\

<div>

![](image-HZI83BCJ.jpg){height="100%"}

</div>

The print subcommand confirms the successful application of the label.

\

To use the GPT partition table type, run "sudo parted /dev/sdb mklabel
gpt" instead.

\

3\. Create a 100MB primary partition starting at 1MB (beginning of the
disk) using mkpart:

\

<div>

![](image-B5KT2H2C.jpg){height="100%"}

</div>

4\. Verify the new partition with print:

\

<div>

![](image-JHXL8DUV.jpg){height="100%"}

</div>

Partition numbering begins at 1 by default.

\

5\. Confirm the new partition with the lsblk command:

\

<div>

![](image-588XNE8G.jpg){height="100%"}

</div>

The device file for the first partition on the sdb disk is sdb1 as
identified on the bottom line. The partition size is 95MB.

\

Different tools will have variance in reporting partition sizes. You
should ignore minor differences.

\

6\. Check the /proc/partitions file also:

\

<div>

![](image-63FMXEBC.jpg){height="100%"}

</div>

The virtual file is also updated with the new partition information.
This completes the steps for creating and verifying an MBR partition
using the parted command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0397.html}

## Exercise 13-3: Delete an MBR Partition {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will delete the sdb1 partition that was created in
Exercise 13-2 and confirm the deletion.

\

1\. Execute parted on /dev/sdb with the rm subcommand to remove
partition number 1:

\

<div>

![](image-AXOLB7MY.jpg){height="100%"}

</div>

2\. Confirm the partition deletion with print:

\

<div>

![](image-7961UAET.jpg){height="100%"}

</div>

The partition no longer exists.

\

3\. Check the /proc/partitions file:

\

<div>

![](image-B25TKSXL.jpg){height="100%"}

</div>

The virtual file has the partition entry deleted as well. You can also
run the lsblk command for further verification. The partition has been
removed successfully.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Knowing either parted or gdisk for the exam is enough.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

We will recreate partitions for use in LVM later in this chapter and
then again in the next chapter to construct file system and swap
structures.

::: {style="page-break-before: always;"}
:::

[]{#chapter0398.html}

## GPT Storage Management with gdisk {.style3}

\

The gdisk (GPT disk) utility partitions disks using the GPT format. This
text-based, menu-driven program can show, add, verify, modify, and
delete partitions among other operations. gdisk can create up to 128
partitions on a single disk on systems with UEFI firmware.

\

The main interface of gdisk can be invoked by specifying a disk device
name such as /dev/sdc with the command. Type help or ? (question mark)
at the prompt to view available subcommands.

\

<div>

![](image-QCNBZ0VW.jpg){height="100%"}

</div>

The output illustrates that there is no partition table defined on the
disk at the moment. There are several subcommands in the main menu
followed by a short description. Refer to the screenshot above for a
list of subcommands. Enter q to quit and return to the command prompt.

::: {style="page-break-before: always;"}
:::

[]{#chapter0399.html}

## Exercise 13-4: Create a GPT Partition {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will assign partition type "gpt" to /dev/sdc for
using it as a GPT disk. You will create and confirm a 200MB partition on
the disk.

\

1\. Execute gdisk on /dev/sdc to view the current partition information:

\

<div>

![](image-9E3PG988.jpg){height="100%"}

</div>

The disk currently does not have any partition table on it.

\

2\. Assign "gpt" as the partition table type to the disk using the o
subcommand. Enter "y" for confirmation to proceed. This operation is
performed only once on a disk.

\

<div>

![](image-HHL2BAA8.jpg){height="100%"}

</div>

3\. Run the p subcommand to view disk information and confirm the GUID
partition table creation:

\

<div>

![](image-NZARY1XW.jpg){height="100%"}

</div>

The output returns the assigned GUID and states that the partition table
can hold up to 128 partition entries.

\

4\. Create the first partition of size 200MB starting at the default
sector with default type "Linux filesystem" using the n subcommand:

\

<div>

![](image-86XFQWVL.jpg){height="100%"}

</div>

5\. Verify the new partition with p:

\

<div>

![](image-KIK83Z1M.jpg){height="100%"}

</div>

6\. Run w to write the partition information to the partition table and
exit out of the interface. Enter "y" to confirm when prompted.

\

<div>

![](image-LQV4DH6R.jpg){height="100%"}

</div>

\

You may need to run the partprobe command after exiting the gdisk
utility to inform the kernel of partition table changes.

\

7\. Verify the new partition by issuing either of the following at the
command prompt:

\

<div>

![](image-U8O9IN1Y.jpg){height="100%"}

</div>

The device file for the first partition on the sdc disk is sdc1 and it
is 200MB in size as reported in the above outputs. This completes the
steps for creating and verifying a GPT partition using the gdisk
command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0400.html}

## Exercise 13-5: Delete a GPT Partition {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will delete the sdc1 partition that was created in
Exercise 13-4 and confirm the removal.

\

1\. Execute gdisk on /dev/sdc and run d1 at the utility's prompt to
delete partition number 1:

\

<div>

![](image-IP250O65.jpg){height="100%"}

</div>

2\. Confirm the partition deletion with p:

\

<div>

![](image-F124Y0JN.jpg){height="100%"}

</div>

The partition no longer exists.

\

3\. Write the updated partition information to the disk with w and quit
gdisk:

\

<div>

![](image-R97S52OF.jpg){height="100%"}

</div>

4\. Verify the partition deletion by issuing either of the following at
the command prompt:

\

<div>

![](image-58Z53OYA.jpg){height="100%"}

</div>

Both commands confirm the successful partition removal.

::: {style="page-break-before: always;"}
:::

[]{#chapter0401.html}

## Logical Volume Manager (LVM) {.style3}

\

The Logical Volume Manager (LVM) solution is widely used for managing
block storage in Linux. LVM provides an abstraction layer between the
physical storage and the file system, enabling the file system to be
resized, span across multiple disks, use arbitrary disk space, etc. LVM
accumulates spaces taken from partitions or entire disks (called
Physical Volumes) to form a logical container (called Volume Group),
which is then divided into logical partitions (called Logical Volumes).
The other key benefits of LVM include online resizing of volume groups
and logical volumes, online data migration between logical volumes and
between physical volumes, user-defined naming for volume groups and
logical volumes, mirroring and striping across multiple disks, and
snapshotting of logical volumes. Figure 13-7 depicts the LVM components.

\

::: {style="text-align: center;"}
![](image-0A8W8M1U.jpg){height="100%"}
:::

Figure 13-7 LVM Structure

\

As noted above, the LVM structure is made up of three key objects called
physical volume, volume group, and logical volume. These objects are
further virtually broken down into Physical Extents (PEs) and Logical
Extents (LEs). The LVM components are explained in the following
subsections.

::: {style="page-break-before: always;"}
:::

[]{#chapter0402.html}

## Physical Volume {.style3}

\

A Physical Volume (PV) is created when a block storage device such as a
partition or an entire disk is initialized and brought under LVM
control. This process constructs LVM data structures on the device,
including a label on the second sector and metadata shortly thereafter.
The label includes the UUID, size, and pointers to the locations of data
and metadata areas. Given the criticality of metadata, LVM stores a copy
of it at the end of the physical volume as well. The rest of the device
space is available for use.

\

You can use an LVM command called pvs (physical volume scan or summary)
to scan and list available physical volumes on server2:

\

<div>

![](image-ZD44Z3KN.jpg){height="100%"}

</div>

The output shows one physical volume (PV) /dev/sda2 of size 19GB in rhel
volume group (VG). Additional information displays the metadata format
(Fmt) used, status of the physical volume under the Attr column (a for
allocatable), and the amount of free space available on the physical
volume (PFree).

\

Try running this command again with the -v flag to view more information
about the physical volume.

::: {style="page-break-before: always;"}
:::

[]{#chapter0403.html}

## Volume Group {.style3}

\

A Volume Group (VG) is created when at least one physical volume is
added to it. The space from all physical volumes in a volume group is
aggregated to form one large pool of storage, which is then used to
build logical volumes. The physical volumes added to a volume group may
be of varying sizes. LVM writes volume group metadata on each physical
volume that is added to it. The volume group metadata contains its name,
date and time of creation, how it was created, the extent size used, a
list of physical and logical volumes, a mapping of physical and logical
extents, etc. A volume group can have a custom name assigned to it at
the time of its creation. For example, it may be called vg01, vgora, or
vgweb that identifies the type of information it is constructed to
store. A copy of the volume group metadata is stored and maintained at
two distinct locations on each physical volume within the volume group.

\

You can use an LVM command called vgs (volume group scan or summary) to
scan and list available volume groups on server2:

\

<div>

![](image-3RA1ON81.jpg){height="100%"}

</div>

The output shows one volume group (VG) rhel on server2 containing one
physical volume (#PV). Additional information displays the number of
logical volumes (#LV) and snapshots (#SN) in the volume group, status of
the volume group under the Attr column (w for writeable, z for
resizable, and n for normal), size of the volume group (VSize), and the
amount of free space available in the volume group (VFree).

\

Try running this command again with the -v flag to view more information
about the volume group.

::: {style="page-break-before: always;"}
:::

[]{#chapter0404.html}

## Physical Extent {.style3}

\

A physical volume is divided into several smaller logical pieces when it
is added to a volume group. These logical pieces are known as Physical
Extents (PE). An extent is the smallest allocatable unit of space in
LVM. At the time of volume group creation, you can either define the
size of the PE or leave it to the default value of 4MB. This implies
that a 20GB physical volume would have approximately 5,000 PEs. Any
physical volumes added to this volume group thereafter will use the same
PE size.

\

You can use an LVM command called vgdisplay (volume group display) on
server2 and grep for 'PE Size' to view the PE size used in the rhel
volume group:

\

<div>

![](image-ZJI1USBI.jpg){height="100%"}

</div>

The output reveals the PE size used for the rhel VG.

::: {style="page-break-before: always;"}
:::

[]{#chapter0405.html}

## Logical Volume {.style3}

\

A volume group consists of a pool of storage taken from one or more
physical volumes. This volume group space is used to create one or more
Logical Volumes (LVs). A logical volume can be created or weeded out
online, expanded or shrunk online, and can use space taken from one or
multiple physical volumes inside the volume group.

\

The default naming convention used for logical volumes is lvol0, lvol1,
lvol2, and so on; however, you may assign custom names to them. For
example, a logical volume may be called system, undo, or webdata1 so as
to establish the type of information it is constructed to store.

\

You can use an LVM command called lvs (logical volume scan or summary)
to scan and list available logical volumes on server2:

\

<div>

![](image-VY154SEV.jpg){height="100%"}

</div>

The output shows two logical volumes root and swap in rhel volume group.
Additional information displays the status of the logical volumes under
the Attr column (w for writeable, i for inherited allocation policy, a
for active, and o for open) and their sizes.

\

Try running this command again with the -v flag to view more information
about the logical volumes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0406.html}

## Logical Extent {.style3}

\

A logical volume is made up of Logical Extents (LE). Logical extents
point to physical extents, and they may be random or contiguous. The
larger a logical volume is, the more logical extents it will have.
Logical extents are a set of physical extents allocated to a logical
volume.

\

The LE size is always the same as the PE size in a volume group. The
default LE size is 4MB, which corresponds to the default PE size of 4MB.

\

You can use an LVM command called lvdisplay (logical volume display) on
server2 to view information about the root logical volume in the rhel
volume group.

\

<div>

![](image-E8W3BEYL.jpg){height="100%"}

</div>

The output does not disclose the LE size; however, you can convert the
LV size in MBs (17,000) and then divide the result by the Current LE
count (4,351) to get the LE size (which comes close to 4MB).

::: {style="page-break-before: always;"}
:::

[]{#chapter0407.html}

## LVM Operations and Commands {.style3}

\

The LVM toolset offers a multitude of administrative commands to carry
out various disk and volume management operations. These operations
include creating and removing a physical volume, volume group, and
logical volume; extending and reducing a volume group and logical
volume; renaming a volume group and logical volume; and listing and
displaying physical volume, volume group, and logical volume
information.

\

[Table 13-2 summarizes the common LVM tasks and the commands that are
employed to accomplish them.](#chapter0407.html)

\

  ----------------------------------- -----------------------------------
  Command                             Description

  Create and Remove Operations        

  pvcreate/pvremove                   Initializes/uninitializes a disk or
                                      partition for LVM use

  vgcreate/vgremove                   Creates/removes a volume group

  lvcreate/lvremove                   Creates/removes a logical volume

  Extend and Reduce Operations        

  vgextend/vgreduce                   Adds/removes a physical volume
                                      to/from a volume group

  lvextend/lvreduce                   Extends/reduces the size of a
                                      logical volume

  lvresize                            Resizes a logical volume. With the
                                      -r option, this command calls the
                                      fsadm command to resize the
                                      underlying file system as well.

  Rename Operations                   

  vgrename                            Renames a volume group

  lvrename                            Renames a logical volume

  List and Display Operations         

  pvs/pvdisplay                       Lists/displays physical volume
                                      information

  vgs/vgdisplay lvs/lvdisplay         Lists/displays volume group
                                      information Lists/displays logical
                                      volume information
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 13-2 Common LVM Operations and Commands

\

All the tools accept the -v switch to support verbosity. Refer to the
manual pages of the commands for usage and additional details.

\

As noted earlier, there are five disks available on server2 for
practice. Issue the lsblk command to confirm:

\

<div>

![](image-IQ604KE2.jpg){height="100%"}

</div>

You will use the sdd and sde disks for LVM activities in the following
exercises.

::: {style="page-break-before: always;"}
:::

[]{#chapter0408.html}

## Exercise 13-6: Create Physical Volume and Volume Group {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will initialize one partition sdd1 (90MB) and one
disk sde (250MB) for use in LVM. You will create a volume group called
vgbook and add both physical volumes to it. You will use the PE size of
16MB and list and display the volume group and the physical volumes.

\

1\. Create a partition of size 90MB on sdd using the parted command and
confirm. You need to label the disk first, as it is a new disk.

\

<div>

![](image-CE00XPQH.jpg){height="100%"}

</div>

The print subcommand confirms the creation of the partition. It is the
first partition on the disk.

\

2\. Initialize the sdd1 partition and the sde disk using the pvcreate
command. Note that there is no need to apply a disk label on sde with
parted as LVM does not require it.

\

<div>

![](image-IJTXXRS0.jpg){height="100%"}

</div>

The command generated a verbose output. You now have two physical
volumes available for use.

\

3\. Create vgbook volume group using the vgcreate command and add the
two physical volumes to it. Use the -s option to specify the PE size in
MBs.

\

<div>

![](image-V1UW06IN.jpg){height="100%"}

</div>

The above command combines the two options with a single hyphen.

\

4\. List the volume group information:

\

<div>

![](image-16BC13SM.jpg){height="100%"}

</div>

The total capacity available in the vgbook volume group is 320MB.

\

5\. Display detailed information about the volume group and the physical
volumes it contains:

\

<div>

![](image-5UI974Y3.jpg){height="100%"}

</div>

The verbose output includes the physical volume attributes as well.
There are a total of 20 PEs in the volume group (5 in sdd1 and 15 in
sde), and each PE is 16MB in size. The collective size of all the
physical volumes represents the total size of the volume group, which is
20x16 = 320MB.

\

6\. List the physical volume information:

\

<div>

![](image-2ZSLLM5D.jpg){height="100%"}

</div>

The output shows the physical volumes in vgbook, along with their
utilization status.

\

7\. Display detailed information about the physical volumes:

\

<div>

![](image-9KCGXIQ4.jpg){height="100%"}

</div>

Once a partition or disk is initialized and added to a volume group,
they are treated identically within the volume group. LVM does not
prefer one over the other.

::: {style="page-break-before: always;"}
:::

[]{#chapter0409.html}

## Exercise 13-7: Create Logical Volumes {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will create two logical volumes, lvol0 and
lvbook1, in the vgbook volume group. You will use 120MB for lvol0 and
192MB for lvbook1 from the available pool of space. You will display the
details of the volume group and the logical volumes.

\

1\. Create a logical volume with the default name lvol0 using the
lvcreate command. Use the -L option to specify the logical volume size,
120MB. You may use the -v, -vv, or -vvv option with the command for
verbosity.

\

<div>

![](image-LM32OX2F.jpg){height="100%"}

</div>

The size for the logical volume may be specified in units such as MBs,
GBs, TBs, or as a count of LEs; however, MB is the default if no unit is
specified (see the previous command). The size of a logical volume is
always in multiples of the PE size. For instance, logical volumes
created in vgbook with the PE size set at 16MB can be 16MB, 32MB, 48MB,
64MB, and so on. The output above indicates that the logical volume is
128MB (16x8), and not 120MB as specified.

\

2\. Create lvbook1 of size 192MB (16x12) using the lvcreate command. Use
the -l switch to specify the size in logical extents and -n for the
custom name. You may use -v for verbose information.

\

<div>

![](image-5WX9APRS.jpg){height="100%"}

</div>

3\. List the logical volume information:

\

<div>

![](image-T04RWZJ7.jpg){height="100%"}

</div>

Both logical volumes are listed in the output with their attributes and
sizes.

\

4\. Display detailed information about the volume group including the
logical volumes and the physical volumes:

\

<div>

![](image-C9RER9NP.jpg){height="100%"}

</div>

\

<div>

![](image-LXNQEW50.jpg){height="100%"}

</div>

Alternatively, you can run the following to view only the logical volume
details:

\

<div>

![](image-YJEYF4QX.jpg){height="100%"}

</div>

Review the attributes of the logical volumes as detailed above.

::: {style="page-break-before: always;"}
:::

[]{#chapter0410.html}

## Exercise 13-8: Extend a Volume Group and a Logical Volume {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will add another partition sdd2 of size 158MB to
vgbook to increase the pool of allocatable space. You will initialize
the new partition prior to adding it to the volume group. You will
increase the size of lvbook1 to 336MB. You will display basic
information for the physical volumes, volume group, and logical volume.

\

1\. Create a partition of size 158MB on sdd using the parted command.
Display the new partition to confirm the partition number and size.

\

<div>

![](image-1LUKNR1B.jpg){height="100%"}

</div>

2\. Initialize sdd2 using the pvcreate command:

\

<div>

![](image-6BRTO4VJ.jpg){height="100%"}

</div>

3\. Extend vgbook by adding the new physical volume to it:

\

<div>

![](image-W08IN5NA.jpg){height="100%"}

</div>

4\. List the volume group:

\

<div>

![](image-16OT9SWB.jpg){height="100%"}

</div>

The output reflects the addition of a third physical volume to vgbook.
The total capacity of the volume group has now increased to 464MB with
144MB free.

\

5\. Extend the size of lvbook1 to 340MB by adding 144MB using the
lvextend command:

\

<div>

![](image-YFBWSLAR.jpg){height="100%"}

</div>

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Make sure the expansion of a logical volume does not affect
the file system and the data it contains. More details in Chapter 14 .

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

6\. Issue vgdisplay on vgbook with the -v switch for the updated
details:

\

<div>

![](image-IA1APY6X.jpg){height="100%"}

</div>

The output will show a lot of information about the volume group and the
logical and physical volumes it contains. It will reflect the updates
made in this exercise. In fact, each time a volume group or a logical
volume is resized, vgdisplay will reflect those changes. The above
output will display three physical volumes with the combined allocatable
space grown to 464MB. The number of PEs will have increased to 29, with
all of them allocated to logical volumes and 0 unused. The Logical
Volume sections will display the updated information for the logical
volumes. And at the very bottom, the three physical volumes will show
with their device names, and total and available PEs in each.

\

7\. View a summary of the physical volumes:

\

<div>

![](image-BNB11UMX.jpg){height="100%"}

</div>

8\. View a summary of the logical volumes:

\

<div>

![](image-KVL01A4Y.jpg){height="100%"}

</div>

This brings the exercise to an end.

::: {style="page-break-before: always;"}
:::

[]{#chapter0411.html}

## Exercise 13-9: Rename, Reduce, Extend, and Remove Logical Volumes {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will rename lvol0 to lvbook2. You will decrease
the size of lvbook2 to 50MB using the lvreduce command and then add 32MB
with the lvresize command. You will then remove both logical volumes.
You will display the summary for the volume groups, logical volumes, and
physical volumes.

\

1\. Rename lvol0 to lvbook2 using the lvrename command and confirm with
lvs:

\

<div>

![](image-MONQ5OD7.jpg){height="100%"}

</div>

2\. Reduce the size of lvbook2 to 50MB with the lvreduce command.
Specify the absolute desired size for the logical volume. Answer "Do you
really want to reduce vgbook/lvbook2?" in the affirmative.

\

<div>

![](image-DHLM2WXM.jpg){height="100%"}

</div>

3\. Add 32MB to lvbook2 with the lvresize command:

\

<div>

![](image-OT804AWH.jpg){height="100%"}

</div>

4\. Use the pvs, lvs, vgs, and vgdisplay commands to view the updated
allocation.

5\. Remove both lvbook1 and lvbook2 logical volumes using the lvremove
command. Use the -f option to suppress the "Do you really want to remove
active logical volume" message.

\

<div>

![](image-9MARYSLB.jpg){height="100%"}

</div>

\

Removing a logical volume is a destructive task. You need to ensure that
you perform a backup of any data in the target logical volume prior to
deleting it. You will need to unmount the file system or disable swap in
the logical volume. See Chapter 15 on how to unmount a file system and
disable swap.

\

6\. Execute the vgdisplay command and grep for "Cur LV" to see the
number of logical volumes currently available in vgbook. It should show
0, as you have removed both logical volumes.

\

<div>

![](image-OTTUCPHQ.jpg){height="100%"}

</div>

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0412.html}

## Exercise 13-10: Reduce and Remove a Volume Group {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will reduce vgbook by removing the sdd1 and sde
physical volumes from it, and then remove the volume group. Confirm the
deletion of the volume group and the logical volumes at the end.

\

1\. Remove sdd1 and sde physical volumes from vgbook by issuing the
vgreduce command:

\

<div>

![](image-DNYF6XNR.jpg){height="100%"}

</div>

2\. Remove the volume group using the vgremove command. This will also
remove the last physical volume, sdd2, from it.

\

<div>

![](image-BJ081UKL.jpg){height="100%"}

</div>

\

You can also use the -f option with the vgremove command to force the
volume group removal even if it contains any number of logical and
physical volumes in it.

\

Remember to proceed with caution whenever you perform reduce and erase
operations.

\

3\. Execute the vgs and lvs commands for confirmation:

\

<div>

![](image-29VMZAKH.jpg){height="100%"}

</div>

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0413.html}

## Exercise 13-11: Uninitialize Physical Volumes {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will uninitialize all three physical
volumes---sdd1, sdd2, and sde---by deleting the LVM structural
information from them. Use the pvs command for confirmation. Remove the
partitions from the sdd disk and verify that all disks used in Exercises
13-6 to 13-10 are now in their original raw state.

\

1\. Remove the LVM structures from sdd1, sdd2, and sde using the
pvremove command:

\

<div>

![](image-I0CEGYL2.jpg){height="100%"}

</div>

2\. Confirm the removal using the pvs command:

\

<div>

![](image-WEFABC3J.jpg){height="100%"}

</div>

The partitions and the disk are now back to their raw state and can be
repurposed.

\

3\. Remove the partitions from sdd using the parted command:

\

<div>

![](image-SA75RDRK.jpg){height="100%"}

</div>

4\. Verify that all disks used in previous exercises have returned to
their original raw state using the lsblk command:

\

<div>

![](image-57AXIZUP.jpg){height="100%"}

</div>

This brings the exercise to an end.

\

We will recreate logical volumes and construct file system and swap
structures in them in the next chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0414.html}

## Storage Optimization with Virtual Data Optimizer (VDO) {.style3}

\

Virtual Data Optimizer (VDO) is a device driver layer that sits between
the Linux kernel and the physical storage devices. The goals are to
conserve disk space, improve data throughput, and save on storage cost.
VDO employs thin provisioning, de-duplication, and compression
technologies to help realize the goals.

::: {style="page-break-before: always;"}
:::

[]{#chapter0415.html}

## How VDO Conserves Storage {.style3}

\

VDO makes use of the thin provisioning technology to identify and
eliminate empty (zero-byte) data blocks. This is referred to as
zero-block elimination. VDO removes randomization of data blocks by
moving in-use data blocks to contiguous locations on the storage device.
This is the initial stage in the process.

\

::: {style="text-align: center;"}
![](image-XYSCLXMC.jpg){height="100%"}
:::

Figure 13-8 Storage Optimization with VDO

\

Next, VDO keeps an eye on data being written to the disk. If it detects
that the new data is an identical copy of some existing data, it makes
an internal note of it but does not actually write the redundant data to
the disk. VDO uses the technique called de-duplication to this end. This
technique is implemented with the inclusion of a kernel module called
UDS (Universal De-duplication Service). This is the second stage in the
process.

\

In the third and final stage, VDO calls upon another kernel module
called kvdo, which compresses the residual data blocks and consolidates
them on a lower number of blocks. This results in a further drop in
storage space utilization.

\

VDO runs in the background and processes inbound data through the three
stages on VDO-enabled volumes. VDO is not a CPU- or memory-intensive
process; it consumes a low amount of system resources.

::: {style="page-break-before: always;"}
:::

[]{#chapter0416.html}

## VDO Integration with LVM {.style3}

\

RHEL 9 uses an LVM VDO implementation for managing VDO logical volumes.
Unlike previous versions of RHEL, a separate set of VDO management tools
are no longer necessary. The LVM utilities have been enhanced to include
options to support VDO volumes.

::: {style="page-break-before: always;"}
:::

[]{#chapter0417.html}

## VDO Components {.style3}

\

VDO utilizes the concepts of pool and volume. A pool is a logical volume
that is created inside an LVM volume group using a deduplicated storage
space. A VDO volume is just like a regular LVM logical volume, but it is
provisioned in a pool. A VDO volume needs to be formatted with file
system structures before it can be used.

\

To create, mount, and manage LVM VDO volumes, two software packages are
installed on the system by default. These packages are vdo and
kmod-kvdo. The former installs the tools necessary to support the
creation and management of VDO volumes and the latter implements
fine-grained storage virtualization, thin provisioning, and compression.

::: {style="page-break-before: always;"}
:::

[]{#chapter0418.html}

## Exercise 13-12: Create an LVM VDO Volume {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will initialize the 5GB disk (sdf) for use in LVM
VDO. You will create a volume group called vgvdo and add the physical
volume to it. You will list and display the volume group and the
physical volume. You will create a VDO volume called lvvdo with a
virtual size of 20GB.

\

1\. Initialize the sdf disk using the pvcreate command:

\

<div>

![](image-HTWOFLGF.jpg){height="100%"}

</div>

2\. Create vgvdo volume group using the vgcreate command:

\

<div>

![](image-7KDEEEEN.jpg){height="100%"}

</div>

3\. Display basic information about the volume group:

\

<div>

![](image-D4LB619H.jpg){height="100%"}

</div>

The volume group contains a total of 1279 PEs.

\

4\. Create a VDO volume called lvvdo using the lvcreate command. Use the
-l option to specify the number of logical extents (1279) to be
allocated and the -V option for the amount of virtual space.

\

<div>

![](image-5WY27FZX.jpg){height="100%"}

</div>

5\. Display detailed information about the volume group including the
logical volume and the physical volume:

\

<div>

![](image-YWZ5VAQD.jpg){height="100%"}

</div>

\

<div>

![](image-8TU5RYEF.jpg){height="100%"}

</div>

The output reflects the creation of two logical volumes: a pool called
/dev/vgvdo/vpool0 and a volume called /dev/vgvdo/lvvdo.

::: {style="page-break-before: always;"}
:::

[]{#chapter0419.html}

## Exercise 13-13: Remove a Volume Group and Uninitialize Physical Volume {.style3}

\

This exercise should be done on server2 as user1 with sudo where
required.

\

In this exercise, you will remove the vgvdo volume group along with the
VDO volumes and uninitialize the physical volume /dev/sdf. You will
confirm the deletion.

\

1\. Remove the volume group along with the VDO volumes using the
vgremove command:

\

<div>

![](image-LL4JPQRK.jpg){height="100%"}

</div>

\

Remember to proceed with caution whenever you perform erase operations.

\

2\. Execute sudo vgs and sudo lvs commands for confirmation.

3\. Remove the LVM structures from sdf using the pvremove command:

\

<div>

![](image-R23G6FMO.jpg){height="100%"}

</div>

4\. Confirm the removal by running sudo pvs.

The disk is now back to its raw state and can be repurposed.

\

5\. Verify that the sdf disk used in the previous exercises has returned
to its original raw state using the lsblk command:

\

<div>

![](image-ELG2JGUL.jpg){height="100%"}

</div>

This brings the exercise to an end.

\

We will recreate logical volumes in Chapter 14 and construct file system
and swap structures in them.

::: {style="page-break-before: always;"}
:::

[]{#chapter0420.html}

## Chapter Summary {.style3}

\

This chapter started with an overview of how and where disk partitioning
information is stored. It presented a comparison between the two common
schemes and explained which one to use and in which situation. A little
later, we touched briefly on the common storage management solutions
available in RHEL.

\

We examined the concept of thin provisioning and realized the benefits
associated with this technology.

\

Next, we carved up available disk devices using both MBR and GPT
partitioning schemes. We demonstrated the partition creation, display,
and delete operations by running one command directly at the command
prompt and launching the other in interactive mode.

\

Next, we explicated the Logical Volume Manager solution. We discovered
how LVM works. We looked at various LVM objects and their relationship
with one another. We explored LVM management commands and common options
available with them. We performed a series of exercises to demonstrate
the creation, expansion, renaming, reduction, and deletion of physical
volumes, logical volumes, and volume groups.

\

Finally, we explored the VDO solution and how it exploits the underlying
thin provisioning, de-duplication, and compression technologies to save
cost, ensure efficient use of storage space, and improve data
throughput. We performed a couple of exercises in the end to demonstrate
the creation and deletion of VDO logical volumes under LVM.

::: {style="page-break-before: always;"}
:::

[]{#chapter0421.html}

## Review Questions {.style3}

\

1\. Where is the partition table information stored on BIOS-based
systems?

2\. What is the name of the technology that VDO employs to remove
randomization of data blocks?

3\. What would sdd3 represent?

4\. Provide the command to add physical volumes /dev/sdd1 and /dev/sdc
to vg20 volume group.

5\. What are the two commands that you can use to add logical extents to
a logical volume?

6\. Provide the command to create a volume group called vg20 on /dev/sdd
disk with physical extent size 64MB.

7\. Thin provisioning technology allows us to create logical volumes of
sizes larger than the actual physical storage size. True or False?

8\. What is the maximum supported number of usable partitions on a GPT
disk?

9\. Which kernel module is responsible for data block compression in VDO
volumes?

10\. What are the three techniques VDO volumes employ for storage
conservation?

11\. What would the command parted /dev/sdc mkpart pri 1 200m do?

12\. What is the maximum number of usable partitions that can be created
on an MBR disk?

13\. The gdisk utility can be used to store partition information in MBR
format. True or False?

14\. What would the command parted /dev/sdd mklabel msdos do?

15\. Which file in the /proc file system stores the in-memory
partitioning information?

16\. De-duplication is the process of zero-block elimination. True or
False?

17\. The parted utility may be used to create LVM logical volumes. True
or False?

18\. What are the two commands that you can use to reduce the number of
logical extents from a logical volume?

19\. A single disk can be used by both parted and LVM solutions at the
same time. True or False?

20\. Provide the command to erase /dev/sdd1 physical volume from vg20
volume group.

21\. Provide the command to remove vg20 along with logical and physical
volumes it contains.

22\. What is the default size of a physical extent in LVM?

23\. What is the default name for the first logical volume in a volume
group?

24\. What is one difference between the pvs and pvdisplay commands?

25\. When can a disk or partition be referred to as a physical volume?

26\. Provide the command to remove webvol logical volume from vg20
volume group.

27\. It is necessary to create file system structures in a logical
volume before it can be used to store files in it. True or False?

28\. Physical and logical extents are typically of the same size. True
or False?

29\. What is the purpose of the pvremove command?

30\. What would the command pvcreate /dev/sdd do?

31\. A disk or partition can be added to a volume group without being
initialized. True or False?

32\. Provide the command to create a logical volume called webvol of
size equal to 100 logical extents in vg20 volume group.

33\. A volume group can be created without any physical volume in it.
True or False?

34\. A partition can be used as an LVM object. True or False?

35\. Which command would you use to view the details of a volume group
and its objects?

::: {style="page-break-before: always;"}
:::

[]{#chapter0422.html}

## Answers to Review Questions {.style3}

\

1\. The partition table information is stored on the Master Boot Record.

2\. VDO employs thin provisioning technology to remove data block
randomization.

3\. sdd3 represents the third partition on the fourth disk.

4\. vgextend vg20 /dev/sdd1 /dev/sdc

5\. The lvextend and lvresize commands.

6\. vgcreate -s 64 vg20 /dev/sdd

7\. True.

8\. 128.

9\. The kvdo module is responsible for compressing data blocks in VDO
volumes.

10\. VDO volumes use thin provisioning, de-duplication, and compression
techniques for storage conservation.

11\. The command provided will create a primary partition of size 200MB
on the sdc disk starting at the beginning of the disk.

12\. 14.

13\. False. The gdisk tool is only for GPT type tables.

14\. The command provided will apply msdos label to the sdd disk.

15\. The partitions file.

16\. False. De-duplication is the process of removing blocks of
identical data.

17\. False.

18\. The lvreduce and lvresize commands.

19\. True. A single disk can be shared between parted-created partitions
and LVM.

20\. vgreduce vg20 /dev/sdd1

21\. vgremove -f vg20

22\. The default PE size is 4MB.

23\. lvol0 is the default name for the first logical volume created in a
volume group.

24\. The pvs command lists basic information about physical volumes
whereas the pvdisplay command shows the details.

25\. After the pvcreate command has been executed on it successfully.

26\. lvremove /dev/vg20/webvol

27\. True.

28\. True.

29\. The pvremove command is used to remove LVM information from a
physical volume.

30\. The command provided will prepare the /dev/sdd disk for use in a
volume group.

31\. False. A disk or partition must be initialized before it can be
added to a volume group.

32\. lvcreate -l 100 -n webvol vg20

33\. False.

34\. True.

35\. The vgdisplay command with the -v option.

::: {style="page-break-before: always;"}
:::

[]{#chapter0423.html}

## Do-It-Yourself Challenge Labs

\

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the labs have already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

\

Use the lab environment built specifically for end-of-chapter labs. See
sub-section "Lab Environment for End-of-Chapter Labs" in Chapter 01
"Local Installation" for details.

\

Add more storage to server4 if required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0424.html}

## Lab 13-1: Create and Remove Partitions with parted {.style3}

\

As user1 with sudo on server4, create a 100MB primary partition on one
of the available 250MB disks (lsblk) by invoking the parted utility
directly at the command prompt. Apply label "msdos" if the disk is new.
Create another 100MB partition by running parted interactively while
ensuring that the second partition won't overlap the first. Verify the
label and the partitions. Remove both partitions at the command prompt.
(Hint: MBR Storage Management with parted).

::: {style="page-break-before: always;"}
:::

[]{#chapter0425.html}

## Lab 13-2: Create and Remove Partitions with gdisk {.style3}

\

As user1 with sudo on server4, create two 80MB partitions on one of the
250MB disks (lsblk) using the gdisk utility. Make sure the partitions
won't overlap. Verify the partitions. You may delete the partitions if
you want. (Hint: GPT Storage Management with gdisk).

::: {style="page-break-before: always;"}
:::

[]{#chapter0426.html}

## Lab 13-3: Create Volume Group and Logical Volumes {.style3}

\

As user1 with sudo on server4, initialize 1x250MB disk for use in LVM
(use lsblk to identify available disks). Create volume group vg100 with
PE size 16MB and add the physical volume. Create two logical volumes
lvol0 and swapvol of sizes 90MB and 120MB. Use the vgs, pvs, lvs, and
vgdisplay commands for verification. (Hint: Logical Volume Manager).

::: {style="page-break-before: always;"}
:::

[]{#chapter0427.html}

## Lab 13-4: Expand Volume Group and Logical Volume {.style3}

\

As user1 with sudo on server4, create a partition on an available 250MB
disk and initialize it for use in LVM (use lsblk to identify available
disks). Add the new physical volume to vg100. Expand the lvol0 logical
volume to size 300MB. Use the vgs, pvs, lvs, and vgdisplay commands for
verification. (Hint: Logical Volume Manager).

::: {style="page-break-before: always;"}
:::

[]{#chapter0428.html}

## Lab 13-5: Add a VDO Logical Volume {.style3}

\

As user1 with sudo on server4, initialize the sdf disk for use in LVM
and add it to vg100. Create a VDO logical volume named vdovol using the
entire disk capacity. Use the vgs, pvs, lvs, and vgdisplay commands for
verification. (Hint: Logical Volume Manager).

::: {style="page-break-before: always;"}
:::

[]{#chapter0429.html}

## Lab 13-6: Reduce and Remove Logical Volumes {.style3}

\

As user1 with sudo on server4, reduce the size of lvol0 logical volume
to 80MB. Then erase all three logical volumes swapvol, lvol0, and
vdovol. Confirm the deletion with vgs, pvs, lvs, and vgdisplay commands.
(Hint: Logical Volume Manager).

::: {style="page-break-before: always;"}
:::

[]{#chapter0430.html}

## Lab 13-7: Remove Volume Group and Physical Volumes {.style3}

\

As user1 with sudo on server4, remove the volume group and uninitialized
the physical volumes. Confirm the deletion with vgs, pvs, lvs, and
vgdisplay commands. Use the lsblk command and verify that the disks used
for the LVM labs no longer show LVM information. (Hint: Logical Volume
Manager).

::: {style="page-break-before: always;"}
:::

[]{#chapter0431.html}
