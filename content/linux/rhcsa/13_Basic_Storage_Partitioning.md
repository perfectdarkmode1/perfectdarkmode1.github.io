

This chapter describes the following major topics:

- Master Boot Record vs. GUID Partition Table
- Identify and understand disk partitions
- The concept of thin provisioning, and its benefits
- Create and delete partition on MBR disk
- Create and delete partition on GPT disk
- Overview of Virtual Data Optimizer and how it conserves storage
- Create and delete a Virtual Data Optimizer volume

RHCSA Objectives:

- List, create, and delete partitions on MBR and GPT disks
- Configure disk compression

Data is stored on disks that are logically divided into
partitions. 

A partition can exist on a portion of a disk, on an entire
disk, or it may span multiple disks. 

Each partition is accessed and managed independent of other partitions and may contain a file system or swap space. 

Partitioning information is stored at special disk locations
that the system references at boot time. 

RHEL offers a number of tools for partition management. 

Partitions created with a combination of most of these tools can coexist on a single disk.

Thin provisioning is a powerful feature that guarantees an efficient use of storage space by allocating only what is needed and by storing data at adjacent locations. 

Many storage management solutions incorporate thin
provisioning technology in their core configuration.

Virtual Disk Optimizer (VDO) is one of the newer storage management solutions incorporated in RHEL. 

It capitalizes on thin provisioning, de-duplication, and compression technologies to conserve storage space,
improve data throughput, and save money.

### Storage Management Overview

partition information is stored on the disk in a small region, which is read by the operating system at boot time. 

This region is referred to as the *Master Boot Record* (MBR) on the BIOS-based systems, and *GUID
Partition Table* (GPT) on the UEFI-based systems. 

At system boot, the BIOS/UEFI
- scans all storage devices,
- detects the presence of MBR/GPT areas, 
- identifies the boot disks, 
- loads the bootloader program in memory from the default boot disk, 
- executes the boot code to read the partition table and identify the */boot* partition, 
- loads the kernel in memory, and passes control over to it. 

Though MBR and GPT are designed for different PC firmware types, their job is essentially the same: to store
disk partition information and the boot code.

## Master Boot Record (MBR)

-  resides on the first sector of the boot disk. MBR 
- was the preferred choice for saving partition table information on x86-based computers. 
- However, with the arrival of bigger and larger hard drives, a newer firmware specification (UEFI) was introduced. 
- MBR is still widely used, but its use is diminishing in favor of UEFI.

MBR allows the creation of three types of partition---*primary*, *extended*, and *logical*---on a single disk. 
- primary and logical 
	- can be used for data storage;
- extended 
	- a mere enclosure for holding the logical partitions and it is not meant for data storage.
- supports the creation of up to four primary partitions numbered 1 through 4 at a time. 
- In case additional partitions are required, one of the primary partitions must be deleted and replaced with an extended partition to be able to add logical partitions (up to 11) within that extended partition. 
- Numbering for logical partitions begins at 5. 
- supports a maximum of 14 usable partitions (3 primary and 11 logical) on a single disk.
- Cannot address storage space beyond 2TB. This is due to its 32-bit nature and its 512-byte disk sector size. 
- non-redundant; the record it contains is not replicated, resulting in an unbootable system in the event of corruption. 
- If your disk is smaller than 2TB and you don't intend to build more than 14 usable partitions, you can use MBR without issues. 

## GUID Partition Table (GPT)

- *Globally Unique Identifiers* (GUID) *Partition Table* (GPT)  This new standard 
- ability to construct up to 128 partitions (no concept of extended or logical partitions), 
- utilize disks larger than 2TB, 
- use 4KB sector size,
- store a copy of the partition information before the end of the disk for redundancy.
- Allows a BIOS-based system to boot from a GPT disk using the bootloader program stored in a protective MBR at the first disk sector. In addition, the 
- UEFI firmware also supports the secure boot feature 
	- allows signed binaries to boot. 

### Disk Partitions

- Care must be taken when adding a new partition to elude data corruption with overlapping an extant partition or wasting storage by leaving unused space between adjacent partitions. 
- On *server1*, the disk that was allocated at the time of installation is recognized as *sda* (**s** for SATA, SAS, or SCSI device) **d**isk **a**, with the first partition identified as *sda1* and the second partition as *sda2*. Any subsequent disks added to the system will be known as *sdb*, *sdc*, *sdd*, and so on, and will use 1, 2, 3, *etc.* for partition numbering.

