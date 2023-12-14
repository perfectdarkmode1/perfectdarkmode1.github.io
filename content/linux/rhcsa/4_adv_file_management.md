# Chapter 4 RHCSA Notes - Advanced File Management

## Goals and Objectives

- ugo/rwx access permissions 
- symbolic/octal notations for permissions
- permissions for file owner, owning group, and others 
- default permissions on new files and directories 
- special permission bits: setuid, setgid, and sticky 
- Use setgid bit for group collaboration 
- sticky bit on public and shared writable directories 
- Search for files
- extended access controls for named users and named groups
- Set default extended access controls on directories

#### RHCSA Objectives: 
10. List, set, and change standard ugo/rwx permissions 
36. Create and configure set-GID directories for collaboration 
39. Diagnose and correct file permission problems 
56. Create and use file access control lists

Setting a default ACL on a directory :: Allows content sharing among user's without having to modify access on each new file and subdirectory.
## Permission Classes #card
- user (u)
- group (g)
- other (o) (public)
- all (a) <- all combined

## Permission types #card
- r,w,x
- work differently on files and directories
- hyphen (-) represents no permissions set

### ls results permissions groupings #card
- - rwx rw- r--
	- user (owner), group, and other (public)
### ls results first character meaning #card
- regular file
d directory
l symbolic link
c character device file
b block device file
p named pipe
s socket
	

## Modifying Access Permission Bits
---
### chmod  command #card
- Modify permissions using symbolic or octal notation.
- Used by root or the file owner.

Flags
chmod -v ::: Verbose.

### Symbolic notation #card
- Letters (ugo/rwx) and symbols (+, -, =) used to add, revoke, or assign permission bits.

### Octal Notation #card
Three-digit numbering system ranging from 0 to 7.
	0 ---
	1 --x
	2 -w-
	3 -wx
	4 r--
	5 r-x
	6 rw-
	7 rwx

### Default Permissions #card
- Calculated based on the umask (user mask) value subtracted from the initial permissions value.

#### umask 
- Three-digit value (octal or symbolic) that refers to read, write, and execute permissions for owner, group, and public.
- Default umask value ::: 0022 for the root user and 0002 normal users.
- The left-most 0 has no significance.
- If umask is set to 000 files will get max of 666
- If the initial permissions are 666 and the umask is 002 then the default permissionss are 664. (666-002)
- Any new files or directories creating after changing the umask will have the new default permissions set. 
- umask settings are lost when you log off. Add it to the appropriate startup file to make it permanent.

Defaults
- files 666 rw-rw-rw-
- directories 777 rwxrwxrwx

### umask command

Options
- -S symbolic form 
## Special File Permissions
---
- 3 types of special permission bits for executable files or directories for non root users
	- setuid
	- setgid
	- sticky
- setuid 
	- set on exe's to provide non-owners the ability to run them with the privileges of the owning user
	- may be set on directories and files but will have no effect.
	- example: the su command
	- shows an 's' in ls -l listing at the end of owners permissions
	- If the file already has the “x” bit set for the user, the long listing will show a lowercase “s”, otherwise it will list it with an uppercase “S”.
- setgid 
	- set on exe's to provide non-group members the ability to run them with the privileges of the owning group.
	- May be set on shared directories
		- allow files and subdirectories created underneath to automatically inherit the directory’s owning group.
		- saves group members who are sharing the directory contents from changing the group ID for every new file and subdirectory that they add.
	- write command has this set by default so a member of the tty group can run it. If the file already has the “x” bit set for the group, the long listing will show a lowercase “s”, otherwise it will list it with an uppercase “S”.
- Sticky bit 
	- may be set on public directories for inhibiting file deletion by non-owners
	- may be set on directories and files but will have no effect.
	- Set on /tmp and /var/tmp by default
	- Letter "t" in other permission feild	
	- If the directory already has the “x” bit set for public, the long listing will show a lowercase “t”, otherwise it will list it with an uppercase “T”.
## Find

