## Appendix A: Sample RHCSA Exam 1 {.style3}

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

### Setup for Sample Exam 1: {.style3}

Build a virtual machine with RHEL 9 Server with GUI (Exercises 1-1 and
1-2). Use a 20GB disk for the OS with default partitioning. Add 2x300MB
disks and a network interface. Do not configure the network interface or
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

### Tasks: {.style3}

Task 01: Assuming the root user password is lost, and your system is
running in multi-user target with no current root session open. Reboot
the system into an appropriate target level and reset the root user
password to root1234. (Exercise 11-2). After completing this task, log
in as the root user and perform the remaining tasks presented below.

\

Task 02: Using a manual method (create/modify files by hand), configure
a network connection on the primary network device with IP address
192.168.0.241/24, gateway 192.168.0.1, and nameserver 192.168.0.1. Use
different IP assignments based on your lab setup. (Exercise 15-3).

\

Task 03: Using a manual method (modify file by hand), set the system
hostname to rhcsa1.example.com and alias rhcsa1. Make sure that the new
hostname is reflected in the command prompt. (Exercises 15-1 and 15-5).

\

Task 04: Set the default boot target to multi-user. (Chapter 12, topic:
Managing Target Units).

\

Task 05: Set SELinux to permissive mode. (Chapter 20, topic: Viewing and
Controlling SELinux Operational State).

\

Task 06: Perform a case-insensitive search for all lines in the
/usr/share/dict/linux.words file that begin with the pattern
"essential". Redirect the output to /var/tmp/pattern.txt file. Make sure
that empty lines are omitted. (Chapter 07, topic: Regular Expressions).

\

Task 07: Change the primary command prompt for the root user to display
the hostname, username, and current working directory information in
that order. Update the per-user initialization file for permanence.
(Exercise 7-1).

\

Task 08: Create user accounts called user10, user20, and user30. Set
their passwords to Temp1234. Make user10 and user30 accounts to expire
on December 31, 2023. (Exercise 5-1; Exercise 6-1 or 6-2).

\

Task 09: Create a group called group10 and add user20 and user30 as
secondary members. (Exercise 6-4).

\

Task 10: Create a user account called user40 with UID 2929. Set the
password to user1234. (Exercise 5-2).

\

Task 11: Attach the RHEL 9 ISO image to the VM and mount it persistently
to /mnt/cdrom. Define access to both repositories and confirm. (Exercise
9-1).

\

Task 12: Create a logical volume called lvol1 of size 280MB in vgtest
volume group. Mount the ext4 file system persistently to /mnt/mnt1.
(Exercises 13-6, 13-7, and 14-3).

\

Task 13: Change group membership on /mnt/mnt1 to group10. Set
read/write/execute permissions on /mnt/mnt1 for group members and revoke
all permissions for public. (Exercises 6-4 and 6-6; Exercise 4-1 or
4-2).

\

Task 14: Create a logical volume called lvswap of size 280MB in vgtest
volume group. Initialize the logical volume for swap use. Use the UUID
and place an entry for persistence. (Exercises 13-13-6, 13-7, and 14-5;
Chapter 14, topic: Automatically Mounting a File System at Reboots).

\

Task 15: Use the combination of tar and bzip2 commands to create a
compressed archive of the /usr/lib directory. Store the archive under
/var/tmp as usr.tar.bz2. (Exercise 3-1).

\

Task 16: Create a directory hierarchy /dir1/dir2/dir3/dir4 and apply
SELinux contexts of /etc on it recursively. (Chapter 03, topic: Creating
Files and Directories; and Exercise 20-2).

\

Task 17: Enable access to the atd service for user20 and deny for
user30. (Chapter 08, topic: Controlling User Access).

\

Task 18: Add a custom message "This is RHCSA sample exam on \$(date) by
\$LOGNAME" to the /var/log/messages file as the root user. Use regular
expression to confirm the message entry to the log file. (Chapter 07,
topic: Regular Expressions; Chapter 12, topic: Logging Custom Messages).

\

Task 19: Allow user20 to use sudo without being prompted for their
password. (Chapter 06, topic: Doing as Superuser (or Doing as Substitute
User)).

\

Task 20: Write a bash shell script to create three user
accounts---user555, user666, and user777---with no login shell and
passwords matching their usernames. The script should also extract the
three usernames from the /etc/passwd file and redirect them into
/var/tmp/newusers. (Chapter 21, topic: Script12; Chapter 07, topic:
Regular Expressions, and Input, Output, and Error Redirections).

\

Task 21: Launch a container as user20 using the latest version of ubi8
image. Configure the container to auto-start at system reboots without
the need for user20 to log in. (Exercise 22-11).

\

Task 22: Launch a container as user20 using the latest version of ubi9
image with two environment variables SHELL and HOSTNAME. Configure the
container to auto-start via systemd without the need for user20 to log
in. Connect to the container and verify variable settings. (Exercises
22-8 and 22-11).

\

### Reboot the system and validate the configuration. {.style3}

::: {style="page-break-before: always;"}
:::

[]{#chapter0687.html}
