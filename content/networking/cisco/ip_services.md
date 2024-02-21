---
title: "IP Services"
date: 2023-11-06T06:20:36-07:00
draft: true
---
3.0 IP Connectivity

3.5 Describe the purpose of First Hop Redundancy Protocol

4.0 Infrastructure Services

4.4 Explain the function of SNMP in network operations

4.9 Describe the capabilities and function of TFTP/FTP in the network

## First Hop Redundancy Protocol

Subnet 10.1.1.0/24 
SW3 
Default 
GW=.9 
SW4 
SWI 
SW2 
.9 
Single Points of Failure 
RI 
Figure 12-1 RI and the One WAN Link as Single Points of Failure ">

Subnet 10. I .1.0/24 
SW3 
Default 
GW=.9 
SW4 
Remote 
Single Points of Failure 
SWI 
SW2 
.9 
R4 
Main Site 
Figure 12-2 Higher Availability but with RI Still as a Single Point of Failure ">

Subnet 10.1.1.0/24 
sw3 1 
Default 
GW=.9 
SW4 1 
SWI 
SW2 1 
GO/O 
.9 
.129 
Figure 12-3 Removing All Single Points ofFailure from the Network Design ">

GW=.9 
GW=.9 
GW=.129 
GW=.129 
GO/O 
.9 
GO/I 
.129 
Figure 124 Balancing Traffic by Assigning Different Default Routers to Different Clients ">

All hosts act like they always have, with one default router setting that never has to change.

The default routers share a virtual IP address in the subnet, defined by the FHRP.

Hosts use the FHRP virtual IP address as their default router address.

The routers exchange FHRP protocol messages so that both agree as to which router does what work at any point in time.

When a router fails or has some other problem, the routers use the FHRP to choose which router takes over responsibilities from the failed router.

The Three Solutions for First-Hop Redundancy

First Hop Redundancy Protocol does not name any one protocol. Instead, it names a family of protocols that fill the same role

acronym 
HSRP 
VRRP 
GLBP 
Full Name 
Hot Standby 
Router Protocol 
Virtual Router 
Redundancy 
Protocol 
Gateway Load 
Balancing 
Protocol 
Origin 
Cisco 
RFC 
5798 
Cisco 
Redundancy 
Approach 
active/standby 
active/standby 
active/active 
Load 
Balancing 
Per... 
subnet 
subnet 
host ">

HSRP Concepts

