```
This chapter covers the following exam topics:
3.0 IP Connectivity
3.2 Determine how a router makes a forwarding decision by default
3.2.b Administrative distance
3.2.c Routing protocol metric
3.4 Configure and verify single area OSPFv
3.4.a Neighbor adjacencies
3.4.b Point-to-point
3.4.c Broadcast (DR/BR selection)
3.4.d Router ID
Comparing Dynamic Routing Protocol Features
Routers add IP routes to their routing tables using routes, and routes learned by using dynamic routing protocols.three methods: connected routes, static
Routing protocol:overall purpose of learning routes. This process includesA set of messages, rules, and algorithms used by routers for the the exchange and analysis of
routing information. Each router chooses the best route to each subnet (path selection) and finally places those best routes in its IP routing table. Examples include RIP, EIGRP,
OSPF, and BGP.
```

##### •

```
Routed protocol and routable protocolpacket structure and logical addressing, allowing routers to forward or route the packets. :Both terms refer to a protocol that defines a
Routers forward packets defined by routed and routable protocols. Examples includeVersion 4 (IPv4) and IP Version 6 (IPv6). IP
```

##### •

#### path selectionthe routing protocol chooses the best route.sometimes refers to part of the job of a routing protocol, in which

```
Routing Protocol Functions
Learn routing information about IP subnets from neighboring routers.
Advertise routing information about IP subnets to neighboring routers.
If more than one possible route exists to reach one subnet, pick the best route based on a
metric.
```

# 19 OSPF Concepts

Thursday, August 26, 2021 1:37 PM

```
metric.
If the network topology changeshave failed and pick a new currently best route. (This process is called convergence.)—for example, a link fails—react by advertising that some routes
```

```
IP routing protocols fall into one of two major categories: interior gateway protocols (IGP) or exterior gateway protocols (EGP).
IGP: A routing protocol that was designed and intended for use inside a single autonomous
system (AS)
EGP:A routing protocol that was designed and intended for use between different autonomous
systems
AnAS is a network under the administrative control of a single organization.
routing protocols designed to exchange routes between routers in different autonomous systems are called EGPs. Today, Border Gateway Protocol (BGP) is the only EGP used.
```

Interior and Exterior Routing Protocols

IGP Routing Protocol Algorithms  
Distance vector (sometimes called Bellman-Ford after its creators)  
Advanced distance vector (sometimes called “balanced hybrid”)  
Link-state (OSPF)  
Routing Information Protocol(RIP)was the first popularly used IP distance vector protocol, with  
theCisco-proprietary Interior Gateway Routing Protocol (IGRP)being introduced a little later.  
proprietary routing protocol called Enhanced Interior Gateway Routing Protocol(EIGRP)  
it used more distance vector features than link-state, so it is more commonly classified as  
anadvanced distance vector protocol.

```
Routing protocols choose the best route to reach a subnet by choosing the route with the metric lowest
RIP usesa counter of the number of routers(hops) between a router and the destination subnet
OSPF totals the cost on link bandwidth associated with each interface in the end-to-end route, with the cost based
```

Metrics

```
The interface. It just tells IOS what speed to assume the interface is using.) bandwidth interface subcommanddoes not change the actual physical speed of the
```

Other IGP Comparisons

```
Classless routing protocols support variablesummarization (supernetting)by sending routing protocol messages that include the subnet -length subnet masks (VLSM) as well as manual route
masks in the messageprotocols—do not.. The older RIPv1 and IGRP routing protocols—both classful routing
```

```
If one company uses OSPF and the other uses EIGRP on at least one router, both OSPF and EIGRP
```

Administrative Distance

If one company uses OSPF and the other uses EIGRP on at least one router, both OSPF and EIGRP must be used. Then thatrouter can take routes learned by OSPF and advertise them into EIGRP,  
and vice versa, through a process called route redistribution.  
When a single routing protocol learns multiple routes to the same subnet, the metric tells it which route is best. However,when two different routing protocols learn routes to the same  
subnet, because each routing protocol’s metric is based on different information, IOS cannot  
compare the metrics  
When IOSconcept called administrative distancemust choose between routes learned using different routing protocols, IOS uses a .Administrative distanceis a number that denotes how  
believable an entire routing protocol is on a single routermore believable, the routing protocol. For example, RIP has a default administrative distance of .The lower the number, the better,or  
120, OSPF uses a default of 110, and EIGRP defaults to 90. When using OSPF and EIGRP, the  
router will believe the EIGRP route instead of the OSPF route (at least by default).administrative distance values are configured on a single router and are not exchanged with The  
other routers

The **show ip route** command lists each route’s administrative distance as the first of the two  
numbers inside the brackets. The second number in brackets is the metric  
IOSparticular route, or even a static route.can be configured to change the administrative distance of a particular routing protocol, a

