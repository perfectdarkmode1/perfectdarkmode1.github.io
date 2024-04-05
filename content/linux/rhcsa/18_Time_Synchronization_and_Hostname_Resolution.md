This chapter describes the following major topics:

[![](images/00001.jpeg){.c37}]{.c36}Describe time synchronization and
the role of Network Time Protocol

[![](images/00001.jpeg){.c37}]{.c36}Comprehend the terms: time source,
NTP roles, and stratum levels

[![](images/00001.jpeg){.c37}]{.c36}Anatomy of the Chrony service
configuration file

[![](images/00001.jpeg){.c37}]{.c36}Configure and verify NTP/Chrony
client service

[![](images/00001.jpeg){.c37}]{.c36}View and set system date and time

[![](images/00001.jpeg){.c37}]{.c36}Overview of Domain Name System and
hostname resolution

[![](images/00001.jpeg){.c37}]{.c36}Understand various DNS roles

[![](images/00001.jpeg){.c37}]{.c36}Analyze entries in resolver
configuration files

[![](images/00001.jpeg){.c37}]{.c36}Perform name resolution using a
variety of lookup tools

[RHCSA Objectives:]{.c39}

43\. Configure time service clients

[48]{#part0030_split_000.html#id_809 .calibre10}. Configure hostname
resolution

::: {#part0030_split_000.html#calibre_pb_1 .calibre12}
:::

[]{#part0030_split_001.html}

[ T]{.c42}[he]{.c43} Chrony service, a new implementation of the Network
Time Protocol, maintains the clock on the system and keeps it
synchronized with a more accurate and reliable source of time. Providing
accurate and uniform time for systems on the network allows
time-sensitive applications such as monitoring software, backup tools,
scheduling utilities, billing systems, file sharing protocols, and
authentication programs to perform correctly and precisely. It also aids
logging and auditing services to capture and record messages and alerts
in log files with accurate timestamps.

Domain Name System is an OS-and hardware-independent network service
employed for determining the IP address of a system when its hostname is
known, and vice versa. This mechanism is implemented to map
human-friendly hostnames to their assigned numeric IP addresses by
consulting one or more servers offering the hostname resolution service.
This service has been used on the Internet and corporate networks as the
de facto standard for this purpose. DNS clients use this service to
communicate with remote systems. There are several lookup programs that
use DNS to obtain information.

**[Time]{#part0030_split_001.html#id_485 .calibre10} Synchronization**

*Network Time Protocol* (NTP) is a networking protocol for synchronizing
the system clock with remote time servers for accuracy and reliability.
This protocol has been in use with tens of millions of computing devices
employing it to synchronize their clocks with tens of thousands of time
servers deployed across the globe. Having steady and exact time on
networked systems allows time-sensitive applications, such as
authentication and email applications, backup and scheduling tools,
financial and billing systems, logging and monitoring software, and file
and storage sharing protocols, to function with precision.

NTP sends a stream of messages to configured time servers and binds
itself to the one with least amount of delay in its responses, the most
accurate, and may or may not be the closest distance-wise. The client
system maintains a drift in time in a file and references this file for
gradual drop in inaccuracy.

RHEL version 8 introduces a new implementation of NTP called *Chrony*.
Chrony uses the UDP protocol over the well-known port 123. If enabled,
it starts at system boot and continuously operates to keep the system
clock in sync with a more accurate source of time.

Chrony performs well on computers that are occasionally connected to the
network, attached to busy networks, do not run all the time, or have
variations in temperature.

**[Time]{#part0030_split_001.html#id_486 .calibre10} Sources**

A *time source* is any reference device that acts as a provider of time
to other devices. The most precise sources of time are the atomic
clocks. They use *Universal Time Coordinated* (UTC) for time accuracy.
They produce radio signals that radio clocks use for time propagation to
computer servers and other devices that require correctness in time.
When choosing a time source for a network, preference should be given to
the one that takes the least amount of time to respond. This server may
or may not be closest physically.

The common sources of time employed on computer networks are the local
system clock, an Internet-based public time server, and a radio clock.

The local system clock can be used as a provider of time. This requires
the maintenance of correct time on the server either manually or
automatically via *cron*. Keep in mind that this server has no way of
synchronizing itself with a more reliable and precise external time
source. Therefore, using the local system clock as a time server is the
least recommended option.

Several public time servers are available over the Internet for general
use (visit *[www.ntp.org](http://www.ntp.org){.calibre5}* for a list).
These servers are typically operated by government agencies, research
and scientific organizations, large software vendors, and universities
around the world. One of the systems on the local network is identified
and configured to receive time from one or more public time servers.
This option is preferred over the use of the local system clock.

The official *[ntp.org](http://ntp.org){.calibre5}* site also provides a
common pool called *[pool.ntp.org](http://pool.ntp.org){.calibre5}* for
vendors and organizations to register their own NTP servers voluntarily
for public use. Examples include
*[rhel.pool.ntp.org](http://rhel.pool.ntp.org){.calibre5}* and
*[ubuntu.pool.ntp.org](http://ubuntu.pool.ntp.org){.calibre5}* for
distribution-specific pools, and
*[ca.pool.ntp.org](http://ca.pool.ntp.org){.calibre5}* and
*[oceania.pool.ntp.org](http://oceania.pool.ntp.org){.calibre5}* for
country and continent/region-specific pools. Under these sub-pools, the
owners maintain multiple time servers with enumerated hostnames such as
*[0.rhel.pool.ntp.org](http://0.rhel.pool.ntp.org){.calibre5}*,*[1.rhel.pool.ntp.org](http://1.rhel.pool.ntp.org){.calibre5}*,
*[2.rhel.pool.ntp.org](http://2.rhel.pool.ntp.org){.calibre5}*, and so
on.

A radio clock is regarded as the perfect provider of time, as it
receives time updates straight from an atomic clock. *Global Positioning
System* (GPS), WWVB, and DCF77 are some popular radio clock methods. A
direct use of signals from these sources requires connectivity of some
hardware to the computer identified to act as an organizational or
site-wide time server.

**[NTP]{#part0030_split_001.html#id_487 .calibre10} Roles**

From an NTP standpoint, a system can be configured to operate as a
primary server, secondary server, peer, or client.

A *primary* server gets time from a time source and provides time to
secondary servers or directly to clients.

A *secondary* server receives time from a primary server and can be
configured to furnish time to a set of clients to offload the primary or
for redundancy. The presence of a secondary server on the network is
optional but highly recommended.

A *peer* reciprocates time with an NTP server. All peers work at the
same stratum level, and all of them are considered equally reliable.
Both primary and secondary servers can be peers of each other.

A *client* receives time from a primary or a secondary server and
adjusts its clock accordingly.

**[Stratum]{#part0030_split_001.html#id_488 .calibre10} Levels**

As mentioned, there are different types of time sources available so you
can synchronize the system clock. These time sources are categorized
hierarchically into several levels that are referred to as *stratum
levels* based on their distance from the reference clocks (atomic,
radio, and GPS). The reference clocks operate at stratum level 0 and are
the most accurate provider of time with little to no delay. Besides
stratum 0, there are fifteen additional levels that range from 1 to 15.
Of these, servers operating at stratum 1 are considered perfect, as they
get time updates directly from a stratum 0 device. See [Figure
18-1](#part0030_split_001.html#page_420){.calibre5} for a sample
hierarchy.

::: c49
::: width_
![](images/00896.jpeg){.calibre13}
:::

**Figure 18-1 NTP Stratum Levels**
:::

A stratum 0 device cannot be used on the network directly. It is
attached to a computer, which is then configured to operate at
stratum 1. Servers functioning at stratum 1 are called *time servers*
and they can be set up to deliver time to stratum 2 servers. Similarly,
a stratum 3 server can be configured to synchronize its time with a
stratum 2 server and deliver time to the next lower level servers, and
so on. Servers sharing the same stratum can be configured as peers to
exchange time updates with one another.

![](images/00002.jpeg){.image} If a secondary server also gets time
updates from a stratum 1 server, it will act as a peer to the primary
server.

There are a number of public NTP servers available for free that
synchronize time. They normally operate at higher stratum levels such as
2 and 3.

**[Chrony]{#part0030_split_001.html#id_489 .calibre10} Configuration
File**

The key configuration file for the Chrony service is *chrony.conf*
located in the */etc* directory. This file is referenced by the Chrony
daemon at startup to determine the sources to synchronize the clock, the
log file location, and other details. This file can be modified by hand
to set or alter directives as required. Some common directives used in
this file along with real or mock values are presented below with an
explanation in [Table 18-1](#part0030_split_001.html#id_751){.calibre5}:

  ----------- ---------------------------------------------------------------------------
  driftfile   *var*lib/chrony/drift
  logdir      *var*log/chrony
  pool        [0.rhel.pool.ntp.org](http://0.rhel.pool.ntp.org){.calibre5} iburst
  server      [server20s8.example.com](http://server20s8.example.com){.calibre5} iburst
  server      127.127.1.0
  peer        [prodntp1.abc.net](http://prodntp1.abc.net){.calibre5}
  ----------- ---------------------------------------------------------------------------

[Table 18-1](#part0030_split_001.html#id_751){.calibre5} describes these
directives.

::: c49
  --------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Directive**   **Description**
  driftfile       Indicates the location and name of the drift file to be used to record the rate at which the system clock gains or losses time. This data is used by Chrony to maintain local system clock accuracy.
  logdir          Sets the directory location to store the log files in
  pool            Defines the hostname that represents a pool of time servers. Chrony binds itself with one of the servers to get updates. In case of a failure of that server, it automatically switches the binding to another server within the pool.
                  The iburst option dictates the Chrony service to send the first four update requests to the time server every 2 seconds. This allows the daemon to quickly bring the local clock closer to the time server at startup.
  server          Defines the hostname or IP address of a single time server. The IP 127.127.1.0 is a special address that epitomizes the local system clock.
  peer            Identifies the hostname or IP address of a time server running at the same stratum level. A peer provides time to a server as well as receives time from the same server.
  --------------- ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0030_split_001.html#id_751} 18-1 Chrony Directives**
:::

There are plenty of other directives and options available with Chrony
that may be defined in this file. Use **man chrony.conf** for details.

**[Chrony]{#part0030_split_001.html#id_490 .calibre10} Daemon and
Command**

The Chrony service runs as a daemon program called *chronyd* that
handles time synchronization in the background. It uses the
configuration defined in the **etc*chrony.conf* file at startup and sets
its behavior accordingly. If the local clock requires a time adjustment,
Chrony takes multiple small steps toward minimizing the gap rather than
doing it abruptly in a single step. There are a number of additional
options available that may be passed to the service daemon if required.

The Chrony service has a command line program called *chronyc* available
that can be employed to monitor the performance of the service and
control its runtime behavior. There are a few subcommands available with
*chronyc*; the *sources* and *tracking* subcommands list current sources
of time and view performance statistics, respectively.

**[Exercise]{#part0030_split_001.html#id_491 .calibre10} 18-1: Configure
NTP Client**

This exercise should be done on *server10* as *user1* with *sudo* where
required.

In this exercise, you will install the Chrony software package and
activate the service without making any changes to the default
configuration. You will validate the binding and operation.

1[.]{.c19}Install the Chrony package using the *dnf* command:

![](images/00897.jpeg){.image2}

The software is already installed on the system.

2[.]{.c19}Ensure that preconfigured public time server entries are
present in the **etc*chrony.conf* file:

![](images/00898.jpeg){.image2}

There is a single pool entry set in the file by default. This pool name
is backed by multiple NTP servers behind the scene.

3[.]{.c19}Start the Chrony service and set it to autostart at reboots:

![](images/00899.jpeg){.image2}

4[.]{.c19}Examine the operational status of Chrony:

![](images/00900.jpeg){.image2}

The service has started successfully and it is set for autostart.

5[.]{.c19}Inspect the binding status using the *sources* subcommand with
*chronyc*:

![](images/00901.jpeg){.image2}

The output shows the number of available time sources in row 1 and rest
of the information in eight columns. Columns 1 to 4---M, S, Name/IP, and
Stratum---illustrate the mode, state, name/IP, and stratum level of the
source. The \^ means server and the \* implies current association.

Columns 4 to 8---Poll, Reach, LastRx, and Last Sample---display the
polling rate (6 means 64 seconds), reachability register (377 indicates
a valid response was received), how long ago the last sample was
received, and the offset between the local clock and the source at the
last measurement. Check out the manual pages of the *chronyc* command
and search for the section 'sources' for additional details.

The last line in the output depicts the *server10* binding with time
server *[gpg.n1zyy.com](http://gpg.n1zyy.com){.calibre5}*. This
association is identified with the asterisk character (\*) beside the
time server.

6[.]{.c19}Display the clock performance using the *tracking* subcommand
with *chronyc*:

![](images/00902.jpeg){.image2}

Lines 1 and 2 in the above output identify the current source of time
(Reference ID) and the stratum level it is configured at (Stratum). Line
3 shows the reference time at which the last measurement from the time
source was processed (Ref time). Line 4 displays the local time offset
from NTP time (System time). Line 5 depicts the last reported offset
from the NTP server (Last offset). Line 6 identifies the frequency at
which time adjustments are occurring (Frequency). The rest of the lines
in the output show additional information. Check out the manual pages of
the *chronyc* command and search for the section "tracking" for
additional details.

[**EXAM TIP:**]{.c56} You will not have access to the outside network
during the exam, so you will need to point your system to an NTP server
available on the exam network. Simply comment the default server/pool
directive(s) and add a single directive "server \<hostname\>" to the
file. Replace \<hostname\> with the NTP server name or its IP address as
provided.

The concludes the exercise.

**[Displaying]{#part0030_split_001.html#id_492 .calibre10} and Setting
System Date and Time**

System date and time can be viewed and manually adjusted with native
Linux tools such as the *timedatectl* command. This command can modify
the date, time, and time zone. When executed without any option, as
shown below, it outputs the local time, Universal time, RTC time
(*real-time clock*, a battery-backed hardware clock located on the
system board), time zone, and the status of NTP:

![](images/00903.jpeg){.image2}

This command requires that the NTP/Chrony service is deactivated in
order to make time adjustments. Run the *timedatectl* command as follows
to turn off NTP and verify:

![](images/00904.jpeg){.image2}

To modify the current date to January 1, 2020, and confirm:

![](images/00905.jpeg){.image2}

To change the time to 11:20 p.m. and date to November 18, 2019:

![](images/00906.jpeg){.image2}

To reactivate NTP:

![](images/00907.jpeg){.image2}

Check out the manual pages of the *timedatectl* command for more
subcommands and usage examples.

Alternatively, you can use the *date* command to view or modify the
system date and time.

To view current date and time:

![](images/00908.jpeg){.image2}

To change the date and time to November 22, 2019 1:00 p.m.:

![](images/00909.jpeg){.image2}

There are many options available with the *date* command. Consult its
manual pages for details.

**[DNS]{#part0030_split_001.html#id_493 .calibre10} and Name
Resolution**

*Domain Name System* (DNS) is an inverted tree-like structure employed
on the Internet and private networks (including home and corporate
networks) as the de facto standard for resolving hostnames to their
numeric IP addresses. DNS is platform-independent with support
integrated in every operating system. DNS is also referred to as BIND,
*Berkeley Internet Name Domain*, which is an implementation of DNS, and
it has been the most popular DNS application in use. *Name resolution*
is the technique that uses DNS/BIND for hostname lookups.

In order to understand DNS, a brief discussion of its components and
roles is imperative. The following subsections provide a look at the
client-side configuration files and commands, along with examples on how
to use the tools for resolving hostnames.

**[DNS]{#part0030_split_001.html#id_494 .calibre10} Name Space and
Domains**

The DNS *name space* is a hierarchical organization of all the domains
on the Internet. The root of the name space is represented by a period
(.). The hierarchy below the root (.) denotes the *top-level domains*
(TLDs) with names such as .com, .net, .edu, .org, .gov, .ca, and .de. A
DNS *domain* is a collection of one or more systems. Subdomains fall
under their parent domains and are separated by a period (.). For
example, *[redhat.com](http://redhat.com){.calibre5}* is a second-level
subdomain that falls under .com, and
*[bugzilla.redhat.com](http://bugzilla.redhat.com){.calibre5}* is a
third-level subdomain that falls under
*[redhat.com](http://redhat.com){.calibre5}*.

[Figure 18-2](#part0030_split_000.html#page_426){.calibre5} exhibits a
sample hierarchy of the name space, showing the top three domain levels.

::: c49
![](images/00910.jpeg){.image2}

**[Figure]{#part0030_split_001.html#id_752} 18-2 Sample DNS Hierarchy**
:::

At the deepest level of the hierarchy are the *leaves* (systems, nodes,
or any device with an IP address) of the name space. For example, a
network switch *net01* in *.travel.gc.ca* subdomain will be known as
*net01.travel.gc.ca*. If a period (.) is added to the end of this name
to look like *net01.travel.gc.ca.*, it will be referred to as the *Fully
Qualified Domain Name* (FQDN) for *net01*.

**[DNS]{#part0030_split_001.html#id_495 .calibre10} Roles**

From a DNS perspective, a system can be configured to operate as a
primary server, secondary server, or client. A DNS server is also
referred to as a *nameserver*.

A *primary* (a.k.a. *master*) *server* is responsible for its domain (or
subdomain). It maintains a master database of all the hostnames and
their associated IP addresses that are included in that domain. Any
changes in the database is done on this server. Each domain must have
one primary server with one or more optional *secondary* (a.k.a.
*slave*) servers for load balancing and redundancy. A secondary server
also stores an updated copy of the master database and it continues to
provide name resolution service in the event the primary server becomes
unavailable or inaccessible.

A *DNS client* queries nameservers for name lookups. Every system with
access to the Internet or other external networks will have the DNS
client functionality configured and operational. Setting up DNS client
on Linux involves two text files that are discussed in the next two
subsections.

**[Understanding]{#part0030_split_001.html#id_496 .calibre10} Resolver
Configuration File**

The *resolv.conf* file under */etc* is the DNS resolver configuration
file where information to support hostname lookups is defined. This file
may be edited manually with a text editor. It is referenced by resolver
utilities to construct and transmit queries. There are three key
directives set in this file--- domain, nameserver, and search---and they
are described in [Table
18-2](#part0030_split_001.html#id_766){.calibre5}.

::: c49
  --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  **Directive**   **Description**
  domain          Identifies the default domain name to be searched for queries
  nameserver      Declares up to three DNS server IP addresses to be queried one at a time in the order in which they are listed. Nameserver entries may be defined as separate line items with the directive or on a single line.
  search          Specifies up to six domain names, of which the first must be the local domain. No need to define the domain directive if the search directive is used.
  --------------- ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**[Table]{#part0030_split_001.html#id_766} 18-2 The Resolver
Configuration File**
:::

A sample entry showing the syntax is provided below for reference:

  ------------ -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  domain       [example.com](http://example.com){.calibre5}
  search       [example.net](http://example.net){.calibre5} [example.org](http://example.org){.calibre5} [example.edu](http://example.edu){.calibre5} [example.gov](http://example.gov){.calibre5}
  nameserver   192.168.0.1 8.8.8.8 8.8.4.4
  ------------ -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

A variation of the above would be:

  ------------ -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  domain       [example.com](http://example.com){.calibre5}
  search       [example.net](http://example.net){.calibre5} [example.org](http://example.org){.calibre5} [example.edu](http://example.edu){.calibre5} [example.gov](http://example.gov){.calibre5}
  nameserver   192.168.0.1
  nameserver   8.8.8.8
  nameserver   8.8.4.4
  ------------ -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Currently, there are two entries "search
[example.com](http://example.com){.calibre5}" and "nameserver
192.168.0.1" defined in the *resolv.conf* file on *server10* and
*server20*.

![](images/00911.jpeg){.image2}

On a system with this file absent, the resolver utilities only query the
nameserver configured on the localhost, determine the domain name from
the hostname of the system, and construct the search path based on the
domain name.

**Viewing and Adjusting Name Resolution Sources and Order** The
*nsswitch.conf* file under */etc* directs the lookup utilities to the
correct source to get hostname information. In the presence of multiple
sources, this file also identifies the order in which to consult them
and an action to be taken next. There are four keywords---success,
notfound, unavail, and tryagain---that oversee this behavior, and are
described along with default actions in [Table
18-3](#part0030_split_001.html#id_753){.calibre5}.

::: c49
  ------------- ------------------------------------------------------------------- -------------------------------------
  **Keyword**   **Meaning**                                                         **Default Action**
  success       Information found in source and provided to the requester           return (do not try the next source)
  notfound      Information not found in source                                     continue (try the next source)
  unavail       Source down or not responding; service disabled or not configured   continue (try the next source)
  tryagain      Source busy, retry later                                            continue (try the next source)
  ------------- ------------------------------------------------------------------- -------------------------------------

**[Table]{#part0030_split_001.html#id_753} 18-3 Name Service Source and
Order Determination**
:::

The following example entry shows the syntax of a relevant entry from
the *nsswitch.conf* file. It shows two sources for name resolution:
files (**etc*hosts*) and DNS (**etc*resolv.conf*).

  -------- ------- -----
  hosts:   files   dns
  -------- ------- -----

Based on the default behavior, the search will terminate if the
requested information is found in the *hosts* table. However, you can
alter this behavior and instruct the lookup programs to return if the
requested information is not found there. The modified entry will look
like:

  -------- --------------------------- -----
  hosts:   files \[notfound=return\]   dns
  -------- --------------------------- -----

This altered entry will ignore the DNS.

![](images/00002.jpeg){.image} See [Chapter
16](#part0028_split_000.html#page_375){.calibre5} for details on the
*etc*hosts file.

Once the *resolv.conf* and *nsswitch.conf* files are configured
appropriately, you can use any of the native client resolver tools for
lookups. Common query tools available in RHEL 8 include *dig*, *host*,
*nslookup*, and *getent*.

**[Performing]{#part0030_split_001.html#id_497 .calibre10} Name
Resolution with dig**

*dig* (*domain information groper*) is a DNS lookup utility. It queries
the nameserver specified at the command line or consults the
*resolv.conf* file to determine the nameservers to be queried. This tool
may be used to troubleshoot DNS issues due to its flexibility and
verbosity. The following shows a few usage examples.

To get the IP for *redhat.com* using the nameserver listed in the
*resolv.conf* file:

![](images/00912.jpeg){.image2}

The output shows the total time (13 milliseconds) it took to get the
result, the IP address (209.132.183.105) of
[redhat.com](http://redhat.com){.calibre5}, the nameserver IP
(192.168.0.1) used for the query, the DNS port number (53), query
timestamp, the size of the received message, and other information.

To perform a reverse lookup on the
[redhat.com](http://redhat.com){.calibre5} IP (209.132.183.105), use the
-x option with the command:

![](images/00913.jpeg){.image2}

![](images/00914.jpeg){.image2}

Reference the command's manual pages for details and options.

**[Performing]{#part0030_split_001.html#id_498 .calibre10} Name
Resolution with host**

*host* is an elementary DNS lookup utility that works on the same
principles as the *dig* command in terms of nameserver determination.
This tool produces lesser data in the output by default; however, you
can add the -v option for verbosity.

To perform a lookup on
*[redhat.com](http://redhat.com:){.calibre5}*[:](http://redhat.com:){.calibre5}

![](images/00915.jpeg){.image2}

Rerun the above with -v added. The output will be similar to that of the
*dig* command.

To perform a reverse lookup on the IP of
*[redhat.com](http://redhat.com){.calibre5}* using the -v flag to add
details:

![](images/00916.jpeg){.image2}

Refer to the command's manual pages for options and more information.

**[Performing]{#part0030_split_001.html#id_499 .calibre10} Name
Resolution with nslookup**

*nslookup* queries the nameservers listed in the *resolv.conf* file or
specified at the command line. The following shows a few usage examples.

To get the IP for *[redhat.com](http://redhat.com){.calibre5}* using
nameserver 8.8.8.8 instead of the nameserver defined in *resolv.conf*:

![](images/00917.jpeg){.image2}

To perform a reverse lookup on the IP of
*[redhat.com](http://redhat.com){.calibre5}* using the nameserver from
the resolver configuration file:

![](images/00918.jpeg){.image2}

Consult the command's manual pages on how to use it in interactive mode.

**[Performing]{#part0030_split_001.html#id_500 .calibre10} Name
Resolution with getent**

The *getent* (*get entries*) command is a rudimentary tool that can
fetch matching entries from the databases defined in the *nsswitch.conf*
file. This command reads the corresponding database and displays the
information if found. For name resolution, use the *hosts* database and
*getent* will attempt to resolve the specified hostname or IP address.
For instance, run the following for forward and reverse lookups:

![](images/00919.jpeg){.image2}

Check the command's manual pages for available flags and additional
information.

**[Chapter]{#part0030_split_001.html#id_501 .calibre10} Summary**

The focus of this chapter was on two topics: network time
synchronization and hostname resolution.

The chapter began with a discussion of Network Time Protocol, what role
it plays in keeping the clocks synchronized, and what is its
relationship with the Chrony service. We explored various sources for
obtaining time, different roles that systems could play, and the strata
paradigm. We analyzed the configuration file to understand some key
directives and their possible settings. We performed an exercise to
configure the service, display clock association, and analyze the
results. We also employed a couple of other RHEL tools to display the
system time and set it instantly.

We concluded the chapter with a deliberation of DNS and name resolution.
We discussed the concepts and roles, analyzed the resolver configuration
file, and examined the source/order determination file. We added
required entries to the resolver configuration file and tested the
functionality by employing client tools for hostname lookup.

**[Review]{#part0030_split_001.html#id_502 .calibre10} Questions**

1[.]{.c19}Chrony is an implementation of the Network Time Protocol. True
or False?

2[.]{.c19}What is the name and location of the DNS resolver file?

3[.]{.c19}What stratum level do two peer systems operate on a network?

4[.]{.c19}Provide the maximum number of nameservers that can be defined
in the resolver configuration file.

5[.]{.c19}What is the purpose of a drift file in Chrony/NTP?

6[.]{.c19}What is a relative distinguished name?

7[.]{.c19}What would you add to the Chrony configuration file if you
want to use the local system clock as the provider of time?

8[.]{.c19}BIND is an implementation of Domain Name System. True or
False?

9[.]{.c19}Define time source.

10[.]{.c23}Name the three DNS roles that a RHEL system can play.

11[.]{.c23}What would you run to check the NTP bind status with time
servers?

12[.]{.c23}Define DNS name space.

13[.]{.c23}Name the four Chrony/NTP roles that a RHEL system can play.

14[.]{.c23}Which file defines the name resolution sources and controls
the order in which they are consulted?

15[.]{.c23}What is the filename and directory location for the Chrony
configuration file?

16[.]{.c23}The Chrony client is preconfigured when the *chrony* software
package is installed. You just need to start the service to synchronize
the clock. True or False?

17[.]{.c23}List any three DNS lookup tools.

18[.]{.c23}List two utilities that you can use to change system time.

**[Answers]{#part0030_split_001.html#id_503 .calibre10} to Review
Questions**

1[.]{.c19}True.

2[.]{.c19}The DNS resolver file is called *resolv.conf* and it is
located in the */etc* directory.

3[.]{.c19}Two peers on a network operate at the same stratum level.

4[.]{.c19}Three.

5[.]{.c19}The purpose of a drift file is to keep track of the rate at
which the system clock gains or losses time.

6[.]{.c19}A relative distinguished name represents individual components
of a distinguished name.

7[.]{.c19}You will add "server 127.127.1.0" to the Chrony configuration
file and restart the service.

8[.]{.c19}True.

9[.]{.c19}A time source is a reference device that provides time to
other devices.

10[.]{.c23}From a DNS perspective, a RHEL machine can be a primary
server, a secondary server, or a client.

11[.]{.c23}You will run *chronyc sources* to check the binding status.

12[.]{.c23}DNS name space is a hierarchical organization of all the
domains on the Internet.

13[.]{.c23}From a Chrony/NTP standpoint, a RHEL machine can be a primary
server, a secondary server, a peer, or a client.

14[.]{.c23}The **etc*nsswitch.conf* file.

15[.]{.c23}The name of the Chrony configuration file is *chrony.conf*
and it is located in the */etc* directory.

16[.]{.c23}True.

17[.]{.c23}Name resolution tools are *dig*, *host*, *getent*, and
*nslookup*.

18[.]{.c23}The *timedatectl* and *date* commands can be used to modify
the system time.

**Do-It-Yourself Challenge Labs**

The following labs are useful to strengthen most of the concepts and
topics learned in this chapter. It is expected that you perform the labs
without external help. A step-by-step guide is not supplied, as the
knowledge and skill required to implement the lab has already been
disseminated in the chapter; however, hints to the relevant major
topic(s) are included.

**[Lab]{#part0030_split_001.html#id_504 .calibre10} 18-1: Modify System
Date and Time**

As *user1* with *sudo* on *server10*, execute the *date* and
*timedatectl* commands to check the current system date and time.
Identify the distinctions between the two outputs. Use *timedatectl* and
change the system date to a future date. Issue the *date* command and
change the system time to one hour ahead of the current time. Observe
the new date and time with both commands. Reset the date and time to the
current actual time using either the *date* or the *timedatectl*
command. (Hint: Time Synchronization).

**[Lab]{#part0030_split_001.html#id_505 .calibre10} 18-2: Configure
Chrony**

As *user1* with *sudo* on *server10*, install Chrony and mark the
service for autostart on reboots. Edit the Chrony configuration file and
comment all line entries that begin with "pool" or "server". Go to the
end of the file, and add a new line "server 127.127.1.0". Start the
Chrony service and run **chronyc sources** to confirm the binding.
(Hint: Time Synchronization).

[]{#part0031_split_000.html}
