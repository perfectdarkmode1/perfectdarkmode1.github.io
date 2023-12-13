# Chapter 16 RHCSA Notes - Networking

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











