

### Networking, Network Devices, and Network Connections {.style3}

\

::: {style="border-style: double; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.375;"}
:::

\

#### This chapter describes the following major topics:

\

Overview of basic networking concepts: hostname, IPv4, network classes,
subnetting, subnet mask, CIDR, protocol, TCP/UDP, well-known ports,
ICMP, Ethernet address, IPv6, IPv4/IPv6 differences, consistent device
naming, etc.

\

Change hostname of the system

\

Understand the concepts of network device and connection

\

Anatomy of a network connection profile

\

Know network device and connection management tools and techniques

\

Configure network connections by hand and using commands

\

Describe the hosts table

\

Test network connectivity using hostname and IP address

\

#### RHCSA Objectives:

\

##### 44. Configure IPv4 and IPv6 addresses

::: {style="page-break-before: always;"}
:::

\

Acomputer network is formed when two or more physical or virtual
computers are connected together for sharing resources and data. The
computers may be linked via wired or wireless means, and a device such
as a switch is used to interconnect several computers to allow them to
communicate with one another on the network. There are numerous concepts
and terms that need to be grasped in order to work effectively and
efficiently with network device and network connection configuration and
troubleshooting, and several other network services. This chapter
provides a wealth of that information.

\

::: {style="text-align: center;"}
![](image-ERRJFIPY.jpg){height="100%"}
:::

For a system to be able to talk to other systems, one of its network
devices must have a connection profile attached containing a unique IP
address, hostname, and other essential network parameters. The network
assignments may be configured statically or obtained automatically from
a DHCP server. Few files are involved in the configuration, which may be
modified by hand or using commands. Testing follows the configuration to
confirm the system's ability to communicate.

::: {style="page-break-before: always;"}
:::

[]{#chapter0464.html}

## Networking Fundamentals {.style3}

\

The primary purpose of computer networks is to allow users to share data
and resources. A simple network is formed when two computers are
interconnected. Using a networking device such as a switch, this network
can be expanded to include additional computers, as well as printers,
scanners, storage, and other devices (collectively referred to as nodes
or entities). A computer on the network can be configured to act as a
file server, storage server, or as a gateway to the Internet for the
rest of the networked computers. Nodes may be interconnected using wired
or wireless means. A corporate network may have thousands of nodes
linked via a variety of data transmission media. The Internet is the
largest network of networks with millions of nodes interconnected.

\

There are many elementary concepts and terms that you need to grasp
before being able to configure network interfaces, connection profiles,
and client/server setups that are elaborated in this and other chapters.
As well, there are many configuration files and commands related to
various network services that you need to understand thoroughly in order
to manage a RHEL-based environment effectively. Some of the concepts,
terms, configuration files, and commands are explained in this chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0465.html}

## Hostname {.style3}

\

A hostname is a unique alphanumeric label (the hyphen (-), underscore
(\_), and period (.) characters are also allowed) that is assigned to a
node to identify it on the network. It can consist of up to 253
characters. It is normally allotted based on the purpose and principal
use of the system. In RHEL, the hostname is stored in the /etc/hostname
file.

\

The hostname can be viewed with several different commands, such as
hostname, hostnamectl, uname, and nmcli, as well as by displaying the
content of the /etc/hostname file. Let's run these commands on server1:

\

<div>

![](image-H5CRP5OT.jpg){height="100%"}

</div>

All the above commands displayed the same output.

::: {style="page-break-before: always;"}
:::

