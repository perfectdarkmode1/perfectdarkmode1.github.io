# Chapter 5 RHCSA Notes - Basic User Management


- Show who is currently logged in
- Review history of successful user login attempts and system reboots 
- Report history of failed user log in attempts 
- View recent user login attempts 
- Examine user and group information 
- Understand the content and syntax of local user authentication files 
- Analyze user configuration files 
- Add, modify, and delete local user accounts with default and custom values 
- Set and modify user passwords 
- Add user account with nologin access

User account information is recorded in several files. These files 
- may be edited manually if necessary (not recommended)

- service user accounts are added to the system when a corresponding service is installed, there may be situations when they need to be added manually. These accounts do not require login access; their presence is needed to support an installed application.

## Listing Logged-In Users

A list of the users who have successfully signed on to the system with valid credentials can be printed using who and w

### who command
- references the /run/utmp file and displays the information.
- displays login name of user
- shows terminal session device filename
- pts stands for pseudo terminal session
- shows data and time of user login
- Shows if terminal session is graphical(:0), remote(IP address), or textual on the console

### what command (w)
- Shows length of time the user has been idle
- CPU time used by all processes including any existing background jobs attached to this terminal (JCPU),
- CPU time used by the current process (PCPU),
- current activity (WHAT).
- current system time
- system up duration
- number of users logged in
- cpu averages over last 1, 5, and 15 minutes
- load average (CPU load): 0.00 and 1.00 correspond to no load and full load, and a number greater than 1.00 signifies excess load (over 100%).

### last command
- Reports the history of successful user login attempts and system 
- Consults the wtmp file located in the /var/log directory.
- wtmp keeps a record of login/logout activities
	- login time
	- duration a user stayed logged in
	- tty
- Output
	- Login name
	- Terminal name
	- Terminal name or IP from where connection was established
	- Day, Month, date, and time when the connection was established
	- Log out time or (still logged in)
	- Duration of session
	- Action name (system reboots section)
	- Activity name (system reboots section)
	- Linux kernel version (system reboots section)
	- Day, Month, date, and time when the reboot command was issued (system reboots section)
	- System restart time (system reboots section)
	- Duration the system remained down or (still running) (system reboots section)
	- log filename (wtmp) (last line)

### lastb command
- reports failed login attempts
- Consults /var/log/btmp
	- record of failed login attempts
	- login name
	- time
	- tty
- Must be root to run this command
- Columns
	- name of user
	- protocol used
	- terminal name or ip address
	- Day, Month, Date, and time of the attempt
	- Duration the attempt was tried
	- Duration the attempt last for
	- log filename (btmp) (last line)

### lastlog command
- most recent login evidence info for every user account that exists on the system
- Consults /var/log/lastlog
	- record of most recent user attempts
	- login name
	- time
	- port (or tty)
	- Columns:
		- Login name of user
		- Terminal name assigned upon Logging in
		- Terminal name or Ip address from where the session was initiated
		- Timestamp for the latest login or "Never logged in"
	- service accounts are used by their respective services, and they are not meant for logging.

### id (identifier) Command
- displays the calling user’s:
	- UID (User IDentifier)
	- username
	- GID (Group IDentifier)
	- group name
	- all secondary groups the user is a member of
	- SELinux security context

### groups Command:
- lists all groups the calling user is a member of:
- first group listed is the primary group for the user who executed this command
- other groups are secondary (or supplementary).
- can also view group membership information for a different user.

## Local User Authentication Files
- Three supported account types: root, normal, service
- root 
	- has full access to all services and administrative functions on the system.
	- created by default during installation.
- Normal
	- user-level privileges
	- cannot perform any administrative functions
	- can run applications and programs that have been authorized.
- Service
	- take care of their respective services, which include apache, ftp, mail, and chrony.
- User account information for local users is stored in four files that are located in the /etc directory.
	- passwd, shadow, group, and gshadow (user authentication files)
	 - updated when a user or group account is created, modified, or deleted.
	 - referenced to check and validate the credentials for a user at the time of their login attempt,
	 - system creates their automatic backups by default as passwd-, shadow-, group-, and gshadow- in the /etc directory.
