---
title: File Permissions
date: 2023-11-06T06:20:36-07:00
draft: true
---
File permissions

$ls -l Desktop/

drwxr-xr-x 2 pete penguins 4096 Dec 1 11:45 .

Four parts to file permissions

Filetype (d (for directory) in the example) a is for regular file

These 3 parts are the actual file permissions.

d | rwx | r-x | r-x

Filetype | User Permissions | Group Permissions | Other Permissions

r - readable

w - writable

x - executable

-  empty

Modifying Permissions

$ chmod u+x myfile

Format: Chmod, permission set (user, group or other), file

The + is adding the permission

$ chmod u-x myfile

The - is removing the permission

$ chmod ug+w

Adding write to user and group (add "o" for other permissions)

Numerical representations for changing permissions

4: read permission

2: write permission

1: execute permission

Ex: $ chmod 755 myfile

Rwx re re user, group, other

Ownership permissions

$ sudo chown patty myfile

Sets the owner of myfile to patty (chown is change owner)

$ sudo chgrp whales myfile

Set the group of myfile to whales (chgrp = change group)

$ sudo chown patty:whales myfile

Changes group and user at the same time.

Umask

Used to chane default permissions

Only persists if you modify .profile

$ umask 021

Takes away x permissions from others (the default is 022)

Setuid

SUID

Allows a user to run a program as the owner of the program file rather than as themselves.

in /usr/bin/passwd you'll see an 's' in permissions for SUID.

This means when a user is running the passwd command they are running as root.

-rwsr-xr-x 1 root root 47032 Dec 1 11:45 /usr/bin/passwd

Modifying SUID

2 ways to modify

Symbolic:

$ sudo chmod u+s myfile

Numerical:

$ sudo chmod 4755 myfile

SUID  is denoted with a 4 and is pre-pended to the permission set.

SUID denoted as a capital S does not have execute permissions

Setgid

SGID

Allows a program to run as if it was a member of that group.

Modifying SGID

$ sudo chmod g+s myfile

$ sudo chmod 2555 myfile

Numerical representations for SGID is 2

Process permissions

Effective user ID

There are three UIDs associated with every process.

When you launch a process, it runs with the same permissions as the user or group that ran it.  This is used to grant access rights to a process.

Real User ID

The ID of the user who launched the process. Used to track down the user who launched a process.

Saved user ID

Allows a process to switch between the effective user ID and the Real user ID

The Sticky Bit

A permission bit that makes it so only the owner  or root can delete or modify the file.

$ls -ld /tmp

drwxrwxrwxt 6 root root 4096 Dec 15 11:45 /tmp

The t at the end is the sticky bit.

Modify sticky bit

$ sudo chmod +t mydir

$ sudo chmod 1755 mydir

The numerical representation of the sticky bit is 1
