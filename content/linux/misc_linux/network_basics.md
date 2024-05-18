---
title: Networking in Linux
date: 2023-11-06T06:20:36-07:00
draft: true
---
fing install: fing.com/products/development-toolkit

used to scan network for ip addresses

view routing table

$ sudo route -n

ug: Network is up & gateway is up

u: Network is up

Network config

create an interface and bring it up

$ ifconfig eth0 192.168.2.1 netmask 255.255.255.0 up

bring an interface up or down

$ ifup eth0

$ ifdown eth0

IP command

\- Manipulate network stack of system

show info for all interfaces

$ iplink show

show statistics for an interface

$ ip -s link show eth0

show ip addresses allocated to interfaces

$ ip address show

Bring interfaces up and down

$ ip link set eth0 up/down

Add ip address to an interface

$ ip address add 192.168.1.1/24 dev eth0

Route

(route commands)

add new route

$sudo route add -net 192.168.2.1/23 gw 10.11.12.3

remove a route

sudo route del -net 192.168.2.1/23

(ip commands)

add a route

$ ip route add 192.168.2.1/23 via 10.11.12.3

delete a route

$ ip route delete 192.168.2.1/23

DHCLIENT

\- dhclient starts on boot >

\- gets a list of network interfaces from dhclient.conf file

\- tries to configure each interface using dhcp

\- Keeps track of leases across system reboots

\- dhclient.conf is read

\- dhclient.leases is read to see what leases are assigned

Obtain a fresh ip

$ sudo dhclient

Network manager (Daemon)

\- configures networks automatically

\- applet software in gui

command line tools to interact with network manager

nmtool

\- reports Network managers state and it's devices

$ nm-tool

$ nmcli

\- control and modify network manager

arp

$ arp

\- view arp cache

$ ip neighbor show

\- view arp cache