[]{#chapter0466.html}

## Exercise 15-1: Change System Hostname {.style3}

\

This exercise should be done on both server1 and server2 as user1 with
sudo where required.

\

In this exercise, you will change the hostnames of both lab servers
persistently. You will rename server1.example.com to
server10.example.com by editing a file and restarting the corresponding
service daemon. You will rename server2.example.com to
server20.example.com using a command. You will validate the change on
both systems.

\

On server1:

\

1\. Open the /etc/hostname file in a text editor and change the current
entry to the following:

\

<div>

![](image-QP2K26GE.jpg){height="100%"}

</div>

2\. Execute the systemctl command to restart the systemd-hostnamed
service and verify the new hostname with the hostname command:

\

<div>

![](image-W43WEV1X.jpg){height="100%"}

</div>

3\. To view the reflection of the new hostname in the command prompt,
log off and log back in as user1. The new prompt will look like:

\

<div>

![](image-YEUTYO6N.jpg){height="100%"}

</div>

\

On server2:

\

1\. Execute the hostnamectl command to change the hostname to
server20.example.com:

\

<div>

![](image-6YWIE1SY.jpg){height="100%"}

</div>

2\. To view the reflection of the new hostname in the command prompt,
log off and log back in as user1. You can also use the hostname command
to view the new name.

\

<div>

![](image-5E8TDXP3.jpg){height="100%"}

</div>

You can also change the system hostname using the nmcli command. For
instance, you could have used nmcli general hostname
server20.example.com to rename server2.example.com. The nmcli command is
explained in detail later in this chapter.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You need to know only one of the available methods to change
the system hostname.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

Going forward, you will be using the new hostnames server10 and
server20.

::: {style="page-break-before: always;"}
:::

[]{#chapter0467.html}

## IPv4 Address

\

IPv4 stands for Internet Protocol version 4 and represents a unique
32-bit software address that every single entity on the network must
have in order to communicate with other entities. It was the first
version of IP that was released for public use. IPv4 addresses are also
referred to as dotted-quad addresses, and they can be assigned on a
temporary or permanent basis. Temporary addresses are referred to as
dynamic addresses and are typically leased from a DHCP server for a
specific period of time. Permanent addresses, on the other hand, are
called static addresses and they are manually set.

\

You can use the ip command with the addr argument to view the current IP
assignments on the system. Let's run this command on server10 and see
what it returns:

\

<div>

![](image-DC5CHQGL.jpg){height="100%"}

</div>

The output indicates one configured network connection (number 2 above)
called enp0s3 with IPv4 address 192.168.0.110 assigned to it. The other
connection (number 1 above), represented as lo, is a special purpose
software device reserved for use on every Linux system. Its IPv4 address
is always 127.0.0.1, and it is referred to as the system's loopback (or
localhost) address. Network programs and applications that communicate
with the local system employ this hostname.

::: {style="page-break-before: always;"}
:::

[]{#chapter0468.html}

## Classful Network Addressing {.style3}

\

An IPv4 address is comprised of four period-separated octets (4 x 8 =
32-bit address) that are divided into a network portion (or network
ID/bits) comprising of the Most Significant Bits (MSBs) and a node
portion (or node/host ID/bits) containing the Least Significant Bits
(LSBs). The network portion identifies the correct destination network,
and the node portion represents the correct destination node on that
network. Public network addresses are classified into three categories:
class A, class B, and class C. Private network addresses are classified
into two categories: class D and class E. Class D addresses are
multicast and they are employed in special use cases only. Class E
addresses are experimental and are reserved for future use.

\

### Class A {.style3}

Class A addresses are used for large networks with up to 16 million
nodes. This class uses the first octet as the network portion and the
rest of the octets as the node portion. The total number of usable
network and node addresses can be up to 126 and 16,777,214,
respectively. The network address range for class A networks is between
0 and 126. See an example below of a random class A IP address, which
also shows two reserved addresses:

\

  ----------------------------------- -----------------------------------
  10.121.51.209                       (class A IP address)

  10.121.51.0                         (network address)

  10.121.51.255                       (broadcast address)
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

The 0 and 255 (highlighted) are network and broadcast addresses, and
they are always reserved.

\

### Class B {.style3}

Class B addresses are used for mid-sized networks with up to 65 thousand
nodes. This class employs the first two octets as the network portion
and the other two as the node portion. The total number of usable
network and node addresses can be up to 16,384 and 65,534, respectively.
The network address range for class B networks is between 128 and 191.
See an example below of a random class B IP address, which also shows
two reserved addresses:

\

  ----------------------------------- -----------------------------------
  161.121.51.209                      (class B IP address)

  161.121.51.0                        (network address)

  161.121.51.255                      (broadcast address)
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

The 0 and 255 (highlighted) are network and broadcast addresses, and
they are always reserved.

\

### Class C {.style3}

Class C addresses are employed for small networks with up to 254 nodes.
This class uses the first three octets as the network portion and the
last octet as the node portion. The total number of usable network and
node addresses can be up to 2,097,152 and 254, respectively. The network
address range for class C networks is between 192 and 223. See an
example below of an arbitrary class C IP address, which also shows two
reserved addresses:

\

  ----------------------------------- -----------------------------------
  215.121.51.209                      (class C IP address)

  215.121.51.0                        (network address)

  215.121.51.255                      (broadcast address)
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

The 0 and 255 (highlighted) are network and broadcast addresses, and
they are always reserved.

\

### Class D {.style3}

Class D addresses range from 224 to 239.

\

### Class E {.style3}

Class E addresses range from 240 to 255.

::: {style="page-break-before: always;"}
:::

[]{#chapter0469.html}

## Subnetting {.style3}

\

Subnetting is a technique by which a large network address space is
divided into several smaller and more manageable logical subnetworks,
referred to as subnets. Subnetting results in reduced network traffic,
improved network performance, and de-centralized and easier
administration, among other benefits. Subnetting does not touch the
network bits; it uses the node bits only.

\

The following should be kept in mind when dealing with subnetting:

\

Subnetting results in the reduction of usable addresses.

\

All nodes in a given subnet have the same subnet mask.

\

Each subnet acts as an isolated network and requires a router to talk to
other subnets.

\

The first and the last IP address in a subnet are reserved. The first
address points to the subnet itself, and the last address is the
broadcast address.

::: {style="page-break-before: always;"}
:::

[]{#chapter0470.html}

## Subnet Mask {.style3}

\

A subnet mask or netmask is the network portion plus the subnet bits. It
segregates the network bits from the node bits. It is used by routers to
pinpoint the start and end of the network/subnet portion and the start
and end of the node portion for a given IP address.

\

The subnet mask, like an IP address, can be represented in either
decimal or binary notation. The 1s in the subnet mask isolate the subnet
bits from the node bits that contain 0s. The default subnet masks for
class A, B, and C networks are 255.0.0.0, 255.255.0.0, and
255.255.255.0, respectively.

\

To determine the subnet address for an arbitrary IP address, such as
192.168.12.72 with netmask 255.255.255.224, write the IP address in
binary format. Then write the subnet mask in binary format with all
network and subnet bits set to 1 and all node bits set to 0. Then
perform a logical AND operation. For each matching 1 you get a 1,
otherwise you get a 0. The following highlights the ANDed bits:

\

<div>

![](image-S525VJKR.jpg){height="100%"}

</div>

This calculation enables you to ascertain the subnet address from a
given IP and subnet mask.

::: {style="page-break-before: always;"}
:::

[]{#chapter0471.html}

## Classless Network Addressing {.style3}

\

Classless Inter-Domain Routing (CIDR) is a technique designed to control
the quick depletion of IPv4 addresses and the rapid surge in the number
of routing tables required to route IPv4 traffic on the network and the
Internet. This technique was introduced as a substitute for the classful
scheme, which was not scalable and had other limitations. Using CIDR,
IPv4 addresses can be allocated in custom blocks suitable for networks
of all sizes. This technique has resulted in smaller and less cluttered
routing tables. CIDR was originally designed to address IPv4 needs;
however, it has been extended to support IPv6 as well.

\

An IPv4 address written in CIDR notation has a leading forward slash (/)
character followed by the number of routing bits. A sample IP address of
192.168.0.20 with the default class C subnet mask of 255.255.255.0 will
be written as 192.168.0.20/24. This notation presents a compact method
of denoting an IP address along with its subnet mask.

::: {style="page-break-before: always;"}
:::

[]{#chapter0472.html}

## Protocol {.style3}

\

A protocol is a set of rules governing the exchange of data between two
network entities. These rules include how data is formatted, coded, and
controlled. The rules also provide error handling, speed matching, and
data packet sequencing. In other words, a protocol is a common language
that all nodes on the network speak and understand. Protocols are
defined in the /etc/protocols file. An excerpt from this file is
provided below:

\

<div>

![](image-E7431CE3.jpg){height="100%"}

</div>

Column 1 in the output lists the name of a protocol, followed by the
associated port number, alias, and a short description in columns 2, 3,
and 4.

\

Some common protocols are TCP, UDP, IP, and ICMP.

::: {style="page-break-before: always;"}
:::

[]{#chapter0473.html}

## TCP and UDP Protocols {.style3}

\

TCP (Transmission Control Protocol) and UDP (User Datagram Protocol)
protocols are responsible for transporting data packets between network
entities. TCP is reliable, connection-oriented, and point-to-point. It
inspects for errors and sequencing upon a packet's arrival on the
destination node, and returns an acknowledgement to the source node,
establishing a point-to-point connection with the peer TCP layer on the
source node. If the packet is received with an error or if it is lost in
transit, the destination node requests a resend of the packet. This
ensures guaranteed data delivery and makes TCP reliable. Due to its
reliability and connection-oriented nature, TCP is widely implemented in
network applications.

\

UDP, in contrast, is unreliable, connectionless, and multi-point. If a
packet is lost or contains errors upon arrival at the destination, the
source node is unaware of it. The destination node does not send an
acknowledgment back to the source node. A common use of this protocol is
in broadcast-only applications where reliability is not sought.

::: {style="page-break-before: always;"}
:::

[]{#chapter0474.html}

## Well-Known Ports {.style3}

\

Both TCP and UDP use ports for data transmission between a client and
its server program. Ports are either well-known or private. A well-known
port is reserved for an application's exclusive use, and it is
standardized across all network operating systems. Well-known ports are
defined in the /etc/services file, an excerpt of which is presented
below:

\

<div>

![](image-CPHWPC0K.jpg){height="100%"}

</div>

Column 1 lists the official name of a network service, followed by the
port number and transport layer protocol the service uses, optional
aliases, and comments in successive columns.

\

Some common services and the ports they listen on are FTP (File Transfer
Protocol) 21, SSH (Secure Shell) 22, SMTP (Simple Mail Transfer
Protocol) 25, DNS (Domain Name System) 53, HTTP (HyperText Transfer
Protocol) 80, NTP (Network Time Protocol) 123, secure HTTP (HyperText
Transfer Protocol Secure) 443, and rsyslog 514.

\

A private port, on the other hand, is an arbitrary number generated when
a client application attempts to establish a communication session with
its server process. This port number no longer exists after the session
has ended.

::: {style="page-break-before: always;"}
:::

[]{#chapter0475.html}

## ICMP Protocol {.style3}

\

The Internet Control Message Protocol (ICMP) is a key protocol. It is
primarily used for testing and diagnosing network connections. Commands
such as ping uses this protocol to send a stream of messages to remote
network devices to examine their health and report statistical and
diagnostic information. The report includes the number of packets
transmitted, received, and lost; a round-trip time for individual
packets with an overall average; a percentage of packets lost during the
communication; and so on. See a sample below that shows two packets
(-c2) sent from server10 to the IP address of server20:

\

<div>

![](image-JL8F9TOU.jpg){height="100%"}

</div>

Other commands, such as traceroute, also employ this protocol for route
determination and debugging between network entities. The IPv6 version
of ICMP is referred to as ICMPv6 and it is used by tools such as ping6
and tracepath6.

::: {style="page-break-before: always;"}
:::

[]{#chapter0476.html}

## Ethernet Address {.style3}

\

An Ethernet address represents an exclusive 48-bit address that is used
to identify the correct destination node for data packets transmitted
from the source node. The data packets include hardware addresses for
the source and the destination node. The Ethernet address is also
referred to as the hardware, physical, link layer, or MAC address.

\

You can use the ip command to list all network interfaces available on
the system along with their Ethernet addresses:

\

<div>

![](image-2F9CISML.jpg){height="100%"}

</div>

IP and hardware addresses work hand in hand, and a combination of both
is critical to identifying the correct destination node on the network.
A network protocol called Address Resolution Protocol (ARP) is used to
enable IP and hardware addresses to work in tandem. ARP determines the
hardware address of the destination node when its IP address is known.

::: {style="page-break-before: always;"}
:::

[]{#chapter0477.html}

## IPv6 Address

\

With the explosive growth of the Internet, the presence of an extremely
large number of network nodes requiring an IP, and an ever-increasing
demand for additional addresses---the conventional IPv4 address space,
which provides approximately 4.3 billion addresses---has been exhausted.
To meet the future demand, a new version of IP is now available and its
use is expanding. This new version is referred to as IPv6 (IP version 6)
or IPng (IP next generation). By default, IPv6 is enabled in RHEL 9 on
all configured network connections.

\

IPv6 is a 128-bit software address, providing access to approximately
340 undecillion (340 followed by 36 zeros) addresses. This is an
extremely large space, and it is expected to fulfill the IP requirements
for several decades to come.

\

IPv6 uses a messaging protocol called Neighbor Discovery Protocol (NDP)
to probe the network to discover neighboring IPv6 devices, determine
their reachability, and map their associations. This protocol also
includes enhanced functionalities (provided by ICMP and ARP on IPv4
networks) for troubleshooting issues pertaining to connectivity, address
duplication, and routing.

\

Unlike IPv4 addresses, which are represented as four dot-separated
octets, IPv6 addresses contain eight colon-separated groups of four
hexadecimal numbers. A sample IPv6 would be
2001:1970:5383:4b00:a00:27ff:fe5f:fd43/64. It looks a bit daunting at
first sight, but there are methods that will simplify their
representation.

\

The ip addr command also shows IPv6 addresses for the interfaces:

\

<div>

![](image-YG09ZPGB.jpg){height="100%"}

</div>

It returns two IPv6 addresses. The first one belongs to the loopback
interface, and the second one is assigned to the enp0s3 connection.

::: {style="page-break-before: always;"}
:::

[]{#chapter0478.html}

## Major Differences between IPv4 and IPv6 {.style3}

\

There are a number of differences between IPv4 and IPv6 protocols. Some
of the major ones are highlighted in Table 15-1.

\

  ----------------------------------- -----------------------------------
  IPv4                                IPv6

  Uses 4x8-bit, period-separated      Uses 8x16-bit, colon-separated
  decimal number format for address   hexadecimal number format for
  representation.                     address representation.

  Example: 192.168.0.100              Example: fe80::a00:27ff:feae:f35b

  Number of address bits: 32          Number of address bits: 128

  Maximum number of addresses: \~4.3  Maximum number of addresses:
  billion.                            virtually unlimited

  Common testing and troubleshooting  Common testing and troubleshooting
  tools: ping, traceroute, tracepath, tools: ping6, traceroute6,
  etc.                                tracepath6, etc.

  Support for IP autoconfiguration:   Support for IP autoconfiguration:
  no                                  yes

  Packet size: 576 bytes              Packet size: 1280 bytes
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 15-1 IPv4 vs IPv6

\

These and other differences not listed here are due to enhancements and
new features added to IPv6.

::: {style="page-break-before: always;"}
:::

[]{#chapter0479.html}

## Network Devices and Connections {.style3}

\

Network Interface Cards (NICs) are hardware adapters that provide one or
more Ethernet ports for network connectivity. NICs may also be referred
to as network adapters and individual ports as network interfaces or
network devices. NICs may be built-in to the system board or are add-on
adapters. They are available in one, two, and four port designs on a
single adapter.

\

Individual interfaces (devices) can have one or more connection profiles
attached to them with different configuration settings. Each connection
profile has a unique name and includes settings such as the device name,
UUID, hardware address, IP address, and so on. A connection profile can
be configured by editing files or using commands. A device can have
multiple connection profiles attached, but only one of them can be
active at a time.

::: {style="page-break-before: always;"}
:::

[]{#chapter0480.html}

## Consistent Network Device Naming {.style3}

\

In RHEL versions 6 and earlier, network interfaces used eth (Ethernet),
em (embedded), and wlan (wireless lan) naming and were numbered 0 and
onwards as the interfaces were discovered during a system boot. This was
the default scheme that had been in place for network device naming for
years. Given multiple interfaces located onboard and on add-on NICs, the
number assignments could possibly change on the next boot due to
failures or errors in their detection, which could possibly result in
connectivity and operational issues.

\

As of RHEL 7, the default naming scheme has been augmented to base on
several rules governed by a service called udevd. The default ruleset is
to assign names using the device's location and topology, and the
setting in firmware. The underlying virtualization layer (VMware,
VirtualBox, KVM, Hyper-V) also plays a role in the naming. Some sample
device names are enp0s3, ens160, etc.

\

This advanced ruleset has resulted in consistent and predictable naming,
eliminating the odds of reenumeration during a hardware rescan.
Moreover, the designated names are not affected by the addition or
removal of interface cards. This naming scheme helps in identifying,
configuring, troubleshooting, and replacing the right adapter without
hassle.

::: {style="page-break-before: always;"}
:::

[]{#chapter0481.html}

## Exercise 15-2: Add Network Devices to server10 and server20 {.style3}

\

This exercise will add one network interface to server10 and one to
server20 using VirtualBox.

\

In this exercise, you will shut down server10 and server20. You will
launch VirtualBox Manager and add one network interface to server10 and
one to server20. You will power on both servers and confirm new
interfaces.

\

1\. Execute sudo shutdown now on server10.

2\. Start VirtualBox on your Windows/Mac computer and highlight the
RHEL9-VM1 virtual machine.

3\. Click Settings at the top and then Network on the window that pops
up. Click on "Adapter 2" and check the "Enable Network Adapter" box.
Select "Internal Network" from the drop down list next to "Attached to".
See Figure 15-1.

\

::: {style="text-align: center;"}
![](image-908NCBCE.jpg){height="100%"}
:::

Figure 15-1 VirtualBox Manager \| Add Network Interface

\

4\. Click OK to return to the main VirtualBox interface.

5\. Power on RHEL9-VM1 to boot RHEL 9 in it.

6\. When the server is up, log on as user1 and run the ip command to
verify the new interface:

\

<div>

![](image-BZSQYGEE.jpg){height="100%"}

</div>

The output reveals a new network device called enp0s8. This is the
interface that you just added to the VM.

\

7\. Repeat steps 1 through 6 to add a network interface to server20 and
verify.

\

This completes the addition of new network interfaces to server10 and
server20. You are now ready to use them in the upcoming exercises.

::: {style="page-break-before: always;"}
:::

[]{#chapter0482.html}

## The NetworkManager Service {.style3}

\

NetworkManager is the default interface and connection configuration,
administration, and monitoring service used in RHEL 9. This service has
a daemon program called NetworkManager, which is responsible for keeping
available interfaces and connections up and active. It offers a powerful
command line tool called nmcli to manage interfaces and connections, and
to control the service. This utility offers many options for their
effective management. The NetworkManager service also furnishes a
text-based interface called nmtui and a graphical equivalent called
nm-connection-editor that you may use in lieu of nmcli.

::: {style="page-break-before: always;"}
:::

[]{#chapter0483.html}

## Understanding Interface Connection Profile {.style3}

\

Each network connection has a configuration file that defines IP
assignments and other relevant parameters for it. The networking
subsystem reads this file and applies the settings at the time the
connection is activated. Connection configuration files (or connection
profiles) are stored in a central location under the
/etc/NetworkManager/system-connections directory. The filenames are
identified by the interface connection names with nmconnection as the
extension. Some instances of connection profiles are
enp0s3.nmconnection, ens160.nmconnection, and em1.nmconnection.

\

On server10 and server20, the device name for the first interface is
enp0s3 with connection name enp0s3 and relevant connection information
stored in the enp0s3.nmconnection file. This connection was established
at the time of RHEL installation. The current content of the file from
server10 are presented below:

\

<div>

![](image-I9WYVULT.jpg){height="100%"}

</div>

The file has multiple sections. Each section defines a set of networking
properties for the connection. The output above shows five
sections---connection, ethernet, ipv4, ipv6, and proxy. There are no
settings under ethernet and proxy. The other three have a few properties
defined and they are outlined in Table 15-2 in the order in which they
are listed.

\

  ----------------------------------- -----------------------------------
  Property                            Description

  id                                  Any description given to this
                                      connection. The default matches the
                                      interface name.

  uuid                                The UUID associated with this
                                      connection

  type                                Specifies the type of this
                                      connection

  autoconnect-priority                If the connection is set to
                                      autoconnect, connections with
                                      higher priority will be preferred.
                                      A higher number means higher
                                      priority. The range is between -999
                                      and 999 with 0 being the default.

  interface_name                      Specifies the device name for the
                                      network interface

  timestamp                           The time, in seconds since the Unix
                                      Epoch that the connection was last
                                      activated successfully. This field
                                      is automatically populated each
                                      time the connection is activated.

  address1/method                     Specifies the static IP for the
                                      connection if the method property
                                      is set to manual. /24 represents
                                      the subnet mask.

  addr-gen-mode/method                Generates an IPv6 address based on
                                      the hardware address of the
                                      interface.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 15-2 Network Connection Configuration Directives

\

There are hundreds of other properties that may be defined in connection
profiles depending on the type of interface. Run man nm-settings for a
description of additional properties.

::: {style="page-break-before: always;"}
:::

[]{#chapter0484.html}

## Network Device and Connection Administration Tools {.style3}

\

There are a few tools and methods available for configuring and
administering network interfaces, connections, and connection profiles.
The NetworkManager service includes a toolset for this purpose as well.
Let's take a quick look at the basic management tools in Table 15-3.

\

  ----------------------------------- -----------------------------------
  Command                             Description

  ip                                  A powerful and versatile tool for
                                      displaying, monitoring, and
                                      managing interfaces, connections,
                                      routing, traffic, etc.

  nmcli                               Creates, updates, deletes,
                                      activates, and deactivates a
                                      connection profile.
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 15-3 Network Interface Management Tools

\

You can manually create a connection profile and attach it to a network
device. Many Linux administrators prefer this approach. RHEL also offers
an alternative method for this purpose, which is discussed later in this
chapter.

\

The ifup, ifdown, and ifconfig commands, and storing interface profiles
in the /etc/sysconfig/network-scripts directory are deprecated and
should not be used anymore. The NetworkManager service and associated
tools are the replacements.

\

In Exercise 15-3, you'll use the manual method to configure a connection
profile for a new network device that was added in Exercise 15-2 and
employ the tools listed in Table 15-3.

::: {style="page-break-before: always;"}
:::

[]{#chapter0485.html}

## The nmcli Command {.style3}

\

nmcli is a NetworkManager command line tool that is employed to create,
view, modify, remove, activate, and deactivate network connections, and
to control and report network device status. It operates on seven
different object categories, with each category supporting several
options to form a complete command. The seven categories are general,
networking, connection, device, radio, monitor, and agent. This
discussion only focuses on the connection and device object categories.
They are described in Table 15-4 along with management operations that
they can perform.

\

  ----------------------------------- -----------------------------------
  Object                              Description

  Connection: activates, deactivates, 
  and administers network connections 

  show                                Lists connections

  up / down                           Activates/deactivates a connection

  add                                 Adds a connection

  edit                                Edits an existing connection or
                                      adds a new one

  modify                              Modifies one or more properties of
                                      a connection

  delete                              Deletes a connection

  reload                              Instructs NetworkManager to re-read
                                      all connection profiles

  load                                Instructs NetworkManager to re-read
                                      a connection profile

  Device: displays and administers    
  network interfaces                  

  status                              Exhibits device status

  show                                Displays detailed information about
                                      all or the specified interface
  ----------------------------------- -----------------------------------

::: {style="page-break-before: always;"}
:::

\

Table 15-4 Network Connection and Device Administration Tools

\

Object categories and the objects within them may be written in an
abridged form to save typing. For instance, the connection category may
be abbreviated as a "c" or "con" and the device category as a "d" or
"dev". The same rule applies to object names as well. For instance, add
may be specified as an "a", delete as a "d", and so on. Check the manual
pages for nmcli-examples.

\

The nmcli command supports tab completion to make its use easier. Let's
run a few examples on server10 to understand the command's usage.

\

To show (s) all available connections (c) including both active and
inactive:

\

<div>

![](image-FEGVOF1H.jpg){height="100%"}

</div>

The output lists two connection profiles (NAME) and the devices (DEVICE)
they are attached to. It also shows their UUID and type.

\

To deactivate (down) the connection (c) enp0s8:

\

<div>

![](image-OGXVUNJ2.jpg){height="100%"}

</div>

The connection profile is detached from the device, disabling the
connection. You can check with nmcli c s.

\

To activate (up) the connection (c) enp0s8:

\

<div>

![](image-BBQZ027O.jpg){height="100%"}

</div>

The connection profile is reattached to the device, enabling the
connection. You can check with nmcli c s.

\

To display the status (s) of all available network devices (d):

\

<div>

![](image-7QIY5FAN.jpg){height="100%"}

</div>

The output shows three devices and their types, states, and the
connection profiles attached to them. The loopback interface is not
managed by the NetworkManager service.

::: {style="page-break-before: always;"}
:::

[]{#chapter0486.html}

## Exercise 15-3: Configure New Network Connection Manually {.style3}

\

This exercise should be done on server10 as user1 with sudo where
required.

\

In this exercise, you will create a connection profile for the new
network interface enp0s8 using a text editing tool. You will assign the
IP 172.10.10.110/24 with gateway 172.10.10.1 and set it to autoactivate
at system reboots. You will deactivate and reactivate this interface at
the command prompt.

\

1\. Create a file called enp0s8-nmconnection in the
/etc/NetworkManager/system-connections directory and enter the following
information to establish a connection profile:

\

<div>

![](image-WDSOD3CW.jpg){height="100%"}

</div>

2\. Deactivate and reactivate this interface using the nmcli command:

\

<div>

![](image-EX3VEWYC.jpg){height="100%"}

</div>

3\. Verify the activation of the connection:

\

<div>

![](image-R1P6M917.jpg){height="100%"}

</div>

The new connection profile has been applied to the new network device
enp0s8. The connection is now ready for use. The connectivity to
server10 over this new connection will be tested later in this chapter.

::: {style="page-break-before: always;"}
:::

[]{#chapter0487.html}

## Exercise 15-4: Configure New Network Connection Using nmcli {.style3}

\

This exercise should be done on server20 as user1 with sudo where
required.

\

In this exercise, you will create a connection profile using the nmcli
command for the new network interface enp0s8 that was added to server20
in Exercise 15-2. You will assign the IP 172.10.10.120/24 with gateway
172.10.10.1, and confirm.

\

1\. Check the presence of the new interface:

\

<div>

![](image-ZKNVR3JS.jpg){height="100%"}

</div>

The output signifies the existence of a new network device called
enp0s8. It does not have a connection profile attached at the moment.

\

2\. Add (a) a connection profile (c) and attach it to the new interface.
Use the type Ethernet, device name (ifname) enp0s8 with a matching
connection name (con-name), CIDR (ip4) 172.10.10.120/24, and gateway
(gw4) 172.10.10.1:

\

<div>

![](image-BFAAEYAO.jpg){height="100%"}

</div>

A new connection has been added, attached to the new interface, and
activated. In addition, the command has saved the connection information
in a new file called enp0s8-nmconnection and stored it in the
/etc/NetworkManager/system-connections directory.

\

3\. Confirm the new connection status:

\

<div>

![](image-0MHFB9HV.jpg){height="100%"}

</div>

The output indicates the association of the new connection with the
network device.

\

4\. Check the content of the enp0s8-nmconnection file:

\

<div>

![](image-V49TV5JB.jpg){height="100%"}

</div>

There are a number of default directives added to the connection profile
in addition to the configuration items you entered with the nmcli
command above.

\

5\. Check the IP assignments for the new connection:

\

<div>

![](image-A19ICJSS.jpg){height="100%"}

</div>

The IP is assigned to the interface. The connection will be tested later
in this chapter.

\

This brings the exercise to a conclusion.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: You need to know only one of the available methods to set IP
assignments.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

::: {style="page-break-before: always;"}
:::

[]{#chapter0488.html}

## Understanding Hosts Table {.style3}

\

Each IP address used on the system should have a hostname assigned to
it. In an environment with multiple systems on the network, it is
prudent to have some sort of a hostname to IP address resolution method
in place to avoid typing the destination system IP repeatedly to access
it. DNS is one such method. It is designed for large networks such as
corporate networks and the Internet. For small, internal networks, the
use of a local hosts table (the /etc/hosts file) is also common. This
table is used to maintain hostname to IP mapping for systems on the
local network, allowing us to access a system by simply employing its
hostname. In this book, there are two systems in place:
server10.example.com with IP 192.168.0.110 and alias server10, and
server20.example.com with IP 192.168.0.120 and alias server20. You can
append this information to the /etc/hosts file on both server10 and
server20 as shown below:

\

  ----------------------- ----------------------- -----------------------
  192.168.0.110           server10.example.com    server10

  192.168.0.120           server20.example.com    server20
  ----------------------- ----------------------- -----------------------

::: {style="page-break-before: always;"}
:::

\

Each row in the file contains an IP address in column 1 followed by the
official (or canonical) hostname in column 2, and one or more optional
aliases thereafter. The official hostname and one or more aliases give
users the flexibility of accessing the system using any of these names.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

EXAM TIP: In the presence of an active DNS with all hostnames
resolvable, there is no need to worry about updating the hosts file.

\

::: {style="border-style: solid; border-color: rgb(0, 0, 0); border-top-width: 1px; width: 0.0625;"}
:::

\

As expressed above, the use of the hosts file is common on small
networks, and it should be updated on each individual system to reflect
any changes for best inter-system connectivity experience.

::: {style="page-break-before: always;"}
:::

[]{#chapter0489.html}

## Testing Network Connectivity {.style3}

\

RHEL includes the ping command to examine network connectivity between
two systems. It uses the IP address of the destination system to send a
series of 64-byte Internet Control Message Protocol (ICMP) test packets
to it. A response from the remote system validates connectivity and
health. With the -c option, you can specify the number of packets that
you want transmitted.

\

The following sends two packets from server10 to 192.168.0.120
(server20):

\

<div>

![](image-K8CE63IT.jpg){height="100%"}

</div>

Under "192.168.0.120 ping statistics," the output depicts the number of
packets transmitted, received, and lost. The packet loss should be 0%,
and the round-trip time should not be too high for a healthy connection.
In general, you can use this command to test connectivity with the
system's own IP, the loopback IP (127.0.0.1), a static route, the
default gateway, and any other address on the local or remote network.

\

If a ping response fails, you need to check if the NIC is seated
properly, its driver is installed, network cable is secured
appropriately, IP and netmask values are set correctly, and the default
or static route is accurate.

::: {style="page-break-before: always;"}
:::

[]{#chapter0490.html}

## Exercise 15-5: Update Hosts Table and Test Connectivity {.style3}

\

This exercise should be done on server10 and server20 as user1 with sudo
where required.

\

In this exercise, you will update the /etc/hosts file on server10 and
server20. You will add the IP addresses assigned to both connections and
map them to hostnames server10, server10s8, server20, and server20s8
appropriately. You will test connectivity from server10 to server20 and
from server10s8 to server20s8 using their IP addresses and then their
hostnames.

\

On server20:

\

1\. Open the /etc/hosts file and add the following entries:

\

<div>

![](image-BDOZQLFQ.jpg){height="100%"}

</div>

The IP addresses for both connections are added for both servers.

\

On server10:

\

2\. Open the /etc/hosts file and add the following entries:

\

<div>

![](image-XRVPK61I.jpg){height="100%"}

</div>

The IP addresses for both connections are added for both servers.

\

3\. Send two packets from server10 to the IP address of server20:

\

<div>

![](image-QXTVCQ9J.jpg){height="100%"}

</div>

4\. Issue two ping packets on server10 to the hostname of server20:

\

<div>

![](image-5QK8GN1C.jpg){height="100%"}

</div>

5\. Send one packet from server10 to the IP address of server20s8:

\

<div>

![](image-93A700QQ.jpg){height="100%"}

</div>

6\. Issue one ping packet on server10 to the hostname of server20s8:

\

<div>

![](image-LCDENG3S.jpg){height="100%"}

</div>

Steps 3 through 6 verified the connectivity to the remote server over
both connections. Each server has two IP addresses, and each IP address
has a unique hostname assigned to it.

\

This concludes the exercise.

::: {style="page-break-before: always;"}
:::

[]{#chapter0491.html}

## Chapter Summary {.style3}

\

This chapter discussed the rudiments of networking. It began by
providing an understanding of various essential networking terms and
concepts to build the foundation for networking topics going forward.
Topics such as hostname, IPv4, IPv6, classful and classless network
addressing, subnetting, subnet mask, protocol, port, Ethernet address,
and consistent device naming were covered in sufficient detail.

\

We modified hostnames on both lab servers by modifying a configuration
file and restarting the hostname service on one server and using a
single command on the other. We employed two different methods to
demonstrate multiple ways of doing the same thing. A third method was
also mentioned to rename a hostname.

\

Next, we described the terms network devices and network connections,
and realized the difference between the two. We examined a connection
profile and looked at a number of directives that may be defined for a
network connection. We added a new network device to each lab server and
configured them by employing two different methods. We activated the new
connections and performed a ping test for functional validation. Lastly,
we populated the hosts tables with the IP and hostname mapping on both
lab servers.

::: {style="page-break-before: always;"}
:::

[]{#chapter0492.html}

## Review Questions {.style3}

\

1\. Which service is responsible for maintaining consistent device
naming?

2\. List three key differences between TCP and UDP protocols.

3\. What is the significance of the NAME and DEVICE directives in a
connection profile?

4\. Which class of IP addresses has the least number of node addresses?

5\. Which command can you use to display the hardware address of a
network device?

6\. Define protocol.

7\. Which directory stores the network connection profiles?

8\. True or False. A network device is a physical or virtual network
port and a network connection is a configuration file attached to it.

9\. IPv4 is a 32-bit software address. How many bits does an IPv6
address have?

10\. Which file defines the port and protocol mapping?

11\. What would the command hostnamectl set-hostname host20 do?

12\. Name the file that stores the hostname of the system.

13\. What would the command nmcli cs do?

14\. The /etc/hosts file maintains hostname to hardware address
mappings. True or False?

15\. Which file contains service, port, and protocol mappings?

16\. What would the ip addr command produce?

17\. Which file would you consult to identify the port number and
protocol associated with a network service?

18\. Name four commands that can be used to display the hostname.

19\. List any two benefits of subnetting.

::: {style="page-break-before: always;"}
:::

[]{#chapter0493.html}

## Answers to Review Questions {.style3}

\

1\. The udevd service handles consistent naming of network devices.

2\. TCP is connection-oriented, reliable, and point-to-point; UDP is
connectionless, unreliable, and multi-point.

3\. The NAME directive sets the name for the network connection and the
DEVICE directive defines the network device the connection is associated
with.

4\. The C class supports the least number of node addresses.

5\. The ip command.

6\. A set of rules that govern the exchange of information between two
network entities.

7\. The /etc/NetworkManager/system-connections directory.

8\. True.

9\. 128.

10\. The /etc/protocols file.

11\. The command provided will update the /etc/hostname file with the
specified hostname and restart the systemd-hostnamed daemon for the
change to take effect.

12\. The /etc/hostname file.

13\. The command provided will display the status information for all
network connections.

14\. False. This file maintains hostname to IP address mapping.

15\. The /etc/services file.

16\. This command provided will display information about network
connections including IP assignments and hardware address.

17\. The /etc/services file.

18\. The hostname, uname, hostnamectl, and nmcli commands can be used to
view the system hostname.

19\. Better manageability and less traffic.

::: {style="page-break-before: always;"}
:::

[]{#chapter0494.html}

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

[]{#chapter0495.html}

Lab 15-1: Add New Interface and Configure Connection Profile with nmcli

\

Add a third network interface to RHEL9-VM3 in VirtualBox.

\

As user1 with sudo on server30, run ip a and verify the addition of the
new interface. Use the nmcli command and assign IP 192.168.0.230/24 and
gateway 192.168.0.1. Deactivate and reactivate this connection manually.
Add entry server30-3 to the hosts table. (Hint: Exercise 15-2 and
Exercise 15-4).

::: {style="page-break-before: always;"}
:::

[]{#chapter0496.html}

## Lab 15-2: Add New Interface and Configure Connection Profile Manually {.style3}

\

Add a third network interface to RHEL9-VM4 in VirtualBox.

\

As user1 with sudo on server40, run ip a and verify the addition of the
new interface. Make a copy of the enp0s3.nmconnection file for the new
connection under /etc/NetworkManager/system-connections. Remove the UUID
directive and set CIDR 192.168.0.240/24. Deactivate and reactivate this
connection manually. Add entry server40-3 to the hosts table and run
ping tests to server40-3 and its IP address. (Hint: Exercise 15-2 and
Exercise 15-3).

::: {style="page-break-before: always;"}
:::

[]{#chapter0497.html}


## Networking, Network Devices, and Network Management

---
## Hostname

- "-", "_ ", and ". " characters are allowed.
- Up to 253 characters.
- Stored in /etc/hostname.

View the hostname:
```
hostnamectl --static
```

```
hostname
```

```
uname -n
```

```
cat /etc/hostname
```

## Lab: Change the Hostname

Server1

1. Open /etc/hostname and change the entry to server10.example.com
2. restart the systemd-hostnamed service daemon
```
sudo systemctl restart systemd-hostnamed
```
3. confirm
```
hostname
```

server2

1. Change the hostname with hostnamectl:
```
sudo hostnamectl set-hostname server21.example.com
```
2. Log out and back in for the prompt to update

3. Change the hostname using nmcli
```
nmcli general hostname server20.example.com
```

---
## IPv4
---

View current ipv4 address:
```
ip addr
```

---
## Protocols
---

- Defined in /etc/protocols
- Well known ports are defined in /etc/services

### ICMP

Send two pings to server 20
```
ping -c2 192.168.0.120
```

Ping the server's loopback interface:
```
ping 172.0.0.1
```

Send a traceroute to server 20 
```
traceroute 192.168.0.120
```

```
tracepath
```

### ICMPv6

- IPv6 version of ICMP
- enabled by default

Ping and ipv6 address:
```
ping6 
```

Trace a route to an IPv6 address:
```
tracepath6
```

```
traceroute6
```

Show IPv6 addresses:
```
ip addr | grep inet6
```

## Misc

List all network interfaces with their ethernet addresses:
```
ip addr | grep ether
```

## Connection Profiles

- unique name for each connection profile
- Device can have multiple connection profiles attached
	- Only one active profile per device at a time
- Stored in /etc/sysconfig/network-scripts/
- Filename format: ifcfg~name-of-connection~
- connection from device to profile is established at the time of installation
- Can manually create a connection profile and attach it to a device

### Connection Profile Directives

BOOTPROTO
- boot protocol used
- (dhcp, none, or static)

BROWSER_ONLY
- Works if PROXY_METHOD is set to auto.
- Default is "no"

DEFROUTE
- Whether to use this connection as the default route

DEVICE
- Device name for the network interface

DNS1
- ip or hostname of first DNS server
- Placed in /etc/resolv.conf if PEERDNS is set to "no"

GATEWAY
- Gateway address if BOOTPROTO is set to "none" or "static"

HWADDR
- Hardware address

IPADDR
- Static IP if BOOTPROTO is set to "none" or "static"

IPV4_FAILURE_FATAL
- Disable device if IPv4 configuration fails
- Default is "no"

IPV6INIT
- Enable IPv6 support for this connection

NAME
- Description for the connection
- Default matches device name

NETMASK
- Sets netmask address if BOOTPROTO is set to "none" or "static"

NM_CONTROLLED
- Allows NetworkManager service to modify this connection's config
- Should be turned off for interfaces that use a static ip
- Default is "yes"

ONBOOT
- Auto activate the connection at system boot

PEERDNS
- Tells system to update /etc/rsolv.conf
- Default is "yes" if BOOTPROTO is set to "dhcp"

PREFIX
- Number of subnet bits
- May be used instead of NETMASK

PROXY_METHOD
- Used for proxy setting
- Default is "no"

UUID
- UUID for this connection

TYPE
- Type of connection (Ethernet, Wireless, etc.)

View additional directives:
```
man nm-settings
```

Naming rules for devices are governed by udevd service based on:
- Device location
- Topology
- setting in firmware
- virtualization layer

## Lab: Add Network Devices to server10 and one to server20 using VirtualBox

1. Shut down your servers (follow each step for both servers)
```
sudo shutdown now
```
2. Add network interface in Virtualbox then power on the VMs
```
Select machine > settings > Network > Adapter 2 > Enable Network Adapter > Internal Network > ok
```
3. Verify the new interfaces:
```
ip a
```


## Administration Tools

ip 
- display monitor and manage network interfaces, routing, connections, traffic, etc. 

ifup
- Brings up an interface

ifdown
- Brings down an interface

## Lab: Configure network connection manually (server 10)

1. Create ifcfg-enp0s8 in /etc/sysconfig/network-scripts/ and add the following directives:
```
TYPE=Ethernet
BOOTPROTO=static
DEFROUTE=yes
IPv4_FAILURE_FATAL=no
IPv6INIT=no
NAME=enp0s8
DEVICE=enp0s8
ONBOOT=yes
IPADDR=172.10.10.110
PREFIX=24
GATEWAY=172.10.10.1
```

2. Bounce the interface:
```
sudo ifdown enp0s8
sudo ifup enp0s8
```

3. Verify:
```
ip a
```

## NetworkManager service

Default service in RHEL for network:
- interface and connection configuration.
- Administration.
- Monitoring.

NetworkManager daemon
- Responsible for keeping interfaces and connection up and active.
- Includes:
	- nmcli
	- nmtui (text-based)
	- nm-connection-editor (GUI)
- Does not manage loopback interfaces.

## nmcli command

- Create, view, modify, remove, activate, and deactivate network connections.
- Control and report network device status.
- Supports abbreviation of commands.

Operates on 7 different object categories.
1. general
2. networking
3. connection (c)(con)
4. device (d)(dev)
5. radio
6. monitor
7. agent

### 3. connection
- Activates, deactivates, and administers network connections.

Options:
- show (list connections)
- up/down (Brings connection up or down)
- add(a) (adds a connection)
- edit (edit connection or add a new one)
- modify (modify properties of a connection)
- delete(d) (delete a connection)
- reload (re-read all connection profiles)
- load (re-read a connection profile)

### 4. Device

Options:
- status (Displays device status)
- show (Displays info about device(s)

Show all connections, inactive or active:
```
nmcli c s
```

Deactivate the connection enp0s8:
```
sudo nmcli c down enp0s8
```

Note:
```
The connection profile gets detached from the device, disabling the connection.
```

Activate the connection enp0s8:
```
$ sudo nmcli c up enp0s8
# connection profile re-attaches to the device.
```

Display the status of all network devices:
```
nmcli d s
```

## Lab: Configure New Network Connection Using nmcli (server20)

1. Verify NetworkManager service is running:
```
sudo systemctl status NetworkManager
```

2. Verify the interface that was added from virtualbox:
```
sudo nmcli d status | grep enp
```

3. Add connection profile  and attach it to the interface:
```
sudo nmcli con add type Ethernet ifname enp0s8 con-name enp0s8 ip4 172.10.10.120/24 gw4 172.10.10.1
```

Note:
```
This creates the file for the connection in /etc/sysconfig/network-scripts/
ONBOOT is set to "yes" automatically
```

4. View the content of the connection profile:
```
cat /etc/sysconfig/network-scripts/ifcfg-enp0s8
```

5. Verify ip address
```
ip a
```

6. Deactivate the connection and detach it from the interface:
```
sudo nmcli c down enp0s8
```

7. Verify:
```
nmcli c s
```

8. Reactivate the connection and attach it to the interface:
```
sudo nmcli c up enp0s8
```

9. Verify:
```
nmcli c s
```

## Hosts Table

/etc/hosts

## Lab: Update Hosts Table and Test Connectivity.

1. Add both server10 and server20's interfaces to both server's /etc/host files:
```
192.168.0.110  server10.example.com  server10 <-- This is an alias
192.168.0.120  server20.example.com  server20   
172.10.10.110  server10s8.example.com   server10s8
172.10.10.120  server20s8.example.com   server20s8
```

2. Send 2 packets from server10 to server20's IP address:
```
ping -c2 192.168.0.120
```

3. Send 2 pings from server10 to server20's hostname:
```
ping -c2 server20
```

## Lab: Add New Interface and Configure Connection Profile with nmcli

1. Add a new network interface to server10 in virtualbox
2. Verify the connection's presence.
3. Use nmcli to assign IP 192.168.0.210/24 and gateway 192.168.0.1
4. Set the connection to auto-activate on boot. 
5. Deactivate and reactivate the connection manually.

## Lab: Add New Interface and Configure Connection Profile Manually

1. Add a new network interface to server20 in virtualbox.
2. Verify the connection's presence.
3. Make a copy of /etc/sysconfig/network-scripts/ifcfg-enp0s3 as ifcfg-enp0s8 in the same directory. 
4. Remove HWADDR and UUID directives.
5. Set values for IPADDR, NETMASK, and GATEWAY.
6. Set the connection to auto-activate on boot.
7. Deactivate and reactivate the connection manually.



**[Review]{#part0028_split_001.html#id_460 .calibre10} Questions**

1[.]{.c19}What is the use of *ifup* and *ifdown* commands?

2[.]{.c19}Which service is responsible for maintaining consistent device
naming?

3[.]{.c19}List three key differences between TCP and UDP protocols.

4[.]{.c19}What is the significance of the NAME and DEVICE directives in
a connection profile?

5[.]{.c19}Which class of IP addresses has the least number of node
addresses?

6[.]{.c19}Which command can you use to display the hardware address of a
network device?

7[.]{.c19}Define protocol.

8[.]{.c19}Which directory stores the network connection profiles?

9[.]{.c19}True or False. A network device is a physical or virtual
network port and a network connection is a configuration file attached
to it.

10[.]{.c23}IPv4 is a 32-bit software address. How many bits does an IPv6
address have?

11[.]{.c23}Which file defines the port and protocol mapping?

12[.]{.c23}What would the command *hostnamectl set-hostname host20* do?

13[.]{.c23}Name the file that stores the hostname of the system.

14[.]{.c23}What would the command *nmcli cs* do?

15[.]{.c23}What is the purpose of the ONBOOT directive in the network
connection profile?

16[.]{.c23}The **etc*hosts* file maintains hostname to hardware address
mappings. True or False?

17[.]{.c23}Which file contains service, port, and protocol mappings?

18[.]{.c23}What would the *ip addr* command produce?

19[.]{.c23}Which file would you consult to identify the port number and
protocol associated with a network service?

20[.]{.c23}Adding a connection profile with the *nmcli* command creates
a connection profile in the **etc*sysconfig/network-scripts* directory.
True or False?

21[.]{.c23}Name four commands that can be used to display the system
hostname?

22[.]{.c23}List any two benefits of subnetting.

**[Answers]{#part0028_split_001.html#id_461 .calibre10} to Review
Questions**

1[.]{.c19}The *ifup* and *ifdown* commands are used to enable and
disable a network connection, respectively.

2[.]{.c19}The *udevd* service handles consistent naming of network
devices.

3[.]{.c19}TCP is connection-oriented, reliable, and point-to-point; UDP
is connectionless, unreliable, and multi-point.

4[.]{.c19}The NAME directive sets the name for the network connection
and the DEVICE directive defines the network device the connection is
associated with.

5[.]{.c19}The C class supports the least number of node addresses.

6[.]{.c19}The *ip* command.

7[.]{.c19}A set of rules that govern the exchange of information between
two network entities.

8[.]{.c19}The **etc*sysconfig/network-scripts* directory.

9[.]{.c19}True.

10[.]{.c23}128.

11[.]{.c23}The **etc*protocols* file.

12[.]{.c23}The command provided will update the **etc*hostname* file
with the specified hostname and restart the *systemd-hostnamed* daemon
for the change to take effect.

13[.]{.c23}The **etc*hostname* file.

14[.]{.c23}The command provided will display the status information for
all network connections.

15[.]{.c23}The purpose of the ONBOOT directive is to direct the boot
scripts whether to activate this connection.

16[.]{.c23}False. This file maintains hostname to IP address mapping.

17[.]{.c23}The **etc*services* file.

18[.]{.c23}This command provided will display information about network
connections including IP assignments and hardware address.

19[.]{.c23}The **etc*services* file.

20[.]{.c23}True.

21[.]{.c23}The *hostname*, *uname*, *hostnamectl*, and *nmcli* commands
can be used to view the system hostname.

22[.]{.c23}Better manageability and less traffic.





