Same tools for mounting and unmounting a filesystem.
- Mounted and accessed the same way as local filesystems.
- Network protocol that allows file sharing over the network.
- Multi-platform
- Multiple clients can access a single share at the same time.
- Reduced overhead and storage cost.
- Give users access to uniform data.
- Consolidate scattered user home directories.
- May cause client to hang if share is not accessible.
- Share stays mounted until manually unmounted or the client shuts down.
- Does not support wildcard characters or environment variables.

## NFS Supported versions

- RHEL 8 Supports versions 3,4.0,4.1, and 4.2 (default)
- NFSv3 supports: 
  - TCP and UDP.
  - asynchronous writes.
  - 64-bit files sizes.
  - Access files larger than 2GB.
- NFSv4.x supports: 
  - All features of NFSv3.
  - Transit firewalls and work on internet.
  - Enhanced security and support for encrypted transfers and ACLs.
  - Better scalability
  - Better cross-platform
  - Better system crash handling
  - use usernames and group names rather than UID and GID.
  - Uses TCP by default.
  - Can use UDP for backwards compatibility.
  - Version 4.2 only supports TCP

## Network File System service

- Export shares to mount on remote clients
- Exporting 
  - When the NFS server makes shares available.
- Mounting 
  - When a client mounts an exported share locally.
  - Mount point should be empty before trying to mount a share on it.
- System can be both client and server.
- Entire directory tree of the share is shared.
- Cannot re-share a subdirectory of a share.
- A mounted share cannot be exported from the client.
- A single exported share is mounted on a directory mount point.
- Make sure to update the fstab file on the client.

## NFS Server and Client Configuration

### How to export a share

- Add entry of the share to /etc/exports using exportfs command
- Add firewall rule to allow access

### Mount a share from the client side

- Use mount and add the filesystem to the fstab file.

## AutoFS

- Automatically mount and unmount on clients during runtime and system reboots.
- Triggers mount or unmount action based on mount point activity.
- Client-side service
- Mount an NFS share on demand
- Entry placed in AutoFS config files.
- Automatically mounts share upon detecting activity in it's mount point. (touch, ls, cd)
- unmounts share if the share hasn't been accessed for a predefined period of time.
- Mounts managed with autofs should not be mounted manually via /etc/fstab to avoid inconsistencies.
- Saves Kernel from having to maintain unused NFS shares. (Improved performance!)
- NFS shares are defined in config files called maps (/etc/ or /etc/auto.master.d/)
- Does not use /etc/fstab.
- Does not require root to mount a share (fstab does).
- Prevents client from hanging if share is down.
- Share is unmounted if not accessed for 5 minutes (default)
- Supports wildcard characters or environment variables.
- Automount daemond 
  - in the userland mounts configured shares automatically upon access.
  - invoked at system boot.
  - Reads AutoFS master map and create inititial mount point entries. (not mounting yet)
  - Does not mount shares until user activity is detected.
  - Unmounts after set timeframe of inactivity.
- Use the mount command on a share to verify the path of the AutoFS map, file system type, and options used during mount.

/etc/autofs.conf/ preset Directives:
master_map_name=auto.master
timeout = 300
negative_timeout = 60
mount_nfs_default_protocol = 4
logging = none

Additional directives:
master_map_name
\- Name of the master map. Default is /etc/auto.master
timeout
\- time in second to unmount a share.
negative_timeout
\- Timeout (in seconds) value for failed mount attempts. (1 minute default)
mount_nfs_default_protocol
\- Sets the NFS version used to mount shares.
logging
\- Logging level (none, verbose, debug)
\- Default is none (disabled)

- Normally left to their default values.

AutoFS Maps

- Where AutoFS finds the shares to mount and their locations.
- Also tells Autofs what options to use. Map Types
- master
- direct
- indirect

Master Map

- /etc/auto.master is default
- Default is defined in /etc/autofs.conf with master_map_name directive.
- May be used to define entries for indirect and direct maps. 
  - But it is recommended to store user-defined maps in /etc/auto.master.d/ 
    - AutoFS service parses this at startup.
- You can append an option to auto.master but it will apply globally to all subentries in the specified map file.

Map entry format examples:

### Direct Map

```
/- /etc/auto.master.d/auto.direct <-- defines direct map and points to auto.direct for details
```

- Mount shares on any number of unrelated mount points
- Always visible to users
- Can exist with an indirect share under one parent directory
- Accessing a directory containing many direct mount points mounts all shares.
- Each direct map entry places a separate share entry to /etc/mtab 
  - /etc/mtab maintains a list of all mounted file systems whether they are local or remote.
  - Updated whenever a local file system, removable file system, or aq network share is mounted or unmounted.

