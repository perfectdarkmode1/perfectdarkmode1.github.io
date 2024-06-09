## Chapter 19 {style="text-align: right"}

\

### The Linux Firewall {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

This chapter describes the following major topics:

\

Describe Linux firewall for host-based security control

\

Overview of the firewalld service

\

Understand the concepts of firewalld zones and services

\

Analyze zone and service configuration files

\

Control access to network services and ports through firewalld

\

Use firewall-cmd command to manage firewall rules

\

RHCSA Objectives:

\

47\. Restrict network access using firewall-cmd/firewall

52\. Configure firewall settings using firewall-cmd/firewalld

::: {style="page-break-before: always;"}
:::

\

Running a system in a networked or an Internet-facing environment
requires that some security measures be taken to tighten access to the
system in general and individual services in particular. This can be
accomplished by implementing a firewall and restricting inbound traffic
to allowed ports from valid source IP addresses only. We discuss a
host-based firewall solution in this chapter.

\

::: {style="text-align: center;"}
![](image-0MNXH66H.jpg){height="100%"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0564.html}

## Firewall Overview {.style3}

\

A firewall is a protective layer implemented at the network or server
level to secure, monitor, and control inbound and outbound traffic flow.
Firewalls employed at the network level use either dedicated hardware or
sophisticated software appliances to form a shield around the network.
Server level firewalls are referred to as host-based firewalls and they
run in a computer operating system to monitor and manage traffic in and
out. Firewalls defend a network or an individual server from undesired
traffic.

\

RHEL is shipped with a host-based firewall solution that works by
filtering data packets. A data packet is formed as a result of a process
called encapsulation whereby the header information is attached to a
message (called payload) during packet formation. The header includes
information such as source and destination IP addresses, port, and type
of data. Based on predefined rules, a firewall intercepts each inbound
and outbound data packet, inspects its header, and decides whether to
allow the packet to pass through.

\

Ports are defined in the /etc/services file for common network services
that are standardized across all network operating systems, including
RHEL. Some common services and the ports they listen on are FTP (File
Transfer Protocol) on port 21, SSH (Secure Shell) 22, Postfix (an email
service) 25, HTTP (HyperText Transfer Protocol) 80, and NTP (Network
Time Protocol) on port 123.

\

The host-based firewall solution employed in RHEL uses a kernel module
called netfilter together with a filtering and packet classification
framework called nftables for policing the traffic movement. It also
supports other advanced features such as Network Address Translation
(NAT) and port forwarding. This firewall solution inspects, modifies,
drops, or routes incoming, outgoing, and forwarded network packets based
on defined rulesets.

::: {style="page-break-before: always;"}
:::