### lsblk command

- list disk and partition information. 

View the current storage status on *server1*:
`lsblk`

Output:
- reveals the presence of one 10GB disk, *sda*, with two partitions:
	- *sda1* and *sda2*. 
	- The first partition holds */boot*, and the second one is an LVM object encapsulating *root* and *swap* logical volumes within it. 
	- Both *sda1* and *sda2* partitions occupy the entire disk capacity.
- *sr0* represents the ISO image mounted as an optical medium.

### fdisk and *parted* commands
- expose disk and partitioning information. 

Run *fdisk* with -l and see what it reveals:
`fdisk -l`

output:
Top Block
- size of *sda* in GBs, bytes, and sectors
- type of disk label (dos) the disk has
- disk's geometry  
Second block 
- two disk partitions: 
	- sda1 as the bootable partition marked with *
	- sda2 as an LVM  partition. It also exposes the starting and ending sector numbers, size in 1KB blocks, and type of each partition.
- identifiers 
	- 83 and 8e are hexadecimal values for the partition types. 
last two blocks 
- Specific to the LVM logical volumes that exist within the *sda2* partition. 

### Storage Management Tools

- *parted*, gdisk, VDO, LVM, and Stratis. 
- Partitions created with a combination of most of these tools
- toolsets can coexist on the same disk. 

*parted* 
- simple tool that understands both MBR and GPT formats.

*gdisk*
- designed to support the GPT format only
- may be used as a replacement of *parted*. 

VDO
- Disk optimizer software that takes advantage of certain technologies to minimize the overall data footprint on storage devices. 

LVM
- feature-rich logical volume management solution that gives flexibility in storage management.

Stratis 
- capitalizes on thin provisioning to create volumes much larger in size than the underlying storage devices they are built upon.

### Thin Provisioning

- Allows for an economical allocation and utilization of storage space by moving arbitrary data blocks to contiguous locations, which results in empty block elimination. 
- With thin provisioning support in VDO, LVM, and Stratis, you can create a *thin pool* of storage space and assign volumes much larger storage space than the physical capacity of the pool. 
- Workloads begin consuming the actual allocated space for data writing. 
- When a preset custom threshold (80%, for instance) on the actual consumption of the physical storage in the pool is reached, expand the pool dynamically by adding more physical storage to it. 
- The volumes will automatically start exploiting the new space right away.
- helps prevent spending more money upfront.

### Adding Storage for Practice

- Need 4x250MB, 1x4GB, and 2x1GB virtual disks for storage exercises.

### Lab: Add Required Storage to server2

- add the required storage disks to *server2* using VirtualBox.
- start VirtualBox and add 4x250MB, 1x4GB, and 2x1GB disks to *server2* 

1. Start VirtualBox on your Windows/Mac computer and highlight server2

2. Click Settings at the top and then Storage on the window that
pops up. Click on "Controller: SATA" to select it. 

![](Pasted%20image%2020240413054446.png)

3. Click on the right-side icon next to "Controller: SATA" to add a hard disk.

4. Follow this sequence to add a 250MB disk: Click "Create new disk", "VDI (Virtualization Disk Image)", "Dynamically allocated", and adjust the size to 250MB. Assign the disk a unique name. 

5. Click Create to create and attach the disk to the VM.

6. Repeat steps to add the other required disks

9.  The final list of disks should look similar to what is shown

10. Power on *RHEL8-VM2* to boot RHEL 8 in it.

12. run `lsblk` command to verify the new storage:
`lsblk`


**MBR Storage Management with parted**

### parted Command (*partition editor*) 
- used to partition disks. This program 
- may be run interactively or directly from the command prompt. It
- understands and supports both MBR and GPT schemes, and 
- can be used to create up to 128 partitions on a single GPT disk. 
- subcommands for viewing, labeling, adding, naming, and deleting partitions. 

| **Subcommand** | **Description**                                                                                                                                 |
| -------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| print          | Displays the partition table that includes disk geometry and partition number, start and end, size, type, file system type, and relevant flags. |
| mklabel        | Applies a label to the disk. Common labels are gpt and msdos.                                                                                   |
| mkpart         | Makes a new partition                                                                                                                           |
| name           | Assigns a name to a partition                                                                                                                   |
| rm             | Removes the specified partition                                                                                                                 |

