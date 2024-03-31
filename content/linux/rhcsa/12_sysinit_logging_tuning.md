## Chapter 12 {#part0024_split_000.html#calibre_pb_0 .calibre11}

**System Initialization, Message Logging, and System Tuning**

This chapter describes the following major topics:

- Understand systemd, units, and targets
- Analyze service and target unit configuration files
- List and view status of running units
- Manage service units and target units 
- Display and configure default system boot target
- Switch into non-default targets
- Analyze system log configuration file
- Examine log file rotation settings
- Review boot and system log files
- Record custom messages in system log file
- Describe systemd journal service
- Retrieve and scrutinize messages from journal
- Store journal information persistently
- Know system tuning and apply tuning profile

RHCSA Objectives:

Boot, reboot, and shut down a system normally
Boot systems into different targets manually
Start, stop, and check the status of network services
Start and stop services and configure services to start automatically at boot
Configure systems to boot into a specific target automatically
Configure network services to start automatically at boot
Manage tuning profiles
Locate and interpret system log files and journals
Preserve system journals


Systemd is the 
- default system initialization and service management scheme.
- boots the system into one of several predefined targets 
- used to handle operational states of services. 
- employs the concepts of units and targets for initialization, service administration, and state changes. 

Log files need to be rotated periodically to prevent the file system
space from filling up. 
configuration files that define the default and custom locations to direct the log messages to and to
configure rotation settings. The 
system log file
- records custom messages sent to it. systemd includes a service for viewing and managing system
logs in addition to the traditional logging service. This service
maintains a log of runtime activities for faster retrieval and can be
configured to store the information permanently.

System tuning service is employed to monitor connected devices and to
tweak their parameters to improve performance or conserve power. A
recommended tuning profile may be identified and activated for optimal
performance and power saving.

