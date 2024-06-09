## Appendix D: Sample RHCSA Exam 4 {.style3}

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

### Setup for Sample Exam 4: {.style3}

Build two virtual machines with RHEL 9 Server with GUI (Exercises 1-1
and 1-2). Use a 20GB disk for the OS with default partitioning. Add
1x5GB disk to VM2 and a network interface to both virtual machines. Do
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

Task 01: On VM1, set the system hostname to rhcsa5.example.com and alias
rhcsa5 using the hostnamectl command. Make sure that the new hostname is
reflected in the command prompt. (Exercises 15-1 and 15-5).

\

Task 02: On rhcsa5, configure a network connection on the primary
network device with IP address 192.168.0.245/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using the nmcli command. Use different IP
assignments based on your lab environment. (Exercise 15-4).

\

Task 03: On VM2, set the system hostname to rhcsa6.example.com and alias
rhcsa6 using a manual method (modify file by hand). Make sure that the
new hostname is reflected in the command prompt. (Exercises 15-1 and
15-5).

\

Task 04: On rhcsa6, configure a network connection on the primary
network device with IP address 192.168.0.246/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using a manual method (create/modify files by
hand). Use different IP assignments based on your lab environment.
(Exercise 15-3).

\

Task 05: Run "ping -c2 rhcsa6" on rhcsa5. Run "ping -c2 rhcsa5" on
rhcsa6. You should see 0% loss in both outputs. (Exercise 15-5).

\

Task 06: On rhcsa5 and rhcsa6, attach the RHEL 9 ISO image to the VM and
mount it persistently to /mnt/sr0. Define access to both repositories
and confirm. (Exercise 9-1).

\

Task 07: Export /share5 on rhcsa5 and mount it to /share6 persistently
on rhcsa6. (Exercises 16-1 and 16-2).

\

Task 08: Use NFS to export home directories for all users (u1, u2, and
u3) on rhcsa6 so that their home directories become available under
/home1 when they log on to rhcsa5. Create u1, u2, and u3. (Exercises
5-1, 16-1 and 16-5).

\

Task 09: On rhcsa5, add HTTP port 8400/UDP to the public firewall zone
persistently. (Exercise 19-1).

\

Task 10: Configure passwordless ssh access for u1 from rhcsa5 to rhcsa6.
Copy the directory /etc/sysconfig from rhcsa5 to rhcsa6 under
/var/tmp/remote securely. (Exercise 18-2; Chapter 18, topic:
Transferring Files Remotely Using sftp).

\

Task 11: On rhcsa6, create LVM VDO volume vdo2 on the 5GB disk with
logical size 20GB and mounted persistently with XFS structures on
/mnt/vdo2. (Exercises 13-12 and 14-4).

\

Task 12: On rhcsa6, flip the value of the Boolean nfs_export_all_rw
persistently. (Exercise 20-5).

\

Task 13: On rhcsa5 and rhcsa6, set the tuning profile to powersave.
(Exercise 12-2).

\

Task 14: On rhcsa5, create file lnfile1 under /var/tmp and create three
hard links called hard1, hard2, and hard3 for it. Identify the inode
number associated with all four files. Edit any of the files and observe
the metadata for all the files for confirmation. (Exercise 3-2).

\

Task 15: On rhcsa5, members (user100 and user200) of group100 should be
able to collaborate on files under /shared but cannot delete each
other's files. (Exercises 4-5 and 4-6).

\

Task 16: On rhcsa6, list all files that are part of the "setup" package,
and use regular expressions and I/O redirection to send the output lines
containing "hosts" to /var/tmp/setup.pkg. (Exercise 9-2; Chapter 07,
topics: Regular Expressions, and Input, Output, and Error Redirections).

\

Task 17: On rhcsa5, check the current version of the Linux kernel.
Download and install the latest version of the kernel from Red Hat
website. Ensure that the existing kernel and its configuration remain
intact. Reboot the system and confirm the new version is loaded.
(Exercise 11-3; Chapter 02, topic: Viewing System Information).

\

Task 18: On rhcsa5, configure journald to store messages permanently
under /var/log/journal and fall back to memory-only option if
/var/log/journal directory does not exist or has permission/access
issues. (Exercise 12-1).

\

Task 19: Write a bash shell script that defines an environment variable
called ENV1=book1 and creates a user account that matches the value of
the variable. (Chapter 21: Script02 and Script03).

\

Task 20: On rhcsa5, launch a named rootful container with host port 443
mapped to container port 443. Employ the latest version of the ubi9
image. Configure a systemd service to auto-start the container at system
reboots. Validate port mapping using an appropriate podman subcommand.
(Exercises 22-6 and 22-10).

\

Task 21: On rhcsa5, launch a named rootless container as user100 with
/data01 mapped to /data01 and two variables KERN=\$(uname -r) and SHELL
defined. Use the latest version of the ubi8 image. Configure a systemd
service to auto-start the container at system reboots without the need
for user100 to log in. Create a file under the shared mount point and
validate data persistence. Verify port mapping using an appropriate
podman subcommand. (Exercises 22-6, 22-8, and 22-11).

\

Task 22: On rhcsa5, write a containerfile to include the PATH
environment variable output in a custom ubi9 image. Launch a named
rootless container as user100 using this image. Confirm command
execution. (Exercises 22-3 and 22-4).

\

### Reboot the system and validate the configuration. {.style3}

::: {style="page-break-before: always;"}
:::

[]{#chapter0690.html}