### Indirect Map

```
/misc /etc/auto.misc <-- indirect map and points to auto.misc for details
```

- Umbrella mount point /misc will precede all mount point entries listed in /etc/auto.misc
- Used to automount removable file systems (CD, DVD, USB disks, etc.)
- Custom indirect map files shouold be located in /etc/auto.master.d/
- Preferred over direct mount for mounting all shares under one common parent directory.
- Become visible only after they have been accessed.
- Local and indirect mounted shares cannot coexist under the same parent directory.
- One entry in /etc/mtab gets added for each indirect map.
- Accessing a directory containing many indirect mount points shows only the shares that are already mounted.
- Usually better to use indirect map for automounting NFS shares.

## Lab: Export Share on NFS Server

1. Install nfs-utils

```
sudo dnf -y install nfs-utils
```

1. Create /common

```
sudo mkdir /common
```

1. Add full permissions

```
sudo chmod 777 /common
```

1. Add NFS service persistently to the firewalld configuration to allow NFS traffic and load the new rule:

```
sudo firewall-cmd --permanent --add-service nfs
sudo firewall-cmd --reload
```

1. Start the NFS service and enable it to autostart at system reboots:

```
sudo systemctl --now enable nfs-server
```

1. Verify Operational Status of the NFS services:

```
sudo systemctl status nfs-server
```

1. Open /etc/exports and add entry for /common to export it to server10 with read/write:

```
/common server10(rw)
```

1. Export the entry defined in /etc/exports. -a option exports all entries in the file. -v is verbose.

```
sudo exportfs -av
```

1. Unexport the share (-u):

```
sudo exportfs -u server10:/common
```

1. Re-export the share:

```
sudo exportfs -av
```

LAB: Mount share on NFS client

1. Install nfs-utils

```
sudo dnf -y install nfs-utils
```

1. Create /local mount point

```
sudo mkdir /local
```

1. Mount the share manually:

```
sudo mount server20:/common /local
```

1. Confirm using mount: (shows nfs version)

```
mount | grep local
```

1. Confirm using df:

```
df -h | grep local
```

1. Add to /fstab for persistence:

```
server20:/common /local nfs _netdev 0 0
```

Note:

```
_netdev option makes system wait for networking to come up before trying to mount the share. 
```

1. Unmount share manually using umount then remount to validate accuracy of the entry in /fstab:

```
sudo umount /local
sudo mount -a
```

1. Verify:

```
df -h
```

1. Create a file in /local/ and verify:

```
touch /local/nfsfile
ls -l /local
```

1. Confirm the sync on server 2

```
ls -l /common/
```

## Lab: Access NFS Share Using Direct Map

1. Install Autofs

```
sudo dnf install -y autofs
```

1. Create mount point /autodir using mkdir

```
sudo mkdir /autodir
```

1. Add an entry to /etc/auto.master to point the AutoFS service to the auto.dir file for more information:

```
/- /etc/auto.master.d/auto.dir
```

1. Create /etc/auto.master.d/auto.dir and add the mount point, NFS server, and share info:

```
/autodir server20:/common
```

1. Start AutoFS service and enable it at startup:

```
sudo systemctl enable --now autofs
```

1. Make sure AUtoFS service is running. Use -l and --no-pager options to show full details without piping the output to a pager program (pg)

```
sudo systemctl status autofs -l --no-pager
```

1. Run ls on the mount point then verify the share is automounted and accessible with mount.

```
ls /autodir
mount | grep autodir
```

1. Wait 5 minutes and run the mount command again to see it has disappeared.

```
mount | grep autodir
```

## Lab: Access NFS Share Using Indirect Map

## Chapter 16 {style="text-align: right"}

\

### Network File System {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Overview of Network File System service and key components

\

Network File System benefits and versions

\

Export a share on NFS server

\

Mount the share on NFS client using standard mount method

\

Understand the AutoFS service, and its benefits and functioning

\

Analyze AutoFS configuration maps

\

Mount the exported share on NFS client using AutoFS

\

Configure NFS and AutoFS to share and mount user home directories

\

#### RHCSA Objectives:

\

33\. Mount and unmount network file systems using NFS

34\. Configure autofs

::: {style="page-break-before: always;"}
:::

\

Network shares may be mounted on RHEL and accessed the same way as local
file systems. This can be done manually using the same tools that are
employed for mounting and unmounting local file systems. An alternative
solution is to implement the AutoFS service to automatically mount and
unmount them without the need to execute any commands explicitly. AutoFS
monitors activities in mount points based on which it triggers a mount
or unmount action.

\

::: {style="text-align: center;"}
![](image-PZNUOJTO.jpg){height="100%"}
:::

