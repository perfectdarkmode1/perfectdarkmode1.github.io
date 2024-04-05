# Appendix C: Sample RHCSA Exam 3**

  -------------------- ----------------------------------------------------------------
  **Time Duration:**   3 hours
  **Passing Score:**   70% (210 out of 300)
  **Instructions:**    The RHCSA exam, EX200, is offered electronically on a physical
  -------------------- ----------------------------------------------------------------

computer running RHEL 8. The computer has two virtual machines with RHEL
8 running in each one of them. The exam presents two sets of tasks that
are to be completed within the stipulated time in the identified virtual
machine. Firewall and SELinux need to be considered. All settings
performed in the virtual machines must survive reboots, or you will lose
marks. Access to the Internet, printed and electronic material, and
electronic devices is prohibited during the exam.

**[Setup for Sample Exam 3:]{.underline1}**

Build two virtual machines with RHEL 8 Server with GUI (Exercises 1-1
and 1-2). Use a 10GB disk for the OS with default partitioning. Add
1x4GB disk to VM1, 2x1GB disks to VM2, and a network interface to both
virtual machines. Do not configure the network interfaces or create a
normal user account during installation.

**[Instructions:]{.underline1}**

**01:** The following tasks are in addition to the exercises and labs
presented in the book. No solutions are furnished, but hints to
applicable exercises, chapters, or topics are provided in parentheses
for reference.

**02:** Please do not browse the Internet or seek help from other
sources. However, you can refer to the manual pages, and the
documentation under the *usr*share/doc directory. This rule does not
apply to the kernel download task if included.

**03:** The exam tasks should be completed in a terminal window using
only the command line interface (no GUI).

**04:** You can reboot the VM whenever you want during this exam, but
retest the configuration after each reboot for verification.

**05:** Use your knowledge and judgement for any missing configuration
in task description.

**[Tasks:]{.underline1}**

