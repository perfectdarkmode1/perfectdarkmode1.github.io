## Chapter 20 {style="text-align: right"}

\

### Security Enhanced Linux {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Describe Security Enhanced Linux and its terminology

\

Understand SELinux contexts for users, processes, files, and ports

\

Copy, move, and archive files with and without SELinux context

\

How domain transitioning works

\

Overview of SELinux Booleans

\

Query and manage SELinux via management tools

\

Modify SELinux contexts for files and ports

\

Add SELinux rules to policy database

\

View and analyze SELinux alerts

\

#### RHCSA Objectives:

\

55\. Set enforcing and permissive modes for SELinux

56\. List and identify SELinux file and process context

57\. Restore default file contexts

58\. Manage SELinux port labels

59\. Use Boolean settings to modify system SELinux settings

60\. Diagnose and address routine SELinux policy violations

::: {style="page-break-before: always;"}
:::

\

Security Enhanced Linux is a mechanism that controls who can access and
do what on the system. It is part and parcel of the Linux kernel. It
handles access beyond what the traditional access control system
delivers including file and directory permissions, user and group-level
permissions, and shadow password and password aging mechanisms.

\

::: {style="text-align: center;"}
![](image-QOXVBGJ9.jpg){height="100%"}
:::

The goal of SELinux is to limit the possible damage that could occur to
the system due to unauthorized user or program access. This chapter
covers SELinux in reasonable detail.

::: {style="page-break-before: always;"}
:::

