
This chapter describes the following major topics:

[![](images/00001.jpeg){.c37}]{.c36}Describe Logical Volume Manager and
its components

[![](images/00001.jpeg){.c37}]{.c36}Understand various Logical Volume
Manager management operations

[![](images/00001.jpeg){.c37}]{.c36}Know Logical Volume Manager
administration commands

[![](images/00001.jpeg){.c37}]{.c36}Create and confirm physical volumes,
volume groups, and logical volumes

[![](images/00001.jpeg){.c37}]{.c36}Rename, reduce, extend, and remove
logical volumes

[![](images/00001.jpeg){.c37}]{.c36}Extend, reduce, and remove volume
groups

[![](images/00001.jpeg){.c37}]{.c36}Remove physical volumes

[![](images/00001.jpeg){.c37}]{.c36}Overview of Stratis (a
volume-managing file system solution in RHEL) service and how it works

[![](images/00001.jpeg){.c37}]{.c36}Understand various Stratis
management operations and the command

[![](images/00001.jpeg){.c37}]{.c36}Create, confirm, expand, rename, and
destroy pools and file systems

[RHCSA Objectives:]{.c39}

[28]{#part0026_split_000.html#id_794 .calibre10}[.]{.c29}Create and
remove physical volumes

[29]{#part0026_split_000.html#id_795 .calibre10}[.]{.c29}Assign physical
volumes to volume groups

[30]{#part0026_split_000.html#id_796 .calibre10}[.]{.c29}Create and
delete logical volumes

32[.]{.c29}Add new partitions and logical volumes, and swap to a system
non-destructively (the swap portion of this objective is covered in
Chapter 15)

[35]{#part0026_split_000.html#id_801 .calibre10}[.]{.c29}Extend existing
logical volumes (additional coverage on this objective is available in
Chapter 15)

[38]{#part0026_split_000.html#id_804 .calibre10}[.]{.c29}Manage layered
volumes

::: {#part0026_split_000.html#calibre_pb_1 .calibre12}
:::

[]{#part0026_split_001.html}

[ T]{.c42}[his]{.c43} chapter is the second of the three chapters (the
other two being [Chapter
13](#part0025_split_000.html#page_301){.calibre5} (previous) and
[Chapter 15](#part0027_split_000.html#page_345){.calibre5} (next)) that
expounds upon storage management concepts and solutions available in
RHEL. We discussed partitioning and thinly provisioned volumes in the
previous chapter. This chapter presents a detailed coverage on Logical
Volume Manager solution. LVM sets up an abstraction layer between the
operating system and the storage hardware. It utilizes virtual objects
for storage pooling and allocation, and offers a whole slew of
management commands, each of which carries out a particular operation.

The other advanced storage management solution discussed in this chapter
is a volume-managing file system that capitalizes on the proven features
of LVM and the kernel device driver software. This solution dynamically
adjusts the size of the underlying volume, eliminating the need for
manual expansion.

**[Logical]{#part0026_split_001.html#id_379 .calibre10} Volume Manager
(LVM)**

The *Logical Volume Manager* (LVM) solution is widely used for managing
block storage in Linux. LVM provides an abstraction layer between the
physical storage and the file system, enabling the file system to be
resized, span across multiple physical disks, use arbitrary disk space,
*etc.* LVM accumulates spaces taken from partitions or entire disks
(called *Physical Volumes*) to form a logical container (called *Volume
Group*), which is then divided into logical partitions (called *Logical
Volumes*). The other key benefits of LVM include online resizing of
volume groups and logical volumes, online data migration between logical
volumes and between physical volumes, user-defined naming for volume
groups and logical volumes, mirroring and striping across multiple
physical disks, and snapshotting of logical volumes. [Figure
14-1](#part0026_split_001.html#id_678){.calibre5} depicts the LVM
components.

::: c49
::: width_
![](images/00692.jpeg){.calibre13}
:::

**Figure 14-1 LVM Structure**
:::

As noted above, the LVM structure is made up of three key objects called
physical volume, volume group, and logical volume. These objects are
further virtually broken down into *Physical Extents* (PEs) and *Logical
Extents* (LEs). The LVM components are explained in the following
subsections.

**Physical Volume**

A *Physical Volume* (PV) is created when a block storage device such as
a partition or an entire disk is initialized and brought under LVM
control. This process constructs LVM data structures on the device,
including a label on the second sector and metadata shortly thereafter.
The label includes the UUID, size, and pointers to the locations of data
and metadata areas. Given the criticality of metadata, LVM stores a copy
of it at the end of the physical volume as well. The rest of the device
space is available for use.

You can use an LVM command called *pvs* (*physical volume scan* or
*summary*) to scan and list available physical volumes on *server2*:

![](images/00693.jpeg){.image2}

The output shows one physical volume (PV) **dev*sda2* of size 9GB in
*rhel* volume group (VG). Additional information displays the metadata
format (Fmt) used, status of the physical volume under the Attr column
(a for allocatable), and the amount of free space available on the
physical volume (PFree).

Try running this command again with the -v flag to view more information
about the physical volume.

**[Volume]{#part0026_split_001.html#id_380 .calibre10} Group**

A *Volume Group* (VG) is created when at least one physical volume is
added to it. The space from all physical volumes in a volume group is
aggregated to form one large pool of storage, which is then used to
build logical volumes. The physical volumes added to a volume group may
be of varying sizes. LVM writes volume group metadata on each physical
volume that is added to it. The volume group metadata contains its name,
date and time of creation, how it was created, the extent size used, a
list of physical and logical volumes, a mapping of physical and logical
extents, *etc.* A volume group can have a custom name assigned to it at
the time of its creation. For example, it may be called *vg01*, *vgora*,
or *vgweb* that identifies the type of information it is constructed to
store. A copy of the volume group metadata is stored and maintained at
two distinct locations on each physical volume within the volume group.

You can use an LVM command called *vgs* (*volume group scan* or
*summary*) to scan and list available volume groups on *server2*:

![](images/00694.jpeg){.image2}

The output shows one volume group (VG) *rhel* on *server2* containing
one physical volume (#PV). Additional information displays the number of
logical volumes (#LV) and snapshots (#SN) in the volume group, status of
the volume group under the Attr column (w for writeable, z for
resizable, and n for normal), size of the volume group (VSize), and the
amount of free space available in the volume group (VFree).

Try running this command again with the -v flag to view more information
about the volume group.

**Physical Extent**

A physical volume is divided into several smaller logical pieces when it
is added to a volume group. These logical pieces are known as *Physical
Extents* (PE). An extent is the smallest allocatable unit of space in
LVM. At the time of volume group creation, you can either define the
size of the PE or leave it to the default value of 4MB. This implies
that a 20GB physical volume would have approximately 5,000 PEs. Any
physical volumes added to this volume group thereafter will use the same
PE size.

You can use an LVM command called *vgdisplay* (*volume group display*)
on *server2* and *grep* for 'PE Size' to view the PE size used in the
*rhel* volume group:

![](images/00695.jpeg){.image2}

The output reveals the PE size used for the *rhel* VG.

**[Logical]{#part0026_split_001.html#id_381 .calibre10} Volume**

A volume group consists of a pool of storage taken from one or more
physical volumes. This volume group space is used to create one or more
*Logical Volumes* (LVs). A logical volume can be created or weeded out
online, expanded or shrunk online, and can use space taken from one or
multiple physical volumes inside the volume group.

The default naming convention used for logical volumes is *lvol0, lvol1,
lvol2*, and so on; however, you may assign custom names to them. For
example, a logical volume may be called *system*, *undo*, or *webdata1*
so as to establish the type of information it is constructed to store.

You can use an LVM command called *lvs* (*logical volume scan* or
*summary*) to scan and list available logical volumes on *server2*:

![](images/00696.jpeg){.image2}

The output shows two logical volumes *root* and *swap* in *rhel* volume
group. Additional information displays the status of the logical volumes
under the Attr column (w for writeable, i for inherited allocation
policy, a for active, and o for open) and their sizes.

Try running this command again with the -v flag to view more information
about the logical volumes.

**[Logical]{#part0026_split_001.html#id_382 .calibre10} Extent**

A logical volume is made up of *Logical Extents* (LE). Logical extents
point to physical extents, and they may be random or contiguous. The
larger a logical volume is, the more logical extents it will have.
Logical extents are a set of physical extents allocated to the logical
volume.

The PE and LE sizes are normally kept the same within a volume group;
however, a logical extent can be smaller or larger than a physical
extent. The default LE size is 4MB, which corresponds to the default PE
size.

You can use an LVM command called *lvdisplay* (*logical volume display*)
on *server2* to view information about the *root* logical volume in the
*rhel* volume group.

![](images/00697.jpeg){.image2}

The output does not disclose the LE size; however, you can convert the
LV size in MBs (8,000) and then divide the result by the Current LE
count (2,047) to get the LE size (which comes close to 4MB).

**[LVM]{#part0026_split_001.html#id_383 .calibre10} Operations and
Commands**

The LVM toolset offers a multitude of administrative commands to carry
out various disk and volume management operations. These operations
include creating and removing a physical volume, volume group, and
logical volume; extending and reducing a volume group and logical
volume; renaming a volume group and logical volume; and listing and
displaying physical volume, volume group, and logical volume
information.

[Table 14-1](#part0026_split_001.html#id_741){.calibre5} summarizes the
common LVM tasks and the commands that are employed to accomplish them.

::: c49
  ---------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Command**                        **Description**
  **Create and Remove Operations**   
  pvcreate/pvremove                  Initializes/uninitializes a disk or partition for LVM use
  vgcreate/vgremove                  Creates/removes a volume group
  lvcreate/lvremove                  Creates/removes a logical volume
  **Extend and Reduce Operations**   
  vgextend/vgreduce                  Adds/removes a physical volume to/from a volume group
  lvextend/lvreduce                  Extends/reduces the size of a logical volume
  lvresize                           Resizes a logical volume. With the -r option, this command calls the resize2fs command and resizes the underlying file system as well. Applies to Ext2/Ext3/Ext4 file system types only.
  **Rename Operations**              
  vgrename                           Renames a volume group
  lvrename                           Renames a logical volume
  **Command**                        **Description**
  **List and Display Operations**    
  pvs/pvdisplay                      Lists/displays physical volume information
  vgs/vgdisplay                      Lists/displays volume group information
  lvs/lvdisplay                      Lists/displays logical volume information
  ---------------------------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0026_split_001.html#id_741} 14-1 Common LVM Operations
and Commands**
:::

All the tools accept the -v switch to support verbosity. Refer to the
manual pages of the commands for usage and additional details.

As noted earlier, there are seven disks available on *server2* for
practice. Issue the *lsblk* command to confirm:

![](images/00698.jpeg){.image2}

You will use the *sdd* and *sde* disks for LVM activities in the
following exercises.

**[Exercise]{#part0026_split_001.html#id_384 .calibre10} 14-1: Create a
Physical Volume and Volume Group**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will initialize one partition *sdd1* (90MB) and
one disk *sde* (250MB) for use in LVM. You will create a volume group
called *vgbook* and add both physical volumes to it. You will use the PE
size of 16MB and list and display the volume group and the physical
volumes.

1[.]{.c19}Create a partition of size 90MB on *sdd* using the *parted*
command and confirm. You need to label the disk first, as it is a new
disk.

![](images/00699.jpeg){.image2}

The *print* subcommand confirms the creation of the partition. It is the
first partition on the disk.

2[.]{.c19}Set (*set*) the flag on the partition (1) to "lvm" using the
*parted* command:

![](images/00700.jpeg){.image2}

3[.]{.c19}Verify flag activation using the *print* subcommand with
*parted*:

![](images/00701.jpeg){.image2}

The flag is applied and enabled on the partition as indicated under the
Flags column.

4[.]{.c19}Initialize the *sdd1* partition and the *sde* disk using the
*pvcreate* command. Note that there is no need to apply a disk label on
*sde* with *parted* as LVM does not require it.

![](images/00702.jpeg){.image2}

The command generated a verbose output. You now have two physical
volumes available for use.

5[.]{.c19}Create *vgbook* volume group using the *vgcreate* command and
add the two physical volumes to it. Use the -s option to specify the PE
size in MBs.

![](images/00703.jpeg){.image2}

The above command combines the two options with a single hyphen.

6[.]{.c19}List the volume group information:

![](images/00704.jpeg){.image5}![](images/00704.jpeg){.image5}

The total capacity available in the *vgbook* volume group is 320MB.

7.Display detailed information about the volume group and the physical
volumes it contains:

![](images/00705.jpeg){.image2}

The verbose output includes the physical volume attributes as well.
There are a total of 20 PEs in the volume group (5 in *sdd1* and 15 in
*sde*), and each PE is 16MB in size. The collective size of all the
physical volumes represents the total size of the volume group, which is
20x16 = 320MB.

8[.]{.c19}List the physical volume information:

![](images/00706.jpeg){.image2}

The output shows the physical volumes in *vgbook*, along with their
utilization status.

9[.]{.c19}Display detailed information about the physical volumes:

![](images/00707.jpeg){.image2}

Once a partition or disk is initialized and added to a volume group,
they are treated identically within the volume group. LVM does not
prefer one over the other.

**[Exercise]{#part0026_split_001.html#id_385 .calibre10} 14-2: Create
Logical Volumes**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create two logical volumes, *lvol0* and
*lvbook1*, in the *vgbook* volume group. You will use 120MB for *lvol0*
and 192MB for *lvbook1* from the available pool of space. You will
display the details of the volume group and the logical volumes.

1[.]{.c19}Create a logical volume with the default name *lvol0* using
the *lvcreate* command. Use the -L option to specify the logical volume
size, 120MB. You may use the -v, -vv, or -vvv option with the command
for verbosity.

![](images/00708.jpeg){.image2}

The size for the logical volume may be specified in units such as MBs,
GBs, TBs, or as a count of LEs; however, MB is the default if no unit is
specified (see the previous command). The size of a logical volume is
always in multiples of the PE size. For instance, logical volumes
created in *vgbook* with the PE size set at 16MB can be 16MB, 32MB,
48MB, 64MB, and so on. The output above indicates that the logical
volume is 128MB (16x8), and not 120MB as specified.

2[.]{.c19}Create *lvbook1* of size 192MB (16x12) using the *lvcreate*
command. Use the -l switch to specify the size in logical extents and -n
for the custom name. You may use -v for verbose information.

![](images/00709.jpeg){.image2}

3[.]{.c19}List the logical volume information:

![](images/00710.jpeg){.image2}

Both logical volumes are listed in the output with their attributes and
sizes.

4[.]{.c19}Display detailed information about the volume group including
the logical volumes and the physical volumes:

![](images/00711.jpeg){.image2}

Alternatively, you can run the following to view only the logical volume
details:

![](images/00712.jpeg){.image2}

Review the attributes of the logical volumes as detailed above.

**[Exercise]{#part0026_split_001.html#id_386 .calibre10} 14-3: Extend a
Volume Group and a Logical Volume**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will add another partition *sdd2* of size 158MB to
*vgbook* to increase the pool of allocatable space. You will initialize
the new partition prior to adding it to the volume group. You will
increase the size of *lvbook1* to 336MB. You will display basic
information for the physical volumes, volume group, and logical volume.

1[.]{.c19}Create a partition of size 158MB on *sdd* and set the flag to
"lvm" using the *parted* command. Display the new partition to confirm
the partition number, size, and flag.

![](images/00713.jpeg){.image2}

2[.]{.c19}Initialize *sdd2* using the *pvcreate* command:

![](images/00714.jpeg){.image2}

3[.]{.c19}Extend *vgbook* by adding the new physical volume to it:

![](images/00715.jpeg){.image2}

4[.]{.c19}List the volume group:

![](images/00716.jpeg){.image2}

The output reflects the addition of a third physical volume to *vgbook*.
The total capacity of the volume group has now increased to 464MB with
144MB free.

5[.]{.c19}Extend the size of *lvbook1* to 340MB by adding 144MB using
the *lvextend* command:

![](images/00717.jpeg){.image2}

[**EXAM TIP:**]{.c56} Make sure the expansion of a logical volume does
not affect the file system and the data it contains. More details in
Chapter 15.

6[.]{.c19}Issue *vgdisplay* on *vgbook* with the -v switch for the
updated details:

![](images/00718.jpeg){.image2}

The output will show a lot of information about the volume group and the
logical and physical volumes it contains. It will reflect the updates
made in this exercise. In fact, each time a volume group or a logical
volume is resized, *vgdisplay* will reflect those changes. The above
output will display three physical volumes with the combined allocatable
space grown to 464MB. The number of PEs will have increased to 29, with
all of them allocated to logical volumes and 0 unused. The Logical
Volume sections will display the updated information for the logical
volumes. And at the very bottom, the three physical volumes will show
with their device names, and total and available PEs in each.

7[.]{.c19}View a summary of the physical volumes:

![](images/00719.jpeg){.image2}

8[.]{.c19}View a summary of the logical volumes:

![](images/00720.jpeg){.image2}

This brings the exercise to an end.

**[Exercise]{#part0026_split_001.html#id_387 .calibre10} 14-4: Rename,
Reduce, Extend, and Remove Logical Volumes**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will rename *lvol0* to *lvbook2*. You will
decrease the size of *lvbook2* to 50MB using the *lvreduce* command and
then add 32MB with the *lvresize* command. You will then remove both
logical volumes. You will display the summary for the volume groups,
logical volumes, and physical volumes.

1[.]{.c19}Rename *lvol0* to *lvbook2* using the *lvrename* command and
confirm with *lvs*:

![](images/00721.jpeg){.image2}

2[.]{.c19}Reduce the size of *lvbook2* to 50MB with the *lvreduce*
command. Specify the absolute desired size for the logical volume.
Answer "Do you really want to reduce vgbook/lvbook2?" in the
affirmative.

![](images/00722.jpeg){.image2}

3[.]{.c19}Add 32MB to *lvbook2* with the *lvresize* command:

![](images/00723.jpeg){.image2}

4[.]{.c19}Use the *pvs*, *lvs*, *vgs*, and *vgdisplay* commands to view
the updated allocation.

5[.]{.c19}Remove both *lvbook1* and *lvbook2* logical volumes using the
*lvremove* command. Use the -f option to suppress the "Do you really
want to remove active logical volume" message.

![](images/00724.jpeg){.image2}

![](images/00002.jpeg){.image} Removing a logical volume is a
destructive task. You need to ensure that you perform a backup of any
data in the target logical volume prior to deleting it. You will need to
unmount the file system or disable swap in the logical volume. See
[Chapter 15](#part0027_split_000.html#page_345){.calibre5} on how to
unmount a file system and disable swap.

6[.]{.c19}Execute the *vgdisplay* command and *grep* for "Cur LV" to see
the number of logical volumes currently available in *vgbook*. It should
show 0, as you have removed both logical volumes.

![](images/00725.jpeg){.image2}

This concludes the exercise.

**[Exercise]{#part0026_split_001.html#id_388 .calibre10} 14-5: Reduce
and Remove a Volume Group**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will reduce *vgbook* by removing the *sdd1* and
*sde* physical volumes from it, and then remove the volume group.
Confirm the deletion of the volume group and the logical volumes at the
end.

1[.]{.c19}Remove *sdd1* and *sde* physical volumes from *vgbook* by
issuing the *vgreduce* command:

![](images/00726.jpeg){.image2}

2[.]{.c19}Remove the volume group using the *vgremove* command. This
will also remove the last physical volume, *sdd2*, from it.

![](images/00727.jpeg){.image2}

![](images/00002.jpeg){.image} You can also use the -f option with the
*vgremove* command to force the volume group removal even if it contains
any number of logical and physical volumes in it.

![](images/00002.jpeg){.image} Remember to proceed with caution whenever
you perform reduce and erase operations.

3[.]{.c19}Execute the *vgs* and *lvs* commands for confirmation:

![](images/00728.jpeg){.image2}

This concludes the exercise.

**[Exercise]{#part0026_split_001.html#id_389 .calibre10} 14-6:
Uninitialize Physical Volumes**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will uninitialize all three physical
volumes---*sdd1*, *sdd2*, and *sde*---by deleting the LVM structural
information from them. Use the *pvs* command for confirmation. Remove
the partitions from the *sdd* disk and verify that all disks used in
Exercises 14-1 to 14-5 are now in their original raw state.

1[.]{.c19}Remove the LVM structures from *sdd1*, *sdd2*, and *sde* using
the *pvremove* command:

![](images/00729.jpeg){.image2}

2[.]{.c19}Confirm the removal using the *pvs* command:

![](images/00730.jpeg){.image2}

The partitions and the disk are now back to their raw state and can be
repurposed.

3[.]{.c19}Remove the partitions from *sdd* using the *parted* command:

![](images/00731.jpeg){.image2}

4[.]{.c19}Verify that all disks used in previous exercises have returned
to their original raw state using the *lsblk* command:

![](images/00732.jpeg){.image2}

This brings the exercise to an end.

We will recreate logical volumes in [Chapter
15](#part0027_split_000.html#page_345){.calibre5} and construct file
system and swap structures in them.

**[Stratis]{#part0026_split_001.html#id_390 .calibre10} Volume-Managing
File System**

RHEL 8 introduces a new simplified storage management solution called
*Stratis*. Stratis capitalizes on three existing matured storage
components: the *device mapper* (dm) kernel driver, the LVM solution,
and the XFS file system. It implements the advanced features of these
components to deliver file systems that are encapsulated within logical
volumes. These logical volumes are created and expanded dynamically and
transparently, hiding the underlying complexity. The Stratis solution
delivers file systems that are referred to as *volume-managing file
systems*. Stratis uses the thin provisioning technology as part of the
solution.

![](images/00002.jpeg){.image} File systems are explained in [Chapter
15](#part0027_split_000.html#page_345){.calibre5} "Local File Systems
and Swap".

The central idea surrounding the Stratis solution is a storage *pool*. A
storage pool is created using at least one disk or partition, which is
referred to as a *blockdev*. There can be a combination of the two in a
single pool and more can be added as the space requirement grows. The
total capacity of the pool is the aggregate of the spaces taken from all
the block devices that are part of the pool. Within a pool, *file
systems* can be created, all sharing the entire pool capacity.

![](images/00002.jpeg){.image} LVM logical volumes can also be used as
block devices in a Stratis pool.

[Figure 14-2](#part0026_split_001.html#id_679){.calibre5} provides a
bird's-eye view of the three major objects---pool, blockdev, and file
system---used in Stratis.

::: c49
::: width_
![](images/00733.jpeg){.calibre13}
:::

**Figure 14-2 Stratis Structure**
:::

The diagram in [Figure 14-2](#part0026_split_001.html#id_679){.calibre5}
shows a pool containing multiple disks and partitions. The pool capacity
is the aggregate of all the block storage devices included in the pool,
and this capacity is shared among all the file systems. Each Stratis
file system appears to occupy the entire pool capacity exclusively;
however, they are thinly provisioned. Their actual size grows as the
amount of data stored in them increases. Stratis takes care of the
dynamic expansion of the file systems and the underlying volumes as
needed. As Stratis handles the creation, formatting, and expansion of
the file systems, they must not be manually initialized or reconfigured.

**Stratis Management Operations and Command**

The primary command to manage Stratis is called *stratis*. This command
has a set of subcommands available to perform management operations such
as creating, viewing, renaming, and destroying pools and file systems,
and expanding pools.

[Table 14-2](#part0026_split_001.html#id_742){.calibre5} summarizes the
common Stratis subcommands that are employed to accomplish various
management tasks.

::: c49
  ------------- ------------------------------------------------------------------------------------------------------------------------------
  **Command**   **Description**
  pool          Administers storage pools. Subcommands are available to list, create, rename, expand, and destroy a pool.
  blockdev      Lists block devices
  filesystem    Administers file systems within storage pools. Subcommands are available to list, create, rename, and destroy a file system.
  ------------- ------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0026_split_001.html#id_742} 14-2 Common Stratis
Subcommands**
:::

Stratis runs as a service, so its operational state can be managed with
the *systemctl* command. The *stratis* command interacts with the
Stratis service to manage the pool and file systems dynamically.

For each pool added, Stratis creates a subdirectory under the */stratis*
directory matching the pool name. It then creates a symbolic link for
each file system under that subdirectory to the actual device file
located in the */dev* directory.

Stratis file systems are not fixed-sized; however, pool space can be
reserved to assure availability if multiple file systems share a pool.

**[Exercise]{#part0026_split_001.html#id_391 .calibre10} 14-7: Install
Software and Activate Stratis**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will install the Stratis software packages, start
the Stratis service, and mark it for autostart on subsequent system
reboots.

1[.]{.c19}Install the packages *stratisd* and *stratis-cli*:

![](images/00734.jpeg){.image2}

2[.]{.c19}Start the service and enable it to start automatically on
future system reboots:

![](images/00735.jpeg){.image2}

3[.]{.c19}Check the operational status of the service:

![](images/00736.jpeg){.image2}

The relevant packages for the Stratis storage management solution are
installed, and the Stratis service is started and activated. This
concludes the exercise.

**[Exercise]{#part0026_split_001.html#id_392 .calibre10} 14-8: Create
and Confirm a Pool and File System**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will create a Stratis pool and a file system in
it. You will display information about the pool, file system, and device
used.

1[.]{.c19}You allocated 2x1GB disks: *sdg* and *sdh* for Stratis
exercises. Use the *lsblk* command to confirm their availability:

![](images/00737.jpeg){.image2}

The 2x1GB disks are available and unused.

2[.]{.c19}Create a pool called *bookpool* using the *sdg* disk and
verify the creation:

![](images/00738.jpeg){.image2}

The specified pool *bookpool* is created. The second command output
returns the basic information about the pool, including the number of
physical devices used in the pool and their sizes, and the amount of
in-use space in MiBs.

3[.]{.c19}Display the block device that is used to form the pool:

![](images/00739.jpeg){.image2}

The pool *bookpool* has a single disk of size 1GiB and it is currently
in use.

4[.]{.c19}Create a file system called *bookfs* in the *bookpool* and
verify the creation:

![](images/00740.jpeg){.image2}

The pool *bookpool* has a single file system *bookfs* of used size
546MiB. Its device file is **stratis*bookpool/bookfs*. The file system's
UUID is also displayed.

5[.]{.c19}Create a directory called */bookfs1* and mount the new file
system on it:

![](images/00741.jpeg){.image2}

6[.]{.c19}Check the pool usage:

![](images/00742.jpeg){.image2}

Observe how the usage grew from 52MiB to 598MiB. This brings this
exercise to an end.

**[Exercise]{#part0026_split_001.html#id_393 .calibre10} 14-9: Expand
and Rename a Pool and File System**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will expand the Stratis pool *bookpool* (created
in [Exercise 14-8](#part0026_split_001.html#id_392){.calibre5}) using
the *sdh* disk. You will rename the pool and the file system it
contains.

1[.]{.c19}Expand the *bookpool* pool by adding the *sdh* disk to it:

![](images/00743.jpeg){.image2}

2[.]{.c19}Verify the new capacity of the pool:

![](images/00744.jpeg){.image2}

The addition of another 1GB disk brings the total physical size to 2GiB.

3[.]{.c19}Change the name of the pool from *bookpool* to *rhcsapool* and
verify:

![](images/00745.jpeg){.image2}

The new name is depicted in the first column.

4[.]{.c19}Change the name of the file system from *bookfs* to *rhcsafs*,
and verify:

![](images/00746.jpeg){.image2}

The file system name is changed and it's reflected in the output of the
second command. The exercise is completed successfully.

**[Exercise]{#part0026_split_001.html#id_394 .calibre10} 14-10: Destroy
a File System and Pool**

This exercise should be done on *server2* as *user1* with *sudo* where
required.

In this exercise, you will destroy the Stratis file system and the pool
that was created, expanded, and renamed in Exercises 14-8 and 14-9. You
will verify the deletion with appropriate commands.

1[.]{.c19}The first step in the process is to unmount the file system
*rhcsafs1* from its mount point */bookfs1*:

![](images/00747.jpeg){.image2}

Unmounting a file system ensures that the file system is not busy.

2[.]{.c19}Remove the file system *rhcsafs* from the pool:

![](images/00748.jpeg){.image2}

3[.]{.c19}Remove the pool *rhcsapool* from the system:

![](images/00749.jpeg){.image2}

4[.]{.c19}Confirm the removal of the file system and the pool:

![](images/00750.jpeg){.image2}

The above outputs confirm the removal of the file system and the pool.

5[.]{.c19}Verify that both *sdg* and *sdh* disks used in the previous
Stratis exercises have returned to their original raw state using the
*lsblk* command:

![](images/00751.jpeg){.image2}

This concludes the exercise.

We will recreate Stratis file systems in [Chapter
15](#part0027_split_000.html#page_345){.calibre5} and add them for
persistent mounting.

**[Chapter]{#part0026_split_001.html#id_395 .calibre10} Summary**

This chapter explicated two advanced storage management solutions:
Logical Volume Manager and Stratis. The LVM solution has been around in
RHEL for decades. The Stratis solution, on the other hand, is recently
added.

We discovered how LVM works. We looked at various LVM objects and their
relationship with one another. We explored LVM management commands and
common options available with them. We performed a series of exercises
to demonstrate the creation, expansion, renaming, reduction, and
deletion of physical volumes, storage pools, and logical volumes.

The next advanced storage solution we looked at is called Stratis, which
is a volume-managing file system. Stratis takes advantage of the
underlying LVM functionality and the device mapper kernel driver to
create and expand the XFS file system that it holds. Stratis dynamically
expands the underlying LVM volume without the need for manual
administrative intervention. We executed a couple of step-by-step
exercises to explain the creation, growth, renaming, and removal of
Stratis pools and file systems.

**[Review]{#part0026_split_001.html#id_396 .calibre10} Questions**

1[.]{.c19}The *parted* utility may be used to create LVM logical
volumes. True or False?

2[.]{.c19}What are the two commands that you can use to reduce the
number of logical extents from a logical volume?

3[.]{.c19}Stratis uses LVM as the underlying logical volume management
solution. True or False?

4[.]{.c19}Provide the command to add physical volumes **dev*sdd1* and
**dev*sdc* to *vg20* volume group.

5[.]{.c19}What are the two commands that you can use to add logical
extents to a logical volume?

6[.]{.c19}Provide the command to create a volume group called *vg20* on
**dev*sdd* disk with physical extent size 64MB.

7[.]{.c19}Name the three Stratis objects?

8[.]{.c19}Provide the command to remove *vg20* along with logical and
physical volumes it contains.

9[.]{.c19}What is the default size of a physical extent in LVM?

10[.]{.c23}What is the default name for the first logical volume in a
volume group?

11[.]{.c23}What is one difference between the *pvs* and *pvdisplay*
commands?

12[.]{.c23}When can a disk or partition be referred to as a physical
volume?

13[.]{.c23}Provide the command to remove *webvol* logical volume from
*vg20* volume group.

14[.]{.c23}It is necessary to create file system structures in a logical
volume before it can be used to store files in it. True or False?

15[.]{.c23}What would the command *stratis pool create pool1 *dev*sdg*
do?

16[.]{.c23}Physical and logical extents are typically of the same size.
True or False?

17[.]{.c23}What is the purpose of the *pvremove* command?

18[.]{.c23}What would the command *pvcreate *dev*sdd* do?

19[.]{.c23}A disk or partition can be added to a volume group without
being initialized. True or False?

20[.]{.c23}What is the file system type that is created in a Stratis
file system?

21[.]{.c23}Provide the command to create a logical volume called
*webvol* of size equal to 100 logical extents in *vg20* volume group.

22[.]{.c23}A volume group can be created without any physical volume in
it. True or False?

23[.]{.c23}A single disk can be used by both *parted* and LVM solutions
at the same time. True or False?

24[.]{.c23}Provide the command to add **dev*sdh* to an existing pool
called *pool1*.

25[.]{.c23}Provide the command to erase **dev*sdd1* physical volume from
*vg20* volume group.

26[.]{.c23}A partition can be used as an LVM object. True or False?

27[.]{.c23}Which command would you use to view the details of a volume
group and its objects?

**[Answers]{#part0026_split_001.html#id_397 .calibre10} to Review
Questions**

1[.]{.c19}False.

2[.]{.c19}The *lvreduce* and *lvresize* commands.

3[.]{.c19}True.

*4[.]{.c19}vgextend vg20 *dev*sdd1 *dev*sdc*

5[.]{.c19}The *lvextend* and *lvresize* commands.

*6[.]{.c19}vgcreate -s 64 vg20 *dev*sdd*

7[.]{.c19}The three Stratis objects are pool, block device, and file
system.

*8[.]{.c19}vgremove -f vg20*

9[.]{.c19}The default PE size is 4MB.

10[.]{.c23}*lvol0* is the default name for the first logical volume
created in a volume group.

11[.]{.c23}The *pvs* command lists basic information about physical
volumes whereas the *pvdisplay* command shows the details.

12[.]{.c23}After the *pvcreate* command has been executed on it
successfully.

*13[.]{.c23}lvremove *dev*vg20/webvol*

14[.]{.c23}True.

15[.]{.c23}The command provided will create a Stratis pool called
*pool1* containing **dev*sdg* device.

16[.]{.c23}True.

17[.]{.c23}The *pvremove* command is used to remove LVM information from
a physical volume.

18[.]{.c23}The command provided will prepare the **dev*sdd* disk for use
in a volume group.

19[.]{.c23}False. A disk or partition must be initialized before it can
be added to a volume group.

20[.]{.c23}XFS.

*21[.]{.c23}lvcreate -l 100 -n webvol vg20*

22[.]{.c23}False.

23[.]{.c23}True. A single disk can be shared between *parted*-created
partitions and LVM.

*24[.]{.c23}stratis pool add-data pool1 *dev*sdh*

*25[.]{.c23}vgreduce vg20 *dev*sdd1*

26[.]{.c23}True.

27[.]{.c23}The *vgdisplay* command with the -v option.

**[Do-]{#part0026_split_001.html#id_398 .calibre10}It-Yourself Challenge
Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

Add more storage to *server2* if required.

**[Lab]{#part0026_split_001.html#id_399 .calibre10} 14-1: Create Volume
Group and Logical Volumes**

As *user1* with *sudo* on *server2*, initialize 1x250MB disk for use in
LVM (use *lsblk* to identify available disks). Create volume group
*vg100* with PE size 16MB and add the physical volume. Create two
logical volumes *lvol0* and *swapvol* of sizes 100MB and 120MB. Use the
*vgs*, *pvs*, *lvs*, and *vgdisplay* commands for verification. (Hint:
Logical Volume Manager).

**[Lab]{#part0026_split_001.html#id_400 .calibre10} 14-2: Expand Volume
Group and Logical Volume**

As *user1* with *sudo* on *server2*, create a partition on an available
250MB disk and initialize it for use in LVM (use *lsblk* to identify
available disks). Add the new physical volume to *vg100*. Expand the
*lvol0* logical volume to size 300MB. Use the *vgs*, *pvs*, *lvs*, and
*vgdisplay* commands for verification. (Hint: Logical Volume Manager).

**[Lab]{#part0026_split_001.html#id_401 .calibre10} 14-3: Reduce and
Remove Logical Volumes**

As *user1* with *sudo* on *server2*, reduce the size of *lvol0* logical
volume to 80MB. Then erase both logical volumes *swapvol* and *lvol0*.
Confirm the deletion with *vgs*, *pvs*, *lvs*, and *vgdisplay* commands.
(Hint: Logical Volume Manager).

**[Lab]{#part0026_split_001.html#id_402 .calibre10} 14-4: Remove Volume
Group and Physical Volumes**

As *user1* with *sudo* on *server2*, remove the volume group and
uninitialized the physical volumes. Confirm the deletion with *vgs*,
*pvs*, *lvs*, and *vgdisplay* commands. Use the *lsblk* command and
verify that the disks used for the LVM labs no longer show LVM
information. (Hint: Logical Volume Manager).

**[Lab]{#part0026_split_001.html#id_403 .calibre10} 14-5: Create Stratis
Pool**

As *user1* with *sudo* on *server2*, check to see if Stratis software is
installed and the Stratis service is enabled and started. Identify 2x1GB
disks with the *lsblk* command and ensure they are not in use. Create
pool *strpool* on one of the 1GB disks and verify the pool and the block
device with the *stratis* command. (Hint: Stratis Volume-Managing File
System).

**[Lab]{#part0026_split_001.html#id_404 .calibre10} 14-6: Expand and
Destroy Stratis Pool**

As *user1* with *sudo* on *server2*, use the other 1GB disk and expand
*strpool* using the *stratis* command. Verify the expansion. Finally,
remove the entire pool and confirm the deletion. Use the *lsblk* command
and verify that the disks used for the Stratis labs no longer show
Stratis information. (Hint: Stratis Volume-Managing File System).

[]{#part0027_split_000.html}
