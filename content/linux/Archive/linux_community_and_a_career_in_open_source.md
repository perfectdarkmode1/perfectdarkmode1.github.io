---
title: Open source and Linux Community
date: 2023-11-06T06:20:36-07:00
draft: true
---
Distributions

Debian

\- dpkg

\- GNU/Linux

\- Ubuntu

\- Rasbian

Major Open source apllications

software packages

Debian, Ubuntu, Linux mint

\- dpkg, apt-get, and apt package managers

\- deb packages

RedHat, Fedora, Centos

\- rpm, yum, and dnf package managers

\- rpm packages

Dependencies = auxiliary packages needed by programs

Individual package files operate on .dpkg and .rpm

Catalogues (works with)

\- apt get, apt, yum, dnf

\- download new packages and their dependencies

$ apt-cache search package-name

$ apt search package_name

\- used to search for apps

\- Installation and removal of packages requires admin

$ apt-get install package name

$ apt install package_name

\- two ways to install package in Debian systems

$ apt-get purge cups

\- uninstall program and config files

$ figlet Awesome

\- picture text program

RPM

$ yum search package_name

$ dnp

\- you can use descriptive terms to find programs by function

$ yum search speaking cow (finds cowsay)

$ cowsay “Linux is fun”

Uninstall a package (remove keyword) (sudo)

$ apt-get remove package_name

$ apt remove package_name

$ yum remove package_name

$ dnf remove package_name

\- config files of removed programs are kept in the system

Office Applications

Apache Open Office and Libre Office

\- compatible with microsoft office doc types

\- ODF (open Document Format)

\- fully open and iso standardized

\- ensure documents can be transferred betwen operating systems & applications from different vendors

Main applications

\- writer

\- Calc (spreadsheets)

\- Impress (presentations)

\- Draw (vector drawing)

\- Math (math formulas)

\- Base (database

Web Browsers

Google Chrome & Firefox

Multimedia

Blender (3d rendering)

GIMP (photoshop)

Inkscape (vector graphics editor)

Audacity (audio editor)

Imagemagick (cli image filetype converter

VLC & smplayer (video playback)

Server Programs

HTTP Servers

\- Apache

\- Nginx

\- Lighttpd

PHP scripting languages

\- server side code

Javascript

\- client side

Popular open source relational databases

\- MariaDB

\- PostgreSQL

Data Sharing

NFS (Network File System)

\- standard way to share filesystems in Linux-only environment

\- read/write

\- share operating systems for thin clients

Samba

\- data sharing in a mixed environment

\- share files and printers

\- associate

Linux systems to a domain controller or SSSD (an authentication subsystem)

Owncloud & Nextcloud (fork)

\- fork = when one app is a spinoff of another

Features

\- filesharing and sync

\- collaborative workspaces

\- calendar, contacts, and mail

Nextcloud

\- private audio/ video confrencing

\- both offer paid versions

\- can install on private server for free

\- must be installed on a configured web server

Network Administrat:cowboy: ion

DNS & DHCP

Programming Languages

\- source code - human readable text file that describes what the program is doing

\- compiled languages - source code is converted to a binary file that can be executed by the computer

\- Compiler - program that converts source code to executable form

\- interpereted languages- interpereter reads source code and executes it's instructions

Java Script

\- used for web pages

C (compiled)

\- closely related with operating systems

Java (compiled)

\- portable to other operating systems

Perl

\- process text content (filtering & parsing)

Shell

\- automate complex or repetitive tasks

Python

\- easy to use

PHP

\- server side web

\- dynamic content

LAMP server

Linux OS/ Apache HTTPserver, My SQL, PHP

Open Source Software and licensing

(skipped for now)

ICT Skills and working in Linux

Open source Hypervisor

\- xen, kvm, and virtualbox

Privacy issues when using the internet

\- almost all actions done in a browser are tracked & analyzed by various parties

Cookie Tracking

\- data sold to ad networks

\- like & share buttons are also tracked

\- can use a cookie manager addon to control cookies better

DNT (do not track)

\- setting that tells companies that they do not want to be tracked

\- they do not have to honor this setting

“private windows”

\- ctrl + shift + p in firefox

\- new browser with no config is opened

\- personal data is not stored (history, passwords, cookies)

\- Leave no trace on computer used

\- good for accessing personal websites on public computers

Password manager

\- keepass

\- oepn source

\- they won't make use of your data

\- Bitwarden

\- open source

\- cloud

\- can host your own bitwarden server

\- use a random password for every password

Encryption

TLS (transport layer security)

\- succesor of SSL

\- provides privacy & authenticity using symmetric and public key cryptography

\- used with HTTPS

File and email encryption with GnuPG (Gnu Privacy guard)

\- open source

\- sign, encrypt, and decrypt text, emails, files, directories, and disk partitions

\- public key for encrypting

\- private key for decrypting

Disk Encryption

\- encrypt whole disk or partition

\- two basic methods

\- stacked

\- block

Stacked

\- implemented on top of existing filesystem

\- stored encrypted

Block

\- Happens below filesystem layer

\- makes sure everything written to a block device is encrypted

\- metadata, directory structure and permissions are also encrypted

Dm-crypt

\- standard for block encryption for Linux

\- native in the kernel

\- can be used with LUKS (Linux Unified Key Setup) extension

\- implements a platform-independent standard for use with various tools

EncFs

Stackable method

Veracrypt

\- multiplatform support