**[System]{#part0024_split_001.html#id_329 .calibre10} Initialization
and Service Management**

*systemd* (short for *system daemon*) is the system initialization and
service management mechanism. It has fast-tracked system initialization
and state transitioning by introducing features such as parallel
processing of startup scripts, improved handling of service
dependencies, and on-demand activation of services. Moreover, it
supports snapshotting of system states, tracks processes using control
groups, and automatically maintains mount points. systemd is the first
process with PID 1 that spawns at boot and it is the last process that
terminates at shutdown.

![](images/00002.jpeg){.image} systemd spawns several processes during a
service startup. It places the processes in a private hierarchy composed
of *control groups* (or *cgroups* for short) to organize processes for
the purposes of monitoring and controlling system resources such as
processor, memory, network bandwidth, and disk I/O. This includes
limiting, isolating, and prioritizing their usage of resources. This way
resources can be distributed among users, databases, and applications
based on need and priority, resulting in overall improved system
performance.

In order to benefit from parallelism, systemd initiates distinct
services concurrently, taking advantage of multiple CPU cores and other
compute resources. To that end, systemd creates sockets for all enabled
services that support socket-based activation instantaneously at the
very beginning of the initialization process. It passes them on to
service daemon processes as they attempt to start in parallel. This
approach lets systemd handle inter-service order dependencies and allows
services to start without any delays. With systemd, dependent daemons
need not be running; they only need the correct socket to be available.
systemd creates sockets first, starts daemons next, and caches any
client requests to daemons that have not yet started in the socket
buffer. It fills the pending client requests when the daemons they were
awaiting come online.

![](images/00002.jpeg){.image} Socket is a communication method that
allows a single process to talk to another process on the same or remote
system.

During the operational state, systemd maintains the sockets and uses
them to reconnect other daemons and services that were interacting with
an old instance of a daemon before that daemon was terminated or
restarted. Likewise, services that use activation based on D-Bus
(*Desktop Bus*) are started when a client application attempts to
communicate with them for the first time. Additional methods used by
systemd for activation are device-based and path-based, with the former
starting the service when a specific hardware type such as USB is
plugged in, and the latter starting the service when a particular file
or directory alters its state.

![](images/00002.jpeg){.image} D-Bus is another communication method
that allows multiple services running in parallel on a system to talk to
one another on the same or remote system.

With on-demand activation, systemd defers the startup of
services---Bluetooth and printing---until they are actually needed
during the boot process or during runtime. Together, parallelization and
on-demand activation save time and compute resources, and contribute to
expediting the boot process considerably.

Another major benefit of parallelism witnessed at system boot is when
systemd uses the autofs service to temporarily mount the configured file
systems. During the boot process, the file systems are checked that may
result in unnecessary delays. With autofs, the file systems are
temporarily mounted on their normal mount points, and as soon as the
checks on the file systems are finished, systemd remounts them using
their standard devices. Parallelism in file system mounts does not
affect the root and virtual file systems.

**[Units]{#part0024_split_001.html#id_330 .calibre10}**

*Units* are systemd objects used for organizing boot and maintenance
tasks, such as hardware initialization, socket creation, file system
mounts, and service startups. Unit configuration is stored in their
respective configuration files, which are auto-generated from other
configurations, created dynamically from the system state, produced at
runtime, or user-developed. Units are in one of several operational
states, including active, inactive, in the process of being activated or
deactivated, and failed. Units can be enabled or disabled. An enabled
unit can be started to an active state; a disabled unit cannot be
started.

Units have a name and a type, and they are encoded in files with names
in the form unitname.type. Some examples are tmp.mount, sshd.service,
syslog.socket, and umount.target. There are two types of unit
configuration files: (1) system unit files that are distributed with
installed packages and located in the **usr*lib/systemd/system*
directory, and (2) user unit files that are user-defined and stored in
the **etc*systemd/user* directory (run **ls -l** on both directories to
list their contents). This information can be vetted with the
*pkg-config* command:

![](images/00587.jpeg) 

Furthermore, there are additional system units that are created at
runtime and destroyed when they are no longer needed. They are located
in the **run*systemd/system* directory. These runtime unit files take
precedence over the system unit files, and the user unit files take
priority over the runtime files.

![](images/00002.jpeg){.image} Unit configuration files are a direct
replacement of the initialization scripts found in the
**etc*rc.d/init.d* directory in older RHEL releases.

systemd includes 11 unit types, which are described in [Table
12-1](#part0024_split_001.html#id_734){.calibre5}.

::: c49
  --------------- ------------------------------------------------------------------------------------------------------------
  **Unit Type**   **Description**
  Automount       Offers automount capabilities for on-demand mounting of file systems
  Device          Exposes kernel devices in systemd and may be used to implement device-based activation
  Mount           Controls when and how to mount or unmount file systems
  Path            Activates a service when monitored files or directories are accessed
  Scope           Manages foreign processes instead of starting them
  Service         Starts, stops, restarts, or reloads service daemons and the processes they are made up of
  Slice           May be used to group units, which manage system processes in a tree-like structure for resource management
  Socket          Encapsulates local inter-process communication or network sockets for use by matching service units
  Swap            Encapsulates swap partitions
  Target          Defines logical grouping of units
  Timer           Useful for triggering activation of other units based on timers
  --------------- ------------------------------------------------------------------------------------------------------------

**[Table]{#part0024_split_001.html#id_734} 12-1 systemd Unit Types**
:::

Unit files contain common and specific configuration elements. Common
elements fall under the \[Unit\] and \[Install\] sections, and comprise
the description, documentation location, dependency information,
conflict information, and other options that are independent of the type
of unit. The unit-specific configuration data is located under the unit
type section: \[Service\] for the service unit type, \[Socket\] for the
socket unit type, and so forth. A sample unit file for *sshd.service* is
shown below from the **usr*lib/systemd/system* directory:

![](images/00588.jpeg) 

Units can have dependency relationships among themselves based on a
sequence (ordering) or a requirement. A sequence outlines one or more
actions that need to be taken before or after the activation of a unit
(the Before and After directives). A requirement specifies what must
already be running (the Requires directive) or not running (the
Conflicts directive) in order for the successful launch of a unit. For
instance, the *graphical.target* unit file tells us that the system must
already be operating in the multi-user mode and not in rescue mode in
order for it to boot successfully into the graphical mode. Another
option, Wants, may be used instead of Requires in the \[Unit\] or
\[Install\] section so that the unit is not forced to fail activation if
a required unit fails to start. Run **man systemd.unit** for details on
systemd unit files.

There are a few other types of dependencies that you may see in other
unit configuration files. systemd generally sets and maintains
inter-service dependencies automatically; however, this can be done
manually if needed.

**[Targets]{#part0024_split_001.html#id_331 .calibre10}**

*Targets* are simply logical collections of units. They are a special
systemd unit type with the .target file extension. They share the
directory locations with other unit configuration files. Targets are
used to execute a series of units. This is typically true for booting
the system to a desired operational run level with all the required
services up and running. Some targets inherit services from other
targets and add their own to them. systemd includes several predefined
targets that are described in [Table
12-2](#part0024_split_001.html#id_735){.calibre5}.

::: c49
  ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Target**   **Description**
  halt         Shuts down and halts the system
  poweroff     Shuts down and powers off the system
  shutdown     Shuts down the system
  rescue       Single-user target for running administrative and recovery functions. All local file systems are mounted. Some essential services are started, but networking remains disabled.
  emergency    Runs an emergency shell. The root file system is mounted in read-only mode; other file systems are not mounted. Networking and other services remain disabled.
  multi-user   Multi-user target with full network support, but without GUI
  graphical    Multi-user target with full network support and GUI
  reboot       Shuts down and reboots the system
  default      A special soft link that points to the default system boot target (multi-user.target or graphical.target)
  hibernate    Puts the system into hibernation by saving the running state of the system on the hard disk and powering it off. When powered up, the system restores from its saved state rather than booting up.
  ------------ ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0024_split_001.html#id_735} 12-2 systemd Targets**
:::

Target unit files contain all information under the \[Unit\] section,
and it comprises the description, documentation location, and dependency
and conflict information. A sample file for the *graphical.target*
target is shown below from the **usr*lib/systemd/system* directory:

![](images/00589.jpeg) 

The file shows four dependencies: Requires, Wants, Conflicts, and After.
It suggests that the system must have already accomplished the
rescue.service, rescue.target, multi-user.target, and
display-manager.service levels in order to be declared running in the
graphical target. Run **man systemd.target** for details on systemd
targets.

**[The]{#part0024_split_001.html#id_332 .calibre10} systemctl Command**

systemd comes with a set of management tools for querying and
controlling operations. The primary tool for interaction in this command
suite is *systemctl*. The *systemctl* command performs administrative
functions and supports plentiful subcommands and flags. [Table
12-3](#part0024_split_001.html#id_736){.calibre5} lists and describes
some common operations.

::: c49
  ----------------------------- -------------------------------------------------------------------------------------------------------------------
  **Subcommand**                **Description**
  daemon-reload                 Re-reads and reloads all unit configuration files and recreates the entire user dependency tree.
  enable (disable)              Activates (deactivates) a unit for autostart at system boot
  get-default (set-default)     Shows (sets) the default boot target
  get-property (set-property)   Returns (sets) the value of a property
  is-active                     Checks whether a unit is running
  is-enabled                    Displays whether a unit is set to autostart at system boot
  is-failed                     Checks whether a unit is in the failed state
  isolate                       Changes the running state of a system
  kill                          Terminates all processes for a unit
  list-dependencies             Lists dependency tree for a unit
  list-sockets                  Lists units of type socket
  list-unit-files               Lists installed unit files
  list-units                    Lists known units. This is the default behavior when systemctl is executed without any arguments.
  mask (unmask)                 Prohibits (permits) auto and manual activation of a unit to avoid potential conflict
  reload                        Forces a running unit to re-read its configuration file. This action does not change the PID of the running unit.
  restart                       Stops a running unit and restarts it
  show                          Shows unit properties
  start (stop)                  Starts (stops) a unit
  status                        Presents the unit status information
  ----------------------------- -------------------------------------------------------------------------------------------------------------------

**[Table]{#part0024_split_001.html#id_736} 12-3 systemctl Subcommands**
:::

You will use a majority of these subcommands with *systemctl* going
forward. Refer to the manual pages of the command for more details.

**[Listing]{#part0024_split_001.html#id_333 .calibre10} and Viewing
Units**

The *systemctl* command is used to view and manage all types of units.
The following examples demonstrate common operations pertaining to
viewing and querying units.

To list all units that are currently loaded in memory along with their
status and description, run the *systemctl* command without any options
or subcommands. A long output is generated. The graphic below shows a
few starting and concluding lines followed by a brief explanation.

![](images/00590.jpeg) 

Here is a breakdown of the graphic above: the UNIT column shows the name
of the unit and its location in the tree, the LOAD column reflects
whether the unit configuration file was properly loaded (other
possibilities are not found, bad setting, error, and masked), the ACTIVE
column returns the high-level activation state (other possible states
are active, reloading, inactive, failed, activating, and deactivating),
the SUB column depicts the low-level unit activation state (reports
unit-specific information), and the DESCRIPTION column illustrates the
unit's content and functionality.

By default, the *systemctl* command lists only the active units. You can
use the \--all option to include the inactive units too.

To list all (\--all) active and inactive units of type (-t) socket:

![](images/00591.jpeg) 

To list all units of type socket (column 2) currently loaded in memory
and the service they activate (column 3), sorted by the listening
address (column 1):

![](images/00592.jpeg) 

To list all unit files (column 1) installed on the system and their
current state (column 2). This will generate a long list of units in the
output. The following only shows a selection.

![](images/00593.jpeg) 

To list all units that failed (\--failed) to start at the last system
boot:

![](images/00594.jpeg) 

To list the hierarchy of all dependencies (required and wanted units)
for the current default target:

![](images/00595.jpeg) 

To list the hierarchy of all dependencies (required and wanted units)
for a specific unit such as *atd.service*:

![](images/00596.jpeg) 

There are other listing subcommands and additional flags available that
can be used to produce a variety of reports.

**[Managing]{#part0024_split_001.html#id_334 .calibre10} Service Units**

The *systemctl* command offers several subcommands to manage service
units, including starting, stopping, restarting, and checking their
status. These and other management operations are summarized in [Table
12-3](#part0024_split_001.html#id_736){.calibre5}. The following
examples demonstrate their use on a service unit called *atd*.

To check the current operational status and other details for the *atd*
service:

![](images/00597.jpeg) 

The above output reveals a lot of information about the *atd* service.
On line 1, it shows the service description (read from the
**usr*lib/systemd/system/atd.service* file). Line 2 illustrates the load
status, which reveals the current load status of the unit configuration
file in memory. Other possibilities for "Loaded" include "error" (if
there was a problem loading the file), \"not-found\" (if no file
associated with this unit was found), \"bad-setting\" (if a key setting
was missing), and \"masked\" (if the unit configuration file is masked).
Line 2 also tells us whether the service is set (enable or disable) for
autostart at system boot.

Line 3 exhibits the current activation status and the time the service
was started. An activation status designates the current state of the
service. Possible states include:

**Active (running)**: The service is running with one or more processes

**Active (exited):** Completed a one-time configuration

**Active (waiting)**: Running but waiting for an event

**Inactive:** Not running

**Activating:** In the process of being activated

**Deactivating**: In the process of being deactivated

**Failed:** If the service crashed or could not be started

The output also depicts the PID of the service process and other
information.

To disable the *atd* service from autostarting at the next system
reboot:

![](images/00598.jpeg) 

To re-enable *atd* to autostart at the next system reboot:

![](images/00599.jpeg) 

To check whether *atd* is set to autostart at the next system reboot:

![](images/00600.jpeg) 

To check whether the *atd* service is running:

![](images/00601.jpeg) 

To stop and restart *atd*, run either of the following:

![](images/00602.jpeg) 

To show the details of the *atd* service:

![](images/00603.jpeg) 

To prohibit *atd* from being enabled or disabled:

![](images/00604.jpeg) 

Try disabling or enabling *atd* and observe the effect of the previous
command:

![](images/00605.jpeg) 

Reverse the effect of the *mask* subcommand and try disable and enable
operations:

![](images/00606.jpeg) 

Notice that the *unmask* subcommand has removed the restriction that was
placed on the *atd* service.

**[Managing]{#part0024_split_001.html#id_335 .calibre10} Target Units**

The *systemctl* command is also used to manage the target units. It can
be used to view or change the default boot target, switch from one
running target into another, and so on. These operations are briefed in
[Table 12-3](#part0024_split_001.html#id_736){.calibre5}. Let's look at
some examples.

To view what units of type (-t) target are currently loaded and active:

![](images/00607.jpeg) 

For each target unit, the above output returns the target unit's name,
load state, high-level and low-level activation states, and a short
description. Add the \--all option to the above to see all loaded
targets in either active or inactive state.

**Viewing and Setting Default Boot Target**

The *systemctl* command is used to view the current default boot target
and to set it. Let's use the *get-default* and *set-default* subcommands
with *systemctl* to perform these operations.

To check the current default boot target:

![](images/00608.jpeg) 

[**EXAM TIP:**]{.c56} You may have to modify the default boot target
persistently.

To change the current default boot target from graphical.target to
multi-user.target:

![](images/00609.jpeg) 

The command simply removes the existing symlink (*default.target*)
pointing to the old boot target and replaces it with the new target file
path.

Execute **sudo systemctl set-default graphical** to revert the default
boot target to graphical.

**Switching into Specific Targets**

The *systemctl* command can be used to transition the running system
from one target state into another. There are a variety of potential
targets available to switch into as listed in [Table
12-2](#part0024_split_001.html#id_735){.calibre5}; however, only a few
of them---graphical, multi-user, reboot, shutdown---are typically used.
The rescue and emergency targets are for troubleshooting and system
recovery purposes, poweroff and halt are similar to shutdown, and
hibernate is suitable for mobile devices. Consider the following
examples that demonstrate switching targets.

The current default target on *server1* is graphical. To switch into
multi-user, use the *isolate* subcommand with *systemctl*:

![](images/00610.jpeg) 

This should stop the graphical service on the system and display the
text-based console login screen, as shown below:

![](images/00611.jpeg) 

Type in a username such as *user1* and enter the password to log in:

![](images/00612.jpeg) 

To return to the graphical target:

![](images/00613.jpeg) 

The graphical login screen should appear shortly and you should be able
to log back in.

To shut down the system and power it off, use the following or simply
run the *poweroff* command:

![](images/00614.jpeg) 

To shut down and reboot the system, use the following or simply run the
*reboot* command:

![](images/00615.jpeg) 

The *halt*, *poweroff*, and *reboot* commands are mere symbolic links to
the *systemctl* command, as the following long listing suggests:

![](images/00616.jpeg) 

The *halt*, *poweroff*, and *reboot* commands are available in RHEL 8
for compatibility reasons only. It is recommended to use the *systemctl*
command instead when switching system states.

The three commands, without any arguments, perform the same action that
the *shutdown* command would with the "-H now", "-P now", and "-r now"
arguments, respectively. In addition, it also broadcasts a warning
message to all logged-in users, blocks new user login attempts, waits
for the specified amount of time for users to save their work and log
off, stops the services, and eventually shut the system down to the
specified target state.

**[System]{#part0024_split_001.html#id_336 .calibre10} Logging**

*System logging* (*syslog* for short) is one of the most rudimentary
elements of an operating system. Its purpose is to capture messages
generated by the kernel, daemons, commands, user activities,
applications, and other events, and forwarded them to various log files,
which store them for security auditing, service malfunctioning, system
troubleshooting, or informational purposes.

The daemon that is responsible for system logging is called *rsyslogd*
(*rocket-fast system for log processing*). This service daemon is
multi-threaded, with support for enhanced filtering,
encryption-protected message relaying, and a variety of configuration
options. The *rsyslogd* daemon reads its configuration file
**etc*rsyslog.conf* and the configuration files located in the
**etc*rsyslog.d* directory at startup. The default depository for most
system log files is the **var*log* directory. Other services such as
audit, Apache, and GNOME desktop manager have subdirectories under
**var*log* for storing their respective log files.

The *rsyslog* service is modular, allowing the modules listed in its
configuration file to be dynamically loaded in the kernel as and when
needed. Each module brings a new functionality to the system upon
loading.

The *rsyslogd* daemon can be stopped manually using **systemctl stop
rsyslog**. Replace stop with start, restart, reload, and status as
appropriate.

A PID is assigned to the daemon at startup and a file by the name
*rsyslogd.pid* is created in the */run* directory to save the PID. The
reason this file is created and stores the PID is to prevent the
initiation of multiple instances of this daemon.

**[The]{#part0024_split_001.html#id_337 .calibre10} Syslog Configuration
File**

The *rsyslog.conf* is the primary syslog configuration file located in
the */etc* directory . The default uncommented line entries from the
file are shown below and explained thereafter. Section headings have
been added to separate the directives in each section.

![](images/00617.jpeg) 

As depicted, the syslog configuration file contains three sections:
Modules, Global Directives, and Rules. The Modules section defines two
modules---*imuxsock* and *imjournal*---and they are loaded on demand.
The *imuxsock* module furnishes support for local system logging via the
*logger* command, and the *imjournal* module allows access to the
systemd journal.

The Global Directives section contains three active directives. The
definitions in this section influence the overall functionality of the
*rsyslog* service. The first directive sets the location for the storage
of auxiliary files (**var*lib/rsyslog*). The second directive instructs
the *rsyslog* service to save captured messages using traditional file
formatting. The third directive directs the service to load additional
configuration from files located in the **etc*rsyslogd.d/* directory.

The Rules section has many two-field line entries. The left field is
called *selector*, and the right field is referred to as *action*. The
selector field is further divided into two period-separated sub-fields
called *facility* (left) and *priority* (right), with the former
representing one or more system process categories that generate
messages, and the latter identifying the severity associated with the
messages. The semicolon (;) character is used as a distinction mark if
multiple facility.priority groups are present. The action field
determines the destination to send the messages to.

There are numerous supported facilities such as auth, authpriv, cron,
daemon, kern, lpr, mail, news, syslog, user, uucp, and local0 through
local7. The asterisk (\*) character represents all of them.

Similarly, there are several supported priorities, and they include
emerg, alert, crit, error, warning, notice, info, debug, and none. This
sequence is in the descending criticality order. The asterisk (\*)
represents all of them. If a lower priority is selected, the daemon logs
all messages of the service at that and higher levels.

Line 1 under the Rules section instructs the syslog daemon to catch and
store informational messages from all services to the
**var*log/messages* file and ignore all messages generated by mail,
authentication, and cron services. Lines 2, 3, and 4 command the daemon
to collect and log all messages produced by authentication, mail, and
cron to the *secure*, *maillog*, and *cron* files, respectively. Line 5
orders the daemon to display emergency messages (omusrmsg stands for
*user message output module*) on the terminals of all logged-in users.
Line 6 shows two comma-separated facilities that are set at a common
priority. These facilities tell the daemon to gather critical messages
from uucp and news facilities and log them to the **var*log/spooler*
file. Line 7 (the last line) is for recording the boot-time service
startup status to the **var*log/boot.log* file.

If you have made any modifications to the syslog configuration file, you
need to run the *rsyslogd* command with the -N switch and specify a
numeric verbosity level to inspect the file for any syntax or typing
issues:

![](images/00618.jpeg) 

The validation returns the version of the command, verbosity level used,
and the configuration file path. With no issues reported, the *rsyslog*
service can be restarted (or reloaded) in order for the changes to take
effect.

**[Rotating]{#part0024_split_001.html#id_338 .calibre10} Log Files**

RHEL records all system activities in log files that are stored in a
central location under the **var*log* directory, as defined in the
rsyslog configuration file. A long listing of this directory reveals the
files along with subdirectories that may have multiple service-specific
logs. Here is a listing from *server1*:

![](images/00619.jpeg) 

The output shows log files for various services. Depending on the usage
and the number of events generated and captured, log files may quickly
fill up the */var* file system, resulting in unpredictable system
behavior. Also, they may grow to an extent that would make it difficult
to load, read, send, or analyze them. To avoid getting into any unwanted
situation, it's important to ensure that they're rotated on a regular
basis and their archives are removed automatically.

To that end, a script called *logrotate* under **etc*cron.daily/*
invokes the *logrotate* command on a daily basis. Via the Anacron
service, the command runs a rotation as per the schedule defined in the
**etc*logrotate.conf* file and the configuration files for various
services located in the **etc*logrotate.d* directory. The configuration
files may be modified to alter the schedule or include additional tasks
such as removing, compressing, and emailing selected log files.

Here is what the **etc*cron.daily/logrotate* script contains:

![](images/00620.jpeg) 

The following returns the default content of the **etc*logrotate.conf*
file:

![](images/00621.jpeg) 

The file content shows the default log rotation frequency (weekly). It
indicates the period of time (4 weeks) to retain the rotated logs before
deleting them. Each time a log file is rotated, an empty replacement
file is created with the date as a suffix to its name, and the *rsyslog*
service is restarted. The script presents the option of compressing the
rotated files using the *gzip* utility. During the script execution, the
*logrotate* command checks for the presence of additional log
configuration files in the **etc*logrotate.d* directory and includes
them as necessary. The directives defined in the *logrotate.conf* file
have a global effect on all log files. You can define custom settings
for a specific log file in *logrotate.conf* or create a separate file in
the **etc*logrotate.d* directory. Any settings defined in user-defined
files overrides the global settings.

The **etc*logrotate.d* directory includes additional configuration files
for other service logs, as shown below:

![](images/00622.jpeg) 

Here there are log configuration files for a number of
services---*chrony*, *cups*, *dnf*, and *samba*---all with their own
rules defined. The following shows the file content for *btmp* (records
of failed user login attempts) that is used to control the rotation
behavior for the **var*log/btmp* file:

![](images/00623.jpeg) 

The rotation is once a month. The replacement file created will get
read/write permission bits for the owner (*root*), the owning group will
be set to *utmp*, and the *rsyslog* service will maintain one rotated
copy of the *btmp* log file.

**[The]{#part0024_split_001.html#id_339 .calibre10} Boot Log File**

Logs generated during the system startup display the service startup
sequence with a status showing whether the service was started
successfully. This information may help in any post-boot troubleshooting
if required. Boot logs are stored in the *boot.log* file under
**var*log*. Here are a few lines from the beginning of the file:

![](images/00624.jpeg) 

OK or FAILED within the square brackets indicates if the service was
started successfully or not.

**[The]{#part0024_split_001.html#id_340 .calibre10} System Log File**

The default location for storing most system activities, as defined in
the *rsyslog.conf* file, is the **var*log/messages* file. This file
saves log information in plain text format and may be viewed with any
file display utility, such as *cat*, *more*, *pg*, *less*, *head*, or
*tail*. This file may be observed in real time using the *tail* command
with the -f switch. The *messages* file captures the date and time of
the activity, hostname of the system, name and PID of the service, and a
short description of the event being logged.

[**EXAM TIP:**]{.c56} It is helpful to "tail" the messages file when
starting or restarting a system service or during testing to identify
any issues encountered.

The following illustrates some recent entries from this file:

![](images/00625.jpeg) 

Each line entry represents the detail for one event.

**[Logging]{#part0024_split_001.html#id_341 .calibre10} Custom
Messages**

Many times it is worthwhile to add a manual note to the system log file
to mark the start or end of an activity for future reference. This is
especially important when you run a script to carry out certain tasks
and you want to record the status or add comments at various stages
throughout its execution. This is also beneficial in debugging the
startup of an application to know where exactly it is failing.

The Modules section in the *rsyslog.conf* file provides the support via
the imuxsock module to record custom messages to the *messages* file
using the *logger* command. This command may be run by normal users or
the *root* user. The following example shows how to add a note
indicating the calling user has rebooted the system:

![](images/00626.jpeg) 

*tail* the last line from the *messages* file and you'll observe the
message recorded along with the timestamp, hostname, and PID:

![](images/00627.jpeg) 

You may add the -p option and specify a priority level either as a
numerical value or in the facility.priority format. The default priority
at which the events are recorded is user.notice. See the manual pages
for the *logger* command for more details.

**[The]{#part0024_split_001.html#id_342 .calibre10} systemd Journal**

In addition to the *rsyslog* service, RHEL offers a systemd-based
logging service for the collection and storage of logging data. This
service is implemented via the *systemd-journald* daemon. The function
of this service is to gather, store, and display logging events from a
variety of sources such as the kernel, *rsyslog* and other services,
initial RAM disk, and alerts generated during the early boot stage. It
stores these messages in the binary format in files called *journals*
that are located in the **run*log/journal* directory. These files are
structured and indexed for faster and easier searches, and may be viewed
and managed using the *journalctl* command. As you know, */run* is a
virtual file system that is created in memory at system boot, maintained
during system runtime, and destroyed at shutdown. Therefore, the data
stored therein is non-persistent, but you can enable persistent storage
for the logs if desired.

RHEL runs both *rsyslogd* and *systemd-journald* concurrently. In fact,
the data gathered by *systemd-journald* may be forwarded to *rsyslogd*
for further processing and persistent storage in text format.

The main configuration file for this service is
**etc*systemd/journald.conf*, which contains numerous default settings
that affect the overall functionality of the service. These settings may
be modified as required.

**[Retrieving]{#part0024_split_001.html#id_343 .calibre10} and Viewing
Messages**

RHEL provides the *journalctl* command to retrieve messages from the
journal for viewing in a variety of ways using different options. One
common usage is to run the command without any options to see all the
messages generated since the last system reboot. The following shows a
few initial entries from the journal:

![](images/00628.jpeg) 

Notice that the format of the messages is similar to that of the events
logged to the **var*log/messages* file that you saw earlier. Each line
begins with a timestamp followed by the system hostname, process name
with or without a PID, and the actual message.

Let's run the *journalctl* command with different options to produce
various reports.

To display detailed output for each entry, use the -o verbose option:

![](images/00629.jpeg) 

To view all events since the last system reboot, use the -b options:

![](images/00630.jpeg) 

You may specify -0 (default, since the last system reboot), -1 (the
previous system reboot), -2 (two reboots before), and so on to view
messages from previous system reboots.

To view only kernel-generated alerts since the last system reboot:

![](images/00631.jpeg) 

To limit the output to view a specific number of entries only (3 in the
example below), use the -n option:

![](images/00632.jpeg) 

To show all alerts generated by a particular service, such as *crond*:

![](images/00633.jpeg) 

To retrieve all messages logged for a certain process, such as the PID
associated with the *chronyd* service:

![](images/00634.jpeg) 

To reveal all messages for a particular system unit, such as
sshd.service:

![](images/00635.jpeg) 

To view all error messages logged between a date range, such as October
10, 2019 and October 16, 2019:

![](images/00636.jpeg) 

To get all warning messages that have appeared today and display them in
reverse chronological order:

![](images/00637.jpeg) 

You can specify the time range in hh:mm:ss format, or yesterday, today,
or tomorrow instead.

Similar to the -f (follow) option that is used with the *tail* command
for real-time viewing of a log file, you can use the same switch with
*journalctl* as well. Press Ctrl+c to terminate.

![](images/00638.jpeg) 

Check the manual pages of the *journalctl* command and the
*systemd-journald* service for more details.

**[Preserving]{#part0024_split_001.html#id_344 .calibre10} Journal
Information**

By default, journals are stored in the **run*log/journal* directory for
the duration of system runtime. This data is transient and it does not
survive across reboots. The *journalctl* command examples demonstrated
earlier retrieve journal information from this temporary location. The
*rsyslogd* daemon, by default, reads the temporary journals and stores
messages in the **var*log/messages* file. You can enable a separate
storage location for the journal to save all its messages there
persistently. The default is under the **var*log/journal* directory.
This will make the journal information available for future reference.

The *systemd-journald* service supports four options with the Storage
directive in its configuration file *journald.conf* to control how the
logging data is handled. These options are described in [Table
12-4](#part0024_split_001.html#id_737){.calibre5}.

::: c49
  ------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Option**   **Description**
  volatile     Stores data in memory only
  persistent   Stores data permanently under *var*log/journal and falls back to memory-only option if this directory does not exist or has a permission or other issue. The service creates *var*log/journal in case of its non-existence.
  auto         Similar to "persistent" but does not create *var*log/journal if it does not exist. This is the default option.
  none         Disables both volatile and persistent storage options. Not recommended.
  ------------ -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0024_split_001.html#id_737} 12-4 Journal Data Storage
Options**
:::

The default (auto) option appears more suitable as it stores data in
both volatile and on-disk storage; however, you need to create the
**var*log/journal* directory manually. This option provides two
fundamental benefits: faster query responses from in-memory storage and
access to historical log data from on-disk storage.

**Exercise 12-1: Configure Persistent Storage for Journal Information**

This exercise should be done on *server1* as *user1* with *sudo* where
required.

In this exercise, you will run the necessary steps to enable and confirm
persistent storage for the journals.

1. Create a subdirectory called *journal* under the **var*log*
directory and confirm:

![](images/00639.jpeg) 

2. Restart the *systemd-journald* service and confirm:

![](images/00640.jpeg) 

3. List the new directory and observe a subdirectory matching the
machine ID of the system as defined in the **etc*machine-id* file is
created:

![](images/00641.jpeg) 

Compare the name of the subdirectory with the ID stored in the
**etc*machine-id* file. They are identical.

![](images/00002.jpeg){.image} This log file is rotated automatically
once a month based on the settings in the *journald.conf* file. Check
the manual pages of the configuration file for details and relevant
directives.

This concludes the exercise.

**[System]{#part0024_split_001.html#id_345 .calibre10} Tuning**

RHEL uses a system tuning service called *tuned* to monitor storage,
networking, processor, audio, video, and a variety of other connected
devices, and adjusts their parameters for better performance or power
saving based on a chosen profile. There are several predefined tuning
profiles for common use cases shipped with RHEL that may be activated
either statically or dynamically.

The *tuned* service activates a selected profile at service startup and
continues to use it until it is switched to a different profile. This is
the static behavior and it is enabled by default.

The dynamic alternative adjusts the system settings based on the live
activity data received from monitored system components to ensure
optimal performance. In most cases, the utilization of system components
vary throughout the day. For example, a disk and processor's utilization
increases during a program startup and the network connection use goes
up during a large file transfer. A surge in a system component activity
results in heightened power consumption.

**[Tuning]{#part0024_split_001.html#id_346 .calibre10} Profiles**

*tuned* includes nine predefined profiles to support a variety of use
cases. In addition, you can create custom profiles from nothing or by
using one of the existing profiles as a template. In either case, you
need to store the custom profile under the **etc*tuned* directory in
order to be recognized by the *tuned* service.

Tuning profiles may be separated into three groups: (1) optimized for
better performance, (2) geared more towards power consumption, and (3)
that offers a balance between the other two and the maximum
performance/power combination. [Table
12-5](#part0024_split_001.html#id_738){.calibre5} lists and describes
these profiles.

::: c49
  ----------------------------------------------- -------------------------------------------------------------------------------------------------------------
  **Profile**                                     **Description**
  **Profiles Optimized for Better Performance**   
  Desktop                                         Based on the balanced profile for desktop systems. Offers improved throughput for interactive applications.
  Latency-performance                             For low-latency requirements
  Network-latency                                 Based on the latency-performance for faster network throughput
  Network-throughput                              Based on the throughput-performance profile for maximum network throughput
  Virtual-guest                                   Optimized for virtual machines
  Virtual-host                                    Optimized for virtualized hosts
  **Profiles Optimized for Power Saving**         
  Powersave                                       Saves maximum power at the cost of performance
  **Balanced/Max Profiles**                       
  Balanced                                        Preferred choice for systems that require a balance between performance and power saving
  Throughput-performance                          Provides maximum performance and consumes maximum power
  ----------------------------------------------- -------------------------------------------------------------------------------------------------------------

**[Table]{#part0024_split_001.html#id_738} 12-5 Tuning Profiles**
:::

Predefined profiles are located in the **usr*lib/tuned* directory in
subdirectories matching their names. The following shows a long listing
of the directory:

![](images/00642.jpeg) 

The default active profile set on *server1* and *server2* is the
*virtual-guest* profile, as the two systems are hosted in a VirtualBox
virtualized environment.

**[The]{#part0024_split_001.html#id_347 .calibre10} tuned-adm Command**

*tuned* comes with a single profile management command called
*tuned-adm*. This tool can list active and available profiles, query
current settings, switch between profiles, and turn the tuning off. This
command can also recommend the best profile for the system based on many
system attributes. Refer to the manual pages of the command for more
details.

The following exercise demonstrates the use of most of the management
operations listed above.

**[Exercise]{#part0024_split_001.html#id_348 .calibre10} 12-2: Manage
Tuning Profiles**

This exercise should be done on *server1* as *user1* with *sudo* where
required.

In this exercise, you will install the *tuned* service, start it now,
and enable it for auto-restart upon future system reboots. You will
display all available profiles and the current active profile. You will
switch to one of the available profiles and confirm. You will determine
the recommended profile for the system and switch to it. Finally, you
will deactivate tuning and reactivate it. You will confirm the
activation to conclude the exercise.

1. Install the *tuned* package if it is not already installed:

![](images/00643.jpeg) 

The output indicates that the software is already installed.

2. Start the *tuned* service and set it to autostart at reboots:

![](images/00644.jpeg) 

3. Confirm the startup:

![](images/00645.jpeg) 

4. Display the list of available tuning profiles:

![](images/00646.jpeg) 

The output shows the nine predefined profiles. It also exhibits the
current active profile.

5. List only the current active profile:

![](images/00647.jpeg) 

6. Switch to the *powersave* profile and confirm:

![](images/00648.jpeg) 

The active profile is now *powersave*.

7. Determine the recommended profile for *server1* and switch to
it:

![](images/00649.jpeg) 

The first instance of the command shows the best recommended profile for
*server1* based on its characteristics, the second command instance
switched to the recommended profile, and the third instance confirmed
the switching.

8. Turn off tuning:

![](images/00650.jpeg) 

The service will not perform any tuning until it is reactivated.

9. Reactivate tuning and confirm:

![](images/00651.jpeg) 

The tuning is re-enabled and the *virtual-guest* profile is in effect.
This concludes the exercise.

**[Chapter]{#part0024_split_001.html#id_349 .calibre10} Summary**

This chapter started with a discussion of systemd, the default service
management and system initialization scheme used in RHEL. We explored
key components of systemd, its key directories, and examined unit and
target configuration files. We utilized the lone systemd administration
command to switch system operational states, identify and set default
boot targets, and manage service start, stop, and status checking.

Next, we looked at the traditional system logging and newer systemd
journaling services. Both mechanisms have similarities and differences
in how they capture log data and where they direct it for storage and
retrieval. We examined the system log configuration file and the
configuration file that controls the log file rotation settings. The log
subsystem proves valuable when records are needed for monitoring,
troubleshooting, auditing, or reporting purpose.

Finally, we explored preconfigured tuning profiles and analyzed pros and
cons associated with each one of them. We demonstrated how to determine
a recommended profile for the system and how to set and activate it.

**[Review]{#part0024_split_001.html#id_350 .calibre10} Questions**

1. The *systemd* command may be used to rebuild a new kernel.
True or False?

2. Which command is used to manage system services?

3. Which configuration file must be modified to ensure journal
log entries are stored persistently?

4. What is the PID of the *systemd* process?

5. What is a target in *systemd*?

6. You need to append a text string "Hello world" to the system
log file. What would be the command to achieve this?

7. What is the recommended location to store custom log
configuration files?

8. What would the command *systemctl list-dependencies crond* do?

9. Name the two directory paths where *systemd* unit files are
stored.

10. What would you run to identify the recommended tuning profile
for the system?

11. What would the command *systemctl get-default* do?

12. *systemd* starts multiple services concurrently during system
boot. True or False?

13. What is the name of the boot log file?

14. Which *systemctl* subcommand is executed after a unit
configuration file has been modified to apply the changes?

15. Which other logging service complements the *rsyslog*
service?

16. A RHEL system is booted up. You want to view all messages
that were generated during the boot process. Which log file would you
look at?

17. What would the command *systemctl restart rsyslog* do?

18. What are the two common *systemd* targets production RHEL
servers are typically configured to run at?

19. By default, log files are rotated automatically every week.
True or False?

**[Answers]{#part0024_split_001.html#id_351 .calibre10} to Review
Questions**

1. False.

2. The *systemctl* command.

3. The *journald.conf* file under the **etc*systemd* directory.

4. The PID of the *systemd* process is 1.

5. A target is a collection of units.

6. The command to accomplish the desired result would be *logger
-i "Hello world"*.

7. The recommended location to store custom log configuration
files is **etc*rsyslog.d* directory.

8. The command provided will display all dependent units
associated with the specified service.

9. The directory locations are **etc*systemd/system* and
**usr*lib/systemd/system*.

10. The *tuned-adm recommend* command.

11. The command provided will reveal the current default boot
target.

12. True.

13. The *boot.log* file in the **var*log* directory.

14. The *daemon-reload* subcommand.

15. The *systemd-journald* service.

16. The **var*log/boot.log* file.

17. The command provided will restart the *rsyslog* service.

18. The two common *systemd* boot targets are multi-user and
graphical.

19. True.

**[Do-]{#part0024_split_001.html#id_352 .calibre10}It-Yourself Challenge
Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

**Lab 12-1: Modify Default Boot Target**

As *user1* with *sudo* on *server1*, modify the default boot target from
graphical to multi-user, and reboot the system to test it. Run the
*systemctl* and *who* commands after the reboot for validation. Restore
the default boot target back to graphical and reboot to verify. (Hint:
System Initialization and Service Management).

**[Lab]{#part0024_split_001.html#id_353 .calibre10} 12-2: Record Custom
Alerts**

As *user1* with *sudo* on *server1*, write the message "This is
\$LOGNAME adding this marker on \$(date)" to **var*log/messages* file.
Ensure that variable and command expansions work. Verify the entry in
the file. (Hint: System Logging).

**[Lab]{#part0024_split_001.html#id_354 .calibre10} 12-3: Apply Tuning
Profile**

As *user1* with *sudo* on *server1*, identify the current system tuning
profile with the *tuned-adm* command. List all available profiles. List
the recommended profile for *server1*. Apply the "balanced" profile and
verify with *tuned-adm*. (Hint: System Tuning).

[]{#part0025_split_000.html}
