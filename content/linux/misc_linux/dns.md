---
title: DNS
date: 2023-11-06T06:20:36-07:00
draft: true
---
DNS Components

Name server

\- authoritive or recursive

Zone file

\- how the name server stores info about domain and how to get there

Resource records

\- located in zone file

record name

TTL - time in which the record is discarded

class - Namespace of record info, usually IN for internet

type - type of info stored (A, MX, etc.)

Data - can contain IP address or other info depending on type

DNS Process

Local DNS Server (ISP)

\- asks root server if unknown

Root servers

\- 13 root servers for the internet

\- contain info about top level domains (.org .com .net etc.)

Top level domain

\- can give ip of server that record is located on

Authoritive DNS server

\- final DNS server with info we want (if no others have)

/etc/hosts

\- contains host/ip mappings

\- local host listed as default

\- manage access to hosts (modify firewall rules instead)

\- /etc/hosts.deny

\- /etc/hosts.allow

/etc/resolv.conf

\- DNS name server mappings (often irrelevant)

DNS setup (popular DNS servers)

BIND

\- standard for Linux distros

\- full featured power and flexibility

DNSmasq

\- lightweight and easy to configure

\- DHCP & DNS

\- for small networks

Power DNS

\- full featured

\- most flexibilty & options

DNS tools

nslookup

$ nslookup [www.google.com](http://www.google.com)

\- query name servers to find info on resource records

dig (domain information grouper)

\- gather info about DNS name servers

$ dig [www.google.com](http://www.google.com)

\- gives more info than nslookup
