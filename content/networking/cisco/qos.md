---
title: QoS
date: 2023-11-06T06:20:36-07:00
draft: false
---

4.0 IP Services

4.7 Explain the forwarding per-hop behavior (PHB) for QoS such as classification, marking, queuing, congestion, policing, shaping

QoS defines these actions as per-hop behaviors (PHBs), which is a formal term to refer to actions other than storing and forwarding a message.

## QoS: Managing Bandwidth, Delay, Jitter, and Loss

four characteristics of network traffic:

Bandwidth

refers to the speed of a link, in bits per second (bps)

helps to also think of bandwidth as the capacity of the link, in terms of how many bits can be sent over the link per second.

Delay

the time between sending one packet and that same packet arriving at the destination host

Round-trip delay

the time it takes to send one packet between two hosts and receive one back

Jitter

variation in one-way delay between consecutive packets sent by the same application

Loss

the number of lost messages, usually as a percentage of packets sent.

people think of loss as something caused by faulty cabling or poor WAN services. That is one cause. However, more loss happens because of the normal operation of the networking devices, in which the devices’ queues get too full, so the device has nowhere to put new packets, and it discards the packet.

Types of Traffic

Data Applications

HTTP GET 
500 Packets 
Figure 11-1 Concept of Disproportionate Packet/Byte Volumes with HTTP Traffic ">

Quality of Experience (QoE) \- users’ perception of their use of the application on the network.

Voice and Video Applications

A flow is all the data moving from one application to another over the network, with one flow for each direction

For example, if you open a website and connect to a web server, the web page content that moves from the server to the client is one flow.

From a voice perspective, a phone call between two IP phones would create a flow for each direction

Step 1. The phone user makes a phone call and begins speaking.

Step 2. A chip called a codec processes (digitizes) the sound to create a binary code (160 bytes with the G.711 codec, for example) for a certain time period (usually 20 ms).

Step 3. The phone places the data into an IP packet.

Step 4. The phone sends the packet to the destination IP phone.

CODEC 
Voice Bytes 
IP UDP ATP Voice Bytes 
Figure 11-2 Creating VolP Packets with an IP Phone and a G.711 Codec ">

guidelines for interactive voice:

Delay (one-way): 150 ms or less

Jitter: 30 ms or less

Loss: 1% or less

requirements for video

Bandwidth: 384 Kbps to 20+ Mbps

Delay (one-way): 200–400 ms

Jitter: 30–50 ms

Loss: 0.1%–1%

QoS as Mentioned in This Book

“Classification and Marking” is about the marking of packets and the definition of trust boundaries.

“Queuing” describes the scheduling of packets to give one type of packet priority over another.

“Shaping and Policing” explains these two tools together because they are often used on opposite ends of a link.

“Congestion Avoidance” addresses how to manage the packet loss that occurs when network devices get too busy.

Classification and Marking

a type of QoS tool that classifies packets based on their header contents then marks the message by changing some bits in specific header fields

Classification Basics

QoS tools sit in the path that packets take when being forwarded through a router or switch, much like the positioning of ACLs. Like ACLs, QoS tools are enabled on an interface. Also like ACLs, QoS tools are enabled for a direction: packets entering the interface (before the forwarding decision) or for messages exiting the interface (after the forwarding decision).

classification refers to the process of matching the fields in a message to make a choice to take some QoS action

QoS tools perform classification (matching of header fields) to decide which packets to take certain QoS actions against. Those actions include the other types of QoS tools discussed in this chapter, such as queuing, shaping, policing, and so on.

Forward 
RI 
Classify 
Queue 
Scheduling 
(Prioritization) 
Transmit 
Figure 11-3 Big Idea: Classification for Queuing in a Router ">

Matching (Classification) Basics

Cisco and by RFCs, suggests doing complex matching early in the life of a packet and then marking the packet. Marking means that the QoS tool changes one or more header fields, setting a value in the header.

Differentiated Services Code Point (DSCP)

a 6-bit field in the IP header meant for QoS marking

Mark DSCP 
at Ingress 
SWI 
Less Complex Matching 
DSCP=X? CLASS 1. 
DSCP=Y? CLASS 2. 
WAN 
SW2 
F igure 11-4 Systematic Classification and Markingfor the Enterprise ">

