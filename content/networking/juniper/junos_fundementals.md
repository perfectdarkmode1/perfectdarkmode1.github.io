---
title: "Junos Basics"
date: 2023-11-06T06:20:36-07:00
draft: true
---

Routing engine = Control Plane

-   OSPF
-   BGP
-   Telenet session

Daemons

-   RPD
    
-   Most important Protocol
    
-   Routing Protocol Daemon
    
-   Works with all routing protocols
    
-   Inet.0
    
-   Routing tables
    
-   MG-D
    
-   DCD
    
-   ChassisD
    
-   VRRPD/ SNMPD
    

Packet forwarding Engine = Forwarding Plane

-   Traffic
-   Line cards (forwarding tables)
-   Switch fabric

# Junos Software architecture

One daemon crashing in the Routing Engine will not crash other Daemons
