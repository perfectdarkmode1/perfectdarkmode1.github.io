---
title: Network Troubleshooting
date: 2023-11-06T06:20:36-07:00
draft: true
---
ICMP

\- type, code, and checksum fields

Type 0 - Echo Reply

Type 3 - Destination unreachable (16 values)

Type 8 - Echo Request

Type 11 - Time exceded

Ping

$ ping -c 3 [www.google.com](http://www.google.com)

\- count 3 times

Traceroute

$traceroute

Netstat

\- displays network connections, routing tables, int info, etc.

socket (ip and port)

\- interface that allows programs to send and receive data

Port

\- used to identify which application should send or receive data

$ netstat -at

-a shows listening and non-listening sockets for network connections

-t shows only tcp connections

output

proto: tcp or udp

recv-q: Data qued to be received

send-q: data qeued to be sent

Local address: locally connected host

foreign address: remotely connected host

state: state of the socket

Socket states (some)

LISTENING: listening for incoming connections

SYN_SENT: actively trying to establish a connection

ESTABLISHED: established connection

CLOSE_WAIT: remote host has shutdown, waiting for socket to close

TIME_WAIT: waiting after cloase to handle packets still in the network

Packet analysis

$ sudo apt install tcpdump

capture packet data on an interface

$ sudo tcpdump -i wlan0

output

\- timestamp

\- ip-protocol info

\- source/dest address

\- seq tcp starting and ending seq number

\- length in bytes

Writing tcpdump output to a file

$ sudo tcpdump -w /somefile