particular route, or even a static route.  
For example, the commandwith a default administrative distance of 1 **ip route 10.1.3.0 255.255.255.0 10.1.130.253** , but the command **ip route 10.1.3.0 255.255.255.0** defines a static route  
**10.1.130.253 210** defines the same static route with an administrative distance of 210  
Topology Information and LSAs  
Each LSA is a data structure with some specific information about the network topology; the  
LSDB is simply the collection of all the LSAs known to a router.  
before sending an LSA to yet another neighbor, routers communicate, asking “Do you already have this LSA?,” and then sending the LSA to the next neighbor only if the neighbor has not yet  
learned about the LSA.  
Routers reflood an LSA when some information changes(for example, when a link goes up or  
comes down). They also minutes). reflood each LSA based on each LSA’s separate aging timer(default 30

Applying Dijkstra SPF Math to Find the Best Routes  
Becoming neighbors:created so that the neighboring routers have a means to exchange their LSDBs.A relationship between two routers that connect to the same data link,  
Exchanging databases: The process of sending LSAs to neighbors so that all routers learn the  
same LSAs.  
Adding the best routes: The process of each routerindependently running SPF, on their local  
copy of the LSDB, calculating the best routes, and adding those to the IPv4 routing table.  
The Basics of OSPF Neighbors  
OSPF neighbors are routers that both use OSPF and both sit on the same data link.can become OSPF neighbors if connected to the same VLAN, or same serial link, or same Two routers  
Ethernet WAN link.  
they must send OSPF messages and agree to become OSPF neighbors.To do so, therouters send  
OSPF Hello messages, introducing themselves to the potential neighbor. Assuming the two potential neighbors have compatible OSPF parameters, the two form an OSPF neighbor  
relationship, and would be displayed in the output of the **show ip ospf neighbor** command.  
allows new routers to be dynamically discovered. That means new routers can be added to a  
network without requiring every router to be reconfiguredHello messages from new routers and react to those messages, attempting to become neighbors. Instead, OSPF routers listen for OSPF  
and exchange LSDBs.  
Meeting Neighbors and Learning Their Router ID  
process starts with messages called OSPF Hello messages. The Hellos in turn list each router’s  
router ID (RID), which serves as each router’s unique name or identifier for OSPF. does several checks of the information in the Hello messages to ensure that the two routers Finally, OSPF  
should become neighbors.  
OSPF RIDs are 32 - bit numbers.

OSPF RIDs are 32 - bit numbers.  
By default, IOS chooses one of the router’s interface IPv4 addresses to use as its OSPF RID.However, the OSPF RID can be directly configured

As soonmeet its OSPF neighbors.as a router has chosen its OSPF RID and some interfaces come up, the router is ready to OSPF routers can become neighbors if they are connected to the same  
subnet. each interface and hopes to receive OSPF Hello packets from other routers connected to those To discover other OSPF-speaking routers, a router sends multicast OSPF Hello packets to  
interfaces.  
They messages themselves have the following features:continue to send Hellos at a regular interval based on their Hello timer settings. The Hello

TheHello messagefollows the IP packet header, withIP protocol type 89.  
Hello packets are sent toOSPF-speaking routers. multicast IP address 224.0.0.5, a multicast IP address intended for all

OSPF routers listen for packets sent to IP multicast address 224.0.0.5, in part hoping to receive Hello packets and learn about new neighbors.

Each router keeps an OSPF state variable for how it views the neighbor.

Hello. This message tells R1 that R2 exists, and it allows R1 to move through the init state and  
quickly to a 2-way state.  
The 2are true:-way state is a particularly important OSPF state. At that point, the following major facts

(^2) it is ready to begin a 2-way means that the router is available to exchange its LSDB with the neighbor.-way exchange of the LSDB. In other words,  
First, they tell each other a list of LSAs in their respective databases—not all the details of the  
LSAs, just a list. (Think of these lists as checklists.) Then each router can check which LSAs it already has and then ask the other router for only the LSAs that are not known yet.  
the OSPF messages that actually send the LSAs between neighbors are called Link(LSU) packets.That is, the LSU packet holds data structures called link-state advertisements -State Update  
(LSA). The LSAs are not packets, but rather data structures that sit inside the LSDB and describe the topology.  
Maintaining Neighbors and the LSDB  
First, the Hello Interval and the Dead Interval. routers monitor each neighbor relationship using Hello messages and two related timers:Routers send Hellos every Hello Interval to each  
neighbor.so if a neighbor is silent for the length of the Each router expects to receive a Hello from each neighbor based on the Hello Interval, Dead Interval (by default, four times as long as the  
Hello Interval),the loss of Hellos means that the neighbor has failed.  
Next, routers must react when the topology changes as well,

```
Next, routers must react when the topology changes as well,
Each router’s LSDB now reflects the fact that the original router’s G0/0 interface failed, so each router will then use SPF to recalculate any routes affected by the failed interface.
A third maintenance task done by neighbors is to reflood each LSA occasionally, even when the network is completely stable. By default, each router that creates an LSA also has the
responsibility to reflood the LSA every 30 minutes (the default), even if no changes occurthateach LSA has a separate timer, based on when the LSA was created, so there is no single big. (Note
event where the network is overloaded with flooding LSAs.)
```

```
On Ethernet links, OSPF defaults to use a network type of broadcastone of the routers on the same subnet to act as the designated router (DR). , which causes OSPF to elect
These five OSPF routers elect one router to act as the DR and one router to be a backup DR
(BDR).
The database exchange process on an Ethernet link does not happen between every pair of
routers on the same VLAN/subnet. Instead, it happens between the DR and each of the other routers,with the DR making sure that all the other routers get a copy of each LSA.
The BDR watches the status of the DR and takes over for the DR if it fails. (When the DR fails, the
BDR takes over, and then a new BDR is elected.)
TheDR can send a packet to all OSPF routers in the subnet by using multicast IP address
224.0.0.
The each router.DR can send one set of messages to all the OSPF routers rather than sending one message to
atake over for the DR) can send those messages to theny OSPF router needing to send a message to theDR and also to the BDR“All SPF DRs” multicast address 224.0.0.6.(so it remains ready to
routers that are neither a DR nor a BDR—called DROthersby OSPF—never reach a full state
because they do not exchange LSDBs directly with each other.
full state(called fully adjacent neighbors
2 - way state(called neighbors)
all OSPF routers on the same link that reach the 2-way state—that is, they send Hello
messages and the parameters match—are called neighbors. The subset of neighbors for
```

Using Designated Routers on Ethernet Links

```
messages and the parameters matchwhich the neighbor relationship continues on and reaches the full state are called adjacent —are called neighbors. The subset of neighbors for
neighbors.
```

OSPF Areas and LSAs  
A larger topology database requires more memory on each router.  
TheSPF algorithm requires processing power that grows exponentially compared to the size of  
the topology database.  
A single interface status change anywhere in the internetwork (up to down, or down to up)  
forces every router to run SPF again!

```
Put all interfaces connected to the same subnet inside the same area.
An area should be contiguous.
Some routers may be internal to an area, with all interfaces assigned to that single area.
Some routers may be Area Border Routers (ABR) because some interfaces connect to the
backbone area, and some connect to nonbackbone areas.
All nonbackbone areas must have a path to reach the backbone area (area 0) by having at least
one ABR connected to both the backbone area and the nonbackbone area.
```

OSPF Areas

How Areas Reduce SPF Calculation Time  
Routers requirefewer CPU cycles to process the smaller per-area LSDB with the SPF algorithm,  
reducing CPU overhead and improving convergence time.  
The smaller per-area LSDB requires less memory.  
Changes in the network (for example, links failing and recovering) require SPF calculations only  
on routers in the area where the link changed state, reducing the number of routers that must rerun SPF.  
Less information must be advertised between areas, reducing the bandwidth required to send LSAs.

LSAs.  
(OSPFv2) Link-State Advertisements  
One router LSA for each router in the area  
One network LSA for each network that has a DR plus one neighbor of the DR  
One summary LSA for each subnet ID that exists in a different area

Router LSAs Build Most of the Intra-Area Topology  
Router LSAs, also known as Type 1 LSAs, describe the router in detail. Each lists a router’s RID, its interfaces, its IPv4 addresses and masks, its interface state, and notes about what neighbors the  
router knows about via each of its interfaces.

```
This chapter covers the following exam topics:
3.0 IP Connectivity
3.2 Determine how a router makes a forwarding decision by default
3.2.b Administrative distance
3.2.c Routing protocol metric
3.4 Configure and verify single area OSPFv
3.4.a Neighbor adjacencies
3.4.b Point-to-point
3.4.c Broadcast (DR/BR selection)
3.4.d Router ID
Implementing Single-Area OSPFv
Step 1. Use the particular OSPF process. router ospf process-id global command to enter OSPF configuration modefor a
Step 2. (Optional) Configure the OSPF router ID by doing the following:
A. Use the router-id id-value router subcommand to define the router ID, or
B. Use the command, to configure an IP address on a loopback interface ( interface loopback number global command, along with an chooses the ip address address mask highest IP address of
all working loopbacks), or
C. Rely on an interface IP address (chooses the highest IP address of all working nonloopbacks).
Step 3. Use one or more network ip-address wildcard-mask area area-id router subcommands
to enable OSPFv2 on any interfaces matched by the configured address and mask, enabling OSPF on the interface for the listed area.
OSPF Single-Area Configuration
for each matched interface, the router enables OSPF on those interfaces, discovers neighbors, creates neighbor relationships, and assigns the interface to the area listed in the network
command.
Verifying OSPF Operation
The show ip ospf neighbor, show ip ospf database, and show ip route commands display
```

# 20 OSPF config

Thursday, August 26, 2021 2:45 PM

```
The information to match each of these three steps, respectively. show ip ospf neighbor, show ip ospf database, and show ip route commands display
```

```
FULL/ use a DR/BDR.-: The neighbor state is full, with the “-“ instead of letters meaning that the link does not
FULL/DR: The neighbor state is full, and the neighbor is the DR.
FULL/BDR: The neighbor state is full, and the neighbor is the backup DR (BDR).
FULL/DROTHER: implies that the local router is a DR or BDR because the state is FULL.)The neighbor state is full, and the neighbor is neither the DR nor BDR. (It also
2WAY/DROTHER: The neighbor state is 2-way, and the neighbor is neither the DR nor BDR—that
is, a DROther router. (It also implies that the local router is also a DROther router because otherwise the state would reach a full state.)
```

Verifying OSPF Configuration  
If you have configuration.enable mode access, use the **show running-config** command to examine the  
If you have only configuration. user mode access,use the **show ip protocols** command to re-create the OSPF  
Use the **show ip ospf interface [brief]** command to determine whether the router enabled OSPF  
on the correct interfaces or not based on the configuration.  
**show ip ospf interface brief** showing all the interfaces on which OSPF has been enabledcommand shown here. It lists one line per interface, with the list

```
the show ip ospf interface command with the brief keywordat the end lists a single line of
output per interface,displays about 20 lines of output per interfacebut the show ip ospf interfacecommand (without the brief keyword)
```

Configuring the OSPF Router ID  
most enterprise networks that use OSPF choose to configure each router’s OSPF router ID  
If therouter-id rid OSPF subcommand is configured, this value is used as the RID.  
If any loopback interfaces have an IP address configured, status of up, the router picks the highest numeric IP address among these loopback interfaces.and the interface has an interface  
The router picks the code (first status code) is up. (In other words, an interface in up/down state will be included by highest numeric IP address from all other interfaces whose interface status  
OSPF when choosing its router ID.)  
stops and restarts the OSPF processup, and later the configuration changes in a way that would impact the OSPF RID, OSPF does not (with the **clear ip ospf process** command). So, if OSPF comes  
change the RID immediately. Instead, IOS waits until the next time the OSPF process is restarted.  
OSPF Interface Configuration Example  
Step 1. Use the **no network network-id area area-id** subcommands in OSPF configuration mode  
to remove the network commands.  
Step 2. Add one **ip ospf process-id area area-id** command in interface configuration mode under  
each interface on which OSPF should operate,correct OSPF area number. with the correct OSPF process (process-id) and the

```
The some different details if you use interface configuration versus the network command show ip protocols command relists most of the routing protocol configuration,so it does list
```

Verifying OSPF Interface Configuration

Additional OSPFv2 Features  
Passive interfaces  
Default routes  
Metrics  
Load balancing  
OSPF Passive Interfaces  
When no routers exist on a link  
OSPF continues to advertise about the subnet that is connected to the interface.  
OSPF no longer sends OSPF Hellos on the interface.  
OSPF no longer processes any received Hellos on the interface.  
OSPF still advertises about the connected subnet, but OSPF also does not form neighbor  
relationships over the interface.  
First, configuration mode:you can add the following command to the configuration of the OSPF process, in router  
**passive-interface** _type number_  
Alternately, the configuration can change the default setting so that all interfaces are passive by default and then add a **no passive-interface** command for all interfaces that need to not be  
passive:  
**passive-interface default  
no passive-interface** _type number_

The passive interfaces. **show ip ospf interface brief** command lists all interfaces on which OSPF is enabled, including  
The **show ip ospf interface** command lists a single line that mentions that the interface is passive.  
OSPF Default Routes  
All routers learn specific (nondefault) routes for subnets inside the company; a default route is not needed when forwarding packets to these destinations.  
One router connects to the Internet, and it has a default route that points toward the Internet.  
All routers should dynamically learn a default route,that all packets destined to locations in the Internet go to the one router connected to the used for all traffic going to the Internet, so  
Internet.  
**default** using OSPF to the remote routers (B1 and B2). **- information originate** command (Step 2) makes the router advertise a default route

```
The default-information originate always router subcommand tells the router to always
advertise the default route, no matter whether the router’s default route is working or not.
```

OSPF Metrics (Cost)  
Cisco routers allow three different ways to change the OSPF interface cost:  
Directly, using the interface subcommand **ip ospf cost x**.  
Using the default calculation per interface, and changing the interface bandwidth setting, which changes the calculated value.  
Using the default calculation per interface, and changing the OSPF reference bandwidth setting, which changes the calculated value.

```
The output also shows a cost value of 1 for the other Gigabit interfaces, which is the default OSPF
cost for any interface faster than 100 Mbps.
```

```
interface bandwidth setting does not influence the actual transmission speed.Instead, the
interface bandwidth acts as a configurable setting to represent the speed of the interface, with the option to configure the bandwidth to match the actual transmission speed...or not
configuration of the interface bandwidth using bandwidth speed interfacesubcommand.
Reference_bandwidth / Interface_bandwidth
you should cost. avoid changing the interface bandwidth as a means to influence the default OSPF
any interface with an interface bandwidth of 100 Mbps or faster ties with a calculated OSPF cost of 1 when using the default reference bandwidth. So, when relying on the default OSPF cost
calculation, it helps to configure the reference bandwidth to another value.
```

Setting the Cost Based on Interface and Reference Bandwidth

You can still use OSPF’s default cost calculation (and many do) just by changing the reference  
bandwidth with the **auto-cost reference-bandwidth speed** OSPF mode subcommand  
For instance, routers to use autoin an enterprise whose fastest links are 10 Gbps (10,000 Mbps), you could set all -cost reference-bandwidth 10000, meaning 10,000 Mbps or 10 Gbps. In that  
case, by default, a 10cost of 10, and a 100--MBps link a cost of 100Gbps link would have an OSPF cost of 1, while a 1. -Gbps link would have a  
Set the cost explicitly, using the 65,535, inclusive. ip ospf cost x interface subcommand, to a value between 1 and  
Although it should be avoided, change the interface bandwidth with the **bandwidth speed**  
command,with speed being a number in kilobits per second (Kbps).  
Change the reference bandwidth, using router OSPF subcommandauto-cost reference-  
bandwidth ref-bw, with a unit of megabits per second (Mbps).  
OSPF Load Balancing  
when the metrics tie for multiple routes to the same subnet, the router can put multiple equalcost routes in the routing table (the default is four different routes) based on the setting of the -  
maximum-paths number router subcommand  
the default (and better) method, the load balancing could be on a per-destination IP address  
basis.

```
This chapter covers the following exam topics:
3.0 IP Connectivity
3.4 Configure and verify single area OSPFv
3.4.a Neighbor adjacencies
3.4.b Point-to-point
3.4.c Broadcast (DR/BDR selection)
3.4.d Router ID
```

```
OSPF Network Types
```

```
TheOSPF Broadcast Network Type
default to use network type broadcast
Attempt to discover neighbors by sending OSPF Hellos to the 224.0.0.5 multicast address (address reserved for sending packets to all OSPF routers in the subnet) an
Attempt to elect a DR and BDR on each subnet
On the interface with no other routers on the subnet (G0/1), become the DR
On the interface with three other routers on the subnet (G0/0), be either DR, BDR, or a DROther router
all discovered routers on the link should become neighbors and at least reach the 2all neighbor relationships that include the DR and/or BDR, the neighbor relationship should -way state. For
further reach the full state. refers to neighbors that reach this full state.That section defined the term fully adjacent as a special term that
```

# 21 OSPF Network Types and Neighbors

Friday, August 27, 2021 9:44 AM

```
To see the setting, use the show ip ospf interface command,as shown in Example 21-4. The first
highlighted item identifies the network type
```

**ip ospf network broadcast** interface subcommand would configure the setting.  
Configuring to Influence the DR/BDR Election  
If the DR fails, the BDR becomes the DR, and a new BDR is elected.  
Preemption:If a new router is configured to be the DR, it will not become the DR until the  
OSPF process is reset.

```
When a better router enters the subnet, no preemption of the existing DR or BDR occurs.-
```

```
As a result of these rules, while you can configure a router to be the best (to become the DR in an election, doing so only increases that router’s statistical chances of being highest priority) router
the DR at a given point in time. If the router fails, other routers will become DR and BDR, and the
```

```
the DR at a given point in time. If the router fails, other routers will become DR and BDR, and best router will not be DR again until the current DR and BDR fail. the
```

```
The highest OSPF interface priority: The highest value wins during an election, with values ranging from 0 to 255.
The highest OSPF Router ID: If the priority ties, the election chooses the router with the highest OSPF RID.
```

```
If an engineer preferred that R1 be the DR, the engineer could add the configuration in Example 21 - 5 to set R1’s interface priority to 99. (default of 1)
```

show that the DR and BDR have not changed at all  
The OSPF Point-to-Point Network Type  
(HDLC and PPP) do not support data-link broadcasts.  
to use OSPF network type pointsame configuration command on its matching interface. -to-point. R2, on the other end of the WAN link, would need the

OSPF Neighbor Relationships  
They must have compatible values for several settings as listed in the Hellos exchanged between the two routers

For items listing a “yes” in this column, if that item is configured incorrectly, the neighbor will not appear in lists of OSPF neighbors—for instance, with the **show ip ospf neighbor** command.

the last section (shaded) lists a couple of OSPF settings that give a different symptom when incorrect

```
for these two items, when incorrect, a router can list the other router as a neighbor, but the
neighbor relationship does not work properly in that the routers do not exchange LSAs as they should
```

10/40 is the default hello/dead timer  
Finding Area Mismatches  
Check the output of **show running-config** to look for  
**ip ospf process-id area area-number** interface subcommands  
network commands in OSPF configuration mode  
Use the **show ip ospf interface [brief]** command to list the area number

```
both routers automatically generate a log message for the duplicate OSPF RID problem between
R1 and R3;
show ip ospf commands on both R3 and R1 to easily list the RID on each router,
use the router-id 3.3.3.3 OSPF subcommand and use the EXEC mode command clear ip ospf
process or reload.). (OSPF will not begin using a new RID value until the process restarts, either via command
```

Finding Duplicate OSPF Router IDs

Finding OSPF Hello and Dead Timer Mismatches

Hello interval/timer: The per-interface timer that tells a router how often to send OSPF Hello  
messages on an interface.  
Dead interval/timer: The perreceived a Hello from a neighbor before believing that neighbor has failed. (Defaults to four times -interface timer that tells the router how long to wait without having  
the Hello timer.)

Shutting Down the OSPF Process  
When a routing protocol process is shut down, IOS does the following:  
Brings down all neighbor relationships and clears the OSPF neighbor table  
Clears the LSDB  
Clears the IP routing table of any OSPF-learned routes  
IOS retains all OSPF configuration.  
IOS still lists all OSPF-enabled interfaces in the OSPF interface list( **show ip ospf interface** )  
but in a DOWN state.

```
defining the largest network layer packet that the router will forward out each interface.
default MTU size of 1500 bytes,
The command sets the equivalent for IPv6 packets. ip mtu size interface subcommand defines the IPv4 MTU setting, and the ipv6 mtu size
Symptom: they fail to exchange their LSDBs. Eventually, after trying and failing to exchange their
LSDBs, the neighbor relationship also fails.
show interfaces command (which lists the IP MTU).
```

Mismatched MTU Settings

Mismatched OSPF Network Types

one router uses broadcast, and the other uses point-to-point, the following occurs:  
The two routers become fully adjacent neighbors (that is, they reach a full state).  
They exchange their LSDBs.  
They do not add IP routes to the IP routing table.

This chapter covers the following exam topics:  
1.0 Network Fundamentals  
1.8 Configure and verify IPv6 addressing and prefix

Introduction to IPv6  
IPv6 increases the address to 128 bits in length.  
Older OSPF Version 2 Upgraded to OSPF Version 3:  
a newer version, OSPF version 3, was created to support IPv6. (Note: OSPFv3 was later  
upgraded to support advertising both IPv4 and IPv6 routes.)  
ICMP Upgraded to ICMP Version 6:  
ARP Replaced by Neighbor Discovery Protocol:  
32 hexadecimal digits (one hex digit per 4 bits)  
Figure 22-3 shows the required 40-byte part of the IPv6 header.

IPv6 Routing  
To be able to build and send IPv6 packets out an interface, endon that interface. -user devices need an IPv6 address  
End-user hosts need to know the IPv6 address of a default router, to which the host sends IPv6

# 22. IPv6

Friday, August 27, 2021 2:01 PM

```
Endpackets if the host is in a different subnet.-user hosts need to know the IPv6 address of a default router, to which the host sends IPv6
IPv6 routers de-encapsulate and re-encapsulate each IPv6 packet when routing the packet.
IPv6 routers make routing decisions by comparing the IPv6 packet’s destination address to the router’s IPv6 routing table; the matched route lists directions of where to send the IPv6 packet
next.
Note
You could take the preceding list and replace every instance of IPv6 with IPv4, and all the statements would be true of IPv4 as well.
```

```
the router must look at a protocol type field in the data-link header, which identifies the type of
packet inside the dataIPv6 packet. -link frame. Today, most data-link frames carry either an IPv4 packet or an
To route an IPv6 packet, a router must use its IPv6 routing table instead of the IPv4 routing table.
the process works like IPv4, except that the IPv6 packet lists IPv6 addresses, and the IPv6 routing table lists routing information for IPv6 subnets (called prefixes).
(The migration strategy of running both IPv4 and IPv6 is called dual stack.) All you have to do is
configure the router to route IPv6 packets, in addition to the existing configuration for routing IPv4 packets.
```

```
Routing Information Protocol (RIP), Open Shortest Path First (OSPF), Enhanced Interior Gateway Routing Protocol (EIGRP), and Border Gateway Protocol (BGP) were all updated to support IPv6.
```

IPv6 Routing Protocols

these routing protocols also follow the same interior gateway protocol (IGP) and exterior gateway protocol (EGP) conventions as their IPv4 cousins. RIPng, EIGRPv6, and OSPFv3 act as interior  
gateway protocols, advertising IPv6 routes inside an enterprise.  
Representing the Prefix Length of an Address  
IPv6 uses a mask concept, called the prefix length, similar to IPv4 subnet masks.  
the IPv6 prefix length is written as a /, followed by a decimal number. The prefix length defines how many bits of the IPv6 address define the IPv6 prefix, which is basically the same concept as  
the IPv4 subnet ID.  
When writing an IPv6 address and prefix length in documentation, you can choose to leave a space before the /, or not, as shown in the next two examples.  
2222:1111:0:1:A:B:C:D/642222:1111:0:1:A:B:C:D /64

```
by zeroing out the last 64 bits (16 digits) of the address, you find the following prefix value:
2000:1234:5678:9ABC:0000:0000:0000:0000/64
This value can be abbreviated, with four quartets of all 0s at the end, as follows:
2000:1234:5678:9ABC::/64
```

Finding the IPv6 Prefix

```
This chapter covers the following exam topics:
1.0 Network Fundamentals
1.8 Configure and verify IPv6 addressing and prefix
1.9 Compare and contrast IPv6 address types
1.9.a Global unicast
1.9.b Unique local
IPv6 does not use any concept like the classful network concept used by IPv4reserve some IPv6 address ranges for specific purposes.. However, IANA does still
Public and Private IPv6 Addresses
global unicast addresses as the public IPv6 address space.
Global unicast: Addresses that work like public IPv4 addresses. The organization that needs IPv6 addresses asks for a registered IPv6 address block, which is assigned as a global routing prefix.
After that, only that organization uses the addresses inside that block of addressesaddresses that begin with the assigned prefix. —that is, the
Unique local: Works somewhat like private IPv4 addresses, with the possibility that multiple organizations use the exact same addresses, and with no requirement for registering with any
numbering authority.
That reserved block of IPv6 addressescalled aglobal routing prefix. —a set of addresses that only one company can use—is
Address Ranges for Global Unicast Addresses
unique local unicast addresses, discussed later in this chapter, all start with hex FD.
any address ranges that are not specifically reserved, for now, are considered to be global unicast addresses.
```

# 23 IPv6 Addressing and Subnetting

Friday, August 27, 2021 3:17 PM

IPv6 Subnetting Using Global Unicast Addresses  
Most everyone uses the easiest possible IPv6 prefix length: /64.  
theright side of the IPv6, formally called the interface ID(short for interface identifier), acts like  
the IPv4 host field.  
the prefix length of the global routing prefix is often between /32 and /48, or possibly as long as  
/56.  
with the commonly used 64being the length of the global routing prefix.-bit interface ID field, the subnet field is typically 64–P bits, with P

```
All subnet IDs begin with the global routing prefix.
Use a different value in the subnet field to identify each different subnet.
All subnet IDs have all 0s in the interface ID.
The IPv6 subnet ID, more formally called the subnet router anycast address, is reserved and should not be used as an IPv6 address for any host.
```

Assigning Addresses to Hosts in a Subnet  
hosts can learn these same settings dynamically, using either Dynamic Host Configuration  
Protocol (DHCP) or a built(SLAAC). -in IPv6 mechanism called Stateless Address Autoconfiguration

Unique Local Unicast Addresses  
Unique local unicast addresses act as private IPv6 addresses.  
The biggest difference lies in the literal number with the administrative process: the unique local prefixes are not registered with any numbering (unique local addresses begin with hex FD) and  
authority and can be used by multiple organizations.

```
authority and can be used by multiple organizations.
Use FD as the first two hex digits.
Choose a unique 40-bit global ID.
Append the global ID to FD to create a 48-bit prefix, used as the prefix for all your addresses.
Use the next 16 bits as a subnet field.
Note that the structure leaves a convenient 64-bit interface ID field.
```

IANA actually reserves prefix FC00::/7, and not FD00::/8, for these addresses. FC00::/7 includes  
all addresses that begin with hex FC and FD. However, an RFC (4193) requires the eighth bit of these addresses to be set to 1, which means that in practice today, the unique local addresses all  
begin with their first two digits as FD.  
Subnetting with Unique Local IPv6 Addresses  
With unique local, you create that prefix locally, and the prefix begins with /48, with the first 8  
bits set and the next 40 bits randomly chosen.  
imagine you chose a 10-hex-digit value of hex 00 0001 0001, prepend a hex FD, making the  
entire prefix be FD00:0001:0001::/48, or FD00:1:1::/48 when abbreviated.  
The Need for Globally Unique Local Addresses  
RFC stresses the importance of choosing your global ID in a way to make it statistically unlikely to be used by other companies.

```
your prefix.in a real network, plan on using the random number generator logic listed in RFC 4193 to create
One of the big reasons to attempt to use a unique prefix, rather than everyone using the same
easyanother company.-to-remember prefixes, is to be ready for the day that your company merges with or buys
```

With IPv6 unique local addresses, if both companies did the right thing and randomly chose a  
prefix, they will most likely be using completely different prefixes, making the merger much simpler

```
This chapter covers the following exam topics:
1.0 Network Fundamentals
1.9 Compare and contrast IPv6 address types
1.9.a Global unicast
1.9.b Unique local
1.9.c Link local
1.9.d Anycast
1.9.e Multicast
1.9.f Modified EUI 64
Configuring the Full 128-Bit Address
To statically configure the full 128-bit unicast address—either global unicast or unique local—the
router needs anThe address can be an abbreviated IPv6 address or the full 32 ipv6 address address/prefix-length interface subcommand on each interface. -digit hex address.The command
includes theprefix length value, at the end, with no space between the address and prefix length.
```

# 24 IPv6 config

Monday, August 30, 2021 9:19 AM

both abbreviated and unabbreviated addresses, and both lowercase and uppercase hex digits,  
showing that all are allowed.  
Enabling IPv6 Routing  
IPv6 routing is not enabled by default. **routing** —whichenables IPv6 routing on the router.The solution takes only a single command— **ipv6 unicast-**  
A router **address)** must enable IPv6 globally before the router will attempt to route IPv6 packets in and out an interface **(ipv6 unicast-routing** ) and enable IPv6 on the interface .If you omit **(ipv6**  
theroute any received IPv6 packets, but the router will act as an IPv6 host **ipv6 unicast-routing** command but configure interface IPv6 addresses, the router will not. If you include the ipv6  
unicastroute IPv6 packets but have no interfaces that have IPv6 enabled, effectively disabling IPv6 -routingcommand but omit all the interface IPv6 addresses, the router will be ready to  
routing  
Verifying the IPv6 Address Configuration  
The **show ipv6 interface brief** command gives you interface IPv6 address info, but not prefix  
length info, similar to the IPv4 **show ip interface** brief command.  
this command lists IPv6 addresses, but not the prefix length or prefixes.  
The **show ipv6 interface** commandgives the details of IPv6 interface settings, much like the **show  
ip interface** command does for IPv4.  
the IPv6 **show interfaces**. So, to see IPv6 interface addresses, use commands that begin withcommand still lists the IPv4 address and mask but tells us nothing about **show ipv6**

IPv6. So, to see IPv6 interface addresses, use commands that begin with **show ipv6**  
Generating a Unique Interface ID Using Modified EUI- 64  
The router then uses EUI-64 rules to create the interface ID part of the address, as follows:  
Key Topic.  
Split the 6-byte (12-hex-digit) MAC address in two halves (6 hex digits each).  
Insert FFFE in between the two, making the interface ID now have a total of 16 hex digits  
(64 bits).  
Invert the seventh bit of the interface ID.

```
Table 24-2 lists some practice problems,
```

```
ipv6 address address/prefix-length eui- 64 interface subcommand.
```

```
mac-address command under R1’s G0/0 interface, which causes IOS to use the configured
MAC address instead of the universal (burned-in) MAC address
for interfaces that do not have a MAC address, like serial interfaces, the router uses the
MAC of the lowest-numbered router interface that does have a MAC.
if you mistakenly type the full address and still use the euicommand and converts the address to the matching prefix before putting the command -64 keyword, IOS accepts the
into the running config file. For example, IOS converts ipv6 address 2000:1:1:1::1/64 euito ipv6 address 2000:1:1:1::/64 eui-64. - 64
```

```
routers can be configured to use dynamically learned IPv6 addresses. These can be useful for routers connecting to the Internet through some types of Internet access technologies, like DSL
and cable modems.
```

```
Stateful DHCP
Stateless Address Autoconfiguration (SLAAC)
```

```
two ways for the router interface to dynamically learn an IPv6 address to use:
```

Dynamic Unicast Address Configuration

Special Addresses Used by Routers  
After you configure thefunction of IPv6 routing, the addition of a unicast IPv6 address on an interface causes the router **ipv6 unicast-routing** global configuration command, to enable the  
to do the following:  
Gives the interface a unicast IPv6 address  
Enables the routing of IPv6 packets in/out that interface  
Defines the IPv6 prefix (subnet) that exists off that interface  
Tells the router to add a connected IPv6 route for that prefix, to the IPv6 routing table,  
when that interface is up/up  
the same ideas happen for IPv4 when you configure an IPv4 address on a router interface.  
Link-Local Addresses  
a special kind of unicast IPv6 address.  
not used for normal IPv6 packet flows that contain data for applications  
used by some overhead protocols and for routing.

```
packets sent to any link-local address should not be forwarded by any router to another subnet.
For example,link-local addresses.Neighbor Discovery Protocol (NDP), which replaces the functions of IPv4’s ARP, uses
Routers also use link-local addresses as the next-hop IP addresses in IPv6 routes,
IPv6 hosts also use a default router (default gateway) concept, like IPv4, but instead of the router address being in the same subnet, hosts refer to the router’s link-local address. The show ipv6
route command lists the linkunicast or unique local unicast address.-local address of the neighboring router, rather than the global
```

Link-Local Address Concepts

key facts about link-local addresse  
Unicast (not multicast): Link-local addresses represent a single host,  
Forwarding scope is the local link only:local data link because routers do not forward packets with linkPackets sent to a link-local address do not leave the -local destination  
addresses.  
Automatically generated: Every IPv6 host interface (and router interface) can create its own  
link-local address automatically,  
Creating Link-Local Addresses on Routers  
all link-local addresses start with the same prefix,(FE80,FE90,FEA0,FEB0)as shown on the left side  
of Figure 24-9.

```
tFE8, FE9, FEA, or FEB. he first 10 bits must match prefix FE80::/10, meaning that the first three hex digits will be either
the next 54 bits should be binary 0, so the link-local address should always start with
FE80:0000:0000:0000 as the first four unabbreviated quartets.
The second half of the linkrandomly generated, or even configured.-local address, in practice, can be formed using EUI-64 rules, can be
IOS creates a linkaddress using the ipv6 address command (global unicast or unique local). To see the link-local address for any interface that has configured at least one other unicast -local
address, just use the usual commands that also list the unicast IPv6 address: and show ipv6 interface brief. show ipv6 interface
```

both addresses have the same interface ID value  
IOS chooses the link-local address for the interface based on the following rules:  
If configured, the router uses the value in the **ipv6 address address link-local** interface  
subcommand. Note that the configured linkrange for link-local addresses; that is, an address from prefix FE80::/10. In other words, the -local address must be from the correct address  
address must begin with FE8, FE9, FEA, or FEB.  
If not configured, the IOS calculates the linkand demonstrated in and around Example 24-local address using EUI-7. The calculation uses EUI-64 rules, as discussed -64 rules even if  
the interface unicast address does not use EUI-64.  
Routing IPv6 with Only Link-Local Addresses on an Interface  
**ipv6 address address/prefix-length** : Static configuration of a specific address  
**ipv6 address prefix/prefix-length eui- 64** : Static configuration of a specific prefix and prefix  
length, with the router calculating the interface ID using EUI-64 rules  
**ipv6 address dhcp:** Dynamic learning on the address and prefix length using DHCP  
**ipv6 address autoconfig** : Dynamic learning of the prefix and prefix length, with the router  
calculating the interface ID using EUI-64 rules (SLAAC)  
**ipv6 enable** : Enables IPv6 processing and adds a link-local address, but adds no other unicast IPv6  
addresses.  
some links, particularly WAN links, do not need a global unicast address  
the routers do not need to have global unicast (or unique local) addresses on the WAN links for routing to work. IPv6 routing protocols use link-local addresses as the next-hop address  
when dynamically building IPv6 routes.  
static routes, as discussed in Chapter 25, “Implementing IPv6 Routing,” can use link-local

```
static routes, as discussed in Chapter 25, “Implementing IPv6 Routing,” can use linkaddresses for the next-hop address. -local
creating a WAN link with no global unicast (or unique local) addresses works. As a result,
you would not even need to assign an IPv6 subnet to each WAN link. Then to configure the WAN interfaces, use the ipv6 enable command, enabling IPv6 and giving each interface a
generated link-local IPv6 address.
To use the command, just configure the ipv6 enable command on the interfaces on both
ends of the WAN link.
```

```
IANA defines the range FF30::/12 (all IPv6 addresses that begin with FF3) as the range of
addresses to be used for some types of multicast applications.
different IPv6 RFCs reserve multicast addresses for specific purposes. For instance, FF02::5andFF02::6 as the all-OSPF-routers and all-DR-Routers multicast addresses, OSPFv3 uses
OSPFv2 uses IPv4 addresses 224.0.0.5 and 224.0.0.6 for the equivalent purposes.
```

IPv6 Multicast Addresses

Reserved Multicast Addresses  
IPv6, instead of using Layer 3 and Layer 2 broadcasts, instead uses Layer 3 multicast addresses, which in turn cause Ethernet frames to use Ethernet multicast addresses. As a result:  
All the hosts that should receive the message receive the message, which is necessary for the protocols to work. However...  
...Hosts that do not need to process the message can make that choice with much less  
processing as compared to IPv4.  
OSPFv3 uses IPv6 multicast addresses FF02::5 and FF02::6. In a subnet, the listen for packets sent to those addresses. However, all the endpoint hosts do not use OSPFv3 OSPFv3 routers will  
and should ignore those OSPFv3 messages  
the most common reserved IPv6 multicast addresses.

```
show ipv6 interface command to show the multicast addresses used by Router R1 on its G0/0
interface.
```

```
Each scope defines a different set of rules about whether routers should or should not forward a packet, and how far routers should forward packets, based on those scopes.
```

Multicast Address Scopes

routers can predict the boundaries of some scopes, like linkknow the boundaries of other scopes, for instance, organization-local, but they need configuration to -local.)

