# Chapter 6 RHCSA Notes - Advanced User Management

## Objectives and Topics
- Configure password aging attributes on local user accounts 
- Lock and unlock user account 
- Understand, create, modify, and delete local groups and group memberships 
- Switch into another user account 
- Configure who can execute which privileged commands 
- Identify and manage file owners and owning groups

RHCSA Objectives: 05. 
Log in and switch users in multi-user targets
Change passwords and adjust password aging for local user accounts
Create, delete, and modify local groups and group memberships
Configure superuser access

## Password Aging attributes
- can be done for an individual user or applied to all users.
- Individual user accounts may be prevented from logging in to the system by locking their access for a period of time or permanently.
- must be performed by a user with elevated privileges of the root user.
- Normal users may be allowed access to privileged commands by defining them appropriately in a configuration file.
- Each file that exists on the system regardless of its type has an owning user and an owning group.  
- every file that a user creates is in the ownership of that user. 
- ownership may be changed and given to another user by a super user.

## Password Aging and management
- setting restrictions on password expiry, account disablement, locking and unlocking users, and password change frequency.
- Can choose to inactivate it completely for an individual user.
- Stored in the /etc/shadow file (fields 4 to 8) and its default policies in the /etc/login.defs configuration file.
- aging management tools—chage and passwd—
- usermod command can be used to implement two aging attributes (user expiry and password expiry) and lock and unlock user accounts.

### chage command
- set or alter password aging parameters on a user account.
- changes various fields in the shadow file
- Switches
	- -d (--lastday) 
		- Specifies an explicit date in the YYYY-MM-DD format, or the number of days since the UNIX time when the password was last modified. With -d 0, the user is forced to change the password at next login. It corresponds to field 3 in the shadow file. 
	- -E (--expiredate) 
		- Sets an explicit date in the YYYY-MM-DD format, or the number of days since the UNIX time on which the user account is deactivated. This feature can be disabled with -E -1. It corresponds to the eighth field in the shadow file. 
	- -I (--inactive) 
		- Defines the number of days of inactivity after the password expiry and before the account is locked. The user may be able to log in during this period with their expired password. This feature can be disabled with -I -1. It corresponds to field 7 in the shadow file. 
	- -l 
		- Lists password aging attributes set on a user account. 
	- -m (--mindays) 
		- Indicates the minimum number of days that must elapse before the password can be changed. A value of 0 allows the user to change their password at any time. It corresponds to field 4 in the shadow file. 
	- -M (--maxdays) 
		- Denotes the maximum number of days of password validity before the user password expires and it must be changed. This feature can be disabled with -M -1. It corresponds to field 5 in the shadow file. 
	- -W (--warndays) 
		- Designates the number of days for which the user gets alerts to change their password before it expires. It corresponds to field 6 in the shadow file.

### passwd command
- set or modify a user’s password
- modify the password aging attributes and 
- lock or unlock account
- Switches
	- -d (--delete) 
		- Deletes a user password 
		- does not expire the user account. 
	- -e (--expire) 
		- Forces a user to change their password upon next logon. 
		- sets date to prior to Unix time
	- -i (--inactive) 
		- Defines the number of days of inactivity after the password expiry and before the account is locked. (field 7 in shadow file)
	- -l (--lock) 
		- Locks a user account. 
	- -n (--minimum) 
		- Specifies the number of days that must elapse before the password can be changed. (field 4 in shadow file)
	- -S (--status) 
		- Displays the status information for a user. 
	- -u (--unlock) 
		- Unlocks a locked user account.
	- -w (--warning) 
		- Designates the number of days for which the user gets alerts to change their password before it actually expires. (field 6 in shadow file)
	- -x (--maximum) 
		- Denotes the maximum number of days of password validity before the user password expires and it must be changed. (field 5 in shadow file)


### usermod command
- modify a user’s attribute
- lock or unlock their account
- Switches
	- -L (--lock) 
		- Locks a user account by placing a single exclamation mark (!) at the beginning of the password field and before the hashed password string. 
	- -U (--unlock) 
		- Unlocks a user’s account by removing the exclamation mark (!) from the beginning of the password field. 


## Linux Groups and their Management
- /etc/group
	- group info
- /etc/login.defs
	- default policies
- /etc/gshadow
	- group administrator information and group-level passwords
- group management tools
	- groupadd, groupmod, and groupdel
	- create, alter, and erase groups

### groupadd command
- adds entries to the group and gshadow files for each group added to the system
- picks up default values from /etc/login.defs
- Switches
	- -g (--gid) 
		- Specifies the GID to be assigned to the group 
	- -o (--non-unique) 
		- Creates a group with a matching GID of an existing group. When two groups have an identical GID, members of both groups get identical rights on each other’s files. This should only be done in specific situations. 
	- -r 
		- Creates a system group with a GID below 1000 
	- groupname 
		- Specifies a group name

