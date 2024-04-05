# Appendix A: Sample RHCSA Exam 1**

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

**[Setup for Sample Exam 1:]{.underline1}**

Build a virtual machine with RHEL 8 Server with GUI (Exercises 1-1 and
1-2). Use a 10GB disk for the OS with default partitioning. Add 2x300MB
disks and a network interface. Do not configure the network interface or
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

**Task 01:** Assuming the root user password is lost, and your system is
running in multi-user target with no current root session open. Reboot
the system into an appropriate target level, and reset the root user
password to root1234. ([Exercise
11-2](#part0023_split_001.html#id_317){.calibre2}). After completing
this task, log in as the root user and perform the remaining tasks
presented below.

**Task 02:** Using a manual method (create/modify files by hand),
configure a network connection on the primary network device with IP
address 192.168.0.241/24, gateway 192.168.0.1, and nameserver
192.168.0.1. Use different IP assignments based on your lab setup.
([Exercise 16-3](#part0028_split_001.html#id_452){.calibre5}).

**[]{#part0036.html#page_536 .calibre5}Task 03:** Using a manual method
(modify file by hand), set the system hostname to
[rhcsa1.example.com](http://rhcsa1.example.com){.calibre5} and alias
rhcsa1. Make sure that the new hostname is reflected in the command
prompt. ([Exercises 16-1](#part0028_split_001.html#id_437){.calibre5}
and [16-5](#part0028_split_001.html#id_458){.calibre5}).

**Task 04:** Set the default boot target to multi-user. ([Chapter
12](#part0024_split_000.html#page_271){.calibre5}, topic: Managing
Target Units).

**Task 05:** Set SELinux to permissive mode. ([Chapter
21](#part0033_split_000.html#page_461){.calibre5}, topic: Viewing and
Controlling SELinux Operational State).

**Task 06:** Perform a case-insensitive search for all lines in the
*usr*share/dict/linux.words file that begin with the pattern
"essential". Redirect the output to *var*tmp/pattern.txt file. Make sure
that empty lines are omitted. ([Chapter
07](#part0019_split_000.html#page_151){.calibre5}, topic: Regular
Expressions).

**Task 07:** Change the primary command prompt for the root user to
display the hostname, username, and current working directory
information in that order. Update the peruser initialization file for
permanence. ([Exercise
7-1](#part0019_split_001.html#id_201){.calibre5}).

**Task 08:** Create user accounts called user10, user20, and user30. Set
their passwords to Temp1234. Make user10 and user30 accounts to expire
on December 31, 2021. ([Exercises
5-1](#part0017_split_001.html#id_163){.calibre5}, and
[6-1](#part0018_split_001.html#id_177){.calibre5} or
[6-2](#part0018_split_000.html#page_139){.calibre5}).

**Task 09:** Create a group called group10 and add user20 and user30 as
secondary members. ([Exercise
6-4](#part0018_split_001.html#id_182){.calibre5}).

**Task 10:** Create a user account called user40 with UID 2929. Set the
password to user1234. ([Exercise
5-2](#part0017_split_001.html#id_164){.calibre5}).

**Task 11:** Create a directory called dir1 under *var*tmp with
ownership and owning group set to root. Configure default ACLs on the
directory and give user10 read, write, and execute permissions.
([Exercise 4-8](#part0016_split_000.html#page_110){.calibre5}).

**Task 12:** Attach the RHEL 8 ISO image to the VM and mount it
persistently to *mnt*cdrom. Define access to both repositories and
confirm. ([Exercise 10-1](#part0022_split_001.html#id_280){.calibre5}).

**Task 13:** Create a logical volume called lvol1 of size 280MB in
vgtest volume group. Mount the ext4 file system persistently to
*mnt*mnt1. ([Exercises
14-1](#part0026_split_001.html#id_384){.calibre5},
[14-2](#part0026_split_001.html#id_385){.calibre5}, and
[15-3](#part0027_split_001.html#id_419){.calibre5}).

**Task 14:** Change group membership on *mnt*mnt1 to group10. Set
read/write/execute permissions on *mnt*mnt1 for group members, and
revoke all permissions for public. ([Exercises
6-4](#part0018_split_001.html#id_182){.calibre5},
[6-6](#part0018_split_001.html#id_188){.calibre5}, and [either
4-1](#part0016_split_001.html#id_121){.calibre5} or
[4-2](#part0016_split_000.html#page_93){.calibre5}).

**Task 15:** Create a logical volume called lvswap of size 280MB in
vgtest volume group. Initialize the logical volume for swap use. Use the
UUID and place an entry for persistence. ([Exercise
15-6](#part0027_split_001.html#id_425){.calibre5}).

**Task 16:** Use the combination of tar and bzip2 commands to create a
compressed archive of the *usr*lib directory. Store the archive under
*var*tmp as usr.tar.bz2. ([Exercise
3-1](#part0015_split_001.html#id_84){.calibre5}).

**Task 17:** Create a directory hierarchy *dir1*dir2/dir3/dir4 and apply
SELinux contexts of /etc on it recursively. ([Chapter
03](#part0015_split_000.html#page_61){.calibre5}, topic: Creating Files
and Directories, and [Exercise
21-2](#part0033_split_001.html#id_553){.calibre5}).

**Task 18:** Enable access to the atd service for user20 and deny for
user30. ([Chapter 08](#part0020_split_000.html#page_175){.calibre5},
topic: Controlling User Access).

**Task 19:** Add a custom message "This is RHCSA sample exam on \$(date)
by \$LOGNAME" to the *var*log/messages file as the root user. Use
regular expression to confirm the message entry to the log file.
([Chapter 07](#part0019_split_000.html#page_151){.calibre5}, topic:
Regular Expressions, and [Chapter
12](#part0024_split_000.html#page_271){.calibre5}, topic: Logging Custom
Messages).

**[]{#part0036.html#page_537 .calibre5}Task 20:** Allow user20 to use
sudo without being prompted for their password. ([Chapter
06](#part0018_split_000.html#page_135){.calibre5}, topic: Doing as
Superuser (or Doing as Substitute User)).

**Task 21:** Write a bash shell script to create three user
accounts---user555, user666, and user777---with no login shell and
passwords matching their usernames. The script should also extract the
three usernames from the *etc*passwd file and redirect them into
*var*tmp/newusers. ([Chapter
22](#part0034_split_000.html#page_481){.calibre5}: Script12 and [Chapter
07](#part0019_split_000.html#page_151){.calibre5}, topics: Regular
Expressions, and Input, Output, and Error Redirections).

**Task 22:** Launch a simple container as user20 using the latest
version of ubi7 image. Configure the container to auto-start at system
reboots without the need for user20 to log in. ([Exercise
23-10](#part0035_split_001.html#id_620){.calibre5}).

**Task 23:** Launch another container as user20 using the latest version
of ubi8 image with two environment variables SHELL and HOSTNAME.
Configure the container to auto-start via systemd without the need for
user20 to log in. Connect to the container and verify variable settings.
([Exercise 23-7](#part0035_split_001.html#id_615){.calibre5} and
[23-10](#part0035_split_001.html#id_620){.calibre5}).

**Reboot the system and validate the configuration.**

[]{#part0037.html}
