1.0 Network Fundamentals  
1.10 Identify IP parameters for Client OS (Windows, Mac OS, Linux)  
4.0 IP Services  
4.3 Explain the role of DHCP and DNS within the network  
4.6 Configure and verify DHCP client and relay  
DHCP Concepts

```
Four messages between the client and server (DORA):
```

- Discover: - Sent by the DHCP client to find a willing DHCP server
- Offer: - Sent by a DHCP server to offer to lease  
    Request: - Sent by the DHCP client to ask the server to lease the IPv4 address listed in the Offer message  
    Acknowledgment: - Sent by the DHCP server to assign the address and to list the mask, default router, and DNS server IP addresses

```
IPv4 addresses that allow a host that has no IP address to still be able to send and receive messages on the local subnet:
0.0.0.0: - An address reserved for use as a source IPv4 address for hosts that do not yet have an IP address.
255.255.255.255: - The local broadcast IP address. Packets sent to this destination address are broadcast on the local data link, but routers do not forward them.
```

- - a client, sends a Discover message, with source IP address of 0.0.0.0Host A sends the packet to destination 255.255.255.255 router R1 will not forward this packet.
        - - assuming the DHCP client chooses to use a DHCP option called the broadcast flag; all examples in this book assume the broadcast flag is used.
        - all hosts in the subnet receive the Offer message
        - the original Discover message lists a number called the client ID□□ includes the host’s MAC address, that identifies the original host (host A in this case).As a result, host A knows that the Offer message is meant for host A, which.

Supporting DHCP for Remote Subnets with DHCP Relay

```
ip helper - Watch for incoming DHCP messages, with destination IP address 255.255.255.255 - address server-ip.
```

# 7 DHCP config

Thursday, September 30, 2021 12:17 PM

- - Watch for incoming DHCP messages, with destination IP address 255.255.255.255Change that packet’s source IP address to the router’s incoming interface IP address..
- Change that packet’s destination IP address to the address of the DHCP server (as configured in the **addres** scommand). **ip helper-**
- Route the packet to the DHCP server.  
    the server simply reverses the source and destination IP address of the packet received from the router  
    (relay agent)

- the Discover message lists source IP address 172.16.1.1, so the server sends the Offer message back to destination IP address 172.16.1.1.
- the DHCP relay agent (router R1) needs to change the destination IP address, so that the real DHCP client (host A), which does not have an IP address yet, can receive and process the packet.
- Sends as broadcast back to the LAN
- for the return packet from the DHCP server

```
types of settings the DHCP server needs to know to support DHCP clients:
```

- Subnet ID and mask:
- Reserved (excluded) addresses: - which addresses in the subnet to not lease.
- - Default router(s)DNS IP address(es)  
        other parameters  
        Maximum lease time- time limit for leasing an IP address  
        DHCP uses three allocation modes  
        Dynamic allocation - the DHCP mechanisms and configuration described throughout this chapter.  
        automatic allocation-sets the DHCP lease time to infinite.  
        static allocation- preconfigures the specific IP address for a client based on the client’s MAC address.  
        Trivial File Transfer Protocol (TFTP) server address

Information Stored at the DHCP Server

Configuring DHCP Relay  
What for?-- DHCP clients exist in the subnetDHCP servers do not exist in the subnet

```
(config-if)# ip helper-address address
Show ip interface g0/0 - Helper Address is address or Helper address is not set
```

Configuring a Switch as DHCP Client

```
(config-if) ip address dhcp
```

- the switch does not attempt DHCP until the interface reaches an up/up state  
    **show interfaces** - verify ip address _interface_  
    **show dhcp lease** - - see the (temporarily) leased IP address and other parametersthe switch does not store the DHCP-learned IP configuration in the running-config

```
show ip default - view address of the default gateway - gateway
```

```
(config-if) # ip address dhcp
```

- IOS displays this route as a static route (destination 0.0.0.0/0)  
    To recognize this route as a DHCP-- administrative distance of 1 for static routes configured with the default of 254 for default routes added because of DHCP.-learned default route, look to the administrative distance value of 254. **ip route** configuration command

Configuring a Router as DHCP Client

```
To work correctly, an IPv4 host needs to know these values:
```

- - DNS server IP addressesDefault gateway (router) IP address
- - Device’s own IP addressDevice’s own subnet mask

Host Settings for IPv

Host IP Settings on Windows

- - lists the host’s IP routing tablethe top of the table lists a route based on the default gateway (0.0.0.0 and 0.0.0.0)
- top of the output also lists several other routes related to having a working interface, like a route to the subnet connected to the interface.

```
netstat -rn
```

```
the PC thinks the destination is on the local subnet (link)
```

```
gateway of “on-link”
```

Host IP Settings on macOS

- - does not have an /all optiondoes not list the default gateway or DNS servers
- Shows mac address and ip address

```
ifconfig
```

```
networksetup - Shows dhcp config, ip, subnet mask, and default gateway - getinfo Ethernet
```

```
networksetup - Shows dns server - getdnsservers Ethernet
```

- adds a default route to its host routing table based on the default gateway
    - output represents the default route using the word default rather than 0.0.0.0 and 0.0.0.
- adds route to the local subnet calculated based on the IP address and mask learned with DHCP- uses the **netstat -rn** command to list those routes

```
some Linux distributions do not include net-tools.
You can add netincludes ifconfig-tools to most Linux distributions.and netstat -rn.
```

- preinstalled on Linuxincludes a set of replacement commands and functions, many performed with the ip command and some
- - parameters.similar to the macOS version but also shows some interface counters.
        - shows basic addressing info
        - Shows subnet in prefix notation rather than in dotted decimal

```
ipaddress
```

```
iproute library
```

```
ifconfig wlan0 - - shows l2 and l3 addressesfrom net-tools
```

- from net-tools
- lists a default route, but with a style that shows the destination as 0.0.0.0. - points to the default gateway as learned with DHCP:

```
The bottom of the example shows the command meant to replace netstat shows a default route that references the default router, along with a route for the local subnet.-rn: ip route. Note that it also
```

- lists a route to the local subnet

```
netstat -rn
```

Host IP Settings on Linux

```
5.0 Security Fundamentals
5.7 Configure Layer 2 security features (DHCP snooping, dynamic ARP inspection, and port security)
```

- notices DHCP messages that fall outside the normal use of DHCP
- - watches the DHCP messages that flow through a LAN switchbuilds a table that lists the details of legitimate DHCP flows
- other switch features can know what legitimate DHCP leases exist for devices connected to the switch.

```
DHCP Snooping
```

- helps prevent packets being redirected to an attacking host.
- Some ARP attacks try to convince hosts to send packets to the attacker’s device instead of the true destination.  
    ○ checks incoming ARP messages,  
    ○ checks those against normal ARP operation as well as  
    ○ checks the details against other data sources, including the DHCP Snooping binding table. When the ARP message does not match the known information about the legitimate  
    addresses in the network, the switch filters the ARP message.

```
○
```

- The switch watches ARP messages as they flow through the switch.

```
Dynamic ARP Inspection (DAI)
```

```
DHCP Snooping Concepts
```

- - analyzes incoming messages on the specified subset of ports in a VLANnever filters non-DHCP messages
- allow the incoming DHCP message or discard the message.
- operates on LAN switches and is commonly used on Layer 2 LAN switches and enabled on Layer 2 ports.
- - Client facing devices are untrustedDHCP facing devices (server, router, switch) are trusted
- works first on all ports in a VLAN, but with each port being trusted or untrusted by DHCP Snooping  
    the rules differentiate between messages normally sent by servers (like DHCPOFFER and  
    DHCPACK) versus those normally sent by DHCP clients:
- - DHCP messages received on an untrusted port, for messages normally sent by a server, will always be discarded.
    - DHCP messages received on an untrusted port, as normally sent by a DHCP client, may be filtered if they appear to be part of an attack.  
        DHCP messages received on a trusted port will be forwarded; trusted ports do not filter  
        (discard) any DHCP messages.
    

```
A Sample Attack: A Spurious DHCP Server
```

- - Spurious DHCP server (attacker) responds to dhcp message by a client pcattacker replies with false dhcp information by naming itself as the default gateway

# 8 DHCP Snooping and ARP Inspection

Friday, October 1, 2021 11:13 AM