### groupmod command
- syntax of this command is very similar to the groupadd with most options identical.
- Additional flags
	- -n
		- change name of existing group

## Switching Users

### su command
- Ctrl-d
	- return to previous user
su -
	- switch user with startup scripts
-c 
	- issue a command as a user without switching to them.
- root user can switch into any user account that exists on the system without being prompted for that user’s password.
- switching into the root account to execute privileged actions is not recommended.

### whoami command
- show current user
### logname command
- Identity of the user who originally logged in.

### groupdel command
- removes entries for the specified group from both group and gshadow files.

## Doing as Superuser (substutute user)
- Any normal user that requires privileged access to administrative commands or non-owning files is defined in the sudoers file.
	- file may be edited with a command called visudo,
	- creates a copy of the file as sudoers.tmp and applies the changes there. After the visudo session is over, the updated updated file overwrites the original sudoers file and sudoers.tmp is deleted.
	- syntax
		- user1 ALL=(ALL) ALL
		- %dba ALL=(ALL) ALL
			group is prefixed by %
	- Make it so members are not prompted for password
		- user1 ALL=(ALL) NOPASSWD:ALL
		- %dba ALL=(ALL) NOPASSWD:ALL
	- Limit access to a single command
		- user1 ALL=/usr/bin/cat
		- %dba ALL=/usr/bin/cat
- too many entries can clutter sudoers file. Use aliases instead:
	- User_Alias
		- you can define a User_Alias called PKGADM for user1, user100, and user200. These users may or may not belong to the same Linux group.
	- Cmnd_Alias
		- you can define a Cmnd_Alias called PKGCMD containing yum and rpm package management commands,
### sudo command
- /etc/sudoers
- /etc/sudoers.d/
	- drop-in directory
/var/log/secure
	- Sudo logs successful authentication and command data to here under the name of the user using the command.
## Owning User and Owning Group
- Every file and directory has an owner.
- Creator assumes ownership by default.
- Every user is a member of one or more groups.
- Owners group is also assigned to file or directory by default.

### chown command
- alter the ownership for files and directories
- Must have root privileges.
- Can also change owning group.
### chgrp command
- alter the owning group for files and directories
- Must have root privileges.

## Labs

### Lab: Set and Confirm Password Aging with chage (root)
1. Set password aging parameters for user100 to mindays (-m) 7, maxdays (-M) 28, and warndays (-W) 5:
```
chage -m 7 -M 28 -W 5 user100
```

2. Confirm
```
chage -l user100
```

3. Set the account expiry to January 31, 2020
```
chage -E 2020-01-31 user100
```

4. Verify the new account expiry setting
```
chage -l user100
```

### Lab: Set and Confirm Password Aging with passwd (root)

1. Set password aging attributes for user200 to mindays (-n) 10, maxdays (-x) 90, and warndays (-w) 14:
```
passwd -n 10 -x 90 -w 14 user200
```

2. Confirm:
```
passwd -S user200
```

3. Set the number of inactivity days to 5:
```
passwd -i 5 user200
```

4. Confirm:
```
passwd -S user200
```

5. Ensure that the user is forced to change their password at next login:
```
passwd -e user200
```

6. Confirm:
```
passwd -S user200
```

### Lab: Lock and Unlock a User Account with usermod and passwd (root)
1. Obtain the current password information for user200 from the shadow file:
```
grep user200 /etc/shadow
```

2. Lock the account for user200:
```
usermod -L user200 
```

3. Confirm:
```
grep user200 /etc/shadow
```

4. Unlock the account with either of the following:
```
usermod -U user200
or
passwd -u user200
```

5. confirm
```
grep user200 /etc/shadow
```


### Lab: Create a Group and Add Members (root)
1. Create the group linuxadm with GID 5000:
```
groupadd -g 5000 linuxadm
```

2. Create a group called dba with the same GID as that of group linuxadm:
```
groupadd -o -g 5000 dba
```

3. Confirm:
```
grep linuxadm /etc/group
grep dba /etc/group
```

4. Add user1 as a secondary member of group dba using the usermod command. The existing membership for the user must remain intact.
```
usermod -aG dba user1
```

5. Verify the updated group membership information for user1 by extracting the relevant entry from the group file, and running the id and groups command for user1:
```
grep dba /etc/group
id user1
groups user1
```


### Lab: Modify and Delete a Group Account (root)
1. Alter the name of linuxadm to sysadm:
```
groupmod -n sysadm linuxadm
```

2. Change the GID of sysadm to 6000:
```
groupmod -g 6000 sysadm
```

3. Confirm:
```
grep sysadm /etc/group
grep linuxadm /etc/group
```

4. Delete sysadm group and confirm:
```
groupdel sysadm
grep sysadm /etc/group
```

### Lab: To switch from user1 (assuming you are logged in as user1) into root without executing the startup scripts
1. 
```
su
```