[]{#chapter0565.html}

## Overview of the firewalld Service {.style3}

\

firewalld is the default host-based firewall management service in RHEL
9. One of the major advantages is its ability to add, modify, or delete
firewall rules immediately without disrupting current network
connections or restarting the service process. This is especially useful
in testing and troubleshooting scenarios. firewalld also allows to save
rules persistently so that they are activated automatically at system
reboots.

\

The firewalld service lets you perform management operations at the
command line using the firewall-cmd command, graphically using the web
console, or manually by editing rules files. firewalld stores the
default rules in files located in the /usr/lib/firewalld directory, and
those that contain custom rules in the /etc/firewalld directory. The
default rules files may be copied to the custom rules directory and
modified.

::: {style="page-break-before: always;"}
:::

[]{#chapter0566.html}

## firewalld Zones {.style3}

\

firewalld uses the concept of zones for easier and transparent traffic
management. Zones define policies based on the trust level of network
connections and source IP addresses. A network connection can be part of
only one zone at a time; however, a zone can have multiple network
connections assigned to it. Zone configuration may include services,
ports, and protocols that may be open or closed. It may also include
rules for advanced configuration items such as masquerading, port
forwarding, NAT'ing, ICMP filters, and rich language. Rules for each
zone are defined and manipulated independent of other zones.

\

firewalld inspects each incoming packet to determine the source IP
address and applies the rules of the zone that has a match for the
address. In the event no zone configuration matches the address, it
associates the packet with the zone that has the network connection
defined, and applies the rules of that zone. If neither works, firewalld
associates the packet with the default zone, and enforces the rules of
the default zone on the packet.

\

The firewalld software installs several predefined zone files that may
be selected or customized. These files include templates for traffic
that must be blocked or dropped, and for traffic that is public-facing,
internal, external, home, public, trusted, and work-related. Of these,
the public zone is the default zone, and it is activated by default when
the firewalld service is started. Table 19-1 lists and describes the
predefined zones sorted based on the trust level from trusted to
untrusted.

\

  ----------------------------------- -----------------------------------
  Zone                                Description

  trusted                             Allow all incoming traffic

  internal                            Reject all incoming traffic except
                                      for what is allowed. Intended for
                                      use on internal networks.

  home                                Reject all incoming traffic except
                                      for what is allowed. Intended for
                                      use in homes.

  work                                Reject all incoming traffic except
                                      for what is allowed. Intended for
                                      use at workplaces.

  dmz                                 Reject all incoming traffic except
                                      for what is allowed. Intended for
                                      use in publicly accessible
                                      demilitarized zones.

  external                            Reject all incoming traffic except
                                      for what is allowed. Outgoing IPv4
                                      traffic forwarded through this zone
                                      is masqueraded to look like it
                                      originated from the IPv4 address of
                                      an outgoing network interface.
                                      Intended for use on external
                                      networks with masquerading enabled.

  public                              Reject all incoming traffic except
                                      for what is allowed. It is the
                                      default zone for any newly added
                                      network interfaces. Intended for us
                                      in public places.

  block                               Reject all incoming traffic with
                                      icmp-host-prohibited message
                                      returned. Intended for use in
                                      secure places.

  drop                                Drop all incoming traffic without
                                      responding with ICMP errors.
                                      Intended for use in highly secure
                                      places.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 19-1 firewalld Default Zones

\

For all the predefined zones, outgoing traffic is allowed by default.

::: {style="page-break-before: always;"}
:::

[]{#chapter0567.html}

## Zone Configuration Files {.style3}

\

firewalld stores zone rules in XML format at two locations: the
system-defined rules in the /usr/lib/firewalld/zones directory, and the
user-defined rules in the /etc/firewalld/zones directory. The files at
the former location can be used as templates for adding new rules, or
applied instantly to any available network connection. A system zone
configuration file is automatically copied to the /etc/firewalld/zones
directory if it is modified with a management tool. Alternatively, you
can copy the required zone file to the /etc/firewalld/zones directory
manually, and make the necessary changes. The firewalld service reads
the files saved in this location, and applies the rules defined in them.
A listing of the system zone files is presented below:

\

<div>

![](image-S4NM3TC3.jpg){height="100%"}

</div>

The default public zone file is displayed below:

\

<div>

![](image-ZBGJ36OA.jpg){height="100%"}

</div>

As depicted in the screenshot, the zone has a name and description, and
it contains a list of all the allowed services---ssh, dhcpv6-client, and
cockpit. See the manual pages for firewalld.zone for details on zone
configuration files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0568.html}

## firewalld Services {.style3}

\

In addition to the concept of zones, firewalld also uses the idea of
services for easier activation and deactivation of specific rules.
firewalld services are preconfigured firewall rules delineated for
various services and stored in different files. The rules consist of
necessary settings, such as the port number, protocol, and possibly
helper modules, to support the loading of the service. firewalld
services can be added to a zone. By default, firewalld blocks all
traffic unless a service or port is explicitly opened.

::: {style="page-break-before: always;"}
:::

[]{#chapter0569.html}

## Service Configuration Files {.style3}

\

firewalld stores service rules in XML format at two locations: the
system-defined rules in the /usr/lib/firewalld/services directory, and
the user-defined rules in the /etc/firewalld/services directory. The
files at the former location can be used as templates for adding new
service rules, or activated instantly. A system service configuration
file is automatically copied to the /etc/firewalld/services directory if
it is modified with a management tool. Alternatively, you can copy the
required service file to the /etc/firewalld/services directory manually,
and make the necessary changes. The firewalld service reads the files
saved in this location, and applies the rules defined in them. A listing
of the system service files is presented below:

\

<div>

![](image-3UHDIN7E.jpg){height="100%"}

</div>

The following shows the content of the ssh service file:

\

<div>

![](image-IH333ZL1.jpg){height="100%"}

</div>

As depicted in the screenshot, the service has a name and description,
and it defines the port and protocol for the service. See the manual
pages for firewalld.service for details on service configuration files.

::: {style="page-break-before: always;"}
:::

[]{#chapter0570.html}

## Firewalld Management {.style3}

\

Managing the firewalld service involves a number of operations, such as
listing, querying, adding, changing, and removing zones, services,
ports, IP sources, and network connections. There are three methods
available in RHEL 9 to perform the management tasks. They include the
firewall-cmd utility for those who prefer to work at the command line
and the web interface for graphical administration. The third management
option is to make use of the zone and service templates, and edit them
manually as desired. We use the command line method in this book.

::: {style="page-break-before: always;"}
:::

[]{#chapter0571.html}

## The firewall-cmd Command {.style3}

\

The firewall-cmd command is a powerful tool to manage the firewalld
service at the command prompt. This tool can be used to add or remove
rules from the runtime configuration, or save any modifications to
service configuration for persistence. It supports numerous options for
the management of zones, services, ports, connections, and so on; Table
19-2 lists and describes the common options only.

\

  ----------------------------------- -----------------------------------
  Option                              Description

  General                             

  \--state                            Displays the running status of
                                      firewalld

  \--reload                           Reloads firewall rules from zone
                                      files. All runtime changes are
                                      lost.

  \--permanent                        Stores a change persistently. The
                                      change only becomes active after a
                                      service reload or restart.

  Zones                               

  \--get-default-zone                 Shows the name of the
                                      default/active zone

  \--set-default-zone                 Changes the default zone for both
                                      runtime and permanent configuration

  \--get-zones                        Prints a list of available zones

  \--get-active-zones                 Displays the active zone and the
                                      assigned interfaces

  \--list-all                         Lists all settings for a zone

  \--list-all-zones                   Lists the settings for all
                                      available zones

  \--zone                             Specifies the name of the zone to
                                      work on. Without this option, the
                                      default zone is used.

  Services                            

  \--get-services                     Prints predefined services

  \--list-services                    Lists services for a zone

  \--add-service                      Adds a service to a zone

  \--remove-service                   Removes a service from a zone

  \--query-service                    Queries for the presence of a
                                      service

  Ports                               

  \--list-ports                       Lists network ports

  \--add-port                         Adds a port or a range of ports to
                                      a zone

  \--remove-port                      Removes a port from a zone

  \--query-port                       Queries for the presence of a port

  Network Connections                 

  \--list-interfaces                  Lists network connections assigned
                                      to a zone

  \--add-interface                    Binds a network connection to a
                                      zone

  \--change-interface                 Changes the binding of a network
                                      connection to a different zone

  \--remove-interface                 Unbinds a network connection from a
                                      zone

  IP Sources                          

  \--list-sources                     Lists IP sources assigned to a zone

  \--add-source                       Adds an IP source to a zone

  \--change-source                    Changes an IP source

  \--remove-source                    Removes an IP source from a zone
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 19-2 Common firewall-cmd Options

\

With all the \--add and \--remove options, the \--permanent switch may
be specified to ensure the rule is stored in the zone configuration file
under the /etc/firewalld/zones directory for persistence. Some of the
options from Table 19-2 are used in the upcoming exercises; the rest are
beyond the scope of this book. Consult the manual pages of the command
for details on the usage of these and other options.

::: {style="page-break-before: always;"}
:::

[]{#chapter0572.html}

## Querying the Operational Status of firewalld {.style3}

\

You can check the running status of the firewalld service using either
the systemctl or the firewall-cmd command. Both commands will produce
different outputs, but the intent here is to ensure the service is in
the running state.

\

<div>

![](image-5SCTOSWV.jpg){height="100%"}

</div>

The output indicates that the firewalld service is in the running state
on server10. The other command outcome also reports that the service is
marked for autostart at system reboots. In case firewalld is not enabled
or is inactive, issue sudo systemctl \--now enable firewalld to start it
immediately, and mark it for autostart on reboots.

\

You are ready to perform the exercises presented next.

::: {style="page-break-before: always;"}
:::

[]{#chapter0573.html}

## Exercise 19-1: Add Services and Ports, and Manage Zones {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will determine the current active zone. You will
add and activate a permanent rule to allow HTTP traffic on port 80, and
then add a runtime rule for traffic intended for TCP port 443 (the HTTPS
service). You will add a permanent rule to the internal zone for TCP
port range 5901 to 5910. You will confirm the changes and display the
contents of the affected zone files. Lastly, you will switch the default
zone to the internal zone and activate it.

\

1\. Determine the name of the current default zone:

\

<div>

![](image-WEEG8L06.jpg){height="100%"}

</div>

2\. Add a permanent rule to allow HTTP traffic on its default port:

\

<div>

![](image-X0KNQ04K.jpg){height="100%"}

</div>

The command made a copy of the public.xml file from
/usr/lib/firewalld/zones directory into the /etc/firewalld/zones
directory, and added the rule for the HTTP service.

\

3\. Activate the new rule:

\

<div>

![](image-DWOATQSW.jpg){height="100%"}

</div>

4\. Confirm the activation of the new rule:

\

<div>

![](image-CWFUIVCE.jpg){height="100%"}

</div>

5\. Display the content of the default zone file to confirm the addition
of the permanent rule:

\

<div>

![](image-7HPRCRQP.jpg){height="100%"}

</div>

6\. Add a runtime rule to allow traffic on TCP port 443 and verify:

\

<div>

![](image-IAF208HM.jpg){height="100%"}

</div>

7\. Add a permanent rule to the internal zone for TCP port range 5901 to
5910:

\

<div>

![](image-KGFPOI7H.jpg){height="100%"}

</div>

8\. Display the content of the internal zone file to confirm the
addition of the permanent rule:

\

<div>

![](image-AH8JJ4D4.jpg){height="100%"}

</div>

The firewall-cmd command makes a backup of the affected zone file with a
.old extension whenever an update is made to a zone.

\

9\. Switch the default zone to internal and confirm:

\

<div>

![](image-FHUNPQFX.jpg){height="100%"}

</div>

10\. Activate the rules defined in the internal zone and list the port
range added earlier:

\

<div>

![](image-Q0SD0X6U.jpg){height="100%"}

</div>

This completes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0574.html}

## Exercise 19-2: Remove Services and Ports, and Manage Zones {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will remove the two permanent rules that were
added in Exercise 19-1. You will switch the public zone back as the
default zone, and confirm the changes.

\

1\. Remove the permanent rule for HTTP from the public zone:

\

<div>

![](image-CDVOAQMO.jpg){height="100%"}

</div>

Notice the equal sign (=) used with the \--remove-service option. The
firewall-cmd command supports the specification of add, remove, change,
and zone options with and without an equal sign (=). The \--zone option
is used to specify the public zone as it is currently not the default.

\

2\. Remove the permanent rule for ports 5901 to 5910 from the internal
zone:

\

<div>

![](image-2WXYGL5G.jpg){height="100%"}

</div>

The \--zone option is not used, as 'internal' is currently the default
zone.

\

3\. Switch the default zone to public and validate:

\

<div>

![](image-FB7XJGXW.jpg){height="100%"}

</div>

4\. Activate the public zone rules, and list the current services:

\

<div>

![](image-UZOYYK3J.jpg){height="100%"}

</div>

The public zone reflects the removal of the http service. This concludes
the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0575.html}

## Exercise 19-3: Test the Effect of Firewall Rule {.style3}

\

This exercise should be done on server10 and server20 as user1 with sudo
where required.

\

In this exercise, you will remove the sshd service rule from the runtime
configuration on server10, and try to access the server from server20
using the ssh command.

\

1\. Remove the rule for the sshd service on server10:

\

<div>

![](image-NOWQA9XK.jpg){height="100%"}

</div>

2\. Issue the ssh command on server20 to access server10:

\

<div>

![](image-YGXLCZR7.jpg){height="100%"}

</div>

The error displayed is because the firewall on server10 blocked the
access. Put the rule back on server10 and try to access it from server20
again:

\

3\. Add the rule back for sshd on server10:

\

<div>

![](image-QTJSC8LG.jpg){height="100%"}

</div>

4\. Issue the ssh command on server20 to access server10. Enter "yes" if
prompted and the password for user1.

\

<div>

![](image-O6909C0F.jpg){height="100%"}

</div>

This brings the exercise to an end.

::: {style="page-break-before: always;"}
:::

[]{#chapter0576.html}

## Chapter Summary {.style3}

\

We discussed a native host-based firewall solution for system protection
in this chapter. We explored the concepts around firewall and described
how it works. We looked at the firewalld service and examined the
concepts of zones and services. We reviewed predefined zones and
services, and analyzed their configuration files. We studied the lone
firewall management command and reviewed options for listing and
administering zones, services, ports, network connections, and source IP
addresses.

\

We learned how to change and check the operational state of the
firewalld service. We performed exercises to add and remove services and
ports persistently and non-persistently, and manage zones. Finally, we
tested the effect of deleting a port from the firewall configuration and
adding it back.

::: {style="page-break-before: always;"}
:::

[]{#chapter0577.html}

## Review Questions {.style3}

\

1\. A firewall can be configured between two networks but not between
two hosts. True or False?

2\. After changing the default firewalld zone to internal, what would
you run to verify?

3\. What is the process of data packet formation called?

4\. What would the command firewall-cmd \--remove-port=5000/tcp do?

5\. What is the primary command line tool for managing firewalld called?

6\. What would the command firewall-cmd \--permanent \--add-service=nfs
\--zone=external do?

7\. If you have a set of firewall rules defined for a service stored
under both /etc/firewalld and /usr/lib/firewalld directories, which of
the two sets will take precedence?

8\. What is the kernel module in RHEL 9 that implements the host-level
protection called?

9\. firewalld is the firewall management solution in RHEL 9. True or
False?

10\. Which directory stores the configuration file for modified
firewalld zones?

11\. Name the default firewalld zone.

12\. What is the purpose of firewalld service configuration files?

::: {style="page-break-before: always;"}
:::

[]{#chapter0578.html}

## Answers to Review Questions {.style3}

\

1\. False. A firewall can also be configured between two host computers.

2\. You run firewall-cmd \--get-default-zone for validation.

3\. The process of data packet formation is called encapsulation.

4\. The command provided will remove the runtime firewall rule for TCP
port 5000.

5\. The primary command line tool for managing firewalld is called
firewall-cmd.

6\. The command provided will add the nfs service to external firewalld
zone persistently.

7\. The ruleset located in the /etc/firewalld directory will have
precedence.

8\. The kernel module that implements the host-level protection is
called netfilter.

9\. True.

10\. The modified firewalld zone files are stored under
/etc/firewalld/zones directory.

11\. The default firewalld zone is the public zone.

12\. firewalld service configuration files store service-specific port,
protocol, and other details, which makes it easy to activate and
deactivate them.

::: {style="page-break-before: always;"}
:::

[]{#chapter0579.html}

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

[]{#chapter0580.html}

## Lab 19-1: Add Service to Firewall {.style3}

\

As user1 with sudo on server30, add and activate a permanent rule for
HTTPs traffic to the default zone. Confirm the change by viewing the
zone's XML file and running the firewall-cmd command. (Hint: Firewall
Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0581.html}

## Lab 19-2: Add Port Range to Firewall {.style3}

\

As user1 with sudo on server30, add and activate a permanent rule for
the UDP port range 8000 to 8005 to the trusted zone. Confirm the change
by viewing the zone's XML file and running the firewall-cmd command.
(Hint: Firewall Management).

::: {style="page-break-before: always;"}
:::

[]{#chapter0582.html}







