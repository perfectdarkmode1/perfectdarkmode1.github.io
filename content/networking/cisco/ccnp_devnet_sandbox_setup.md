Max reservation time: 4 hours

Sandbox user reserves the CML Sandbox and receives software VPN access information and credentials via email at the start of the reservation. (For more information, see the next tab called "VPN Access".) Once connected via software VPN the developer can access the Sandbox's resources with the details below.

AFTER you've established a VPN connection:

Cisco Modeling Labs Server

Address: 10.10.20.161

Username: developer

Password: C1sco12345

HTTPS Port for CML GUI/API: 443

Example Connection: [https://10.10.20.161](https://10.10.20.161 "https://10.10.20.161")

SSH Port for Console Connections: 22

Simulated Hosts and Network Devices

By default CML nodes will use credentials of cisco cisco

For detailed addressing and credential details for the sample simulation, please see the Network Devices tab

Devbox

SSH Port: 22

RDP Port: 3389

Establishing a VPN connection

download and install Cisco's AnyConnect VPN Client software

[https://developer.cisco.com/site/sandbox/anyconnect/](https://developer.cisco.com/site/sandbox/anyconnect/ "https://developer.cisco.com/site/sandbox/anyconnect/")

Install guide

[https://devnetsandbox.cisco.com/Docs/VPN_Access/AnyConnect_Installation_Guide.pdf](https://devnetsandbox.cisco.com/Docs/VPN_Access/AnyConnect_Installation_Guide.pdf "https://devnetsandbox.cisco.com/Docs/VPN_Access/AnyConnect_Installation_Guide.pdf")



![Pasted image 20230120133647.png](Pasted%20image%2020230120133647.png)
When your Lab reservation begins, you will receive several emails communicating important information about the status of your Lab.

The first email is sent to you from the Lab provisioning automation engine, and indicates that resources in your Lab are in the process of being provisioned and tested. Your Lab is NOT READY yet, but this email will give an estimate of when your Lab will be available.

The second email will be sent to you when your Lab is fully provisioned, tested and READY for you to connect. In this email you'll find the information required by AnyConnect to establish a VPN connection to your Lab (Network IP Address, VPN Username, VPN Password).

How to connect to vpn

[https://devnetsandbox.cisco.com/Docs/VPN_Access/AnyConnect_Connection_Guide.pdf](https://devnetsandbox.cisco.com/Docs/VPN_Access/AnyConnect_Connection_Guide.pdf "https://devnetsandbox.cisco.com/Docs/VPN_Access/AnyConnect_Connection_Guide.pdf")

Click reserve

You will get an email saying that the setup will last about 10 minutes

Follow email instructions to connect to the vpn

then go to the ip address in the setup guide 10.10.20.161

here is their sample network

![Pasted image 20230120133730.png](Pasted%20image%2020230120133730.png)

Linux install

![Pasted image 20230120133747.png](Pasted%20image%2020230120133747.png)

To get to a switch console:

-   select the switch
-   select consol
-   Enable password is cisco
-   Default user is cisco

Credentials for sample lab devices

![Pasted image 20230120133835.png](Pasted%20image%2020230120133835.png)

Component

Type

IP Address

Method

Credentials

internet-host01

Linux

10.10.20.182

SSH

cisco / cisco

internet-rtr01

IOS XE

10.10.20.181

TELNET

cisco / cisco

edge-firewall01

ASA

10.10.20.171

TELNET

cisco / cisco

edge-sw01

IOS

10.10.20.172

TELNET

cisco / cisco

core-rtr01

IOS XR

10.10.20.173

TELNET

cisco / cisco

core-rtr02

IOS XR

10.10.20.174

TELNET

cisco / cisco

dist-rtr01

IOS XE

10.10.20.175

TELNET

cisco / cisco

dist-rtr02

IOS XE

10.10.20.176

TELNET

cisco / cisco

dist-sw01

NX-OS

10.10.20.177

TELNET

cisco / cisco

dist-sw02

NX-OS

10.10.20.178

TELNET

cisco / cisco

inside-host01

Linux

10.10.20.179

SSH

cisco / cisco

inside-host02

Linux

10.10.20.180

VNC

cisco / cisco