### /etc/passwd
- vital user login data
- each row hold info for one user 
- 644 permissions by default
- 7 feilds per row
	- login name
		- up to 255 characters
		- _ and - characters are supported
		- not recommended to include special characters and uppercase letters in login names.
	- password
		- "x" in this field points to /etc/shadow for actual password.
		- "\*" identifies disabled account
		- Can also include a hashed password (RHEL uses SHA-512 by default)
	- UID
		- Number between 0 and 4.2 billion
		- UID 0 is reserved for root account
		- UIDs 1-200 are used by Red Hat for core service accounts
		- UIDs 201-999 are reserved for non-core service accounts
		- UIDs 1000 < are for normal user accounts (starts at 1000 by default)
	- GID
		- GID that matches entry in /etc/group (primary group)
		- Group for every user by default that matches UID
	- Comments (GECOS) or (GCOS)
		- general comments about the user
	- Home Directory
		- absolute path to the user home directory.
	- Shell
		- absolute path of the shell file for the user's primary shell after logging in. (default = (/bin/bash))

### /etc/shadow
- no access permissions for any user (even root) (but owned by root)
- secure password control (shadow password)
- user passwords are hashed and stored in a more secure file /etc/shadow,
- limits on user passwords in terms of expiration, warning period, etc. applied on per-user basis
- limits and other settings are defined in /etc/login.defs
- user is initially checked in the passwd file for existence and then in the shadow file for authenticity.
- contains user authentication and password aging information. 
- Each row in the file corresponds to one entry in the passwd file. 
- login names are used as a common key between the shadow and passwd files.
- nine colon-separated fields per line entry.
	- 1 Login name
	- 2 Encrypted password
		- ! at the beginning of this field shows that the user account is locked
		- if field is empty then user has passwordless entry
	- 3 last change
		- Number of days (lastchg) since the UNIX epoch, (UNIX time (January 01, 1970 00:00:00 UTC) when the password was last modified. 
		- Empty field represents the passiveness of password aging features.
		- 0 forces the user to change their password upon next login.
	- 4 minimum 
		- number of days (mindays) that must elapse before the user is allowed to change their password
		- can be altered using the chage command with the -m option or the passwd command with the -n option. 
		- 0 or null in this field disables this feature.
	- 5 (Maximum)
		- maximum number of days (maxdays) before the user password expires and must be changed. 
		- may be altered using the chage command with the -M option or the passwd command with the -x option. 
		- null value here disables this feature along with other features such as the maximum password age, warning alerts, and the user inactivity period.
	- 6 Field 6 (Warning)
		- number of days (warndays) the user gets warnings for changing their password before it expires.
		- may be altered using the chage command with the -W option or the passwd command with the -w option. 
		- 0 or null in this field disables this feature.
	- 7 Password Expiry)
		 - maximum allowable number of days for the user to be able to log in with the expired password. (inactivity period).
		 - may be altered using the chage command with the -I option or the passwd command with the -i option. 
		 - empty field disables this feature. 
	- 8 (Account Expiry) 
		- number of days since the UNIX time when the user account will expire and no longer be available. 
		- may be altered using the chage command with the -E option. 
		- empty field disables this feature. 
	- 9 (Reserved): Reserved for future use.

### /etc/group
- plaintext file and contains critical group information. 
- 644 permissions by default and owned by root.
- Each row in the file stores information for one group entry. 
- Every user on the system must be a member of at least one group (User Private Group (UPG)). 
- a group name matches the username it is associated with by default
- four colon-separated fields per line entry.
	- Field 1 (Group Name): 
		- Holds a group name that must begin with a letter. Group names with up to 255 characters, including the 
		- uppercase, underscore (_) and hyphen (-) characters, are also supported. (not recommended)
	 - Field 2 (Encrypted Password): 
		 - Can be empty or contain an “x” (points to the /etc/gshadow file for the actual password), or a hashed group-level password. 
		 - can set a password on a group for non-members to be able to change their group identity temporarily using the newgrp command.
		 - non-members must enter the correct password in order to do so. 
	- Field 3 (GID): 
		- Holds a GID, that is also placed in the GID field of the passwd file. 
		- By default, groups are created with GIDs starting at 1000 and with the same name as the username.  
		- system allows several users to belong to a single group
		- also allows a single user to be a member of multiple groups at the same time. 
	- Field 4 (Group Members): 
		- Lists the membership for the group. (user’s primary group is always defined in the GID field of the passwd file.)