- search files and display the full path
- execute command on search results
- Different search criteria
	- name
	- part name
	- ownership
	- owning group
	- permissions
	- inode number
	- last access
	- modification time in days or minutes
	- size
	- file type
- Command syntax
	- {find} + {path} + {search option} + {action}
- Options
	- -name / -iname (search by name)
	- -user / -group (UID / GID)
	- -perm (permissions)
	- -inum (inode)
	- -atime/amin (access time)
	- -mtime/amin (modification time)
	- -size / -type (size / type)
	-
- Action
	- copy, erase, rename, change ownership, modify permissions
		- -exec  {} \\;
			- replaces {} for each filename as it is found. The semicolon character (;) marks the termination of the command and it is escaped with the backslash character (\\).
		- -ok  {} \\;
			- same as exec but requires confirmation.
	- -delete
	- -print <- default
## Access Control Lists (ACLs)

- Extra permissions that can be set on files and directories.
- define permissions for named user and named groups.
- Configured the same way on both files and directories.
- Named Users
	- May or may not be a part of the same group.
- 2 different groups of ACLs. Default ACLs and Access ACLs.
	- Access ACLs
		- Set on individual files and directories
	- Default ACLs
		- Applied on directories
		- files and subdirectories inherit the ACL
		- Execute bit must be set on the directory for public.
		- Files receive the shared directory's default ACLs as their access ACLs - what the mask limits.
		- Subdirectories receive both default ACLs and access ACLs as they are.

- A "+" at the end of ls -l listing indicates ACL is set
	- -rw-rw-r--+

### ACL Commands
getfacl
- Display ACL settings
	- Displays:
	- name of file
	- owner
	- owning group
	- Permissions
		- colon characters save space for named user/group (or UID/GID) when extended Permissions are set.
		- Example: user:1000:r--
			- the named user with UID 1000, who is neither the file owner nor a member of the owning group, is allowed read-only access to this file.
		- Example: group:dba:rw- 
			- give the named group (dba) read and write access to the file.l
setfacl
	- set, modify, substitute, or delete ACL settings
	- If you want to give read and write permissions to a specific user (user1) and change the mask to read-only at the same time, the setfacl command will allocate the permissions as mentioned; however, the effective permissions for the named user will only be read-only.

u:UID:perms
- named user must exist in /etc/passwd
- if no user specified, permissions are given to the owner of the file/directory

g:GID:perms
- Named group must exist in /etc/group
- If no group specified, permissions are given to the owning group of the file/directory

o:perms
- Nither owner not owning group

m:perms
- Maximum permissions for named user or named group

Switches

|Switch|Description|
|---|---|
|-b|Remove all Access ACLs|
|-d|Applies to default ACLs|
|-k|Removes all default ACLs|
|-m|Sets or modifies ACLs|
|-n|Prevent auto mask recalculation|
|-R|Apply Recursively to directory|
|-x|Remove Access ACL|
|-c|Display output without header|

## Mask Value

- Determine maximum allowable permissions for named user or named group
- Mask value displayed on separate line in getfacl output
- Mask is recalculated every time an ACL is modified unless value is manually entered
- Overrides the set ACL value

## Labs
### Lab: find stuff

1. Create file 10 and search for it.
```
[vagrant@server1 ~]$ sudo touch /root/file10
[vagrant@server1 ~]$ sudo find / -name file10 -print
/root/file10
```

2. Perform a case insensitive search for files and directories in /dev that begin with "usb" followed by any characters.
```
[vagrant@server1 ~]$ find /dev -iname usb*
/dev/usbmon0
```

3. Find files smaller than 1MB (-1M) in size (-size) in the root user’s home directory (~).
```
[vagrant@server1 etc]$ find ~ -size -1M
```

4. Search for files larger than 40MB (+40M) in size (-size) in the /usr directory:
```
[vagrant@server1 etc]$ sudo find /usr -size +40M
/usr/share/GeoIP/GeoLite2-City.b
```

5. Find files in the entire root file system (/) with ownership (-user) set to user daemon and owning group (-group) set to any group other than (-not or ! for negation) user1:
```
[vagrant@server1 etc]$ sudo find / -user daemon -not -group user1
```

