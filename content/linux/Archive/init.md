---
title: Init
date: 2023-11-06T06:20:36-07:00
draft: true
---
System V Overview (sys v) ("system five")

\- init stops and starts essential processes

\- 3 major versions of init

1\. system V (most traditional version)

2\. upstart

3\. syst

\- Starts and stops processes sequentially

\- uses scripts to start and stop processes

\- Easy to solve dependencies (A comes before B)

\- Con: Only one service stops or starts at a time.

\- State of the machine is defined by runlevels (0-6) (varies by distro)

0: Shutdown

1: Single User Mode

2: multiuser mode without networking

3: multiuser mode with networking

4: unused

5: multiuser mode w/ networking and GUI

6: Reboot

\- systems boots and runs scripts associated with runlevel

\- scripts locations:

/etc/rc.d/rc\[runlevel number\].d/

/etc/init.d

\- Scripts that start with S(start) or K(kill) will run on startup and shutdown

\- numbers next to s or k are the sequence they run in

/etc/rc.d/rc0.d $ ls

k10 updates K80openvpn

\- See what runlevel your machine is booting to

/etc.inittab

\- You can change default runlevel

\- slowly getting replaced

\- runlevels exsist in other distros to support systemv scripts

System V Service

Command tools to manage sysv services (not specific to sysv)

List services

$ service --status-all

Start a service

$ sudo service networking start

Stop a service

$ sudo service networking stop

Restart a service

$ sudo service networking restart

Upstart

developed by canonical (Ubuntu) but Ubuntu uses syst now.

\- Event and job driven model

\- improves on sysv (strict startup processes/ blocking of tasks.

\- To see if your system uses Upstart

/usr/share/upstart (exists)

\- Jobs = actions that upstart performs

\- Events = messages that are received from other processes to trigger jobs

$ ls /etc/init

\- see a list of jobs and their configurations

\- Shows how and when to start jobs

\- How upstart works

\- Loads job config files from /etc/init

\- when startup event occurs, run jobs triggered by it

\- those jobs make new events and those events trigger more jobs

\- Does this until all jobs are complete

Upstart Jobs

\- no easy way to see where an event or job originated

\- will have to look around in /etc/iniit

View Jobs

$ initctl list

\- show jobs and their status

\- format: job goal/status

\- Will change as jobs start/ stop

View specific jobs

$ initctl status networking

Manually start a job

$ sudo initctl start networking

Manually stop a job

$ sudo initctl stop networking

Manually restart a job

$ sudo initctl restart networking

Manually emit an event

$ sudo initctl omit some_event

Syst

\- Emerging standard for init

\- To tell if your system uses syst

/use/lib/syst (exists)

\- Uses goals to get system up and running

\- targets to acheive with dependancies needed for those targets

\- does not follow strict sequence

How syst boots

1\. loads config files located in /etc/syst/ system or /usr/lib/syst/system

2\. Determines boot goal (usually default.target)

3\. Finds out dependencies of boot target and activates them

\- boots into different targets (like run levels)

poweroff.target

-shutdown

rescue.target

-single user mode

multi-user.target

-multiuser with networking

graphical.target

-multiuser with networking and GUI

reboot.target

-restart

default.target

\- usually points to graphical.target

Units

\- the main object for syst

\- can also mount filesystems, monitor network sockets, etc.

different types of units

Service Units

\- end in .service

\- The ones that are starting and stopping

Mount Units

\- Mount filesystems

\- end in .mount

Target units

\- group together other units (which all get activated)

\- end in .target

Syst goals

Unit file/ how to control units

service unit

\[unit\]

(description/ when to activate)

\[service\]

(start/stop/reload service)

\[install\]

(used for dependencies)

Syst commands

List units

$ systemctllist-units

View status of unit

$ systemctl ststua networking.service

start a service

$ sudo systemctl start networking.service

stop a service

$ sudo systemctl stop networking.service

restart a service

$ sudo systemctl.restart networking.service

Enable a unit

$ sudo systemctl enable networking.service

Disable a unit

$ sudo systemctl disable networking.service

Power States

Shutdown system

$ sudo shutdown -h now

\- power off

Shutdown and specify the time

$ sudo shutdown -n +2

\- can be in minutes

Restart

$ sudo shutdown -r now

Reboot

$ sudo reboot