### /etc/gshadow
- no access permissions for any user (even root)
- group passwords are hashed and stored
- group names are used as a common key between the gshadow and group files.
- 000 permissions and owned by root
- four colon-separated fields
	- Field 1 (Group Name): 
		- Consists of a group name as appeared in the group file. 
	- Field 2 (Encrypted Password): 
		- Can contain a hashed password, which may be set with the gpasswd command for non-group members to access the group temporarily using the newgrp command. 
		- single exclamation mark (!) or a null value in this field allows group members password-less access and restricts non-members from switching into this group. 
	- Field 3 (Group Administrators): 
		- Lists usernames of group administrators that are authorized to add or remove members with the gpasswd command. 
	- Field 4 (Members): 
		- comma-separated list of members.
### gpasswd command:
	- add group administrators.
	- add or delete group members.
	- assign or revoke a group-level password.
	- disable the ability of the newgrp command to access a group. 
	- picks up the default values from the /etc/login.defs file.

## useradd and login.defs configuration files
### useradd command
- picks up the default values from the /etc/default/useradd and /etc/login.defs files for any options that are not specified at the command line when executing it.
- login.defs file is also consulted by the usermod, userdel, chage, and passwd commands 
- Both files store several defaults including those that affect the password length and password lifecycle.
/etc/default/useradd Default Directives:
- starting GID (GROUP) (provided the USERGROUPS_ENAB directive in the login.defs file is set to no)
- home directory location (HOME), 
- number of inactivity days between password expiry and permanent account disablement (INACTIVE), 
- account expiry date (EXPIRE), 
- login shell (SHELL), 
- skeleton directory location to copy user initialization files from (SKEL)
- whether to create mail spool directory (CREATE_MAIL_SPOOL)

### /etc/login.defs default directives:
MAIL_DIR 
- mail directory location 

PASS_MAX_DAYS, PASS_MIN_DAYS, PASS_MIN_LEN, and PASS_WARN_AGE 
- password aging attributes. 

UID_MIN, UID_MAX, GID_MIN, and GID_MAX 
- ranges of UIDs and GIDs to be allocated to new users and groups 

SYS_UID_MIN, SYS_UID_MAX, SYS_GID_MIN, and SYS_GID_MAX 
- ranges of UIDs and GIDs to be allocated to new service users and groups 

CREATE_HOME 
- whether to create a home directory 

UMASK 
- permissions to be set on the user home directory at creation based on this umask value 

USERGROUPS_ENAB 
- whether to delete a user’s group (at the time of user deletion) if it contains no more members 

ENCRYPT_METHOD 
- encryption method for user passwords

## User Account Management
## useradd Command
- add a new user to the system
- adds entries to the four user authentication files for each account added to the system
- creates a home directory for the user and copies the default user startup files from the skeleton directory /etc/skel into the user’s home directory
- used to update the default settings that are used at the time of new user creation for unspecified settings
- Options
	- -b (--base-dir) 
		- Defines the absolute path to the base directory for placing user home directories. The default is /home. 
	- -c (--comment) 
		- Describes useful information about the user. 
	- -d (--home-dir) 
		- Defines the absolute path to the user home directory. 
	- -D (--defaults) 
		- Displays the default settings from the /etc/default/useradd file and modifies them. 
	- -e (--expiredate) 
		- Specifies a date on which a user account is automatically disabled. The format for the date specification is YYYY-MM-DD. 
	- -f (--inactive) 
		- Denotes maximum days of inactivity between password expiry and permanent account disablement. 
	- -g (--gid) 
		- Specifies the primary GID. Without this option, a group account matching the username is created with the GID matching the UID. 
	- -G (--groups) 
		- Specifies the membership to supplementary groups.
	- -k (--skel) 
		- location of the skeleton directory (default is /etc/skel) (stores default user startup files)
			- These files are copied to the user’s home directory at the time of account creation. 
			- Three hidden bash shell files: (default)
				- .bash_profile, .bashrc, and .bash_logout
				- You can customize these files or add your own to be used for accounts created thereafter.
	- -m (--create-home) 
		- Creates a home directory if it does not already exist.
	- -o (--non-unique) 
		- Creates a user account sharing the UID of an existing user. 
		- When two users share a UID, both get identical rights on each other’s files. 
		- Should only be done in specific situations. 
	- -r (--system) 
		- Creates a service account with a UID below 1000 and a never-expiring password.
	- -s (--shell) 
		- Defines the absolute path to the shell file. The default is /bin/bash. 
	- -u (--uid) 
		- Indicates a unique UID. Without this option, the next available UID from the /etc/passwd file is used. 
	- login 
		- Specifies a login name to be assigned to the user account.
