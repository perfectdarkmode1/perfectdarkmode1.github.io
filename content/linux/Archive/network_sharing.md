---
title: Sharing Resources
date: 2023-11-06T06:20:36-07:00
draft: true
---
file sharing

scp (secure copy)

\- uses ssh to copy files to a host on the network

$ scp myfile.txt username@remotehost.com:/remote/directory

\- copy file to remote host from local host

$ scp username@remotehost.com:/remote/directory/file.txt /local/directory

\- copy file to local host from remote host

$ scp -r mydir username@remotehost.com: /remote/directory

\- copy directory to remote host from local host

rsync

\- can check for data before copying and only copy differences

\- similar to scp

\- verify file integrity with checksums

\- ideal for backups and large data transfers

rsync options (some)

v - verbose output

r - recursive into directories

h - human readable output

z - compressed for easier transfer (for slow connections)

$ rsync -zvr /dir1 dir/2

\- copy/sync files on same host

$ rsync /localdir user@host:/remotedir

\- from remote to local

$ rsync user@host.com:/dir1 /localdir

\- copy/sync from local to remote

Simple HTTP Server

\- create a quick network share

\- go to directory you want to share and run:

$ python3 -m http.server 8000

NFS (Network File System)

\- allows server to share directories and files w/ clients(s) over the network

setting up NFS clients

$ sudo service nfsclient start

$ sudo mount server:/directory /mount_directory

Automounting (automount tool)

\-  in new Linux versions

\- when file is accessed in a specified directory automount will look up the remote server and automatically mount it

Samba

Common Internet File System (CIFS)

\- optimized form of SMB

Samba

\- what we call the linux utilities to work with CIFS

\- Can share files and resources like printers

Create a network share w/ Samba (that windows can access)

Install Samba

$ sudo apt update

$ sudo apt install samba

setup smb.conf

\- config [file:/etc/samba/smb.conf](file://etc/samba/smb.conf)

\- tells system what directories to share, permissions, etc.

\- can use commented code to write your config

$ sudo vi /etc/samba/smb.conf

Set up a password

$ sudo smb passwd -a \[username\]

Create a shared directory

$ mkdir /my/directory/to/share

restart the samba service

$ sudo service smbd restart

Accessing the samba share in windows

type in the network connection in the run prompts

[\\\HOST\\sharename](file://HOST/sharename)

Accessing Samba\\windows share in Linux

$ smbclient //HOST/directory -u user

smbclient (tool)

\- used to access windows or Samba server

Attach a samba share to your system

$ sudo mount -t cifs servername:directory mountpointpoint-o user=username, pass=password