Classification on Routers with ACLs and NBAR

many QoS tools support the ability to simply refer to an IP ACL, with this kind of logic:

For any packet matched by the ACL with a permit action, consider that packet a match for QoS, so do a particular QoS action.

All these fields are matchable for QoS classification.

IP Header 
4 
TCP Header 
9 
Miscellaneous 
Header 
Fields 
4 
Variable 
2 
2 
16+ 
Rest 
Protocol Header 
6 (TCP) Checksum 
6 = TCP 
Source IP Destination IP 
Address Address 
Source Dest. 
Options 
of 
Port Port 
TCP 
Figure 11-5 Classification with Five Fields Used by Extended ACLs ">

not every classification can be easily made by matching with an ACL. In more challenging cases, Cisco Network Based Application Recognition (NBAR) can be used. NBAR is basically in its second major version, called NBAR2, or next-generation NBAR. In short, NBAR2 matches packets for classification in a large variety of ways that are very useful for QoS.

NBAR2 looks far beyond what an ACL can examine in a message

Cisco also organizes what NBAR can match in ways that make it easy to separate the traffic into different classes.

you might classify WebEx traffic and give it a unique DSCP marking. NBAR provides easy built-in matching ability for WebEx, plus more than 1000 different subcategories of applications.

NBAR refers to this idea of defining the characteristics of different applications as application signatures.)

Rl#(config)# class-map matchingexample 
RI (config-cmap)# match protocol attribute category voice-and-video ? 
! output heavily edited for length 
amazon-instant-video 
cisco-ip-camera 
cisco-phone 
espn-video 
facetime 
! Output snipped. 
VOD service by Amazon 
Cisco video surveillance camera 
Cisco IP Phones and PC-based Unified Com 
ESPN related websites and mobile applica 
Facetime video calling software ">

Marking IP DSCP and Ethernet CoS

example plan

Classify all voice payload traffic that is used for business purposes as IP DSCP EF and CoS 5.

Classify all video conferencing and other interactive video for business purposes as IP DSCP AF41 and CoS 4.

Classify all business-critical data application traffic as IP DSCP AF21 and CoS 2

Marking the IP Header

Marking a QoS field in the IP header works well with QoS because the IP header exists for the entire trip from the source host to the destination host.

IPv4 defines a Type of Service (ToS) byte in the IPv4 header, as shown in Figure 11-6. The original RFC defined a 3-bit IP Precedence (IPP) field for QoS marking. That field gave us eight separate values—binary 000, 001, 010, and so on, through 111—which when converted to decimal are decimals 0 through 7.

IPP 
Type of 
Service 
DSCP 
RFC 2474 
Unused 
ECN 
Old Use 
IP Header 
(Rest of IP Header...) 
Current Use 
RFC 3168 
Figure 11-6 IP Precedence and Differentiated Services Code Point Fields ">

Those last 5 bits of the ToS byte per RFC 791 were mostly defined for some purpose but were not used in practice to any significant extent.

DSCP increased the number of marking bits to 6 bits, allowing for 64 unique values that can be marked. The DiffServ RFCs, which became RFCs back in the late 1990s, have become accepted as the most common method to use when doing QoS, and using the DSCP field for marking has become quite common.

IPv6 has a similar field to mark as well. The 6-bit field also goes by the name DSCP, with the byte in the IPv6 header being called the IPv6 Traffic Class byte.

Marking the Ethernet 802.1Q Header

marking field exists in the 802.1Q header

It goes by two different names: Class of Service, or CoS, and Priority Code Point, or PCP.

sits in the third byte of the 4-byte 802.1Q header, as a 3-bit field, supplying eight possible values to mark (see Figure 11-7). It goes by two different names: Class of Service, or CoS, and Priority Code Point, or PCP.

Ethernet 
8021 Q 
Type 
Data 
Trailer 
Class of Service (COS) (3 Bits) 
Priority Code Point (PCP) 
Figure 11-7 Class ofService Field in 802.1Q/p Header ">

802.1Q header is not included in all Ethernet frames

only exists when 802.1Q trunking is used on a link