RHEL exports shares using the Network File System service for remote
mounting on clients. A combination of this service and AutoFS/standard
mount is prevalent in real world scenarios. This chapter elaborates on
the benefits of the file sharing solution and expounds upon AutoFS. It
demonstrates a series of exercises to detail the server-side and
client-side configurations. It also explores the automatic mounting of
user home directories on clients.

::: {style="page-break-before: always;"}
:::

[]{#chapter0498.html}

## Network File System {.style3}

\

Network File System (NFS) is a networking protocol that allows file
sharing over the network. The Network File System service is based upon
the client/server architecture whereby users on one system access files,
directories, and file systems (collectively called "shares") that reside
on a remote system as if they are mounted locally on their system. The
remote system that makes its shares available for network access is
referred to as an NFS server, and the process of making the shares
accessible is referred to as exporting. The shares the NFS server
exports may be accessed by one or more systems. These systems are called
NFS clients, and the process of making the shares accessible on clients
is referred to as mounting. See Figure 16-1 for a simple NFS
client/server arrangement that shows two shares---/export1 and
/export2---exported on the network to a remote system, which has them
mounted there.

\

::: {style="text-align: center;"}
![](image-W460VEES.jpg){height="100%"}
:::

Figure 16-1 NFS Server/Client

\

A system can provide both server and client functionality concurrently.
When a directory or file system share is exported, the entire directory
structure beneath it becomes available for mounting on the client. A
subdirectory or the parent directory of a share cannot be re-exported if
it exists in the same file system. Similarly, a mounted share cannot be
exported further. A single exported file share is mounted on a directory
mount point.

::: {style="page-break-before: always;"}
:::

[]{#chapter0499.html}

Benefits of Using NFS

\

The use of NFS provides several benefits, some of which are highlighted
below:

\

Supports a variety of operating system platforms including Linux, UNIX,
and Microsoft Windows.

\

Multiple NFS clients can access a single share simultaneously.

\

Enables the sharing of common application binaries and other read-only
information, resulting in reduced administration overhead and storage
cost.

\

Gives users access to uniform data.

\

Allows the consolidation of scattered user home directories on the NFS
server and then exporting them to the clients. This way users will have
only one home directory to maintain.

::: {style="page-break-before: always;"}
:::

[]{#chapter0500.html}

## NFS Versions {.style3}

\

RHEL 9 provides the support for NFS versions 3, 4.0, 4.1, and 4.2, with
version 4.2 being the default. NFSv3 supports both TCP and UDP transport
protocols, asynchronous writes, and 64-bit file sizes that gives clients
the ability to access files of sizes larger than 2GB.

\

NFSv4.x are Internet Engineering Task Force (IETF) series of protocols
that provide all the features of NFSv3, plus the ability to transit
firewalls and work on the Internet. They provide enhanced security and
support for encrypted transfers, as well as greater scalability, better
cross-platform interoperability, and better system crash handling. They
use usernames and group names rather than UIDs and GIDs for files
located on network shares. NFSv4.0 and NFSv4.1 use the TCP protocol by
default, but can work with UDP for backward compatibility. In contrast,
NFSv4.2 only supports TCP.

::: {style="page-break-before: always;"}
:::

[]{#chapter0501.html}

## NFS Server and Client Configuration {.style3}

\

This section presents two exercises, one demonstrating how to export a
share on a server (NFS server) and the other outlines the steps on
mounting and accessing a share on a remote system (NFS client). The
basic setup of the NFS service is straightforward. It requires adding an
entry of the share to a file named /etc/exports and using a command
called exportfs to make it available on the network. It also requires
the addition of a firewall rule to allow access to the share by NFS
clients.

\

The mount command employed on an NFS client is the same command that was
used in Chapter 14 "Local File Systems and Swap" to mount local file
systems. Moreover, the fstab file requires an entry for the NFS share on
the client for persistent mounting.

\

The exercises in this section illustrate the usage of both commands and
the syntax of both files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0502.html}

## Exercise 16-1: Export Share on NFS Server {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will create a directory called /common and export
it to server10 in read/write mode. You will ensure that NFS traffic is
allowed through the firewall. You will confirm the export.

\

1\. Install the NFS software called nfs-utils:

\

<div>

![](image-Y3HSOQJ1.jpg){height="100%"}

</div>

\

Follow the instructions outlined in "Exercise 9-1: Mount RHEL 9 ISO
Persistently" and "Exercise 10-1: Configure Access to Pre-Built
Repositories" to ensure the above software installation works.

\

2\. Create /common directory to be exported as a share:

\


![](image-9XVK7KG5.jpg){height="100%"}



3\. Add full permissions to /common:

\

<div>

![](image-7FVQ1A64.jpg){height="100%"}

</div>

4\. Add the NFS service persistently to the Linux firewall to allow the
NFS traffic to pass through it, and load the new rule:

\

<div>

![](image-F3QXBPMD.jpg){height="100%"}

</div>

\

Refer to Chapter 19 "The Linux Firewall" for details around the Linux
firewall service.

\

5\. Start the NFS service and enable it to autostart at system reboots:

\

<div>

![](image-Z7KMDEV3.jpg){height="100%"}

</div>

6\. Verify the operational status of the NFS service:

\

<div>

![](image-FLE6D24E.jpg){height="100%"}

</div>

7\. Open the /etc/exports file in a text editor and add an entry for
/common to export it to server10 with read/write option:

\

<div>

![](image-3P396CJ4.jpg){height="100%"}

</div>

8\. Export the entry defined in the /etc/exports file. The -a option
exports all the entries listed in the file and -v displays verbose
output.

\

<div>

![](image-P67WMV3I.jpg){height="100%"}

</div>

The NFS service is now set up on server20 with the /common share
available for mounting on server10 (NFS client in this case).

\

For practice, you can unexport the share by issuing the exportfs command
with the -u flag as follows:

\

<div>

![](image-VF7055NU.jpg){height="100%"}

</div>

Before proceeding, re-export the share using sudo exportfs -av.

::: {style="page-break-before: always;"}
:::

[]{#chapter0503.html}

## Exercise 16-2: Mount Share on NFS Client {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will mount the /common share exported in Exercise
16-1. You will create a mount point called /local, mount the remote
share manually, and confirm the mount. You will add the remote share to
the file system table for persistence. You will remount the share and
confirm the mount. You will create a test file in the mount point and
confirm the file creation on the NFS server (server20).

\

1\. Install the NFS software called nfs-utils:

\

<div>

![](image-VR7N9PHK.jpg){height="100%"}

</div>

2\. Create /local mount point:

\

<div>

![](image-6U8QXI0Z.jpg){height="100%"}

</div>

3\. Mount the share manually using the mount command:

\

<div>

![](image-BKFJJK0I.jpg){height="100%"}

</div>

The remote share is successfully mounted on server10, and it can be
accessed as any other local file system.

\

4\. Confirm the mount using either the mount or the df command:

\

<div>

![](image-40F15W4K.jpg){height="100%"}

</div>

The mount command output returns the NFS protocol version (NFS4.2) and
all the default options used in mounting the share.

\

5\. Open the /etc/fstab file and append the following entry for
persistence:

\

<div>

![](image-D1EFHGXS.jpg){height="100%"}

</div>

\

The \_netdev option will make the system wait for networking to
establish before attempting to mount this share.

\

A mount point should be empty and must not be in use when an attempt is
made to mount a share to it.

\

6\. Unmount the share manually using the umount command and remount it
via the fstab file to validate the accuracy of the entry placed in the
file:

\

<div>

![](image-TORCBQDK.jpg){height="100%"}

</div>

7\. Run mount and df -h again to verify the remounting.

8\. Create a file called nfsfile under /local and verify:

\

<div>

![](image-RMXWFJB1.jpg){height="100%"}

</div>

9\. Confirm the file creation on the NFS server (server20):

\

<div>

![](image-RRSA2THB.jpg){height="100%"}

</div>

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Do not forget to update the /etc/fstab file on the client.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

This completes the setup and testing of mounting, unmounting, and
remounting of an NFS share on the client.

::: {style="page-break-before: always;"}
:::

[]{#chapter0504.html}

## Auto File System (AutoFS) {.style3}

\

In the previous section, you learned how to attach (mount) an NFS share
to the Linux directory tree manually for access by users and
applications on an NFS client. Once attached, the share was treated just
like any other local file system. You also learned how to detach
(unmount) an NFS share manually from the directory tree to make it
inaccessible to users and applications. You placed an entry for the
share in the fstab file to guarantee a remount during system reboots.

\

RHEL offers an alternative way of mounting and unmounting a share on the
clients during runtime as well as system reboots. This feature is
delivered by a service called the Auto File System (AutoFS). AutoFS is a
client-side service, which is employed to mount an NFS share on-demand.
With a proper entry placed in AutoFS configuration files, the AutoFS
service automatically mounts a share upon detecting an activity in its
mount point with a command such as ls or cd. In the same manner, AutoFS
unmounts the share automatically if it has not been accessed for a
predefined period of time.

\

To avoid inconsistencies, mounts managed with AutoFS should not be
mounted or unmounted manually or via the /etc/fstab file.

\

The use of AutoFS saves the kernel from dedicating system resources to
maintain unused NFS shares, resulting in slight improvement in system
performance.

::: {style="page-break-before: always;"}
:::

[]{#chapter0505.html}

## Benefits of Using AutoFS {.style3}

\

There are several benefits associated with using the AutoFS service over
placing entries in the /etc/fstab file. Some of the key benefits are
described below:

\

AutoFS requires that NFS shares be defined in text configuration files
called maps , which are located in the /etc or /etc/auto.master.d
directory. AutoFS does not make use of the /etc/fstab file.

\

AutoFS does not require root privileges to mount an NFS share; manual
mounting and mounting via fstab do require that privilege.

\

AutoFS prevents an NFS client from hanging if an NFS server is down or
inaccessible. With the other method, the unavailability of the NFS
server may cause the NFS client to hang.

\

With AutoFS, a share is unmounted automatically if it is not accessed
for five minutes by default. With the fstab method, the share stays
mounted until it is either manually unmounted or the client shuts down.

\

\### AutoFS supports wildcard characters and environment variables,
which the other method does not support.

::: {style="page-break-before: always;"}
:::

[]{#chapter0506.html}

## How AutoFS Works {.style3}

\

The AutoFS service consists of a daemon called automount in the userland
that mounts configured shares automatically upon access. This daemon is
invoked at system boot. It reads the AutoFS master map and creates
initial mount point entries, but it does not mount any shares yet. When
the service detects a user activity under a mount point during runtime,
it mounts the requested file system at that time. If a share remains
idle for a certain time period, automount unmounts it by itself.

::: {style="page-break-before: always;"}
:::

[]{#chapter0507.html}

## AutoFS Configuration File {.style3}

\

The configuration file for the AutoFS service is /etc/autofs.conf, which
AutoFS consults at service startup. Some key directives from this file
are shown below along with preset values:

\

master_map_name = auto.master

timeout = 300

negative_timeout = 60

mount_nfs_default_protocol = 4

logging = none

\

There are additional directives available in this file and more can be
added to modify the default behavior of the AutoFS service. Table 16-1
describes the above directives.

\

  ----------------------------------- -----------------------------------
  Directive                           Description

  master_map_name                     Defines the name of the master map.
                                      The default is auto.master located
                                      in the /etc directory.

  timeout                             Specifies, in seconds, the maximum
                                      idle time after which a share is
                                      automatically unmounted. The
                                      default is five minutes.

  negative_timeout                    Expresses, in seconds, a timeout
                                      value for failed mount attempts.
                                      The default is one minute.

  mount_nfs_default_protocol          Sets the default NFS version to be
                                      used to mount shares.

  logging                             Configures a logging level. Options
                                      are none, verbose, and debug. The
                                      default is none (disabled).
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 16-1 AutoFS Directives

\

The directives in the autofs.conf file are normally left to their
default values, but you can alter them if required.

::: {style="page-break-before: always;"}
:::

[]{#chapter0508.html}

## AutoFS Maps {.style3}

\

The AutoFS service needs to know the NFS shares to be mounted and their
locations. It also needs to know any specific options to use with
mounting them. This information is defined in AutoFS files called maps.
There are three common AutoFS map types: master, direct, and indirect.

\

### The Master Map {.style3}

The auto.master file located in the /etc directory is the default master
map, as defined in the /etc/autofs.conf configuration file with the
master_map_name directive. This map may be used to define entries for
direct and indirect maps. However, it is recommended to store
user-defined map files in the /etc/auto.master.d directory, which the
AutoFS service automatically parses at startup. The following presents
two samples to explain the format of the map entries:

\

  ----------------------- -------------------------------- -----------------------
  /-                      /etc/auto.master.d/auto.direct   \# Line 1

  /misc                   /etc/auto.misc                   \# Line 2
  ----------------------- -------------------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

The two entries are explained below.

\

### The Direct Map {.style3}

The direct map is used to mount shares automatically on any number of
unrelated mount points. Some key points to note when working with direct
maps are:

\

Direct mounted shares are always visible to users.

\

Local and direct mounted shares can coexist under one parent directory.

\

Accessing a directory containing many direct mount points mounts all
shares.

\

Each direct map entry places a separate share entry to the /etc/mtab
file, which maintains a list of all mounted file systems whether they
are local or remote. This file is updated whenever a local file system,
removable file system, or a network share is mounted or unmounted.

\

Line 1 from above defines a direct map and points to the
/etc/auto.master.d/auto.direct file for mount details.

\

You may append an option to the line entry in the auto.master file
above; however, that option will apply to all subentries in the
specified map file.

\

### The Indirect Map {.style3}

The indirect map is preferred over the direct map if you want to mount
all shares under one common parent directory. Some key points to note
when working with indirect maps are:

\

Indirect mounted shares become visible only after they have been
accessed.

\

Local and indirect mounted shares cannot coexist under the same parent
directory.

\

Each indirect map puts only one entry in the /etc/mtab mount table.

\

Accessing a directory containing many indirect mount points shows only
the shares that are already mounted.

\

Line 2 from above represents an indirect map, notifying AutoFS to refer
to the /etc/auto.misc file for mount details. The umbrella mount point
/misc will precede all mount point entries listed in the /etc/auto.misc
file. This indirect map entry is normally used to automount removable
file systems, such as CD, DVD, external USB disks, and so on. Any custom
indirect map file should be located in the /etc/auto.master.d directory.

\

You may append an option to the corresponding line entry in the
auto.master file above; however, that option will apply to all
subentries in the specified map file.

\

### Direct Map vs. Indirect Map {.style3}

Both direct and indirect maps have their own merits and demerits. By
comparing their features, it seems more prudent to use the indirect map
for automounting NFS shares. However, this statement may not be true for
every environment, as there could be specifics that would dictate which
option to go with.

::: {style="page-break-before: always;"}
:::

[]{#chapter0509.html}

## Exercise 16-3: Access NFS Share Using Direct Map {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will configure a direct map to automount the NFS
share /common that is available from server20. You will install the
relevant software, create a local mount point /autodir, and set up
AutoFS maps to support the automatic mounting. Note that /common is
already mounted to /local on server10 (NFS client) via the fstab file.
There should not be any conflict in configuration or functionality
between the two.

\

1\. Install the AutoFS software package called autofs:

\

<div>

![](image-JV0VLRKV.jpg){height="100%"}

</div>

2\. Create a mount point /autodir using the mkdir command:

\

<div>

![](image-WX4PVBAM.jpg){height="100%"}

</div>

3\. Edit the /etc/auto.master file and add the following entry at the
beginning of the file. This entry will point the AutoFS service to the
auto.dir file for additional information.

\

<div>

![](image-25VG0T6I.jpg){height="100%"}

</div>

4\. Create /etc/auto.master.d/auto.dir file and add the mount point, NFS
server, and share information to it:

\

<div>

![](image-D1DBM7Z4.jpg){height="100%"}

</div>

5\. Start the AutoFS service now and set it to autostart at system
reboots:

\

<div>

![](image-217ZEA7U.jpg){height="100%"}

</div>

6\. Verify the operational status of the AutoFS service. Use the -l and
\--no-pager options to show full details without piping the output to a
pager program (the pg command in this case).

\

<div>

![](image-5ZDWYN76.jpg){height="100%"}

</div>

7\. Run the ls command on the mount point /autodir and then issue the
mount command to verify that the share is automounted and accessible:

\

<div>

![](image-BVSYBB5B.jpg){height="100%"}

</div>

Observe the above outcomes. An activity in the mount point (the ls
command) caused AutoFS to mount the share /common on /autodir. The mount
command output depicts the path of the AutoFS map
(/etc/auto.master.d/auto.dir), the file system type (autofs), and the
options used during the mount process. Wait for five minutes and run the
mount command again. You'll see that the auto file system has
disappeared. A cd, ls, or another activity in the mount point will bring
it back.

\

This completes the AutoFS setup for an NFS share on the client using a
direct map.

::: {style="page-break-before: always;"}
:::

[]{#chapter0510.html}

## Exercise 16-4: Access NFS Share Using Indirect Map {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will configure an indirect map to automount the
NFS share /common that is available from server20. You will install the
relevant software and set up AutoFS maps to support the automatic
mounting. You will observe that the specified mount point "autoindir" is
created automatically under /misc.

\

Note that /common is already mounted on the /local mount point via the
fstab file and it is also configured via a direct map for automounting
on /autodir. There should occur no conflict in configuration or
functionality among the three.

\

1\. Install the autofs software package if it is not already there:

\

<div>

![](image-5ZCH4XO4.jpg){height="100%"}

</div>

2\. Confirm the entry for the indirect map /misc in the /etc/auto.master
file exists:

\

<div>

![](image-RB8VLK54.jpg){height="100%"}

</div>

3\. Edit the /etc/auto.misc file and add the mount point, NFS server,
and share information to it:

\

<div>

![](image-NJSLAQTL.jpg){height="100%"}

</div>

4\. Start the AutoFS service now and set it to autostart at system
reboots:

\

<div>

![](image-LFTPDKG9.jpg){height="100%"}

</div>

5\. Verify the operational status of the AutoFS service. Use the -l and
\--no-pager options to show full details without piping the output to a
pager program (the pg command in this case):

\

<div>

![](image-S0ND3WG4.jpg){height="100%"}

</div>

6\. Run the ls command on the mount point /misc/autoindir and then grep
for both auto.misc and autoindir on the mount command output to verify
that the share is automounted and accessible:

\

<div>

![](image-9VMDJ9FI.jpg){height="100%"}

</div>

Observe the above outcomes. An activity in the mount point (ls command
in this case) caused AutoFS to mount the share /common on
/misc/autoindir. The mount command output illustrates the path of the
AutoFS map (/etc/auto.misc), the auto-generated mount point
(/misc/autoindir), file system type (autofs), and the options used
during the mount process. You can use the same umbrella mount point
/misc to mount additional auto-generated mount points.

\

This mount point will automatically disappear after five minutes of
idling. You can verify that by issuing the mount command again. A cd,
ls, or another activity in the mount point will bring it back.

\

This completes the AutoFS setup for an NFS share on the client using an
indirect map.

::: {style="page-break-before: always;"}
:::

[]{#chapter0511.html}

## Automounting User Home Directories {.style3}

\

AutoFS allows us to automount user home directories by exploiting two
special characters in indirect maps. The asterisk (\*) replaces the
references to specific mount points and the ampersand (&) substitutes
the references to NFS servers and shared subdirectories. With user home
directories located under /home, on one or more NFS servers, the AutoFS
service will connect with all of them simultaneously when a user
attempts to log on to a client. The service will mount only that
specific user's home directory rather than the entire /home. The
indirect map entry for this type of substitution is defined in an
indirect map, such as /etc/auto.master.d/auto.home, and will look like:

\

<div>

![](image-FPTPKH8O.jpg){height="100%"}

</div>

With this entry in place, there is no need to update any AutoFS
configuration files if additional NFS servers with /home shared are
added or removed. Similarly, if user home directories are added or
deleted, there will be no impact on the functionality of AutoFS. If
there is only one NFS server sharing the home directories, you can
simply specify its name in lieu of the first & symbol in the above
entry.

::: {style="page-break-before: always;"}
:::

[]{#chapter0512.html}

## Exercise 16-5: Automount User Home Directories Using Indirect Map {.style3}

\

There are two portions for this exercise. The first portion should be
done on server20 (NFS server) and the second portion on server10 (NFS
client) as user1 with sudo where required.

\

In the first portion, you will create a user account called user30 with
UID 3000. You will add the /home directory to the list of NFS shares so
that it becomes available for remote mount.

\

In the second portion, you will create a user account called user30 with
UID 3000, base directory /nfshome, and no home directory. You will
create an umbrella mount point called /nfshome for mounting the user
home directory from the NFS server. You will install the relevant
software and establish an indirect map to automount the remote home
directory of user30 under /nfshome. You will observe that the home
directory is automounted under /nfshome when you sign in as user30.

\

On NFS server server20:

\

1\. Create a user account called user30 with UID 3000 (-u) and assign
password "password1":

\

<div>

![](image-1Z5AFEAS.jpg){height="100%"}

</div>

2\. Edit the /etc/exports file and add an entry for /home (do not modify
or remove the previous entry):

\

<div>

![](image-JW7ANJY0.jpg){height="100%"}

</div>

3\. Export all the shares listed in the /etc/exports file:

\

<div>

![](image-FAG808ZE.jpg){height="100%"}

</div>

On NFS client server10:

\

1\. Install the autofs software package if it is not already there:

\

<div>

![](image-97MYNTLA.jpg){height="100%"}

</div>

2\. Create a user account called user30 with UID 3000 (-u), base home
directory location /nfshome (-b), no home directory (-M), and password
"password1":

\

<div>

![](image-T0WVSMTF.jpg){height="100%"}

</div>

This is to ensure that the UID for the user is consistent on the server
and the client to avoid access issues.

\

3\. Create the umbrella mount point /nfshome to automount the user's
home directory:

\

<div>

![](image-UN1HDEOX.jpg){height="100%"}

</div>

4\. Edit the /etc/auto.master file and add the mount point and indirect
map location to it:

\

<div>

![](image-RELSQT0W.jpg){height="100%"}

</div>

5\. Create the /etc/auto.master.d/auto.home file and add the following
information to it:

\

<div>

![](image-ZSB5R08Q.jpg){height="100%"}

</div>

For multiple user setup, you can replace "user30" with the & character,
but ensure that those users exist on both the server and the client with
consistent UIDs.

\

6\. Start the AutoFS service now and set it to autostart at system
reboots. This step is not required if AutoFS is already running and
enabled.

\

<div>

![](image-PPPSE8XC.jpg){height="100%"}

</div>

7\. Verify the operational status of the AutoFS service. Use the -l and
\--no-pager options to show full details without piping the output to a
pager program (the pg command):

\

<div>

![](image-JD2MMF3Q.jpg){height="100%"}

</div>

8\. Log in as user30 and run the pwd, ls, and df commands for
verification:

\

<div>

![](image-8VYYLD55.jpg){height="100%"}

</div>

The user is successfully logged in with their home directory automounted
from the NFS server. The pwd command confirms the path. The df command
verifies the NFS server name and the source home directory path for
user30, as well as the mount location. You can also use the mount
command and pipe the output to grep for user30 to view mount details
(mount \| grep user30).

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You may need to configure AutoFS for mounting a remote user
home directory.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

This completes the setup for an automounted home directory share for a
user.

::: {style="page-break-before: always;"}
:::

[]{#chapter0513.html}

## Chapter Summary {.style3}

\

This chapter discussed the sharing and mounting of remote file systems
using the Network File System protocol. It elucidated the concepts,
benefits, and versions of the NFS service, and described the commands
and configuration files involved in NFS management on the server and the
client.

\

Next, we performed an exercise to demonstrate the configuration and
sharing of a directory on one of the lab servers (NFS server) and
another exercise on the second lab system (NFS client) to mount that
share manually and persistently using the standard NFS mount method.

\

We explored the client-side service called AutoFS for automounting NFS
shares. We discussed the concepts, benefits, and components associated
with AutoFS, and analyzed its maps. We performed exercises to mount,
confirm, and unmount the remote NFS share using both direct and indirect
methods.

\

Finally, we described the AutoFS setting to automount user home
directories from the NFS server.

::: {style="page-break-before: always;"}
:::

[]{#chapter0514.html}

## Review Questions {.style3}

\

1\. The name of the AutoFS service daemon is autofs. True or False?

2\. What would the line entry /dir1 \*(rw) in the /etc/exports file
mean?

3\. What type of AutoFS map would have the /- /etc/auto.media entry in
the auto.master file?

4\. AutoFS requires root privileges to automatically mount a network
file system. True or False?

5\. What is the default timeout value for a file system before AutoFS
unmounts it automatically?

6\. Name the three common types of maps that AutoFS support.

7\. Arrange the tasks in three different correct sequences to export a
share using NFS: (a) update /etc/exports, (b) add service to firewall,
(c) run exportfs, (d) install nfs-utils, and (e) start nfs service.

8\. What would the entry \* server10:/home/& in an AutoFS indirect map
imply?

9\. Which command is used to export a share?

10\. An NFS server exports a share and an NFS server mounts it. True or
False?

11\. Which command would you use to unexport a share?

12\. What is the name of the NFS server configuration file?

13\. What is the name of the AutoFS configuration file and where is it
located?

::: {style="page-break-before: always;"}
:::

[]{#chapter0515.html}

## Answers to Review Questions {.style3}

\

1\. False. The name of the AutoFS service daemon is automount.

2\. The line entry would export /dir1 in read/write mode to all systems.

3\. A direct map.

4\. False.

5\. Five minutes.

6\. The three common AutoFS maps are master, direct, and indirect.

7\. d/e/b/a/c, d/e/a/c/b, or d/e/a/b/c.

8\. This indirect map entry would mount individual user home directories
from server10.

9\. The exportfs command.

10\. True.

11\. The exportfs command with the -u switch.

12\. The /etc/nfs.conf file.

13\. The name of the AutoFS configuration file is autofs.conf and it is
located in the /etc directory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0516.html}

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

::: {style="page-break-before: always;"}
:::

[]{#chapter0517.html}

## Lab 16-1: Configure NFS Share and Automount with Direct Map {.style3}

\

As user1 with sudo on server30, share directory /sharenfs (create it) in
read/write mode using NFS. On server40 as user1 with sudo, install the
AutoFS software and start the service. Configure the master and a direct
map to automount the share on /mntauto (create it). Run ls on /mntauto
to trigger the mount. Use df -h to confirm. (Hint: NFS Server and Client
Configuration, and Auto File System).

::: {style="page-break-before: always;"}
:::

[]{#chapter0518.html}

Lab 16-2: Automount NFS Share with Indirect Map

\

As user1 with sudo on server40, configure the master and an indirect map
to automount the share under /autoindir (create it). Run ls on
/autoindir/sharenfs to trigger the mount. Use df -h to confirm. (Hint:
Auto File System).

::: {style="page-break-before: always;"}
:::

[]{#chapter0519.html}
