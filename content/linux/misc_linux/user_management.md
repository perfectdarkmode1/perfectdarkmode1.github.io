---
title: User Management
date: 2023-11-06T06:20:36-07:00
draft: true
---
Users and groups

Exist soley for access and permissions

home/ username : where each user's specific files get stored

can vary in different distros

user ids (UID) are used to manage users. The system identifies user by UID.

Groups are also used to manage permissions

sets of users with permissions set by that group

system identifies groups by group ID (GID)

users can be humans or system daemons that run processes to keep the system running

root or superuser

can access any file or start or terminate any process

$ sudo

used to run a command with root access

$ls -la /etc/shadow

views permissions of /etc/shadow

Root

$  su

opens a root shell if no user is specified

/etc/sudoers

lists users who can run sudo

$visudo

to edit the sudoers file

/etc/passwd

to find what users are mapped to what UID, shows list of users and detailed information about them.

$cat /etc/passwd

root:x:0:0;root:/root:/bin/bash

From left to right from above:

Username

User's password

x means the password is stored in the /etc/shadow file

\* means the user doesn't have login access

blank field means the user doesn't have a password

user ID

The group ID

GECOS field - comma delimeted field that allows for comments about the user.

User's home directory

User's shell

You can edit the /etc/passwd file by hand with the vipw tool but it is best to leave it to useradd and userdel tools

/etc/shadow

$sudo cat/etc/shadow

root:MyEPTEa$6Nonsense:15000:0:99999:7:::

Left to right from above

Username

Encrypted password

Date of last password change - expressed as the number of days since Jan 1, 1970. If 0 then the user should change their password the next time they log in.

Minimum password age - days the user will have to wait before changing their password again.

Maximum password age - Maximum number of days before a user has to change their password.

Password warning period - Number of days before a password is going to expire

Password inactivity period - # of days after a password has expired  to allow login with their password.

Account expiration date - date that user will not be able to log in.

Reserved field  for future use.

In most distributions today, user authentication doesn't rely on just the /etc/shadow file, there are other mechanisms in place such as PAM (Pluggable Authentication Modules) that replace authentication.

/etc/group

$ cat /etc/group

root:*:0:pete

left to right from above

Group name

Group Password

Group ID

List of users - you can manually specify users you want in a specific group

User management tools

Used on a single machine:

$ sudo useradd bob

creates an entry in /etc/passwd for Bob. sets up default groups and adds an entry to the /etc/shadow file.

$ sudo userdel bob

to remove a user.

$ passwd bob

to change a password