- attacker replies with false dhcp information by naming itself as the default gatewayPc1 send all messages to another network to attacker, becoming a man-in-the-middle  
    attack (pc2 could forward the messages to the actual default gateway
- the legitimate DHCP also returns a DHCPOFFER message to host PC1, but most hosts use the  
    first received DHCPOFFER, and the attacker will likely be first in this scenario.

DHCP Snooping Logic

- stops attacks by making ports untrusted

```
▪ client can tell the DHCP server it no longer needs the address, releasing it back to the DHCP server
```

- DHCP RELEASE

```
▪ turn down the use of an IP address during the normal DORA flow on messages.
```

- DHCP DECLINE
- DHCP clients also use the DHCP RELEASE and DHCP DECLINE messages.

```
DHCP Snooping rules:
```

- - Examine all incoming DHCP messages.If normally sent by servers, discard the message.
- If normally sent by clients, filter as follows:
    - check for MAC address consistency between the Ethernet frame and the DHCP message.
- DISCOVER and REQUEST

```
check the incoming interface plus IP address versus the DHCP Snooping binding
table.
```

```
RELEASE or DECLINE -
```

- FSnooping binding table.or messages not filtered that result in a DHCP lease, build a new entry to the DHCP

DHCP snooping checking MAC Address

- Source MAC address included in DISCOVER message
- frame encapsulating the dhcp message also includes the source mac address
    - if not the packet is dropped
- DHCP Snooping checks to make sure those values match.
- Used on untrusted ports
- chaddr (client hardware address)
- stops attacker from leasing all available addresses so no other client can get a lease  
    Filtering Messages that Release IP Addresses
- creates entry for all legitimate DHCP entriesDHCP Snooping, and other features like Dynamic ARP Inspection, can use the table to make  
    decisions.

- - MACIP
- VLAN
- DHCP Snooping Binding Table:
- DHCP Snooping binding table

- - VLANINTERFACE
- attacker pretends his source IP is the legitimate IP trying to RELEASE
- the source interface in the DHCP Snooping Binding Table does not match so dhcp snooping bloacks the request
- attacker could RELEASE an address that is not his and attempt steal it for himself

```
checks client-sent messages like RELEASE and DECLINE that would cause the DHCP server to be
allowed to release an address
```

DHCP Snooping Configuration

- **ip dhcp snooping**
- enable DHCP Snooping
- **ip dhcp snooping vlan** _vlan-id_
- list the VLANs on which to use DHCP Snooping

```
Required:
```

- default is untrusted.
- **(config-if) # ip dhcp snooping trust**

```
Often used:- configure trusted ports
```

DHCP Snooping verification  
**show ip dhcp snooping**

- enabled or disabled
- - operational in which vlanstrusted interfaces
        - (enabled by default)  
            **no ip dhcp information option** - (because this switch is not a dhcp relay agent)command is configured
        
        - DHCP relay agents add option 82 DHCP header fields (RFC 3046)
        - - If enabled on a non relay agent then dhcp stops working for end usersThe switch sets fields in the DHCP messages as if it were a DHCP relay agent
        - changes to those messages cause most DHCP servers (and most DHCP relay agents) to ignore the received DHCP messages.
- Insertion of option 82 is disabled
- Rate limit on each interface

```
Shows actual dhcp snooping binding table
```

```
Show ip dhcp snooping binding
```

DHCP Rate Limiting

- attacker generates large volumes of DHCP messages to overload the DHCP Snooping feature and the switch CPU itself
    - optional feature that tracks the number of incoming DHCP messages.
        - port changes to an err-disabled state.
    - If the number of incoming DHCP messages exceeds that limit over a one-second period:
        - can be on both on trusted and untrusted interfaces.
    - Default of no rate limit

- Default of no rate limit

```
(config-int) # ip dhcp snooping rate limit number
errdisable recovery cause dhcp - recover from errdisable if caused by dhcp snooping - rate-limit
errdisable recovery interval - seconds to wait before recovering number
(config-int) # no ip dhcp snooping rate limit
```

```
how to enable DHCP Snooping rate limits and err-disabled recovery.
```

Dynamic ARP Inspection (DAI)  
examines incoming ARP messages on untrusted ports to filter those it believes to be part of an  
attack.

- - - DHCP Snooping binding tableconfigured ARP ACLs.
- compares incoming ARP messages with two sources of data:
- If the incoming ARP message does not match the tables in the switch, the switch discards the ARP message.

DAI Concepts  
gratuitous ARP (arp reply)triggers hosts to add incorrect ARP entries to their ARP tables.—

```
Both hosts learn the other host’s MAC address with this twolearn R2’s MAC address based on the ARP reply (message 2), but router R2 learns PC1’s IP and -message flow. Not only does PC
MAC address because of the ARP request (message 1).
```

- source mac
- destination mac (broadcast)
- Ethernet Frame
- - Origin IPTarget IP
- - Origin MACTarget MAC ??
- ARP

```
ARP Request
```

- - Source MACDest. MAC
- Ethernet Frame
- - Origin IPTarget IP
- - Origin MACTarget MAC
- ARP

```
ARP Reply
```

Review of Normal IP ARP

Gratuitous ARP as an Attack Vector

- when a host changes its MAC address it can send a gratuitous ARP message with these features:
    - ARP reply.
    - sent without having first received an ARP request.sent to an Ethernet destination broadcast address so that all hosts in the subnet receive the
    - message.
    - attacker uses gratuitous arp to make replies go back to it instead of original host
- could be part of a man-in-the-middle attack

Dynamic ARP Inspection Logic

- Host does not need arp if it doesn't have an IP yet
- Once DHCP assigns and IP then ARP is usedfor untrusted interfaces DAI confirms an ARP’s correctness based on the DHCP Snooping Binding  
    table

- compares origin MAC and IP
- - if not found on the table, discard the arpsame trusted and untrusted rules as dhcp snooping
        - statically configured
        - list correct pairs of IP and mac addressesUseful for ip addresses configured statically because they will not be in the dhcp snooping  
            binding table
        

```
ARP ACL
```

```
DAI can check Ethernet header and arp source and destination messages mac addresses to make
sure they match
```

- DAI can also check Messages with unexpected IP addresses in the two ARP IP address fields
    - DAI itself can be more susceptible to DoS attacks.
    - attacker could generate large numbers of ARP messages, driving up CPU usage in the switch.  
        DAI can avoid these problems through rate limiting the number of ARP messages on a port  
        over time.
    
- does its work in the switch CPU rather than in the switch ASIC

Configuring ARP Inspection on a Layer 2 Switch  
decisions include the following:

- Choose whether to rely on DHCP Snooping, ARP ACLs, or both.
- - If using DHCP Snooping, configure it and make the correct ports trusted for DHCP Snooping.Choose the VLAN(s) on which to enable DAI.
- Make DAI trusted (rather than theVLANs, typically for the same ports you trusted for DHCP Snooping.default setting of untrusted) on select ports in those  
    **ip arp inspection vlan** - enable arp DAI on that vlan _vlan-id_  
    **(config** - dhcp snooping should be enabled or DAI will filter all packets **- if)# ip arp inspection trust  
    ip dhcp snoopingip dhcp snooping vlan** _vlan-id_  
    **ip dhcp snooping trust**

```
ip dhcp snooping trust (configure arp ACLs)
```

```
gives both -- forwarded, dropped, dhcp drops, acl drop countsIs logging enabled?configuration settings along with status variables and counters
```

```
show ip arp inspection -
```

- counts per vlan- forwarded, dropped, dhcp drops, acl drops
- permits

```
show ip arp inspection statistics
```

ARP Rate Limiting

- (trusted and untrusted)
- Default for all interfaces
- - x ARP messages over y seconds”(DHCP Snooping does not define a burst setting)
- optional configuration
- 8 messages in a burst of 4 seconds

```
ip arp inspection limit rate 8 burst interval 4
```

- default of 15 messages over a one second burst  
    **show ip arp inspection interfaces** - rate, burst interval, trust state, per interface

```
burst interval (a number of seconds)
```

```
ip arp inspection limit rate number
```

- disable rate limiting

```
ip arp inspection limit rate none
```

**errdisable recovery cause arperrdisable recovery interval** _30_ **- inspection**

Configuring Optional DAI Message Checks

- one, two, or all three of the options
- - command with overrides previous versions of the same command **show ip arp inspection** to validate

```
ip arp inspection validate {dst-mac, ip, src-mac}
```

```
drop ARP packets the body of the ARP packets do not match the addresses specified in the Ethernet header.when the IP addresses in the packets are invalid or when the MAC addresses in
Forin the ARP body. This check is src-mac, check the source MAC address in the Ethernet header against the sender MAC address performed on both ARP requests and responses. When enabled,
packets with different MAC addresses are classified as invalid and are dropped.
```

- Foraddress in ARP body. This check isdst-mac, check the destination MAC address in the Ethernet header against the target MAC performed for ARP responses.When enabled, packets with  
    different MAC addresses are classified as invalid and are dropped.
- For255.255.255.255, and all IP multicast addresses. ip, check the ARP body for invalid and unexpected IP addresses. Addresses include 0.0.0.0, Sender IP addresses are checked in all ARP  
    requests and responses, and target IP addresses are checked only in ARP responses

```
2.0 Network Access
2.3 Configure and verify Layer 2 discovery protocols (Cisco Discovery Protocol and LLDP)
4.0 IP Services
4.2 Configure and verify NTP operating in a client and server mode
4.5 Describe the use of syslog features including facilities and levels
```

## System Message Logging (Syslog)

```
Sending Messages in Real Time to Current Users
```

- Telnet and SSH users, the device requires a two-step process before the user sees the messages.  
    global configuration setting—logging monitor—tells IOS to enable the sending of log  
    messages to all logged users.

must also issue theterminal monitorEXEC command during the login session, which tells  
IOS that this terminal session would like to receive log messages.

```
Storing Log Messages for Later Review
two primary means to keep a copy
```

- can configuration command.store copies of the log messages in RAMby virtue of the **logging buffered** global  
    any user can come back later and see the old log messagesby using the **show**  
    **logging EXEC command.**  
    store log messages centrally to a syslog server.  
    syslog protocol - a UDP protocol to send messages to a syslog server for storage  
    To configure a router or switch to send log messages to a syslog server, add the

# 9 Device Management Protocols

Monday, October 4, 2021 2:02 PM

```
To configure a router or switch to logging host {address | hostname } send log messages to a syslog serverglobal command , add the
```

```
*Dec 18 17:10:15.079: %LINEPROTOchanged state to down - 5 - UPDOWN: Line protocol on Interface FastEthernet0/0,
A timestamp: *Dec 18 17:10:15.
The facility on the router that generated the message : %LINEPROTO
The severity level : 5
A mnemonic for the message : UPDOWN
The description of the message: Line protocol on Interface FastEthernet0/0, changed
state to down
you can at least toggle on and off the use of thelog message sequence number (which is not enabled by default)timestamp (which is included by default). Example 9-1 reverses those and a
defaults by turning off timestamps and turning on sequence numbers.
```

Log Message Format

Log Message Severity Levels  
the lower the number, the more severe the event that caused the message.

```
last level in the figure is used for messages requested by the debug command
Table 9severity level for each type.-2 summarizes the configuration commands used to enable logging and to set the
For example, the command logging console 4 causes IOS to send severity level 0the console –4 messages to
```

Configuring and Verifying System Logging

the example configures the same message level at the console and for terminal monitoring  
(level 7, or debug), and the same level for both buffered and logging to the syslog server (level 4, or warning). The levels may be set using the numeric severity level or the name as  
shown earlier in Figure 9-3.  
**show logging** messages per the logging buffered configuration.commandconfirms those same configuration settings and also lists the log

If any log messages had been buffered, the actual log messages would be listed at  
the end of the command  
clear out the old messages from the log with the **clear logging** EXEC command.

The debug Command and Log Messages  
**debug** internal events, with that monitoring process continuing over time, so that IOS can issue log EXEC command gives the network engineer a way to ask IOS to monitor for certain  
messages when those events occur  
debug remains active until some user issues the **no debug command** with the same parameters,  
disabling the debug.

```
anyone logged in with SSH at the time Example 9the output, even with the logging monitor debug - 4’s output was gathered would not have seen command configured on router R1, without
first issuing a terminal monitor command.
```

```
all enabled debug options use router CPU, which can cause problems for the router. You can
monitor CPU use withtheshow process cpucommand
use caution when using debug commands carefully on production devices.
the more CLI users that receive debug messages, the more CPU that is consumed.
```

#### Network Time Protocol (NTP)

```
Devices send timestamps to each other with NTP messages, continually exchanging messages, with one device changing its clock to match the other, eventually synchronizing the clocks.
How NTP defines the sources of time data (stratum). (reference clocks) andhow good each time source is
```

**Setting the Time and Timezone**  
NTP works best if you set the device clock to a reasonably close time before enabling the NTP  
client functionwith the **ntp server** command  
I shouldset the time to 8:52 p.m., set the correct date and timezone, and even tell the device to  
adjust for daylight savings time—and then enable NTP  
Example 9-7 shows how to set the date, time, timezone, and daylight savings time.

```
You should set the first two commands before setting the time of day with the EXEC command because the two configuration commands impact the time that is set. clock set
chose EDT because it is the acronym for daylight savings time in that same EST time zone.
Finally, thehour automatically over the years.recurring keyword tells the router to spring forward an hour and fall back an
clock set EXEC command
uses a time syntax with a 24-hour format, not with a 12-hour format plus a.m./p.m.).
```

```
uses a time syntax with a 24-hour format, not with a 12-hour format plus a.m./p.m.).
The EDT, rather than UTC time. show clock command (issued seconds later)lists that time, but also notes the time as
```

**Basic NTP Configuration**  
two ntp configuration commands  
**ntp master {stratum** not as an NTP client. The device gets its time information from the internal clock on the **- level}:** NTP server mode—the device acts only as an NTP server, and  
device.  
**ntp server {address | hostname}** : NTP client/server mode—the device acts as both client  
and serversynchronized, the device can then act as an NTP server, to supply time to other NTP. First, it acts as an NTP client, to synchronize time with a server. Once  
clients.

```
show ntp status command
```

**show ntp status** command  
lists a status of synchronizedchanging its time to match the server’s time. , which confirms the NTP client has completed the process of Any router acting as an NTP client will list  
“unsynchronized” in that first line until the NTP synchronization process completes with at least one server. It also confirms the IP address of the server—this device’s reference  
clock—with the IP address configured in Example 9-8 (172.16.2.2).

```
show ntp associations
lists all the NTP servers that the local device can attempt to use, with status information
about the association between the local device (client) and the various NTP servers.
```

###### NTP Reference Clock and Stratum

```
Devices that act solely as an NTP server get their time from either internal device hardware or from some external clock using mechanisms other than NTP.
NTP servers and clients use a number to show the perceived accuracy of their reference clock data based on stratum level. The lower the stratum level, the more accurate the reference clock
is considered to be.sets its own stratum level. Then,An NTP server that uses its internal hardware or external reference clock an NTP client adds 1 to the stratum level it learns from its NTP
server, so that the stratum level increases the more hops away from the original clock source.
For instance, back in Figure 9which references R3, adds 1 so it has a stratum of 3. R1 uses R2 as its NTP server, so R1 adds 1 to -5, you can see the NTP primary server (R3) with a stratum of 2. R2,
have a stratum of 4. These increasing stratum levels allow devices to refer to several NTP servers
and then use time information from the best NTP server, best being the server with the lowest stratum level.
Routers and switches use the default stratum level of 8 for their internal reference clock based
on the default setting of 8 for the stratum level in the command allows you to set a value from 1 through 15 ntp master [stratum ; in Example 9-8, the - ntp master 2level] command. The
command set router R3’s stratum level to 2.
Note
NTP considers 15 to be the highest useful stratum level, so any devices that calculate their
stratum as 16 consider the time data unusable and do not trust the time. So, avoid setting higher stratum values on the ntp master command.
```

```
stratum values on the ntp master command.
```

###### Redundant NTP Configuration

```
an enterprise could use NTP to reference NTP servers that use an atomic clock as their reference source, like the NTP primary servers in Figure 9-6, which happen to be run by the US National
Institute of Standards and Technology (NIST) (see tf.nist.gov).
```

```
AnNTP primary server acts only as a server, with a reference clock external to the device,
and has a stratum level of 1secondary servers are servers that use client/server mode as described throughout this , like the two NTP primary servers shown in Figure 9-6.NTP
section, relying on synchronization with some other NTP server.
```

```
NTP primary server and NTP secondary server.
```

```
After losing their reference clock, R1 and R2 could no longer be useful NTP servers to the rest of the enterprise.
To overcome this potential issue, the routers can also be configured with the ntp master
command, resulting in this logic:
Establish an association with the NTP servers per thentp server command.
Establish an association with your internal clock using the ntp master stratum command.
Set the stratum level of the internal clock (per thea higher (worse) stratum level than the Internet-based NTP servers.ntp master {stratum-level} command) to
Synchronize with the best (lowest) known time source, which will be one of the Internet NTP servers in this scenario
ntp master 7 command, with a much higher stratum,
```

###### NTP Using a Loopback Interface for Better Availability

```
what happens when one interface on R4 fails
for any NTP clients that had referred to that specific IP address
There would likely still be a route to reach R4 itself.
The NTP client would not be able to send packets to the configured address because that interface is down.
```

```
loopback interface to meet that exact need
once configured, it remains in an up/up state as long as
Key Topic.The router remains up.
You do not issue a shutdown command on that loopback interface.
```

#### Analyzing Topology Using CDP and LLDP

###### Examining Information Learned by CDP

```
Cisco-proprietary
Layer 2 protocol
does not rely on a working Layer 3 protocol
```

does not rely on a working Layer 3 protocol  
Devices that support CDP learn information about others by listening for the advertisements sent by other devices.

CDP discovers several useful details from the neighboring Cisco devices:

**Device identifier** : Typically the host name  
**Address list:** Network and data-link addresses  
**Port identifier:** link that sent the CDP advertisementThe interface on the remote router or switch on the other end of the  
**Capabilities list** : Information on what type of device it is (for example, a router or a  
switch)  
**Platform** : The model and OS level running on the device  
Cisco IP Phones use CDP to learn the data and voice VLAN IDs as configured on the access  
switch.

routers and switches support the same CDP commands, with the same parameters and  
same types of output.

To ensure all devices receive a CDP message, tdestination MAC address (0100.0CCC.CCCC). he Ethernet header uses a multicast

the device processes the message and then discards it, rather than forwarding it  
**show cdp neighbors detail**  
lists the full name of the switch model (WSconfigured on the neighboring device. -2960XR-24TS-I) and the IP address

```
The show cdp entry name command lists the exact same details shown in the output of
the command. show cdp neighbors detail command, but for only the one neighbor listed in the
Cisco recommends that CDP be disabled on any interface that might not have a need for CDP. For switches, any switch port connected to another switch, a router, or to an IP
phone should use CDP.
```

###### Configuring and Verifying CDP

```
IOS typically enables CDP globally and on each interface by defaultinterface with the no cdp enable interface subcommand. You can then disable CDP per
re-enable it with the cdp enable interface subcommand
disable and re-enable CDP globally on the device
no cdp run and cdp run global commands
```

```
send time and the hold time. CDP sends messages every 60 seconds by default, with a hold time
of 180 seconds.device before removing those details from the CDP tables. You can override the defaults with The hold time tells the device how long to wait after no longer hearing from a
the cdp timer seconds and cdp holdtime seconds global commands, respectively.
```

#### Examining Information Learned by LLDP

the LLDP output in the example does differ from CDP in a few important ways:

```
LLDP uses B as the capability code for switching, referring to bridgetype that existed before switches that performed the same basic functions., a term for the device
LLDP does not identify IGMP as a capability, while CDP does (I).
CDP lists the neighbor’s platform, a code that defines the device type, while LLDP does not.
LLDP lists capabilities with different conventions (see upcoming Example 9-19).
```

```
System Capabilities : What the device can do
Enabled Capabilities : What the device does now with its current configuration
LLDP uses the same messaging concepts as CDP, encapsulating messages directly in dataheaders. Devices do not forward LLDP messages so that LLDP learns only of directly connected -link
neighbors. LLDP does use a differentmulticast MAC address(0180.C200.000E)
```

```
Cisco devices default to disable LLDP
LLDP separates the sending and receiving of LLDP messages as separate functions.
LLDP support processing receives LLDP messages on an interface so that the switch or router
learns about the neighboring device while not transmitting LLDP messages to the neighboring device.
the commands include options to toggle on|off the transmission of LLDP messages separately
from the processing of received messages.
[no] lldp run: A global configuration command thatsets the default mode of LLDP operationfor
any interface that does not have more specific LLDP subcommands (lldp transmit, lldp receive). The lldp run global command enables LLDP in both directions on those interfaces, while no lldp
```

###### Configuring and Verifying LLDP

The lldp run global command enables LLDP in both directions on those interfaces, while no lldp run disables LLDP.

**[no] lldp transmit** : An interface sub-command that defines the operation of LLDP on the  
interface subcommand causes the device to transmit LLDP messages, while no lldp transmit causes it to regardless of the global [no] lldp run command. The lldp transmit interface  
not transmit LLDP messages.  
**[no] lldp receive** :An interface subcommand that defines the operation of LLDP on the interface  
regardless of the global [no] lldp run command.the device to process received LLDP messages, while no lldp receive causes it to not process The lldp receive interface subcommand causes  
received LLDP messages.

**show lldp interface** lists the interfaces on which LLDP is enabled.

like CDP,shows the default settings of 30 seconds for the send timer and 120 seconds for the hold timer. LLDP uses a send timer and hold timer for the same purposes as CDP.The example  
You can override the defaults with the commands **lldp timer seconds** and **lldp holdtime seconds** global

4.0 IP Services  
4.1 Configure and verify inside source NAT using static and pools

CIDR

```
most public address assignments for the last 20 years have been a CIDR block rather than an entire class A, B, or C network.
```

Private Addressing

```
no organization is allowed to advertise these networks using a routing protocol on the Internet.
```

## 10 NAT

Friday, October 8, 2021 7:12 AM

Network Address Translation Concepts

Static NAT  
IP addresses statically mapped to each other.

NAT router simply configures a oneregistered address that is used on its behalf. -to-one mapping between the private address and the

Supporting a second IP host with static NAT requires a second static onesecond IP address in the public address range. -to-one mappingusing a

the router statically maps 10.1.1.2 to 200.1.1.2. Because the enterprise has a single registered Class C network, it can support at most 254 private IP addresses with NAT, with the usual two  
reserved numbers (the network number and network broadcast address).  
inside local for the private IP addresses in this example and inside global for the public IP addresses.

Dynamic NAT  
Dynamic NAT sets up a pool of possible inside global addresses and defines matching criteria to determine which inside local IP addresses should be translated with NAT.

```
Host 10.1.1.1 sends its first packet to the server at 170.1.1.1.
As the packet enters the NAT router, the router applies some matching logic to decide whether
```

```
As the packet enters the NAT router, the router applies some matching logic to decide whether the packet should have NAT applied. Because the logic has been configured to match source IP
addresses that begin with 10.1.1, the router adds an entry in the NAT table for 10.1.1.1 as an inside local address.
The NAT router needs to allocate an IP address from the pool of valid inside global addresses. It picks the first one available (200.1.1.1, in this case) and adds it to the NAT table to complete the
entry.
The NAT router translates the source IP address and forwards the packet.
The dynamic entry stays in the table as long as traffic flows occasionally. You can configure a timeout value that defines how long the router should wait, having not translated any packets
with that address, before removing the dynamic entry.entries from the table using the clear ip nat translation You can also * command.manually clear the dynamic
NAT can be configured with more IP addresses in the inside local address list than in the inside global address pool.
If a new packet arrives from yet another inside host, and it needs a NAT entry, but all the pooled IP addresses are in use, the router simply discards the packet. The user must try again until a NAT
entry times out, at which point the NAT function works for the next host that sends a packet. Essentially, the inside global pool of addresses needs to be as large as the maximum number of
concurrent hosts that need to use the Internet at the same timeexplained in the next section. —unless you use PAT, as is
```

Overloading NAT with Port Address Translation  
NAT Overload feature, also called Port Address Translation (PAT)

```
The NAT router keeps a NAT table entry for every unique combination of inside local IP address and port, with translation to the inside global address and a unique port number associated with
```

```
and port, with translation to the inside global address and a unique port number associated with the inside global address.
NAT overload can use more than 65,000 port numbers
PAT is by far the most popular option
```

##### NAT Configuration and Troubleshooting

Static NAT Configuration  
Each static mapping between a local (private) address and a global (public) address must be configured.  
Those same interface subcommands tell NAT whether the interface is inside or outside.  
Step 1. Use thebe in the inside part of the NAT design. **ip nat inside** command in interface configuration mode to configure interfaces to  
Step 2. Use the be in the outside part of the NAT design. **ip nat outside** command in interface configuration mode to configure interfaces to  
Step 3. Use theconfiguration mode to configure the static mappings. **ip nat inside source static inside-local inside-global** command in global

```
static mappings are created using the ip nat inside source static command.
Source keyword means that NAT translates the source IP address of packets coming into its inside interfaces. The static keyword means that the parameters define a static entry, which should
never be removed from the NAT table because of timeout.hosts—10.1.1.1 and 10.1.1.2—to have Internet access, two ip nat inside commands are needed.Because the design calls for two
show ip nat translations The show ip nat statistics command lists the two static NAT entries created in the configuration. command lists statistics, listing things such as the number of currently
active translation table entries. The statistics also include the number of hits, which increments for every packet for which NAT must translate addresses.
```

Dynamic NAT Configuration  
Dynamic NAT still requires that each interface be identified as either an inside or outside interface  
Dynamic NAT uses an access control list (ACL) to identify which inside local (private) IP addresses need to have their addresses translated, and it defines a pool of registered public IP addresses to  
allocate.  
Step 1. Use the be in the inside part of the NAT design (just like with static NAT). **ip nat inside** command in interface configuration mode to configure interfaces to  
Step 2. Use the be in the outside part of the NAT design (just like with static NAT). **ip nat outside** command in interface configuration mode to configure interfaces to  
Step 3. be performed.Configure an ACL that matches the packets entering inside interfaces for which NAT should  
Step 4. Use the global configuration mode to configure the pool of public registered IP addresses. **ip nat pool name first-address last-address netmask subnet-mask** command in

Step 5. Use theconfiguration mode to enable dynamic NAT. Note the command references the ACL (step 3) and **ip nat inside source list acl-number pool pool-name** command in global  
pool (step 4) per previous steps.

“misses,” as highlighted in the example. The first occurrence of this counter counts the number of times a new packet comes along, needing a NAT entry, and not finding one.

The second misses counter toward the end of the command output lists the number of misses in the pool. This counter increments only when dynamic NAT tries to allocate a new NAT table entry  
and finds no available addresses

**debug ip nat** packet has its address translated for NAT.command. This debug command causes the router to issue a message every time a

NAT Overload (PAT) Configuration  
If PAT uses a pool of inside global addresses, the configuration looks exactly like dynamic NAT, except the ip nat inside source list global command has an **overload** keyword added to the end. If  
PAT just needs to use one inside global IP address, the router can use one of its interface IP addresses  
configuration when using an interface IP address as the sole inside global IP address:  
Step 1. As with dynamic and static NAT, configure theto identify inside interfaces. **ip nat inside** interface sub-command  
Step 2. As with dynamic and static NAT, configure theto identify outside interfaces. **ip nat outside** interface subcommand  
Step 3. As with dynamic NAT, interfaces. configure an ACL that matches the packets entering inside  
Step 4. Configure the global configuration command, referring to the ACL created in step 3 and to the interface **ip nat inside source list acl-number interface type/number overload**  
whose IP address will be used for translations.

```
ip nat inside source list 1 interface serial 0/0/0 overload command has several parameters
The matching ACL 1 have their addresses translated. The list 1 parameter means the same thing as it does for dynamic NAT: inside local IP addresses interface serial 0/0/0 parameter means that
the only inside global IP address available is the IP address of the NAT router’s interface serial 0/0/0.
The router creates one NAT table entry for each unique combination of inside local IP address and port
```

NAT Troubleshooting  
Reversed inside and outside  
Static NAT: Check the address first and the inside global IP address second. **ip nat inside source static** command to ensure it lists the inside local

address first and the inside global IP address second.  
Dynamic NAT (ACL): Ensure that the ACL configured to match packets sent by the inside hosts match that host’s packets before any NAT translation has occurred.

Dynamic NAT (pool): For dynamic NAT without PAT, ensure that the pool has enough IP addresses\

A large or growing value in the second misses counter in thecommand output can indicate this problem. Also, compare the configured pool to the list of **show ip nat statistics**  
addresses in the NAT translation table the problem may be that the configuration intended to use PAT and is missing the overload **(show ip nat translations** ). Finally, if the pool is small,  
keyword  
PAT: It is easy to forget to add the overload option  
perhaps NAT has been configured correctly, but the packets. an ACL exists on one of the interfaces, discarding

IOS processes ACLs before NATafter translating the addresses with NAT.. For packets exiting an interface, IOS processes any outbound ACL

User traffic required  
IPv4 routing

4.0 IP Services  
4.7 Explain the forwarding percongestion, policing, shaping -hop behavior (PHB) for QoS such as classification, marking, queuing,

QoSthan storing and forwarding a message. defines these actions as per-hop behaviors (PHBs),which isa formal term to refer to actions other

## QoS: Managing Bandwidth, Delay, Jitter, and Loss

```
four characteristics of network traffic:
Bandwidth
refers to the speed of a link, in bits per second (bps)
helps to also think of bandwidth as the capacity of the link, in terms of how many bits can be sent over the link per second.
Delay
the time between sending one packet and that same packet arriving at the destination host
Round-trip delay
Jitter the time it takes to send one packet between two hosts and receive one back
variation in one-way delay between consecutive packets sent by the same application
Loss
the number of lost messages, usually as a percentage of packets sent.
people think of loss as something caused by faulty cabling or poor WAN services. That is one cause. However, more loss happens because of the normal operation of the
networking devices, in which the devices’ queues get too full, so the device has nowhere to put new packets, and it discards the packet.
```

Types of Traffic  
Data Applications

# 11 QoS

Friday, October 8, 2021 11:48 AM

Quality of Experience (QoE) -users’ perception of their use of the application on the  
network.  
Voice and Video Applications  
Aflowisall the data moving from one application to another over the network, with one  
flow for each direction  
For example, if you open a website and connect to a web server, the web page content that moves from the server to the client is one flow.  
From a voice perspective, a phone call between two IP phones would create a flow for each direction  
Step 1. The phone user makes a phone call and begins speaking.  
Step 2. A chip called a codec processes (digitizes) the sound to create a binary code (160  
bytes with the G.711 codec, for example) for a certain time period (usually 20 ms).  
Step 3. The phone places the data into an IP packet.  
Step 4. The phone sends the packet to the destination IP phone.

```
guidelines for interactive voice:
Delay (one-way): 150 ms or less
Jitter: 30 ms or less
Loss: 1% or less
```

requirements for video  
Bandwidth: 384 Kbps to 20+ Mbps  
Delay (one-way): 200–400 ms  
Jitter: 30–50 ms  
Loss: 0.1%–1%  
QoS as Mentioned in This Book  
“Classification and Marking” is about the marking of packets and the definition of trust  
boundaries.  
“Queuing” describes the scheduling of packets to give one type of packet priority over another.  
“Shaping and Policing” explains these two tools together because they are often used on opposite ends of a link.  
“devices get too busy.Congestion Avoidance” addresses how to manage the packet loss that occurs when network

Classification and Marking  
a type of QoS tool that by changing some bits in specific header fieldsclassifies packets based on their header contents then marks the message  
Classification Basics  
QoS tools sit in the path that packets take when being forwarded through a router or switch,  
much like the positioning of ACLs. Like ACLs, ACLs, QoS tools are enabled for a direction: packets entering the interface (before the QoS tools are enabled on an interface. Also like  
forwarding decision) or for messages exiting the interface (after the forwarding decision).  
classification refers to the process of matching the fields in a message to make a choice to  
take some QoS action  
QoS tools perform classification (matching of header fields) to decide which packets to take certain QoS actions against.Those actions include the other types of QoS tools discussed in  
this chapter, such as queuing, shaping, policing, and so on.

```
Matching (Classification) Basics
```

```
Cisco and by RFCs, suggests doing complex matching early in the life of a packet and then
marking the packet. Marking means that the QoS tool changes one or more header fields, setting a value in the header.
Differentiated Services Code Point (DSCP)
a 6-bit field in the IP header meant for QoS marking
```

Classification on Routers with ACLs and NBAR  
many QoS tools support the ability to simply refer to an IP ACL,with this kind of logic:  
For any packet matched by the ACL with a permit action, consider that packet a match for  
QoS, so do a particular QoS action.  
All these fields are matchable for QoS classification.

```
not every classification can be easily made by matching with an ACL. In more challenging cases, Cisco Network Based Application Recognition (NBAR)can be used. NBAR is basically in
its second major version, called NBAR2, or nextpackets for classification in a large variety of ways that are very useful for QoS.-generation NBAR. In short,NBAR2 matches
NBAR2 looks far beyond what an ACL can examine in a message
Cisco also organizes what NBAR can match in ways that make it easy to separate the traffic into different classes.
you might classify WebEx traffic and give it a unique DSCP marking. NBAR provides
easy builtof applications.-in matching ability for WebEx, plus more than 1000 different subcategories
NBAR refers to this idea of defining the characteristics of different applications as application signatures.)
```

```
application signatures.)
```

Marking IP DSCP and Ethernet CoS  
example plan  
Classify all voice payload traffic that is used for business purposes as IP DSCP EF and  
CoS 5.  
Classify all video conferencing and other interactive video for business purposes as IP DSCP AF41 and CoS 4.  
Classify all business-critical data application traffic as IP DSCP AF21 and CoS 2  
Marking the IP Header  
Marking a QoS field in the IP header works well with QoS because the IP header exists for the entire trip from the source host to the destination host.  
IPv4 defines a Type of Service (ToS) byte in the IPv4 headerThe original RFC defined a 3-bit IP Precedence (IPP) field for QoS marking. That field , as shown in Figure 11-6.  
gave us eight separate valueswhen converted to decimal are decimals 0 through 7.—binary 000, 001, 010, and so on, through 111—which

```
Those last 5 bits of the ToS byte per RFC 791 were mostly defined for some purpose but were not used in practice to any significant extent.
```

DSCP increased the number of marking bits to 6 bits, allowing for64 unique values  
that can be marked. The DiffServ RFCs, which became RFCs back in the late 1990s, have become accepted as the most common method to use when doing QoS, and  
using the DSCP field for marking has become quite common.  
IPv6 has a similar field to mark as well.The 6-bit field also goes by the name DSCP,  
with the byte in the IPv6 header being called the IPv6 Traffic Class byte.  
Marking the Ethernet 802.1Q Header  
marking field exists in the 802.1Q header  
It goes bytwo different names:Class of Service, orCoS, and Priority Code Point, or  
PCP.  
sits in the third byte of the 4possible valuesto mark (see Figure 11-byte 802.1Q header, as a 3-7). It goes by two different names: Class of -bit field,supplying eight  
Service, or CoS, and Priority Code Point, or PCP.

```
802.1Q header is not included in all Ethernet frames
only exists when 802.1Q trunking is used on a link
only for QoS features enabled on interfaces that use trunking, as shown
```

Other Marking Fields

Defining Trust Boundaries  
most voice traffic is marked with a DSCP called Expediteddecimal value of 46 Forwarding (EF), which has a  
trust boundary  
the point in the path of a packet flowing through the network at which the networking devices can trust the current QoS markings

```
when the access layer includes an IP Phone, the phone is typically the trust boundary
IP Phones can set the CoS and DSCP fields of the messages created by the phone, as
well as those forwarded from the PC through the phone. are actually configured on the attached access switch The specific marking values
```

DiffServ Suggested Marking Values  
DiffServ architecture as defined originally by RFC 2475  
three sets of DSCP values as used in DiffServ.  
Expedited Forwarding (EF)  
Expedited Forwarding (EF) DSCP value—a single value  
use for packets that need low latency (delay), low jitter, and low loss.  
decimal 46  
Most often QoS plans use EF to mark voice payloadpackets. With voice calls, some  
packets carry voice payload, and other packets carry call signaling messages.signaling messages set up (create) the voice call between two devices, and they do not Call  
require low delay, jitter, and loss.  
By default, Cisco IP Phones mark voice pay-load with EF,and mark voice signaling  
packets sent by the phone with another value called CS3.  
Assured Forwarding (AF)  
Thmeant to be used in concert with each othere Assured Forwarding (AF) DiffServ RFC (2597) defines a set of 12 DSCP values  
defines the defines three levels of drop priority within each queue for use with congestion concept of four separate queues in a queuing system. Additionally, it  
avoidance tools.need 12 different DSCP markings, one for each combination of queue and drop With four queues, and three drop priority classes per queue, you  
priority. (Queuing and congestion avoidance mechanisms are discussed later in this  
chapter.)  
and Y referring to the drop priority (1 through 3).The text names follow a format of AFXY, with X referring to the queue (1 through 4)

```
Class Selector (CS)
eight DSCP values for backward compatibility with IPP values.
The DSCP values have the last 3 bits, as shown on the left side of the figure. CSx represents the text names, same first 3 bits as the IPP field, and with binary 0s for the
where x is the matching IPP value (0 through 7).
```

Guidelines for DSCP Marking Values  
how all devices should mark data  
DSCP EF: Voice payload  
AF4x: Interactive video (for example, videoconferencing)  
AF3x: Streaming video  
AF2x: High priority (low latency) data  
CS0: Standard data  
Queuing

```
interfacethe QoS toolset for managing the queues that hold packets while they wait their turn to exit an
```

To use multiple queues, the queuing system needs a classifierfunction to choose which packets  
are placed into which queue  
The queuing system needs a interface becomes availablescheduleras well, to decide which message to take next when the

Prioritizationrefers to the concept of giving priority to one queue over another  
Round-Robin Scheduling (Prioritization) (Two Types)  
weighting  
the more preference to one queue over another.scheduler takes a different number of packets (or bytes) from each queue, giving  
Class-Based Weighted Fair Queuing (CBWFQ)  
Each class receives at least the amount of bandwidth configured during times of congestion, but maybe more

Low Latency Queuing

```
tells the scheduler to treat one or more queues as special priority queues
```

if thethe voice queue? The scheduler never services the other queues (calledspeed of the interface is X bits per second, but more than X bits per second come into queue starvation).  
limit the amount of traffic placed into the priority queue, using a feature called policing  
a cap on the bandwidth used by the priority queue  
Call Admission Control (CAC) tools  
Find a way to this link, so that the policer never discards any of the trafficlimit the amount of voice and video that the network routes out  
CAC tools did not get a mention in the exam topics, so this chapter leaves those  
tools at a brief mention  
A Prioritization Strategy for Data, Voice, and Video  
approach queuing in their QoS plans:  
Key Topic.

```
Use a round-robin queuing method like CBWFQ for data classes and for noninteractive voice
and video.
If faced with too little bandwidth compared to the typical amount of traffic, give data classes that support business-critical applications much more guaranteed bandwidth than is given
to less important data classes.
Use a priority queue with LLQ scheduling for interactive voice and video, to achieve low
delay, jitter, and loss.
Put voice in a separate queue from video so that the policing function applies separately to each.
Define enough bandwidth for each priority queue so that the builtdiscard any messages from the priority queues. -in policer should not
Use Call Admission Control (CAC) tools to avoid adding too much voice or video to the
network, which would trigger the policer function.
```

### Shaping and Policing

```
not found in as many locations in a typical enterprise
often used at the WAN edge in an enterprise network design.
monitor the bit rate of the combined messages that flow through a device.
notes each packet that passes and measures the number of bits per second over time
attempt to keep the bit rate at or below the configured speed
policersdiscard packets,and shapershold packets in queues to delay the packets.
Does this next packet push the measured rate past the configured shaping rate or policing rate?
If no:
Let the packet keep moving through the normal path and do nothing extra to the packet.
If yes:
If shaping, delay the message by queuing it.
If policing, either discard the message or mark it differently.
policing, which discards or rewhich slows down messages that exceed the shaping rate.-marks messages that exceed the policing rate, followed by shaping,
```

#### Policing

Policers activity.allow for a burst beyond the policing rate for a short time, after a period of low

Where to Use Policing  
Policing makes sense only in certain cases, and as a general tool, it can be best used at  
the edge between two networks.

```
a 200-Mbps committed information rate (CIR).
the Mbps of traffic in each directionSP providing the WAN service agrees to allow the enterprise to send 200. However, remember that the enterprise
routers transmit the data at the speed of the access link, or 1 Gbps in this case.
Thethat the customer chooses for that link.SP can police incoming packets, setting the policing rate to match the CIR
Policers can also re-mark packets.
SP could mark the messages with a new marking value, with this strategy:
Renetwork.-mark packets that exceed the policing rate, but let them into the SP’s
If other SP network devices are experiencing congestion when they process the packet, the different marking means that device can discard the packet.
However...
...if no other SP network devices are experiencing congestion when forwarding that re-marked packet, it gets through the SP network anyway.
```

```
that re-marked packet, it gets through the SP network anyway.
SP canstill protecting the SP’s network during times of stress.treat their customers a little better by discarding less traffic, while
key features of policing:
Key Topic.
It rate.measures the traffic rate over time for comparison to the configured policing
It allows for a burst of data after a period of inactivity.
It is enabled on an interface, in either direction, but typically at ingress.
It cancandidate for more aggressive discard later in its journey.discard excess messages but can also re-mark the message so that it is a
```

```
Use a shaper to slow down the traffic
shaping before sending data to an SP that is policing—is one of the typical uses of a shaper
slows messages down by queuing the messages.
then services the shaping queues, but not based on when the physical interface is available
schedules messages from the shaping queues based on the shaping rate
the shaper queues packets so that the sending rate through the shaper does not exceed the shaping rate; and then output queuing works as normal, if needed.
```

```
shaping queuesapply the round-robin and priority queuing features of CBWFQ and LLQ, respectively, to the
```

###### Setting a Good Shaping Time Interval for Voice and Video

```
you can (and should) configure a shaper’s setting that changes the internal operation of the shaper, which then reduces the delay and jitter caused to voice and video
traffic.
```

#### Shaping

```
traffic.
A shaper’s time interval refers to its internal logic and how a shaper averages, over time, sending at a particular rate
Because the interface transmits bits at 1 Gbps, it takes just .2 seconds, or 200 ms, to send all 200 million bits. Then the shaper must wait for the rest of the
time interval, another 800 ms, before beginning the next time interval.
```

```
configure a short time interval so there is less wait time
Tc = 1 second (1000 ms): Send at 1 Gbps for 200 ms, rest for 800 ms
Tc = .1 second (100 ms): Send at 1 Gbps for 20 ms, rest for 80 ms
Tc = .01 second (10 ms): Send at 1 Gbps for 2 ms, rest for 8 ms
When shaping, use a short time interval. By recommendation, use a interval to support voice and video. 10 - ms time
key features of shapers:
Key Topic.
Shapers measure the traffic rate over time for comparison to the configured shaping rate.
Shapers allow for bursting after a period of inactivity.
Shapers areenabled on an interface for egress (outgoing packets).
Shapers slow down packets by queuing them and over time releasing them from the queue at the shaping rate.
Shapers use queuing tools to create and schedule the shaping queues, which is very
important for the same reasons discussed for output queuing.
```

#### Congestion Avoidance

```
attempts to reduce overall packet loss by preemptively discarding some packets used in TCP connections
```

connections  
TCP Windowing Basics  
tail drop  
one queue being totally full. Any new packets that arrive for that queue right now will  
be dropped because there is no room at the tail of the queue (tail drop).

Congestion Avoidance Tools  
discard some TCP segments before the queues fill, hoping that enough TCP connections will  
slow down, reducing congestion, and avoiding tail drop  
monitor the average queue depth over time, triggering more severe actions the deeper the  
queue  
the queue depth passes the maximum thresholdcalled full drop. ,the tool drops all packets, in an action  
congestion avoidance tools can classify messages to treat some packets better than others

```
3.0 IP Connectivity
3.5 Describe the purpose of First Hop Redundancy Protocol
4.0 Infrastructure Services
4.4 Explain the function of SNMP in network operations
4.9 Describe the capabilities and function of TFTP/FTP in the network
```

## First Hop Redundancy Protocol

# 12 IP Services

Monday, October 25, 2021 8:33 AM

All hosts act like they always have, with one default router setting that never has to change.  
The default routers share a virtual IP address in the subnet, defined by the FHRP.  
Hosts use the FHRP virtual IP address as their default router address.  
The routers exchange FHRP protocol messages so that both agree as to which router does what work at any point in time.  
When a router fails or has some other problem, the routers use the FHRP to choose which router  
takes over responsibilities from the failed router.  
The Three Solutions for First-Hop Redundancy  
First Hop Redundancy Protocol does not name any one protocol. Instead, it names a family of  
protocols that fill the same role

HSRP Concepts  
operates with an active/standby model(also more generally called active/passive  
allows two (or more) routers to cooperate

HSRP Failover

```
To make the switches change their MAC address table entries for VMAC1, R2 sends an Ethernet frame with VMAC1 as the source MAC address.
he frame is also a LAN broadcast, so all the switches learn a MAC table entry for VMAC1 that leads toward R2.
```

HSRP Load Balancing  
you canconfigure multiple instances of HSRP in the same subnet (called multiple HSRP groups),  
preferring one router to be active in one group and the other router to be preferred as active in another.

```
FHRPs are needed on any device that acts as a default router,
includes both traditional routers and Layer 3 switches.
```

#### Simple Network Management Protocol

```
SNMPv2c and SNMPv3
```

application layer protocol  
provides a message format for communication between what are termed managers and agents  
manager  
a network management application running on a PC or server  
typically being called a Network Management Station (NMS)  
uses SNMP protocols to communicate with each SNMP agent.  
Cisco Primeseries of management products (www.cisco.com/go/prime) use SNMP (and  
other protocols) to manage networks.  
agents  
exist in the network, one per device that is managed.  
software running inside each device (router, switch, and so on), with knowledge of all the  
variables on that device that describe the device’s configuration, status, and counters.  
keeps a operations of the device.database of variables that make up the parameters, status, and counters for the This database, called the Management Information Base (MIB)  
IOS on routers and switches include an SNMP agent, with builtwith the configuration shown later -in MIB, that can be enabled

SNMP Variable Reading and Writing: SNMP Get and Set  
NMS typically polls the SNMP agent on each device  
NMS can notify the human user in front of the PC or send emails, texts, and so on to notify  
the network operations staff of any issues identified by the data found by polling the devices. You can even reconfigure the device through these SNMP variables in the MIB if  
you permit this level of control.  
NMS uses the SNMPGet messages)to ask for information from an agent.Get, GetNext, and GetBulk messages(together referenced simply as  
NMS sends an SNMP Set message to write variables on the SNMP agent as a means to change the configuration of the device.

```
change the configuration of the device.
messages come in pairs, with, for instance, a Get Request asking the agent for the contents of a variable, and the Get Response supplying that information
```

```
NMS can analyze various statistical facts such as averages, minimums, and maximums
NMS can set thresholds for certain key variables, telling the NMS to send a notification (email, text, and so on) when a threshold is passed.
```

SNMP Notifications: Traps and Informs  
SNMP agents can initiate communications to the NMS.  
generally called notifications, use two specific SNMP messages: Trap and Inform  
SNMP agents MIB variables when those variables reach a certain state.send a Trap or Inform SNMP message to the NMS to list the state of certain

```
SNMP Traps and Inform messages have the exact same purpose but differ in the protocol mechanisms
trap
The SNMP agent transport protocol as with all SNMP messages,sends the Trap to the IP address of the NMS, with UDP as the
less overhead than inform
Inform
```

```
Like Trap messages but with reliability added
Added to the protocol with SNMP Version 2 (SNMPv2),
use UDP but add application layer reliability
NMS must acknowledge receipt of the Inform with an SNMP Response message, or the SNMP agent will time out and resend the Inform.
```

The Management Information Base  
Every SNMP agent has its own Management Information Base  
defines variables whose values are set and updated by the agent  
enable the management software to monitor/control the network device.  
defineseach variable as an object ID (OID)  
organizes the OIDs based in part on RFC standards, and in part with vendor-proprietary  
variables  
organizes all the variables into a hierarchy of OIDs, usually shown as a tree  
Each node in the tree can be described based on the tree structure sequence, either by name or by number.

you could use an SNMP manager and type MIB variable 1.3.6.1.4.1.9.2.1.58.0 and click a  
button to get that variable, to see the current CPU usage percentage from a Cisco router  
Securing SNMP

Securing SNMP  
use ACLs to limit SNMP messages to those from known servers only.  
can configure an IPv4 ACL to filter incoming SNMP messages that arrive in IPv4 packets and an IPv6 ACL to filter SNMP messages that arrive in IPv6 packets.  
all versions of SNMP support a basic clear-text password mechanism,  
SNMPv1 defined clear-text passwords called SNMP communities.  
SNMP agent and the SNMP manager need prior knowledge of the same SNMP community value (called a community string)  
Get messages and the Set message include the appropriate community string value, in clear text.  
NMS sends a Get or Set with the correct community string, as configured on the  
SNMP agent, the agent processes the message.  
SNMPv1 defines both a read-only community and a read-write community.  
read-only (RO) community allows Get messages, and the read-write (RW)  
community allows both reads and writes (Gets and Sets).

```
SNMPv2, and the related Community-based SNMP Version 2 (SNMPv2c)
The original specifications for SNMPv2 did not include SNMPv1 communities
SNMPv3
security had arrived with the powerful network management protocol. away with communities and replaces them with the following features:SNMPv3 does
Message integrity:This mechanism, applied to all SNMPv3 messages, confirms
whether or not each message has been changed during transit.
Authentication:and password,withThis optional feature the password never sent as clear text. Instead, it uses a adds authentication with both a username
hashing method like many other modern authentication processes.
Encryption (privacy): This optional feature encrypts the contents of SNMPv3
messages so that attackers who intercept the messages cannot read their contents.
```

#### FTP and TFTP

```
Opaque:and commandsTo represent logical internal file systems for the convenience of internal functions
Network: To represent external file systems found on different types of servers for the
convenience of reference in different IOS commands
Disk: For flash
Usbflash: For USB flash
NVRAM: A special type for NVRAM memory, the default location of the startup-config file
the command more flash0:/wotemp/fred woulddisplay the contents of file fred in directory
/wotemp in the first flash memory slot in the router.
many commands use a keyword that indirectly refers to a formal filename, to reduce typing.For
example:
```

example:  
**show running-config** command:Refers to file system:running-config  
**show startup-config** command: Refers to file nvram:startup-config  
**show flash** command: Refers to default flash IFS (usually flash0:)

###### Upgrading IOS Images

```
process to upgrade an IOS image into flash memory, using the following steps:
Step 1.Obtain the IOS image from Cisco, usually by downloading the IOS image from
Cisco.com using HTTP or FTP.
Step 2. Place the IOS image someplace that the router can reach. Locations include
TFTP or FTP servers in the network or a USB flash drive that is then inserted into the router.
Step 3. Issue the copy command from the router, copying the file into the flash
memory that usually remains with the router on a permanent basis. (Routers usually cannot boot from the IOS image in a USB flash drive.)
```

```
Copying a New IOS Image to a Local IOS File System Using TFTP
```

```
copy command
```

copy command  
works through these kinds of questions:  
What is the IP address or host name of the TFTP server?  
What is the name of the file?  
Ask the server to learn the size of the file, and then check the local router’s flash  
to ask whether enough space is available for this file in flash memory.  
Does the server actually have a file by that name?  
Do you want the router to erase any old files in flash?  
Afterward  
verifies that the checksum for the file shows that no errors occurred  
view the contents of the flash file system  
**show flash**  
shows the files in the default flash file system (flash0:)

```
dir flash0 : commandlists the contents of that same file system, with similar
information.IFS.) (You can use the dircommand to display the contents of any local
```

```
show flash(bytes used plus bytes free).lists the bytes used, whereas the know which command lists which particular total.dir command lists the total bytes
```

Verifying IOS Code Integrity with MD5  
when Cisco builds a new IOS image, it calculates and publishes an MD5 hash value for  
that specific IOS file.  
IOS **verify** command.  
will list the MD5 hash as recalculated on your router. If both MD5 hashes are  
equal, the file has not changed.

```
verify /md5 commandgenerates the MD5 hash on your router,
you can include the hash value computed by Cisco as the last parameter (as
shown in the example), or leave it offlocally computed value matches what you copied into the command. If you. If you include it, IOS will tell you if the
leave it out, the verify command lists the locally computed MD5 hash, and you
```

```
leave it out, the verify command lists the locally computed MD5 hash, and you have to do the picky character-by-character check of the values yourself.
```

Copying Images with FTP

```
copy ftp flash
```

```
can configure the FTP username and password on the router so that you do not
have to include them in the copy command. For instance, the global
```

have to include them in the configuration commands **ip ftp username wendellcopy** command. For instance, the global and **ip ftp password odom**  
would have configured those values.  
The FTP and TFTP Protocols  
copycommand, when using the tftp or ftp keyword, makes the command act as a client  
FTP ProtocolBasics  
uses TCP  
TCP port 21 and in some cases also well-known port 20.  
FTP uses a client/server model for file transfer

```
FTP control connection—define the kinds of functions supported by FTP
allow the client to navigate around the directory structures of the server, list files, and
then transfer files from the server (FTP GET) or to the server (FTP PUT).
summary of some of the FTP actions:
Navigate directories : List the current directory, change the current directory to
a new directory, go back to the home directory, all on both the server and client side of the connection.
Add/remove directories: Create new directories and remove existing
directories on both the client and server.
List files : List files on both the client and server.
File transfer: Get (client gets a copy of the file from the server), Put (client takes
a file that exists on the client and puts a copy of the FTP server).
FTP Active and Passive Modes
may impact whether the TCP client can or cannot connect to the server and
perform normal functions
user at the FTP client can choose which mode to use
FTP passive mode may be the more likely option to work.
FTP uses two types of TCP connections:
```

FTP uses two types of TCP connections:  
Control Connection: Used to exchange FTP commands  
Data Connection: Used for sending and receiving data, both for file transfers and for output to display to a user

when a client connects to an FTP server, the client first creates the FTP control connection

server listens for new control connections on its well-known port 21  
client allocates any new dynamic port (49222 in this case) and creates a TCP connection to the server

```
The FTP client allocates a currently unused dynamic port and starts
listening on that port.
The client identifies that port (and its IP address) to the FTP server by
sending an FTP PORT command to the server.
The server, because it also operates in active mode, expects the PORT command; the server reacts and initiates the FTP data connection to the
client’s address (192.168.1.102) and port (49333).
```

Passive mode helps solve the firewall restrictions by having the FTP client  
initiate the FTP data connection to the server.  
passive mode does not simply cause the FTP client to connect to a well-known  
port on the server;  
The FTP client changes to use FTP passive mode, notifying the server using the FTP PASV command.  
The server chooses a port to listen on for the upcoming new TCP

```
The server chooses a port to listen on for the upcoming new TCP connection, in this case TCP port 49444.
The FTP notifies the FTP client of its IP address and chosen port with the
FTP PORT command.
The FTP client opens the TCP data connection to the IP address and port
learned at the previous step.
```

FTP over TLS (FTP Secure)  
FTPS encrypts both the control and data connections with TLS, including the exchange of the usernames and passwords  
**FTPS explicit mode process:**  
The client creates the FTP control TCP connection to server well-known port 21.  
The client initiates the use of TLS in the control connection with the FTP AUTH command.  
When the user takes an action that requires an FTP data connection, the client  
creates an FTP data TCP connection to server well-known port 21.  
The client initiates the use of TLS in the data connection with the FTP AUTH  
command.

```
implicit mode process
begins with a required TLS connection, with no need for an FTP AUTH
command, using wellthe data connection).-known ports 990 (for the control connection) and 989 (for
SFTP
uses SSH to encrypt file transfers over an SSH connection. However, the acronym SFTP does not refer to a secure version of FTP.
```

**TFTP Protocol Basics**  
Trivial File Transfer Protocol uses UDP well-known port 69. Because it uses UDP, TFTP adds a  
feature to check each file for transmission errors by using a checksum process on each file after the transfer completes.  
the code requires less space to install, which can be useful for devices with limited memory.  
can Get and Put files, but it includes no commands to change directories, create/remove directories, or even to list files on the server.  
does not support even simple clearit should accept requests from any TFTP client.-text authentication. In effect, if a TFTP server is running,

```
1.2 Describe characteristics of network topology architectures
1.2.a 2 tier
1.2.b 3 tier
1.2.e Small office/home office (SOHO)
1.3 Compare physical interface and cabling types
1.3.c Concepts of PoE
```

```
Two-Tier Campus Design (Collapsed Core)
access, distribution, and core.
```

```
Access switches connect directly to end users,
Distribution switches provide a path through which the access switches can forward traffic to
each other
each of the access switches connects to at least one distribution switch, typically to two
distribution switches for redundancy.
most designs use at least two uplinks to two different distribution switches (as shown in Figure 13 - 1) for redundancy.
Provides a place to connect end-user devices (the access layer, with access switches)
Connects the switches with a reasonable number of cables and switch ports by connecting all 40 access switches to two distribution switches
```

# 13 LAN Architecture

Monday, October 25, 2021 11:51 AM

```
Star: A design in which one central device connects to several others, so that if you
drew the links out in all directions, the design would look like a star with light shining in all directions.
```

```
Topology Terminology Seen Within a Two-Tier Design
```

```
Full mesh: For any set of network nodes, a design that connects a link between each pair of nodes.
Partial mesh: For any set of network nodes, a design that connects a link between
some pairs of nodes, but not all. In other words, a mesh that is not a full mesh.
Hybrid: A design that combines topology design concepts into a larger (typically more
complex) design.
twoand a partial mesh at the distribution layer.-tier design is indeed a hybrid design that uses both a star topology at the access layer
```

```
The distribution layer creates a partial mesh.
none of the access layer switches connect to each other.
```

Three-Tier Campus Design (Core)

Three-Tier Campus Design (Core)  
collapsed core refers to the fact that the two-tier design does not have a third tier, the core tier

```
Sometimes the center of the network uses a full mesh, sometimes a partial mesh, depending on
the availability of cables between the buildings.
provide one function: to connect the distribution switches.
```

```
Access: Provides a connection point (access) for endbetween two other access switches under normal circumstances.-user devices. Does not forward frames
Distribution: Provides an aggregation point for access switches, providing connectivity to the rest
of the devices in the LAN, forwarding frames between switches, but not connecting directly to end-user devices.
```

Core: Aggregates distribution switches in very large campus LANs, providing very high forwarding  
rates for the larger volume of traffic due to the size of the network.  
Topology Design Terminology

```
the right side of Figure 13-6 combines the star topology of the access layer with the partial mesh
of the distribution layer. So you might hear these designs that combine concepts called a hybrid design.
```

###### Small Office/Home Office

```
that one wireless router acts like separate devices you would find in an enterprise campus:
Key Topic.
An Ethernet switch, for the wired Ethernet connections
A wireless access point (AP), to communicate with the wireless devices and forward the frames to/from the wired network
A router, to route IP packets to/from the LAN and WAN (Internet) interfaces
A firewallbut not vice versa, which often defaults to allow only clients to connect to servers in the Internet,
```

#### Power over Ethernet (PoE)

```
a LAN switch, acts as the Power Sourcing Equipment (PSE
supplies DC power so the device does not need an AC/DC converter.
A device that has the capability to be powered over the Ethernet cable
is called the Powered Device (PD)
```

```
PoE Operation
PoE must (and does) have processes in place to determine if PoE is needed, and for how much power, before applying any potentially harmful power levels to the circuit.
autonegotiation mechanisms need to work before the PD has booted,
By using these IEEE autonegotiation messages and watching for the return signal levels, PoE
can determine whether the device on the end of the cable requires power (that is, it is a PD) and how much power to supply
Step 1. the device needs power.Do not supply power on a PoE-capable port unless negotiation identifies that
Step 2. Use Ethernet autonegotiation techniques, sending low power signals and
monitoring the return signal, to determine the PoE power class, which determines how much power to supply to the device.
Step 3allows the device to boot.. If the device is identified as a PD, supply the power per the power class, which
Step 4. Monitor for changes to the power class, both with autonegotiation and
listening for CDP and LLDP messages from the PD.
```

```
listening for CDP and LLDP messages from the PD.
Step 5.If a new power class is identified, adjust the power level per that class.
PDs signaling how many watts of power they would like to receive from the PSon the specific PoE standard, the PSE will then supply the power, either over two pairs or E. Depending
four pairs, as noted in Table 13-2.
```

PoE and LAN Design  
some of the key points to consider when planning a LAN design that includes PoE:  
**Powered Devices:** power requirements.Determine the types of devices and specific models, along with their  
**Power Requirements** : Plan the numbers of different types of PDs to connect into each  
wiring closet to build a power budget. That power budget can then be processed to determine the amount of PoE power to make available through each switch.  
Sa subset of ports. Research the various switch models so that you purchase enough PoE **witch Ports** : Some switches support PoE standards on all ports, some on no ports, some on -  
capable ports for the switches planned for each wiring closet.  
**Switch Power Supplies** so that it delivers enough power to power the switch itself. With PoE, the switch acts as a : Without PoE, when purchasing a switch, you choose a power supply  
distributor of electrical power, so the switch power supply must deliver many more watts than it needs to run the switch itself. You will need to create a power budget per switch,  
based on the number of connected PDs, and purchase power supplies to match those  
requirements.  
**PoE Standards versus Actual** standards they support, the standards supported by the PDs, and how much power they : Consider the number of PoE switch ports needed, the  
consume. For instance, a PD and a switch port may both support PoE+, which supports up to 30 watts supplied by the PSE. However, that powered device may need at most 9 watts

to 30 watts supplied by the PSE. However, that powered device may need at most 9 watts to operate, so your power budget needs to reserve less power than the maximum for those  
devices.