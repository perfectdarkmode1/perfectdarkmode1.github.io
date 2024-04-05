# Appendix D: Sample RHCSA Exam 4**

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

**[Setup for Sample Exam 4:]{.underline1}**

Build two virtual machines with RHEL 8 Server with GUI (Exercises 1-1
and 1-2). Use a 10GB disk for the OS with default partitioning. Add
1x4GB disk to VM2 and a network interface to both virtual machines. Do
not configure the network interfaces or create a normal user account
during installation.

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
[rhcsa5.example.com](http://rhcsa5.example.com){.calibre2} and alias
rhcsa5 using the hostnamectl command. Make sure that the new hostname is
reflected in the command prompt. ([Exercises
16-1](#part0028_split_001.html#id_437){.calibre2} and
[16-5](#part0028_split_001.html#id_458){.calibre2}).

**Task 02:** On rhcsa5, configure a network connection on the primary
network device with IP address 192.168.0.245/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using the nmcli command. Use different IP
assignments based on your lab environment. ([Exercise
16-4](#part0028_split_001.html#id_455){.calibre5}).

**[]{#part0039.html#page_548 .calibre5}Task 03:** On VM2, set the system
hostname to [rhcsa6.example.com](http://rhcsa6.example.com){.calibre5}
and alias rhcsa6 using a manual method (modify file by hand). Make sure
that the new hostname is reflected in the command prompt. ([Exercises
16-1](#part0028_split_001.html#id_437){.calibre5} and
[16-5](#part0028_split_001.html#id_458){.calibre5}).

**Task 04:** On rhcsa6, configure a network connection on the primary
network device with IP address 192.168.0.246/24, gateway 192.168.0.1,
and nameserver 192.168.0.1 using a manual method (create/modify files by
hand). Use different IP assignments based on your lab environment.
([Exercise 16-3](#part0028_split_001.html#id_452){.calibre5}).

**Task 05:** Run "ping -c2 rhcsa6" on rhcsa5. Run "ping -c2 rhcsa5" on
rhcsa6. You should see 0% loss in both outputs. ([Exercise
16-5](#part0028_split_001.html#id_458){.calibre5}).

**Task 06:** On rhcsa5 and rhcsa6, attach the RHEL 8 ISO image to the VM
and mount it persistently to *mnt*sr0. Define access to both
repositories and confirm. ([Exercise
10-1](#part0022_split_001.html#id_280){.calibre5}).

**Task 07:** Export *share5 on rhcsa5 and mount it to* share6
persistently on rhcsa6. ([Exercises
17-1](#part0029_split_001.html#id_469){.calibre5} and
[17-2](#part0029_split_001.html#id_470){.calibre5}).

**Task 08:** Use NFS to export home directories for all users (u1, u2,
and u3) on rhcsa6 so that their home directories become available under
/home1 when they log on to rhcsa5. Create u1, u2, and u3. ([Exercises
17-1](#part0029_split_001.html#id_469){.calibre5} and
[17-5](#part0029_split_001.html#id_479){.calibre5}).

**Task 09:** On rhcsa5, add HTTP port 8400/udp to the public zone
persistently. ([Exercise
21-3](#part0033_split_000.html#page_474){.calibre5}).

**Task 10:** Configure password-less ssh access for u1 from rhcsa5 to
rhcsa6. Copy the directory *etc*sysconfig from rhcsa5 to rhcsa6 under
*var*tmp/remote securely. ([Exercise
19-2](#part0031_split_001.html#id_513){.calibre5}, and [Chapter
19](#part0031_split_000.html#page_433){.calibre5}, topic: Copying Files
Remotely Using scp).

**Task 11:** On rhcsa6, create VDO volume vdo2 on the 4GB disk with
logical size 16GB and mounted persistently with XFS structures on
*mnt*vdo2. ([Exercises 13-6](#part0025_split_001.html#id_370){.calibre5}
and [13-7](#part0025_split_000.html#page_316){.calibre5}).

**Task 12:** On rhcsa6, install module "container-tools" stream rhel8.
([Exercise 10-5](#part0022_split_001.html#id_297){.calibre5}).

**Task 13:** On rhcsa6, flip the value of the Boolean nfs_export_all_rw
persistently. ([Exercise
21-5](#part0033_split_001.html#id_555){.calibre5}).

**Task 14:** On rhcsa5 and rhcsa6, set the tuning profile to powersave.
([Exercise 12-2](#part0024_split_001.html#id_348){.calibre5}).

**Task 15:** On rhcsa5, create file lnfile1 under *var*tmp and create
three hard links called hard1, hard2, and hard3 for it. Identify the
inode number associated with all four files. Edit any of the files and
observe the metadata for all the files for confirmation. ([Exercise
3-2](#part0015_split_001.html#id_106){.calibre5}).

**Task 16:** On rhcsa5, members (user100 and user200) of group100 should
be able to collaborate on files under /shared but cannot delete each
other's files. ([Exercises
4-5](#part0016_split_001.html#id_130){.calibre5} and
[4-6](#part0016_split_001.html#id_132){.calibre5}).

**Task 17:** Synchronize the entire /etc directory on rhcsa5 to
*var*tmp/etc on rhcsa6. Use in-transit compression. Capture the output
and any errors in the *var*tmp/etc.transfer file on rhcsa5 during the
synchronization process. ([Chapter
19](#part0031_split_000.html#page_433){.calibre5}, topic: Synchronizing
Files Remotely Using rsync, and [Chapter
07](#part0019_split_000.html#page_151){.calibre5}, topic: Regular
Expressions).

**Task 18:** On rhcsa6, list all files that are part of the "setup"
package, and use regular expressions and I/O redirection to send the
output lines containing "hosts" to *var*tmp/setup.pkg. ([Exercise
9-2](#part0021_split_001.html#id_263){.calibre5}, and [Chapter
07](#part0019_split_000.html#page_151){.calibre5}, topics: Regular
Expressions, and Input, Output, and Error Redirections).

**Task 19:** On rhcsa5, check the current version of the Linux kernel.
Register rhcsa5 with RHSM and install the latest version of the kernel
available. Ensure that the existing kernel and its configuration remain
intact. Reboot the system and confirm the new version is loaded.
([Exercise 11-3](#part0023_split_001.html#id_322){.calibre5}, and
[Chapter 02](#part0014_split_000.html#page_35){.calibre5}, topic:
Viewing System Information).

**[]{#part0039.html#page_549 .calibre5}Task 20:** On rhcsa5, configure
journald to store messages permanently under *var*log/journal and fall
back to memory-only option if *var*log/journal directory does not exist
or has permission/access issues. ([Exercise
12-1](#part0024_split_000.html#page_294){.calibre5}).

**Task 21:** Write a bash shell script that defines an environment
variable called ENV1=book1 and creates a user account that matches the
value of the variable. ([Chapter
22](#part0034_split_000.html#page_481){.calibre5}: Script02 and
Script03).

**Task 22:** On rhcsa5, launch a named root container with host port 443
mapped to container port 443. Employ the latest version of the ubi7
image. Configure a systemd service to auto-start the container at system
reboots. Validate port mapping using an appropriate podman subcommand.
([Exercises 23-5](#part0035_split_000.html#page_518){.calibre5} and
[23-9](#part0035_split_001.html#id_619){.calibre5}).

**Task 23:** On rhcsa5, launch a named container as user100 with *data01
mapped to* data01 and two variables KERN=\$(uname -r) and SHELL defined.
Use the latest version of the ubi8 image. Configure a systemd service to
auto-start the container at system reboots without the need for user100
to log in. Create a file under the shared mount point and validate data
persistence. Verify port mapping using an appropriate podman subcommand.
([Exercises 23-7](#part0035_split_001.html#id_615){.calibre5},
[23-8](#part0035_split_001.html#id_617){.calibre5}, and
[23-10](#part0035_split_001.html#id_620){.calibre5}).

**Reboot the system and validate the configuration.**

