Chapter 1. Introduction to TCP/IP Transport and Applications

This chapter covers the following exam topics:

1.0 Network Fundamentals

1.5 Compare TCP to UDP

4.0 IP Services

4.3 Explain the role of DHCP and DNS in the network

TCP/IP Layer 4 Protocols: TCP and UDP

- TCP provides retransmission (error recovery) and
- TCP helps to avoid congestion (flow control),
- UDP needs fewer bytes in its header (less overhead)
- UDP software does not slow down data transfer
- TCP can purposefully slow down data transfer
- Voice over IP (VoIP) and video over IP, do not need error recovery, so they use UDP

UDP Supports:

- Multiplexing using ports

TCP Supports:

- Multiplexing using ports
- Error recovery (reliability)

- numbering and acknowledging data with sequence and acknowledgment header fields

- Flow control using windowing

- use window sizes to protect buffer space

- Connection establishment and termination

- initialize port numbers and sequence and acknowledgment fields

- Ordered data transfer and segmentation

Transmission Control Protocol

- TCP header is 20 bytes (without options)

- source port/ destination port
- Sequence Number
- Acknowledgement Number
- Offset, Reserved, Flag bits, Window
- Checksum, Urgent

*TCP segment, Layer 4 PDU, or L4PDU

Multiplexing

example

All open on one computer:

Port 80 Web Server

Port 800 Ad Server

Port 9876 Wire Application

Socket

- Includes IP address, transport protocol, and port number

- (10.1.1.2, TCP, port 80)

Well Known (System) Ports:

- 0 to 1023

User (Registered) Ports:

- 1024 to 49151

Ephemeral (Dynamic, Private) Ports:

- 49152 to 65535,
- not assigned

- Servers use well-known ports (or user ports), whereas clients use dynamic ports

- uses the same port number for all connections. For example,
- web server with 100 clients would have only one socket (one port number)
- server looks at source port of received TCP segments.

Popular TCP/IP Applications

Simple Network Management Protocol (SNMP)

- query, compile, store, and display information about a network’s operation
- Cisco Prime software

FTP/ TFTP

- FTP allows many more features
- TFTPis very simple, good tools for embedded parts of networking devices.

SMTP/ POP3

- Simple Mail Transfer Protocol (SMTP) and Post Office Protocol version 3 (POP3)
- both used for transferring mail (TCP).

Port numbers and protocols

- FTP Data TCP 20
- FTP Control TCP 21
- SSH TCP 22
- Telnet TCP 23
- SMTP TCP 25
- DNS UDP/TCP 53
- DHCP Server UDP 67
- DHCP Client UDP 68
- TFTP UDP 69
- HTTP TCP 80
- POP2 TCP 110
- SNMP UDP 161
- SSL TCP 443
- Syslog UDP 514

Connection Establishment and Termination

TCP connection establishment (3 way handshake) occurs 1st

- SYN, DPORT=80, SPORT=49145
- SYN ACK , DPORT= 49145, SPORT=80
- ACK DPORT=80, SPORT=49145

- initializing Sequence and Acknowledgment fields
- agreeing on the port numbers
- 2 bits inside the flag fields of the TCP header. Called the SYN and ACK flags

TCP connection termination. (four-way)

\- uses an additional flag, called the FIN bit

- ACK, FIN >
- < ACK
- ACK, FIN <
- < ACK

Error Recovery and Reliability

- reliability in both directions
- Sequence Number field of one direction and Acknowledgment field in the other direction

- 1000 bytes, Seq = 1000 >
- 1000 bytes, Seq = 2000 >
- 1000 bytes, Seq = 3000 >
- < no data, ACK = 4000

- received all data with sequence numbers up through one less than 4000
- ready to receive your byte 4000 next.

- ack by listing the next expected byte (forward acknowledgment)
- sequence number field identifies the data (sender)
- forward acknowledgments acknowledge the data (receiver)
- Sequence and Acknowledgment fields let the receiving host can notice lost data

- ask the sending host to resend
- acknowledge that the re-sent data arrived

- 1000 bytes, SEQ 1000 >
- 1000 bytes, SEQ 2000 X >
- 1000 bytes, SEQ 3000 >
- < no data, ACK = 2000

- (received 1000 - 1999 and 3000 - 3999, asking for 2000)

- 1000 bytes, SEQ 2000 >
- < no data, ACK 4000

- Retransmission timer

- Sender may wait a few moments to make sure no other acknowledgments arrive

Flow Control Using Windowing

Sliding window (dynamic window

- Receiver slides the window size up and down

- < ACK=1000, Window=3000
- SEQ=1000, SEQ=2000, SEQ=3000 >
- < ACK=4000, Window=4000

User Datagram Protocol

- connectionless
- no reliability,
- no windowing,
- no reordering of the received data, and
- no segmentation of large chunks of data into the right size for transmission
- provides data transfer and multiplexing using port numbers
- Less overhead and processing than TCP.
- no reordering or recovery
- DNS requests use UDP, user will retry an operation if the DNS resolution fails
- Network File System (NFS), a remote file system application, performs recovery with application layer code, so UDP features are acceptable to NFS.
- 8 byte header

- Source port, Destination Port
- Length, Checksum

TCP/IP Applications

Uniform Resource Identifiers (URI)

- clicking a link and typing a URI—refer to a URI
- referred to as web address or  Universal (uniform) Resource Locator \[URL\]
- three key components

- before the :// identifies the protocol
- between the // and / identifies the server by name
- after the / identifies the web page.

- http:// (Scheme)
- [www.certskills.com](http://www.certskills.com) (Authority)
- /blog (path)

DNS

- < Name Resolution Request (IP Header, UDP Header, DNS Request)
- Name resolution Reply (Ip Header, UDP Header, DNS Request (IP address) >
- < TCP connection to requested web server

- DNS requests can be cached by hosts and servers
- Local DNS may need to ask for help
- The enterprise DNS acts as a recursive DNS server

- Sends repeated DNS messages to find the authoritative DNS server.

- Recursive DNS lookup

- host > Enterprise DNS >

- Root DNS
- .com TLD DNS
- Authoritative cisco.com DNS

Transferring Files with HTTP

- HTTP GET request lists file it needs
- HTTP GET response from server with a return code of 200 (meaning OK) and file’s contents.
- Server may issue a return code of 404, (file not found)
- Web pages consist of multiple files, called objects
- Objects are stored as different files on the web server
- Web browser gets the first file which can include references to other URIs that the browser also requests

- < HTTP GET /go/ccna
- HTTP OK data >
- < HTTP GET /graphics/logo1.gif
- HTTP OK data >
- < HTTP GET /graphics/ad1.gif
- HTTP OK data >

- Flow over one or more TCP connection between the client and the server.

Identifying the Correct Receiving Application

- tracks which port opened which request

Fields that identify next header

< Ethernet (Type) (0x0800)

< IPv4 (Protocol) (6)

< TCP (Destination port) (49124)
