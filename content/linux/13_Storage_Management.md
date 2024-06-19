
Identify and understand disk partitions

The concept of thin provisioning, and its benefits

Create and delete partition on MBR disk

Create and delete partition on GPT disk

Describe Logical Volume Manager and its components

Understand various Logical Volume Manager management operations

Know Logical Volume Manager administration commands

Overview of Virtual Data Optimizer and how it conserves storage

Create and confirm physical volumes, volume groups, LVM logical volumes, and VDO logical volumes

Rename, reduce, extend, and remove logical volumes

Extend, reduce, and remove volume groups

Remove physical volumes

#### RHCSA Objectives:

26\. List, create, and delete partitions on MBR and GPT disks

27\. Create and remove physical volumes

28\. Assign physical volumes to volume groups

29\. Create and delete logical volumes

31\. Add new partitions and logical volumes, and swap to a system
nondestructively (the swap portion of this objective is covered in
Chapter 14 )

35\. Extend existing logical volumes (additional coverage on this
objective is available in Chapter 14 )


- Data is stored on disks that are logically divided into partitions. 
- A partition can exist on a portion of a disk, on an entire disk, or it may span multiple disks. 
Each partition is accessed and managed independent of other partitions and may contain a file system or swap space.
Partitioning information is stored at special disk locations that the system references at boot time. 
Partitions created with a combination of most tools can coexist on a single disk.

Thin provisioning is a powerful feature that guarantees an efficient use of storage space by allocating only what is needed and by storing data at adjacent locations. 
Many storage management solutions incorporate thin provisioning technology in their core configuration.

Virtual Data Optimizer capitalizes on thin provisioning, de-duplication, and compression technologies to conserve storage space, improve data throughput, and save money.


The Logical Volume Manager solution sets up an abstraction layer between the operating system and the storage hardware. 
It utilizes virtual objects for storage pooling and allocation, and offers a slew of
commands to carry out management operations.


## Storage Management Overview


Partition information is stored on the disk in a small region, which is read by the operating system at boot time. 
This region is referred to as the Master Boot Record (MBR) on the BIOS-based systems, and GUID Partition Table (GPT) on the UEFI-based systems. 
At system boot, the BIOS/UEFI scans all storage devices, detects the presence of MBR/GPT areas, identifies the boot disks, loads the bootloader program in memory from the default boot disk, executes the boot code to read the partition table and identify the /boot partition, loads the kernel in memory, and passes control over to it. 
Though MBR and GPT store disk partition information and the boot code.


## Master Boot Record (MBR) 


resides on the first sector of the boot disk. 
was the preferred choice for saving partition table information on x86-based
computers.
with the arrival of bigger and larger hard drives, a new firmware specification (UEFI) was introduced. 
still widely used, but its use is diminishing in favor of UEFI.


allows the creation of three types of partition on a single disk.
primary, extended, and logical--- 
only primary and logical can be used for data storage
extended is a mere enclosure for holding the logical partitions and it is not meant for data storage. 
supports the creation of up to four primary partitions numbered 1 through 4 at a time. 
In case additional partitions are required, one of the primary partitions must be deleted and replaced with an extended
partition to be able to add logical partitions (up to 11) within that extended partition. 
Numbering for logical partitions begins at 5. 
supports a maximum of 14 usable partitions (3 primary and 11 logical) on a single disk.

Cannot address storage space beyond 2TB ue to its 32-bit nature and its 512-byte disk sector size. 
non-redundant; the record it contains is not replicated, resulting in an unbootable system in the event of corruption. 
If your disk is smaller than 2TB and you don't intend to build more than 14 usable partitions, you can use MBR
without issues. 

## GUID Partition Table (GPT) 


ability to construct up to 128 partitions (no concept of extended or logical partitions)
utilize disks larger than 2TB
use 4KB sector size
store a copy of the partition information before the end of the disk for redundancy


allows a BIOS-based system to boot from a GPT disk using the bootloader program stored in a protective MBR at the first disk sector
UEFI firmware also supports the secure boot feature, which only allows signed binaries to boot

## Disk Partitions 

Care must be taken when adding a new partition to elude data corruption with overlapping an extant partition or wasting storage by leaving unused space between adjacent partitions. 

disk allocated at the time of installation is recognized as sda (s for SATA, SAS, or SCSI device) disk a, 
first partition identified as sda1 and the second partition as sda2. 
Any subsequent disks added to the system will be known as sdb, sdc, sdd, and so on, and will use 1, 2, 3,
etc. for partition numbering.

RHEL offers a command called `lsblk` to list disk and partition information. 

```bash
[root@server1 ~]# lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0   10G  0 disk 
├─sda1          8:1    0    1G  0 part /boot
└─sda2          8:2    0    9G  0 part 
  ├─rhel-root 253:0    0    8G  0 lvm  /
  └─rhel-swap 253:1    0    1G  0 lvm  [SWAP]
sr0            11:0    1  9.8G  0 rom  /mnt
```

sr0 represents the ISO image mounted as an optical medium

```bash
[root@server1 ~]# sudo fdisk -l
Disk /dev/sda: 10 GiB, 10737418240 bytes, 20971520 sectors
Disk model: VBOX HARDDISK   
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xfc8b3804

Device     Boot   Start      End  Sectors Size Id Type
/dev/sda1  *       2048  2099199  2097152   1G 83 Linux
/dev/sda2       2099200 20971519 18872320   9G 8e Linux LVM


Disk /dev/mapper/rhel-root: 8 GiB, 8585740288 bytes, 16769024 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/mapper/rhel-swap: 1 GiB, 1073741824 bytes, 2097152 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

identifiers 83 and 8e are hexadecimal values for the partition types

## Storage Management Tools 


parted, gdisk, and LVM
Partitions created with a combination of most of these tools and toolsets can coexist on the same disk.

parted 
understands both MBR and GPT formats. 

gdisk
idesigned to support the GPT format only
may be used as a replacement of parted. 

LVM
feature-rich logical volume management solution that gives flexibility in storage management.

## Thin Provisioning

allows for an economical allocation and utilization of storage space by moving arbitrary data blocks to contiguous locations, which results in empty block elimination. 
can create a thin pool of storage space and assign volumes much larger storage space than the physical capacity of the pool. 
Workloads begin consuming the actual allocated space for data writing. 
When a preset custom threshold (80%, for instance) on the actual consumption of the physical storage in the pool is reached, expand the pool dynamically by adding more physical storage to it. 
The volumes will automatically start exploiting the new space right away. 
helps prevent spending more money upfront.

## Adding Storage for Practice


## Exercise 13-1: Add Required Storage to server2


In this exercise, you will start VirtualBox and add 4x250MB and 1x5GB
disks to server2 in preparation for exercises in this and the next
chapter.


1\. Start VirtualBox on your Windows/Mac computer and highlight the RHEL9-VM2 virtual machine that you created in Lab 1-1. See Figure 13-1.


![](image-KEGS1BT1.jpg)

2\. Click Settings at the top and then Storage on the window that pops
up. Click on "Controller: SATA" to select it. Figure 13-2.

![](image-KWA12KXW.jpg)


3\. Click on the right-side icon next to "Controller: SATA" to add a hard disk and then click Create (on the Medium Selector screen)
![](image-Q6NZNE81.jpg)

4\. Follow this sequence to add a 250MB disk: Click Next on the next two screens to select the two defaults for the "VDI (Virtualization Disk Image)" and "Dynamically allocated" options. Adjust the size on the third screen to 250MB. 

![](image-DPO9QA8O.jpg)

5\. Repeat step 4 three more times to create additional disks of the
same size.

6\. Repeat step 4 one time to create a disk of size 5GB.

7\. On the Medium Selector screen, the five new disks will appear under the Not Attached list of disks. Double-click on each one of them to add to RHEL9-VM2.


![](image-I02OKCQR.jpg)

8\. The final list of disks should look similar to what is shown in Figure 13-6 after the addition of all five disks (RHEL9-VM2_1 to
RHEL9-VM2_5). Disk names may vary.

![](image-38AAB6BK.jpg)

9\. Click OK to return to the main VirtualBox interface.

10\. Power on RHEL9-VM2.

11\. When the server is booted up, log on as user1 and run the lsblk command to verify the new storage:

12\. The five new disks added to server2 are 250MB (sdb, sdc, sdd, and sde) and 5GB (sdf).

## MBR Storage Management with parted


parted (partition editor) 
- can be used to partition disks
- run interactively or directly from the command prompt.
- understands and supports both MBR and GPT schemes
- can be used to create up to 128 partitions on a single GPT disk
- viewing, labeling, adding, naming, and deleting partitions. 


  Subcommand                          Description

  print                               Displays the partition table that includes disk geometry and partition number, start and end, size, type, file system type, and relevant flags.

  mklabel                             Applies a label to the disk. Common labels are gpt and msdos.

  mkpart                              Makes a new partition

  name                                Assigns a name to a partition

  rm                                  Removes the specified partition

use the print subcommand to ensure you created what you wanted. 
/proc/partitions file is also updated to reflect the results of partition management operations.

## Exercise 13-2: Create an MBR Partition (server2)

assign partition type "msdos" to /dev/sdb for using it as an MBR disk
create and confirm a 100MB primary partition on the disk.

1\. Execute parted on /dev/sdb to view the current partition information:
```bash
[root@server2 ~]# sudo parted /dev/sdb print
Error: /dev/sdb: unrecognised disk label
Model: ATA VBOX HARDDISK (scsi)                                           
Disk /dev/sdb: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: unknown
Disk Flags: 
```


There is an error on line 1 of the output, indicating an unrecognized label. 
disk must be labeled before it can be partitioned.

2\. Assign disk label "msdos" to the disk with mklabel. This operation
is performed only once on a disk.

```bash
[root@server2 ~]# sudo parted /dev/sdb mklabel msdos
Information: You may need to update /etc/fstab.
```

```bash
[root@server2 ~]# sudo parted /dev/sdb print                              
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start  End  Size  Type  File system  Flags