only for QoS features enabled on interfaces that use trunking, as shown

WAN 
SWI 
Trunk 
SW2 
can Use COS 
Figure 11-8 Useful Life of COS Marking ">

Other Marking Fields

Field Name 
DSCP 
IPP 
cos 
TID 
EXP 
Header(s) 
IPv4, IPv6 
IPv4, IPv6 
802.1Q 
802.11 
MPLS Label 
Length (bits) 
6 
3 
3 
3 
3 
Where Used 
End-to-end packet 
End-to-end packet 
Over VLAN trunk 
over Wi-Fi 
over MPLS WAN ">

Defining Trust Boundaries

most voice traffic is marked with a DSCP called Expedited Forwarding (EF), which has a decimal value of 46

trust boundary

the point in the path of a packet flowing through the network at which the networking devices can trust the current QoS markings

Set DSCP and 
COS Inbound 
SWI 
Trust Boundary 
WAN 
SW2 
Figure 11-9 Trusting Devices—PC ">

when the access layer includes an IP Phone, the phone is typically the trust boundary

IP Phones can set the CoS and DSCP fields of the messages created by the phone, as well as those forwarded from the PC through the phone. The specific marking values are actually configured on the attached access switch

Set Phone DSCP and COS 
SWI 
Trust Boundary 
WAN 
SW2 
Figure 11-10 Trusting Devices—IP Phone ">

DiffServ Suggested Marking Values

DiffServ architecture as defined originally by RFC 2475

three sets of DSCP values as used in DiffServ.

Expedited Forwarding (EF)

Expedited Forwarding (EF) DSCP value—a single value

use for packets that need low latency (delay), low jitter, and low loss.

decimal 46

Most often QoS plans use EF to mark voice payload packets. With voice calls, some packets carry voice payload, and other packets carry call signaling messages. Call signaling messages set up (create) the voice call between two devices, and they do not require low delay, jitter, and loss.

By default, Cisco IP Phones mark voice pay-load with EF, and mark voice signaling packets sent by the phone with another value called CS3.

Assured Forwarding (AF)

The Assured Forwarding (AF) DiffServ RFC (2597) defines a set of 12 DSCP values meant to be used in concert with each other

defines the concept of four separate queues in a queuing system. Additionally, it defines three levels of drop priority within each queue for use with congestion avoidance tools. With four queues, and three drop priority classes per queue, you need 12 different DSCP markings, one for each combination of queue and drop priority. (Queuing and congestion avoidance mechanisms are discussed later in this chapter.)

The text names follow a format of AFXY, with X referring to the queue (1 through 4) and Y referring to the drop priority (1 through 3).

Best Queue 
Worst Queue 
AF41 
(34) 
AF31 
(26) 
AF21 
(18) 
AFII 
(10) 
AF42 
(36) 
AF32 
(28) 
AF22 
(20) 
AF12 
(12) 
AF43 
(38) 
AF33 
(30) 
AF23 
(22) 
AF13 
14) 
11-11 Differentiated Services Assured Forwarding Values and Meaning ">

Class Selector (CS)

eight DSCP values for backward compatibility with IPP values.

The DSCP values have the same first 3 bits as the IPP field, and with binary 0s for the last 3 bits, as shown on the left side of the figure. CSx represents the text names, where x is the matching IPP value (0 through 7).

o 
1 
2 
3 
4 
5 
6 
7 
CSO 
CSI 
CS2 
CS3 
CS4 
CS5 
CS6 
CS7 
Decimal 
DSCP 
16 
24 
32 
40 
56 
Figure 11-12 Class Selector ">

Guidelines for DSCP Marking Values

how all devices should mark data

DSCP EF: Voice payload

AF4x: Interactive video (for example, videoconferencing)

AF3x: Streaming video

AF2x: High priority (low latency) data

CS0: Standard data

Queuing

the QoS toolset for managing the queues that hold packets while they wait their turn to exit an interface

Router Internals 
ingress 
services 
Output Queue 
Forwarding 
Transmit 
Figure 11-13 Output Queuing in a Router: Last Output Action Before Transmission ">

To use multiple queues, the queuing system needs a classifier function to choose which packets are placed into which queue