- use the /dev/sdb disk for these exercises.
- After making a partition, use the *print* subcommand to ensure you created what you wanted.
- /proc/partitions is also updated to reflect the results of partition management operations.

### Lab:  Create an MBR Partition

- assign partition type "msdos" to /dev/sdb for using it as an MBR disk. 
- create and confirm a 100MB primary partition on the disk.

1. Execute *parted* on /dev/sdb to view the current partition information:
`parted /dev/sdb print`

- Notice the error on line 1 of the output, indicating an unrecognized label. 
- Disk must be labeled before it can be partitioned.

2. Assign disk label "msdos" to the disk with mklabel. (performed only once on a disk.)
`parted /dev/sdb mklabel msdos`

The *print* subcommand confirms the successful application of the label.
`parted /dev/sdb print`

To use the GPT partition table type, run `parted /dev/sdb mklabel gpt` instead.

3. Create a 100MB primary partition starting at 1MB (beginning of the disk) using mkpart:
`parted /dev/sdb mkpart primary 1 101m`

4. Verify the new partition with *print*:
`parted /dev/sdb print`

- Partition numbering begins at 1 by default.

5. Confirm the new partition with the `lsblk` command:
`lsblk /dev/sdb`

- Different tools will have variance in reporting partition sizes. Ignore minor differences.

6. Check /proc/partitions also:
`cat /proc/partitions | grep sdb`

- The virtual file is also updated with the new partition information.


### Lab: Delete an MBR Partition

- Delete the *sdb1* partition and confirm the deletion.

1. Execute *parted* on /dev/sdb with the `rm` subcommand to remove partition number 1:
`parted /dev/sdb rm 1`

2. Confirm the partition deletion with *print*:
`parted /dev/sdb print`

3. Check /proc/partitions:
`cat /proc/partitions | grep sdb`

- The virtual file has the partition entry deleted as well. 
- can also run the `lsblk` command for further verification.
- Knowing either parted or gdisk for the exam is enough.

### GPT Storage Management with gdisk

#### gdisk (GPT disk) command 
- partitions disks using the GPT format.  
- text-based, menu-driven program 
- show, add, verify, modify, and delete partitions among other operations. 
- can create up to 128 partitions on a single disk on systems with UEFI firmware.

- Specify a disk device name such as /dev/sdc/ with the command. 
- Type *help* or *?* at the prompt to view available subcommands.

`gdisk /dev/sdc`

### Lab: Create a GPT Partition

- assign partition type "gpt" to /dev/sdc for using it as a GPT disk. 
- create and confirm a 200MB partition on the disk.

1. Execute *gdisk* on /dev/sdc/ to view the current partition information:
`gdisk /dev/sdc`

2. Assign "gpt" as the partition table type to the disk using the o subcommand. Enter "y" for confirmation to proceed. This operation is
performed only once on a disk.

3. Run the *p* subcommand to view disk information and confirm the GUID partition table creation:

4. Create the first partition of size 200MB starting at the default sector with default type "Linux filesystem" using the *n* subcommand:
```
Command (? for help): n
Partition number (1-128, default 1): 
First sector (34-511966, default = 2048) or {+-}size{KMGTP}: 
Last sector (2048-511966, default = 511966) or {+-}size{KMGTP}: +200M
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): 
Changed type of partition to 'Linux filesystem'
```

5. Verify the new partition with *p*:

6. Run *w* to write the partition information to the partition table and exit out of the interface. Enter "y" to confirm when prompted.

- You may need to run the partprobe command after exiting the gdisk utility to update the kernel of the changes.
`partprobe`

7. Verify the new partition by issuing either of the following at the command prompt:
`grep sdc /proc/partitions`
`lsblk /dev/sdc`

### Lab: Delete a GPT Partition

