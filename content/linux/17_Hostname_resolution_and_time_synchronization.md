## Chapter 17

\

### Hostname Resolution and Time Synchronization

\


\

#### This chapter describes the following major topics:

\

- Overview of Domain Name System and hostname resolution
- Understand various DNS roles
- Analyze entries in resolver configuration files
- Perform name resolution using a variety of lookup tools
- Describe time synchronization and the role of Network Time Protocol
- Comprehend the terms: time source, NTP roles, and stratum levels
- Anatomy of the Chrony service configuration file
- Configure and verify NTP/Chrony client service
- View and set system date and time

\

#### RHCSA Objectives:

##### 45. Configure hostname resolution
##### 41. Configure time service clients
\

Domain Name System is an OS- and hardware-independent network service
employed for determining the IP address of a system when its hostname is
known, and vice versa. This mechanism is implemented to map
human-friendly hostnames to their assigned numeric IP addresses by
consulting one or more servers offering the hostname resolution service.
This service has been used on the Internet and corporate networks as the
de facto standard for this purpose. DNS clients use this service to
communicate with remote systems. There are several lookup programs that
use DNS to obtain information.

\

::: {style="text-align: center;"}
![](image-NAZVOO3N.jpg){height="100%"}

The Chrony service, an implementation of the Network Time Protocol, maintains the clock on the system and keeps it synchronized with a more
accurate and reliable source of time. Providing accurate and uniform time for systems on the network allows time-sensitive applications such
as monitoring software, backup tools, scheduling utilities, billing systems, file sharing protocols, and authentication programs to perform
correctly and precisely. It also aids logging and auditing services to capture and record messages and alerts in log files with accurate
timestamps.

## DNS and Name Resolution 

\

Domain Name System (DNS) is an inverted tree-like structure employed on the Internet and private networks (including home and corporate
networks) as the de facto standard for resolving hostnames to their
numeric IP addresses. DNS is platform-independent with support
integrated in every operating system. DNS is also referred to as BIND,
Berkeley Internet Name Domain, which is an implementation of DNS, and it
has been the most popular DNS application in use. Name resolution is the
technique that uses DNS/BIND for hostname lookups.

\

To understand DNS, a brief discussion of its components and roles is
imperative. The following subsections provide a look at the client-side
configuration files and commands, along with examples on how to use the
tools for resolving hostnames.


## DNS Name Space and Domains {.style3}

\

The DNS name space is a hierarchical organization of all the domains on
the Internet. The root of the name space is represented by a period (.).
The hierarchy below the root (.) denotes the top-level domains (TLDs)
with names such as .com, .net, .edu, .org, .gov, .ca, and .de. A DNS
domain is a collection of one or more systems. Subdomains fall under
their parent domains and are separated by a period (.). For example,
redhat.com is a second-level subdomain that falls under .com, and
bugzilla.redhat.com is a third-level subdomain that falls under
redhat.com.

\