Link-local address: An IPv6 address that begins FE80. This serves as a unicast address for an  
interface to which devices apply a linkaddresses using EUI-64 rules. A more complete term for comparison would be -local scope.Devices often create their own linklink-local unicast -local  
address.

```
address.
Linkmulticast address to which devices apply a link-local multicast address: An IPv6 address that begins with FF02. This -local scope. serves as a reserved
Linkrouters should not forward packets sent to an address in this scope.-local scope: A reference to the scope itself, rather than an address. This scope defines that
```

Solicited-Node Multicast Addresses  
IPv6 Neighbor Discovery Protocol (NDP) replaces IPv4 ARP,  
NDP improves the MACprocessed by the correct host but discarded with less processing by the rest of the hosts in the -discovery process by sending IPv6 multicast packets that can be  
subnet  
Figure 24unicast address- 12 shows how to determine the solicited node multicast address associated with a. Start with the predefined /104 prefix (26 hex digits) shown in Figure 24-12. In  
other words, all the solicitedthe last 24 bits (6 hex digits), copy the last 6 hex digits of the unicast address into the solicited-node multicast addresses begin with the abbreviated FF02::1:FF. In -  
node address.

```
a host or router calculates a matching solicited node multicast address for every unicast address
on an interface
the router interface has a unicast address of 2001:DB8:1111:1::1/64, and a linkFE80::AA:AAAA. As a result, the interface has two solicited node multicast addresses, shown at -local address of
the end of the output.
```

```
all IPv6 hosts can use two additional special addresses:
The unknown (unspecified) IPv6 address, ::, or all 0s
The loopback IPv6 address, ::1, or 127 binary 0s with a single 1
A host can use the unknown address (::) when its own IPv6 address is not yet known or when the host wonders if its own IPv6 address might have problems.
hosts use the unknown address during the early stages of dynamically discovering their IPv6 address. When a host does not yet know what IPv6 address to use, it can use the ::
address as its source IPv6 address
IPv6 loopback address gives each IPv6 host a way to test its own protocol stack. Just like the IPv4 127.0.0.1 loopback address, packets sent to ::1 do not leave the host but are instead simply
delivered down the stack to IPv6 and back up the stack to the application on the local host
```

Miscellaneous IPv6 Addresses

Anycast Addresses  
service works best when implemented on several routers  
Hosts can send just one packet to an IPv6 address, and the routers will forward the packet to the nearest router that supports that service by virtue of supporting that destination IPv6 address.  
Step 1.Two routers configure the exact same IPv6 address, designated as an anycast  
address, to support some service.  
Step 2.routers simply route the packet to the nearest router that supports the address.In the future, when any router receives a packet for that anycast address, the other  
the routers implementing the anycast address must be configured and then advertise a route for the anycast address. The addresses do not come from a special reserved range of addresses;  
they are from the unicast address range. Often, the address is configured with a /128 prefix so  
that the routers advertise a host route for that one anycast address.

```
the routing protocol advertises the route just like any other IPv6 route; the other routers cannot
tell the difference
the actual address (2001:1:1:2::99) looks like any other unicast address
note the different anycast keyword on the ipv6 address command, telling the local router that
the address has a special purpose as an anycast address
the ipv6 show ipv6 interface interface brief command does not.command does identify the address as an anycast address, but the show
```

IPv6 Addressing Configuration Summary

3.0 IP Connectivity  
3.3 Configure and verify IPv4 and IPv6 static routing  
3.3.a Default route  
3.3.b Network route  
3.3.c Host route  
3.3.d Floating static

Connected and Local IPv6 Routes  
a router adds IPv6 routes based on the following:  
The configuration of IPv6 addresses on working interfaces (connected and local routes)  
The direct configuration of a static route (static routes)  
The configuration of a routing protocol, like OSPFv3, on routers that share the same data link (dynamic routes)

```
Firstthe ipv6 address , the router looks for any configured unicast addresses on any interfaces by looking for command.
if the interface is working—if the interface has a “line status is up, protocol status is up”
notice in the output of theand local route. show interfaces command—the router adds both a connected
Routers do not create connected or local IPv6 routes for link-local addresses.
Theroute connected route is a host route for only the specific IPv6 address configured on the interface.represents the subnet connected to the interface,whereas thelocal
Routers create IPv6 routes based on each unicast IPv6 address on an interface, as configured with the ipv6 address command, as follows:
The router creates a route for the subnet (a connected route).
The router creates a host route (/128 prefix length) for the router IPv6 address (a local
route).
Routers do not create routes based on the link-local addresses associated with the interface.
Routers remove the connected and local routes for an interface if the interface fails, and
they re-add these routes when the interface is again in a working (up/up) state
```

```
Rules for Connected and Local Routes
```

# 25 IPv6 Routing

Tuesday, August 31, 2021 2:58 PM

```
they re-add these routes when the interface is again in a working (up/up) state
```

Examples of Local IPv6 Routes  
**show ipv6 route local** command

Static IPv6 Routes  
static routes require direct configuration with the **ipv6 route** command  
the **ipv6 route** command begins with the prefix and prefix length. Then the respective commands

the list the directions of how this router should forward packets toward that destination subnet or **ipv6 route** command begins with the prefix and prefix length. Then the respective commands  
prefix by listing the outgoing interface or the address of the next-hop router.  
A static route on R1, for this subnet, will begin witheither the outgoing interface (S0/0/0) or the next-hop IPv6 address, or both. **ipv6 route 2001:DB8:1111:2::/64,** followed by

```
when the command references an interface, the interface is a local interface
```

```
show ipv6 route command will list all the IPv6 routes.
show ipv6 route static command, whichlists only static routes
```

```
directly connected” might mislead you to think this is a connected route; trust the “S” code.
show ipv6 route 2001:DB8:1111:2::22 route that the router would use when forwarding packets to that particular address.command. This command asks the router to list the
Example 25-7 shows an example.
```

Static Routes Using the Outgoing Interface

```
Static IPv6 routes that refer to a next-hop address have two options: the unicast address on
the neighboring router (global unicast or unique local) or the linkneighboring router -local address of that same
```

Static Routes Using Next-Hop IPv6 Address

Example Static Route with a Link-Local Next-Hop Address  
**ipv6 route** the link-local address does not, by itself, tell the local router which outgoing interface to command cannot simply refer to a link-local next-hop address by itself because  
use.  
With a linkoutgoing interface must also be configured.-local next-hop address, a router cannot work through this same logic, so the

```
show commands also list both the next-hop (link-local) address and the outgoing interface
```