operates with an active/standby model (also more generally called active/passive

allows two (or more) routers to cooperate

GW=.I 
GW=.I 
Host ARP Table 
MAC 
10.1.1.1 VMACI 
HSRP Active 
.1 
VMACI 
RI 
HSRP 
HSRP Standby 
Figure 12-5 All Traffic Goes to .1 (RI, Which Is Active); R2 Is Standby ">

HSRP Failover

GW=.I 
GW=.I 
GW=.I 
GW=.I 
c 
.9 
vrMC1 
VMACI 
.129 
HSRP Active 
Host ARP Table 
MAC 
No Change 
10.1.1.1 VMACI 
Figure 12-6 Packets Sent Through R2 (New Active) Once It Takes Overfor Failed RI ">

To make the switches change their MAC address table entries for VMAC1, R2 sends an Ethernet frame with VMAC1 as the source MAC address.

he frame is also a LAN broadcast, so all the switches learn a MAC table entry for VMAC1 that leads toward R2.

HSRP Load Balancing

you can configure multiple instances of HSRP in the same subnet (called multiple HSRP groups), preferring one router to be active in one group and the other router to be preferred as active in another.

Subnet 10.1.1.0/24 
SW3 
10.1.2.1 
VLAN 2 
Subnet 10.1.2.0/24 
Active Subnet I 
Standby Subnet 2 
10.1.1.1 
SWI 
HSRP 
RI 
SW2 
10.1.2.1 
Active Subnet 2 
Standby Subnet 1 
F igure 12-7 Load Balancing with HSRP by Using Different Active Routers per Subnet ">

FHRPs are needed on any device that acts as a default router,

includes both traditional routers and Layer 3 switches.

## Simple Network Management Protocol

SNMPv2c and SNMPv3

application layer protocol

provides a message format for communication between what are termed managers and agents

manager

a network management application running on a PC or server

typically being called a Network Management Station (NMS)

uses SNMP protocols to communicate with each SNMP agent.

Cisco Prime series of management products ([www.cisco.com/go/prime](http://www.cisco.com/go/prime)) use SNMP (and other protocols) to manage networks.

agents

exist in the network, one per device that is managed.

software running inside each device (router, switch, and so on), with knowledge of all the variables on that device that describe the device’s configuration, status, and counters.

keeps a database of variables that make up the parameters, status, and counters for the operations of the device. This database, called the Management Information Base (MIB)

IOS on routers and switches include an SNMP agent, with built-in MIB, that can be enabled with the configuration shown later

i.e. Cisco Prime) 
The MB 
The Cisco Router and 
SNMP Agent Software 
Figure 12-8 Elements of Simple Network Management Protocol ">

SNMP Variable Reading and Writing: SNMP Get and Set

NMS typically polls the SNMP agent on each device

NMS can notify the human user in front of the PC or send emails, texts, and so on to notify the network operations staff of any issues identified by the data found by polling the devices. You can even reconfigure the device through these SNMP variables in the MIB if you permit this level of control.

NMS uses the SNMP Get, GetNext, and GetBulk messages (together referenced simply as Get messages) to ask for information from an agent.

NMS sends an SNMP Set message to write variables on the SNMP agent as a means to change the configuration of the device.

messages come in pairs, with, for instance, a Get Request asking the agent for the contents of a variable, and the Get Response supplying that information

o find out if GiO/O is UP/UP 
SNMP Get Request 
The MIB 
Gi0/0 
Router I 
Figure 12-9 SNMP Get Request and Get Response Message Flow ">

NMS can analyze various statistical facts such as averages, minimums, and maximums

NMS can set thresholds for certain key variables, telling the NMS to send a notification (email, text, and so on) when a threshold is passed.

SNMP Notifications: Traps and Informs

SNMP agents can initiate communications to the NMS.

generally called notifications, use two specific SNMP messages: Trap and Inform

SNMP agents send a Trap or Inform SNMP message to the NMS to list the state of certain MIB variables when those variables reach a certain state.

y GiO/O Interface Failed! 
Take a Look! 
SNMP Trap @ 
The MIB 
Router 1 
Figure 12-10 SNMP Trap Notification Process ">

SNMP Traps and Inform messages have the exact same purpose but differ in the protocol mechanisms

trap

The SNMP agent sends the Trap to the IP address of the NMS, with UDP as the transport protocol as with all SNMP messages,

less overhead than inform

Inform

Like Trap messages but with reliability added

Added to the protocol with SNMP Version 2 (SNMPv2),

use UDP but add application layer reliability

NMS must acknowledge receipt of the Inform with an SNMP Response message, or the SNMP agent will time out and resend the Inform.

The Management Information Base

Every SNMP agent has its own Management Information Base

defines variables whose values are set and updated by the agent

enable the management software to monitor/control the network device.

defines each variable as an object ID (OID)

organizes the OIDs based in part on RFC standards, and in part with vendor-proprietary variables

organizes all the variables into a hierarchy of OIDs, usually shown as a tree

Each node in the tree can be described based on the tree structure sequence, either by name or by number.

nternet I 
rivate 4 
enterprises (I) 
Cisco 9 
1.3.6.1.4.1.9.2.2 
1.3.6.1.4.1.9.9.10 
Figure 12-11 Management Information Base (MIB) ">

you could use an SNMP manager and type MIB variable 1.3.6.1.4.1.9.2.1.58.0 and click a button to get that variable, to see the current CPU usage percentage from a Cisco router

Securing SNMP

use ACLs to limit SNMP messages to those from known servers only.

can configure an IPv4 ACL to filter incoming SNMP messages that arrive in IPv4 packets and an IPv6 ACL to filter SNMP messages that arrive in IPv6 packets.

all versions of SNMP support a basic clear-text password mechanism,

SNMPv1 defined clear-text passwords called SNMP communities.

SNMP agent and the SNMP manager need prior knowledge of the same SNMP community value (called a community string)

Get messages and the Set message include the appropriate community string value, in clear text.

NMS sends a Get or Set with the correct community string, as configured on the SNMP agent, the agent processes the message.

SNMPv1 defines both a read-only community and a read-write community.

read-only (RO) community allows Get messages, and the read-write (RW) community allows both reads and writes (Gets and Sets).

RI RO Passi 
RI RW Pass2 
O Get (?assl or Pass2 Worki) 
@Set (Pass2 Only Works) 
Figure 12-12 RO and RW Communities with the Get and Set Commands 
RO Passi 
RI RW Pass2 ">

SNMPv2, and the related Community-based SNMP Version 2 (SNMPv2c)

The original specifications for SNMPv2 did not include SNMPv1 communities

SNMPv3

security had arrived with the powerful network management protocol. SNMPv3 does away with communities and replaces them with the following features:

Message integrity: This mechanism, applied to all SNMPv3 messages, confirms whether or not each message has been changed during transit.

Authentication: This optional feature adds authentication with both a username and password, with the password never sent as clear text. Instead, it uses a hashing method like many other modern authentication processes.

Encryption (privacy): This optional feature encrypts the contents of SNMPv3 messages so that attackers who intercept the messages cannot read their contents.

## FTP and TFTP

lick here to view code image 
R2# show file systems 
File Systems: 
* 
Size(b) 
256487424 
262136 
7794737152 
Free(b) 
49238016 
253220 
7483719680 
copied in 187. 
Type 
opaque 
opaque 
opaque 
opaque 
network 
disk 
disk 
nvram 
opaque 
opaque 
opaque 
network 
network 
network 
network 
network 
opaque 
network 
opaque 
usbflash 
Flags 
rw 
rw 
rw 
rw 
rw 
rw 
rw 
rw 
rw 
rw 
prefixes 
archive: 
system : 
tmpsys : 
null : 
tftp: 
flasho 
: flash:# 
flashl: 
nvram: 
sys log: 
xmodem : 
ymodem : 
rcp: 
pram: 
http : 
scp: 
tar: 
https: 
cns: 
usbflashø: 
74503236 bytes 
876 secs (396555 bytes/sec) ">

Opaque: To represent logical internal file systems for the convenience of internal functions and commands

Network: To represent external file systems found on different types of servers for the convenience of reference in different IOS commands

Disk: For flash

Usbflash: For USB flash

NVRAM: A special type for NVRAM memory, the default location of the startup-config file

the command more flash0:/wotemp/fred would display the contents of file fred in directory /wotemp in the first flash memory slot in the router.

many commands use a keyword that indirectly refers to a formal filename, to reduce typing. For example:

show running-config command: Refers to file system:running-config

show startup-config command: Refers to file nvram:startup-config

show flash command: Refers to default flash IFS (usually flash0:)

### Upgrading IOS Images

process to upgrade an IOS image into flash memory, using the following steps:

Step 1. Obtain the IOS image from Cisco, usually by downloading the IOS image from Cisco.com using HTTP or FTP.

Step 2. Place the IOS image someplace that the router can reach. Locations include TFTP or FTP servers in the network or a USB flash drive that is then inserted into the router.

Step 3. Issue the copy command from the router, copying the file into the flash memory that usually remains with the router on a permanent basis. (Routers usually cannot boot from the IOS image in a USB flash drive.)

nternet 
Figure 12-13 
TFTp server 
Router 
o 
copy tftp flash 
Copying an IOS Image as Part of the Cisco IOS Software Upgrade Process ">

Copying a New IOS Image to a Local IOS File System Using TFTP

ddress or name of remote host [ ] ? 2.2.2.1 
Source filename [ ] ? c29øe-universa1k9-mz . SPA. 152-4. Ml.bin 
Destination filename [c29ee-universa1k9-mz.SPA.152-4.M1.bin ] ? 
Ml. bin 
—mz. SPA. 
Accessing tftp://2.2.2.1/c29ee-universa1k9-mz. 
Loading 
c29ee 
-universalk9 
152-4. 
- 9779404e 
97794e4e 
bytes 
bytes ] 
copied 
in 
187 . 876 
secs 
(396555 
SPA. 152-4. Ml. bin 
(via Gigi 
from 2.2.2.1 
bytes/ sec) ">

copy command

works through these kinds of questions:

What is the IP address or host name of the TFTP server?

What is the name of the file?

Ask the server to learn the size of the file, and then check the local router’s flash to ask whether enough space is available for this file in flash memory.

Does the server actually have a file by that name?

Do you want the router to erase any old files in flash?

Afterward

verifies that the checksum for the file shows that no errors occurred

view the contents of the flash file system

show flash

shows the files in the default flash file system (flash0:)

3:38. 
3 
4 
ee:es. 
5 
ee:es. 
6 
ee:es. 
7 
ee:es. 
8 
18:20. 
9 
21 :es. 
-#- - -length-- -----date/time-- 
Jul 
Jul 
Jul 
Jul 
Jul 
Jul 
Aug 
Oct 
show flash 
le4193476 
seee32e 
1038 
12288e 
1697952 
415956 
1153 
9779404e 
21 
10 
10 
10 
10 
10 
16 
10 
2e15 
2e12 
2e12 
2e12 
2e12 
2e12 
2e12 
2e14 
ee. 
: 44 
52 
02 
16 
28 
56 
• 38 
path 
+00. 
c29ee-universa1k9-mz . SPA 
cpexpress . tar 
home . shtml 
home . tar 
securedesktop-ios-3.1.1. 
ss1c1ient-win-1.1.4.176. 
wo-lic-l 
c29ee-universa1k9-mz.SPA 
49238e16 bytes 
available (207249408 
bytes used) ">

dir flash0: command lists the contents of that same file system, with similar information. (You can use the dir command to display the contents of any local IFS.)

irectory of flashe:/ 
1 
3 
4 
5 
6 
7 
8 
9 
-rw- 
-rw- 
-rw- 
le4193476 
seee32e 
le38 
12288e 
1697952 
415956 
1153 
97794e4e 
Jul 21 2e15 +ee:ee 
Jul 10 2e12 +ee:ee 
Jul 10 2e12 +ee:ee 
Jul 10 2e12 +ee:ee 
Jul 10 2e12 +ee:ee 
Jul 10 2e12 +ee:ee 
Aug 16 2e12 +ee:ee 
Oct 10 2e14 +ee:ee 
c29ee-universa1 
cpexpress . tar 
home . shtml 
home . tar 
securedesktop-i 
sslclient-win-l 
wo-lic-l 
c29ee-universa1 
256487424 bytes total (49238e16 bytes free) ">

show flash lists the bytes used, whereas the dir command lists the total bytes (bytes used plus bytes free). know which command lists which particular total.

Verifying IOS Code Integrity with MD5

when Cisco builds a new IOS image, it calculates and publishes an MD5 hash value for that specific IOS file.

IOS verify command.

will list the MD5 hash as recalculated on your router. If both MD5 hashes are equal, the file has not changed.

ww.cisco.com 
Compare 
Download: 
MD5: xxxxxxx... 
Figure 12-14 MDS Verification of IOS Images—Concepts ">

verify 5 command generates the MD5 hash on your router,

you can include the hash value computed by Cisco as the last parameter (as shown in the example), or leave it off. If you include it, IOS will tell you if the locally computed value matches what you copied into the command. If you leave it out, the verify command lists the locally computed MD5 hash, and you have to do the picky character-by-character check of the values yourself.

lick here to view code image 
R2# verify 5 flashø:c29ee-universa1k9-mz.SPA.154-3.M3.bin a79e325 
.MD5 of flashe:c29ee-universa1k9-mz.SPA.154-3.M3.bin Done! 
Verified (flashe:c29ee-universa1k9-mz . SPA. 154-3.M3. bin) 
= a79e325e6c ">

Copying Images with FTP

ethod 
TFTP 
FTP 
SCP 
Method (Full Name) 
Trivial File Transfer Protocol 
File Transfer Protocol 
Secure Copy Protocol 
Encrypted? 
No 
No 
Yes ">

copy ftp flash

lick here to view code image 
RI* copy 
Tl.bxn 
—mz. SPA. 
155-2. 
Tl.bxn 
—mz. SPA. 
155-2. 
Destination filename [c29ee-universa1k9-mz .SPA.155 
-2. Tl.bin]? 
Accessing ftp 
Loading 
c29ee 
: //192.168.1.17e/c29ee-universa1k9 
-universalk9 
[OK - I e7410736/4096 
bytes ] 
le741e736 
bytes 
copied 
in 
119 . 604 
secs 
(898e53 
bytes/ sec) ">

can configure the FTP username and password on the router so that you do not have to include them in the copy command. For instance, the global configuration commands ip ftp username wendell and ip ftp password odom would have configured those values.

The FTP and TFTP Protocols

copy command, when using the tftp or ftp keyword, makes the command act as a client

FTP Protocol Basics

uses TCP

TCP port 21 and in some cases also well-known port 20.

FTP uses a client/server model for file transfer

<img src="data:image/png;base64,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Bhw2bPno3Rf8MNN9x6660333zzhRdeOH78eFA9XgXMlra2tueff76qqioQCHzcehkwYMCAAQMnFR6PZ9myZbt37+7p6eEhZrM5Ozt71qxZV1999W233XbLLbd8/etfP++88yZNmpSVlQVux8U4YnTw44EWQ/r95YibCB927HAIoss5B5Ok3PDPDmw7BIzxMW0sbUw7Czxc+HTESbuGxxpnUHOTP+L9+O2GMdHR0VFaWurz+RYtWpSUlMTZXiT6Y4Eu27Hf6iYPdSwPI0LFyxot8afEYRSND+vU1NQpU6ZgAuAs57vf/e511103b9684uLiIUOGOJ1Or9e7cePGDRs2NDU1GQzPgAEDBgycIsCSFAwG6+rqnn32WaxQIHYJCQm5ubkTJ04En7v55pt/8pOffO9737vooouKioocDgeSDCZzxOwGeY8PvvhFpOGhm388OV+5iXxFlki6MHM4Isnp7h/Jcn4XxUGnzn422iQcfPA9QvMYTqC0EYFoapYd5X5QyReOk8XwGLtGPVnjUvvxlmP7yLuox2u+wxoX3s2bN9fU1IwYMQJjCANo//79O3fuZF348VqTlYczOrZRcioei6KQwX38CUAaSWfEHXPEPvnD3SkpKWedddY999zz3//+989//vO1114Lnmex0K+iPfHEE+vXr+eSLMWXB+x719GnUNHkse2g/6g4elRskJzAVDRgwIABAx8bsK6xbxo3NzevWrVq165dbrc7OTl5xowZd9999wMPPHDffffddNNNY8aMsVqtXBLA+jV4CeNejkjQ0YFobJQtScaERY3xPL4UUCAkmH8wiO1FRBgiAhE9sS0GpodriqZiSo/UfFRAjLcMFnfI8yTRLI7CPL8AnLRreJ8Ohw0CjLAVK1b09PQMHTo0PT397LPPdrlcra2t7e3t/FGAiNzpA1SQv3AUHx8/a9asO++8869//evf/va366+/HoHbt2/funUrjbto1U7HOh6Og1dKaf6ASB/cWCTbH1lNHnLIeOCANt5Eh40WAwYMGDDwmYAvVdj39/dv2bLlzTffHDVq1He+851//OMff/7zn6+55pqioiKsYoc9ZvepwV/JZAqxQmiiSWPrBPJgV4iicV8sBBGLD1+9UDLsaLHSQPuwMtEvYpwCOEUZ3mCEw+Gurq7y8nJwuylTpjidzjPOOCMtLa2xsRFMSFXVz3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" width="483" height="140" alt="FTP Client 
o 
o 
FTP server 
TCP 3-way Handshake 
FTP Authentication 
FTP Commands 
Figure 12-15 Major Concepts with FTP Clients and Servers ">

FTP control connection—define the kinds of functions supported by FTP

allow the client to navigate around the directory structures of the server, list files, and then transfer files from the server (FTP GET) or to the server (FTP PUT).

summary of some of the FTP actions:

Navigate directories: List the current directory, change the current directory to a new directory, go back to the home directory, all on both the server and client side of the connection.

Add/remove directories: Create new directories and remove existing directories on both the client and server.

List files: List files on both the client and server.

File transfer: Get (client gets a copy of the file from the server), Put (client takes a file that exists on the client and puts a copy of the FTP server).

FTP Active and Passive Modes

may impact whether the TCP client can or cannot connect to the server and perform normal functions

user at the FTP client can choose which mode to use

FTP passive mode may be the more likely option to work.

FTP uses two types of TCP connections:

Control Connection: Used to exchange FTP commands

Data Connection: Used for sending and receiving data, both for file transfers and for output to display to a user

when a client connects to an FTP server, the client first creates the FTP control connection

server listens for new control connections on its well-known port 21

client allocates any new dynamic port (49222 in this case) and creates a TCP connection to the server

9222 
192.168.1.102 
TCP SYN 
TCP SYN ACK 
TCP ACK 
Figure 12-17 FTP Client Creates an FTP Control Connection 
FTP Server 
192.168.1.11 ">

The FTP client allocates a currently unused dynamic port and starts listening on that port.

The client identifies that port (and its IP address) to the FTP server by sending an FTP PORT command to the server.

The server, because it also operates in active mode, expects the PORT command; the server reacts and initiates the FTP data connection to the client’s address (192.168.1.102) and port (49333).

9222 
TCP control 
FTP PORT 192.168.1.102 49333 
TCP SYN for FTP Data 
FTP Server 
21 
49160 
Figure 12-18 FTP Active Mode Process to Create the Data Connection ">

Passive mode helps solve the firewall restrictions by having the FTP client initiate the FTP data connection to the server.

passive mode does not simply cause the FTP client to connect to a well-known port on the server;

The FTP client changes to use FTP passive mode, notifying the server using the FTP PASV command.

The server chooses a port to listen on for the upcoming new TCP connection, in this case TCP port 49444.

The FTP notifies the FTP client of its IP address and chosen port with the FTP PORT command.

The FTP client opens the TCP data connection to the IP address and port learned at the previous step.

92.168.1.102 
49222 
49160 
192.168.1.11 
FTP Server 
FTP PASV 
49444 
FTP PORT 192.168.1.11 49444 0 
TCP SYN for FTP Data Connection 
Figure 12-19 FTP Passive Mode Process to Create the Data Connection ">

FTP over TLS (FTP Secure)

FTPS encrypts both the control and data connections with TLS, including the exchange of the usernames and passwords

FTPS explicit mode process:

The client creates the FTP control TCP connection to server well-known port 21.

The client initiates the use of TLS in the control connection with the FTP AUTH command.

When the user takes an action that requires an FTP data connection, the client creates an FTP data TCP connection to server well-known port 21.

The client initiates the use of TLS in the data connection with the FTP AUTH command.

92.168.1.102 
192.168.1.11 
FTP Server 
o 
49222 
FTP AUTH (Starts TLS) 
49299 
o 
FTP AUTH (Starts TLS) 
Figure 12-20 FTPS Explicit Mode Control and Data Connection Establishment ">

implicit mode process

begins with a required TLS connection, with no need for an FTP AUTH command, using well-known ports 990 (for the control connection) and 989 (for the data connection).

SFTP

uses SSH to encrypt file transfers over an SSH connection. However, the acronym SFTP does not refer to a secure version of FTP.

TFTP Protocol Basics

Trivial File Transfer Protocol uses UDP well-known port 69. Because it uses UDP, TFTP adds a feature to check each file for transmission errors by using a checksum process on each file after the transfer completes.

the code requires less space to install, which can be useful for devices with limited memory.

can Get and Put files, but it includes no commands to change directories, create/remove directories, or even to list files on the server.

does not support even simple clear-text authentication. In effect, if a TFTP server is running, it should accept requests from any TFTP client.