## usermod Command
- modify the attributes of an existing user
- similar syntax to useradd and most switches identical.
- Options unique to usermod:
	- -a (--append) 
		- Adds a user to one or more supplementary groups 
	- -l (--login) 
		- Specifies a new login name
	- -m (--move-home) 
		- Creates a home directory and moves the content over from the old location
	- -G
		- Add a list of groups a user is a member of.
## userdel Command
- to remove a user from the system
## passwd Command
- set or modify a user’s password

## No-Login (Non-Interactive) User Account
### nologin shell
- /sbin/nologin
- special purpose program that can be employed for user accounts that do not require login access to the system. 
- located in the /usr/sbin (or /sbin) directory
- user is refused with the message, “This account is currently not available.” 
- If a custom message is required, you can create a file called nologin.txt in the /etc directory and add the desired text to it.
- If a no-login user is able to log in with their credentials, there is a problem. Use the grep command against the /etc/passwd file to ensure ‘/sbin/nologin’ is there in the shell field for that user.
- examples of user accounts that do not require login access are the service accounts such as ftp, apache, and sshd.

## Labs
### Lab: who

```
who
```

### Lab: what
```
w
```

### Lab: last

1. List all user login, logout, and system reboot occurrences:
```
last
```

2. List system reboot info only:
```
last reboot
```

### Lab: lastb
```
lastb
```

### Lab: lastlog
```
lastlog
```

### Lab: id
1. View info about currently active user:
```
id
```

2. View info about another user:
```
id user1
```

### Lab: groups
1. View current user's groups:
```
groups
```

2. View groups of another user:
```
groups user1
```

### Lab: user authentication files
1. list of the four files and their backups from the /etc directory:
```
ls -l /etc/passwd* /etc/group* /etc/shadow* /etc/gshadow*
```

2. View first and last 3 lines of the passwd file
```
head -3 /etc/passwd ; tail -3 /etc/passwd
```

3. verify the permissions and ownership on the passwd file:
```
ls -l /etc/passwd
```

4. View first and last 3 lines of the shadow file:
```
head -3 /etc/shadow ; tail -3 /etc/shadow
```

5. verify the permissions and ownership on the shadow file:
```
ls -l /etc/shadow
```

6. View first and last 3 lines of the group file:
```
head -3 /etc/group ; tail -3 /etc/group
```

7. Verify the permissions and ownership on the group file:
```
ls -l /etc/group
```

8. View first and last 3 lines of the gshadow file:
```
head -3 /etc/gshadow ; tail -3 /etc/gshadow
```

9. Verify the permissions and ownership on the gshadow file:
```
ls -l /etc/gshadow
```

### Lab: useradd and login.defs
1. use the cat or less command to view the useradd file content or display the settings with the useradd command:
```
useradd -D
```
2. grep on the/etc/login.defs with uncommented and non-empty lines:
```
grep -v ^# /etc/login.defs | grep -v ^$
```

### Lab: Create a User Account with Default Attributes (root)
1. Create user2 with all the default directives:
```
useradd user2
```

2. Assign this user a password and enter it twice when prompted:
```
passwd user2
```

3. grep for user2: on the authentication files to examine what the useradd command has added:
```
cd /etc ; grep user2: passwd shadow group gshadow
```

4. Test this new account by logging in as user2 and then run the id and groups commands to verify the UID, GID, and group membership information:
```
su - user2
id
groups
```

### Lab: Create a User Account with Custom Values

1. Create user3 with UID 1010 (-u), home directory /usr/user3a (-d), and shell /bin/sh (-s): 
```
useradd -u 1010 -d /usr/user3a -s /bin/sh user3
```
2. Assign user1234 as password (passwords assigned in the following way is not recommended; however, it is okay in a lab environment):
```
echo user1234 | passwd --stdin user3
```

3. grep for user3: on the four authentication files to see what was added for this user:
```
cd /etc ; grep user3: passwd shadow group gshadow
```

4. Test this account by switching to or logging in as user3 and entering user1234 as the password. Run the id and groups commands for further verification.
```
su - user3 
id
groups
```

### Lab: Modify and Delete a User Account
1. Modify the login name for user2 to user2new (-l), UID to 2000 (-u), home directory to /home/user2new (-m and -d), and login shell to /sbin/nologin (-s). 
```
usermod -l user2new -m -d /home/user2new -s /sbin/nologin -u 2000 user2
```