The queuing system needs a scheduler as well, to decide which message to take next when the interface becomes available

Queues 
Scheduler 
Transmit 
Figure 11-14 Queuing Components ">

Prioritization refers to the concept of giving priority to one queue over another

Round-Robin Scheduling (Prioritization) (Two Types)

weighting

the scheduler takes a different number of packets (or bytes) from each queue, giving more preference to one queue over another.

Class-Based Weighted Fair Queuing (CBWFQ)

Each class receives at least the amount of bandwidth configured during times of congestion, but maybe more

Queues 
02 
03 
Scheduler 
20% 
30% 
50% 
Round Robin 
Transmit 
Figure 11-15 CBWFQ Round-Robin Scheduling ">

Low Latency Queuing

Bandwidth/call 
30-320 Kbps 
One-way Delay (max) Jitter (max) 
Loss (max) 
150 ms 
30 ms ">

Queues 
data 2 
default 
Scheduler 
50% 
10% 
Round Robin 
Transmit 
Figure 11-16 Round Robin Not Goodfor Voice Delay (Latency) and Jitter ">

tells the scheduler to treat one or more queues as special priority queues

Scheduler 
LLQ 
voice 
data 1 
data 2 
default 
—Always Next 
Transmit 
Round Robin 
Figure 11-17 LLQ Always Schedules Voice Packet Next ">

if the speed of the interface is X bits per second, but more than X bits per second come into the voice queue? The scheduler never services the other queues (called queue starvation).

limit the amount of traffic placed into the priority queue, using a feature called policing

a cap on the bandwidth used by the priority queue

Call Admission Control (CAC) tools

Find a way to limit the amount of voice and video that the network routes out this link, so that the policer never discards any of the traffic

CAC tools did not get a mention in the exam topics, so this chapter leaves those tools at a brief mention

A Prioritization Strategy for Data, Voice, and Video

approach queuing in their QoS plans:

Key Topic.

Use a round-robin queuing method like CBWFQ for data classes and for noninteractive voice and video.

If faced with too little bandwidth compared to the typical amount of traffic, give data classes that support business-critical applications much more guaranteed bandwidth than is given to less important data classes.

Use a priority queue with LLQ scheduling for interactive voice and video, to achieve low delay, jitter, and loss.

Put voice in a separate queue from video so that the policing function applies separately to each.

Define enough bandwidth for each priority queue so that the built-in policer should not discard any messages from the priority queues.

Use Call Admission Control (CAC) tools to avoid adding too much voice or video to the network, which would trigger the policer function.

# Shaping and Policing

not found in as many locations in a typical enterprise

often used at the WAN edge in an enterprise network design.

monitor the bit rate of the combined messages that flow through a device.

notes each packet that passes and measures the number of bits per second over time

attempt to keep the bit rate at or below the configured speed

policers discard packets, and shapers hold packets in queues to delay the packets.

Does this next packet push the measured rate past the configured shaping rate or policing rate?

If no:

Let the packet keep moving through the normal path and do nothing extra to the packet.

If yes:

If shaping, delay the message by queuing it.

If policing, either discard the message or mark it differently.

policing, which discards or re-marks messages that exceed the policing rate, followed by shaping, which slows down messages that exceed the shaping rate.

## Policing

Traffic Rate 
Outgoing Measured 
Traffic Rate 
Burst 
Policing 
Rate 
Figure 11-18 Effect ofa Policer and Shaper on an Offered Traffic Load ">

Policers allow for a burst beyond the policing rate for a short time, after a period of low activity.

Where to Use Policing

Policing makes sense only in certain cases, and as a general tool, it can be best used at the edge between two networks.

200 Mb s CIR 
sw 
Police to 
200 Mbps 
GO/2 
GO/2 
sw 
Police to 
200 Mbps 
Figure 11-19 Ethernet WAN: Link Speed Versus CIR ">

a 200-Mbps committed information rate (CIR).

the SP providing the WAN service agrees to allow the enterprise to send 200 Mbps of traffic in each direction. However, remember that the enterprise routers transmit the data at the speed of the access link, or 1 Gbps in this case.

The SP can police incoming packets, setting the policing rate to match the CIR that the customer chooses for that link.

Policers can also re-mark packets.

