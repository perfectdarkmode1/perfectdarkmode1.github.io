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