```

To use the GPT partition table type, run "sudo parted /dev/sdb mklabel gpt" instead.


3\. Create a 100MB primary partition starting at 1MB (beginning of the disk) using mkpart:
```bash
[root@server2 ~]# sudo parted /dev/sdb mkpart primary 1 101m
Information: You may need to update /etc/fstab.
```

4\. Verify the new partition with print:
```bash
[root@server2 ~]# sudo parted /dev/sdb print                              
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End    Size    Type     File system  Flags
 1      1049kB  101MB  99.6MB  primary
 ```

Partition numbering begins at 1 by default.

5\. Confirm the new partition with the lsblk command:
```bash
[root@server2 ~]# lsblk /dev/sdb
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sdb      8:16   0  250M  0 disk 
└─sdb1   8:17   0   95M  0 part 
```


The device file for the first partition on the sdb disk is sdb1 as identified on the bottom line. 
The partition size is 95MB.

Different tools will have variance in reporting partition sizes. 
ignore minor differences.

6\. Check the /proc/partitions file also:
```bash
[root@server2 ~]# cat /proc/partitions | grep sdb
   8       16     256000 sdb
   8       17      97280 sdb1
```


## Exercise 13-3: Delete an MBR Partition (server2)

delete the sdb1 partition that was created in Exercise 13-2
confirm the deletion.

1\. Execute parted on /dev/sdb with the rm subcommand to remove partition number 1:
```bash
[root@server2 ~]# sudo parted /dev/sdb rm 1
Information: You may need to update /etc/fstab.
```

2\. Confirm the partition deletion with print:
```bash
[root@server2 ~]# sudo parted /dev/sdb print                              
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start  End  Size  Type  File system  Flags
```


3\. Check the /proc/partitions file:
```bash
[root@server2 ~]# cat /proc/partitions | grep sdb
   8       16     256000 sdb
```

can also run the lsblk command for further verification. T

EXAM TIP: Knowing either parted or gdisk for the exam is enough.


## GPT Storage Management with gdisk

gdisk (GPT disk)
partitions disks using the GPT format. 
text-based, menu-driven program
show, add, verify, modify, and delete partitions
can create up to 128 partitions on a single disk on systems with UEFI firmware.

The main interface of gdisk can be invoked by specifying a disk device name such as /dev/sdc with the command. 
Type help or ? (question mark) at the prompt to view available subcommands.

```bash
[root@server2 ~]# sudo gdisk /dev/sdc
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries in memory.

Command (? for help): ?
b	back up GPT data to a file
c	change a partition's name
d	delete a partition
i	show detailed information on a partition
l	list known partition types
n	add a new partition
o	create a new empty GUID partition table (GPT)
p	print the partition table
q	quit without saving changes
r	recovery and transformation options (experts only)
s	sort partitions
t	change a partition's type code
v	verify disk
w	write table to disk and exit
x	extra functionality (experts only)
?	print this menu

Command (? for help): 
```

## Exercise 13-4: Create a GPT Partition (server2)

assign partition type "gpt" to /dev/sdc for using it as a GPT disk.
create and confirm a 200MB partition on the disk.

1\. Execute gdisk on /dev/sdc to view the current partition information:
```bash
[root@server2 ~]# sudo gdisk /dev/sdc
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
  MBR: not present
  BSD: not present
  APM: not present
  GPT: not present

Creating new GPT entries in memory.