6. Search for directories (-type) by the name “src” (-name) in /usr at a maximum of two subdirectory levels below (-maxdepth):
```
[vagrant@server1 etc]$ sudo find /usr -maxdepth 2 -type d -name src
/usr/local/src
/usr/src
```

7. Run the above search but at least three subdirectory levels beneath /usr, substitute -maxdepth 2 with -mindepth 3.
```
[vagrant@server1 etc]$ sudo find /usr -mindepth 3 -type d -name src
/usr/src/kernels/4.18.0-425.3.1.el8.x86_64/drivers/gpu/drm//display/dmub/src
/usr/src/kernels/4.18.0-425.3.1.el8.x86_64/tools/usb/usbip/src
```

8. Find files in the /etc directory that were modified (-mtime) more than (the + sign) 2000 days ago:
```
[vagrant@server1 etc]$ sudo find /etc -mtime +2000
/etc/libuser.conf
/etc/xattr.conf
/etc/whois.conf
```

9. Run the above search for files that were modified exactly 12 days ago, replace “+2000” with “12”.
```
[vagrant@server1 etc]$ sudo find /etc -mtime 12
```

10. To find files in the /var/log directory that have been modified (-mmin) in the past (the - sign) 100 minutes:
```
[vagrant@server1 etc]$ sudo find /etc -mtime +2000
/etc/libuser.conf
/etc/xattr.conf
/etc/whois.conf
[vagrant@server1 etc]$ sudo find /etc -mtime 12
[vagrant@server1 etc]$ sudo find /var/log -mmin -100
/var/log/rhsm/rhsmcertd.log
/var/log/rhsm/rhsm.log
/var/log/audit/audit.log
/var/log/dnf.librepo.log
/var/log/dnf.rpm.log
/var/log/sa
/var/log/sa/sa16
/var/log/sa/sar15
/var/log/dnf.log
/var/log/hawkey.log
/var/log/cron
/var/log/messages
/var/log/secure
```

11. Run the above search for files that have been modified exactly 25 minutes ago, replace “-100” with “25”.
```
[vagrant@server1 etc]$ sudo find /var/log -mmin 25
```

12. To search for block device files (-type) in the /dev directory with permissions (-perm) set to exactly 660:
```
[vagrant@server1 etc]$ sudo find /dev -type b -perm 660
/dev/dm-1
/dev/dm-0
/dev/sda2
/dev/sda1
/dev/sda
```

13. Search for character device files (-type) in the /dev directory with at least (-222) world writable permissions (this example would ignore checking the write and execute permissions):
```
[vagrant@server1 etc]$ sudo find /dev -type c -perm -222
```

14. Find files in the /etc/syst directory that are executable by at least their owner or group members:
```
[vagrant@server1 etc]$ sudo find /etc/syst -perm /110
```

15. Search for symlinked files (-type) in /usr with permissions (-perm) set to read and write for the owner and owning group:
```
 sudo find /usr -type l -perm -ug=rw
 ```

16. Search for directories in the entire directory tree (/) by the name “core” (-name) and list them (ls-ld) as they are discovered without prompting for user confirmation (-exec):
```
[vagrant@server1 etc]$ sudo find / -name core -exec ls -ld {} \;
```

17. Use the -ok switch to prompt for confirmation before it copies each matched file (-name) in /etc/sysconfig to /tmp:
```
[vagrant@server1 etc]$ sudo find /etc/sysconfig -name '*.conf' -ok cp {} \;
< cp ... /etc/sysconfig/nftables.conf > ?
```

### Lab: Display ACL and give permissions

1. Create and empty file aclfile1 in /tmp and display ACLs on it:
```
cd /tmp
touch aclfile1
getfacl aclfile1
```
2. Give rw permission to user 1 but with a mask of read only and view the results.
```
setfacl -m u:user1:rw,m:r aclfile1
```

3. Promote the mask value to include write bit and verify:
```
setfacl -m m:rw aclfile1
getfacl -c aclfile1
```

