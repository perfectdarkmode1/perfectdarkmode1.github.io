## Appendix B: Sample RHCSA Exam 2 {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

Time Duration:3 hours

Passing Score:70% (210 out of 300)

Instructions: The RHCSA exam, EX200, is offered electronically on a
physical computer running RHEL 9 as the base operating system. The
computer has two virtual machines with RHEL 9 running in each one of
them. The exam presents two sets of tasks that are to be completed
within the stipulated time in the identified virtual machine. Firewall
and SELinux must be taken into consideration for all network services.
All settings performed in the virtual machines must survive system
reboots, or you will lose marks. Access to the Internet, printed and
electronic material, and electronic devices is prohibited during the
exam.

\

### Setup for Sample Exam 2: {.style3}

Build a virtual machine with RHEL 9 Server with GUI (Exercises 1-1 and
1-2). Use a 20GB disk for the OS with default partitioning. Add 1x400MB
disk and a network interface. Do not configure the network interface or
create a normal user account during installation.

\

### Instructions: {.style3}

01: The following tasks are in addition to the exercises and labs
presented in the book. No solutions are furnished, but hints to
applicable exercises, chapters, or topics are provided in parentheses
for reference.

\

02: Do not browse the Internet or seek help from other sources. However,
you can refer to the manual pages, and the documentation under the
/usr/share/doc directory. This rule does not apply to the kernel
download task if included.

\

03: All exam tasks must be executed in a terminal window using only the
command line interface (no GUI).

\

04: You can reboot the VM whenever you want during this exam but retest
the configuration after each reboot for verification.

\

05: Use your knowledge and judgement for any missing configuration in
task description.

\

06: Read all the storage tasks and set your strategy for disk
partitioning prior to attempting them.

\

### Tasks: {.style3}

Task 01: Using the nmcli command, configure a network connection on the
primary network device with IP address 192.168.0.242/24, gateway
192.168.0.1, and nameserver 192.168.0.1. Use different IP assignments
based on your lab environment. (Exercise 15-3).

\

Task 02: Using the hostnamectl command, set the system hostname to
rhcsa2.example.com and alias rhcsa2. Make sure that the new hostname is
reflected in the command prompt. (Exercises 15-1 and 15-5).

\

Task 03: Create a user account called user70 with UID 7000 and comments
"I am user70". Set the maximum allowable inactivity for this user to 30
days. (Exercises 5-2; Exercise 6-1 or 6-2).

\

Task 04: Create a user account called user50 with a non-interactive
shell. (Exercise 5-4).

\

Task 05: Attach the RHEL 9 ISO image to the VM and mount it persistently
to /mnt/dvdrom. Define access to both repositories and confirm.
(Exercise 9-1).

\

Task 06: Create a logical volume called lv1 of size equal to 10 LEs in
vg1 volume group (create vg1 with PE size 8MB in a partition on the
400MB disk). Initialize the logical volume with XFS type and mount it on
/mnt/lvfs1. Create a file called lv1file1 in the mount point. Set the
file system to automatically mount at each system reboot. (Exercises
13-6, 13-7, and 14-2; Chapter 14, topic: Automatically Mounting a File
System at Reboots).

\

Task 07: Add a group called group20 and change group membership on
/mnt/lvfs1 to group20. Set read/write/execute permissions on /mnt/lvfs1
for the owner, group members, and others. (Exercises 6-4 and 6-6;
Exercise 4-1 or 4-2).

\

Task 08: Extend the file system in the logical volume lv1 by 64MB
without unmounting it and without losing any data. Confirm the new size
for the logical volume and the file system. (Exercise 14-3).

\

Task 09: Create a swap partition of size 85MB on the 400MB disk. Use its
UUID and ensure it is activated after every system reboot. (Exercise
14-5; Chapter 14, topic: Automatically Mounting a File System at
Reboots).

\

Task 10: Create a disk partition of size 100MB on the 400MB disk and
format it with Ext4 file system structures. Assign label stdlabel to the
file system. Mount the file system on /mnt/stdfs1 persistently using the
label. Create file stdfile1 in the mount point. (Exercise 13-2 or 13-4;
Chapter 14, topic: Labeling a File System; and Exercise 14-1).

\

Task 11: Use the tar and gzip command combination to create a compressed
archive of the /etc directory. Store the archive under /var/tmp using a
filename of your choice. (Exercise 3-1).

\

Task 12: Create a directory /direct01 and apply SELinux contexts for
/root to it. (Exercise 20-2).

\

Task 13: Set up a cron job for user70 to search for files by the name
"core" in the /var directory and copy them to the directory
/var/tmp/coredir1. This job should run every Monday at 1:20 a.m.
(Chapter 04, topics: Using the find Command and Using find with -exec
and -ok Flags; and Exercise 8-4).

\

Task 14: Search for all files in the entire directory structure that
have been modified in the past 30 days and save the file listing in the
/var/tmp/modfiles.txt file. (Chapter 04, topics: Using the find Command
and Using find with -exec and -ok Flags).

\

Task 15: Modify the bootloader program and set the default autoboot
timer value to 2 seconds. (Exercise 11-1).

\

Task 16: Determine the recommended tuning profile for the system and
apply it. (Exercise 12-2).

\

Task 17: Configure Chrony to synchronize system time with the hardware
clock. Remove all other NTP sources. (Exercise 17-1).

\

Task 18: Install package group called "Development Tools" and capture
its information in /var/tmp/systemtools.out file. (Chapter 03, topic:
Regular Expressions; and Exercise 10-3).

\

Task 19: Lock user account user70. Use regular expressions to capture
the line that shows the lock and store the output in file
/var/tmp/user70.lock. (Chapter 03, topic: Regular Expressions; and
Exercise 6-3).

\

Task 20: Write a bash shell script so that it prints RHCSA when RHCE is
passed as an argument, and vice versa. If no argument is provided, the
script should print a usage message and quit with exit value 5. (Chapter
21: Script10).

\

Task 21: Launch a rootful container and configure it to auto-start via
systemd. (Exercise 22-10).

\

Task 22: Launch a rootless container as user80 with /data01 mapped to
/data01 using the latest version of the ubi9 image. Configure a systemd
service to auto-start the container on system reboots without the need
for user80 to log in. Create files under the shared mount point and
validate data persistence. (Exercise 22-7 and 22-10).

\

### Reboot the system and validate the configuration. {.style3}

::: {style="page-break-before: always;"}
:::

[]{#chapter0688.html}