Command (? for help):
```

The disk currently does not have any partition table on it.

2\. Assign "gpt" as the partition table type to the disk using the o subcommand. Enter "y" for confirmation to proceed. This operation is
performed only once on a disk.
```bash
Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): y
```


3\. Run the p subcommand to view disk information and confirm the GUID
partition table creation:
```bash
Command (? for help): p
Disk /dev/sdc: 512000 sectors, 250.0 MiB
Model: VBOX HARDDISK   
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 9446222A-28AC-4F96-816F-518510F95019
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 511966
Partitions will be aligned on 2048-sector boundaries
Total free space is 511933 sectors (250.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
```


The output returns the assigned GUID and states that the partition table can hold up to 128 partition entries.


4\. Create the first partition of size 200MB starting at the default
sector with default type "Linux filesystem" using the n subcommand:
```bash
Command (? for help): n
Partition number (1-128, default 1): 
First sector (34-511966, default = 2048) or {+-}size{KMGTP}: 
Last sector (2048-511966, default = 511966) or {+-}size{KMGTP}: +200M
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): 
Changed type of partition to 'Linux filesystem'
```


5\. Verify the new partition with p:
```bash
Command (? for help): p
Disk /dev/sdc: 512000 sectors, 250.0 MiB
Model: VBOX HARDDISK   
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 9446222A-28AC-4F96-816F-518510F95019
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 511966
Partitions will be aligned on 2048-sector boundaries
Total free space is 102333 sectors (50.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048          411647   200.0 MiB   8300  Linux filesystem
```


6\. Run w to write the partition information to the partition table and exit out of the interface. Enter "y" to confirm when prompted.
```bash
Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdc.
The operation has completed successfully.

```

You may need to run the partprobe command after exiting the gdisk utility to inform the kernel of partition table changes.

7\. Verify the new partition by issuing either of the following at the command prompt:
```bash
[root@server2 ~]# grep sdc /proc/partitions
   8       32     256000 sdc
   8       33     204800 sdc1
   
[root@server2 ~]# lsblk /dev/sdc
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sdc      8:32   0  250M  0 disk 
└─sdc1   8:33   0  200M  0 part 
```


## Exercise 13-5: Delete a GPT Partition(server2)

delete the sdc1 partition that was created in Exercise 13-4 and confirm the removal.

1\. Execute gdisk on /dev/sdc and run d1 at the utility's prompt to delete partition number 1:
```bash
[root@server2 ~]# gdisk /dev/sdc
GPT fdisk (gdisk) version 1.0.7

Partition table scan:
  MBR: protective
  BSD: not present
  APM: not present
  GPT: present

Found valid GPT with protective MBR; using GPT.

Command (? for help): d1
Using 1
```

2\. Confirm the partition deletion with p:
```bash
Command (? for help): p
Disk /dev/sdc: 512000 sectors, 250.0 MiB
Model: VBOX HARDDISK   
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 9446222A-28AC-4F96-816F-518510F95019
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 511966
Partitions will be aligned on 2048-sector boundaries
Total free space is 511933 sectors (250.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
```

3\. Write the updated partition information to the disk with w and quit gdisk:
```bash
Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdc.
The operation has completed successfully.
```

4\. Verify the partition deletion by issuing either of the following at
the command prompt:
```bash
[root@server2 ~]# grep sdc /proc/partitions
   8       32     256000 sdc
[root@server2 ~]# lsblk /dev/sdc
NAME MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sdc    8:32   0  250M  0 disk 
```

## Logical Volume Manager (LVM)

used for managing block storage in Linux. 
provides an abstraction layer between the physical storage and the file system
enables the file system to be resized, span across multiple disks, use arbitrary disk space, etc. 
accumulates spaces taken from partitions or entire disks (called Physical Volumes) to form a logical container (called Volume Group) which is then divided into logical partitions (called Logical Volumes).
online resizing of volume groups and logical volumes, 
online data migration between logical volumes and between physical volumes
user-defined naming for volume groups and logical volumes
mirroring and striping across multiple disks
snapshotting of logical volumes. 

![](image-0A8W8M1U.jpg){

the LVM structure is made up of three key objects called physical volume, volume group, and logical volume. 
These objects are further virtually broken down into Physical Extents (PEs) and Logical Extents (LEs). 

## Physical Volume(PV)

created when a block storage device such as a partition or an entire disk is initialized and brought under LVM
control. This process constructs LVM data structures on the device, including a label on the second sector and metadata shortly thereafter.

The label includes the UUID, size, and pointers to the locations of data and metadata areas. Given the criticality of metadata, LVM stores a copy of it at the end of the physical volume as well. The rest of the device space is available for use.

You can use an LVM command called pvs (physical volume scan or summary) to scan and list available physical volumes on server2:
```bash
[root@server2 ~]# sudo pvs
  PV         VG   Fmt  Attr PSize   PFree
  /dev/sda2  rhel lvm2 a--  <19.00g    0
```

(a for allocatable under Attr)


Try running this command again with the -v flag to view more information
about the physical volume.

## Volume Group

A Volume Group (VG) is created when at least one physical volume is added to it. 
The space from all physical volumes in a volume group is aggregated to form one large pool of storage, which is then used to
build logical volumes. 
The physical volumes added to a volume group may be of varying sizes. 
LVM writes volume group metadata on each physical volume that is added to it. 
The volume group metadata contains its name,date and time of creation, how it was created, the extent size used, a list of physical and logical volumes, a mapping of physical and logical extents, etc. 
A volume group can have a custom name assigned to it at the time of its creation. 
A copy of the volume group metadata is stored and maintained at two distinct locations on each physical volume within the volume group.

You can use an LVM command called vgs (volume group scan or summary) to scan and list available volume groups on server2:
```bash
[root@server2 ~]# sudo vgs
  VG   #PV #LV #SN Attr   VSize   VFree
  rhel   1   2   0 wz--n- <19.00g    0
```

status of the volume group under the Attr column (w for writeable, z for resizable, and n for normal), 

Try running this command again with the -v flag to view more information
about the volume group.

## Physical Extent

A physical volume is divided into several smaller logical pieces when it is added to a volume group. These logical pieces are known as Physical Extents (PE). An extent is the smallest allocatable unit of space in LVM. 
At the time of volume group creation, you can either define the size of the PE or leave it to the default value of 4MB. 
This implies that a 20GB physical volume would have approximately 5,000 PEs. 
Any physical volumes added to this volume group thereafter will use the same PE size.

You can use an LVM command called vgdisplay (volume group display) on server2 and grep for 'PE Size' to view the PE size used in the rhel volume group:
```bash
[root@server2 ~]# sudo vgdisplay rhel | grep 'PE Size'
  PE Size               4.00 MiB
```

## Logical Volume

A volume group consists of a pool of storage taken from one or more physical volumes. 
This volume group space is used to create one or more Logical Volumes (LVs). 
A logical volume can be created or weeded out online, expanded or shrunk online, and can use space taken from one or
multiple physical volumes inside the volume group.

The default naming convention used for logical volumes is lvol0, lvol1,
lvol2, and so on
you may assign custom names to them. 

You can use an LVM command called lvs (logical volume scan or summary) to scan and list available logical volumes on server2:
```bash
[root@server2 ~]# sudo lvs
  LV   VG   Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rhel -wi-ao---- <17.00g                                                    
  swap rhel -wi-ao----   2.00g
```

Attr column (w for writeable, i for inherited allocation policy, a for active, and o for open) and their sizes.

Try running this command again with the -v flag to view more information about the logical volumes.

## Logical Extent

A logical volume is made up of Logical Extents (LE). 
Logical extents point to physical extents, and they may be random or contiguous. 
The larger a logical volume is, the more logical extents it will have.
Logical extents are a set of physical extents allocated to a logical volume.

The LE size is always the same as the PE size in a volume group. 
The default LE size is 4MB, which corresponds to the default PE size of 4MB.

You can use an LVM command called `lvdisplay` (logical volume display) on server2 to view information about the root logical volume in the rhel volume group. 

![](image-E8W3BEYL.jpg)

```bash
david@fedora:~/Documents/perfectdarkmode/perfectdarkmode1.github.io$ sudo lvdisplay /dev/rhel/root
Place your right index finger on the fingerprint reader
  Volume group "rhel" not found
  Cannot process volume group rhel
```

The output does not disclose the LE size; 
however, you can convert theLV size in MBs (17,000) and then divide the result by the Current LE
count (4,351) to get the LE size (which comes close to 4MB).

## LVM Operations and Commands

creating and removing a physical volume, volume group, and logical volume
extending and reducing a volume group and logical volume
renaming a volume group and logical volume
listing and displaying physical volume, volume group, and logical volume
information.

### Create and Remove Operations        

**pvcreate/pvremove**                   
  Initializes/uninitializes a disk or partition for LVM use

**vgcreate/vgremove**                  
  Creates/removes a volume group

**lvcreate/lvremove**                   
  Creates/removes a logical volume
  

### Extend and Reduce Operations        

**vgextend/vgreduce**                   
  Adds/removes a physical volume to/from a volume group

**lvextend/lvreduce**                   
  Extends/reduces the size of a logical volume

**lvresize**                            
  Resizes a logical volume. With the -r option, this command calls the fsadm command to resize the underlying file system as well.


### Rename Operations                   

**vgrename**                            
  Renames a volume group

**lvrename**                            
  Renames a logical volume
  

### List and Display Operations         

**pvs/pvdisplay**                       
  Lists/displays physical volume information

**vgs/vgdisplay lvs/lvdisplay**         
  Lists/displays volume group information Lists/displays logical volume information


All the tools accept the -v switch to support verbosity. 


## Exercise 13-6: Create Physical Volume and Volume Group (server2)

initialize one partition sdd1 (90MB) and one disk sde (250MB) for use in LVM.
create a volume group called vgbook and add both physical volumes to it
use the PE size of 16MB
list and display the volume group and the physical volumes.

1\. Create a partition of size 90MB on sdd using the parted command and confirm. You need to label the disk first, as it is a new disk.

```bash
[root@server2 ~]# sudo parted /dev/sdd mklabel msdos
Information: You may need to update /etc/fstab.

[root@server2 ~]# sudo parted /dev/sdd mkpart primary 1 91m               
Information: You may need to update /etc/fstab.

[root@server2 ~]# sudo parted /dev/sdd print                              
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdd: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  91.2MB  90.2MB  primary
```

2\. Initialize the sdd1 partition and the sde disk using the `pvcreate` command. Note that there is no need to apply a disk label on sde with parted as LVM does not require it.
```bash
[root@server2 ~]# sudo pvcreate /dev/sdd1 /dev/sde -v
  Wiping signatures on new PV /dev/sdd1.
  Wiping signatures on new PV /dev/sde.
  Set up physical volume for "/dev/sdd1" with 176128 available sectors.
  Zeroing start of device /dev/sdd1.
  Writing physical volume data to disk "/dev/sdd1".
  Physical volume "/dev/sdd1" successfully created.
  Set up physical volume for "/dev/sde" with 512000 available sectors.
  Zeroing start of device /dev/sde.
  Writing physical volume data to disk "/dev/sde".
  Physical volume "/dev/sde" successfully created.
```


3\. Create vgbook volume group using the vgcreate command and add the two physical volumes to it. Use the -s option to specify the PE size in
MBs.
```bash
[root@server2 ~]# sudo vgcreate -vs 16 vgbook /dev/sdd1 /dev/sde
  Wiping signatures on new PV /dev/sdd1.
  Wiping signatures on new PV /dev/sde.
  Adding physical volume '/dev/sdd1' to volume group 'vgbook'
  Adding physical volume '/dev/sde' to volume group 'vgbook'
  Creating volume group backup "/etc/lvm/backup/vgbook" (seqno 1).
  Volume group "vgbook" successfully created
```

4\. List the volume group information:
```bash
[root@server2 ~]# sudo vgs vgbook
  VG     #PV #LV #SN Attr   VSize   VFree  
  vgbook   2   0   0 wz--n- 320.00m 320.00m
```

5\. Display detailed information about the volume group and the physical volumes it contains:
```bash
[root@server2 ~]# sudo vgdisplay -v vgbook
  --- Volume group ---
  VG Name               vgbook
  System ID             
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               320.00 MiB
  PE Size               16.00 MiB
  Total PE              20
  Alloc PE / Size       0 / 0   
  Free  PE / Size       20 / 320.00 MiB
  VG UUID               zRu1d2-ZgDL-bnzV-I9U1-0IFo-uM4x-w4bX0Q
   
  --- Physical volumes ---
  PV Name               /dev/sdd1     
  PV UUID               8x8IgZ-3z5T-ODA8-dofQ-xk5s-QN7I-KwpQ1e
  PV Status             allocatable
  Total PE / Free PE    5 / 5
   
  PV Name               /dev/sde     
  PV UUID               xJU0Hh-W5k9-FyKO-d6Ha-1ofW-ajvh-hJSo8R
  PV Status             allocatable
  Total PE / Free PE    15 / 15
```

6\. List the physical volume information:
```bash
[root@server2 ~]# sudo pvs
  PV         VG     Fmt  Attr PSize   PFree  
  /dev/sda2  rhel   lvm2 a--  <19.00g      0 
  /dev/sdd1  vgbook lvm2 a--   80.00m  80.00m
  /dev/sde   vgbook lvm2 a--  240.00m 240.00m
```


The output shows the physical volumes in vgbook, along with their utilization status.


7\. Display detailed information about the physical volumes:
```bash
[root@server2 ~]# sudo pvdisplay /dev/sdd1
  --- Physical volume ---
  PV Name               /dev/sdd1
  VG Name               vgbook
  PV Size               86.00 MiB / not usable 6.00 MiB
  Allocatable           yes 
  PE Size               16.00 MiB
  Total PE              5
  Free PE               5
  Allocated PE          0
  PV UUID               8x8IgZ-3z5T-ODA8-dofQ-xk5s-QN7I-KwpQ1e
```

Once a partition or disk is initialized and added to a volume group, they are treated identically within the volume group. LVM does not
prefer one over the other.

## Exercise 13-7: Create Logical Volumes(server2)

create two logical volumes, lvol0 and lvbook1, in the vgbook volume group.
use 120MB for lvol0 and 192MB for lvbook1 from the available pool of space. 
display the details of the volume group and the logical volumes.


1\. Create a logical volume with the default name lvol0 using the `lvcreate` command. Use the -L option to specify the logical volume size,
120MB. You may use the -v, -vv, or -vvv option with the command for verbosity.
```bash
root@server2 ~]# sudo lvcreate -vL 120 vgbook
  Rounding up size to full physical extent 128.00 MiB
  Creating logical volume lvol0
  Archiving volume group "vgbook" metadata (seqno 1).
  Activating logical volume vgbook/lvol0.
  activation/volume_list configuration setting not defined: Checking only host tags for vgbook/lvol0.
  Creating vgbook-lvol0
  Loading table for vgbook-lvol0 (253:2).
  Resuming vgbook-lvol0 (253:2).
  Wiping known signatures on logical volume vgbook/lvol0.
  Initializing 4.00 KiB of logical volume vgbook/lvol0 with value 0.
  Logical volume "lvol0" created.
  Creating volume group backup "/etc/lvm/backup/vgbook" (seqno 2).
```


The size for the logical volume may be specified in units such as MBs, GBs, TBs, or as a count of LEs; however, MB is the default if no unit is
specified (see the previous command). 

The size of a logical volume is always in multiples of the PE size. For instance, logical volumes created in vgbook with the PE size set at 16MB can be 16MB, 32MB, 48MB,
64MB, and so on. The output above indicates that the logical volume is 128MB (16x8), and not 120MB as specified.

2\. Create lvbook1 of size 192MB (16x12) using the lvcreate command. Use the -l switch to specify the size in logical extents and -n for the custom name. 
```bash
[root@server2 ~]# sudo lvcreate -l 12 -n lvbook1 vgbook
  Logical volume "lvbook1" created.
```


3\. List the logical volume information:
```bash
[root@server2 ~]# sudo lvs
  LV      VG     Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel   -wi-ao---- <17.00g                                                    
  swap    rhel   -wi-ao----   2.00g                                                    
  lvbook1 vgbook -wi-a----- 192.00m                                                    
  lvol0   vgbook -wi-a----- 128.00m 
```

4\. Display detailed information about the volume group including the logical volumes and the physical volumes:
```bash
[root@server2 ~]# sudo vgdisplay -v vgbook
  --- Volume group ---
  VG Name               vgbook
  System ID             
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               0
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               320.00 MiB
  PE Size               16.00 MiB
  Total PE              20
  Alloc PE / Size       20 / 320.00 MiB
  Free  PE / Size       0 / 0   
  VG UUID               zRu1d2-ZgDL-bnzV-I9U1-0IFo-uM4x-w4bX0Q
   
  --- Logical volume ---
  LV Path                /dev/vgbook/lvol0
  LV Name                lvol0
  VG Name                vgbook
  LV UUID                9M9ahf-1L3y-c0yk-3Z2O-UzjH-0Amt-QLi4p5
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-12 02:42:51 -0700
  LV Status              available
  # open                 0
  LV Size                128.00 MiB
  Current LE             8
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:2
   
  --- Logical volume ---
  LV Path                /dev/vgbook/lvbook1
  LV Name                lvbook1
  VG Name                vgbook
  LV UUID                pgd8qR-YXXK-3Idv-qmpW-w8Az-WGLR-g2d8Yn
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-12 02:45:31 -0700
  LV Status              available
  # open                 0
  LV Size                192.00 MiB
  Current LE             12
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:3
   
  --- Physical volumes ---
  PV Name               /dev/sdd1     
  PV UUID               8x8IgZ-3z5T-ODA8-dofQ-xk5s-QN7I-KwpQ1e
  PV Status             allocatable
  Total PE / Free PE    5 / 0
   
  PV Name               /dev/sde     
  PV UUID               xJU0Hh-W5k9-FyKO-d6Ha-1ofW-ajvh-hJSo8R
  PV Status             allocatable
  Total PE / Free PE    15 / 0
```


Alternatively, you can run the following to view only the logical volume
details:

```bash
[root@server2 ~]# sudo lvdisplay /dev/vgbook/lvol0
  --- Logical volume ---
  LV Path                /dev/vgbook/lvol0
  LV Name                lvol0
  VG Name                vgbook
  LV UUID                9M9ahf-1L3y-c0yk-3Z2O-UzjH-0Amt-QLi4p5
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-12 02:42:51 -0700
  LV Status              available
  # open                 0
  LV Size                128.00 MiB
  Current LE             8
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:2
 ```

```bash
[root@server2 ~]# sudo lvdisplay /dev/vgbook/lvbook1
  --- Logical volume ---
  LV Path                /dev/vgbook/lvbook1
  LV Name                lvbook1
  VG Name                vgbook
  LV UUID                pgd8qR-YXXK-3Idv-qmpW-w8Az-WGLR-g2d8Yn
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-12 02:45:31 -0700
  LV Status              available
  # open                 0
  LV Size                192.00 MiB
  Current LE             12
  Segments               2
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:3
```


## Exercise 13-8: Extend a Volume Group and a Logical Volume(server2)

add another partition sdd2 of size 158MB to vgbook to increase the pool of allocatable space
initialize the new partition prior to adding it to the volume group. 
increase the size of lvbook1 to 336MB.
display basic information for the physical volumes, volume group, and logical volume.

1\. Create a partition of size 158MB on sdd using the parted command. Display the new partition to confirm the partition number and size.
```bash
[root@server2 ~]# sudo parted /dev/sdd print                              
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdd: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End     Size    Type     File system  Flags
 1      1049kB  91.2MB  90.2MB  primary
 2      92.3MB  250MB   157MB   primary               lvm
```

2\. Initialize sdd2 using the pvcreate command:
```bash
[root@server2 ~]# sudo pvcreate /dev/sdd2
  Physical volume "/dev/sdd2" successfully created.
```

3\. Extend vgbook by adding the new physical volume to it:
```bash
[root@server2 ~]# sudo vgextend vgbook /dev/sdd2
  Volume group "vgbook" successfully extended
```

4\. List the volume group:
```bash
[root@server2 ~]# sudo vgs
  VG     #PV #LV #SN Attr   VSize   VFree  
  rhel     1   2   0 wz--n- <19.00g      0 
  vgbook   3   2   0 wz--n- 464.00m 144.00m
```

5\. Extend the size of lvbook1 to 340MB by adding 144MB using the lvextend command:
```bash
[root@server2 ~]# sudo lvextend -L +144 /dev/vgbook/lvbook1
  Size of logical volume vgbook/lvbook1 changed from 192.00 MiB (12 extents) to 336.00 MiB (21 extents).
  Logical volume vgbook/lvbook1 successfully resized.
  ```

EXAM TIP: Make sure the expansion of a logical volume does not affect the file system and the data it contains.

6\. Issue vgdisplay on vgbook with the -v switch for the updated
details:
```bash
[root@server2 ~]# sudo vgdisplay -v vgbook
  --- Volume group ---
  VG Name               vgbook
  System ID             
  Format                lvm2
  Metadata Areas        3
  Metadata Sequence No  5
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               0
  Max PV                0
  Cur PV                3
  Act PV                3
  VG Size               464.00 MiB
  PE Size               16.00 MiB
  Total PE              29
  Alloc PE / Size       29 / 464.00 MiB
  Free  PE / Size       0 / 0   
  VG UUID               zRu1d2-ZgDL-bnzV-I9U1-0IFo-uM4x-w4bX0Q
   
  --- Logical volume ---
  LV Path                /dev/vgbook/lvol0
  LV Name                lvol0
  VG Name                vgbook
  LV UUID                9M9ahf-1L3y-c0yk-3Z2O-UzjH-0Amt-QLi4p5
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-12 02:42:51 -0700
  LV Status              available
  # open                 0
  LV Size                128.00 MiB
  Current LE             8
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:2
   
  --- Logical volume ---
  LV Path                /dev/vgbook/lvbook1
  LV Name                lvbook1
  VG Name                vgbook
  LV UUID                pgd8qR-YXXK-3Idv-qmpW-w8Az-WGLR-g2d8Yn
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-12 02:45:31 -0700
  LV Status              available
  # open                 0
  LV Size                336.00 MiB
  Current LE             21
  Segments               3
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:3
   
  --- Physical volumes ---
  PV Name               /dev/sdd1     
  PV UUID               8x8IgZ-3z5T-ODA8-dofQ-xk5s-QN7I-KwpQ1e
  PV Status             allocatable
  Total PE / Free PE    5 / 0
   
  PV Name               /dev/sde     
  PV UUID               xJU0Hh-W5k9-FyKO-d6Ha-1ofW-ajvh-hJSo8R
  PV Status             allocatable
  Total PE / Free PE    15 / 0
   
  PV Name               /dev/sdd2     
  PV UUID               1olOnk-o8FH-uJRD-2pJf-8GCy-3K0M-gcf3pF
  PV Status             allocatable
  Total PE / Free PE    9 / 0
```

7\. View a summary of the physical volumes:
```bash
root@server2 ~]# sudo pvs
  PV         VG     Fmt  Attr PSize   PFree
  /dev/sda2  rhel   lvm2 a--  <19.00g    0 
  /dev/sdd1  vgbook lvm2 a--   80.00m    0 
  /dev/sdd2  vgbook lvm2 a--  144.00m    0 
  /dev/sde   vgbook lvm2 a--  240.00m    0