2. Obtain the information for user2new from the passwd file for confirmation:
```
grep user2new /etc/passwd
```

3. Remove user2new along with their home and mail spool directories (-r):
```
userdel -r user2new
```

4. Confirm the user deletion:
```
grep user2new /etc/passwd
```

## Lab: Create a User Account with No-Login Access (root)
1. Look at the current nologin users:
```
grep nologin /etc/passwd
```

2. Create user4 with non-interactive shell file /sbin/nologin:
```
useradd -s /sbin/nologin user4
```

3. Assign user1234 as password:
```
echo user1234 | passwd --stdin user4
```

4. grep for user4 on the passwd file and verify the shell field containing the nologin shell:
```
grep user4 /etc/passwd
```

5. Test this account by attempting to log in or switch:
```
su - user4
```

## Lab: Check User Login Attempts (root)
1. execute the last, lastb, and lastlog commands, and observe the outputs. 
```
last
lastb
lastlog
```

2. List the timestamps when the system was last rebooted (last). 
```
last | grep reboot
```

## Lab 5-2: Verify User and Group Identity (user1)
1. run the who and w commands one at a time, and compare the outputs. 
```
who
w
```

2. Execute the id and groups commands, and compare the outcomes. Examine the extra information that the id command shows, but not the groups command. 
```
id
groups
```

## Lab 5-3: Create Users (root)
1. create user account user4100 with UID 4100 and home directory under /usr. 
```
useradd -m -d /usr/user4100 -u 4100 user4100 
```

2. Create another user account user4200 with default attributes.
```
useradd user4200
```

3. Assign both users a password. 
```
passwd user4100
passwd user4200
```

4. View the contents of the passwd, shadow, group, and gshadow files, and observe what has been added for the two new users. 
```
cat /etc/passwd
cat /etc/shadow
cat /etc/group
cat /etc/gshadow
```
## Lab: Create User with Non-Interactive Shell (root)
1. Create user account user4300 with the disability of logging in. 
```
useradd -s /sbin/nologin user4300
```

3. Assign this user a password. 
```
passwd user4300
```

5. Try to log on with this user and see is displayed on the screen. 
```
su - user4300
```

7. View the content of the passwd file, and see what is there that prevents this user from logging in. 
```
cat /etc/passwd
```

## Review Questions

Q. What would the command useradd -D do?
A. This command displays the defaults settings used at the time of user creation or modification.

Q. What does the lastlog command do? 
A. The lastlog command provides information about recent user logins. 

Q. What would the command useradd user500 do? 
A. The command provided will add user500 with all predefined default values. 

Q. The id and groups commands are useful for listing a user identification. True or False. 
A. False. Only the id command is used for this purpose.

Q. Name the four local user authentication files. 
A. The passwd, shadow, group, and gshadow files. 

Q. The passwd file contains secondary user group information. True or False? 
A. False. The passwd file contains primary user group information. 

Q. What is the first UID assigned to a normal user? 
A. The first UID assigned to a normal user is 1000. 

Q. Name the three fundamental user account classes in RHEL. 
A. The three fundamental user account categories are root, normal, and system. 

Q. Every user in RHEL gets a private group by default. True or False? 
A. True.

Q. What does the “x” in the password field in the passwd file imply? 
A. The “x” in the password field implies that the hashed password is stored in the shadow file. 

Q. Name the file that the who command consults to display logged-in users. 
A. The who command consults the /run/utmp file to list logged-in users. 

Q. What information does the lastb command provide? 
A. The lastb command reports the history of unsuccessful user login attempts. 

Q. The who command may be used to view logged out users. True or False? 
A. False. The who command shows currently logged-in users only. 

Q. What would the userdel command do if it is run with the -r option?
A. The userdel command with -r will delete the specified user along with their home directory.

Q. What is the first GID assigned to a group? 
A. The first GID assigned to a normal user is 1000. 

Q. What is the name of the default backup file for shadow? 
A. The name of the default backup file for shadow is shadow-. 

Q. Which file does the last command consult to display reports? 
A. The last command consults the /var/log/wtmp file to display reports.

Q. UID 999 is reserved for normal users. True or False? 
A. False. UID 999 is reserved for system accounts. 

A. Which file is assigned to users to deny them login access? 
Q. The /sbin/nologin file is assigned to users to deny them login. 

Q. You execute the lastb command as a normal user. The output reports an error. What do you need to do to run this command successfully? 
A. You need to run the lastb command as root or with the root privilege.