[Figure 17-1 exhibits a sample hierarchy of the name space, showing the
top three domain levels.](#chapter0521.html)

\


![](image-TJ7OW7U5.jpg)

\

At the deepest level of the hierarchy are the leaves (systems, nodes, or
any device with an IP address) of the name space. For example, a network
switch net01 in .travel.gc.ca subdomain will be known as
net01.travel.gc.ca. If a period (.) is added to the end of this name to
look like net01.travel.gc.ca., it will be referred to as the Fully
Qualified Domain Name (FQDN) for net01.



## DNS Roles {.style3}

\

From a DNS perspective, a system can be configured to operate as a
primary server, secondary server, or client. A DNS server is also
referred to as a nameserver.

\

A primary server is responsible for its domain (or subdomain). It
maintains a master database of all the hostnames and their associated IP
addresses that are included in that domain. All changes in the database
are done on this server. Each domain must have one primary server with
one or more optional secondary servers for load balancing and
redundancy. A secondary server also stores an updated copy of the master
database, and it continues to provide name resolution service in the
event the primary server becomes unavailable or inaccessible.

\

A DNS client queries nameservers for name lookups. Every system with
access to the Internet or other external networks will have the DNS
client functionality configured and operational. Setting up DNS client
on Linux involves two text files that are discussed in the next two
subsections.


## Understanding Resolver Configuration File

\

The resolv.conf file under /etc is the DNS resolver configuration file where information to support hostname lookups is defined. This file may
be edited manually with a text editor. It is referenced by resolver utilities to construct and transmit queries. There are three key
directives set in this file---domain, nameserver, and search---and they are described in Table 17-1.

\

  ----------------------------------- -----------------------------------
  Directive                           Description

  domain                              Identifies the default domain name
                                      to be searched for queries

  nameserver                          Declares up to three DNS server IP
                                      addresses to be queried one at a
                                      time in the order in which they are
                                      listed. Nameserver entries may be
                                      defined as separate line items with
                                      the directive or on a single line.

  search                              Specifies up to six domain names,
                                      of which the first must be the
                                      local domain. No need to define the
                                      domain directive if the search
                                      directive is used.
  ----------------------------------- -----------------------------------

 
\

Table 17-1 The Resolver Configuration File

\

A sample entry showing the syntax is provided below for reference:

\

  ----------------------------------- -----------------------------------
  domain                              example.com

  search                              example.net example.org example.edu
                                      example.gov

  nameserver                          192.168.0.1 8.8.8.8 8.8.4.4
  ----------------------------------- -----------------------------------

 
\

A variation of the above would be:

\

  ----------------------------------- -----------------------------------
  domain                              example.com

  search                              example.net example.org example.edu
                                      example.gov

  nameserver                          192.168.0.1

  nameserver                          8.8.8.8

  nameserver                          8.8.4.4
  ----------------------------------- -----------------------------------


\

Currently, there are two search and three nameserver entries in the
resolv.conf file on both server10 and server20. These entries are
automatically placed by the NetworkManager service.

\


![](image-KOBUAFWS.jpg){height="100%"}

</div>

On a system with this file absent, the resolver utilities only query the
nameserver configured on the localhost, determine the domain name from
the hostname of the system, and construct the search path based on the
domain name.



## Viewing and Adjusting Name Resolution Sources and Order

\

The nsswitch.conf file under /etc directs the lookup utilities to the
correct source to get hostname information. In the presence of multiple
sources, this file also identifies the order in which to consult them
and an action to be taken next. There are four keywords---success,
notfound, unavail, and tryagain---that oversee this behavior, and they
are described along with default actions in Table 17-2.

\

  ----------------------- ----------------------- -----------------------
  Keyword                 Meaning                 Default Action

  success                 Information found in    return (do not try the
                          source and provided to  next source)
                          the requester           

  notfound                Information not found   continue (try the next
                          in source               source)

  unavail                 Source down or not      continue (try the next
                          responding; service     source)
                          disabled or not         
                          configured              

  tryagain                Source busy, retry      continue (try the next
                          later                   source)
  ----------------------- ----------------------- -----------------------



\

Table 17-2 Name Service Source and Order Determination

\

The following example entry shows the syntax of a relevant entry from
the nsswitch.conf file. It shows two sources for name resolution: files
(/etc/hosts) and DNS (/etc/resolv.conf).

\

  ----------------------- ----------------------- -----------------------
  hosts:                  files                   dns

  ----------------------- ----------------------- -----------------------



\

Based on the default behavior, the search will terminate if the
requested information is found in the hosts table. However, you can
alter this behavior and instruct the lookup programs to return if the
requested information is not found there. The modified entry will look
like:

\

  ----------------------- ----------------------- -----------------------
  hosts:                  files                   dns
                          \[notfound=return\]     

  ----------------------- ----------------------- -----------------------



\

This altered entry will ignore the DNS.

\

See Chapter 15 "Networking, Network Devices, and Network Connections"
for details on the /etc/hosts file.

\

Once the resolv.conf and nsswitch.conf files are configured
appropriately, you can use any of the native client resolver tools for
lookups. Common query tools available in RHEL 9 include dig, host,
nslookup, and getent.



## Performing Name Resolution with dig {.style3}

\

dig (domain information groper) is a DNS lookup utility. It queries the
nameserver specified at the command line or consults the resolv.conf
file to determine the nameservers to be queried. This tool may be used
to troubleshoot DNS issues due to its flexibility and verbosity. The
following shows a few usage examples.

\

To get the IP for redhat.com using the nameserver listed in the
resolv.conf file:

\


![](image-YDHYBNK1.jpg)


![](image-TGZ3IJXO.jpg)

The output shows the total time (20 milliseconds) it took to get the
result, the IP addresses (52.200.142.250 and 34.235.198.240) of
redhat.com, the nameserver IPv6 (2001:1970:xxxxxx) used for the query,
query timestamp, the size of the received message (71 bytes), and other
information.

\

To perform a reverse lookup on the redhat.com IP (52.200.142.250), use
the -x option with the command:

\

![](image-H3BLEJ3V.jpg){height="100%"}

</div>

Reference the command's manual pages for details and options.



## Performing Name Resolution with host

\

host is an elementary DNS lookup utility that works on the same
principles as the dig command in terms of nameserver determination. This
tool produces lesser data in the output by default; however, you can add
the -v option for verbosity.

\

To perform a lookup on redhat.com:

\

![](image-5QNYLQ6V.jpg){height="100%"}

</div>

Rerun the above with -v added. The output will be similar to that of the
dig command.

\

To perform a reverse lookup on the IP of redhat.com using the -v flag to
add details:

\

![](image-WOZD6C5K.jpg){height="100%"}

</div>

Refer to the command's manual pages for options and more information.



## Performing Name Resolution with nslookup {.style3}

\

nslookup queries the nameservers listed in the resolv.conf file or
specified at the command line. The following shows a few usage examples.

\

To get the IP for redhat.com using nameserver 8.8.8.8 instead of the
nameserver defined in resolv.conf:

\

![](image-6MJ73J5Q.jpg)

To perform a reverse lookup on the IP of redhat.com using the nameserver
from the resolver configuration file:

\
![](image-TCI69YR4.jpg)

Consult the command's manual pages on how to use it in interactive mode.



## Performing Name Resolution with getent

\

The getent (get entries) command is a rudimentary tool that can fetch
matching entries from the databases defined in the nsswitch.conf file.
This command reads the corresponding database and displays the
information if found. For name resolution, use the hosts database and
getent will attempt to resolve the specified hostname or IP address. For
instance, run the following for forward and reverse lookups:


![](image-TMDUQ18Q.jpg)

Check the command's manual pages for available flags and additional
information.


## Time Synchronization {.style3}

### Network Time Protocol (NTP)

- networking protocol for synchronizing the system clock with remote time servers for accuracy and reliability.
- Having steady and exact time on networked systems allows time-sensitive applications, such as authentication and email applications, backup and scheduling tools, financial and billing systems, logging and monitoring software, and file and storage sharing protocols, to function with precision.

\

- sends a stream of messages to configured time servers and binds itself to the one with least amount of delay in its responses, the most accurate, and may or may not be the closest distance-wise. 
- client system maintains a drift in time in a file and references this file for gradual drop in inaccuracy.

\
### Crony
- RHEL 9 implementation of NTP
- uses the UDP port 123. 
- If enabled, it starts at system boot and continuously operates to keep the system clock in sync with a more accurate source of time.

\

- performs well on computers that are occasionally connected to the network, attached to busy networks, do not run all the time, or have variations in temperature.


## Time Sources


- A time source is any reference device that acts as a provider of time to other devices. 
- The most precise sources of time are the atomic clocks. 
- They use Universal Time Coordinated (UTC) for time accuracy. 
-  They produce radio signals that radio clocks use for time propagation to computer servers and other devices that require correctness in time. 
- When choosing a time source for a network, preference should be given to the one that takes the least amount of time to respond. 
- This server may or may not be closest physically.


The common sources of time employed on computer networks are:
- the local system clock
- Internet-based public time server
- radio clock.

\

local system clock 
- can be used as a provider of time. 
- This requires the maintenance of correct time on the server either manually or automatically via cron. 
- Keep in mind that this server has no way of synchronizing itself with a more reliable and precise external time source. 
- Using the local system clock as a time server is the least recommended option.

\
Public time server
- Several public time servers are available over the Internet for general use (visit www.ntp.org for a list). 
- These servers are typically operated by government agencies, research and scientific organizations, large software vendors, and universities around the world. 
- One of the systems on the local network is identified and configured to receive time from one or more public time servers. 
- Preferred over the use of the local system clock.

\

The official ntp.org site also provides a common pool called pool.ntp.org for vendors and organizations to register their own NTP
servers voluntarily for public use. 
Examples:
- rhel.pool.ntp.org and ubuntu.pool.ntp.org for distribution-specific pools, 
- ca.pool.ntp.org and oceania.pool.ntp.org for country and continent/region-specific pools. 

Under these sub-pools, the owners maintain multiple time servers with enumerated hostnames such as 0.rhel.pool.ntp.org, 1.rhel.pool.ntp.org, 2.rhel.pool.ntp.org, and so on.

\

Radio clock 
- Regarded as the perfect provider of time
- Receives time updates straight from an atomic clock. 
- Global Positioning System (GPS), WWVB, and DCF77 are some popular radio clock methods. 
- A direct use of signals from these sources requires connectivity of some hardware to the computer identified to act as an organizational or site-wide time server.

## NTP Roles


- a system can be configured to operate as a primary server, secondary server, peer, or client.\

**Primary server** 
- gets time from a time source and provides time to secondary servers or directly to clients.

**secondary server** 
- receives time from a primary server and can be configured to furnish time to a set of clients to offload the primary or for redundancy. 
- The presence of a secondary server on the network is optional but highly recommended.

**peer** 
- reciprocates time with an NTP server. 
- All peers work at the same stratum level, and all of them are considered equally reliable.

**client** 
- Receives time from a primary or a secondary server and adjusts its clock accordingly.

## Stratum Levels

\
- time sources are categorized hierarchically into several levels that are referred to as stratum levels based on their distance from the reference clocks (atomic, radio, and GPS). 
- The reference clocks operate at stratum level 0 and are the most accurate provider of time with little to no delay. 
-  Besides stratum 0, there are fifteen additional levels that range from 1 to 15. 
-  Of these, servers operating at stratum 1 are considered perfect, as they get time updates directly from a stratum 0 device. 

- A stratum 0 device cannot be used on the network directly. It is attached to a computer, which is then configured to operate at stratum 1. 
- Servers functioning at stratum 1 are called time servers and they can be set up to deliver time to stratum 2 servers. 
- Similarly, a stratum 3 server can be configured to synchronize its time with a stratum 2 server and deliver time to the next lower-level servers, and so on. 
- Servers sharing the same stratum can be configured as peers to exchange time updates with one another.

![](image-OOGYXDFA.jpg){height="100%"}

\
There are numerous public NTP servers available for free that synchronize time. 
They normally operate at higher stratum levels such as 2 and 3.

## Chrony Configuration File

**/etc/chrony.conf**
- key configuration file for the Chrony service
- referenced by the Chrony daemon at startup to determine the sources to synchronize the clock, the log file location, and other details. 
- can be modified by hand to set or alter directives as required. 
- common directives used in this file along with real or mock values are presented below:

driftfile                           
- /var/lib/chrony/drift
- Indicates the location and name of the drift file to be used to record the rate at which the system clockgains or losses time. This data is used by Chrony to maintain local system clock accuracy.

logdir                              
- /var/log/chrony
-  Sets the directory location to store the log files in

pool                                
- 0.rhel.pool.ntp.org iburst
- Defines the hostname that represents a pool of time servers. Chrony binds itself with one of the servers to get updates. In case of a failure of that server, it automatically switches the binding to another server within the pool.
- The iburst option dictates the Chrony service to send the first four update requests to the time server every 2 seconds. This allows the daemon to quickly bring the local clock closer to the time server at startup.

server                              
- server20s8.example.com iburst
- Defines the hostname or IP address of a single time server. 

server                              
- 127.127.1.0
- The IP 127.127.1.0 is a special address that epitomizes the local system clock.

peer                                
- prodntp1.abc.net
-  Identifies the hostname or IP address of a time server running at the same stratum level. A peer provides time to a server as well as receives time from the same server

There are plenty of other directives and options available with Chrony
that may be defined in this file. Use man chrony.conf for details.

## Chrony Daemon and Command


The Chrony service runs as a daemon program called chronyd that handles time synchronization in the background. 
It uses the configuration defined in the /etc/chrony.conf file at startup and sets its behavior accordingly. 
If the local clock requires a time adjustment, Chrony takes multiple small steps toward minimizing the gap rather than doing it abruptly in a single step. 
There are a number of additional options available that may be passed to the service daemon if required.

The Chrony service has a command line program called `chronyc` available that can be employed to monitor the performance of the service and control its runtime behavior. 
There are a few subcommands available with chronyc; 
the sources and tracking subcommands list current sources of time and view performance statistics, respectively.

## Exercise 17-1: Configure NTP Client (server10)

- install the Chrony software package and activate the service without making any changes to the default configuration. 
- validate the binding and operation.

1\. Install the Chrony package using the dnf command:

![](image-12U3TD72.jpg)

The software is already installed on the system.


2\. Ensure that preconfigured public time server entries are present in
the /etc/chrony.conf file:

```
[root@server1 ~]# grep -E 'pool|server' /etc/chrony.conf | grep -v ^#
pool 2.rhel.pool.ntp.org iburst
```

There is a single pool entry set in the file by default. This pool name is backed by multiple NTP servers behind the scenes.

3\. Start the Chrony service and set it to autostart at reboots:
`sudo systemctl --now enable chronyd`

![](image-05VCU30R.jpg)

4\. Examine the operational status of Chrony:
`sudo systemctl status chronyd --no-pager -l`
![](image-Z4GH16SN.jpg)

The service has started successfully and it is set for autostart.

5\. Inspect the binding status using the sources subcommand with chronyc:
```
[root@server1 ~]# chronyc sources
MS Name/IP address         Stratum Poll Reach LastRx Last sample               
===============================================================================
^+ ntp7-2.mattnordhoffdns.n>     2   8   377   324  -3641us[-3641us] +/-   53ms
^* 2600:1700:4e60:b983::123      1   8   377   430   +581us[  +84us] +/-   36ms
^- 2600:1700:5a0f:ee00::314>     2   8   377    58  -1226us[-1226us] +/-   50ms
^- 2603:c020:6:b900:ed2f:b4>     2   9   377   320   +142us[ +142us] +/-   73ms

```

![](image-QQAUUTE5.jpg)

^ means the source is a server
\* implies current association with the source.

Poll
- polling rate (6 means 64 seconds), 
Reach
- reachability register (377 indicates a valid response was received), 
Last sample
- how long ago the last sample was received, and the offset between the local clock and the source at the
last measurement

asterisk character (\*) beside the time server depicts the NTP server bound to the local server
The second time source ntp3.torix.ca from the top in the output depicts that server10 is bound to it.


6\. Display the clock performance using the tracking subcommand with chronyc:
```
[root@server1 ~]# chronyc tracking
Reference ID    : 2EA39303 (2600:1700:4e60:b983::123)
Stratum         : 2
Ref time (UTC)  : Sun Jun 16 12:05:45 2024
System time     : 286930.187500000 seconds slow of NTP time
Last offset     : -0.000297195 seconds
RMS offset      : 2486.306152344 seconds
Frequency       : 3.435 ppm slow
Residual freq   : -0.034 ppm
Skew            : 0.998 ppm
Root delay      : 0.064471066 seconds
Root dispersion : 0.003769779 seconds
Update interval : 517.9 seconds
Leap status     : Normal
```

![](image-U9AIT51T.jpg)

Rows 1 and 2 in the above output identify the current source of time
(Reference ID) and the stratum level it is configured at (Stratum). Row
3 shows the reference time at which the last measurement from the time
source was processed (Ref time). Row 4 displays the local time offset
from the NTP time (System time). Row 5 depicts the last reported offset
from the NTP server (Last offset). Row 6 identifies the frequency at
which time adjustments are occurring (Frequency). The rest of the rows
show additional information. Check out the manual pages of the chronyc
command and search for the section "tracking" for additional details.
\

EXAM TIP: You will not have access to the outside network during the exam. You will need to point your system to an NTP server available on the exam network. Simply comment the default server/pool directive(s) and add a single directive "server \<hostname\>" to the file. Replace \<hostname\> with the NTP server name or its IP address as provided.

The concludes the exercise.

## Displaying and Setting System Date and Time


System date and time can be viewed and manually adjusted with native Linux tools such as the timedatectl command. 
This command can modify the date, time, and time zone. 
When executed without any option, as shown below, it outputs the local time, Universal time, RTC time (real-time
clock, a battery-backed hardware clock located on the system board), time zone, and the status of the NTP service:


![](image-2VNY85LG.jpg)

This command requires that the NTP/Chrony service is deactivated in
order to make time adjustments. Run the timedatectl command as follows
to turn off NTP and verify:

\

![](image-UYIURDAL.jpg){height="100%"}

</div>

To modify the current date to February 28, 2023, and confirm:

\

![](image-PBWZS3DT.jpg){height="100%"}

</div>

To change both date and time in one go (March 18, 2023 11:20 p.m.):

\

![](image-KLSPK1PF.jpg){height="100%"}

</div>

To reactivate NTP:

\

![](image-XCSIHCHZ.jpg){height="100%"}

</div>

Check out the manual pages of the timedatectl command for more
subcommands and usage examples.

\

Alternatively, you can use the date command to view or modify the system
date and time.

\

To view current date and time:

\

![](image-WD0CY9GL.jpg){height="100%"}

</div>

To change the date and time to February 11, 2023, 8:00 a.m.:

\

<div>

![](image-8U96CFAF.jpg){height="100%"}

</div>

There are many options available with the date command. Consult its
manual pages for details.

\

To return the system to the current date and time execute sudo
timedatectl set-ntp with the false and then with the true argument.

::: {style="page-break-before: always;"}
:::

[]{#chapter0537.html}

## Chapter Summary {.style3}

\

The focus of this chapter was on two topics: hostname resolution and
network time synchronization.

\

The chapter began with a discussion of DNS and name resolution. We
discussed the concepts and roles, analyzed the resolver configuration
file, and examined the source/order determination file. We added
required entries to the resolver configuration file and tested the
functionality by employing client tools for hostname lookup.

\

We concluded the chapter with a deliberation of Network Time Protocol,
what role it plays in keeping the clocks synchronized, and what is its
relationship with the Chrony service. We explored various sources for
obtaining time, different roles that systems could play, and the strata
paradigm. We analyzed the configuration file to understand some key
directives and their possible settings. We performed an exercise to
configure the service, display clock association, and analyze the
results. We also employed a couple of other RHEL tools to display the
system time and set it instantly.

::: {style="page-break-before: always;"}
:::

[]{#chapter0538.html}

## Review Questions {.style3}

\

1\. Provide the maximum number of nameservers that can be defined in the
resolver configuration file.

2\. What is the purpose of a drift file in Chrony/NTP?

3\. The Chrony client is preconfigured when the chrony software package
is installed. You just need to start the service to synchronize the
clock. True or False?

4\. List any three DNS lookup tools.

5\. List two utilities that you can use to change system time.

6\. What is a relative distinguished name in a DNS hierarchy?

7\. What would you add to the Chrony configuration file if you want to
use the local system clock as the provider of time?

8\. BIND is an implementation of Domain Name System. True or False?

9\. Define time source.

10\. Name the three DNS roles that a RHEL system can play.

11\. Chrony is an implementation of the Network Time Protocol. True or
False?

12\. What is the name and location of the DNS resolver file?

13\. What stratum level do two peer time sources operate on a network?

14\. What would you run to check the NTP bind status with time servers?

15\. Define DNS name space.

16\. Name the four Chrony/NTP roles that a RHEL system can play.

17\. Which file defines the name resolution sources and controls the
order in which they are consulted?

18\. What is the filename and directory location for the Chrony
configuration file?

::: {style="page-break-before: always;"}
:::

[]{#chapter0539.html}

## Answers to Review Questions {.style3}

\

1\. Three.

2\. The purpose of a drift file is to keep track of the rate at which
the system clock gains or losses time.

3\. True.

4\. Name resolution tools are dig, host, getent, and nslookup.

5\. The timedatectl and date utilities can be used to modify the system
time.

6\. A relative distinguished name represents individual components of a
distinguished name.

7\. You will add "server 127.127.1.0" to the Chrony configuration file
and restart the service.

8\. True.

9\. A time source is a reference device that provides time to other
devices.

10\. From a DNS perspective, a RHEL machine can be a primary server, a
secondary server, or a client.

11\. True.

12\. The DNS resolver file is called resolv.conf and it is located in
the /etc directory.

13\. Two peers on a network operate at the same stratum level.

14\. You will run chronyc sources to check the binding status.

15\. DNS name space is a hierarchical organization of all the domains on
the Internet.

16\. From a Chrony/NTP standpoint, a RHEL machine can be a primary
server, a secondary server, a peer, or a client.

17\. The /etc/nsswitch.conf file.

18\. The name of the Chrony configuration file is chrony.conf and it is
located in the /etc directory.

::: {style="page-break-before: always;"}
:::

[]{#chapter0540.html}

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

[]{#chapter0541.html}

## Lab 17-1: Configure Chrony {.style3}

\

As user1 with sudo on server40, install Chrony and mark the service for
autostart on reboots. Edit the Chrony configuration file and comment all
line entries that begin with "pool" or "server". Go to the end of the
file, and add a new line "server 127.127.1.0". Start the Chrony service
and run chronyc sources to confirm the binding. (Hint: Time
Synchronization).

::: {style="page-break-before: always;"}
:::

[]{#chapter0542.html}

## Lab 17-2: Modify System Date and Time {.style3}

\

As user1 with sudo on server40, execute the date and timedatectl
commands to check the current system date and time. Identify the
distinctions between the two outputs. Use timedatectl and change the
system date to a future date. Issue the date command and change the
system time to one hour ahead of the current time. Observe the new date
and time with both commands. Reset the date and time to the current
actual time by disabling and re-enabling the NTP service using the
timedatectl command. (Hint: Time Synchronization).

::: {style="page-break-before: always;"}
:::

[]{#chapter0543.html}