```

8\. View a summary of the logical volumes:
```bash
root@server2 ~]# sudo lvs
  LV      VG     Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel   -wi-ao---- <17.00g                                                    
  swap    rhel   -wi-ao----   2.00g                                                    
  lvbook1 vgbook -wi-a----- 336.00m                                                    
  lvol0   vgbook -wi-a----- 128.00m 
```

## Exercise 13-9: Rename, Reduce, Extend, and Remove Logical Volumes(server2)

rename lvol0 to lvbook2.
decrease the size of lvbook2 to 50MB using the lvreduce command  
add 32MB with the lvresize command. 
remove both logical volumes.display the summary for the volume groups, logical volumes, and
physical volumes.

1\. Rename lvol0 to lvbook2 using the lvrename command and confirm with
lvs:
```bash
[root@server2 ~]# sudo lvrename vgbook lvol0 lvbook2
  Renamed "lvol0" to "lvbook2" in volume group "vgbook"
```

2\. Reduce the size of lvbook2 to 50MB with the `lvreduce` command. Specify the absolute desired size for the logical volume. Answer "Do you
really want to reduce vgbook/lvbook2?" in the affirmative.
```bash
[root@server2 ~]# sudo lvreduce -L 50 /dev/vgbook/lvbook2
  Rounding size to boundary between physical extents: 64.00 MiB.
  No file system found on /dev/vgbook/lvbook2.
  Size of logical volume vgbook/lvbook2 changed from 128.00 MiB (8 extents) to 64.00 MiB (4 extents).
  Logical volume vgbook/lvbook2 successfully resized.