### Lab: Identify, Apply, and Erase Access ACLs
1. Switch to user1 and create file acluser1 in /tmp:
```
su - user1
cd /tmp
touch acluser1
```

2. Use ls and getfacl to check existing acl entries:
```
ls -l acluser1
getfacl acluser1 -c
```

3. Allocate rw permissions to user100 with setfacl in octal form:
```
setfacl -m u:user100:6 acluser1
```

4. Run ls (+) and getfacl to verify:
```
ls -l acluser1
getfacl -c acluser1
```
5. Open another terminal as user100 and open the file and edit it. 

6. Add user200 with full rwx permissions to acluser1 using the symbolic notation and then show the updated ACL settings:
```
setfacl -m u:user200:rwx acluser1
getfacl -c acluser1
```
7. Delete the ACL entries set for user200 and validate:
```
setfacl -x u:user200 acluser1
getfacl acluser1 -c
```
8. Delete the rest of the ACLs:
```
setfacl -b acluser1
```
9. Use the ls and getfacl commands and confirm for the ACLs removal:
```
ls -l acluser1
getfacl acluser1 -c
```
10. create group aclgroup1 
```
groupadd -g 8000 aclgroup1
```
11. add this group as a named group along with the two named users (user100 and user200).

### Lab: Apply, Identify, and erase default ACLs
1. Switch or log in as user1 and create a directory projects in /tmp:
```
su - user1
cd /tmp
mkdir projects
```

2. Use the getfacl command for an initial look at the permissions on the directory:
```
getfacl -c projects
```

3. Allocate default read, write, and execute permissions to user100 and user200 on the directory. Use both octal and symbolic notations and the -d (default) option with the setfacl command.
```
setfacl -dm u:user100:7,u:user200:rwx projects/
getfacl -c projects/
```

4. Create a subdirectory prjdir1 under projects and observe the ACL inheritance:
```
mkdir prjdir1
getfacl -c prjdir1
```

5. Create a file prjfile1 under projects and observe the ACL inheritance:
```
touch prjfile1
getfacl -c prjfilel
```

6. log in as one of the named users, change directory into /tmp/projects, and edit prjfile1 (add some random text). Then change into the prjdir1 and create file file100.
```
su - user100
cd /tmp/projects
vim prjfile1
ls -l prjfile1
cd prjdir1
touch file100
pwd
```

7. Delete all the default ACLs from the projects directory as user1 and confirm:
```
exit
su - user1
cd /tmp
setfacl -k projects
getfacl -c projects
```

8. create a group such as aclgroup2 by running groupadd -g 9000 aclgroup2 as the root user and repeat this exercise by adding this group as a named group along with the two named users (user100 and user200).

### Lab: Modify Permission Bits Using Symbolic Form

1. Add an execute bit for the owner and a write bit for group and public
```
[vagrant@server1 ~]$ chmod u+x permfile1 -v
mode of 'permfile1' changed from 0444 (r--r--r--) to 0544 (r-xr--r--)
[vagrant@server1 ~]$ chmod -v go+w permfile1
mode of 'permfile1' changed from 0544 (r-xr--r--) to 0566 (r-xrw-rw-)
```

2. Revoke the write bit from public and assign read, write, and execute bits to the three user categories at the same time.
```
[vagrant@server1 ~]$ chmod -v o-w permfile1
mode of 'permfile1' changed from 0566 (r-xrw-rw-) to 0564 (r-xrw-r--)
[vagrant@server1 ~]$ chmod -v a=rwx permfile1
mode of 'permfile1' changed from 0564 (r-xrw-r--) to 0777 (rwxrwxrwx)
```

3. Revoke write from the owning group and write and execute bits from public.
```
[vagrant@server1 ~]$ chmod g-w,o-wx permfile1 -v
mode of 'permfile1' changed from 0777 (rwxrwxrwx) to 0754 (rwxr-xr--)
```

### Lab: Modify Permission Bits Using Octal Form

1. Read only for user, group, and other:
```
[vagrant@server1 ~]$ touch permfile2
[vagrant@server1 ~]$ chmod 444 permfile2
[vagrant@server1 ~]$ ls -l permfile2
-r--r--r--. 1 vagrant vagrant 0 Feb  4 12:22 permfile2
```