Static Routes over Ethernet Links  
To configure a static route that uses an Ethernet interface, the parameters should always include a next-hop IPv6 address. IOS allows you to configure the ipv6 **ipv6 route** command’s forwarding  
route command using only the outgoingThe router will accept the command; however, -interface parameter, without listing a nextif that outgoing interface happens to be an -hop address.  
Ethernet interface, the router cannot successfully forward IPv6 packets using the route.  
To configure the ipv6 route correctly when directing packets out an Ethernet interface, the configuration should use one of these styles:  
Refer to the next-hop global unicast address (or unique local address) only  
Refer to both the outgoing interface and nextaddress) -hop global unicast address (or unique local  
Refer to both the outgoing interface and next-hop link-local address

```
Branch routers could use default routes instead of a routing protocol.
```

```
use a specific value to note the route as a default route: ::/0
```

Static Default Routes

Static IPv6 Host Routes  
a route to a single host IP address. With IPv4, those routes use a /32 mask, which identifies a  
single IPv4 address in thethe ipv6 route command. **ip route** command; with IPv6, a /128 mask identifies that single host in

Floating Static IPv6 Routes

IOS considers static routes better than OSPFdistance. IOS uses the same administrative distance concept and default values for IPv6 as it does -learned routes by default due to administrative  
for IPv4  
IPv6 floating static route floats or moves into and out of the IPv6 routing table depending on  
whether the better (lower) administrative distance route learned by the routing protocol happens to exist currently.

To implement an IPv6 floating static route, just override the default administrative distance on the static route, making the value larger than the default administrative distance of the routing  
protocol.  
**ipv6 route 2001:db8:1111:7::/64 2001:db8:1111:9::3 130** that, setting the static route’s administrative distance to 130. command on R1 would do exactly

Troubleshooting Incorrect Static Routes That Appear in the IPv6 Routing Table  
IOS cannot tell if you choose the incorrect outgoing interface, incorrect nextincorrect prefix/prefix-length in a static route. -hop address, or  
IOS puts the route into the IP routing tablepoorly chosen parameters. —even though the route may not work because of the  
R1 cannot use its own IPv6 address as a next-hop address.  
routes may have incorrect parameters. Check for these types of mistakes:  
Step 1. Prefix/Length: Does the ipv6 route command reference the correct subnet ID (prefix) and mask (prefix length)?  
Step 2. If using a next-hop IPv6 address that is a link-local address:  
A. Is the link-local address an address on the correct neighboring router? (It should be  
an address on another router on a shared link.)  
B. Does the ipv6 route command also refer to the correct outgoing interface on the  
local router?  
Step 3. If using a nextaddress the correct unicast address of the neighboring router?-hop IPv6 address that is a global unicast or unique local address, is the  
Step 4. If referencing an outgoing interface, does the ipv6 route command reference the interface on the local router (that is, the same router where the static route is configured)?

The Static Route Does Not Appear in the IPv6 Routing Table  
IOS makes the following checks before adding the route;  
For ipv6 route commands that list an outgoing interface, that interface must be in an up/up state.  
For ipv6 route commands that list a global unicast or unique local next-hop IP address (that

```
For ipv6 route commands that list a global unicast or unique local nextis, not a link-local address), the local router must have a route to reach that next-hop IP address (that -hop
address.
If another IPv6 route exists for that exact same prefix/prefixhave a better (lower) administrative distance. -length, the static route must
```

The Neighbor Discovery Protocol  
with 1pv4 ARP works as a separate protocol; with IPv6, thepart of ICMPv6,performs the same functions. Neighbor Discovery Protocol (NDP), a  
few of the functions of the NDP protocol (RFC 4861). Some of those NDP functions are  
Neighbor MAC Discovery:of other hosts in the same subnet. NDP replaces IPv4’s ARP, providing messages that An IPv6 LAN-based host will need to learn the MAC address  
replace the ARP Request and Reply messages.  
Router Discoverysame subnet. : Hosts learn the IPv6 addresses of the available IPv6 routers in the  
SLAACmessages to learn the subnet (prefix) used on the link plus the prefix length.: When using Stateless Address Auto Configuration (SLAAC), the host uses NDP  
DAD: Before using an IPv6 address, hosts use NDP to perform a Duplicate Address  
Detection (DAD) process, to ensure no other host uses the same IPv6 address before attempting to use it.  
Discovering Neighbor Link Addresses with NDP NS and NA  
using a pair of matched solicitation and advertisement messages:(NS)and Neighbor Advertisement (NA)messages. the Neighbor Solicitation  
the send back a replyNS acts like an IPv4 ARP request. The NA message acts like an IPv4 ARP Reply, listing that host’s MAC , asking the host with a particular unicast IPv6 address to  
address.  
Neighbor Solicitation (NS)(the target address) to reply with an NA message that lists its MAC address. : This message asks the host with a particular IPv6 address The NS  
message is sent to the solicitedaddress, so the message is processed only by hosts whose last six hex digits match the -node multicast address associated with the target  
address that is being queried.  
Neighbor Advertisement (NA): This message lists the sender’s IPv6 and MAC  
addresses. IPv6 unicast address of the host that sent the original NS messageIt can be sent in reply to an NS message, and if so, the packet is sent to the .A host can also  
send an unsolicited NA, announcing its IPv6 and MAC addresses, in which case the message is sent to the all-IPv6-hosts local-scope multicast address FF02::1.

To view a host’s NDP neighbor table, use these commands: (Windows) netsh interface ipv6  
show neighbors; (Linux) ip -6 neighbor show; (Mac OS) ndp -an.  
Discovering Routers with NDP RS and RA  
NDP defines two messages that allow any host to discover all routers in the subnet:  
Router Solicitation (RS):This message is sent to the “all-IPv6-routers” local-scope multicast  
address of FF02::2 so that the message asks all routers, on the local link only, to identify themselves.  
Router Advertisement (RA): link-local IPv6 address of the router. When sent in response to an RS message, it flows back This message, sent by the router, lists many facts, including the  
to either the unicast address of the host that sent the RS or to the allFF02::1. Routers also send RA messages without being asked, sent to the all-IPv6-hosts address -IPv6-hosts local-  
scope multicast address of FF02::1.

IPv6 allows multiple prefixes and multiple default routers to be listed in the RA message; Figure 25-9 just shows one of each for simplicity’s sake.  
also periodically send unsolicited RA messages  
the RA messages flow to the FF02::1 all-nodes IPv6 multicast address.  
Using SLAAC with NDP RS and RA

```
IPv6 supports an alternative method for IPv6 hosts to dynamically choose an unused IPv6 address
to use
The process goes by the nameStateless Address Autoconfiguration (SLAAC).
Learn the IPv6 prefix used on the link, from any router, using NDP RS/RA messages.
Build an address from the prefix plus an interface ID, chosen either by using EUI-64 rules or
as a random value.
Before using the address, first use DAD to make sure that no other host is already using the same address.
```

Discovering Duplicate Addresses Using NDP NS and NA  
IPv6 uses the Duplicate Address Detection (DAD) process before using a unicast address to make sure that no other node on that link is already using the address. Hosts use DAD not only at the  
end of the SLAAC process, but also any time that a host interface initializes, no matter whether using SLAAC, DHCP, or static address configuration. When performing DAD, if another host already  
uses that address, the first host simply does not use the address until the problem is resolved.  
a host sends an NS message for its own IPv6 address. No other host should be using that address,  
so no other host should send an NDP NA in reply. However, if another host already uses that address, that host will reply with an NA, identifying a duplicate use of the address.  
Hosts do the DAD check for each of their unicast addresses, link-local addresses included, both  
when the address is first used and each time the host’s interface comes up.  
NDP Summary  
NDP does more than what is listed in this chapter, and the protocol allows for addition of other  
functions, so NDP might continue to grow over time. For now, use Table 25for the four NDP features discussed here. -3 as a study reference

This chapter covers the following exam topics:  
1.0 Network Fundamentals  
1.1 Explain the role and function of network components  
1.1.d Access Points  
1.11 Describe wireless principles  
1.11.a Nonoverlapping Wi-Fi channels  
1.11.b SSID  
1.11.c RF

Comparing Wired and Wireless Networks

Wireless devices must adhere to a common standard (IEEE 802.11).  
Wireless coverage must exist in the area where devices are expected to use it.  
Wireless LAN Topologies  
IEEE 802.11 WLANs are always half duplex because transmissions between stations use the same frequency or channel.

Basic Service Set  
before a device can participate, it must advertise its capabilities and then be granted permission to join. The 802.11 standard calls this a basic service set (BSS). At the heart of every BSS is a  
wireless access point (AP),  
The AP operates ininfrastructure mode,which meansit offers the services that are necessary to  
form the infrastructure of a wireless networkchannel. The AP and the members of the BSS must all use the same channel to communicate. The AP also establishes its BSS over a single wireless  
properly.

# 26 Wireless

Wednesday, September 1, 2021 12:43 PM

the operation of a BSS hinges on the AP, the BSS is bounded by usable. This is known as thebasic service area (BSA)or cell. the area where the AP’s signal is

the cell is shown as a simple shaded circular area that centers around the AP itself.  
It advertises the existence of the BSS so that devices can find it and try to join. To do that, the AP  
uses a unique BSS identifier (BSSID) that is based on the AP’s own radio MAC address.  
Wireless devices must also have unique MAC addresses to send wireless frames at Layer 2 over  
the air.  
the AP advertises the wireless network with a Service Set Identifier (SSID), which is a text string containing a logical name.Think of the BSSID as a machine-readable name tag that uniquely  
identifies the BSS ambassador (the AP), and the SSID as a nonunique, humanthat identifies the wireless service. -readable name tag

Membership with the BSS is called an association. request to the AP and the AP must either grant or deny the request. Once associated, a device A wireless device must send an association  
becomes a client, or an 802.11 station (STA), of the BSS.  
As long as a wireless client remains associated with a BSS, most communications to and from the client must pass through the AP,

By using the BSSID as a source or destination address, data frames can be relayed to or from the AP.

By sending data through the AP first, the BSS remains stable and under control.  
Distribution System  
The 802.11 standard refers to the upstream wired Ethernet as the distribution system (DS) for the wireless BSS,  
the AP is in charge of mapping a virtual local-area network (VLAN) to an SSID.

```
The AP must be connected to the switch by a trunk link that carries the VLANs.
The AP uses the 802.1Q tag to map the VLAN numbers to the appropriate SSIDs.
```

```
The AP then appears as multiple logical APs—one per BSS—with a unique BSSID for each. With
Cisco APs, this is usually accomplished byfor each SSID. incrementing the last digit of the radio’s MAC address
Even though wireless clients can be distributed across many SSIDs, all of those clients must share the same AP’s hardware and must contend for airtime on the same channel.
```

Extended Service Set  
When APs are placed at different geographic locations, they can all be interconnected by a switched infrastructure. The 802.11 standard calls this an extended service set (ESS),  
Ideally,any SSIDs that are defined on one AP should be defined on all the APs in an ESS  
each cell in Figure 26-8 has a unique BSSID, but both cells share one common SSID.

```
Passing from one AP to anotheris called roaming
Each AP offers its own BSS on its own channel, to prevent interference between the APs. As a client device roams from one AP to another, it must scan the available channels to find a new AP
(and BSS) to roam toward.
```

```
(and BSS) to roam toward.
```

```
The 802.11 standard allows two or more wireless clients to communicate directly with each other, with no other means of network connectivity. This is known as an ad hoc wireless network, or an
independent basic service set (IBSS),
One of the devices must take the lead and begin advertising a network name and the necessary
radio parameters, much like an AP would do.
```

Independent Basic Service Set

Other Wireless Topologies  
Repeater  
A wireless repeater takes the signal it receives and repeats or retransmits it in a new cell  
area around the repeater.

```
Some repeaters can use two transmitters and receivers to keep the original and repeated signals isolated on different channels. One transmitter and receiver pair is dedicated to
signals in the AP’s cell, while the other pair is dedicated to signals in the repeater’s own cell.
Workgroup Bridge
WGB acts as an external wireless network adapter for a device that has none.
```

```
You might encounter two types of workgroup bridges:
```

```
You might encounter two types of workgroup bridges:
Universal workgroup bridge (uWGB): wireless network. A single wired device can be bridged to a
Workgroup bridge (WGB)wired devices to be bridged to a wireless network.:A Cisco-proprietary implementation that allows multiple
```

Outdoor Bridge  
act as a bridge to form a single wireless link from one LAN to another over a long distance.  
One AP configured in bridge mode is needed on each end of the wireless link. Special purpose antennas are normally used with the bridges to focus their signals in one direction

```
A point-to-multipoint bridged link allows a central site to be bridged to several other sites
```

Mesh Network  
In a mesh topology, wireless traffic is bridged from AP to AP, in a daisy-chain fashion, using  
another wireless channel.  
Mesh APs can leverage dual radiosone a different range. Each mesh AP usually maintains a BSS on one channel, with which —one using a channel in one range of frequencies and  
wireless clients can associate. Client traffic is then usually bridged from AP to AP over other channels as a backhaul network.  
The mesh network runs its own dynamic routing protocol to work out the best path for backhaul traffic to take across the mesh APs.

RF Overview  
Electromagnetic waves do not travel in a straight line. Instead, they travel by expanding in all directions away from the antenna.  
frequencyin 1 secondof the wave, or the number of times the signal makes one complete up and down cycle

```
A second.hertz (Hz)is themost commonly used frequency unit and is nothing other than one cycle per
```

3 kHz to 300 GHz is commonly called radio frequency (RF).  
Wireless Bands and Channels

Wireless Bands and Channels  
Because a range of frequencies might be used for the same purpose, it is customary to refer to the range as a band of frequencies.  
the range from 530 kHz to around 1710 kHz is used by AM radio stations; therefore, it is commonly called the AM band or the AM broadcast band.  
One of the two main frequency ranges used for wireless LAN communication lies between 2.400  
and 2.4835 GHz. This is usually called the 2.4entire range between 2.4 and 2.5 GHz -GHz band, even though it does not encompass the  
The other wireless LAN range is usually called the 55.825 GHz. The 5-GHz band actually contains the following four separate and distinct bands:-GHz band because it lies between 5.150 and  
5.150 to 5.250 GHz  
5.250 to 5.350 GHz  
5.470 to 5.725 GHz  
5.725 to 5.825 GHz  
Gap between 5.350 and 5.470 this gap exists and cannot be used for wireless LANs.  
Do not worry about memorizing the band names or exact frequency ranges; just be aware of the two main bands at 2.4 and 5 GHz.  
A frequency band contains a continuous range of frequencies.  
bands are usually divided into a number of distinct channels. Each channel is known by a channel  
number and is assigned to a specific frequency.

In the 5not encroach on or overlap the frequencies allocated for any other channel. In other words, the 5-GHz band, this is the case because each channel is allocated a frequency range that does -  
GHz band consists of nonoverlapping channels.  
APs and Wireless Standards

```
Wireless client devices and APs can be compatible with one or more amendments;
APs can usually operate on both bands simultaneously to support any clients that might be present on each band.
wireless clients typically associate with an AP on one band at a time, while scanning for potential
```

wireless clients typically associate with an AP on one band at a time, while scanning for potential APs on both bands. The band used to connect to an AP is chosen according to the operating  
system, wireless adapter driver, and other internal configuration.  
Cisco APs have dual radios (sets of transmitters and receivers) to support BSSs on one 2.4channel and other BSSs on one 5-GHz channel simultaneously. Some models also have two 5-GHz -GHz  
radios that can be configured to operate BSSs on two different channels at the same time,  
providing wireless coverage to higher densities of users that are located in the same vicinity.  
RF signals propagate or reach further on the 2.4to penetrate indoor walls and objects easier at 2.4 GHz than 5 GHz. However, the 2.4-GHz band than on the 5-GHz band. They also tend -GHz band is  
commonly more crowded with wireless devices. Remember that only three nonoverlapping channels are available, so the chances of other neighboring APs using the same channels is  
greater. In contrast, the 5-GHz band has many more channels available to use, making channels  
less crowded and experiencing less interference.

This chapter covers the following exam topics:  
2.0 Network Access  
2.6 Compare Cisco Wireless Architectures and AP modes

Autonomous AP Architecture  
VLANs must be trunked from the distribution layer switch (where routing commonly takes place) to the access layer, where they are extended further over a trunk link to the AP.  
Two wireless users that are associated to the same autonomous AP can reach each other through the AP without having to pass up into the wired network

```
configure SSIDs, VLANs, and many RF parameters like the channel and transmit power to be used.
```

```
An autonomous AP must also be configured with a management IP address so that you can remotely manage it.
```

management address is not normally part of any of the data VLANs, so a dedicated management  
VLAN (i.e., VLAN 10) must be added to the trunk links to reach the AP.  
Each AP must be configured and maintained individually unless you leverage a management platform such as Cisco Prime Infrastructure or Cisco DNA Center.  
That might sound straightforward until you have to add a new VLAN and configure every switch  
and AP in your network to carry and support it.  
Cloud-based AP Architecture  
Cisco Meraki is cloudnetworks built from Meraki products. For example, through the cloud networking service, you can -based and offers centralized management of wireless, switched, and security  
configure and manage APs, monitor wireless performance and activity, generate reports, and so  
on.  
Cisco Meraki APs can be deployed automatically, once you register with the Meraki cloud. Each AP will contact the cloud when it powers up and will self-configure. From that point on, you can  
manage the AP through the Meraki cloud dashboard.  
From the cloud, you can push out code upgrades and configuration changes to the APs in the  
enterprise  
adds the intelligence needed to automatically instruct each AP on which channel and transmit power level to use.  
Can also collect information from all of the APs about things such as RF interference, rogue or  
unexpected wireless devices that were overheard, and wireless usage statistics.

# 27 Wireless Architectures

Wednesday, September 1, 2021 2:55 PM

```
The data path from the wireless network to the wired network is very short; the autonomous AP links the two networks.Data to and from wireless clients does not have to travel up into the cloud
and back; the cloud is used to bring management functions into the data plane.
the network in Figure 27-3 consists of two distinct paths—one for data traffic and another for
management traffic, corresponding to the following two functions:
```

A control plane: Traffic used to control, configure, manage, and monitor the AP itself  
A data plane: End-user traffic passing through the AP  
Split-MAC Architectures

The realmessages. -time processes involve802.11 data encryption is also handled in real time, on a persending and receiving 802.11 frames, beacons, and probe -packet basis. The AP must  
interact with wireless clients on some low level, known as the Media Access Control (MAC) layer. These functions must stay with the AP hardware, closest to the clients.

The management functionsare not integral to handling frames over the RF channels, but are  
things that should be centrally administered.centrally located platform away from the AP.Therefore, those functions can be moved to a

When the functions of an autonomous AP are divided, the AP hardware is known as a lightweight access point, and performs only the real-time 802.11 operation.

domain. the AP is left with duties in Layers 1 and 2, where frames are moved into and out of the RF The AP becomes totally dependent on the WLC for every other WLAN function,such as  
authenticating users, managing security policies, and even selecting RF channels and output power.

The lightweight APMAC operations are pulled apart into two distinct locations.-WLC division of labor is known as a split-MAC architecture, where the normal

the AP and WLC can be located on the same VLAN or IP subnet, but they do not have to be  
CAPWAP relationship actually consists of two separate tunnels, as follows:  
CAPWAP control messagesits operation. The control messages are authenticated and encrypted, so the AP is securely : Carries exchanges that are used to configure the AP and manage

its operation. The control messages are authenticated and encrypted, so the AP is securely controlled by only the appropriate WLC, then transported over the control tunnel.  
CAPWAP data: with the AP. Data packets are transported over the data tunnel but are not encrypted by Used for packets traveling to and from wireless clients that are associated  
default. When data encryption is enabled for an AP, packets are protected with Datagram  
Transport Layer Security (DTLS).  
Every AP and WLC must also authenticate each other with digital certificates. An X.509 certificate is preinstalled in each device when it is purchased.

Notice how VLAN 100 exists at the WLC and in the air as SSID 100, near the wireless clientsnot in between the AP and the WLC —but

Becauseaddress for both management and tunnelingthe AP sits on the access layer where its CAPWAP tunnels terminate, it can use one IP. No trunk link is needed because all of the VLANs it  
supports are encapsulated and tunneled as Layer 3 IP packetsVLANs. ,rather than individual Layer 2

As the wireless network grows, the WLC simply builds more CAPWAP tunnels to reach more Aps

```
WLC can begin offering a variety of additional functions:
Dynamic channel assignment : The WLC canautomatically choose and configure the RF
channel used by each AP, based on other active access points in the area.
Transmit power optimization AP based on the coverage area needed.:The WLC can automatically set the transmit power of each
Self-healing wireless coverage :If an AP radio dies, the coverage hole can be “healed” by
turning up the transmit power of surrounding APs automatically.
Flexible client roaming : Clients can roam between APs with very fast roaming times.
Dynamic client load balancing geographic area, the WLC can associate clients with the least used AP. This distributes the : If two or more APs are positioned to cover the same
client load across the APs.
RF monitoring usage. By listening to a channel, the WLC can remotely gather information about RF : TheWLC manages each AP so that it scans channels to monitor the RF
interference, noise, signals from neighboring APs, and signals from rogue APs or ad hoc clients.
Security management : The WLC can authenticate clients from a central service and can
require wireless clients to obtain an IP address from a trusted DHCP server before allowing them to associate and access the WLAN.
Wireless intrusion protection system client data to detect and prevent malicious activity.: Leveraging its central location, the WLC can monitor
```

Comparing Wireless LAN Controller Deployments

Comparing Wireless LAN Controller Deployments  
locate the WLC in a central location so that you can maximize the number of APs joined to itis usually called a unified or centralized WLC deployment. This

```
Typical unified WLCs can support a maximum of 6000 APs
A WLC can also be located in a central position in the network, inside a data center in a private cloud, as shown in Figure 27-9. This is known as a cloud-based WLC deployment, where the WLC
exists as a virtual machine rather than a physical device.
Such a controller can typically support up to 3000 APs.
```

```
For small campuses or distributed branch locations, where the number of APs is relatively small in
```

For small campuses or distributed branch locations, where the number of APs is relatively small in each, the WLC can be co-located with a stack of switches, as shown in Figure 27-10. This is known  
as an embedded WLC deployment  
Typical Cisco embedded WLCs can support up to 200 APsto be connected to the switches that host the WLC. The APs do not necessarily have

the a Cisco WLC function can be coMobility Express WLC deployment-located with an AP that is installed at the branch site. This is known as

```
A Mobility Express WLC can support up to 100 APs.
```

Cisco AP Modes  
WLC, you can also configure a lightweight AP to operate in one of the following specialmodes: -purpose  
**Local** :The default lightweight mode that offers one or more functioning BSSs on a specific  
channel. measure the level of noise, measure interference, discover rogue devices, and match against During times that it is not transmitting, the AP will scan the other channels to  
intrusion detection system (IDS) events.  
**Monitor** sensor. The AP checks for IDS events, detects rogue access points, and determines the : The AP does not transmit at all, but its receiver is enabled to act as a dedicated  
position of stations through location-based services.  
**FlexConnect** its CAPWAP tunnel to the WLC is down and if it is configured to do so.: An AP at a remote site can locally switch traffic between an SSID and a VLAN if  
**Sniffer** sniffer or packet capture device. The captured traffic is then forwarded to a PC running : An AP dedicates its radios to receiving 802.11 traffic from other sources, much like a  
network analyzer software such as Wildpackets OmniPeek or WireShark, where it can be analyzed further.  
**Rogue detector** addresses heard on the wired network with those heard over the air. Rogue devices are : An AP dedicates itself to detecting rogue devices by correlating MAC  
those that appear on both networks.  
**Bridge** two networks. Two APs in bridge mode can be used to link two locations separated by a : An AP becomes a dedicated bridge (point-to-point or point-to-multipoint) between

two networks. Two APs in bridge mode can be used to link two locations separated by a distance. Multiple APs in bridge mode can form an indoor or outdoor mesh network.  
**Flex+Bridge** : FlexConnect operation is enabled on a mesh AP.  
**SE-Connect** :The AP dedicates its radios to spectrum analysis on all wireless channels. You  
can remotely connect a PC running software such as MetaGeek Chanalyzer or Cisco Spectrum Expert to the AP to collect and analyze the spectrum analysis data to discover  
sources of interference.  
Remember thatclient devices to associate to wireless LANs. When an AP is configured to operate in one of the a lightweight AP is normally in local mode when it is providing BSSs and allowing  
other modes, local mode (and the BSSs) is disabled.

This chapter covers the following exam topics:  
1.0 Network Fundamentals  
1.11 Describe wireless principles  
1.11.d Encryption  
5.0 Security Fundamentals  
5.9 Describe wireless security protocols (WPA, WPA2, and WPA3)

A comprehensive approach to wireless security focuses on the following areas:  
Identifying the endpoints of a wireless connection  
Identifying the end user (authentication)  
Protecting the wireless data from eavesdroppers (encryption)  
Protecting the wireless data from tampering (integrity)  
Authentication  
To use a wireless network, it. Clients should be authenticated by some means before they can become functioning members of the wireless LAN.clients must first discover a basic service set (BSS) and then request permission to associate with  
A fake AP could also send spoofed management frames to disassociate or deauthenticate legitimate and active clients, just to disrupt normal network operation.  
To prevent this type of manauthenticated -in-the-middle attack, the client should authenticate the AP before the client itself is

Message Privacy  
data should be encrypted for its journey through free space. This is accomplished by encrypting the data payload in each wireless frame just prior to being transmitted, then decrypting it as it is received. The idea is to use an encryption method  
that the transmitter and receiver share, so the data can be encrypted and decrypted successfully.  
the AP should securely negotiate a unique encryption key to use for each associated client.  
No other device should know about or be able to use the same keys to eavesdrop and decrypt the data.  
The Each of the associated clients uses the same group key to decrypt the data.AP also maintains a “group key” that it uses when it needs to send encrypted data to all clients in its cell at one time.

Message Integrity  
what if someone managed to alter the contents along the way? The recipient would have a very difficult time discovering that the original data had been modified.

## 28 Wireless security

Thursday, September 2, 2021 11:46 AM

```
Amessage integrity check (MIC)is a security tool that can protect against data tampering.
a way for the sender to add a secret stamp inside the encrypted data frame. The stamp is based on the contents of the data bits to be transmitted. Once the recipient decrypts the frame, it can compare the secret stamp to its own
idea of what the stamp should be, based on the data bits that were received. If the two stamps are identical, the recipient can safely assume that the data has not been tampered with.
```

Wireless Client Authentication Methods

1. Open Authentication  
    original 802.11 standard offered only two choices to authenticate a client: open authentication and WEP.  
    Open authentication is true to its name; it offers use an 802.11 authentication request before it attempts to associate with an AP. No other credentials are needed.open access to a WLAN. The only requirement is that a client must  
    Most client operating systems flag such networks to warn you that your wireless data will not be secured in any way if you join.
2. WEP  
    open authentication offers nothing that can obscure or encrypt the data being sent between a client and an AP.  
    Wired Equivalent Privacy (WEP)  
    WEP same algorithm encrypts data at the sender and decrypts it at the receiver.uses the RC4 cipher algorithm to make every wireless data frame private and hidden from eavesdroppers. The The algorithm uses a string of bits as a  
    key, commonly called a WEP key, to derive other encryption keysreceiver have an identical key, one can decrypt what the other encrypts.—one per wireless frame. As long as the sender and  
    WEP is ahead of time, so that each can derive other mutually agreeable encryption keysknown as a shared-key security method. The same key must be shared between the sender and receiver. In fact, every potential client and AP  
    must share the same key ahead of time so that any client can associate with the AP.  
    The WEP key use the correct WEP key, it cannot associate with an AP. The AP tests the client’s knowledge of the WEP key by can also be used as an optional authentication method as well as an encryption tool. Unless a client can  
    sending it a random challenge phrase. The client encrypts the challenge phrase with WEP and returns the result to the AP. The AP can compare the client’s encryption with its own to see whether the two WEP keys yield identical results.  
    WEP keys can be either 40 or 104 bits long, represented by a string of 10 or 26 hex digits  
    longer keys offer more unique bits for the algorithm, resulting in more robust encryption

```
longer keys offer more unique bits for the algorithm, resulting in more robust encryption
WEP was officially deprecated. Both WEP encryption and WEP sharedweak methods to secure a wireless LAN. -key authentication are widely considered to be
```

3. 802.1x/EAP  
    With only open authentication and WEP available in the original 802.11 standard, a more secure authentication method was needed.  
    Extensible Authentication Protocol (EAP)  
    EAP is extensible and does not consist of any one authentication method.  
    EAP defines through this section, notice how many authentication methods have EAP in their names. Each method is unique and a set of common functions that actual authentication methods can use to authenticate users. As you read  
    different, but each one follows the EAP framework.  
    itnetwork media until a client authenticates.can integrate with the IEEE 802.1x port-based access control standardThis means that a wireless client might be able to associate with an AP but. When 802.1x is enabled, it limits access to a  
    will not be able to pass data to any other part of the network until it successfully authenticates.  
    with 802.1x; the client uses open authentication to associate with the AP, and then the actual client authentication process occurs at a dedicated authentication server  
    shows the three-party 802.1x arrangement that consists of the following entities:  
    Supplicant: The client device that is requesting access  
    Authenticator[WLC]) : The network device that provides access to the network (usually a wireless LAN controller  
    Authentication server (AS)access based on a user database and policies (usually a RADIUS server): The device that takes user or client credentials and permits or denies network

```
The wireless LAN controller becomes a middleman in the client authentication process, controlling user access with 802.1x and communicating with the authentication server using the EAP framework.
The goal here is to become aware of the many methods without trying to memorize them all
even when you configure user authentication on a wireless LAN, you will not have to select a specific method. Instead, you select 802.1x on the WLC so that it is ready to handle a variety of EAP methods. It is then up to the client
and the authentication server to use a compatible method.
```

```
and the authentication server to use a compatible method.
```

4. LEAP  
    proprietary wireless authentication method called supply username and password credentials. Both the authentication server and the client exchange challenge Lightweight EAP (LEAP). To authenticate, the client must  
    messages that are then encrypted and returned.  
    the method used to encrypt the challenge messages was found to be vulnerable, so LEAP has since been deprecated. Even though wireless clients and controllers still offer LEAP, you should not use it.
5. EAP-FAST  
    Cisco developed a more secure method called Authentication credentials are protected by passing aEAP Flexible Authentication by Secure Tunneling (EAPprotected access credential (PAC)between the AS and -FAST).  
    the supplicant. The PAC is authentication. a form of shared secret that is generated by the AS and used for mutual  
    EAP-FAST is a sequence of three phases:  
    Phase 0: The PAC is generated or provisioned and installed on the client.  
    Phase 1: Security (TLS) tunnel.After the supplicant and AS have authenticated each other, they negotiate a Transport Layer  
    Phase 2: The end user can then be authenticated through the TLS tunnel for additional security.  
    two separate authentication processes occur in EAPwith the end user. These occur in a nested fashion, as an outer authentication (outside the TLS tunnel) and an -FAST—one between the AS and the supplicant and another  
    inner authentication (inside the TLS tunnel).  
    a RADIUS server is required. However, the RADIUS server must also operate as an EAPgenerate PACs, one per user. -FAST server to be able to
6. PEAP  
    Protected EAP (PEAP) method uses an inner and outer authentication  
    the AS presents a digital certificate to authenticate itself with the supplicant in the outer authentication. If the supplicant is satisfied with the identity of the AS, the two will build a TLS tunnel to be used for the inner client  
    authentication and encryption key exchange.  
    The digital certificate of the AS consists of data in a standard format that identifies the owner and is “signed” or validated by a third party. The third party is known as a certificate authority (CA) and is known and trusted by  
    both the AS and the supplicants. The supplicant must also possess the CA certificate just so that it can validate the one it receives from the AS. The certificate is also used to pass a public key, in plain view, which can be used  
    to help decrypt messages from the AS.  
    only the AS has a certificate for PEAP  
    it must be authenticated within the TLS tunnel using one of the following two methods:  
    MSCHAPv2: Microsoft Challenge Authentication Protocol version 2  
    GTCmanually generated password: Generic Token Card; a hardware device that generates one-time passwords for the user or a
7. EAP-TLS

```
PEAP leverages a digital certificate on the AS as a robust method to authenticate the RADIUS server
EAP Transport Layer Security (EAP-TLS)
goes one step further by requiring certificates on the AS and on every client device.
the AS and the supplicant exchange certificates and can authenticate each other. A TLS tunnel is built afterward so that encryption key material can be securely exchanged.
EAP-TLS is considered to be the most secure wireless authentication method available;
implementing it can sometimes be complex.
Along with the AS, each wireless client must obtain and install a certificate
EAPsuch as communicators, medical devices, and RFID tags, have an underlying operating system that cannot -TLS is practical only if the wireless clients can accept and use digital certificates. Many wireless devices,
interface with a CA or use certificates.
```

```
original method to secure wireless data from eavesdroppers: WEP
WEP has been compromised, deprecated, and can no longer be recommended.
```

```
Temporal Key Integrity Protocol (TKIP)
TKIP adds the following security features using legacy hardware and the underlying WEP encryption:
MIC:commonly called “Michael” as an informal reference to MIC.This efficient algorithm adds a hash value to each frame as a message integrity check to prevent tampering;
Time stamp: have already been sent.A time stamp is added into the MIC to prevent replay attacks that attempt to reuse or replay frames that
Sender’s MAC address:The MIC also includes the sender’s MAC address as evidence of the frame source.
TKIP sequence counter: from being replayed as an attack.This feature provides a record of frames sent by a unique MAC address, to prevent frames
Key mixing algorithm: This algorithm computes a unique 128-bit WEP key for each frame.
Longer initialization vector (IV)WEP keys by brute-force calculation.: The IV size is doubled from 24 to 48 bits, making it virtually impossible to exhaust all
```

```
TKIP
```

Wireless Privacy and Integrity Methods

should be avoided if a better method is available.In fact, TKIP was deprecated in the 802.11-2012 standard.  
CCMP  
Counter/CBC-MAC Protocol (CCMP)  
more secure than TKIP.CCMP consists of two algorithms:  
AES counter mode encryption  
Cipher Block Chaining Message Authentication Code (CBC-MAC) used as a message integrity check (MIC)

Cipher Block Chaining Message Authentication Code (CBC-MAC) used as a message integrity check (MIC)  
(AES) is the current encryption algorithm adopted by U.S. National Institute of Standards and Technology (NIST) and the U.S. government, and widely used around the world  
AES is open, publicly accessible, and represents the most secure encryption method available today.  
client devices and APs must support the AES counter mode and CBClegacy devices that support only WEP or TKIP. How can you know if a device supports CCMP? Look for the WPA2 -MAC in hardware. CCMP cannot be used on  
designation, which is described in the following section.  
GCMP  
Galois/Counter Mode Protocol (GCMP)  
more efficient than CCMP  
GCMP consists of two algorithms:  
AES counter mode encryption  
Galois Message Authentication Code (GMAC) used as a message integrity check (MIC)  
GCMP is used in WPA3  
WPA, WPA2, and WPA3  
Wi-Fi Protected Access (WPA) industry certifications.  
WPA was based on parts of 802.11i and included 802.1x authentication, TKIP, and a method for dynamic encryption key management.  
WPA2 is based around the superior AES CCMP algorithms, rather than the deprecated TKIP from WPA  
WPA3 leverages stronger encryption by AES with the Galois/Counter Mode Protocol (GCMP). It Management Frames (PMF)to secure important 802.11 management frames between APs and clients, to prevent malicious also uses Protected  
activity that might spoof or tamper with a BSS’s operation.  
WPA3 includes other features beyond WPA and WPA2secrecy, and Protected management frames (PMF). , such asSimultaneous Authentication of Equals (SAE), Forward  
You should avoid using WPA and use WPA2 insteaddevices, APs, and WLCs. —at least until WPA3 becomes widely available on wireless client

all three WPA versions support two client authentication modes: a pre-shared key (PSK) or 802.1x  
These are also known as personal mode and enterprise mode, respectively. With

```
a key string must be shared or configured on every client and AP before the clients can connect to the wireless network. The pre-shared key is normally kept confidential so that unauthorized users have no knowledge of it. The
key string is never sent over the air. Instead, clients and APs work through a fourthe pre-shared key string to construct and exchange encryption key material that can be openly exchanged.-way handshake procedure that uses
```

```
personal mode,
```

```
a malicious user can eavesdrop and capture the fourthen use a dictionary attack to automate guessing the pre-way handshake between a client and an AP. That user can -shared key. If he is successful, he can then decrypt
the wireless data or even join the network posing as a legitimate user.
```

```
WPA-Personal and WPA2-Personal modes
```

WPA3-Personal  
avoids such an attack by strengthening the key exchange between clients and APs through a method known as Simultaneous Authentication of Equals (SAE). Rather than a client authenticating against a server or AP, the  
client and AP can initiate the authentication process equally and even simultaneously.  
Even if a password or key is compromised, WPA3from being able to use a key to unencrypt data that has already been transmitted over the air-Personal offers forward secrecy, which prevents attackers.  
The Personal mode of any WPA version is usually easy to deploy in a small environment or with clients that are embedded in certain devices because a simple text key string is all that is needed to authenticate the clients.Be  
aware thaupdate or change the key, you must touch every device to do so. As well, the pret every device using the WLAN must be configured with an identical pre-shared key should remain a well -shared key. If you ever need to  
kept secret; you should never divulge the pre-shared key to any unauthorized person.  
WPA, WPA2, and WPA3 also support  
802.1x or enterprise authentication.  
EAP-based authentication  
WPA versions do not require any specific EAP method

```
WPA versions do not require any specific EAP method
interoperability with well-known EAP methods like EAP-TLS, PEAP, EAP-TTLS, and EAP-SIM
Enterprise authentication is more complex to deploy than personal mode because authentication servers must be set up and configured as a critical enterprise resource.
You should always select the highest WPA version that the clients and wireless infrastructure in your environment will support.
```

an effective wireless security strategy includes a method to authenticate clients and a method to provide data privacy and integrity. These two types of methods are listed in the leftmost column. Work your way to the right to remember what types of  
authentication and privacy/integrity are available. The table also expands the name of each acronym as a memory tool.

WPA, WPA2, and WPA3 simplify wireless network configuration and compatibility because they limit which authentication and privacy/integrity methods can be used.

multiple VLANs must be brought to it over a trunk link.  
The wireless side of an AP inherently trunks 802.11 frames by marking them with the BSSID of the WLAN where they belong.

lightweight AP  
Wired VLANs that terminate at the WLC can be mapped to WLANs that emerge at the AP.  
The AP needs only an access link to connect to the network infrastructure and terminate its end of the tunnel

you can also use Telnet or SSH to connect to its CLI over the wired networkbrowser-based management sessions via HTTP and HTTPS.You can manage lightweight APs from a .Autonomous APs support  
browser session to the WLC.

you can also use Telnet or SSH to connect to its CLI over the wired network. Autonomous APs support browser-based management sessions via HTTP and HTTPS. You can manage lightweight APs from a  
browser session to the WLC.  
Accessing a Cisco WLC  
management users to log in. Users can be authenticated against an internal list of local usernames or against an authentication, authorization, and accounting (AAA) server, such as TACACS+ or  
RADIUS.  
When you are successfully logged in, the WLC will display a monitoring dashboard  
must click on the Advanced link in the upper-right corner. This will bring up the full WLC GUI

## 29 Wireless LAN

Wednesday, November 24, 2021 11:34 AM

Monitor, WLANs, Controller, Wireless, Security, and so on.  
Connecting a Cisco WLC  
Cisco wireless controllers differ a bit; ports and interfaces refer to different concepts.  
Controller ports are physical connections made to an external wired or switched network, whereas interfaces are logical connections made internally within the controller

Using WLC Ports  
You can connect several different types of controller ports to your network, as shown in Figure 29 - 5 and discussed in the following list:  
**Service port:** functions; always connects to a switch port in access modeUsed for out-of-band management, system recovery, and initial boot  
**Distribution system port:** to a switch port in 802.1Q trunk modeUsed for all normal AP and management traffic; usually connects  
**Console port:** functions; asynchronous connection to a terminal emulator (9600 baud, 8 data bits, 1 stop Used for out-of-band management, system recovery, and initial boot  
bit, by default)  
**Redundancy port:** Used to connect to a peer controller for high availability (HA) operation  
Controllers can have a single service port that must be connected to a switched network. Usually, the service port is assigned to a management VLAN so that you can access the controller with SSH  
or a web browser to perform initial configuration or for maintenance. Notice that the service port supports only a single VLAN, so the corresponding switch port must be configured for access mode  
only.  
Controllers also have multiple distribution system ports that you must connect to the network. These ports carry most of the data coming to and going from the controller. For example, the  
CAPWAP tunnels (control and data) that extend to each of a controller’s APs pass across the distribution system ports. Client data also passes from wireless LANs to wired VLANs over the  
ports. In addition, any management traffic using a web browser, SSH, Simple Network Management Protocol (SNMP), Trivial File Transfer Protocol (TFTP), and so on, normally reaches  
the controller in-band through the ports.  
the distribution system ports always operate in 802.1Q trunking mode.  
The distribution system ports can operate independently, each one transporting multiple VLANs to a unique group of internal controller interfaces. For resiliency, you can configure  
distribution system ports in redundant pairs. One port is primarily used; if it fails, a backup

```
distribution system ports in redundant pairs. One port is primarily used; if it fails, a backup port is used instead.
Controller distribution system ports can be configured as a link aggregation group (LAG) such that they are bundled together to act as one larger link
traffic can be load-balanced across the individual ports that make up the LAG
LAG offers resiliency; if one individual port fails, traffic will be redirected to the remaining working ports instead.
Cisco WLCs do not support any link aggregation negotiation protocol, like LACP or PAgP, at all.
```

Using WLC Interfaces  
the controller must somehow map those wired VLANs to equivalent logical wireless networks  
APs.VLAN must be connected to a unique wireless LAN that exists on a controller and its associated  
Cisco wireless controllers provide the necessary connectivity through internal logical interfaces, which must be configured with an IP address, subnet mask, default gateway, and a Dynamic Host  
Configuration Protocol (DHCP) server. Each interface is then assigned to a physical port and a VLAN ID. You can think of an interface as a Layer 3 termination on a VLAN.  
Cisco controllers support the following interface types:  
**Management interface:** authentication, WLC-to-WLC communication, webUsed for normal management traffic, such as RADIUS user -based and SSH sessions, SNMP, Network  
Time Protocol (NTP), syslog, and so on. The management interface is also used to terminate CAPWAP tunnels between the controller and its APs.  
**Redundancy management** a high availability pair of controllers. The active WLC uses the management interface : The management IP address of a redundant WLC that is part of  
address, while the standby WLC uses the redundancy management address.  
**Virtual interface:** DHCP requests, performing client web authentication, and supporting client mobility.IP address facing wireless clients when the controller is relaying client  
**Service port interface:** Bound to the service port and used for out-of-band management.  
**Dynamic interface:** Used to connect a VLAN to a WLAN.

The management interface faces the switched network, where management users and APs are located. Management traffic will usually consist of protocols like HTTPS, SSH, SNMP, NTP, TFTP,  
and so on  
consists of CAPWAP packets that carry control and data tunnels to and from the APs.  
The virtual interface is used only for certain client-facing operations.  
when a wireless client issues a request to obtain an IP address, the controller can relay the request on to an actual DHCP server that can provide the appropriate IP address  
DHCP server appears to be the controller’s virtual interface address. Clients may see the virtual interface’s address, but that address is never used when the controller  
communicates with other devices on the switched network.  
Because the virtual interface is used only for some client management functions, you should configure it with a unique, nonroutable address. For example, you might use 10.1.1.1  
because it is within a private address space defined in RFC 1918.  
The virtual interface address is also used to support client mobility.  
every controller that exists in the same mobility group should be configured with a virtual address that is identical to the others. By using one common virtual address, all  
the controllers will appear to operate as a cluster as clients roam from controller to controller.  
Dynamic interfaces map WLANs to VLANs,  
making the logical connections between wireless and wired networks. You will configure one dynamic interface for each wireless LAN that is offered by the controller’s APs and then  
map the interface to the WLAN.  
Each dynamic interface must also be configured with its own IP address and can act as a DHCP relay for wireless clients. To filter traffic passing through a dynamic interface, you can  
configure an optional access list.  
Configuring a WLAN  
To complete the path between the SSID and the VLAN, as illustrated in Figure 29define a WLAN on the controller. -7, you must first

The controller will bind the WLAN to one of its interfaces and then push the WLAN configuration out to all of its APs by default.

Like VLANs, you can use WLANs to segregate wireless users and their traffic into logical networks. Users associated with one WLAN cannot cross over into another one unless their  
traffic is bridged or routed from one VLAN to another through the wired network infrastructure.

Cisco controllers support a maximum of 512 WLANs, but only 16 of them can be actively configured on an AP.  
Advertising each WLAN to potential wireless clients uses up valuable airtime.  
Every AP must broadcast beacon management frames at regular intervals to advertise the existence of a BSS

Beacons are normally sent 10 times per second, or once every 100 ms, at the lowest mandatory data rate  
if you create too many WLANs, a channel can be starved of any usable airtime  
always limit the number of WLANs to five or fewer; a maximum of three WLANs is best  
Before you create a new WLAN, think about the following parameters it will need to have:  
SSID string  
Controller interface and VLAN number  
Type of wireless security needed  
you will create the appropriate dynamic controller interface to support the new WLAN; then you will enter the necessary WLAN parameters

```
Step 1. Configure a RADIUS Server
RADIUS server, such as WPA2-Enterprise or WPA3-Enterprise,
Select Security > AAA > RADIUS > Authentication to see a list of servers that have already been configured
If multiple servers are defined, the controller will try them in sequential order. Click New to create a new server.
```

```
Next, enter the server’s IP address, shared secret key, and port number Because the controller already had two other RADIUS servers configured, the server at
192.168.200.30 will be index number 3. Be sure to set the server status to Enabled so that the controller can begin using it. At the bottom of the page, you
can select the type of user that will be authenticated with the server. Check Network User to authenticate wireless clients or Management to authenticate
wireless administrators that will access the controller’s management functions. Click Apply to complete the server configuration.
```

Step 2. Create a Dynamic Interface  
create a new dynamic interface, navigate to Controller > Interfaces. You should see a list of all the controller interfaces that are currently configured  
Click the New button to define a new interface. Enter a name for the interface and the VLAN number it will be bound to. In Figure 29-11, the interface named  
Engineering is mapped to wired VLAN 100. Click the Apply button

```
Next, enter the IP address, subnet mask, and gateway address for the interface. You should also define primary and secondary DHCP server addresses that the
controller will use when it relays DHCP requests from clients that are bound to the interface
Click the Apply button to complete the interface configuration and return to the list of interfaces.
```

Step 3. Create a New WLAN  
selecting WLANs from the top menu bar (displays current WLANs)  
You can create a new WLAN by selecting Create New from the dropand then clicking the Go button. -down menu  
Next, enter a descriptive name as the profile name and the SSID text string.  
The ID number is used as an index into the list of WLANs that are defined on the controller. The ID number becomes useful when you use templates in Prime  
Infrastructure (PI) to configure WLANs on multiple controllers at the same time.

```
WLAN templates are applied to specific WLAN ID numbers on controllers. The WLAN ID is only locally significant and is not passed between controllers. As a
rule, you should keep the sequence of WLAN names and IDs consistent across multiple controllers so that any configuration templates you use in the future
will be applied to the same WLANs on each controller.
Click the Apply button to create the new WLAN. The next page will allow you to edit four categories of parameters, corresponding to the tabs across the top
```

```
You can control whether the WLAN is enabled or disabled with the Status check box
Under Radio Policy, select the type of radio that will offer the WLAN. By default, the WLAN will be offered on all radios that are joined with the controller. You
can select a more specific policy with 802.11a only, 802.11a/g only, 802.11g only, or 802.11b/g only.
Next, select which of the controller’s dynamic interfaces will be bound to the WLAN. By default, the management interface is selected. The drop-down list
contains all the interface names that are available
Finally, use the Broadcast SSID check box to select whether the APs should broadcast the SSID name in the beacons they transmit.
Hiding the SSID name, by not broadcasting it, does not really provide any worthwhile security
```

Configuring WLAN Security  
Select the Security tab to configure the security settings. By default, the Layer 2 Security tab is selected. From the Layer 2 Security drop-down menu, select the appropriate security scheme to  
use. Table 29-2 lists the types that are available.

Further down the screen, you can select which specific WPA, WPA2, and WPA3 methods to support on the WLAN

To use WPA2would be used to authenticate wireless clients against one or more RADIUS servers.-Enterprise, the 802.1X option would be selected. In that case, 802.1x and EAP

To specify which servers the WLAN should use, you would select the Security tab and then the AAA Servers tab in the WLAN edit screen. You can identify up to six specific RADIUS  
servers in the WLAN configuration. Beside each server, select a specific server IP address from the drop-down menu of globally defined servers. The servers are tried in sequential  
order until one of them responds

```
By default, a controller will contact a RADIUS server from its management interface. You can override this behavior by checking the box next to Radius Server Overwrite Interface so that
the controller sources RADIUS requests from the dynamic interface that is associated with the WLAN.
```

Configuring WLAN QoS  
Select the QoS tab to configure quality of service settings for the WLAN  
By default, the controller will consider all frames in the WLAN to be normal data, to be handled in a “best effort” manner. You can set the Quality of Service (QoS) drop-down menu to classify all  
frames in one of the following ways:  
Platinum (voice)  
Gold (video)  
Silver (best effort)  
Bronze (background)

```
You can also set the Wibandwidth parameters on the QoS page-Fi Multimedia (WMM) policy, call admission control (CAC) policies, and
```

bandwidth parameters on the QoS page  
Configuring Advanced WLAN Settings  
Advanced Tab  
can enable functions such as coverage hole detection, peerexclusion, client load limits, and so on. -to-peer blocking, client

By default, client sessions with the WLAN are limited to 1800 seconds (30 minutes). Once that session time expires, a client will be required to reauthenticate. This setting is  
controlled by the Enable Session Timeout check box and the Timeout field.  
all clients are subject to the policies configured under Security > Wireless Protection Policies > Client Exclusion Policies. These policies include excessive 802.11 association  
failures, 802.11 authentication failures, 802.1x authentication failures, web authentication failures, and IP address theft or reuse. Offending clients will be automatically excluded or  
blocked for 60 seconds, as a deterrent to attacks on the wireless network.  
Finalizing WLAN Configuration

```
by default, a controller will not allow management traffic that is initiated from a WLAN. That means you (or anybody else) cannot access the controller GUI or CLI from a wireless device that is
associated to the WLAN. This is considered to be a good security practice because the controller is kept isolated from networks that might be easily accessible or where someone might eavesdrop
on the management session traffic
You can change the default behavior on a global basis (all WLANs) by selecting the Management
```

You can change the default behavior on a global basis (all WLANs) by selecting the Management tab and then selecting Mgmt Via Wireless, as shown in Figure 29-21. Check the box to allow  
management sessions from any WLAN that is configured on the controller.

```
Chapter 1. Introduction to TCP/IP Transport and Applications
This chapter covers the following exam topics:
1.0 Network Fundamentals
1.5 Compare TCP to UDP
4.0 IP Services
4.3 Explain the role of DHCP and DNS in the network
```

```
TCP/IP Layer 4 Protocols: TCP and UDP
```

- - TCP provides retransmission (error recovery) and TCP helps to avoid congestion (flow control),
- - UDP needs fewer bytes in its header (less overhead)UDP software does not slow down data transfer
- - TCP can purposefully slow down data transferVoice over IP (VoIP) and video over IP, do not need error recovery, so they use UDP
- Multiplexing using ports

```
UDP Supports:
```

- Multiplexing using ports
- Error recovery (reliability) ○ numbering and acknowledging data with sequence and acknowledgment header fields
- Flow control using windowing ○ use window sizes to protect buffer space

```
○ initialize port numbers and sequence and acknowledgment fields
```

- Connection establishment and termination
- Ordered data transfer and segmentation

```
TCP Supports:
```

```
○○ source port/ destination portSequence Number
○ Acknowledgement Number
○ Offset, Reserved, Flag bits, Window
○ Checksum, Urgent
```

- TCP header is 20 bytes (without options)

```
Transmission Control Protocol
```

```
*TCP segment, Layer 4 PDU, or L4PDU
```

# 1 TCP/IP Transport and Applications

Friday, September 3, 2021 10:34 AM

```
example
All open on one computer:
Port 80 Web ServerPort 800 Ad Server
Port 9876 Wire Application
Socket
```

- Includes IP address, transport protocol, and port number
- (10.1.1.2, TCP, port 80)

Multiplexing

- 0 to 1023

Well Known (System) Ports:

- 1024 to 49151

User (Registered) Ports:

- 49152 to 65535,
- not assigned
    - - uses the same port number for all connections. For example, web server with 100 clients would have only one socket (one port number)
    - server looks at source port of received TCP segments.
- Servers use well-known ports (or user ports), whereas clients use dynamic ports

Ephemeral (Dynamic, Private) Ports:

Popular TCP/IP Applications  
Simple Network Management Protocol (SNMP)

- - query, compile, store, and display information about a network’s operationCisco Prime software  
        FTP/ TFTP
- FTP allows many more features
- TFTPis very simple, good tools for embedded parts of networking devices.  
    SMTP/ POP3
- Simple Mail Transfer Protocol (SMTP) and Post Office Protocol version 3 (POP3)
- both used for transferring mail (TCP).  
    Port numbers and protocols

Port numbers and protocols

- - FTP Data TCP 20FTP Control TCP 21
- - SSH TCP 22Telnet TCP 23
- SMTP TCP 25
- - DNS UDP/TCP 53DHCP Server UDP 67
- - DHCP Client UDP 68TFTP UDP 69
- - HTTP TCP 80POP2 TCP 110
- SNMP UDP 161
- - SSL TCP 443Syslog UDP 514

Connection Establishment and Termination

```
▪▪ SYN, DPORT=80, SPORT=49145SYN ACK , DPORT= 49145, SPORT=80
▪ ACK DPORT=80, SPORT=49145
```

- - initializing Sequence and Acknowledgment fields agreeing on the port numbers
- 2 bits inside the flag fields of the TCP header. Called the SYN and ACK flags

```
TCP connection establishment (3 way handshake) occurs 1st
```

```
TCP connection termination. (four-way)
```

```
▪▪ ACK, FIN >< ACK
▪▪ ACK, FIN << ACK
```

- uses an additional flag, called the FIN bit

Error Recovery and Reliability

- - reliability in both directionsSequence Number field of one direction and Acknowledgment field in the other direction
        - 1000 bytes, Seq = 1000 >
        - - 1000 bytes, Seq = 2000 >1000 bytes, Seq = 3000 >
        - < no data, ACK = 4000  
            ▪ received all data with sequence numbers up through one less than 4000  
            ▪ ready to receive your byte 4000 next.
- - ack by listing the next expected byte (forward acknowledgment)sequence number field identifies the data (sender)
- forward acknowledgments acknowledge the data (receiver)

- forward acknowledgments acknowledge the data (receiver)
    - - ask the sending host to resendacknowledge that the re-sent data arrived
- Sequence and Acknowledgment fields let the receiving host can notice lost data
    - - 1000 bytes, SEQ 1000 >1000 bytes, SEQ 2000 X>
    - 1000 bytes, SEQ 3000 >  
        □ (received 1000 -1999 and 3000 -3999, asking for 2000)
    - < no data, ACK = 2000
    - 1000 bytes, SEQ 2000 >
    - < no data, ACK 4000
    - Sender may wait a few moments to make sure no other acknowledgments arrive
    - Retransmission timer

Flow Control Using Windowing  
Sliding window (dynamic window- Receiver slides the window size up and down

- - < ACK=1000, Window=3000SEQ=1000, SEQ=2000, SEQ=3000 >
- < ACK=4000, Window=4000  
    User Datagram Protocol
- connectionless
- - no reliability, no windowing,
- - no reordering of the received data, andno segmentation of large chunks of data into the right size for transmission
- - provides data transfer and multiplexing using port numbersLess overhead and processing than TCP.
- no reordering or recovery
- DNS requests use UDP, user will retry an operation if the DNS resolution failsNetwork File System (NFS), a remote file system application, performs recovery with  
    application layer code, so UDP features are acceptable to NFS.

##### -

- - Source port, Destination PortLength, Checksum
- 8 byte header

```
Uniform Resource Identifiers (URI)
```

- - clicking a link and typing a URIreferred to as web address or Universal (uniform) Resource Locator [URL]—refer to a URI
- three key components
    - before the :// identifies the protocol
    - - between the // and / identifies the server by nameafter the / identifies the web page.

TCP/IP Applications

- [http://](http:) (Scheme)
- - [http://www.certskills.com/blog](http://www.certskills.com/blog) (path) (Authority)
- - < Name Resolution Request (IP Header, UDP Header, DNS Request)Name resolution Reply (Ip Header, UDP Header, DNS Request (IP address) >
- < TCP connection to requested web server
- - DNS requests can be cached by hosts and serversLocal DNS may need to ask for help
- Sends repeated DNS messages to find the authoritative DNS server.

```
➢➢ Root DNS .com TLD DNS
➢ Authoritative cisco.com DNS
```

- Recursive DNS lookup- host > Enterprise DNS >
- The enterprise DNS acts as a recursive DNS server

##### DNS

- HTTP GET request lists file it needs
- - HTTP GET response from server with a Server may issue areturn code of 404, (file not found)return code of 200 (meaning OK) and file’s contents.
- Web pages consist of multiple files, called objects
- Objects are stored as different files on the web serverWeb browser gets the first file which can include references to other URIs that the browser  
    also requests

##### -

- - < HTTP GET /go/ccnaHTTP OK data >
- < HTTP GET /graphics/logo1.gif
- - HTTP OK data >< HTTP GET /graphics/ad1.gif
- HTTP OK data >
    - Flow over one or more TCP connection between the client and the server.

Transferring Files with HTTP

Identifying the Correct Receiving Application

- tracks which port opened which request

Fields that identify next header  
< Ethernet (Type) (0x0800)  
< IPv4 (Protocol) (6)< TCP (Destination port) (49124)

This chapter covers the following exam topics:  
5.0 Security Fundamentals  
5.6 Configure and verify access control lists

Can be used to match packets for applying Quality of Service (QoS) features.  
ACL Location and Direction

- inbound to the router, before the router makes its forwarding (routing) decisionoutbound, after the router makes its forwarding decision and has determined the exit
- interface to use.enable an ACL on an interface that processes the packet, in the direction the packet flows
- - through that interface.the router then processes every inbound or outbound IP packet using that ACL

Taking Action When a Match Occurs

- deny or permit  
    Types of IP ACLs
- - Standard numbered ACLs (1Extended numbered ACLs (100–99) or (1300–199) or (2000-1999)-2699)

Named ACLs

- - Editing with sequence numbersconfiguration identifies the ACL either using a number or a name. ACLs will also be
- either standard or extended  
    Standard Numbered IPv4 ACLs
- - matches only the source IP address identify the ACL using numbers rather than names (numbered)
- Looks at IPv4 packets.  
    List Logic with IP ACLs
- - router takes the action listed in that line of the ACL and stops looking further in the ACLevery IP ACL has a deny all statement implied at the end of the ACL

Matching Logic and Command Syntax

- - ACL is one or more accessany number from the ranges shown in the preceding line of syntax. -list commands with the same number,
- - (One number is no better than the other.) IOS refers to each line in an ACL is an Access Control Entry (ACE
- - engineers just call them ACL statements.each access-list command also lists the action (permit or deny), plus the matching logic.

Matching the Exact IP Address

### 2 Standard ACLs

Friday, September 17, 2021 12:28 PM

Matching the Exact IP Address

- permit if source = 10.1.1.1
    - - accessIf you use Host keyword IOS will remove the keyword in the config-list 1 permit 10.1.1.1
    - access-list 1 permit any

Matching Any/All Addresses

ACL show commands list

- - counters for the number of packets matched by each command in the ACLno counter for that implicit denyany concept at the end of the ACL. , but there is
- Configure deny any command to see deny counts  
    Implementing Standard IP ACLs

# access-list _access-list-number_ {deny | permit} _source_ [source-wildcard]

- Plan the location (router and interface) and direction (in or out) on that interface:
    - placed near to the destination of the packetsdiscard packets that should not be discarded.so that they do not unintentionally
    - identify the source IP addresses of packets as they go in the direction that the ACL is examining.
    - # access-list _access-list-number_ {deny | permit} _source_ [source-wildcard]
        
- Configure one or more access-list
- Enable the ACL
    - _(config-if)# ip access-group number {in | out}_  
        Standard Numbered ACL Example 1  
        R2(config)# accessR2(config)# access--list 1 permit 10.1.1.1list 1 deny 10.1.1.0 0.0.0.255  
        R2(config)# access-list 1 permit 10.0.0.0 0.255.255.255  
        R2(config-if)# ip access-group 1 in

# show ip access-lists

- details about IPv4 ACLs only

# show access-lists

- lists details about any configure ACL, not just IPv4
- lists the number or name of any IP ACL enabled on the interface

# show ip interface s0/0/1

Standard Numbered ACL Example 2

- standard ACLs cannot check the destination IP address.

- - standard ACLs cannot check the destination IP address.extended ACL lets you check both the source and destination IP address.
- - accessrouter checks packets that it routes against the ACL for outbound ACLs- to leave text documentation that stays with the ACL.-list remark parameter
- a router does not filter packets that the router itself creates with an outbound ACL  
    Troubleshooting and Verification Tips
- IOS keeps statistics about the packets matched by each line of an ACL  
    logkeyword  
    ▪ add to end of accessIOS then issues log messages with occasional statistics about matches of that -list command  
    ▪ ACL line
- Double check the ACL is enabled on the right interface, or for the right direction  
    Practice Building access-list Commands  
    Tips to consider when choosing matching parameters to any access-list command:
- - To match a specific address, just list the address.To match any and all addresses, use the any keyword.

several practice problems (wildcard)

- Packets from 172.16.5.4- 0.0.0.0
- Packets from hosts with 192.168.6- 0.0.0.255
- Packets from hosts with 192.168- 0.0.255.255
- Packets from any hosts- 255.255.255.255
- Packets from subnet 10.1.200.0/21- 0.0.7.255
- Packets from subnet 172.20.112.0/23- 0.0.1.255
- Packets from subnet 172.20.112.0/26- 0.0.0.63
- Packets from subnet 192.168.9.64/28- 0.0.0.15
- Packets from subnet 192.168.9.64/30- 0.0.0.3

Reverse Engineering from ACL to Address Range (practice problems)  
1.2. one address192.168.4.0 -192.168.4.127  
3.4. 192.168.6.0 172.30.96.0 --192.168.6. 31172.30.96.255  
5.6. 172.30.96.0 10.1.192.0 --10.1.192..3172.30.96. 63  
7.8. 10.1.192.0 10.1.192.0 --10.1.193.25510.1.255.255

```
128 64 32 16 8 4 2 1
128 192 224 240 248 252 254 255
```

This chapter covers the following exam topics:  
5.0 Security Fundamentals  
5.6 Configure and verify access control lists

- all the parameters must be matched correctly to match that one ACE..  
    Matching the Protocol, Source IP, and Destination IP 9Extended)
- Uses the access-list global command. The
- - syntax is identical up until permit or deny keywordRequires three matching parameters:  
        ○ IP protocol type  
        ○ source IP address  
        ○ destination IP address.
- - identifies the header that follows the IP header (layer 4)TCP, UDP, EIGRP, IGMP, etc
- - Use protocol as keywordKeyword IP means all IPv4 packets

IP header’s Protocol Type field

Syntax

# Access(Destination-list 101 (list #) permit/ Deny tcp (protocol) 10.0.0.1 0.0.0.0 (Source) 10.1.0.1 0.0.0.255

- Requires the use of the host keyword for specific address
- Examples

```
▪ Any IP packet that has a TCP header
```

- access-list 101 deny tcp any any
- access▪ Any IP packet that that has a UDP header-list 101 deny udp any any
- access▪ Any IP packet that has a ICMP header-list 101 deny icmp any any

```
▪ All IP packets from host 1.1.1.1 going to host 2.2.2.2
```

- access-list 101 deny ip host 1.1.1.1 host 2.2.2.2

```
access▪ All IP packets that have a UDP header following the IP header, from subnet 1.1.1.0/24 going to any destination-list 101 deny udp 1.1.1.0 0.0.0.255 any
```

##### -

IP and TCP Header

# 3 Extended ACLs

Friday, September 17, 2021 1:11 PM

IP and TCP Header  
IP Header  
Misc Header Fields▪ 9 bytes

```
▪ 1 byte
▪▪ ie 6 = tcpidentify TCP header
```

```
Protocol
```

```
Header Checksum▪ 2 bytes
```

```
▪ 4 bytes
```

```
Source IP
```

```
Dest. IP▪ 4 bytes
Options▪ variable
TCP Header
Source Port- 2 bytes
```

- 2 bytes

```
Dest. port
```

```
Rest of TCP- 16 bytes
```

tcp or udp keyword

- - can optionally reference the source and/or destination portequal, not equal, less than, greater than, and for a range of port numbers
- can use port numbers or keywords for some well-known application ports  
    positions of the source and destination port fields in the access-list command and these port  
    number keywords.  
    # access-list 101 permit **(protocol)** Source_IP **(source port)** dest_IP **(dest port)**  
    Protocol-- tcpudp  
    - - eq _ne_  
    - lt_

```
Source Port
```

- - lt_gt_
- range_
- - eq _ne_
- - lt_gt_
- range_

```
Dest. Port
```

```
eq: =lt: <
ne: not equal
gt: >range: x to y
ie:
# access-list 101 permit tcp 172.16.1.0 0.0.0.255 172.16.3.0 0.0.0.255 eq 21
```

- eq 21 is in the destination port position  
    Apps and Port number shortcuts for ACL Commands  
    20 21 **ftpftp-data**  
    22 -  
    23 25 **telnetsmtp**  
    53 67 **domainbootps (dhcp server)**  
    68 69 **bootpc (dhcp clienttftp** )  
    80 **www**  
    110 161 **pop3snmp**  
    443 514 - -  
    16,384 -32,767 (RTP/ Voice/ Video) -  
    Extended IP ACL Configuration

- enable the ACL using the sameip access-groupcommand used with standard ACLs.
    - saves some bandwidth.
- Place extended ACLs as close as possible to the source of the packets that will be filtered.
- ACL numbers - 100 – 199 and 2000– 2699

```
(If you were to type eq 80, the config would show eq http://www.)
```

Extended IP Access Lists: Example 1

#(int) ip access-group 101 in

```
Named IP Access Lists
```

- Easier to remember
- - Uses ACL subcommands instead of global config commandsediting features allow deleting individual lines and inserting new ones  
        Config  
        #(ACLmode) permit 1.1.1.1  
        #(ACLmode) permit 2.2.2.2#(ACLmode) permit 3.3.3.3  
        #(ACLmode) deny ip 10.1.2.0 0.0.0.255 10.2.3.0 0.0.0.255

```
# ip access-list (standard/ extended) (name)
```

```
#(int) ip access-group barney out
```

```
#(ACLmode) no deny ip 10.1.2.0 0.0.0.255
```

- deleting a single entry from the ACL.
- delete and add new lines to the ACL from within ACL configuration mode

Named ACLs and ACL Editing

- ACL sequence number is added to each ACL permit or deny statement,
- numbers represent the sequence of statements in the ACLNumbered ACLs can use a configuration style like named ACLs, as well as the traditional
- style, for the same ACL; the new style is required to perform advanced ACL editing.
- Deleting single lines:- delete an ACE with a **no sequence-number** subcommand.  
    New ACEs can be configured with a sequence number before the deny or permit  
    command, dictating the location of the statement within the ACL.
- Inserting new lines: -
- Automatic sequence numbering: - sequence numbers are added to ACEs automatically
    
    # Show ip access- Shows access list 24 and sequence numbers with each entry-lists 24
    
    ```
     - delete entry 20
    ```
    
    #(ACLmode) no 20  
    - - enters this new ace as sequence #5Places the sequence number in the list in order

```
#(ACLmode) 5 deny 10.1.1.1
```

```
although Example 3-6 uses a numbered ACL, named ACLs use the same process to edit (add
and remove) entries.
```

Editing ACLs Using Sequence Numbers (named and numbered (not the global numbered way)

```
numbered ACLs are stored with the original style of configuration, as global access-list commands,
no matter which method is used to configure the ACL.
```

##### -

```
the parts of ACL 24 configured with both new-style commands and old-style commands are all
listed in the same old-style ACL (show running-config).
```

##### -

Numbered ACL Configuration Versus Named ACL Configuration

- Place more specific statements early in the ACL.
    - By doing so, you avoid issues with the ACL during an interim state
- Disable an ACL from its interfacemaking changes to the ACL. (using the **no ip access-group interface** subcommand)before

ACL Implementation Considerations

Mitigating Security Issues with ACLs  
Security threats that can be mitigated with ACLs

- IP address spoofing, inbound
- -IP address spoofing, outboundDoS TCP SYN attacks, blocking external attacks
- Dos TCP SYN attacks, using TCP Intercept
- -DoS smurf attacksDenying/filtering ICMP messages, inbound
- -Denying/filtering ICCMP messages, outboundDenying/filtering Traceroute

```
* Don't allow external packets that have an internal destination address.
Configuring ACLs from the internet
```

- -Deny any source addresses from your internal networks Deny any local host addresses (127.0.0.0/8)
- -Deny any reserved private addresses (RFC 1918)Deny any addresses in the IP multicast address range (224.0.0.0/4)

Controlling VTY (Telnet/ SSH) Access

1. Create a standard IP access list that permits only the host or hosts you want to be able to telnet into the routers.
2. Apply the access list to the VTY line with the access-class in command.  
    (g) # access-list 50 permit host 172.16.10.3  
    (g) # line vty 0 4(int) # access-class 50 in

Monitoring Access Lists

# show access-list

shows access lists, parameters, statistics, etc.

# show access-list 110

Shows info for access list 110

# show ip access-list

shows IP access lists on the router

# show ip interface

Shows which interfaces have access lists set on them.

# show running-config

Shows ACLs and what interfaces that have them.

This chapter covers the following exam topics:  
5.0 Security Fundamentals  
5.1 Define key security concepts (threats, vulnerabilities, exploits, and mitigation techniques)  
5.2 Describe security program elements (user awareness, training, and physical access control)  
5.4 Describe security password policies elements, such as management, complexity, and password  
alternatives (multifactor authentication, certificates, and biometrics)  
5.8 Differentiate authentication, authorization, and accounting concepts

Attacks That Spoof Addresses

- - attacker sends packets with a spoofed source IP addressattacker sends spoofed MAC addresses
- DHCP requests with spoofed MAC addresses can be sent to a DHCP server○ filling its address lease table and leaving no free IP addresses for normal use.

Denial-of-Service Attacks

```
○ no ack replies cause the server to leave open the connection and fill up the table
○ Server is no longer able to do legitimate TCP connections
```

- server adds the TCP connection and replies to the fake address with a SYN-ACK.
- ICMP echo (ping) packets
- flood of UDP packets, and TCP connections, such as the TCP SYN flood
- distributed denial- attack is distributed across a large number of bots, all flooding or attacking the same target.-of-service (DDoS)

Reflection and Amplification Attacks  
Reflection attack

- - Attacker sends packets to the reflector hosthost (reflector) reflects the exchange toward the spoofed address that is the target.
- The attacker might also send the spoofed packets to multiple reflectors, causing the target to receive multiple copies of the unexpected traffic.

```
▪ when reflector (Corporate server) responds, it sends packets to victim
```

- Attackers source packet is the IP of the victim
- attacker sends a small amount of traffic to a reflector to generate large volume of traffic to a target
- leverages a protocol or service to generate the traffic
- mechanisms of DNS and NTP have been exploited for this

```
Amplification attack
```

# 4 Security Architectures

Tuesday, September 21, 2021 2:02 PM

- mechanisms of DNS and NTP have been exploited for this  
    Man-in-the-Middle Attacks
- can exploit the ARP table to communicate with other hosts on the local networkattacker sends the last ARP reply so that any listening host will update its ARP table with the most
- recent information.
- attacker can repeat this process by poisoning the ARP entries on multiple hosts and then relaying traffic between them without easy detection.

Address Spoofing Attack Summary

- Exhaust a system service or resource
- Crash target system

```
DoS/DDoS
```

```
Reflection/ Amplification- Trick unwilling accomplice host to send traffic to target
```

- Eavesdrop on traffic
- Modify traffic passing through

```
man-in-the-middle
```

Reconnaissance Attacks

- discover details about the target and its systems prior to an actual attack.use common tools to uncover public details like who owns a domain and what IP address ranges
- are used there.
- **nslookup** The **whois** can reveal the owner of the domain and the IP address space registered to it. and **dig** commands are complementary tools that can query DNS information to reveal  
    detailed information about domain owners, contact information, mail servers, authoritative name servers, and so on.

##### -

- using ping sweeps to send pings to each IP address in the target range. Hosts that answer the ping sweep then become live targets.  
    Port scanning tools can then sweep through a range of UDP and TCP ports to see if a target host  
    answers on any port numbers. Any replies indicate that a corresponding service is running on the target host.

##### -

- not a true attack because nothing is exploited as a result.  
    Buffer Overflow Attacks  
    incoming data might be stored in unexpected memory locations if a buffer is allowed to fill beyond  
    its limit.

##### -

- sending data that is larger than expected.
- If a vulnerability exists, the target system might store that data, overflowing its buffer into another area of memory, eventually crashing a service or the entire system.  
    attackers specially craft the large message by inserting malicious code in it. - If the target system stores that data as a result of a buffer overflow, then it can potentially run the malicious code without realizing.

##### -

- can spread from one computer to another only through user interaction
- Trojan horse

Malware

- can spread from one computer to another only through user interaction such as opening email attachments, downloading software from the Internet, and inserting  
    a USB drive into a computer.

##### -

- Packaged inside other software  
    can propagate between systems more readily. To spread, into another application, then rely on users to transport the infected application software to virus software must inject itself  
    other victims.

##### -

- Self-injected into other software
- viruses
- Worms- -propagates automatically

Human Vulnerabilities

```
targets a group of similar users who might work for the same company, shop at the same
stores, and so on.
```

##### -

- all receive the same convincing email with a link to a malicious site.  
    Whaling ▪▪ similar to phishing targets high-profile individuals in corporations, governments, and organizations.

##### -

- - voice calls (vishing)SMS text messages (smishing).

```
Spear phishing
```

- - altered DNS service or local hosts file entry for a legitimate site. altered name resolution returns the address of a malicious site instead.  
        Pharming:
- frequently visited site is compromised and malware is deposited there.
- infects only the target users who visit the site

```
Watering Hole:
```

Securing Network Access with Cisco AAA  
Authentication, Authorization, and Accounting  
Authentication

- -Name and passwordChallenge and response
- Token cards  
    Authorization
- Takes place after authentication is validated
- the operation that specific user is allowed to performProvides needed resources specifically allowed to a certain user and permits  
    Accounting
- accessed.Records what the user did on the network as well as the resources they
- Keeps track of how much time they spent using network resources.  
    Authentication Methods  
    Least secure to most secure methods:
- No username or password
- - Username/password (static)Aging username/password
- - OneToken cards/soft tokens-time passwords (OTP

This chapter covers the following exam topics:  
1.0 Network Fundamentals  
1.1 Explain the Role of Network Components  
1.1.c Next-generation Firewalls and IPS  
4.0 IP Services  
4.8 Configure network devices for remote access using SSH  
5.0 Security Fundamentals  
5.3 Configure device access control using local passwords

Encrypting Older IOS Passwords with service password-encryption

```
▪▪ password username passwordname password (console or vty mode) password
▪ enable password password
```

- encrypts passwords that are normally held as clear text
- encoding type of “7”

```
service password-encryption
```

```
no service password - passwords remain encrypted until password is changed - encryption
```

Hashing the enable secret

- never stores the clearIOS computes the MD5 hash of the password in the enable secret command and stores the hash -text password  
    of the password in the configuration.

##### -

- IOS hashes the clear-text password as typed by the user.
- IOS compares the two hashed values
    - Can be used without having to enter the password

```
no enable secret
```

Improved Hashes for Cisco’s Enable Secret  
The two newer alternative algorithm types - Both use an SHA-256 hash instead of MD5

- Type 5
- MD5

```
enable [algorithm-type md5] secret password
```

# 5 Securing Network Devices

Thursday, September 23, 2021 10:32 AM

##### - MD5

- Type 8
- SHA- 256

```
enable algorithm-type sha256 secret password
```

- - Type 9 SHA- 256

```
enable algorithm-type scrypt secret password
```

```
New enable secret commands with different algorithm types replace any existing enable secret
command.
```

##### -

Encoding the Passwords for Local Usernames  
Username secret command Encoding  
**username** _name_ **[algorithm-type md5] secret** _password_  
**username username** _namename_ **algorithmalgorithm--type shatype scrypt secret -256 secret** _passwordpassword_

Controlling Password Attacks with ACLs  
(line vty)# - Bond ACL 3 to a vty line **access-class 3 in**

- looks at the destination IP address instead of the source
- filters based on the device to which the telnet or ssh command is trying to connect.

```
(line vty)# access-class 3 out
```

Traditional Firewalls

- - match the source and destination IP addressesmatching their static well-known TCP and UDP ports
- - additional TCP and UDP portsMatch the text in the URI of an HTTP request
        - storing information about each packetmake decisions about filtering future packets based on the historical state
        - - information (could be tracking the number of TCP connections per secondstateful inspection)
        - recording state information based on earlier packets
- state information (stateful firewall)
- would not have had the historical state information to realize that a DoS attack was occurring.
    - stateless firewall or a router ACL

Security Zones

- Secure
- Zone Inside
- Not secure
- Zone Outside
- DMZ
- defining which hosts can initiate new connections.

- DMZ- Access by public

Intrusion Prevention Systems (IPS

- IPS first IPS can log the event, discard packets, or even redirect the packets to another security application downloads a database of exploit signatures  
    for further examination.

##### -

- needs to download and keep updating its signature database.  
    Cisco Next-Generation Firewalls  
    Cisco firewall- Cisco Adaptive Security Appliance (ASA).  
    comparing fields in the IP, TCP, and UDP headers, and using security zones when defining  
    firewall rules
- stateful filtering-
    - looks at the application layer data to identify the applicationdeep packet inspection
    - can identify many applications based on the data sent application data structures far past the TCP and UDP headers).(application layer headers plus

```
Application Visibility and Control (AVC)
```

```
Duties of a NGFW
Traditional firewall:stateful firewall filtering, NAT/PAT, and VPN termination.
Application Visibility and Control (AVC)
```

- A networktransfers that would install malware, and saving copies of files for later analysis.-based antimalware function can run on the firewall itself, blocking file  
    Advanced Malware Protection:

```
examines the URLs in each web request, categorizes the URLs, and either filters or
rate limits the traffic based on rules. The Cisco Talos security group monitors and creates reputation scores for each domain known in the Internet, with URL filtering
being able to use those scores in its decision to categorize, filter, or rate limit.
```

```
URL Filtering- : This feature
```

##### NGIPS

Cisco Next-Generation IPS

- examines the context by gathering data from all the hosts and the users of those hosts. will know the OS, software revision levels, what apps are running, open ports, the transport
- protocols and port numbers in use, and so on.
- Armed with that data, the NGIPSlog. can make much more intelligent choices about what events to  
    NGIPS Duties

- using exploit signatures to compare packet flows, creating a log of events, and possibly discarding and/or redirecting packets.

Traditional IPS:

Application Visibility and Control (AVC):

```
gather data from hosts—OS, software version/level, patches applied, applications
running, open ports, applications currently sending data, and so on. Those facts inform the NGIPS as to the often more limited vulnerabilities in a portion of the
network so that the NGIPS can focus on actual vulnerabilities while greatly reducing the number of logged events.
```

Contextual Awareness: -

Reputationcan perform reputation-Based Filtering: -based filtering, taking the scores into account.

```
provides an assessment based on impact levels
```

Event Impact Level:

5.0 Security Fundamentals  
5.7 Configure Layer 2 security features (DHCP snooping, dynamic ARP inspection, and port security)

Port Security Concepts and Configuration

- identifies devices based on the source MAC address of Ethernet frames that the devices send.no restrictions on whether the frame came from a local device or was forwarded through other  
    switches

##### -

- examines frames received on the interface to determine if a violation has occurred.
- defines a maximum number of unique source MAC addresses allowed for all frames coming in the interface.
- keeps a list and counter of all unique source MAC addresses on the interface.monitors newly learned MAC addresses, considering those MAC addresses to cause a violation if  
    the newly learned MAC address would push the total number of MAC table entries for the  
    interface past the configured maximum allowed MAC addresses for that port.

##### -

```
takes action to discard frames from the violating MAC addresses, plus other actions depending on
the configured violation mode.
```

##### -

```
Other port security options
```

- Define a maximum of three MAC addresses, defining all three specific MAC addresses.
- Define a maximum of three MAC addresses but allow those addresses to be dynamically learned, allowing the first three MAC addresses learned.
- Define a maximum of three MAC addresses, predefining one specific MAC address, and allowing two more to be dynamically learned.  
    port security learns the MAC addresses off each port so that you do not have to preconfigure the values. It also adds the learned MAC addresses to the port security  
    configuration (in the running-config file).

```
sticky secure MAC addresses.-
```

Configuring Port Security

- works on both access ports and trunk portsrequires you to statically configure the port as a trunk or an access port.
- Use theUse the **switchport mode accessswitchport port-security** or the interface subcommand to enable port security on the **switchport mode trunk** interface subcommands  
    interface.

##### -

- switchport port□ override the default maximum number of allowed MAC addresses associated with the interface (1).-security maximum number
- (Optional)
- override thedefault action to take upon a security violation (shutdown).

```
(Optional) - switchport port-security violation {protect | restrict | shutdown}
```

# 6 Switchport security config

Tuesday, September 28, 2021 2:44 PM

- **switchport port** - predefine any allowed source MAC addresses for this interface. **- security mac-address** _mac-address_

```
(Optional)
```

- tell the switch to “sticky learn” dynamically learned MAC addresses.

```
(Optional)- switchport port-security mac-address sticky
```

```
switchport port - enables port security, with all defaults - security
```

```
defines a specific source MAC address. With the default maximum source address setting of
1
```

```
switchport port - - security mac-address 0200.1111.1111
```

```
default violation action disable the interface.
```

- Port security does not save the configuration of the sticky addresses - use the copy running-config startup-config command if desired.

```
make sure to configure the maximum MAC address to at least two (one for the phone,
or for a PC connected to the phone)
```

- voice ports-
    - the port security configuration should be placed on the portthan the individual physical interfaces in the channel. -channel interface, rather
- EtherChannels

```
voice ports and EtherChannels
```

Verifying Port Security

- provides the most insight to how port security operates
- lists the configuration settings for port security on an interface
    - - Port Security: EnabledPort Status: Secure-shutdown
    - - Violation mode: shutdownMaximum MAC Addresses : 1
    - Last source Address:VLAN: 0013:197b:5004 1
- includes information about any security violations

```
Show port-security interface
```

- - Port Security: EnabledPort Status: Secure-shutdown
- - Violation Mode: ShutdownMaximum MAC Addresses: 1
- Sticky MAC Addresses: 1
- Last Source Address: Vlan 0013:197b:5004 1

```
Show port-security interface fastEthernet 0/2
```

```
secure- the interface has been disabled because of port security-shutdown state
```

Port Security MAC Addresses

```
No longer listed as dynamic entries- Do not show up in the results from show mac address-table dynamic EXEC command.
```

##### -

```
you need to use one of these options to see the MAC table entries associated with ports
using port security:
```

##### -

- Port security ports

```
show mac address - Lists MAC addresses associated with ports that use port security - table secure :
```

```
Lists MAC addresses associated with ports that use port security, as well as any
other statically defined MAC addresses
```

```
show mac address - - table static:
```

```
show mac address-table secure interface F0/2
```

```
(All three options cause the switch to discard the offending frame)
```

- Discard frame

```
Protect
```

- - Discard frameSend log and snmp messages
- increment violation counter

```
Restrict
```

- Discard frame
- - Send log and snmp messagesincrement violation counter
- Puts interface into err-disabled state, discarding all traffic

```
Shutdown
```

Port Security Violation Modes

Shutdown Mode

- interface must be shut down with the shutdown command and then enabled with the no shutdown command.
- recover from an err-disabled state
- automatically recover from the err-disabled state:
- automatic recovery for interfaces in an err-disabled state caused by port security

```
errdisable recovery cause psecure-violation
```

```
errdisable recovery interval - set the time to wait before recovering the interface seconds
```

```
lists the current port-security status (secure-shutdown) as well as the configured mode
(shutdown)
```

##### -

```
last line of output lists the number of violations that caused the interface to fail to an err-
disabled state
```

##### -

```
show port-security interface
```

```
disabled statesecond-to-last line identifies the MAC address and VLAN of the device that caused the
violation.
```

##### -

- notes the number of times the interface has been moved to the errshutdown) state. -disabled (secure-
- while errafter shutdown/no shutdown, another violation that causes the interface to fail to an err-disabled, many frames can arrive, but the counter remains at 1. -  
    disabled state will cause the counter to increment to 2.

##### -

```
violations counter
```

Protect and Restrict Modes  
still discard offending traffic, but the interface remains in a connected (up/up) state and in a port  
security state of secure-up.

##### -

- port continues to forward good traffic but discards offending traffic.
    - - discard the frame.does not change the port to an err-disabled state
    - does not generate messages
    - does not even increment the violations counter

```
protect
```