In this exercise, you will delete the *sdc1* partition that was created in [Exercise 13-4](#part0025_split_001.html#id_366){.calibre5} and confirm the removal.

1. Execute *gdisk* on /dev/sdc/ and run `d1` at the utility's prompt to delete partition number 1:
`gdisk /dev/sdc`
`d1`

2. Confirm the partition deletion with *p*:

3. Write the updated partition information to the disk with `w` and quit *gdisk*:

4. Verify the partition deletion by issuing either of the following at the command prompt:
`grep sdc /proc/partitions`
`lsblk /dev/sdc`


## Storage Optimization with Virtual Data Optimizer (VDO)

VDO
- device driver layer that sits between the operating system kernel and the physical storage devices. 
- conserve disk space
- improve data throughput
- save on storage cost. 
- employs thin provisioning, de-duplication, and compression technologies 
- runs in the background and processes inbound data through the three stages on VDO-enabled volumes. 
- not a CPU-or memory-intensive process; it consumes a low amount of system resources.

### How VDO Conserves Storage Space

thin provisioning (Stage 1)
- identify and eliminate empty (zero-byte) data blocks. (zero-block elimination). 
- removes randomization of data blocks by moving in-use data blocks to contiguous locations on the storage device.

de-duplication (Stage 2)
- If VDO detects that new data is an identical copy of some existing data, it makes an internal note of it but does not actually write the redundant data to the disk. 
-  implemented in RHEL with the inclusion of a kernel module called *UDS* (*Universal Deduplication Service*). T

kvdo (Stage 3)
- kernel module
- compresses the residual data blocks and consolidates them on a lower number of blocks.
- results in a further drop in storage space utilization.

**Creating and Managing VDO Volumes**

- VDO volumes can be initialized for use just like disk partitions, or they can be used as LVM physical volumes.

*vdo* and *vdostats* commands
VDO offers a set of commands to create, manage, and monitor volumes. Of
these  are discussed and used in this
section. The *vdo* command is used to create and perform essential
operations on VDO volumes, and the *vdostats* command is employed to
monitor usage statistics of the underlying physical storage device.

[Table 13-2](#part0025_split_001.html#id_740){.calibre5} summarizes the
subcommands available with *vdo*.

::: c49
  ---------------- -----------------------------------------------------
  **Subcommand**   **Description**
  create           Adds a new VDO volume on the specified block device
  status           Returns the status and attributes of VDO volumes
  list             Lists the names of all started VDO volumes
  start            Starts a VDO volume
  stop             Stops a VDO volume
  ---------------- -----------------------------------------------------

**[Table]{#part0025_split_001.html#id_740} 13-2 vdo Subcommands**
:::

The *vdostats* command has a couple of interesting options that you will
use shortly.

**[Exercise]{#part0025_split_001.html#id_370 .calibre10} 13-6: Install
Software and Activate VDO**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will install the VDO software packages, start the
VDO service, and mark it for autostart on subsequent system reboots.

1[.]{.c19}Install packages *vdo* and *kmod-kvdo*:

![](images/00680.jpeg){.image2}

2[.]{.c19}Start the service and enable it to start automatically on
future system reboots:

![](images/00681.jpeg){.image2}

3[.]{.c19}Check the operational status of the service:

![](images/00682.jpeg){.image2}

The relevant packages for VDO are installed, and the VDO service is
started and activated. This concludes the exercise.

**Exercise 13-7: Create a VDO Volume**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create a volume called *vdo-vol1* of logical
size 16GB on **dev*sdf* disk (the actual size of **dev*sdf* is 4GB). You
will list the volume and display its status information. You will also
show the activation status of the compression and de-duplication
features.

1[.]{.c19}Create a volume called *vdo-vol1* (\--name) on the **dev*sdf*
device (\--device) with a logical size of 16GB (\--vdoLogicalSize) and
slab size of 128MB (\--vdoSlabSize):

![](images/00683.jpeg){.image2}

![](images/00002.jpeg){.image} Increase the amount of memory allocated
to the virtual machine to 2GB if the output complains about insufficient
memory.

![](images/00002.jpeg){.image} If the logical size is not specified, the
VDO volume will have the same size as the underlying disk (*dev*sdf in
this case).

![](images/00002.jpeg){.image} The slab size is the size of the
increment by which VDO volumes grow. This value must be a power of two
between 128MB and 32GB; the default is 2GB. The default unit of size
specification is MB.

2[.]{.c19}List the new volume using the *vdo* and *lsblk* commands:

![](images/00684.jpeg){.image2}

As indicated, the major number for the VDO volume is 253, which is
associated with the device mapper kernel driver. The output also shows
the logical volume size (16GB) and type (vdo). It also depicts the disk
(*sdf*) that houses the volume, along with its actual size (4GB).

3[.]{.c19}Display the usage status of the volume:

![](images/00685.jpeg){.image2}

The size of the actual disk is 4GB. Due to thin provisioning, the system
allowed you to create the VDO volume much larger in size (4 times) than
the physical disk capacity.

4[.]{.c19}Show detailed statistics for the volume including
configuration information:

![](images/00686.jpeg){.image2}

The output will expose over one hundred different settings for the
volume.

5[.]{.c19}Display detailed statistics for the volume including
configuration information:

![](images/00687.jpeg){.image2}

The status includes volume, kernel module, and configuration
information. It also provides a detailed look at volume-specific
elements.

6[.]{.c19}Show the activation status of the compression and
de-duplication features:

![](images/00688.jpeg){.image2}

Both compression and de-duplication features are activated by default on
new VDO volumes. This concludes the exercise.

**Exercise 13-8: Delete a VDO Volume**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will delete the *vdo-vol1* volume that was created
in [Exercise 13-7](#part0025_split_000.html#page_316){.calibre5} and
confirm the removal.

1[.]{.c19}Verify that the volume still exists with the *vdo* and *lsblk*
commands:

![](images/00689.jpeg){.image2}

2[.]{.c19}Specify the name (\--name) of the volume with the *vdo*
command to delete:

![](images/00690.jpeg){.image2}

3[.]{.c19}Confirm the removal with the *vdo* and *lsblk* commands:

![](images/00691.jpeg){.image2}

The volume has been deleted successfully as reported in the above
outputs.

[**EXAM TIP:**]{.c56} Make sure that you run the lsblk command before
attempting any storage task. The VDO task is usually performed on the
biggest sized available disk.

You will recreate VDO volumes in [Chapter
15](#part0027_split_000.html#page_345){.calibre5} "Local File Systems
and Swap" for use as file systems and swap areas.

**[Chapter]{#part0025_split_001.html#id_371 .calibre10} Summary**

This chapter started with an overview of how and where disk partitioning
information is stored. It presented a comparison between the two common
schemes and explained which one to use and in which situation. A little
later, we touched briefly on the common storage management solutions
available in RHEL.

We examined the concept of thin provisioning and realized the benefits
associated with this technology.

Next, we carved up available disk devices using both MBR and GPT
partitioning schemes. We demonstrated the partition creation, display,
and delete operations by running one command directly at the command
prompt and launching the other in interactive mode.

The last topic of the chapter focused on a storage management solution
that was introduced in RHEL not too long ago. This solution exploits the
underlying thin provisioning, de-duplication, and compression
technologies to save cost, ensure efficient use of storage space, and
improve data throughput. We performed a couple of exercises in the end
to demonstrate the creation and deletion of volumes using this solution.

**[Review]{#part0025_split_001.html#id_372 .calibre10} Questions**

1[.]{.c19}What is missing in the command *vdo create \--name vdo1
\--vdoLogicalSize 16GB \--vdoSlabSize 128MB*?
1[.]{.c19}The storage device (\--device) name is missing from the
command provided.

2[.]{.c19}What is the maximum number of usable partitions that can be
created on a GPT disk?

3[.]{.c19}Which kernel module is responsible for data block compression
in VDO volumes?

4[.]{.c19}What are the three techniques VDO volumes employ for storage
conservation?

5[.]{.c19}What would the command *parted *dev*sdc mkpart pri 1 200m* do?

6[.]{.c19}Where is the partition table information stored on BIOS-based
systems?

7[.]{.c19}What is the name of the technology that VDO employs to remove
randomization of data blocks?

8[.]{.c19}What would *sdd3* represent?

9[.]{.c19}Which command can be used to view the usage statistics of VDO
volumes?

10[.]{.c23}Thin provisioning technology allows us to create logical
volumes of sizes larger than the actual physical storage size. True or
False?

11[.]{.c23}You have an unused VDO volume called *vdo1* on **dev*sdf*
disk and you try to delete it. You run *vdo remove \--device *dev*sdf*,
but the removal fails. What are you doing wrong?

12[.]{.c23}What is the maximum number of usable partitions that can be
created on an MBR disk?

13[.]{.c23}What would the command *systemctl \--now enable vdo* do?

14[.]{.c23}The *gdisk* utility can be used to store partition
information in MBR format. True or False?

15[.]{.c23}What would the command *parted *dev*sdd mklabel msdos* do?

16[.]{.c23}VDO is a memory-intensive storage optimization solution and
should not be used. True or False?

17[.]{.c23}Which file in the */proc* file system stores the in-memory
partitioning information?

18[.]{.c23}You have created a VDO volume and you want to check whether
compression is enabled. Which command would you use?

19[.]{.c23}Deduplication is the process of zero-block elimination. True
or False?

**[Answers]{#part0025_split_001.html#id_373 .calibre10} to Review
Questions**



2[.]{.c19}128.

3[.]{.c19}The *kvdo* module is responsible for compressing data blocks
in VDO volumes.

4[.]{.c19}VDO volumes use thin provisioning, de-duplication, and
compression techniques for storage conservation.

5[.]{.c19}The command provided will create a primary partition of size
200MB on the *sdc* disk starting at the beginning of the disk.

6[.]{.c19}The partition table information is stored on the Master Boot
Record.

7[.]{.c19}VDO employs thin provisioning technology to remove data block
randomization.

8[.]{.c19}*sdd3* represents the third partition on the fourth disk.

9[.]{.c19}The *vdostats* command can be used to view VDO volume usage
statistics.

10[.]{.c23}True.

11[.]{.c23}The correct command would be *vdo remove \--name vdo1*.

12[.]{.c23}14.

13[.]{.c23}The command provided will start the VDO service and enable it
to autostart on system reboots.

14[.]{.c23}False. The *gdisk* tool is only for GPT type tables.

15[.]{.c23}The command provided will apply msdos label to the *sdd*
disk.

16[.]{.c23}False. VDO uses low memory and other compute resources.

17[.]{.c23}The *partitions* file.

18[.]{.c23}You can issue the *vdo status* command and pipe the output to
*grep* for the pattern "compression".

19[.]{.c23}False. Deduplication is the process of removing blocks of
identical data.

**[Do-]{#part0025_split_001.html#id_374 .calibre10}It-Yourself Challenge
Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

Add more storage to *server2* if required.

**[Lab]{#part0025_split_001.html#id_375 .calibre10} 13-1: Create and
Remove Partitions with parted**

As *user1* with *sudo* on *server2*, create a 100MB primary partition on
one of the available 250MB disks (*lsblk*) by invoking the *parted*
utility directly at the command prompt. Apply label "msdos" if the disk
is new. Create another 100MB partition by running *parted* interactively
while ensuring that the second partition won't overlap the first. Verify
the label and the partitions. Remove both partitions from the command
prompt. (Hint: MBR Storage Management with parted).

**[Lab]{#part0025_split_001.html#id_376 .calibre10} 13-2: Create and
Remove Partitions with gdisk**

As *user1* with *sudo* on *server2*, create two 80MB partitions on one
of the 250MB disks (*lsblk*) using the *gdisk* utility. Make sure the
partitions won't overlap. Verify the partitions. You may delete the
partitions if you want. (Hint: GPT Storage Management with gdisk).

**[Lab]{#part0025_split_001.html#id_377 .calibre10} 13-3: Create and
Delete VDO Volumes**

As *user1* with *sudo* on *server2*, check to see if VDO software is
installed and the VDO service is enabled and started. Identify the 4GB
disk with the *lsblk* command, and make sure that it is not in use.
Create a volume *testvdo* with a logical size 16GB on the 4GB disk using
the *vdo* command. Select an appropriate slab size for the volume.
Verify the volume creation with the *vdo*, *lsblk*, and *vdostats*
commands. (Hint: Storage Optimization with Virtual Data Optimizer).

**[Lab]{#part0025_split_001.html#id_378 .calibre10} 13-4: Disable and
Enable VDO Volume Features**

As *user1* with *sudo* on *server2*, use the *vdostats* command to check
whether compression and de-duplication are enabled for the volume
created in Lab 13-3. Use the *vdo* command with disableCompression and
disableDeduplication subcommands to disable compression and
de-duplication, and verify with *vdostats*. Reactivate both features and
confirm activation. You may delete the volume if you want. (Hint:
Storage Optimization with Virtual Data Optimizer).

[]{#part0026_split_000.html}