```

3\. Add 32MB to lvbook2 with the lvresize command:
```bash
[root@server2 ~]# sudo lvresize -L +32 /dev/vgbook/lvbook2
  Size of logical volume vgbook/lvbook2 changed from 64.00 MiB (4 extents) to 96.00 MiB (6 extents).
  Logical volume vgbook/lvbook2 successfully resized.
```

4\. Use the pvs, lvs, vgs, and vgdisplay commands to view the updated
allocation.
```bash
[root@server2 ~]# pvs
  PV         VG     Fmt  Attr PSize   PFree 
  /dev/sda2  rhel   lvm2 a--  <19.00g     0 
  /dev/sdd1  vgbook lvm2 a--   80.00m     0 
  /dev/sdd2  vgbook lvm2 a--  144.00m     0 
  /dev/sde   vgbook lvm2 a--  240.00m 32.00m
  
[root@server2 ~]# lvs
  LV      VG     Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel   -wi-ao---- <17.00g                                                    
  swap    rhel   -wi-ao----   2.00g                                                    
  lvbook1 vgbook -wi-a----- 336.00m                                                    
  lvbook2 vgbook -wi-a-----  96.00m  
 
[root@server2 ~]# vgs
  VG     #PV #LV #SN Attr   VSize   VFree 
  rhel     1   2   0 wz--n- <19.00g     0 
  vgbook   3   2   0 wz--n- 464.00m 32.00m
  
[root@server2 ~]# vgdisplay
  --- Volume group ---
  VG Name               vgbook
  System ID             
  Format                lvm2
  Metadata Areas        3
  Metadata Sequence No  8
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               0
  Max PV                0
  Cur PV                3
  Act PV                3
  VG Size               464.00 MiB
  PE Size               16.00 MiB
  Total PE              29
  Alloc PE / Size       27 / 432.00 MiB
  Free  PE / Size       2 / 32.00 MiB
  VG UUID               zRu1d2-ZgDL-bnzV-I9U1-0IFo-uM4x-w4bX0Q
   
  --- Volume group ---
  VG Name               rhel
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <19.00 GiB
  PE Size               4.00 MiB
  Total PE              4863
  Alloc PE / Size       4863 / <19.00 GiB
  Free  PE / Size       0 / 0   
  VG UUID               UiK3fy-FGOc-2fnP-C1Y6-JS0l-irEe-Sq3c4h

```

5\. Remove both lvbook1 and lvbook2 logical volumes using the lvremove
command. Use the -f option to suppress the "Do you really want to remove
active logical volume" message.
```bash
[root@server2 ~]# sudo lvremove /dev/vgbook/lvbook1 -f
  Logical volume "lvbook1" successfully removed.
[root@server2 ~]# sudo lvremove /dev/vgbook/lvbook2 -f
  Logical volume "lvbook2" successfully removed.
```

Removing a logical volume is a destructive task. You need to ensure that you perform a backup of any data in the target logical volume prior to
deleting it. You will need to unmount the file system or disable swap in the logical volume. 

\
6\. Execute the `vgdisplay` command and grep for "Cur LV" to see the number of logical volumes currently available in vgbook. It should show
0, as you have removed both logical volumes.
```bash
[root@server2 ~]# sudo vgdisplay vgbook | grep 'Cur LV'
  Cur LV                0
```

## Exercise 13-10: Reduce and Remove a Volume Group(server2)
\

- reduce vgbook by removing the sdd1 and sde physical volumes from it
- remove the volume group. 
- Confirm the deletion of the volume group and the logical volumes at the end.


1\. Remove sdd1 and sde physical volumes from vgbook by issuing the `vgreduce` command:
```bash
[root@server2 ~]# sudo vgreduce vgbook /dev/sdd1 /dev/sde
  Removed "/dev/sdd1" from volume group "vgbook"
  Removed "/dev/sde" from volume group "vgbook"
```

2\. Remove the volume group using the `vgremove` command. This will also remove the last physical volume, sdd2, from it.
```bash
[root@server2 ~]# sudo vgremove vgbook
  Volume group "vgbook" successfully removed

```

You can also use the -f option with the vgremove command to force the volume group removal even if it contains any number of logical and physical volumes in it.

Remember to proceed with caution whenever you perform reduce and erase operations.

3\. Execute the vgs and lvs commands for confirmation:
```bash
[root@server2 ~]# sudo vgs
  VG   #PV #LV #SN Attr   VSize   VFree
  rhel   1   2   0 wz--n- <19.00g    0 
[root@server2 ~]# sudo lvs
  LV   VG   Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rhel -wi-ao---- <17.00g                                                    
  swap rhel -wi-ao----   2.00g    
```

## Exercise 13-11: Uninitialize Physical Volumes (Server2)\

- Uninitialize all three physical volumes---sdd1, sdd2, and sde---by deleting the LVM structural information from them. 
- Use the `pvs` command for confirmation. 
- Remove the partitions from the sdd disk and 
- verify that all disks used in Exercises 13-6 to 13-10 are now in their original raw state.

1\. Remove the LVM structures from sdd1, sdd2, and sde using the `pvremove` command:
```bash
[root@server2 ~]# sudo pvremove /dev/sdd1 /dev/sdd2 /dev/sde
  Labels on physical volume "/dev/sdd1" successfully wiped.
  Labels on physical volume "/dev/sdd2" successfully wiped.
  Labels on physical volume "/dev/sde" successfully wiped.
```

2\. Confirm the removal using the `pvs` command:
```bash
[root@server2 ~]# sudo pvs
  PV         VG   Fmt  Attr PSize   PFree
  /dev/sda2  rhel lvm2 a--  <19.00g    0 
```


The partitions and the disk are now back to their raw state and can be repurposed.

3\. Remove the partitions from sdd using the `parted` command:
```bash
[root@server2 ~]# sudo parted /dev/sdd rm 1 ; sudo parted /dev/sdd rm 2
Information: You may need to update /etc/fstab.

Information: You may need to update /etc/fstab.  
```

4\. Verify that all disks used in previous exercises have returned to their original raw state using the lsblk command:
```bash
[root@server2 ~]# lsblk                                                   
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0   20G  0 disk 
├─sda1          8:1    0    1G  0 part /boot
└─sda2          8:2    0   19G  0 part 
  ├─rhel-root 253:0    0   17G  0 lvm  /
  └─rhel-swap 253:1    0    2G  0 lvm  [SWAP]
sdb             8:16   0  250M  0 disk 
sdc             8:32   0  250M  0 disk 
sdd             8:48   0  250M  0 disk 
sde             8:64   0  250M  0 disk 
sdf             8:80   0    5G  0 disk 
sr0            11:0    1  9.8G  0 rom  

```

## Storage Optimization with Virtual Data Optimizer (VDO)

VDO is a device driver layer that sits between the Linux kernel and the physical storage devices.
conserve disk space, improve data throughput, and save on storage cost.
VDO employs thin provisioning, de-duplication, and compression technologies to help realize the goals.

## How VDO Conserves Storage

**Stage 1**
makes use of the thin provisioning technology to identify and eliminate empty (zero-byte) data blocks. (zero-block elimination)
removes randomization of data blocks by moving in-use data blocks to contiguous locations on the storage device.

![](image-XYSCLXMC.jpg)

**Stage 2**
If it detects that new data is an identical copy of some existing data, it makes an internal note of it but does not actually write the redundant data to
the disk. (de-duplication) to this end. 
Implemented with the inclusion of a kernel module calledUDS (Universal De-duplication Service). 
\
**Stage 3**
calls upon another kernel module called kvdo, which compresses the residual data blocks and consolidates them on a lower number of blocks. 
results in a further drop in storage space utilization.

VDO runs in the background and processes inbound data through the three stages on VDO-enabled volumes. 
VDO is not a CPU- or memory-intensive process

## VDO Integration with LVM
\

RHEL 9 uses an LVM VDO implementation for managing VDO logical volumes. 
Unlike previous versions of RHEL, a separate set of VDO management tools are no longer necessary. 
The LVM utilities have been enhanced to include options to support VDO volumes.

## VDO Components

utilizes the concepts of pool and volume. 
Pool:
	is a logical volume that is created inside an LVM volume group using a deduplicated storage space. 
volume: 
	just like a regular LVM logical volume, but it is provisioned in a pool. 
	needs to be formatted with file system structures before it can be used.

\
`vdo` and `kmod-kvdo`
create, mount, and manage LVM VDO volumes
installed on the system by default.

`vdo`
installs the tools necessary to support the creation and management of VDO volumes

`kmod-kvdo`
implements fine-grained storage virtualization, thin provisioning, and compression.
Not installed by default?


## Exercise 13-12: Create an LVM VDO Volume

-  initialize the 5GB disk (sdf) for use in LVM VDO. 
- create a volume group called vgvdo and add the physical volume to it.
- list and display the volume group and the physical volume. 
- create a VDO volume called lvvdo with a virtual size of 20GB.

\

1\. Initialize the sdf disk using the pvcreate command:
```bash
[root@server2 ~]# sudo pvcreate /dev/sdf
  Physical volume "/dev/sdf" successfully created.