2. Add an execute bit for the owner:
```
[vagrant@server1 ~]$ chmod -v 544 permfile2
mode of 'permfile2' changed from 0444 (r--r--r--) to 0544 (r-xr--r--)
```

3. Add a write permission bit for group and public:
```
[vagrant@server1 ~]$ chmod -v 566 permfile2
mode of 'permfile2' changed from 0544 (r-xr--r--) to 0566 (r-xrw-rw-)
```

4. Revoke the write bit for public:
```
[vagrant@server1 ~]$ chmod -v 564 permfile2
mode of 'permfile2' changed from 0566 (r-xrw-rw-) to 0564 (r-xrw-r--)
```

5. Assign read, write, and execute permission bits to all three user categories:
```
[vagrant@server1 ~]$ chmod -v 777 permfile2
mode of 'permfile2' changed from 0564 (r-xrw-r--) to 0777 (rwxrwxrwx)
```

6. Run the umask command without any options and it will display the current umask value in octal notation:
```
[vagrant@server1 ~]$ umask
0002
```

7. Symbolic form

```
[vagrant@server1 ~]$ umask -S
u=rwx,g=rwx,o=rx
```

8. Set all new files and directories to get 640 and 750 permissions,
```
umask 027
umask u=rwx,g=rx,o=
```

9. Test new umask (666-027=640) (777-027=750)
```
[vagrant@server1 ~]$ touch tempfile1
[vagrant@server1 ~]$ ls -l tempfile1
-rw-r-----. 1 vagrant vagrant 0 Feb  5 12:09 tempfile1
[vagrant@server1 ~]$ mkdir tempdir1
[vagrant@server1 ~]$ ls -ld tempdir1
drwxr-x---. 2 vagrant vagrant 6 Feb  5 12:10 tempdir1
```

### Lab:  View suid bit on su command
```
[vagrant@server1 ~]$ ls -l /usr/bin/su
-rwsr-xr-x. 1 root root 50152 Aug 22 10:08 /usr/bin/su
```
### Lab: Test the Effect of setuid Bit on Executable Files

1. Open 2 terminal windows. Switch to user1 in terminal1
```
[vagrant@server1 ~]$ su - user1
Password:
Last login: Sun Feb  5 12:37:12 UTC 2023 on pts/1
```

2. Switch to root on terminal2
```
sudo su - root
```

3. T1 Revoke the setuid bit from /usr/bin/su
```
chmod -v u-s /usr/bin/su
```

4. T2 log off as root
```
ctrl+d
```

5. Try to log in has root from both terminals
```
[user1@server1 ~]$ su - root
Password:
su: Authentication failure
```

6. T1 restore the setuid bit
```
[vagrant@server1 ~]$ sudo chmod -v +4000 /usr/bin/su
mode of '/usr/bin/su' changed from 0755 (rwxr-xr-x) to 4755 (rwsr-xr-x)
```

### Lab: Test the Effect of setgid Bit on Executable Files

1. Log into two terminals
T1 root
T2 user1
Opened with ssh

2. T2 list users currently logged in
```
who
```

3. T2 send a message to root
```
write root
```

3. T1 revoke setgid from /usr/bin/write
```
chmod g-s /usr/bin/write -v
```

4. Try to write root
```
[user1@server1 ~]$ write root
write: effective gid does not match group of /dev/pts/0
```

5. Restore the setgid bit on /usr/bin/write:
```
[root@server1 ~]# sudo chmod -v +2000 /usr/bin/write
mode of '/usr/bin/write' changed from 0755 (rwxr-xr-x) to 2755 (rwxr-sr-x)
```

6. Test
```
write root
```

### Lab: Set up Shared Directory for Group Collaboration

1. set up 2 test users
```
[root@server1 ~]# adduser user100
[root@server1 ~]# adduser user200
```

2. Add group sgrp with GID 9999 with the groupadd command:
```
[root@server1 ~]# groupadd -g 9999 sgrp
```

