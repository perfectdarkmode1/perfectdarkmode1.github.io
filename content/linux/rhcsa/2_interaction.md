# Chapter 2 RHCSA Notes - Interaction

## Linux Graphical Environment

## Wayland
- Client/server display protocol. 
- Foundation for running GUI apps.
- Better graphics capabilities, features, and performance than X.

### Core Components

- Display manager (login manager)
- Desktop environment

### Display/ Login Manager 
- Presentation of graphical login screen
- Allows users to enter credentials to log on to the system
- Preconfigured graphical desktop manager appears after the credentials are verified

- Default display manager for RHEL8 :: GNOME Display Manager (GDM).

#### Desktop Environment 

- After login, the display/login manager establishes a Desktop Environment (DE).

# Linux Directory Structure and Filesystems

Filesystem Hierarchy Standard (FHS) :: Describes names, locations, and permissions for many file types and directories.

## Top-Level Directories

- Key top-level directories under /
- Some of these directories hold static data
- Others contain dynamic (or variable) information.

### Static directories

- commands
- configuration files
- library routines
- kernel files
- device files

### Dynamic directories 

- log files
- status files
- temporary files\

## File System Categories

Three groups: 
- disk-based
- network-based
- memory-based

### Disk-based 

- created on physical media such as a hard drive or a USB flash drive
- store information persistently

two disk-based file systems that  are created when you select the default partitioning :: root and boot file systems.
### Network Based

- disk-based file systems that are shared over the network for remote access.
- store information persistently

### Memory Based

- virtual; created automatically at system startup and destroyed when the system goes down.
- lost at system reboots.

## Root File System (/), Disk-Based

Size of the root file system is automatically determined by the installer program based on the available disk space when you select the default partitioning (it may be altered)

### Key Directories:

#### /etc 
- etcetera (extended text configuration)
- system configuration files
- common subdirectories
	systemd
	sysconfig
	lvm
	skel
-   comprise configuration files for systemd
-   most system services
-   Logical Volume Manager
-   per-user shell startup template files

/root :: default home directory for the root user

/mnt :: used to temporarily mount a file system

#### Boot File System (/boot), Disk-Based 

- Linux kernel
- boot support files
- boot configuration files
- size determined by the installer program based on the available disk space when you select the default partitioning
- may be set to a different size during or after the installation

#### The Home Directory (/home) 

- store user home directories and other user contents.

#### The Optional Directory (/opt) 

- hold additional software that may need to be installed on the system
- subdirectory is created for each installed software.

#### UNIX System Resources Directory (/usr)

- most of the system files.

##### /usr/bin
- binary directory
- crucial user executable commands.

##### /usr/sbin
- Most commands are required at system boot,
- system binary
- crucial system administration commands not intended for execution by normal users (although they can still run a few of them).
- not included in the default search path for normal users

##### /usr/lib and /usr/lib64
- shared library routines
- required by many commands/programs located in /usr/bin and /usr/sbin
- used by kernel and other applications and programs for their successful installation and operation
- /usr/lib directory also stores system initialization and service management programs
- /usr/lib64 contains 64-bit shared library routines.

##### /usr/include
- header files for C language.

##### /usr/local:
- system administrator repository for storing commands and tools
- commands not generally included with the original Linux distribution.
	/usr/local/bin
		executables
	/usr/local/etc
		configuration files
	/usr/local/lib and /usr/local/lib64
		holds library routines.
	/usr/share:
		directory location for manual pages, documentation, sample templates, configuration files, etc.
		may be shared with other Linux platforms.

##### /usr/src:
- used to store source code.

#### Variable Directory (/var)

- data that frequently changes while the system is operational.
- log, status, spool, lock, and other dynamic data.

common subdirectories

##### /var/log
- Most system log files
- system logs, boot logs, user logs, failed user logs, installation logs, cron logs, mail logs, etc.

##### /var/opt

- log, status, and other variable data files for additional software installed in /opt, t.

##### /var/spool
- print jobs, cron jobs, mail messages, and other queued items.

##### /var/tmp

- Large temporary files or temporary files that need to exist for longer periods of time than what is typically allowed in /tmp
- survive system reboots
- deleted if they are not accessed or modified for a period of 30 days.

