## Appendix C: Sample RHCSA Exam 3 {.style3}

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

### Setup for Sample Exam 3: {.style3}

Build two virtual machines with RHEL 9 Server with GUI (Exercises 1-1
and 1-2). Use a 20GB disk for the OS with default partitioning. Add
1x5GB disk to VM1 and a network interface to both virtual machines. Do
not configure the network interfaces or create a normal user account
during installation.

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

Task 01: On VM1, set the system hostname to rhcsa3.example.com and alias
rhcsa3 using the hostnamectl command. Make sure that the new hostname is
reflected in the command prompt. (Exercises 15-1 and 15-5).

\

Task 02: On rhcsa3, configure a network connection on the primary
network device with IP address 192.168.0.243/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using the nmcli command (use different IP
assignments based on your lab environment). (Exercise 15-4).

\

Task 03: On VM2, set the system hostname to rhcsa4.example.com and alias
rhcsa4 using a manual method (modify file by hand). Make sure that the
new hostname is reflected in the command prompt. (Exercises 15-1 and
15-5).

\

Task 04: On rhcsa4, configure a network connection on the primary
network device with IP address 192.168.0.244/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using a manual method (create/modify files by
hand). Use different IP assignments based on your lab environment.
(Exercise 15-3).

\

Task 05: Run "ping -c2 rhcsa4" on rhcsa3. Run "ping -c2 rhcsa3" on
rhcsa4. You should see 0% loss in both outputs. (Exercise 15-5).

\

Task 06: On rhcsa3 and rhcsa4, attach the RHEL 9 ISO image to the VM and
mount it persistently to /mnt/sr0. Define access to both repositories
and confirm. (Exercise 9-1).

\

Task 07: On rhcsa3, add HTTP port 8300/TCP to the SELinux policy
database persistently. (Exercise 20-3).

\

Task 08: On rhcsa3, create LVM VDO volume called vdo1 on the 5GB disk
with logical size 20GB and mounted with Ext4 structures on /mnt/vdo1.
(Exercises 13-12 and 14-4; Chapter 14, topic: Automatically Mounting a
File System at Reboots).

\

Task 09: Configure NFS service on rhcsa3 and share /rh_share3 with
rhcsa4. Configure AutoFS direct map on rhcsa4 to mount /rh_share3 on
/mnt/rh_share4. User user80 (create on both systems) should be able to
create files under the share on the NFS server as well as under the
mount point on the NFS client. (Exercises 5-1, 16-1, and 16-3).

\

Task 10: Configure NFS service on rhcsa4 and share the home directory
for user60 (create user60 on both systems) with rhcsa3. Configure AutoFS
indirect map on rhcsa3 to automatically mount the home directory under
/nfsdir when user60 logs on to rhcsa3. (Exercises 5-1, 16-1, 16-4, and
16-5).

\

Task 11: On rhcsa3, create a group called group30 with GID 3000, and add
user60 and user80 to this group. Create a directory called /sdata,
enable setgid bit on it, and add write permission bit for group members.
Set ownership and owning group to root and group30. Create a file called
file1 under /sdata as user60 and modify the file as user80 successfully.
(Exercises 4-5, 6-4, and 6-6).

\

Task 12: On rhcsa3, create directory /var/dir1 with full permissions for
everyone. Disallow non-owners to remove files. Test by creating file
/var/dir1/stkfile1 as user60 and removing it as user80. (Exercise 4-6).

\

Task 13: On rhcsa3, search for all manual pages for the description
containing the keyword "password" and redirect the output to file
/var/tmp/man.out. (Chapter 02, topic: Searching by Keyword; Chapter 07,
topic: Input, Output, and Error Redirections).

\

Task 14: On rhcsa3, create file lnfile1 under /var/tmp and create one
hard link /var/tmp/lnfile2 and one soft link /boot/file1. Edit lnfile1
using one link at a time and confirm. (Exercises 3-2 and 3-3).

\

Task 15: On rhcsa3, install software group called "Legacy UNIX
Compatibility". (Exercise 10-3).

\

Task 16: On rhcsa3, add the http service to "external" firewalld zone
persistently. (Exercise 19-1).

\

Task 17: On rhcsa3, set SELinux type shadow_t on a new file testfile1 in
/usr and ensure that the context is not affected by a SELinux
relabeling. (Chapter 03, topic: File and Directory Operations; Exercises
20-1 and 20-2).

\

Task 18: Configure passwordless ssh access for user60 from rhcsa3 to
rhcsa4. (Exercise 18-2).

\

Task 19: Write a bash shell script that checks for the existence of
files (not directories) under the /usr/bin directory that begin with the
letters "ac" and display their statistics (the stat command). (Chapter
21: Table 21-1 and Script07).

\

Task 20: On rhcsa3, write a containerfile to include the ls and pwd
commands in a custom ubi8 image. Launch a named rootless container as
user60 using this image. Confirm command execution. (Exercises 22-3 and
22-4).

\

Task 21: On rhcsa3, launch a named rootless container as user60 with
host port 10000 mapped to container port 80. Employ the latest version
of the ubi8 image. Configure a systemd service to autostart the
container without the need for user60 to log in. Validate port mapping
using an appropriate podman subcommand. (Exercises 22-4 and 22-11).

\

Task 22: On rhcsa3, launch another named rootless container (use a
unique name for the container) as user60 with /host_data01 mapped to
/container_data01, one variable ENVIRON=Exam, and host port 1050 mapped
to container port 1050. Use the latest version of the ubi9 image.
Configure a separate systemd service to auto-start the container without
the need for user60 to log in. Create a file under the shared directory
and validate data persistence. Verify port mapping and variable settings
using appropriate podman subcommands. (Exercises 22-6, 22-8, 22-7, and
22-11).

\

### Reboot the system and validate the configuration. {.style3}

::: {style="page-break-before: always;"}
:::

[]{#chapter0689.html}