3. Add user100 and user200 as members to sgrp using the usermod command:
```
[root@server1 ~]# usermod -aG sgrp user100
[root@server1 ~]# usermod -aG sgrp user200
```

4. Create /sdir directory
```
[root@server1 ~]# mkdir /sdir
```

5. Set ownership and owning group on /sdir to root and sgrp, using the chown command:
```
[root@server1 ~]# chown root:sgrp /sdir
```

6. Set the setgid bit on /sdir using the chmod command:
```
[vagrant@server1 ~]$ sudo chmod g+s /sdir
```

7. Add write permission to the group members on /sdir and revoke all permissions from public:
```
[root@server1 ~]# chmod g+w,o-rx /sdir
```

8. Verify
```
[root@server1 ~]# ls -ld /sdir
drwxrws---. 2 root sgrp 6 Feb 13 15:49 /sdir
```

9. Switch or log in as user100 and change to the /sdir directory:
```
[root@server1 ~]# su - user100
[user100@server1 ~]$ cd /sdir
```

10. Create a file and check the owner and owning group on it:
```
[user100@server1 sdir]$ touch file100
[user100@server1 sdir]$ ls -l file100
-rw-rw-r--. 1 user100 sgrp 0 Feb 10 22:41 file100
```

11. Log out as user100, and switch or log in as user200 and change to the /sdir directory:
```
[root@server1 ~]# su - user200
[user200@server1 ~]$ cd /sdir
```

12. Create a file and check the owner and owning group on it:
```
[user200@server1 sdir]$ touch file200
[user200@server1 sdir]$ ls -l file200
-rw-rw-r--. 1 user200 sgrp 0 Feb 13 16:01 file200
```

### Lab: View "t" in permissions for sticky bit
```
[user200@server1 sdir]$ ls -l /tmp /var/tmp -d
drwxrwxrwt. 8 root root 185 Feb 13 16:12 /tmp
drwxrwxrwt. 4 root root 113 Feb 13 16:00 /var/tmp
```

### Lab: Test the effect of Sticky Bit

1. Switch to user100 and change to the /tmp directory
```
[user100@server1 sdir]$ cd /tmp
```

2. Create file called stckyfile
```
[user100@server1 tmp]$ touch stickyfile
```

3. Try to delete the file as user200
```
[user200@server1 tmp]$ rm stickyfile
rm: remove write-protected regular empty file 'stickyfile'? y
rm: cannot remove 'stickyfile': Operation not permitted
```

4. Revoke the /tmp stickybit and confirm
```
[vagrant@server1 ~]$ sudo chmod o-t /tmp
[vagrant@server1 ~]$ ls -ld /tmp
drwxrwxrwx. 8 root root 4096 Feb 13 22:00 /tmp
```

5. Retry the removal as user200
```
rm stickyfile
```

6. Restore the sticky bit on /tmp
```
sudo chmod -v +1000 /tmp
```

### Lab: Manipulate File Permissions (user1)
1. Create file file11 and directory dir11 in the home directory. Make a note of the permissions on them. 
```
touch 1
mkdir dir11
```

2. Run the umask command to determine the current umask. 
```
umask
```

3. Change the umask value to 0035 using symbolic notation. 
```
umask g=r,0=w
```

4. Create file22 and directory dir22 in the home directory. 
```
touch file22
mkdir dir22
```

5. Observe the permissions on file22 and dir22, and compare them with the permissions on file11 and dir11. 
```
ls -l
```

6. Use the chmod command and modify the permissions on file11 to match those on file22. 
```
chmod g-w,o-r,o+w file11
```

7. Use the chmod command and modify the permissions on dir22 to match those on dir11. Do not remove file11, file22, dir11, and dir22 yet.
```
chmod g-wx,o-rx,o+w dir11
```
### Lab: Configure Group Collaboration and Prevent File Deletion (root)
1. create directory /sdir. Create group sgrp and create user1000 and user2000 and add them to the group:
```
mkdir /sdir
groupadd sgrp
adduser user1000 && adduser user2000
usermod -a -G sgrp user1000
usermod -a -G sgrp user2000
```

