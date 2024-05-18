---
title: Process Utilization
date: 2023-11-06T06:20:36-07:00
draft: true
---
Tracking Processes: top

\- realtime view of system utilization

1st line

\- current time - system uptime - # of users logged in - load average

2nd line

\- tasks running, sleeping, stopped, or zombied

3rd line

\- us: user cpu time spent running non-niced user processes

\- sy: system cpu time running kernel/ kernel processes

\- ni: nice cpu time spent running niced processes

\- id: cpu idle time %

\- wa: i/o wait, if low, problem is probably not disk or network i/o

\- hi: hardware interrupts/ % of cpu time

\- si: software interrupts/ % of cpu time

\- st: steal time that vms use

4th and 5th lines = memory + swap usage

Processes List that are currently in use

PID: ID of Process

USER: Owner of process

PR: Priority

NI: nice value

VIRT: virtual memory used by process

RES: Physical memory used

SHR: shared memory

S: status: s=sleep r=running z=zombie D=uninterruptible T=stopped

%cpu: How much cpu this process is using

%MEM: Ram used

TIME+: time (total) of activity

COMMAND: name of the process

Specify process to drack by PID

$ top -p 1

isof and fuser

\- view files in use

ISOF

$ isof

\- shows processes that are holding a device/ file open

fuser

\- shows info about process that is using a file

$ fuser -v .

\- shows current directory

Process Threads

\- used to execute the same program as processes

\- use isolated system resources

\- Threads can share resources easily

\- multithreaded applications may be better than multi-process

$ ps m

\- view process threads

\- underneath PID is thread

cpu monitoring

$ uptime

\- load average feild

\- see cpu load on your system

\- 1, 5, and 15 minute intervals

\- load = average number of processes waiting to be executed by cpu

$ cat /proc/cpuinfo

\- take into account # of cores when looking at load

Show disk usage on a specific directory:
```
du -sch /var/www/nextcloud/data/david/files/Games/battlenet/*
```