[]{#chapter0583.html}

## Security Enhanced Linux {.style3}

\

Security Enhanced Linux (SELinux) is an implementation of the Mandatory
Access Control (MAC) architecture developed by the U.S. National
Security Agency (NSA) in collaboration with other organizations and the
Linux community for flexible, enriched, and granular security controls
in Linux. MAC is integrated into the Linux kernel as a set of patches
using the Linux Security Modules (LSM) framework that allows the kernel
to support various security implementations, including SELinux.

\

MAC provides an added layer of protection above and beyond the standard
Linux Discretionary Access Control (DAC) security architecture. DAC
includes the traditional file and directory permissions, extended
attribute settings, setuid/setgid bits, su/sudo privileges, and other
controls. MAC limits the ability of a subject (Linux user or process) to
access an object (file, directory, file system, device, network
interface/connection, port, pipe, socket, etc.) to reduce or eliminate
the potential damage the subject may be able to inflict on the system if
compromised due to the exploitation of vulnerabilities in services,
programs, or applications.

\

MAC controls are fine-grained; they protect other services in the event
one service is negotiated. For instance, if the HTTP service process is
compromised, the attacker can only damage the files the hacked process
will have access to, and not the other processes running on the system,
or the objects the other processes will have access to. To ensure this
coarse-grained control, MAC uses a set of defined authorization rules
called policy to examine security attributes associated with subjects
and objects when a subject tries to access an object, and decides
whether to permit the access attempt. These attributes are stored in
contexts (a.k.a. labels), and are applied to both subjects and objects.

\

SELinux decisions are stored in a special cache area called Access
Vector Cache (AVC). This cache area is checked for each access attempt
by a process to determine whether the access attempt was previously
allowed. With this mechanism in place, SELinux does not have to check
the policy ruleset repeatedly, thus improving performance.

\

By default, SELinux controls are enabled at the time of RHEL
installation with the default configuration, which confines the
processes to the bare minimum privileges that they need to function.

::: {style="page-break-before: always;"}
:::

[]{#chapter0584.html}

## Terminology {.style3}

\

To comprehend SELinux, an understanding of some key terms is essential.
These terms are useful in explaining the concepts and SELinux
functionality in the remainder of this chapter.

\

### Subject {.style3}

A subject is any user or process that accesses an object. Examples
include system_u for the SELinux system user, and unconfined_u for
subjects that are not bound by the SELinux policy. The subject is stored
in field 1 of the context.

\

### Object {.style3}

An object is a resource, such as a file, directory, hardware device,
network interface/connection, port, pipe, or socket, that a subject
accesses. Examples include object_r for general objects, system_r for
system-owned objects, and unconfined_r for objects that are not bound by
the SELinux policy.

\

### Access {.style3}

An access is an action performed by the subject on an object. Examples
include creating, reading, or updating a file, creating or navigating a
directory, and accessing a network port or socket.

\

### Policy {.style3}

A policy is a defined ruleset that is enforced system-wide, and is used
to analyze security attributes assigned to subjects and objects. This
ruleset is referenced to decide whether to permit a subject's access
attempt to an object, or a subject's attempt to interact with another
subject. The default behavior of SELinux in the absence of a rule is to
deny the access. Two standard preconfigured policies are targeted and
mls with targeted being the default.

\

The targeted policy dictates that any process that is targeted runs in a
confined domain, and any process that is not targeted runs in an
unconfined domain. For instance, SELinux runs logged-in users in the
unconfined domain, and the httpd process in a confined domain by
default. Any subject running unconfined is more vulnerable than the one
running confined.

\

The mls policy places tight security controls at deeper levels.

\

A third preconfigured policy called minimum is a light version of the
targeted policy, and it is designed to protect only selected processes.

\

### Context {.style3}

A context (a.k.a. label) is a tag to store security attributes for
subjects and objects. In SELinux, every subject and object has a context
assigned, which consists of a SELinux user, role, type (or domain), and
sensitivity level. SELinux uses this information to make access control
decisions.

\

### Labeling {.style3}

Labeling is the mapping of files with their stored contexts.

\

### SELinux User {.style3}

SELinux policy has several predefined SELinux user identities that are
authorized for a particular set of roles. SELinux policy maintains Linux
user to SELinux user identity mapping to place SELinux user restrictions
on Linux users. This controls what roles and levels a process (with a
particular SELinux user identity) can enter. A Linux user, for instance,
cannot run the su and sudo commands or the programs located in their
home directories if they are mapped to the SELinux user user_u.

\

### Role {.style3}

A role is an attribute of the Role-Based Access Control (RBAC) security
model that is part of SELinux. It classifies who (subject) is allowed to
access what (domains or types). SELinux users are authorized for roles,
and roles are authorized for domains and types. Each subject has an
associated role to ensure that the system and user processes are
separated. A subject can transition into a new role to gain access to
other domains and types. Examples roles include user_r for ordinary
users, sysadm_r for administrators, and system_r for processes that
initiate under the system_r role. The role is stored in field 2 of the
context.

\

### Type Enforcement {.style3}

Type enforcement (TE) identifies and limits a subject's ability to
access domains for processes, and types for files. It references the
contexts of the subjects and objects for this enforcement.

\

### Type and Domain {.style3}

A type is an attribute of type enforcement. It is a group of objects
based on uniformity in their security requirements. Objects such as
files and directories with common security requirements, are grouped
within a specific type. Examples of types include user_home_dir_t for
objects located in user home directories, and usr_t for most objects
stored in the /usr directory. The type is stored in field 3 of a file
context.

\

A domain determines the type of access that a process has. Processes
with common security requirements are grouped within a specific domain
type, and they run confined within that domain. Examples of domains
include init_t for the systemd process, firewalld_t for the firewalld
process, and unconfined_t for all processes that are not bound by
SELinux policy. The domain is stored in field 3 of a process context.

\

SELinux policy rules outline how types can access each other, domains
can access types, and domains can access each other.

\

### Level {.style3}

A level is an attribute of Multi-Level Security (MLS) and Multi-Category
Security (MCS). It is a pair of sensitivity:category values that defines
the level of security in the context. A category may be defined as a
single value or a range of values, such as c0.c4 to represent c0 through
c4. In RHEL 9, the targeted policy is used as the default, which
enforces MCS (MCS supports only one sensitivity level (s0) with 0 to
1023 different categories).

::: {style="page-break-before: always;"}
:::

[]{#chapter0585.html}

## SELinux Contexts for Users {.style3}

\

SELinux contexts define security attributes placed on subjects and
objects. Each context contains a type and a security level with subject
and object information. Use the id command with the -Z option to view
the context set on Linux users. The following example shows the context
for user1:

\

<div>

![](image-YKLSKI5R.jpg){height="100%"}

</div>

The output indicates that user1 is mapped to the SELinux unconfined_u
user, and that there are no SELinux restrictions placed on this user.
You'll get the same result if you run this command for other users. This
entails that all Linux users, including root, run unconfined by default,
which gives them full access to the system.

\

In addition to the unconfined user with unlimited privileges, SELinux
includes seven confined user identities with restricted access to
objects. These accounts are mapped to Linux users via SELinux policy.
This regulated access helps safeguard the system from potential damage
that Linux users might inflict on the system.

\

You can use the seinfo query command to list the SELinux users; however,
the setools-console software package must be installed before doing so.

\

<div>

![](image-LOZZ2VMP.jpg){height="100%"}

</div>

The output shows the eight predefined SELinux users. You can use the
semanage command to view the mapping between Linux and SELinux users:

\

<div>

![](image-FTYBWHPD.jpg){height="100%"}

</div>

The output displays Linux users in column 1 (Login Name) and SELinux
users they are mapped to in column 2 (SELinux User). Columns 3 and 4
show the associated security level (MLS/MCS Range), and the context for
the Linux user (the \* represents all services). By default, all
non-root Linux users are represented as \_\_default\_\_, which is mapped
to the unconfined_u user in the policy.

::: {style="page-break-before: always;"}
:::

[]{#chapter0586.html}

## SELinux Contexts for Processes {.style3}

\

You can determine the context for processes using the ps command with
the -Z flag. The following example shows only the first two lines from
the command output:

\

<div>

![](image-3IUBCZG9.jpg){height="100%"}

</div>

In the output, the subject (system_u) is a SELinux username (mapped to
Linux user root), object is system_r, domain (init_t) reveals the type
of protection applied to the process, and level of security (s0). Any
process that is unprotected will run in the unconfined_t domain.

::: {style="page-break-before: always;"}
:::

[]{#chapter0587.html}

## SELinux Contexts for Files {.style3}

\

You can spot the context for files and directories. To this end, use the
ls command with the -Z switch. The following shows the four attributes
set on the /etc/passwd file:

\

<div>

![](image-CVWMH63C.jpg){height="100%"}

</div>

The outcome indicates the subject (system_u), object (object_r), type
(passwd_file_t), and security level (s0) for the passwd file. Contexts
for system-installed and user-created files are stored in the
file_contexts and file_contexts.local files located in the
/etc/selinux/targeted/contexts/files directory. These policy files can
be updated using the semanage command.

::: {style="page-break-before: always;"}
:::

[]{#chapter0588.html}

## Copying, Moving, and Archiving Files with SELinux Contexts {.style3}

\

As mentioned, all files in RHEL are labeled with an SELINUX security
context by default. New files inherit the parent directory's context at
the time of creation. However, three common file management
operations---copy, move, and archive---require special attention. There
are certain rules to be kept in mind during their use to ensure correct
contexts on affected files. These rules are:

\

1\. If a file is copied to a different directory, the destination file
will receive the destination directory's context, unless the
\--preserve=context switch is specified with the cp command to retain
the source file's original context.

2\. If a copy operation overwrites the destination file in the same or
different directory, the file being copied will receive the context of
the overwritten file, unless the \--preserve=context switch is specified
with the cp command to preserve the source file's original context.

3\. If a file is moved to the same or different directory, the SELinux
context will remain intact, which may differ from the destination
directory's context.

4\. If a file is archived with the tar command, use the \--selinux
option to preserve the context.

Later in the chapter, we will perform an exercise to confirm the
behavior of the three operations.

::: {style="page-break-before: always;"}
:::

[]{#chapter0589.html}

## SELinux Contexts for Ports {.style3}

\

SELinux contexts define security attributes for network ports, which can
be viewed with the semanage command . The following illustrates a few
entries from the output of this command:

\

<div>

![](image-PI56EPH1.jpg){height="100%"}

</div>

The output is displayed in three columns. Column 1 shows the SELinux
type, column 2 depicts the protocol, and column 3 indicates the port
number(s). By default, SELinux allows services to listen on a restricted
set of network ports only. This is evident from the above output.

::: {style="page-break-before: always;"}
:::

[]{#chapter0590.html}

## Domain Transitioning {.style3}

\

SELinux allows a process running in one domain to enter another domain
to execute an application that is restricted to run in that domain only,
provided a rule exists in the policy to support such transition. SELinux
defines a permission setting called entrypoint in its policy to control
processes that can transition into another domain. To understand how
this works, a basic example is provided below that shows what happens
when a Linux user attempts to change their password using the
/usr/bin/passwd command.

\

The passwd command is labeled with the passwd_exec_t type, which can be
confirmed as follows:

\

<div>

![](image-C3IGIFWM.jpg){height="100%"}

</div>

The passwd command requires access to the /etc/shadow file in order to
modify a user password. The shadow file has a different type set on it
(shadow_t):

\

<div>

![](image-MWXZ82SY.jpg){height="100%"}

</div>

The SELinux policy has rules that specifically allow processes running
in domain passwd_t to read and modify the files with type shadow_t, and
allow them entrypoint permission into domain passwd_exec_t. This rule
enables the user's shell process executing the passwd command to switch
into the passwd_t domain and update the shadow file.

\

Open two terminal windows. In window 1, issue the passwd command as
user1 and wait at the prompt:

\

<div>

![](image-X73DGFDE.jpg){height="100%"}

</div>

In window 2, run the ps command:

\

<div>

![](image-4C5U90XV.jpg){height="100%"}

</div>

As you can see, the passwd command (process) transitioned into the
passwd_t domain to change the user password. A process running in this
domain is allowed to modify the content of the /etc/shadow file.

::: {style="page-break-before: always;"}
:::

[]{#chapter0591.html}

## SELinux Booleans {.style3}

\

Booleans are on/off switches that SELinux uses to determine whether to
permit an action. Booleans activate or deactivate certain rule in the
SELinux policy immediately and without the need to recompile or reload
the policy. For instance, the ftpd_anon_write Boolean can be turned on
to enable anonymous users to upload files. This privilege can be revoked
by turning this Boolean off. Boolean values are stored in virtual files
located in the /sys/fs/selinux/booleans directory. The filenames match
the Boolean names. A sample listing of this directory is provided below:

\

<div>

![](image-V5VHRBAY.jpg){height="100%"}

</div>

On a typical server, you'll see hundreds of Boolean files in the output.

\

The manual pages of the Booleans are available through the
selinux-policy-doc package. Once installed, use the -K option with the
man command to bring the pages up for a specific Boolean. For instance,
issue man -K abrt_anon_write to view the manual pages for the
abrt_anon_write Boolean.

\

Boolean values can be viewed, and flipped temporarily or for permanence.
The new value takes effect right away. Temporary changes are stored as a
"1" or "0" in the corresponding Boolean file in the
/sys/fs/selinux/booleans directory and permanent changes are saved in
the policy database.

\

One of the exercises in the next section demonstrates how to display and
change Boolean values.

::: {style="page-break-before: always;"}
:::

[]{#chapter0592.html}

## SELinux Administration {.style3}

\

Managing SELinux involves plentiful tasks, including controlling the
activation mode, checking operational status, setting security contexts
on subjects and objects, and switching Boolean values. RHEL provides a
set of commands to perform these operations. These commands are
available through multiple packages, such as libselinux-utils provides
getenforce, getenforce, and getsebool commands, policycoreutils contains
sestatus, setsebool, and restorecon commands,
policycoreutils-python-utils provides the semanage command, and
setools-console includes the seinfo and sesearch commands.

\

For viewing alerts and debugging SELinux issues, a graphical tool called
SELinux Alert Browser is available, which is part of the
setroubleshoot-server package. In order to fully manage SELinux, you
need to ensure that all these packages are installed on the system.
Besides this toolset, there are additional utilities available to
accomplish specific SELinux administration tasks, but their use is not
as frequent.

::: {style="page-break-before: always;"}
:::

[]{#chapter0593.html}

## Management Commands {.style3}

\

SELinux delivers a variety of commands for effective administration.
Table 20-1 lists and describes the commands mentioned above plus a few
more under various management categories.

\

  ----------------------------------- --------------------------------------
  Command                             Description

  Mode Management                     

  getenforce                          Displays the current mode of operation

  grubby                              Updates and displays information about
                                      the configuration files for the grub2
                                      boot loader

  sestatus                            Shows SELinux runtime status and
                                      Boolean values

  setenforce                          Switches the operating mode between
                                      enforcing and permissive temporarily

  Context Management                  

  chcon                               Changes context on files (changes do
                                      not survive file system relabeling)

  restorecon                          Restores default contexts on files by
                                      referencing the files in the
                                      /etc/selinux/targeted/contexts/files
                                      directory

  semanage                            Changes context on files with the
                                      fcontext subcommand (changes survive
                                      file system relabeling)

  Policy Management                   

  seinfo                              Provides information on policy
                                      components

  semanage                            Manages policy database

  sesearch                            Searches rules in the policy database

  Boolean Management                  

  getsebool                           Displays Booleans and their current
                                      settings

  setsebool                           Modifies Boolean values temporarily,
                                      or in the policy database

  semanage                            Modifies Boolean values in the policy
                                      database with the boolean subcommand

  Troubleshooting                     

  sealert                             The graphical troubleshooting tool
  ----------------------------------- --------------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 20-1 SELinux Management Commands

\

Most of these commands are employed in this chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0594.html}

## Viewing and Controlling SELinux Operational State {.style3}

\

One of the key configuration files that controls the SELinux operational
state, and sets its default type is the config file located in the
/etc/selinux directory. The default content of the file is displayed
below:

\

<div>

![](image-4I2KET1R.jpg){height="100%"}

</div>

\

<div>

![](image-XUENBUT2.jpg){height="100%"}

</div>

The SELINUX directive sets the activation mode for SELinux. Enforcing
activates it and allows or denies actions based on the policy rules.
Permissive activates SELinux, but permits all actions. It records all
security violations. This mode is useful for troubleshooting and in
developing or tuning the policy. The third option is to completely turn
SELinux off. When running in enforcing mode, the SELINUXTYPE directive
dictates the type of policy to be enforced. The default is targeted.

\

Issue the getenforce command to determine the current operating mode:

\

<div>

![](image-KIAZTF77.jpg){height="100%"}

</div>

The output returns enforcing as the current active policy. You may flip
the state to permissive using the setenforce command, and verify the
change with getenforce:

\

<div>

![](image-D0QYY2M6.jpg){height="100%"}

</div>

\

You may alternatively use a "0" for permissive and a "1" for enforcing.

\

The change takes effect at once; however, it will be lost at the next
system reboot. To make it persistent, edit the /etc/selinux/config file
and set the SELINUX directive to the desired mode.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You may switch SELinux to permissive for troubleshooting a
non-functioning service. Don't forget to change it back to enforcing
when the issue is resolved.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

To disable SELinux persistently, use the grubby command as follows:

\

<div>

![](image-SDC7QAMZ.jpg){height="100%"}

</div>

The above command appends the selinux=0 setting to the end of the
"options" line in the bootloader configuration file located in the
/boot/loader/entries directory:

\

<div>

![](image-4PRM2RQ3.jpg){height="100%"}

</div>

To revert the above, simply re-run the grubby command with the
\--remove-args option as shown below:

\

<div>

![](image-W8N8UCVE.jpg){height="100%"}

</div>

::: {style="page-break-before: always;"}
:::

[]{#chapter0595.html}

## Querying Status {.style3}

\

The current runtime status of SELinux can be viewed with the sestatus
command. This command also displays the location of principal
directories, the policy in effect, and the activation mode.

\

<div>

![](image-CTNX8VDY.jpg){height="100%"}

</div>

The output reveals that SELinux is enabled (SELinux status), and it is
running in permissive mode (Current mode) with the targeted policy in
effect (Loaded policy name). It also indicates the current mode setting
in the config file (Mode from config file) along with other information.

\

The sestatus command may be invoked with the -v switch to report on
security contexts set on files and processes, as listed in the
/etc/sestatus.conf file. The default content of this file is shown
below:

\

<div>

![](image-7ET3D3TB.jpg){height="100%"}

</div>

Run the sestatus command with -v:

\

<div>

![](image-WYM1K20B.jpg){height="100%"}

</div>

With -v included, the command reports the contexts for the current
process (Current context) and the init (systemd) process (Init context)
under Process Contexts. It also reveals the file contexts for the
controlling terminal and associated files under File Contexts.

::: {style="page-break-before: always;"}
:::

[]{#chapter0596.html}

## Exercise 20-1: Modify SELinux File Context {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will create a directory sedir1 under /tmp and a
file sefile1 under sedir1. You will check the context on the directory
and file. You will change the SELinux user and type to user_u and
public_content_t on both and verify.

\

1\. Create the hierarchy sedir1/sefile1 under /tmp:

\

<div>

![](image-LG132C4M.jpg){height="100%"}

</div>

2\. Determine the context on the new directory and file:

\

<div>

![](image-BPSQSN4Z.jpg){height="100%"}

</div>

The directory and the file get unconfined_u and user_tmp_t as the
SELinux user and type.

\

3\. Modify the SELinux user (-u) on the directory to user_u and type
(-t) to public_content_t recursively (-R) with the chcon command:

\

<div>

![](image-9UPQD9QD.jpg){height="100%"}

</div>

4\. Validate the new context:

\

<div>

![](image-3996HHX3.jpg){height="100%"}

</div>

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0597.html}

## Exercise 20-2: Add and Apply File Context {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will add the current context on sedir1 to the
SELinux policy database to ensure a relabeling will not reset it to its
previous value (see Exercise 20-1). Next, you will change the context on
the directory to some random values. You will restore the default
context from the policy database back to the directory recursively.

\

1\. Determine the current context:

\

<div>

![](image-F00NNSKY.jpg){height="100%"}

</div>

The output indicates the current SELinux user (user_u) and type
(public_content_t) set on the directory and the file.

\

2\. Add (-a) the directory recursively to the policy database using the
semanage command with the fcontext subcommand:

\

<div>

![](image-EKPD36A9.jpg){height="100%"}

</div>

The regular expression (/.\*)? instructs the command to include all
files and subdirectories under /tmp/sedir1. This expression is needed
only if recursion is required.

\

The above command added the context to the
/etc/selinux/targeted/contexts/files/file_contexts.local file. You can
use the cat command to view the content.

\

3\. Validate the addition by listing (-l) the recent changes (-C) in the
policy database:

\

<div>

![](image-43FGMCZI.jpg){height="100%"}

</div>

4\. Change the current context on sedir1 to something random
(staff_u/etc_t) with the chcon command:

\

<div>

![](image-DVU7HJIB.jpg){height="100%"}

</div>

5\. The security context is changed successfully. Confirm with the ls
command:

\

<div>

![](image-EPB77XF4.jpg){height="100%"}

</div>

6\. Reinstate the context on the sedir1 directory recursively (-R) as
stored in the policy database using the restorecon command:

\

<div>

![](image-PSCUDQ9V.jpg){height="100%"}

</div>

The output confirms the restoration of the default context on the
directory and the file.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Use the combination of semanage and restorecon commands to add
a file context to the SELinux policy and then apply it. This will
prevent the context on file to reset to the original value in the event
of SELinux relabeling (disabled to enforcing/permissive).

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0598.html}

## Exercise 20-3: Add and Delete Network Ports {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will add a non-standard network port 8010 to the
SELinux policy database for the httpd service and confirm the addition.
You will then remove the port from the policy and verify the deletion.

\

1\. List (-l) the ports for the httpd service as defined in the SELinux
policy database:

\

<div>

![](image-I7IEBXV4.jpg){height="100%"}

</div>

The output reveals eight network ports the httpd process is currently
allowed to listen on.

\

2\. Add (-a) port 8010 with type (-t) http_port_t and protocol (-p) tcp
to the policy:

\

<div>

![](image-MVS328YY.jpg){height="100%"}

</div>

3\. Confirm the addition:

\

<div>

![](image-HWUVYBEO.jpg){height="100%"}

</div>

The new network port is visible in the outcome.

\

4\. Delete (-d) port 8010 from the policy and confirm:

\

<div>

![](image-XXMQB1XR.jpg){height="100%"}

</div>

The port is removed from the policy database.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: Any non-standard port you want to use for any service, make
certain to add it to the SELinux policy database with the correct type.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0599.html}

## Exercise 20-4: Copy Files with and without Context {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will create a file called sefile2 under /tmp and
display its context. You will copy this file to the /etc/default
directory, and observe the change in the context. You will remove
sefile2 from /etc/default, and copy it again to the same destination,
ensuring that the target file receives the source file's context.

\

1\. Create file sefile2 under /tmp and show context:

\

<div>

![](image-IWBMLDNS.jpg){height="100%"}

</div>

The context on the file is unconfined_u, object_r, and user_tmp_t.

\

2\. Copy this file to the /etc/default directory, and check the context
again:

\

<div>

![](image-20SSJWZQ.jpg){height="100%"}

</div>

The target file (/etc/default/sefile2) received the default context of
the destination directory (/etc/default).

\

3\. Erase the /etc/default/sefile2 file, and copy it again with the
\--preserve=context option:

\

<div>

![](image-6ALPRW7H.jpg){height="100%"}

</div>

4\. List the file to view the context:

\

<div>

![](image-IX5PBEGW.jpg){height="100%"}

</div>

The original context (user_tmp_t) is preserved on the target file after
the copy operation has finished.

::: {style="page-break-before: always;"}
:::

[]{#chapter0600.html}

## Exercise 20-5: View and Toggle SELinux Boolean Values {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will display the current state of the Boolean
nfs_export_all_rw. You will toggle its value temporarily, and reboot the
system. You will flip its value persistently after the system has been
back up.

\

1\. Display the current setting of the Boolean nfs_export_all_rw using
three different commands---getsebool, sestatus, and semanage:

\

<div>

![](image-AS5UMV6B.jpg){height="100%"}

</div>

2\. Turn off the value of nfs_export_all_rw using the setsebool command
by simply furnishing "off" or "0" with it and confirm:

\

<div>

![](image-54GJPHZL.jpg){height="100%"}

</div>

3\. Reboot the system and rerun the getsebool command to check the
Boolean state:

\

<div>

![](image-B9PUQ6A8.jpg){height="100%"}

</div>

The value reverted to its previous state.

\

4\. Set the value of the Boolean persistently (-P or -m as needed) using
either of the following:

\

<div>

![](image-NZ8B36EB.jpg){height="100%"}

</div>

5\. Validate the new value using the getsebool, sestatus, or semanage
command:

\

<div>

![](image-Y6HUFBNB.jpg){height="100%"}

</div>

The command outputs confirm the permanent change.

::: {style="page-break-before: always;"}
:::

[]{#chapter0601.html}

## Monitoring and Analyzing SELinux Violations {.style3}

\

SELinux generates alerts for system activities when it runs in enforcing
or permissive mode. It writes the alerts to the /var/log/audit/audit.log
file if the auditd daemon is running, or to the /var/log/messages file
via the rsyslog daemon in the absence of auditd. SELinux also logs the
alerts that are generated due to denial of an action, and identifies
them with a type tag AVC (Access Vector Cache) in the audit.log file. It
also writes the rejection in the messages file with a message ID, and
how to view the message details.

\

If it works with SELinux in permissive mode and not in enforcing,
something needs to be adjusted in SELinux.

\

SELinux denial messages are analyzed, and the audit data is examined to
identify the potential cause of the rejection. The results of the
analysis are recorded with recommendations on how to fix it. These
results can be reviewed to aid in troubleshooting, and recommended
actions taken to address the issue. SELinux runs a service daemon called
setroubleshootd that performs this analysis and examination in the
background. This service also has a client interface called SELinux
Troubleshooter (the sealert command) that reads the data and displays it
for assessment. The client tool has both text and graphical interfaces.
The server and client components are part of the setroubleshoot-server
software package that must be installed on the system prior to using
this service.

\

[Figure 20-1 shows how SELinux handles an incoming access request (from
a subject) to a target object.](#chapter0601.html)

\

::: {style="text-align: center;"}
![](image-I8RMYVE6.jpg){height="100%"}
:::

Figure 20-1 SELinux Allow/Deny Process

\

The following reveals a sample allowed record in raw format from the
/var/log/audit/audit.log file:

\

<div>

![](image-QUPXH72X.jpg){height="100%"}

</div>

The record indicates a successful user1 attempt to su into the root user
account on server10.

\

The following is a sample denial record from the same file in raw
format:

\

<div>

![](image-C7TMRBJO.jpg){height="100%"}

</div>

The message has the AVC type, and it is related to the passwd command
(comm) with source context (scontext)
"unconfined_u:unconfined_r:passwd_t:s0-s0:c0.c1023", and the nshadow
file (name) with file type (tclass) "file", and target context
(tcontext) "system_u:object_r:etc_t:s0". It also indicates the SELinux
operating mode, which is enforcing (permissive=0). This message
indicates that the /etc/shadow file does not have the correct context
set on it, and that's why SELinux prevented the passwd command from
updating the user's password.

\

You can also use the sealert command to analyze (-a) all AVC records in
the audit.log file. This command produces a formatted report with all
relevant details:

\

<div>

![](image-WYWDQX1V.jpg){height="100%"}

</div>

The above SELinux denial was due to the fact that I produced the
scenario by changing the SELinux type on the shadow file to something
random (etc_t). I then issued the passwd command as user1 to modify the
password. As expected, SELinux disallowed the passwd command to write
the new password to the shadow file, and it logged the password
rejection attempt to the audit log. I then restored the type on the
shadow file with restorecon /etc/shadow. I re-tried the password change
and it worked.

::: {style="page-break-before: always;"}
:::

[]{#chapter0602.html}

## Chapter Summary {.style3}

\

In this chapter, we discussed security enhanced Linux in fair detail. We
looked at the concepts, features, and terminology at length. We examined
how security contexts are associated with users, processes, files, and
ports, and viewed and modified contexts for them. We analyzed the
configuration file that controls its state and defines the policy to be
enforced. We examined how domain transitioning works. We learned several
SELinux administrative commands and performed tasks such as checking and
switching activation mode and operational status. We studied the concept
of Booleans and learned how to modify certain parts of the SELinux
policy temporarily and persistently. Finally, we reviewed the SELinux
Troubleshooter program and used it to view and analyze SELinux related
messages.

::: {style="page-break-before: always;"}
:::

[]{#chapter0603.html}

## Review Questions {.style3}

\

1\. What would the command semanage login -a -s user_u user10 do?

2\. Name the two commands that can be used to modify a Boolean value.

3\. Which option is used with the ps command to view the security
contexts for processes?

4\. What would the command restorecon -F /etc/sysconfig do?

5\. What is the name of the default SELinux policy used in RHEL 9?

6\. SELinux is an implementation of discretionary access control. True
or False?

7\. Where are SELinux denial messages logged in the absence of the
auditd daemon?

8\. Name the four parts of a process context.

9\. What would the command sestatus -b \| grep nfs_export_all_rw do?

10\. Name the directory that stores SELinux Boolean files.

11\. What are the two commands to display and modify the SELinux mode?

12\. Name the two SELinux subjects.

13\. What one task must be done to change the SELinux mode from
enforcing to disabled?

14\. Which option with the cp command must be specified to preserve
SELinux contexts?

15\. What is the purpose of the command sestatus?

16\. What is the name and location of the SELinux configuration file?

17\. What would the command semanage fcontext -Cl do?

18\. Which command can be used to ensure modified contexts will survive
file system relabeling?

19\. With SELinux running in enforcing mode and one of the services on
the system is compromised, all other services will be affected. True or
False?

20\. Name the command that starts the SELinux Troubleshooter program.

::: {style="page-break-before: always;"}
:::

[]{#chapter0604.html}

## Answers to Review Questions {.style3}

\

1\. This command provided will map Linux user user10 with SELinux user
user_u.

2\. The semanage and setsebool commands.

3\. The -Z option.

4\. The command provided will restore the default SELinux contexts on
the specified directory.

5\. The default SELinux policy used in RHEL 9 is targeted.

6\. False. SELinux is an implementation of mandatory access control.

7\. The SELinux denial messages are logged to the /var/log/messages
file.

8\. The four parts of a process context are user, role, type/domain, and
sensitivity level.

9\. The command provided will display the current value of the specified
Boolean.

10\. The /sys/fs/selinux/booleans directory.

11\. The getenforce and setenforce commands.

12\. User and process are two SELinux subjects.

13\. The system must be rebooted.

14\. The \--preserve=context option.

15\. The sestatus command displays SELinux status information.

16\. The SELinux configuration filename is config and it is located in
the /etc/selinux directory.

17\. The command provided will show recent changes made to the SELinux
policy database.

18\. The semanage command.

19\. False.

20\. The command name is sealert.

::: {style="page-break-before: always;"}
:::

[]{#chapter0605.html}

## Do-It-Yourself Challenge Labs

\

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the labs have already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

\

Use the lab environment built specifically for end-of-chapter labs. See
sub-section "Lab Environment for End-of-Chapter Labs" in Chapter 01
"Local Installation" for details.

::: {style="page-break-before: always;"}
:::

[]{#chapter0606.html}

## Lab 20-1: Disable and Enable the SELinux Operating Mode {.style3}

\

As user1 with sudo on server30, check and make a note of the current
SELinux operating mode. Modify the configuration file and set the mode
to disabled. Reboot the system to apply the change. Run sudo getenforce
to confirm the change when the system is up. Restore the directive's
value to enforcing in the configuration file, and reboot to apply the
new mode. Run sudo getenforce to confirm the mode when the system is up.
(Hint: SELinux Administration).

::: {style="page-break-before: always;"}
:::

[]{#chapter0607.html}

## Lab 20-2: Modify Context on Files {.style3}

\

As user1 with sudo on server30, create directory hierarchy /tmp/d1/d2.
Check the contexts on /tmp/d1 and /tmp/d1/d2. Change the SELinux type on
/tmp/d1 to etc_t recursively with the chcon command and confirm. Add
/tmp/d1 to the policy database with the semanage command to ensure the
new context is persistent on the directory hierarchy. (Hint: SELinux
Administration).

::: {style="page-break-before: always;"}
:::

[]{#chapter0608.html}

Lab 20-3: Add Network Port to Policy Database

\

As user1 with sudo on server30, add network port 9005 to the SELinux
policy database for the secure HTTP service using the semanage command.
Verify the addition. (Hint: SELinux Administration).

::: {style="page-break-before: always;"}
:::

[]{#chapter0609.html}

## Lab 20-4: Copy Files with and without Context {.style3}

\

As user1 with sudo on server30, create file sef1 under /tmp. Copy the
file to the /usr/local directory. Check and compare the contexts on both
source and destination files. Create another file sef2 under /tmp and
copy it to the /var/local directory using the \--preserve=context option
with the cp command. Check and compare the contexts on both source and
destination files. (Hint: SELinux Administration).

::: {style="page-break-before: always;"}
:::

[]{#chapter0610.html}

## Lab 20-5: Flip SELinux Booleans {.style3}

\

As user1 with sudo on server30, check the current value of Boolean
ssh_use_tcpd using the getsebool and sestatus commands. Use the
setsebool command and toggle the value of the directive. Confirm the new
value with the getsebool, semanage, or sestatus command. (Hint: SELinux
Administration).

::: {style="page-break-before: always;"}
:::

[]{#chapter0611.html}