2. switch to user100
```
su - user100
```

3. See what whoami and logname reports now:
```
whoami
logname
```

4. use su as follows and execute this privileged command to obtain desired results:
```
su -c 'firewall-cmd --list-services'
```
### Lab: Add user1 to sudo file but only for the cat command.
1. Open up /etc/sudoers and add the following:
```
user1 ALL=/usr/bin/cat
```

2. run cat as user1 with and without sudo:
```
cat /etc/sudoers
sudo cat /etc/sudoers
```

### Lab: Add user and command aliases to the sudoer file.

1. Add the following to the bottom of the sudoers file:
```
Cmnd_Alias PKGCMD = /usr/bin/yum, /usr/bin/rpm
User_Alias PKGADM = user1, user100, user200 
PKGADM ALL=PKGCMD
```

2. Run rpm or yum with sudo as one of the users.
```
sudo yum 
```

### Lab: Take a look at examples in the sudoers file.
```
cat /etc/sudoers
```

### Lab: Viewing owner and group information
1. Create a file file1 as user1 in their home directory and exhibit the file’s long listing:
```
touch file1
ls -l file1
```

2. View the corresponding UID and GID instead, you can specify the -n option with the command:
```
ls -ln file1
```
### Lab: Modify File Owner and Owning Group
1. Change into the /tmp directory and create file10 and dir10:
```
cd /tmp
touch file10
mkdir dir10
```

2. Check and validate that both attributes are set to user1:
```
ls -l file10
ls -ld dir10
```

3. Set the ownership of file10 to user100 and confirm:
```
sudo chown user100 file10
ls -l file10
```

4. Alter the owning group to dba and verify:
```
sudo chgrp dba file10
ls -l file10
```

5. Change the ownership to user200 and owning group to user100 and confirm:
```
sudo chown user200:user100 file10
```

6. Modify the ownership to user200 and owning group to dba recursively on dir10 and validate:
```
sudo  chown -R user200:dba dir10
ls -ld dir10
```

### Lab: Create User and Configure Password Aging (root)
1. Create group lnxgrp with GID 6000. 
```
groupadd lnxgrp -g 6000
```

2. Create user user5000 with UID 5000 and GID 6000. Assign this user a password.
```
useradd -u 5000 -g 6000 user5000
```

3. Establish password aging attributes so that this user cannot change their password within 4 days after setting it and with a password validity of 30 days. This user should start getting warning messages for changing password 10 days prior to account lock down. 
```
chage -m 4 -M 30 -W 10 user5000
```

4. This user account needs to expire on the 20th of December, 2021. 
```
chage -E 2021-12-20 user5000
```

### Lab 6-2: Lock and Unlock User (root)
1. Lock the user account for user5000 using the passwd command, and 
```
passwd -l user5000
```

2. confirm by examining the change in the /etc/shadow file. 
```
cat /etc/shadow
```

3. Try to log in with user5000 and observe what happens. 
```
su - user1
su - user5000
```

4. Use the usermod command and unlock

## Review Questions 
Q. Which command can be used to display the effective (current) username?
A. `whoami `

Q. What is the recommended location to store custom sudo rules? 
A. The custom sudo rules should be stored in files under the /etc/sudoers.d directory.

Q. What would the command passwd -l user10 do? 
A. This command will lock user10.
 
Q. The chown command may be used to modify both ownership and group membership on a file. True or False? 
A. True.
 
Q. What would the command passwd -n 7 -x 15 -w 3 user5 do? 
A. The command will set mindays to 7, maxdays to 15, and warndays to 3 for user5.
 
Q. Write the two command names for managing all of the password aging attributes. 
A. The passwd and chage commands.

Q. Which file has the default password aging settings defined? 
A. The /etc/login.defs file has the defaults for password aging defined.
 
Q. What would the command chage -E 2020-10-22 user10 do? 
A. The command provided will set October 22, 2020 as the expiry date for user10. 

Q. What would the command chage -l user5 do?
A. The command provided will display password aging attributes for user5. 

Q. Which two commands can be used to lock and unlock a user account?
A. `usermod` and `passwd`

Q. When using sudo, log files record activities under the root user account. True or False? 
A. False. The activities are registered under the username who invokes the sudo command. 

Q. What is the difference between running the su command with and without the hyphen sign? 
A. With the dash sign the su command processes the specified user’s startup files, and it won’t without this sign. 

Q. What is the significance of the -o option with the groupadd and groupmod commands? 
A. The -o option lets the commands share a GID between two or more groups. 

Q. What would the entry user10 ALL=(ALL) NOPASSWD:ALL in the sudoers file imply? 
A. It will give user10 password-less access to all privileged commands. 

Q. The chgrp command may be used to modify both ownership and group membership on a file. True or False? 
A. False. 
 
Q. What would the command chage -d 0 user60 do?
A. The command provided will force user60 to change their password at next login.


