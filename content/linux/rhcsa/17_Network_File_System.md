# Chapter 16 RHCSA Notes - Network File System

- Same tools for mounting and unmounting a filesystem.
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


**[Exercise]{#part0029_split_001.html#id_477 .calibre10} 17-4: Access
NFS Share Using Indirect Map**

This exercise should be done on *server10* as *user1* with *sudo* where
required.

In this exercise, you will configure an indirect map to automount the
NFS share */common* that is available from *server20*. You will install
the relevant software and set up AutoFS maps to support the automatic
mounting. You will observe that the specified mount point "autoindir" is
created automatically under */misc*.

Note that */common* is already mounted on the */local* mount point via
the *fstab* file and it is also configured via a direct map for
automounting on */autodir*. There should occur no conflict in
configuration or functionality among the three.

1[.]{.c19}Install the AutoFS software package called *autofs*:

![](images/00877.jpeg){.image2}

2[.]{.c19}Confirm the entry for the indirect map */misc* in the
**etc*auto.master* file exists:

![](images/00878.jpeg){.image2}

3[.]{.c19}Edit the **etc*auto.misc* file and add the mount point, NFS
server, and share information to it:

![](images/00879.jpeg){.image2}

4[.]{.c19}Start the AutoFS service now and set it to autostart at system
reboots:

![](images/00880.jpeg){.image2}

5[.]{.c19}Verify the operational status of the AutoFS service. Use the
-l and \--no-pager options to show full details without piping the
output to a pager program (the *pg* command in this case):

![](images/00881.jpeg){.image2}

6[.]{.c19}Run the *ls* command on the mount point **misc*autoindir* and
then *grep* for both *auto.misc* and *autoindir* on the *mount* command
output to verify that the share is automounted and accessible:

![](images/00882.jpeg){.image2}

Observe the above outcomes. The *mount* command output illustrates the
path of the AutoFS map (**etc*auto.misc*), the auto-generated mount
point (**misc*autoindir*), file system type (autofs), and the options
used during the mount process. An activity in the mount point (*ls*
command in this case) caused AutoFS to mount the share */common* on
**misc*autoindir*. You can use the same umbrella mount point */misc* to
mount additional auto-generated mount points.

This mount point will automatically disappear after five minutes of
idling. You can verify that by issuing the *mount* command again. A
*cd*, *ls*, or some other activity in the mount point will bring it
back.

This completes the AutoFS setup for an NFS share on the client using an
indirect map.

**[Automounting]{#part0029_split_001.html#id_478 .calibre10} User Home
Directories**

AutoFS allows us to automount user home directories by exploiting two
special characters in indirect maps. The asterisk (\*) replaces the
references to specific mount points and the ampersand (&) substitutes
the references to NFS servers and shared subdirectories. With user home
directories located under */home*, on one or more NFS servers, the
AutoFS service will connect with all of them simultaneously when a user
attempts to log on to a client. The service will mount only that
specific user's home directory rather than the entire */home*. The
indirect map entry for this type of substitution is defined in an
indirect map, such as **etc*auto.master.d/auto.home*, and will look
like:

![](images/00883.jpeg){.image2}

With this entry in place, there is no need to update any AutoFS
configuration files if NFS servers with */home* shared are added or
removed. Similarly, if user home directories are added or deleted, there
will be no impact on the functionality of AutoFS. If there is only one
NFS server sharing the home directories, you can simply specify its name
in lieu of the first & symbol in the above entry.

**[Exercise]{#part0029_split_001.html#id_479 .calibre10} 17-5: Automount
User Home Directories Using Indirect Map**

There are two portions for this exercise. The first portion should be
done on *server20* (NFS server) and the second portion on *server10*
(NFS client) as *user1* with *sudo* where required.

In the first portion, you will create a user account called *user30*
with UID 3000. You will add the */home* directory to the list of NFS
shares so that it becomes available for remote mount.

In the second portion, you will create a user account called *user30*
with UID 3000, base directory */nfshome*, and no user home directory.
You will create an umbrella mount point called */nfshome* for mounting
the user home directory from the NFS server. You will install the
relevant software and establish an indirect map to automount the remote
home directory of *user30* under */nfshome*. You will observe that the
home directory of *user30* is automounted under */nfshome* when you sign
in as *user30*.

**On NFS server *server20*:**

1[.]{.c19}Create a user account called *user30* with UID 3000 (-u) and
assign password "password1":

![](images/00884.jpeg){.image2}

2[.]{.c19}Edit the **etc*exports* file and add an entry for */home* (do
not remove the previous entry):

![](images/00885.jpeg){.image2}

3[.]{.c19}Export all the shares listed in the **etc*exports* file:

![](images/00886.jpeg){.image2}

**On NFS client *server10*:**

1[.]{.c19}Install the AutoFS software package called *autofs*:

![](images/00887.jpeg){.image2}

![](images/00888.jpeg){.image2}

2[.]{.c19}Create a user account called *user30* with UID 3000 (-u), base
home directory location */nfshome* (-b), no home directory (-M), and
password "password1":

![](images/00889.jpeg){.image2}

This is to ensure that the UID for the user is consistent on the server
and the client to avoid access issues.

3[.]{.c19}Create the umbrella mount point */nfshome* to automount the
user's home directory:

![](images/00890.jpeg){.image2}

4[.]{.c19}Edit the **etc*auto.master* file and add the mount point and
indirect map location to it:

![](images/00891.jpeg){.image2}

5[.]{.c19}Create the **etc*auto.master.d/auto.home* file and add the
following information to it:

![](images/00892.jpeg){.image2}

For multiple user setup, you can replace "user30" with the & character,
but ensure that those users exist on both the server and the client with
consistent UIDs.

6[.]{.c19}Start the AutoFS service now and set it to autostart at system
reboots. This step is not required if AutoFS is already running and
enabled.

![](images/00893.jpeg){.image2}

7[.]{.c19}Verify the operational status of the AutoFS service. Use the
-l and \--no-pager options to show full details without piping the
output to a pager program (the *pg* command):

![](images/00894.jpeg){.image2}

8[.]{.c19}Log in as *user30* and run the *pwd*, *ls*, and *df* commands
for verification:

![](images/00895.jpeg){.image2}

The user is successfully logged in with their home directory automounted
from the NFS server. The *pwd* command confirms the path. The *df*
command verifies the NFS server name and the source home directory path
for *user30*, as well as the mount location. You can also use the
*mount* command and pipe the output to *grep* for *user30* to view mount
details (**mount \| grep user30**).

[**EXAM TIP:**]{.c56}You may need to configure AutoFS for mounting a
remote user home directory.

This completes the setup for an automounted home directory share for a
user.

**[Chapter]{#part0029_split_001.html#id_480 .calibre10} Summary**

This chapter discussed the sharing and mounting of remote file systems
using the Network File System protocol. It elucidated the concepts,
benefits, and versions of the NFS service, and described the commands
and configuration files involved in NFS management on the server and the
client.

Next, we performed an exercise to demonstrate the configuration and
sharing of a directory on one of the lab servers (NFS server) and
another exercise on the second lab system (NFS client) to mount that
share manually and persistently using the standard NFS mount method.

We explored the client-side service called AutoFS for automounting NFS
shares. We discussed the concepts, benefits, and components associated
with AutoFS, and analyzed its maps. We performed exercises to mount,
confirm, and unmount the remote NFS share using both direct and indirect
methods.

Finally, we described the AutoFS setting to automount user home
directories from the NFS server.

**[Review]{#part0029_split_001.html#id_481 .calibre10} Questions**

1[.]{.c19}What would the entry *\* server10:/home/&* in an AutoFS
indirect map imply?

2[.]{.c19}Which command is used to export a share?

3[.]{.c19}An NFS server exports a share and an NFS server mounts it.
True or False?

4[.]{.c19}Which command would you use to unexport a share?

5[.]{.c19}What is the name of the NFS server configuration file?

6[.]{.c19}What would the line entry */dir1 \*(rw)* in the **etc*exports*
file mean?

7[.]{.c19}What type of AutoFS map would have the */- *etc*auto.media*
entry in the *auto.master* file?

8[.]{.c19}AutoFS requires *root* privileges to automatically mount a
network file system. True or False?

9[.]{.c19}What is the default timeout value for a file system before
AutoFS unmounts it automatically?

10[.]{.c23}Name the three common types of maps that AutoFS support.

11[.]{.c23}Arrange the tasks in three different correct sequences to
export a share using NFS: (a) update **etc*exports*, (b) add service to
firewalld, (c) run *exportfs*, (d) install *nfs-utils*, and (e) start
nfs service.

12[.]{.c23}What is the name of the AutoFS configuration file and where
is it located?

13[.]{.c23}The name of the AutoFS service daemon is *autofs*. True or
False?

**[Answers]{#part0029_split_001.html#id_482 .calibre10} to Review
Questions**

1[.]{.c19}This indirect map entry would mount individual user home
directories from *server10*.

2[.]{.c19}The *exportfs* command.

3[.]{.c19}True.

4[.]{.c19}The *exportfs* command with the -u switch.

5[.]{.c19}The **etc*nfs.conf* file.

6[.]{.c19}The line entry would export */dir1* in read/write mode to all
systems.

7[.]{.c19}A direct map.

8[.]{.c19}False.

9[.]{.c19}Five minutes.

10[.]{.c23}The three common AutoFS maps are master, direct, and
indirect.

11[.]{.c23}d/e/b/a/c, d/e/a/c/b, or d/e/a/b/c.

12[.]{.c23}The name of the AutoFS configuration file is *autofs.conf*
and it is located in the */etc* directory.

13[.]{.c23}False. The name of the AutoFS service daemon is *automount*.

**[Do-]{#part0029_split_001.html#id_483 .calibre10}It-Yourself Challenge
Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

**Lab 17-1: Configure NFS Share and Automount with Direct Map**

As *user1* with *sudo* on *server10*, share directory */sharenfs*
(create it) in read/write mode using NFS. On *server20* as *user1* with
*sudo*, install the AutoFS software and start the service. Configure the
master and a direct map to automount the share on */mntauto* (create
it). Run *ls* on */mntauto* to trigger the mount. Use **df -h** to
confirm. (Hint: NFS Server and Client Configuration, and Auto File
System).

**[Lab]{#part0029_split_001.html#id_484 .calibre10} 17-2: Automount NFS
Share with Indirect Map**

As *user1* with *sudo* on *server20*, configure the master and an
indirect map to automount the share under */autoindir* (create it). Run
*ls* on */autoindir/sharenfs* to trigger the mount. Use **df -h** to
confirm. (Hint: Auto File System).

[]{#part0030_split_000.html}