```

2\. Create vgvdo volume group using the vgcreate command:
```bash
[root@server2 ~]# sudo vgcreate vgvdo /dev/sdf
  Volume group "vgvdo" successfully created
```

3\. Display basic information about the volume group:
```bash
[root@server2 ~]# sudo vgdisplay vgvdo
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  --- Volume group ---
  VG Name               vgvdo
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  1
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                0
  Open LV               0
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <5.00 GiB
  PE Size               4.00 MiB
  Total PE              1279
  Alloc PE / Size       0 / 0   
  Free  PE / Size       1279 / <5.00 GiB
  VG UUID               tED1vC-Ylec-fpeR-KM8F-8FzP-eaQ4-AsFrgc
```

4\. Create a VDO volume called lvvdo using the `lvcreate` command. Use the -l option to specify the number of logical extents (1279) to be allocated and the -V option for the amount of virtual space.
```bash
[root@server2 ~]# sudo dnf install kmod-kvdo
[root@server2 ~]# sudo lvcreate --type vdo -l 1279 -n lvvdo -V 20G vgvdo
    The VDO volume can address 2 GB in 1 data slab.
    It can grow to address at most 16 TB of physical storage in 8192 slabs.
    If a larger maximum size might be needed, use bigger slabs.
  Logical volume "lvvdo" created.
```

5\. Display detailed information about the volume group including the logical volume and the physical volume:
```bash
[root@server2 ~]# sudo vgdisplay -v vgvdo
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  --- Volume group ---
  VG Name               vgvdo
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               0
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <5.00 GiB
  PE Size               4.00 MiB
  Total PE              1279
  Alloc PE / Size       1279 / <5.00 GiB
  Free  PE / Size       0 / 0   
  VG UUID               tED1vC-Ylec-fpeR-KM8F-8FzP-eaQ4-AsFrgc
   
  --- Logical volume ---
  LV Path                /dev/vgvdo/vpool0
  LV Name                vpool0
  VG Name                vgvdo
  LV UUID                yGAsK2-MruI-QGy2-Q1IF-CDDC-XPNT-qkjJ9t
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-16 09:35:46 -0700
  LV VDO Pool data       vpool0_vdata
  LV VDO Pool usage      60.00%
  LV VDO Pool saving     100.00%
  LV VDO Operating mode  normal
  LV VDO Index state     online
  LV VDO Compression st  online
  LV VDO Used size       <3.00 GiB
  LV Status              NOT available
  LV Size                <5.00 GiB
  Current LE             1279
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
   
  --- Logical volume ---
  LV Path                /dev/vgvdo/lvvdo
  LV Name                lvvdo
  VG Name                vgvdo
  LV UUID                nnGTW5-tVFa-T3Cy-9nHj-sozF-2KpP-rVfnSq
  LV Write Access        read/write
  LV Creation host, time server2, 2024-06-16 09:35:47 -0700
  LV VDO Pool name       vpool0
  LV Status              available
  # open                 0
  LV Size                20.00 GiB
  Current LE             5120
  Segments               1
  Allocation             inherit
  Read ahead sectors     auto
  - currently set to     8192
  Block device           253:4
   
  --- Physical volumes ---
  PV Name               /dev/sdf     
  PV UUID               0oAXHG-C4ub-Myou-5vZf-QxIX-KVT3-ipMZCp
  PV Status             allocatable
  Total PE / Free PE    1279 / 0
```


The output reflects the creation of two logical volumes: a pool called /dev/vgvdo/vpool0 and a volume called /dev/vgvdo/lvvdo.

## Exercise 13-13: Remove a Volume Group and Uninitialize Physical Volume(Server2)


- remove the vgvdo volume group along with the VDO volumes
- uninitialize the physical volume /dev/sdf. 
- confirm the deletion.

1\. Remove the volume group along with the VDO volumes using the vgremove command:
```bash
[root@server2 ~]# sudo vgremove vgvdo -f
  Logical volume "lvvdo" successfully removed.
  Volume group "vgvdo" successfully removed
```

Remember to proceed with caution whenever you perform erase operations.

2\. Execute `sudo vgs` and `sudo lvs` commands for confirmation.
```bash
[root@server2 ~]# sudo vgs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  VG   #PV #LV #SN Attr   VSize   VFree
  rhel   1   2   0 wz--n- <19.00g    0 
  
[root@server2 ~]# sudo lvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  LV   VG   Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root rhel -wi-ao---- <17.00g                                                    
  swap rhel -wi-ao----   2.00g  
  ```
  
3\. Remove the LVM structures from sdf using the `pvremove` command:
```bash
[root@server2 ~]# sudo pvremove /dev/sdf
  Labels on physical volume "/dev/sdf" successfully wiped.
```

4\. Confirm the removal by running `sudo pvs`.
```bash
[root@server2 ~]# sudo pvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  PV         VG   Fmt  Attr PSize   PFree
  /dev/sda2  rhel lvm2 a--  <19.00g    0 
```
 
The disk is now back to its raw state and can be repurposed.

5\. Verify that the sdf disk used in the previous exercises has returned to its original raw state using the `lsblk` command:
```bash
[root@server2 ~]# lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0   20G  0 disk 
├─sda1          8:1    0    1G  0 part /boot
└─sda2          8:2    0   19G  0 part 
  ├─rhel-root 253:0    0   17G  0 lvm  /
  └─rhel-swap 253:1    0    2G  0 lvm  [SWAP]
sdb             8:16   0  250M  0 disk 
sdc             8:32   0  250M  0 disk 
sdd             8:48   0  250M  0 disk 
sde             8:64   0  250M  0 disk 
sdf             8:80   0    5G  0 disk 
sr0            11:0    1  9.8G  0 rom 
```

This brings the exercise to an end.

## Review Questions


Q. Where is the partition table information stored on BIOS-based systems?
A. The partition table information is stored on the Master Boot Record.

---

Q\. What is the name of the technology that VDO employs to remove randomization of data blocks?
A\. VDO employs thin provisioning technology to remove data block randomization.

---

Q\. What would sdd3 represent?
A\. sdd3 represents the third partition on the fourth disk.

---

Q\. Provide the command to add physical volumes /dev/sdd1 and /dev/sdc to vg20 volume group.
A\. `vgextend vg20 /dev/sdd1 /dev/sdc`

---

Q\. What are the two commands that you can use to add logical extents to a logical volume?
A\. The `lvextend` and `lvresize` commands.

---

Q\. Provide the command to create a volume group called vg20 on /dev/sdd disk with physical extent size 64MB.
A\. `vgcreate -s 64 vg20 /dev/sdd`

---

Q\. Thin provisioning technology allows us to create logical volumes of sizes larger than the actual physical storage size. True or False?
A\. True.

---

Q\. What is the maximum supported number of usable partitions on a GPT disk?
A\. 128.

---

Q\. Which kernel module is responsible for data block compression in VDO volumes?
A\. The kvdo module is responsible for compressing data blocks in VDO volumes.

---

Q\. What are the three techniques VDO volumes employ for storage conservation?
A\. VDO volumes use thin provisioning, de-duplication, and compression techniques for storage conservation.

---

Q\. What would the command `parted /dev/sdc mkpart pri 1 200m` do?
A\. The command provided will create a primary partition of size 200MB on the sdc disk starting at the beginning of the disk.

---

Q\. What is the maximum number of usable partitions that can be created on an MBR disk?
A\. 14.

---

Q\. The gdisk utility can be used to store partition information in MBR format. True or False?
A\. False. The gdisk tool is only for GPT type tables.

---

Q\. What would the command `parted /dev/sdd mklabel msdos` do?
A\. The command provided will apply msdos label to the sdd disk.

---

Q\. Which file in the /proc file system stores the in-memory partitioning information?
A\. The partitions file.

---

Q\. De-duplication is the process of zero-block elimination. True or False?
A\. False. De-duplication is the process of removing blocks of identical data.

---

Q\. The parted utility may be used to create LVM logical volumes. True or False?
A\. False.

---

Q\. What are the two commands that you can use to reduce the number of logical extents from a logical volume?
A\. The `lvreduce` and `lvresize` commands.

---

Q\. A single disk can be used by both parted and LVM solutions at the same time. True or False?
A\. True. A single disk can be shared between parted-created partitions
and LVM.

---

Q\. Provide the command to erase /dev/sdd1 physical volume from vg20 volume group.
A\. `vgreduce vg20 /dev/sdd1`

---

Q\. Provide the command to remove vg20 along with logical and physical volumes it contains.
A\. `vgremove -f vg20`

---

Q\. What is the default size of a physical extent in LVM?
A\. The default PE size is 4MB.

---

Q\. What is the default name for the first logical volume in a volume group?
A\. lvol0 is the default name for the first logical volume created in a
volume group.

---

Q\. What is one difference between the `pvs` and `pvdisplay` commands?
A\. The `pvs` command lists basic information about physical volumes
whereas the `pvdisplay` command shows the details.

---

Q\. When can a disk or partition be referred to as a physical volume?
A\. After the `pvcreate` command has been executed on it successfully.

---

Q\. Provide the command to remove webvol logical volume from vg20 volume group.
A\. `lvremove /dev/vg20/webvol`

---

Q\. It is necessary to create file system structures in a logical volume before it can be used to store files in it. True or False?
A\. True.

---

Q\. Physical and logical extents are typically of the same size. True or False?
A\. True.

---

Q\. What is the purpose of the `pvremove` command?
A\. The `pvremove` command is used to remove LVM information from a physical volume.

---

Q\. What would the command `pvcreate /dev/sdd` do?
A\. The command provided will prepare the /dev/sdd disk for use in a volume group.

---

Q\. A disk or partition can be added to a volume group without being initialized. True or False?
A\. False. A disk or partition must be initialized before it can be added to a volume group.

---

Q\. Provide the command to create a logical volume called webvol of size equal to 100 logical extents in vg20 volume group.
A\. `lvcreate -l 100 -n webvol vg20`

---

Q\. A volume group can be created without any physical volume in it. True or False?
A\. False.

---

Q\. A partition can be used as an LVM object. True or False?
A\. True.

---

Q\. Which command would you use to view the details of a volume group and its objects?
A\. The `vgdisplay` command with the `-v` option.


## Do-It-Yourself Challenge Labs

## Lab 13-1: Create and Remove Partitions with parted


Create a 100MB primary partition on one of the available 250MB disks (lsblk) by invoking the parted utility directly at the command prompt. Apply label "msdos" if the disk is new.
```bash
[root@server20 ~]# sudo parted /dev/sdb mklabel msdos
Warning: The existing disk label on /dev/sdb will be destroyed and all data on this disk will be lost. Do you want to
continue?
Yes/No? yes                                                               
Information: You may need to update /etc/fstab.