2. Set up appropriate ownership (root), owning group (sgrp), and permissions (rwx for group, --- for public, s for group, and t for public) on the directory to support group collaboration and ensure non-owners cannot delete files. 
```
chgrp sgrp sdir
chmod g=rwx,o=--- sdir
chmod o+t sdir
chmod g+s sdir
```

3. Log on as user1000 and create a file under /sdir. 
```
su - user1000
cd /sdir
touch testfile

```

4. Log on as user2000 and try to edit that file. You should be able to edit the file successfully. 
```
su - user2000
cd /sdir
vim testfile
cat testfile
```

5. As user2000 try to delete the file. You should not be able to. 
```
rm testfile
```
### Lab: Find Files (root)
1. Search for all files in the entire directory structure that have been modified in the last 300 minutes and display their type. 
```
find /sdir -mtime -300 -exec file {} \;
```
2. Search for named pipe and socket files. 
```
find / -type p
find / -type s
```
### Lab: Find Files Using Different Criteria (root)
1. Search for regular files under /usr that were accessed more than 100 days ago, are not bigger than 5MB in size, and are owned by the user root. 
```
find /usr -type f -mtime +100 -size -5M -user root
```
### Lab: Apply ACL Settings (root)
1. Create file testfile under /tmp. 
```
touch /tmp/testfile
```
2. Create users.
 ```
 adduser user2000
 adduser user3000
 adduser user4000
 ```
 
3. Apply ACL settings on the file so that user2000 gets 7, user3000 gets 6, and user4000 gets 4 permissions. 
```
setfacl -m u:user2000:7 testfile
setfacl -m u:user3000:6 testfile
setfacl -m u:user4000:4 testfile
```

4. Remove the ACLs for user2000, and verify. 
```
setfacl -x user2000 testfile
getfacl testfile
```
 
5. Erase all remaining ACLs at once, and confirm.
```
setfacl -b testfile
getfacl testfile
```

## Review Questions 

Q. The output generated by the umask command shows the current user mask in four digits. What is the significance of the left-most digit? 

A. The left-most digit has no significance in the umask value.

--- 

Q. What would the command find /dev -type c -perm 660 do?

A. The find command provided will find all character device files under /dev with exact permissions of 660. 

---

Q. Default permissions are calculated by subtracting the initial permissions from the umask value. True or False? 

A. False. Default permissions are calculated by subtracting the umask value from the initial permission values. 

---

Q. What would be the effect of the sticky bit on an executable file? 

A. Nothing. The sticky bit is meant for directories only.

---

Q. Name the permission classes, types, and modes. 

A. Permission classes are user, group, and public; permission types are read, write, and execute; and permission modes are add, revoke, and assign. 

---

Q. Default ACLs are meant for directories only. True or False? 

A. True. Default ACLs are meant for directories only. 

---

Q. The default umask for a normal user in bash shell is 0027. True or False? 

A. False. The default umask for bash shell users is 0002. 

---

Q. What digit represents the setuid bit in the chmod command? 

A. The digit 4 represents the setuid bit. 

---

Q. What would the command chmod g-s file1 do? 

A. It would erase the setgid bit from file1.

---

Q. Sticky bit is recommended for every system directory. True or False? 

A. False. 

---

Q. What would the command setfacl -m g:dba:rw file1 do? 

A. This command will give the users of the dba group read and write permissions on file1. 

---

Q. The setgid bit enables group members to run a command at a higher priority. True or False? 

A. False. 

---

Q. What is the equivalent symbolic value for permissions 751? 

A. The equivalent for octal 751 is rwxr-x--x. 

---

Q. What permissions would the owner of the file get if the chmod command is executed with 555? 

A. The owner will get read and execute permissions. 

---

Q. What would the find / -name core -ok rm {} \; command do?

A. The find command provided will display all files by the name core in the entire directory hierarchy and ask for removal confirmation as it finds them. 

---

Q. Which special permission bit is set on a directory for team sharing? 

A. The setgid bit is set for team sharing.



 