**Task 01:** On VM1, set the system hostname to
[rhcsa3.example.com](http://rhcsa3.example.com){.calibre2} and alias
rhcsa3 using the hostnamectl command. Make sure that the new hostname is
reflected in the command prompt. ([Exercises
16-1](#part0028_split_001.html#id_437){.calibre2} and
[16-5](#part0028_split_001.html#id_458){.calibre2}).

**Task 02:** On rhcsa3, configure a network connection on the primary
network device with IP address 192.168.0.243/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using the nmcli command (use different IP
assignments based on your lab environment). ([Exercise
16-4](#part0028_split_001.html#id_455){.calibre5}).

**[]{#part0038.html#page_544 .calibre5}Task 03:** On VM2, set the system
hostname to [rhcsa4.example.com](http://rhcsa4.example.com){.calibre5}
and alias rhcsa4 using a manual method (modify file by hand). Make sure
that the new hostname is reflected in the command prompt. ([Exercises
16-1](#part0028_split_001.html#id_437){.calibre5} and
[16-5](#part0028_split_001.html#id_458){.calibre5}).

**Task 04:** On rhcsa4, configure a network connection on the primary
network device with IP address 192.168.0.244/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using a manual method (create/modify file by
hand). Use different IP assignments based on your lab environment.
([Exercise 16-3](#part0028_split_001.html#id_452){.calibre5}).

**Task 05:** Run "ping -c2 rhcsa4" on rhcsa3. Run "ping -c2 rhcsa3" on
rhcsa4. You should see 0% loss in both outputs. ([Exercise
16-5](#part0028_split_001.html#id_458){.calibre5}).

**Task 06:** On rhcsa3 and rhcsa4, attach the RHEL 8 ISO image to the VM
and mount it persistently to *mnt*sr0. Define access to both
repositories and confirm. ([Exercise
10-1](#part0022_split_001.html#id_280){.calibre5}).

**Task 07:** On rhcsa3, add HTTP port 8300/tcp to the SELinux policy
database persistently. ([Exercise
21-3](#part0033_split_000.html#page_474){.calibre5}).

**Task 08:** On rhcsa3, create VDO volume called vdo1 on the 4GB disk
with logical size 16GB and mounted with Ext4 structures on *mnt*vdo1.
([Exercises 13-6](#part0025_split_001.html#id_370){.calibre5} and
[13-7](#part0025_split_000.html#page_316){.calibre5}).

**Task 09:** Configure NFS service on rhcsa3 and share *rh_share3 with
rhcsa4. Configure AutoFS direct map on rhcsa4 to mount* rh_share3 on
*mnt*rh_share4. User user80 (create on both systems) should be able to
create files under the share on the NFS server as well as under the
mount point on the NFS client. ([Exercises
5-1](#part0017_split_001.html#id_163){.calibre5},
[17-1](#part0029_split_001.html#id_469){.calibre5}, and
[17-3](#part0029_split_001.html#id_476){.calibre5}).

**Task 10:** Configure NFS service on rhcsa4 and share the home
directory for user60 (create user60 on both systems) with rhcsa3.
Configure AutoFS indirect map on rhcsa3 to automatically mount the home
directory under /nfsdir when user60 logs on to rhcsa3. ([Exercises
5-1](#part0017_split_001.html#id_163){.calibre5},
[17-1](#part0029_split_001.html#id_469){.calibre5},
[17-4,](#part0029_split_001.html#id_477){.calibre5} and
[17-5](#part0029_split_001.html#id_479){.calibre5}).

**Task 11:** On rhcsa4, create Stratis pool pool1 and volume str1 on a
1GB disk and mount it to *mnt*str1. ([Exercise
15-5](#part0027_split_000.html#page_365){.calibre5}).

**Task 12:** On rhcsa4, expand Stratis pool pool1 using the other 1GB
disk. Confirm that *mnt*str1 sees the storage expansion. ([Exercise
15-5](#part0027_split_000.html#page_365){.calibre5}).

**Task 13:** On rhcsa3, create a group called group30 with GID 3000, and
add user60 and user80 to this group. Create a directory called *sdata,
enable setgid bit on it, and add write permission bit for group members.
Set ownership and owning group to root and group30. Create a file called
file1 under* sdata as user60 and modify the file as user80 successfully.
([Exercises 4-5](#part0016_split_001.html#id_130){.calibre5},
[6-4](#part0018_split_001.html#id_182){.calibre5}, and
[6-6](#part0018_split_001.html#id_188){.calibre5}).

**Task 14:** On rhcsa3, create directory *var*dir1 with full permissions
for everyone. Disallow non-owners to remove files. Test by creating file
*var*dir1/stkfile1 as user60 and removing it as user80. ([Exercise
4-6](#part0016_split_001.html#id_132){.calibre5}).

**Task 15:** On rhcsa3, search for all manual pages for the description
containing the keyword "password" and redirect the output to file
*var*tmp/man.out. ([Chapter
02](#part0014_split_000.html#page_35){.calibre5}, topic Searching by
Keyword, and [Chapter 07](#part0019_split_000.html#page_151){.calibre5},
topic: Input, Output, and Error Redirections).

**Task 16:** On rhcsa3, create file lnfile1 under *var*tmp and create
one hard link *var*tmp/lnfile2 and one soft link *boot*file1. Edit
lnfile1 using one link at a time and confirm. (Exercises 3-2 and 3-3).

**Task 17:** On rhcsa3, install module postgresql version 9.6 (select a
different non-default version if 9.6 is not available). ([Exercise
10-5](#part0022_split_001.html#id_297){.calibre5}).

**[]{#part0038.html#page_545 .calibre5}Task 18:** On rhcsa3, add the
http service to the "external" firewalld zone persistently. ([Exercise
201](#part0032_split_001.html#id_532){.calibre5}).

**Task 19:** On rhcsa3, set SELinux type shadow_t on a new file
testfile1 in /usr and ensure that the context is not affected by a
SELinux relabeling. ([Exercises
21-1](#part0033_split_001.html#id_552){.calibre5} and
[21-2](#part0033_split_001.html#id_553){.calibre5}).

**Task 20:** Configure password-less ssh access for user60 from rhcsa3
to rhcsa4. ([Exercise
19-2](#part0031_split_001.html#id_513){.calibre5}).

**Task 21:** Write a bash shell script that checks for the existence of
files (not directories) under the *usr*bin directory that begin with the
letters "ac" and display their statistics (the stat command). ([Chapter
22](#part0034_split_000.html#page_481){.calibre5}: [Table
22-1](#part0034_split_001.html#id_760){.calibre5} and Script07).

**Task 22:** On rhcsa3, launch a named container as user60 with host
port 10000 mapped to container port 80. Employ the latest version of the
ubi7 image. Configure a systemd service to auto-start the container
without the need for user60 to log in. Validate port mapping using an
appropriate podman subcommand. ([Exercises
23-5](#part0035_split_000.html#page_518){.calibre5} and
[23-10](#part0035_split_001.html#id_620){.calibre5}).

**Task 23:** On rhcsa3, launch another named container as user60 with
*host_data01 mapped to* container_data01, one variable ENVIRON=Exam, and
host port 1050 mapped to container port 1050. Use the latest version of
the ubi8 image. Configure a separate systemd service to auto-start the
container without the need for user60 to log in. Create a file under the
shared directory and validate data persistence. Verify port mapping and
variable settings using appropriate podman subcommands. ([Exercises
23-5](#part0035_split_000.html#page_518){.calibre5},
[23-7](#part0035_split_001.html#id_615){.calibre5},
[23-8](#part0035_split_001.html#id_617){.calibre5}, and
[23-10](#part0035_split_001.html#id_620){.calibre5}).

**Reboot the system and validate the configuration.**

[]{#part0039.html}