[root@server20 ~]# sudo parted /dev/sdb mkpart primary 1 101m             
Information: You may need to update /etc/fstab.
```

Create another 100MB partition by running parted interactively while ensuring that the second partition won't overlap the first. 
```bash
[root@server20 ~]# parted /dev/sdb
GNU Parted 3.5
Using /dev/sdb
Welcome to GNU Parted! Type 'help' to view a list of commands.
(parted) mkpart primary 101 201m                                         
```

Verify the label and the partitions. 
```bash
(parted) print                                                            
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdb: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End    Size    Type     File system  Flags
 1      1049kB  101MB  99.6MB  primary
 2      101MB   201MB  101MB   primary
```

Remove both partitions at the command prompt.
```bash
[root@server20 ~]# sudo parted /dev/sdb rm 1 rm 2
```

## Lab 13-2: Create and Remove Partitions with gdisk


Create two 80MB partitions on one of the 250MB disks (lsblk) using the gdisk utility. Make sure the partitions won't overlap. 
```bash
Command (? for help): o
This option deletes all partitions and creates a new protective MBR.
Proceed? (Y/N): y

Command (? for help): p
Disk /dev/sdb: 512000 sectors, 250.0 MiB
Model: VBOX HARDDISK   
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 226F7476-7F8C-4445-9025-53B6737AD1E4
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 511966
Partitions will be aligned on 2048-sector boundaries
Total free space is 511933 sectors (250.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name

Command (? for help): n
Partition number (1-128, default 1): 
First sector (34-511966, default = 2048) or {+-}size{KMGTP}: 
Last sector (2048-511966, default = 511966) or {+-}size{KMGTP}: +80M
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): 
Changed type of partition to 'Linux filesystem'

Command (? for help): n
Partition number (2-128, default 2): 2
First sector (34-511966, default = 165888) or {+-}size{KMGTP}: 165888
Last sector (165888-511966, default = 511966) or {+-}size{KMGTP}: +80M
Current type is 8300 (Linux filesystem)
Hex code or GUID (L to show codes, Enter = 8300): 
Changed type of partition to 'Linux filesystem'
```

Verify the partitions. 
```bash
Command (? for help): p
Disk /dev/sdb: 512000 sectors, 250.0 MiB
Model: VBOX HARDDISK   
Sector size (logical/physical): 512/512 bytes
Disk identifier (GUID): 226F7476-7F8C-4445-9025-53B6737AD1E4
Partition table holds up to 128 entries
Main partition table begins at sector 2 and ends at sector 33
First usable sector is 34, last usable sector is 511966
Partitions will be aligned on 2048-sector boundaries
Total free space is 184253 sectors (90.0 MiB)

Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048          165887   80.0 MiB    8300  Linux filesystem
   2          165888          329727   80.0 MiB    8300  Linux filesystem
```

Save
```bash
Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdb.
The operation has completed successfully.
```

Delete the partitions
```bash
Command (? for help): d  
Partition number (1-2): 1

Command (? for help): d
Using 2

Command (? for help): w

Final checks complete. About to write GPT data. THIS WILL OVERWRITE EXISTING
PARTITIONS!!

Do you want to proceed? (Y/N): y
OK; writing new GUID partition table (GPT) to /dev/sdb.
The operation has completed successfully.

```

## Lab 13-3: Create Volume Group and Logical Volumes

\
initialize 1x250MB disk for use in LVM (use lsblk to identify available disks). 
```bash
root@server2 ~]# sudo parted /dev/sdd mklabel msdos
Warning: The existing disk label on /dev/sdd will be destroyed and all data
on this disk will be lost. Do you want to continue?
Yes/No? yes                                                               
Information: You may need to update /etc/fstab.

[root@server2 ~]# sudo parted /dev/sdd mkpart primary 1 250m              
Information: You may need to update /etc/fstab.

[root@server2 ~]# sudo parted /dev/sdd print                              
Model: ATA VBOX HARDDISK (scsi)
Disk /dev/sdd: 262MB
Sector size (logical/physical): 512B/512B
Partition Table: msdos
Disk Flags: 

Number  Start   End    Size   Type     File system  Flags
 1      1049kB  250MB  249MB  primary
 
[root@server2 ~]# sudo pvcreate /dev/sdd1
  Physical volume "/dev/sdd1" successfully created.

```

Create volume group vg100 with PE size 16MB and add the physical volume. 
```bash
[root@server2 ~]# sudo vgcreate -vs 15 vg100 /dev/sdd1
  Wiping signatures on new PV /dev/sdd1.
  Adding physical volume '/dev/sdd1' to volume group 'vg100'
  Creating volume group backup "/etc/lvm/backup/vg100" (seqno 1).
  Volume group "vg100" successfully created
```

Create two logical volumes lvol0 and swapvol of sizes 90MB and 120MB. 
```bash
[root@server2 ~]# sudo lvcreate -vL 90 vg100
  Creating logical volume lvol0
  Archiving volume group "vg100" metadata (seqno 1).
  Activating logical volume vg100/lvol0.
  activation/volume_list configuration setting not defined: Checking only host tags for vg100/lvol0.
  Creating vg100-lvol0
  Loading table for vg100-lvol0 (253:2).
  Resuming vg100-lvol0 (253:2).
  Wiping known signatures on logical volume vg100/lvol0.
  Initializing 4.00 KiB of logical volume vg100/lvol0 with value 0.
  Logical volume "lvol0" created.
  Creating volume group backup "/etc/lvm/backup/vg100" (seqno 2).

[root@server2 ~]# sudo lvcreate -l 8 -n swapvol vg100
  Logical volume "swapvol" created.
```


Use the vgs, pvs, lvs, and vgdisplay commands for verification.
```bash
[root@server2 ~]# lvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  LV      VG    Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel  -wi-ao---- <17.00g                                                    
  swap    rhel  -wi-ao----   2.00g                                                    
  lvol0   vg100 -wi-a-----  90.00m                                                    
  swapvol vg100 -wi-a----- 120.00m                                                    
[root@server2 ~]# vgs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  VG    #PV #LV #SN Attr   VSize   VFree 
  rhel    1   2   0 wz--n- <19.00g     0 
  vg100   1   2   0 wz--n- 225.00m 15.00m
  
[root@server2 ~]# pvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  PV         VG    Fmt  Attr PSize   PFree 
  /dev/sda2  rhel  lvm2 a--  <19.00g     0 
  /dev/sdd1  vg100 lvm2 a--  225.00m 15.00m
  
[root@server2 ~]# vgdisplay
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  --- Volume group ---
  VG Name               vg100
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  5
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               0
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               225.00 MiB
  PE Size               15.00 MiB
  Total PE              15
  Alloc PE / Size       14 / 210.00 MiB
  Free  PE / Size       1 / 15.00 MiB
  VG UUID               fEUf8R-nxKF-Uxud-7rmm-JvSQ-PsN1-Mrs3zc
   
  --- Volume group ---
  VG Name               rhel
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <19.00 GiB
  PE Size               4.00 MiB
  Total PE              4863
  Alloc PE / Size       4863 / <19.00 GiB
  Free  PE / Size       0 / 0   
  VG UUID               UiK3fy-FGOc-2fnP-C1Y6-JS0l-irEe-Sq3c4h