SP could mark the messages with a new marking value, with this strategy:

Re-mark packets that exceed the policing rate, but let them into the SP’s network.

If other SP network devices are experiencing congestion when they process the packet, the different marking means that device can discard the packet. However…

…if no other SP network devices are experiencing congestion when forwarding that re-marked packet, it gets through the SP network anyway.

SP can treat their customers a little better by discarding less traffic, while still protecting the SP’s network during times of stress.

key features of policing:

Key Topic.

It measures the traffic rate over time for comparison to the configured policing rate.

It allows for a burst of data after a period of inactivity.

It is enabled on an interface, in either direction, but typically at ingress.

It can discard excess messages but can also re-mark the message so that it is a candidate for more aggressive discard later in its journey.

## Shaping

Use a shaper to slow down the traffic

shaping before sending data to an SP that is policing—is one of the typical uses of a shaper

slows messages down by queuing the messages.

then services the shaping queues, but not based on when the physical interface is available

schedules messages from the shaping queues based on the shaping rate

the shaper queues packets so that the sending rate through the shaper does not exceed the shaping rate; and then output queuing works as normal, if needed.

Forwarding 
Shaper 
LLQ 
At 
Shape 
Rate 
Output 
Queuing 
Transmit 
Figure 11-20 Shaping Queues: Scheduling with LLQ and CBWFQ ">

apply the round-robin and priority queuing features of CBWFQ and LLQ, respectively, to the shaping queues

### Setting a Good Shaping Time Interval for Voice and Video

you can (and should) configure a shaper’s setting that changes the internal operation of the shaper, which then reduces the delay and jitter caused to voice and video traffic.

A shaper’s time interval refers to its internal logic and how a shaper averages, over time, sending at a particular rate

Because the interface transmits bits at 1 Gbps, it takes just .2 seconds, or 200 ms, to send all 200 million bits. Then the shaper must wait for the rest of the time interval, another 800 ms, before beginning the next time interval.

Send: 
200 ms 
200 
Million 
Bits 
Sent 
wait: 800 ms 
1 Second Тле lnterval 
Send: 
200 ms 
200 
Million 
wait: 800 ms 
Bits 
Sent 
Т: 1 sec 
Т: 2 sec 
Figure 11-21 Опе Second (1000 ms) Shaping Time Intewal, Shaping at 20 Percent ofLine Rate ">

configure a short time interval so there is less wait time

Tc = 1 second (1000 ms): Send at 1 Gbps for 200 ms, rest for 800 ms

Tc = .1 second (100 ms): Send at 1 Gbps for 20 ms, rest for 80 ms

Tc = .01 second (10 ms): Send at 1 Gbps for 2 ms, rest for 8 ms

When shaping, use a short time interval. By recommendation, use a 10-ms time interval to support voice and video.

key features of shapers:

Key Topic.

Shapers measure the traffic rate over time for comparison to the configured shaping rate.

Shapers allow for bursting after a period of inactivity.

Shapers are enabled on an interface for egress (outgoing packets).

Shapers slow down packets by queuing them and over time releasing them from the queue at the shaping rate.

Shapers use queuing tools to create and schedule the shaping queues, which is very important for the same reasons discussed for output queuing.

## Congestion Avoidance

attempts to reduce overall packet loss by preemptively discarding some packets used in TCP connections

TCP Windowing Basics

tail drop

one queue being totally full. Any new packets that arrive for that queue right now will be dropped because there is no room at the tail of the queue (tail drop).

@Medium Congestion 
Tail Drop 
Much Congestion 
Tail Drop 
Figure 11-22 Tail Drop Concepts with Three Different Scenarios ">

Congestion Avoidance Tools

discard some TCP segments before the queues fill, hoping that enough TCP connections will slow down, reducing congestion, and avoiding tail drop

monitor the average queue depth over time, triggering more severe actions the deeper the queue

the queue depth passes the maximum threshold, the tool drops all packets, in an action called full drop.

congestion avoidance tools can classify messages to treat some packets better than others

Maximum Threshold 
% Drops 
Minimum Threshold 
NO Drops 
Queue Empty 
Figure 11-23 Mechanisms ofCongestion Avoidance ">