#### Temporary Directory (/tmp)

- temporary files
- programs can create temporary files here during runtime or installation.
- These files survive system reboots and are automatically removed if they are not accessed or modified for a period of 10 days.

#### Devices File System (/dev)

- Device nodes for (physical  and virtual)
- Linux kernel talks to devices through device nodes.
- Device nodes are automatically created and deleted by the udevd service.

udevd service :: A Linux service for dynamic device management.

Two types of device files :: Character (or raw), and block.

kernel accesses devices using :: Character (or raw), and/or  block Device files.

#### Character devices

- Accessed serially.
- Console, serial printers, mice, keyboards, terminals, etc.

#### Block devices

- Accessed in a parallel fashion with data exchanged in blocks.
- Data on block devices is accessed randomly.
- Hard disk drives, optical drives, parallel printers, etc.

## Procfs File System (/proc)

- Config and status info on:
	- Kernel, CPU, memory, disks, partitioning, file systems, networking, running processes, etc.
- Zero-length pseudo files point to data maintained by the kernel in the memory.
- Interface to interact with kernel-maintained information.
- Contents created in memory at system boot time, updated during runtime, and destroyed at system shutdown.

## Runtime File System (/run)

- Data for processes running on the system.
	- /run/media
- Used to automatically mount external file systems (CD, DVD, flash USB.)
- Contents deleted at shutdown.

## The System File System (/sys)

- Info about hardware devices, drivers, and some kernel features.
- Used by the kernel to load necessary support for devices, create device nodes in /dev, and configure devices.
- Auto-maintained.
# Essential System Commands

### tree command
- List hierarchy of directories and files.
- Column 2
	- Size.
-  Column 3
	- Full path.

Options.
	tree -a :: Include hidden files in the output.
	tree -d :: Exclude files from the output.
	tree -h :: Displays file sizes in human-friendly format.
	tree -f :: Prints the full path for each file.
	tree -p :: Includes file permissions in the output

## Labs

### List only the directories (-d) in the root user’s home directory (/root).
```
tree -d /root
```

### List files in the /etc/sysconfig directory along with their permissions, sizes in human-readable format, and full path.
```
tree -phf /etc/sysconfig
```

### View tree man pages.
```
man tree
```