```

## Lab 13-4: Expand Volume Group and Logical Volume

create a partition on an available 250MB disk and initialize it for use in LVM (use lsblk to identify available disks). 
```bash
[root@server2 ~]# parted /dev/sdb mklabel msdos
Warning: The existing disk label on /dev/sdb will be destroyed and all data on this disk will be lost. Do you want to continue?
Yes/No? yes                                                               
Information: You may need to update /etc/fstab.

[root@server2 ~]# parted /dev/sdb mkpart primary 1 250m                   
Information: You may need to update /etc/fstab.

```

Add the new physical volume to vg100. 
```bash
[root@server2 ~]# sudo vgextend vg100 /dev/sdb1
  Device /dev/sdb1 has updated name (devices file /dev/sdd1)
  Physical volume "/dev/sdb1" successfully created.
  Volume group "vg100" successfully extended
```

Expand the lvol0 logical volume to size 300MB. 
```bash
[root@server2 ~]# lvextend -L +210 /dev/vg100/lvol0
  Size of logical volume vg100/lvol0 changed from 90.00 MiB (6 extents) to 300.00 MiB (20 extents).
  Logical volume vg100/lvol0 successfully resized.
```

Use the vgs, pvs, lvs, and vgdisplay commands for verification.
```bash
[[root@server2 ~]# lvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  LV      VG    Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel  -wi-ao---- <17.00g                                                    
  swap    rhel  -wi-ao----   2.00g                                                    
  lvol0   vg100 -wi-a-----  90.00m                                                    
  swapvol vg100 -wi-a----- 120.00m](<[root@server20 ~]# lvs
  LV      VG    Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel  -wi-ao---- %3C17.00g                                                    
  swap    rhel  -wi-ao----   2.00g                                                    
  lvol0   vg100 -wi-a----- 300.00m                                                    
  swapvol vg100 -wi-a----- 120.00m>)                                                  
[root@server2 ~]# vgs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  VG    #PV #LV #SN Attr   VSize   VFree 
  rhel    1   2   0 wz--n- <19.00g     0 
  vg100   2   2   0 wz--n- 450.00m 30.00m
  
[root@server2 ~]# pvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  PV         VG    Fmt  Attr PSize   PFree 
  /dev/sda2  rhel  lvm2 a--  <19.00g     0 
  /dev/sdb1  vg100 lvm2 a--  225.00m 30.00m
  /dev/sdd1  vg100 lvm2 a--  225.00m     0 
  
[root@server2 ~]# lvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  LV      VG    Attr       LSize   Pool Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root    rhel  -wi-ao---- <17.00g                                                    
  swap    rhel  -wi-ao----   2.00g                                                    
  lvol0   vg100 -wi-a----- 300.00m                                                    
  swapvol vg100 -wi-a----- 120.00m                                                    
[root@server2 ~]# vgdisplay
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  --- Volume group ---
  VG Name               vg100
  System ID             
  Format                lvm2
  Metadata Areas        2
  Metadata Sequence No  7
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               0
  Max PV                0
  Cur PV                2
  Act PV                2
  VG Size               450.00 MiB
  PE Size               15.00 MiB
  Total PE              30
  Alloc PE / Size       28 / 420.00 MiB
  Free  PE / Size       2 / 30.00 MiB
  VG UUID               fEUf8R-nxKF-Uxud-7rmm-JvSQ-PsN1-Mrs3zc
   
  --- Volume group ---
  VG Name               rhel
  System ID             
  Format                lvm2
  Metadata Areas        1
  Metadata Sequence No  3
  VG Access             read/write
  VG Status             resizable
  MAX LV                0
  Cur LV                2
  Open LV               2
  Max PV                0
  Cur PV                1
  Act PV                1
  VG Size               <19.00 GiB
  PE Size               4.00 MiB
  Total PE              4863
  Alloc PE / Size       4863 / <19.00 GiB
  Free  PE / Size       0 / 0   
  VG UUID               UiK3fy-FGOc-2fnP-C1Y6-JS0l-irEe-Sq3c4h
   
```

### Lab 13-5: Add a VDO Logical Volume

initialize the sdf disk for use in LVM and add it to vgvdo1. 
```bash
[root@server2 ~]# pvcreate /dev/sdc
  Physical volume "/dev/sdc" successfully created.
  
[root@server2 ~]# sudo vgextend vgvdo1 /dev/sdc
  Volume group "vgvdo1" successfully extended


```


Create a VDO logical volume named vdovol using the entire disk capacity. 
```bash
[root@server2 ~]# lvcreate --type vdo -n vdovol -l 100%FREE vgvdo1
WARNING: LVM2_member signature detected on /dev/vgvdo1/vpool0 at offset 536. Wipe it? [y/n]: y
  Wiping LVM2_member signature on /dev/vgvdo1/vpool0.
    Logical blocks defaulted to 523108 blocks.
    The VDO volume can address 2 GB in 1 data slab.
    It can grow to address at most 16 TB of physical storage in 8192 slabs.
    If a larger maximum size might be needed, use bigger slabs.
  Logical volume "vdovol" created.

```

Use the vgs, pvs, lvs, and vgdisplay commands for verification. 
```bash
[root@server2 ~]# vgs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB123ecea1-63467dee PVID RjcGRyHDIWY0OqAgfIHC93WT03Na1WoO last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VBa5e3cbf7-10921e08 PVID qeP9dCevNnTy422I8p18NxDKQ2WyDodU last seen on /dev/sdf1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID brKVLFEG3AoBzhWoso0Sa1gLYHgNZ4vL last seen on /dev/sdb1 not found.
  VG     #PV #LV #SN Attr   VSize   VFree  
  rhel     1   2   0 wz--n- <19.00g      0 
  vgvdo1   2   2   0 wz--n-  <5.24g 248.00m
```


## Lab 13-6: Reduce and Remove Logical Volumes
\
reduce the size of vdovol logical volume to 80MB. 
```bash
[root@server2 ~]# lvreduce -L 80 /dev/vgvdo1/vdovol
  No file system found on /dev/vgvdo1/vdovol.
  WARNING: /dev/vgvdo1/vdovol: Discarding 1.91 GiB at offset 83886080, please wait...
  Size of logical volume vgvdo1/vdovol changed from 1.99 GiB (510 extents) to 80.00 MiB (20 extents).
  Logical volume vgvdo1/vdovol successfully resized.
[root@server2 ~]# lvs
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID none last seen on /dev/sdd2 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB123ecea1-63467dee PVID RjcGRyHDIWY0OqAgfIHC93WT03Na1WoO last seen on /dev/sdd1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VBa5e3cbf7-10921e08 PVID qeP9dCevNnTy422I8p18NxDKQ2WyDodU last seen on /dev/sdf1 not found.
  Devices file sys_wwid t10.ATA_VBOX_HARDDISK_VB428913dd-446a194f PVID brKVLFEG3AoBzhWoso0Sa1gLYHgNZ4vL last seen on /dev/sdb1 not found.
  LV     VG     Attr       LSize   Pool   Origin Data%  Meta%  Move Log Cpy%Sync Convert
  root   rhel   -wi-ao---- <17.00g                                                      
  swap   rhel   -wi-ao----   2.00g                                                      
  vdovol vgvdo1 vwi-a-v---  80.00m vpool0        0.00                                   
  vpool0 vgvdo1 dwi-------  <5.00g               60.00                                  
[root@server2 ~]# 

```

erase logical volume vdovol. 
```bash
[root@server2 ~]# lvremove /dev/vgvdo1/vdovol
Do you really want to remove active logical volume vgvdo1/vdovol? [y/n]: y
  Logical volume "vdovol" successfully removed.
```

Confirm the deletion with vgs, pvs, lvs, and vgdisplay commands.


## Lab 13-7: Remove Volume Group and Physical Volumes

\remove the volume group and uninitialized the physical volumes. 
```bash
[root@server2 ~]# vgremove vgvdo1
  Volume group "vgvdo1" successfully removed
```

```bash
[root@server2 ~]# pvremove /dev/sdc
  Labels on physical volume "/dev/sdc" successfully wiped.
[root@server2 ~]# pvremove /dev/sdf
  Labels on physical volume "/dev/sdf" successfully wiped.
```

Confirm the deletion with vgs, pvs, lvs, and vgdisplay commands. 

Use the lsblk command and verify that the disks used for the LVM labs no longer show LVM information. 
```bash
[root@server2 ~]# lsblk
NAME          MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
sda             8:0    0   20G  0 disk 
├─sda1          8:1    0    1G  0 part /boot
└─sda2          8:2    0   19G  0 part 
  ├─rhel-root 253:0    0   17G  0 lvm  /
  └─rhel-swap 253:1    0    2G  0 lvm  [SWAP]
sdb             8:16   0  250M  0 disk 
sdc             8:32   0  250M  0 disk 
sdd             8:48   0  250M  0 disk 
sde             8:64   0  250M  0 disk 
sdf             8:80   0    5G  0 disk 
sr0            11:0    1  9.8G  0 rom  
```




