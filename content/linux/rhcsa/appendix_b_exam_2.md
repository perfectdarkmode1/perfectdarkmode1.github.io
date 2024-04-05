# Appendix B: Sample RHCSA Exam 2**

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

**[Setup for Sample Exam 2:]{.underline1}**

Build a virtual machine with RHEL 8 Server with GUI (Exercises 1-1 and
1-2). Use a 10GB disk for the OS with default partitioning. Add 1x400MB
disk and a network interface. Do not configure the network interface or
create a normal user account during installation.

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

**Task 01:** Using the nmcli command, configure a network connection on
the primary network device with IP address 192.168.0.242/24, gateway
192.168.0.1, and nameserver 192.168.0.1. Use different IP assignments
based on your lab environment. ([Exercise
16-4](#part0028_split_001.html#id_455){.calibre2}).

**Task 02:** Using the hostnamectl command, set the system hostname to
[rhcsa2.example.com](http://rhcsa2.example.com){.calibre5} and alias
rhcsa2. Make sure that the new hostname is reflected in the command
prompt. ([Exercises 16-1](#part0028_split_001.html#id_437){.calibre5}
and [16-5](#part0028_split_001.html#id_458){.calibre5}).

**Task 03:** Create a user account called user70 with UID 7000 and
comments "I am user70". Set the maximum allowable inactivity for this
user to 30 days. ([Exercises
5-2](#part0017_split_001.html#id_164){.calibre5}, and
[6-1](#part0018_split_001.html#id_177){.calibre5} or
[6-2](#part0018_split_000.html#page_139){.calibre5}).

**Task 04:** Create a user account called user50 with a non-interactive
shell. ([Exercise 5-4](#part0017_split_001.html#id_166){.calibre5}).

**[]{#part0037.html#page_540 .calibre5}Task 05:** Create a file called
testfile1 under *var*tmp with ownership and owning group set to root.
Configure access ACLs on the file and give user10 read and write access.
Test access by logging in as user10 and editing the file. ([Chapter
03](#part0015_split_000.html#page_61){.calibre5}, topic: Creating Files
and Directories, and [Exercise
4-7](#part0016_split_001.html#id_140){.calibre5}).

**Task 06:** Attach the RHEL 8 ISO image to the VM and mount it
persistently to *mnt*dvdrom. Define access to both repositories and
confirm. ([Exercise 10-1](#part0022_split_001.html#id_280){.calibre5}).

**Task 07:** Create a logical volume called lv1 of size equal to 10 LEs
in vg1 volume group (create vg1 with PE size 8MB in a partition on the
400MB disk). Initialize the logical volume with XFS type and mount it on
*mnt*lvfs1. Create a file called lv1file1 in the mount point. Set the
file system to automatically mount at each system reboot. ([Exercises
14-1](#part0026_split_001.html#id_384){.calibre5},
[14-2](#part0026_split_001.html#id_385){.calibre5}, and
[15-3](#part0027_split_001.html#id_419){.calibre5}).

**Task 08:** Add a group called group20 and change group membership on
*mnt*lvfs1 to group20. Set read/write/execute permissions on *mnt*lvfs1
for the owner, group members, and others. ([Exercises
6-4](#part0018_split_001.html#id_182){.calibre5},
[6-6](#part0018_split_001.html#id_188){.calibre5}, and [either
4-1](#part0016_split_001.html#id_121){.calibre5} or
[4-2](#part0016_split_000.html#page_93){.calibre5}).

**Task 09:** Extend the file system in the logical volume lv1 by 64MB
without unmounting it and without losing any data. Confirm the new size
for the logical volume and the file system. ([Exercise
15-4](#part0027_split_001.html#id_420){.calibre5}).

**Task 10:** Create a swap partition of size 85MB on the 400MB disk. Use
its UUID and ensure it is activated after every system reboot.
([Exercise 15-6](#part0027_split_001.html#id_425){.calibre5}).

**Task 11:** Create a disk partition of size 100MB on the 400MB disk and
format it with Ext4 file system structures. Assign label stdlabel to the
file system. Mount the file system on *mnt*stdfs1 persistently using the
label. Create file stdfile1 in the mount point. ([Exercise
13-2](#part0025_split_001.html#id_363){.calibre5} or
[13-4](#part0025_split_001.html#id_366){.calibre5}, [Chapter
15](#part0027_split_000.html#page_345){.calibre5}, topic: Labeling a
File System, and [Exercise
15-1](#part0027_split_000.html#page_356){.calibre5}).

**Task 12:** Use the tar and gzip command combination to create a
compressed archive of the /etc directory. Store the archive under
*var*tmp using a filename of your choice. ([Exercise
3-1](#part0015_split_001.html#id_84){.calibre5}).

**Task 13:** Create a directory *direct01 and apply SELinux contexts
for* root to it. ([Exercise
21-2](#part0033_split_001.html#id_553){.calibre5}).

**Task 14:** Set up a cron job for user70 to search for files by the
name "core" in the /var directory and copy them to the directory
*var*tmp/coredir1. This job should run every Monday at 1:20 a.m.
([Chapter 04](#part0016_split_000.html#page_89){.calibre5}, topics:
Using the find Command, and Using find with -exec and -ok Flags, and
[Exercise 8-4](#part0020_split_001.html#id_237){.calibre5}).

**Task 15:** Search for all files in the entire directory structure that
have been modified in the past 30 days and save the file listing in the
*var*tmp/modfiles.txt file. ([Chapter
04](#part0016_split_000.html#page_89){.calibre5}, topics: Using the find
Command and Using find with -exec and -ok Flags).

**Task 16:** Modify the bootloader program and set the default autoboot
timer value to 2 seconds. ([Exercise
11-1](#part0023_split_001.html#id_315){.calibre5}).

**Task 17:** Determine the recommended tuning profile for the system and
apply it. ([Exercise 12-2](#part0024_split_001.html#id_348){.calibre5}).

**Task 18:** Configure Chrony to synchronize system time with the
hardware clock. Remove all other NTP sources. ([Exercise
18-1](#part0030_split_001.html#id_491){.calibre5}).

**Task 19:** Install package group called "Development Tools" and
capture its information in *var*tmp/systemtools.out file. ([Chapter
03](#part0015_split_000.html#page_61){.calibre5}, topic: Regular
Expressions, and [Exercise
10-3](#part0022_split_001.html#id_290){.calibre5}).

**Task 20:** Lock user account user70. Use regular expressions to
capture the line that shows the lock and store the output in file
*var*tmp/user70.lock. ([Chapter
03](#part0015_split_000.html#page_61){.calibre5}, topic: Regular
Expressions, and [Exercise
6-3](#part0018_split_001.html#id_180){.calibre5}).

**[]{#part0037.html#page_541 .calibre5}Task 21:** Write a bash shell
script so that it prints RHCSA when RHCE is passed as an argument, and
vice versa. If no argument is provided, the script should print a usage
message and quit with exit value 5. ([Chapter
22](#part0034_split_000.html#page_481){.calibre5}: Script10).

**Task 22:** Launch a root container and configure it to auto-start via
systemd. ([Exercise 23-9](#part0035_split_001.html#id_619){.calibre5}).

**Task 23:** Launch a container as user80 with *data01 mapped to* data01
using the latest version of the ubi8 image. Configure a systemd service
to auto-start the container on system reboots without the need for
user80 to log in. Create files under the shared mount point and validate
data persistence. ([Exercise
23-7](#part0035_split_001.html#id_615){.calibre5} and
[23-10](#part0035_split_001.html#id_620){.calibre5}).

**Reboot the system and validate the configuration.**

[]{#part0038.html}