# Prompt Symbols
- Hash sign (#) for root user.
- Dollar sign ($) for normal users.

# Linux Commands

Two types of commands:
1. User 
	- General purpose.
	- For any user.
2. System Management
	- Superuser.
	- Require elevated privileges.

# Command Mechanics

Basic Syntax
- command option(s) argument(s)
- Many commands have preconfigured default options and arguments. 

An option that starts with a single hyphen character (-la, for instance) ::: Short-option format.

- Two hyphen characters (--all, for instance)  ::: Long-option format.
## Listing Files and Directories

## ls 

- ll :: shortcut for ls -l 

Flags
ls -l ::: View long listing format.
ls -d ::: View info on the specified directory.
ls -h ::: Human readable format.
ls -a ::: List all files, including the hidden files.
ls -t ::: Sort output by date and time with the newest file first.
ls -R ::: List contents recursively.
ls -i ::: View inode information.
### labs:

#### Show the long listing of only /usr without showing its contents.
```
ls -ld /usr
```

#### Display all files in the current directory with their sizes in human-friendly format.
```
ls -lh
```

#### List all files, including the hidden files, in the current directory with detailed information.
```
ls -la
```

#### Sort output by date and time with the newest file first. 
```
ls -lt
```

#### List contents of the /etc directory recursively.
```
ls -R /etc
```

#### List directory info and the contents of a directory recursively.
```
ls -lR /etc
```

#### View ls manpage.
```
man ls
```

### Printing Working Directory (pwd) command

- Returns the absolute path to a file or directory.

## Navigating Directories

Absolute path (full path or a fully qualified pathname) :: Points to a file or directory in relation to the top of the directory tree. It always starts with the forward slash (/).

Relative path :: Points to a file or directory in relation to your current location.

### Labs:

#### Go one level up into the parent directory using the relative path
```
cd ..
```

#### cd into /etc/sysconfig using the absolute path (/etc/sysconfig), or the relative path (etc/sysconfig) 
```
cd /etc/sysconfig
cd /
cd etc/sysconfig
```

#### Change into the /usr/bin directory from /etc/sysconfig using relative or absolute path 
```
cd /usr/bin
```
or
```
cd ../usr/bin
```

#### Return to your home directory
```
cd
```
or
```
cd ~
```

#### Use the absolute path to change into the home directory of the root user from /etc/sysconfig
```
cd ../../root
```

#### Switch between the current and previous directories 
```
cd ..
```

#### use the cd command to print the home directory of the current user
```
cd -
```

# Terminal Device Files

- Unique pseudo (or virtual) numbered device files that represent terminal sessions opened by users.
- Used to communicate with individual sessions. 
- Stored in the /dev/pts/ (pseudo terminal session).
- Created  when a user opens a new terminal session.
- Removed when a session closes.


## tty command

- Identify current terminal session.
- Displays filename and location.
- Example: /dev/pts/0

# Inspecting System’s Uptime and Processor Load

## uptime command

- Displays:
	- System’s current time.
	- System up time.
	- Number of users currently logged in.
	- Average % CPU load over the past 1, 5, and 15 minutes. 
		- 0.00 and 1.00 represent no load and full load.
		- Greater than 1.00 signifies excess load (over 100%).

### clear command 
- Clears the terminal screen and places the cursor at the top left of the screen.
- Can also use Ctrl+l for this command.
```
clear
```

## Determining Command Path

tools for identifying the absolute path of the command that will be executed when you run it without specifying its full path.

which, whereis, and type

show the full location of the ls command:

## which command 
- Show command aliases and location.
```
[root@server1 bin]# which ls
alias ls='ls --color=auto'
        /usr/bin/ls
```

## whereis command
- Locates binary, source, and manual files for specified command name. 
```
[root@server1 bin]# whereis ls
ls: /usr/bin/ls /usr/share/man/man1/ls.1.gz /usr/share/man/man1p/ls.1p.gz>)
```

## type command
- Find whether the given command is an alias, shell built-in, file, function, or keyword.
```
type ls
```

## Viewing System Information

#### uname command
- Show system operating system name.
```
[root@server1 bin]# uname
Linux
```

Flags
uname -s ::: Show kernel name.
uname -n ::: Show hostname.
uname -r ::: Show kernel release.
uname -v ::: Show kernel build date.
uname -m ::: Show machine hardware name.
uname -p ::: Show processor type.
uname -i ::: Show hardware platform.
uname -o ::: Show OS name.
uname -a ::: Show kernel name, nodename, release, version, machine, and os.

```
uname
```

```
uname -a
```

	Linux = Kernel name
	server1.example.com = Hostname of the system
	4.18.0-80.el8.x86_64 = Kernel release
	#1 SMP Wed Mar 13 12:02:46 UTC 2019 = Date and time of the kernel built
	x86_64 = Machine hardware name
	x86_64 = Processor type
	x86_64 = Hardware platform
	GNU/Linux = Operating system name

## Viewing CPU Specs

## lscpu command
- Shows CPU:
	- Architecture.
	- Operating modes.
	- Vendor.
	- Family.
	- Model.
	- Speed.
	- Cache memory.
	- Virtualization support type.

```
lscpu
```

	architecture of the CPU (x86_64)
	supported modes of operation (32-bit and 64-bit)
	sequence number of the CPU on this system (1)
	threads per core (1)
	cores per socket (1)
	number of sockets (1)
	vendor ID (GenuineIntel)
	CPU model (58) model name (Intel …)
	speed (2294.784 MHz)
	amount and levels of cache memory (L1d, L1i, L2, and L3)

## Getting Help

### Manual pages
- Informational pages stored in /usr/share/man for each program. 

#### man command

man -k {keyword} ::: perform a keyword search on manual pages.
man -f ::: Equivalent to whatis.
	
#### Commands to find information/help about programs.
- apropos 
- whatis 
- info 
- pinfo 

Directory with additional program documentation ::: /usr/share/doc/

```
man passwd
```

line at the bottom indicates the line number of the manual page. 

### Man page navigation
h ::: Help on navigation.
q ::: Quit the man page.
Up arrow key ::: Scroll up one line.
Enter or Down arrow key ::: Scroll down one line.
f / Spacebar / Page down ::: Move forward one page.
b / Page up ::: Move backward one page.
d / u ::: Move down/up half a page.
g / G ::: Move to the beginning / end of the man pages.
:f ::: Display line number and bytes being viewed.
/pattern ::: Searches forward for the specified pattern.
?pattern ::: Searches backward for the specified pattern.
n / N ::: Find the next / previous occurrence of a pattern.

## Headings in the Manual
NAME :: Name of the command or file with a short description.
SYNOPSIS :: Syntax summary.
DESCRIPTION :: Overview of the command or file.
OPTIONS :: Options available for use.
EXAMPLES :: Some examples to explain the usage.
FILES :: A list of related files.
SEE ALSO :: Reference to other manual pages or topics.
BUGS :: Any reported bugs or issues.
AUTHOR :: Contributor information.

## Manual Sections
- Manual information is split into nine sections for organization and clarity.
- Man searches through each section until it finds a match. 
	- Starts at section 1, then section 2, etc.
- Some commands in Linux also have a configuration file with an identical name. 
	- Ex: passwd command in /usr/bin and the passwd file in /etc.
- Specify the section to find that page only.
	- Ex: ```man 5 passwd```
- Section number is located at the top (header) of the page.

Section 1 :: Refers to user commands.
Section 4 :: Contains special files.
Section 5 :: Describes file formats for many system configuration files.
Section 8 :: Documents system administration and privileged commands designed for the root user.

## Searching by Keyword

#### apropos command
- search all sections of the manual pages and show a list of all entries matching the specified keyword in their names or descriptions.
- Must mandb command in order to build an indexed database of the manual pages prior to using.
```
mandb
```

#### mandb command
- Build an indexed database of the manual pages.

#### Lab: Find a forgotten XFS administration command.
```
man -k xfs
or
apropos xfs
```

#### Lab: Show a brief list of options and a description.
```
passwd --help
or
passwd -?
```

#### whatis command
- same output as ```man -f```
- Display one-line manual page descriptions.
		
## info and pinfo Commands

info and pinfo commands 
- Display command detailed documentation.
- Divided into sections called nodes. The 
- Header:
	- Name of the file being displayed.
	- Names of the current, next, and previous nodes.
- info and pinfo commands is almost identical.

```
info ls
```

u navigate efficiently.

### info page Navigation
Down / Up arrows :: Move forward / backward one line.
Spacebar / Del :: Move forward / backward one page.
q :: Quit the info page.
t :: Go to the top node of the document.
s :: Search 

## Documentation in  /usr/share/doc/

/usr/share/doc/ ::: stores general documentation for installed packages under subdirectories that match their names. 

```
ls -l /usr/share/doc/gzip
```

## Online RHEL Documentation
- docs.redhat.com 
- Release notes and guides on planning, installation, administration, security, storage management, virtualization, etc. 
- access.redhat.com

## Labs
### Lab 2: Navigate Linux Directory Tree

Check your location in the directory tree. 
```
pwd
```

Show file permissions in the current directory including the hidden files. 
```
ls -la
```

Change directory into /etc and confirm the directory change. 
```
cd /etc
pwd
```

Switch back to the directory where you were before, and run pwd again to verify. 
```
cd -
pwd
```

### Lab: Miscellaneous Tasks

Identify the terminal device file.
```
tty
```

Open a couple of terminal sessions. Compare the terminal numbers. 
```
[vagrant@server1 ~]$ tty
/dev/pts/1
```

Execute the uptime command and analyze the system uptime and processor load information. 
```
uptime
```

Use three commands to identify the location of the vgs command. 
```
which vgs
whereis vgs
type vgs
```

### Lab: Identify System and Kernel Information

1. Analyze the basic information about the system and kernel reported. 
```
uname -a
```

Examine the key items relevant to the processor. 
```
lscpu
```

### Lab: Man

View man page for uname.
```
man uname
```

View the 5 man page section for the shadow.
```
man 5 shadow
```



